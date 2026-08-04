# Consumer Data Right (Energy) (cdr-energy)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Consumer Data Right (CDR) is Australia's statutory consumer data-sharing regime, created under Part IVD of the Competition and Consumer Act 2010 and extended from banking into electricity by the Consumer Data Right (Energy Sector) Designation 2020. It is run by three bodies: the ACCC as lead regulator and operator of the CDR Register, the OAIC as privacy regulator, and the Treasury Data Standards Body, which writes the binding Consumer Data Standards. In energy the regime obliges electricity retailers to expose plans, accounts, billing, invoices, payment schedules, concessions, service points, interval usage and DER data through one identical, versioned API contract, with AEMO acting as the Secondary Data Holder gateway for NMI standing data, metering data and the DER register. Unlike almost every other energy-sector data mandate, this one is verifiably implemented rather than merely announced: the public CDR Register listed 84 energy data holder brands with live public base URIs when probed on 2026-07-27, and 53 of those base URIs returned standards-conformant product data anonymously on the first request. Its API posture is a clean two-speed split — genuinely open, unauthenticated market data (retail plan and tariff reference data, plus the participant register itself) sitting alongside consumer data that is closed behind ACCC accreditation, mutual TLS, FAPI-grade OAuth 2.0 / OpenID Connect and explicit, revocable consumer consent. Home market Australia.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cdr-energy/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cdr-energy/refs/heads/main/apis.yml)

## Tags

- Energy
- Australia
- Utilities
- Electricity
- Consumer Data Right
- Open Energy
- Smart Metering
- DER
- Energy Markets
- Regulation
- Government
- Open Data

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### CDR Register API

The ACCC-operated Consumer Data Right Register, the ecosystem's source of truth for who is allowed to participate. Unauthenticated endpoints return the energy data holder brand summary (84 brands with their live public base URIs), data holder statuses, accredited data recipients and software product statuses; they were all served anonymously over the open internet on 2026-07-27 with only an x-v version header. Authenticated endpoints issue Software Statement Assertions to accredited data recipients using mutual TLS and private_key_jwt client credentials against the Register's own OpenID Provider.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#cdr-register-api-schemas](https://consumerdatastandardsaustralia.github.io/standards/#cdr-register-api-schemas)
- **Base URL:** `https://api.cdr.gov.au/cdr-register/v1`

#### Tags

- Register
- Discovery
- Accreditation
- Government

#### Properties

