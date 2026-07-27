---
name: cdr-energy-monitor-ecosystem-health
description: >-
  Monitor the availability of the Australian Consumer Data Right energy ecosystem using only
  unauthenticated endpoints - the CDR Register's participant status endpoints and the status and
  outage endpoints every data holder is mandated to expose.
api: openapi/cdr-common-openapi.json
apis:
- openapi/cdr-register-openapi.json
- openapi/cdr-common-openapi.json
operations:
- getDataHolderBrandsSummary
- getDataHolderStatuses
- getDataRecipientsStatuses
- getSoftwareProductsStatuses
- getStatus
- getOutages
authentication: none
---

# Monitor CDR energy ecosystem health

The CDR is one of the few regimes where a regulator mandates a **public status API**. Every data
holder must expose machine-readable status and planned outages, and the CDR Register publishes its
own view of every participant's status. All of it is unauthenticated.

## Step 1 — the register's view of every data holder

Operation: `getDataHolderStatuses`

```
GET https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/status
x-v: 2
```

This is the ecosystem-wide answer: which energy data holders the ACCC currently considers active.

Companion operations for the other side of the market:

- `getDataRecipientsStatuses` — `GET /cdr-register/v1/{industry}/data-recipients/status`
- `getSoftwareProductsStatuses` — `GET /cdr-register/v1/{industry}/data-recipients/brands/software-products/status`
- `getDataRecipients` — `GET /cdr-register/v1/{industry}/data-recipients`

These endpoints support `If-None-Match` with the `Etag` response header, so poll them conditionally
and handle HTTP 304 Not Modified rather than re-downloading.

## Step 2 — resolve brands to hosts

Operation: `getDataHolderBrandsSummary`

```
GET https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary
x-v: 1
```

Take `publicBaseUri` from each brand.

## Step 3 — ask each data holder directly

Operation: `getStatus`

```
GET {publicBaseUri}/cds-au/v1/discovery/status
x-v: 1
```

Returns `data.status` and `data.updateTime`. Verified live: a registered brand returned
`{"data":{"status":"OK","updateTime":"..."}}` on 2026-07-27
(`examples/cdr-energy-discovery-status-response-example.json`).

Operation: `getOutages`

```
GET {publicBaseUri}/cds-au/v1/discovery/outages
x-v: 1
```

Returns `data.outages[]` — the holder's scheduled and current outages. Planned outages must be
published to data recipients with at least one week of lead time for normal changes, so this is a
forward-looking feed, not just a current-state check.

## What "healthy" means here

These are the published obligations you are measuring against:

- **Availability: 99.5% per month**, for data holders and secondary data holders, on both
  authenticated and unauthenticated endpoints. Planned outages are excluded.
- **Performance: 95% of calls per hour** within the tier threshold — 1500ms unauthenticated, 1000ms
  high priority, 4000ms unattended, 6000ms large payload.
- Unavailability means any endpoint in the standard cannot reliably return a successful response to a
  correctly formed request.

Full detail in `lifecycle/cdr-energy-lifecycle.yml` and `rate-limits/cdr-energy-rate-limits.yml`.

## Rules to follow

- Send `x-v` on every request; endpoint versions differ per operation, so read the `x-v` **response**
  header to learn what you actually got.
- Send an `x-fapi-interaction-id` UUID so you can correlate your monitoring logs with a holder's.
- Poll politely. Excess traffic may be throttled or rejected without breaching the holder's
  obligations; a 429 means back off.
- A 404 on `{publicBaseUri}/cds-au/v1/...` is usually a different holder path for unauthenticated
  endpoints, not an outage. Do not report it as downtime.
- The ACCC's own compliance view comes from `getMetrics` on each holder's Admin API, which is
  restricted to the CDR Register. Do not attempt it.
