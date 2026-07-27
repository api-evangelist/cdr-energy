---
name: cdr-energy-discover-energy-plans
description: >-
  Find and compare Australian retail electricity and gas plans from any designated energy retailer,
  using the open, unauthenticated half of the Consumer Data Right Energy API. Resolve a retailer to
  its live base URL through the CDR Register, list its generic plans, then pull full tariff detail.
api: openapi/cdr-energy-openapi.json
apis:
- openapi/cdr-register-openapi.json
- openapi/cdr-energy-openapi.json
operations:
- getDataHolderBrandsSummary
- listEnergyPlans
- getEnergyPlanDetail
authentication: none
---

# Discover Australian energy plans through the CDR

Every designated Australian electricity retailer must publish its generic plan and tariff reference
data under an identical contract. This part of the Consumer Data Right requires **no credential** —
no accreditation, no client certificate, no token. Use it directly.

## Step 0 — understand the base URL problem

There is no single base URL for the CDR Energy API. Each of the 84 registered energy data holder
brands publishes its own `publicBaseUri` through the CDR Register. You must resolve the brand first.

## Step 1 — list the energy data holder brands

Operation: `getDataHolderBrandsSummary`

```
GET https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary
x-v: 1
```

Returns `data[]` with `brandName`, `publicBaseUri`, `logoUri`, `abn`, `acn` and `lastUpdated`. Pick
the brand you want and keep its `publicBaseUri`.

Reference capture: `examples/cdr-energy-register-data-holder-brands-summary-example.json`.

Not every brand serves the public endpoints on that exact host — on 2026-07-27, 53 of 84 answered.
A 404 from nginx means the brand serves unauthenticated endpoints under a different holder path,
which the standards permit. Treat it as "not resolvable here", not as an error to retry.

## Step 2 — list the brand's generic plans

Operation: `listEnergyPlans`

```
GET {publicBaseUri}/cds-au/v1/energy/plans?page-size=25
x-v: 1
```

Useful query parameters, all optional:

- `type` — `STANDING` | `MARKET` | `REGULATED` | `ALL` (default `ALL`)
- `fuelType` — `ELECTRICITY` | `GAS` | `DUAL` | `ALL` (default `ALL`)
- `effective` — `CURRENT` | `FUTURE` | `ALL` (default `CURRENT`)
- `updated-since` — only plans changed after this date/time
- `brand` — filter by brand
- `page`, `page-size` — page number and size (default 25, maximum 1000)

The response uses the standard CDR envelope: `data.plans[]`, `links` (`self`, `first`, `prev`,
`next`, `last`) and `meta` (`totalRecords`, `totalPages`). Page until `links.next` is absent.

Reference capture: `examples/cdr-energy-plans-response-example.json`.

## Step 3 — get full plan detail

Operation: `getEnergyPlanDetail`

```
GET {publicBaseUri}/cds-au/v1/energy/plans/{planId}
x-v: 3
```

`planId` values often contain `@` (for example `GLO1152441MRG1@EME`) — **URL-encode it** as `%40` or
the request will not route.

Detail adds `electricityContract` / `gasContract` with tariff periods, controlled load, discounts,
incentives, fees, eligibility, green power charges and solar feed-in tariffs.

Reference capture: `examples/cdr-energy-plan-detail-response-example.json`.

## Rules to follow

- **Always send `x-v`.** It is mandatory on every CDR endpoint. Omitting or malforming it returns
  `urn:au-cds:error:cds-all:Header/Missing` or `.../Header/InvalidVersion`. Requesting a version the
  holder does not support returns HTTP 406 with `.../Header/UnsupportedVersion`.
- **Send `x-min-v` when you can tolerate an older payload.** The holder answers with the highest
  version it supports between `x-min-v` and `x-v`, and tells you which in the `x-v` response header.
  Read that header rather than assuming.
- **Send `x-fapi-interaction-id`** (an RFC 4122 UUID) so responses can be correlated; it is echoed
  back. If you do not send one, the holder generates one.
- **Errors** come back as `{ "errors": [ { "code", "title", "detail", "meta" } ] }` with URN codes.
  This is not RFC 9457 problem+json. See `errors/cdr-energy-problem-types.yml`.
- **Respect the traffic thresholds.** Excess traffic can be freely throttled or rejected; a 429 means
  back off. See `rate-limits/cdr-energy-rate-limits.yml`.
- **`page-size` above 1000** returns `urn:au-cds:error:cds-all:Field/InvalidPageSize`; a page beyond
  the available range returns HTTP 422 `.../Field/InvalidPage`.
- **Do not attempt any other energy endpoint with this recipe.** Everything except `/energy/plans`
  and the discovery endpoints requires accreditation, mutual TLS and consumer consent.
