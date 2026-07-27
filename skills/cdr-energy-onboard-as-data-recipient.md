---
name: cdr-energy-onboard-as-data-recipient
description: >-
  The real onboarding path for consumer energy data under the Australian Consumer Data Right - ACCC
  accreditation, CDR Register client credentials, a Software Statement Assertion, and Dynamic Client
  Registration with each data holder over mutual TLS. Use this to understand what access actually
  costs before writing integration code.
api: openapi/cdr-dcr-openapi.json
apis:
- openapi/cdr-register-openapi.json
- openapi/cdr-dcr-openapi.json
- openapi/cdr-energy-openapi.json
operations:
- getRegisterOpenIdProviderConfig
- getRegisterJwks
- getSoftwareStatementAssertion
- postClientRegistration
- getClientRegistration
- putClientRegistration
- deleteClientRegistration
authentication: mutual TLS + private_key_jwt + consumer consent
---

# Onboard as a CDR accredited data recipient (energy)

There is no developer portal that issues an API key. Access to Australian consumers' energy data is
gated on statutory accreditation. This skill describes the real path so an agent does not waste
effort looking for a signup form.

## Step 0 — accreditation (out of band, months not minutes)

Apply to the **ACCC** for accreditation as a CDR Data Recipient, then register a software product on
the CDR Register. The Register issues the PKI client certificates used for mutual TLS. Nothing below
is reachable without this.

Consumer-facing obligations attach at the same time: CDR Privacy Safeguards 1-13, consent that is
explicit, scoped, time-bounded and revocable, and deletion/de-identification duties on revocation.

## Step 1 — read the Register's OpenID Provider metadata

Operation: `getRegisterOpenIdProviderConfig`

```
GET https://api.cdr.gov.au/idp/.well-known/openid-configuration
```

Unauthenticated. Captured verbatim at
`well-known/cdr-energy-register-openid-configuration.json`. Live values:

- `issuer`: `https://api.cdr.gov.au/idp`
- `token_endpoint`: `https://secure.api.cdr.gov.au/idp/connect/token`
- `grant_types_supported`: `client_credentials`
- `token_endpoint_auth_methods_supported`: `private_key_jwt`
- `token_endpoint_auth_signing_alg_values_supported`: `PS256`, `ES256`
- `scopes_supported`: `cdr-register:read`
- `tls_client_certificate_bound_access_tokens`: `true`

Operation: `getRegisterJwks` — `GET https://api.cdr.gov.au/cdr-register/v1/jwks`. Captured at
`well-known/cdr-energy-register-jwks.json`. Use it to verify Register-signed artefacts.

## Step 2 — get a Register access token

`client_credentials` grant at the token endpoint, authenticated with `private_key_jwt` (assertion
signed PS256 or ES256), over mutual TLS. Scope `cdr-register:read`. The token is bound to your client
certificate.

## Step 3 — fetch your Software Statement Assertion

Operation: `getSoftwareStatementAssertion`

```
GET https://api.cdr.gov.au/cdr-register/v1/{industry}/data-recipients/brands/{dataRecipientBrandId}/software-products/{softwareProductId}/ssa
```

The SSA is a signed JWT attesting your accreditation. Required claims include `iss`, `iat`, `exp`,
`jti`, `org_id`, `org_name`, `client_name`, `client_description`, `client_uri`, `redirect_uris`,
`logo_uri`, `jwks_uri`, `revocation_uri`, `recipient_base_uri`, `software_id`, `software_roles` and
`scope`.

Failure modes: HTTP 403 `urn:au-cds:error:cds-register:Field/InvalidBrand`, HTTP 404
`.../Field/InvalidSoftwareProduct`, HTTP 404 `.../Field/InvalidIndustry`, HTTP 422 on SSA validation
failure.

## Step 4 — register with each data holder

Operation: `postClientRegistration`

```
POST {dataHolderMtlsBase}/cds-au/v1/register
```

Present the SSA. This is Dynamic Client Registration (RFC 7591) over mutual TLS — there is no human
approval step at the data holder. There are 84 registered energy brands; you register with each one
you want to collect from.

Manage the registration with `getClientRegistration`, `putClientRegistration` and
`deleteClientRegistration` on `/register/{ClientId}` (RFC 7592).

## Step 5 — obtain consumer consent

Per data holder, using the FAPI 1.0 Advanced Authorization Code Flow:

- Pushed Authorisation Request (RFC 9126) — data holders set `require_pushed_authorization_requests`.
- PKCE with `code_challenge_method` `S256`.
- Request object signed PS256 or ES256.
- `private_key_jwt` client authentication at the token endpoint.
- Access and refresh tokens are mutual-TLS sender-constrained; refresh token `exp` equals the sharing
  duration the consumer authorised.
- The OIDC Hybrid Flow was retired on 12 May 2025 — use Authorization Code Flow only.

Request only the scopes you need. Consent is presented to the consumer in standardised data cluster
and permission language, not raw scope strings. The energy scopes are in
`scopes/cdr-energy-scopes.yml`.

## Step 6 — honour revocation

Expose the `revocation_uri` you declared in your SSA. The data holder will POST a signed
`cdr_arrangement_jwt` to it when the consumer withdraws consent, and you must stop collecting. You
may also revoke from your side at the holder's `cdr_arrangement_revocation_endpoint`. See
`asyncapi/cdr-energy-webhooks.yml`.

Related errors: `urn:au-cds:error:cds-all:Authorisation/RevokedConsent`,
`.../Authorisation/InvalidConsent`, `.../Authorisation/InvalidArrangement`,
`.../Authorisation/AdrStatusNotActive`.

## Before you build

Develop against the free ACCC-hosted sandbox at <https://cdrsandbox.gov.au/> and the open-source mock
participants, and validate against the published conformance test cases. See
`sandbox/cdr-energy-sandbox.yml`.

If all you need is plan and tariff reference data, **you do not need any of this** — use
`cdr-energy-discover-energy-plans` instead.