- [OpenAPI](openapi/cdr-register-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-register-api-schemas)
- [Documentation](https://cdr-register.github.io/register/)
- [Authentication](https://api.cdr.gov.au/idp/.well-known/openid-configuration)
- [GitHub Repository](https://github.com/ConsumerDataStandardsAustralia/register)

### CDR Energy API

The mandated energy data contract that every designated Australian electricity retailer must implement identically. Eighteen paths covering generic plan reference data, electricity service points, interval usage, distributed energy resources, accounts, balances, invoices, billing, payment schedules and concessions. The two `/energy/plans` endpoints are public product reference data and require no authentication; every other endpoint requires an accredited data recipient, mutual TLS and a consumer-authorised OAuth 2.0 / OpenID Connect token. There is no single base URL — each of the 84 registered energy data holder brands publishes its own base URI through the CDR Register, and 53 of them answered `GET /cds-au/v1/energy/plans` anonymously when probed on 2026-07-27.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-api-schemas](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-api-schemas)

#### Tags

- Energy
- Electricity
- Usage
- Billing
- DER
- Consumer Data Right

#### Properties

- [OpenAPI](openapi/cdr-energy-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-api-schemas)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)
- [Documentation](https://dsb.gov.au/consumer-data-right/data-standards)
- [Sandbox](https://github.com/ConsumerDataStandardsAustralia/mock-data-holder-java)
- [Conformance](https://github.com/ConsumerDataStandardsAustralia/standards-testing)
- [GitHub Repository](https://github.com/ConsumerDataStandardsAustralia/standards)

### CDR Energy Secondary Data Holder API

The gateway contract AEMO implements as the CDR Secondary Data Holder for energy. Retailers are the primary data holders for the customer relationship, but the physical data — NMI standing data, meter and interval usage records, and the distributed energy resources register — lives with AEMO, so the standards define a separate six-operation server-to-server API that retailers call on the consumer's behalf. This is the piece of machinery that has no banking equivalent, and it is why energy needed a shared-responsibility model rather than a straight copy of the banking contract.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-secondary-data-holder-api-schemas](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-secondary-data-holder-api-schemas)

#### Tags

- Energy
- AEMO
- Metering
- DER
- Gateway

#### Properties

- [OpenAPI](openapi/cdr-energy-sdh-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-secondary-data-holder-api-schemas)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)

### CDR Common API

The cross-sector endpoints every CDR data holder must expose regardless of industry — `GET /common/customer` and `/common/customer/detail` for the consented customer's identity, and the unauthenticated `/discovery/status` and `/discovery/outages` endpoints that let the ecosystem see whether a data holder is up and when it plans to be down. The discovery pair is a rare example of a regulator mandating a public status API.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#cdr-common-api-schemas](https://consumerdatastandardsaustralia.github.io/standards/#cdr-common-api-schemas)

#### Tags

- Common
- Customer
- Status
- Discovery

#### Properties

- [OpenAPI](openapi/cdr-common-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-common-api-schemas)

### CDR Dynamic Client Registration API

The onboarding contract. Rather than a developer portal issuing keys, an accredited data recipient presents a Software Statement Assertion obtained from the CDR Register and self-registers with each data holder over mutual TLS, then manages or deletes that registration. This is how a developer actually "gets keys" in the CDR — machine-to-machine, gated on accreditation, with no human approval step at the data holder.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#cdr-dynamic-client-registration-api-schemas](https://consumerdatastandardsaustralia.github.io/standards/#cdr-dynamic-client-registration-api-schemas)

#### Tags

- Onboarding
- Registration
- OAuth
- Accreditation

#### Properties

- [OpenAPI](openapi/cdr-dcr-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-dynamic-client-registration-api-schemas)

### CDR Admin API

The mandated reporting surface every data holder must expose to the ACCC — `GET /admin/metrics` returns availability, performance, invocation, error and rejection statistics, and `POST /admin/register/metadata` forces a metadata refresh. A regulator that requires the industry to publish its own operational telemetry through an API is unusual, and it is the mechanism that makes CDR compliance measurable rather than self-declared.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#cdr-admin-api-schemas](https://consumerdatastandardsaustralia.github.io/standards/#cdr-admin-api-schemas)

#### Tags

- Admin
- Metrics
- Reporting
- Compliance

#### Properties

- [OpenAPI](openapi/cdr-admin-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-admin-api-schemas)

## Common Properties

- [Website](https://www.cdr.gov.au/)
- [Developer Portal](https://consumerdatastandardsaustralia.github.io/standards/)
- [Documentation](https://dsb.gov.au/consumer-data-right/data-standards)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-api-schemas)
- [Authentication](https://api.cdr.gov.au/idp/.well-known/openid-configuration)
- [Security](https://consumerdatastandardsaustralia.github.io/infosec/)
- [GitHub Organization](https://github.com/ConsumerDataStandardsAustralia)
- [GitHub Repository](https://github.com/ConsumerDataStandardsAustralia/standards)
- [Sandbox](https://github.com/ConsumerDataStandardsAustralia/mock-register)
- [Conformance](https://github.com/ConsumerDataStandardsAustralia/standards-testing)
- [Support](https://github.com/ConsumerDataStandardsAustralia/standards-maintenance)
- [Blog](https://dsb.gov.au/news-and-announcements)

## Mandate Posture

| Field | Value |
| --- | --- |
| Mandate regime | `cdr-energy` |
| Mandate status | `live-implemented` — verified anonymously, not claimed |
| Data standard | CDR Consumer Data Standards (Energy) v1.36.0 |
| Consumer data API | Yes — 18 mandated paths, gated by consent + accreditation |
| Open market data | Yes — public CDR Register and unauthenticated retail plan/tariff data |
| Access gate | `accredited-only` for consumer data; open for market data |
| Auth model | mTLS + OAuth 2.0/OIDC (CDR InfoSec profile), private_key_jwt, DCR via SSA |
| Home market | Australia |

Evidence, probe log and HTTP statuses are recorded in [review.yml](review.yml).

## Maintainers

- **Kin Lane** — kin@apievangelist.com
