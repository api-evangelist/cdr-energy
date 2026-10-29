# Consumer Data Right (Energy)

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
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

**Areas:** Energy · Australia · Utilities · Electricity · Consumer Data Right · Open Energy · Smart Metering · DER · Energy Markets · Regulations · Government · Open Data

## Consumer Data Right (Energy) on APIs.io

Everything profiled for Consumer Data Right (Energy) is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/cdr-energy/](https://apis.io/providers/cdr-energy/)** — or go straight to one of the APIs or properties below.

### APIs (17)

- [Consumer Data Right (Energy) Data Holder Admin API](https://apis.io/apis/cdr-energy/cdr-energy-data-holder-admin-api/) — Data Holder Admin endpoints
- [Consumer Data Right (Energy) Data Holder Client Registration API](https://apis.io/apis/cdr-energy/cdr-energy-data-holder-client-registration-api/) — Data Holder Client Registration endpoints
- [Consumer Data Right (Energy) Data Holder Customers API](https://apis.io/apis/cdr-energy/cdr-energy-data-holder-customers-api/) — Data Holder Customer endpoints
- [Consumer Data Right (Energy) Data Holder Operations API](https://apis.io/apis/cdr-energy/cdr-energy-data-holder-operations-api/) — Data Holder Operations endpoints
- [Consumer Data Right (Energy) Distributed Energy Resources API](https://apis.io/apis/cdr-energy/cdr-energy-distributed-energy-resources-api/) — Distributed Energy Resource endpoints
- [Consumer Data Right (Energy) Distributed Energy Resources (SR) API](https://apis.io/apis/cdr-energy/cdr-energy-distributed-energy-resources-sr-api/) — Distributed Energy Resource (SR) endpoints
- [Consumer Data Right (Energy) Electricity Service Points API](https://apis.io/apis/cdr-energy/cdr-energy-electricity-service-points-api/) — Electricity Service Point endpoints
- [Consumer Data Right (Energy) Electricity Service Points (SR) API](https://apis.io/apis/cdr-energy/cdr-energy-electricity-service-points-sr-api/) — Electricity Service Point (SR) endpoints
- [Consumer Data Right (Energy) Electricity Usage API](https://apis.io/apis/cdr-energy/cdr-energy-electricity-usage-api/) — Electricity Usage endpoints
- [Consumer Data Right (Energy) Electricity Usage (SR) API](https://apis.io/apis/cdr-energy/cdr-energy-electricity-usage-sr-api/) — Electricity Usage (SR) endpoints
- [Consumer Data Right (Energy) Energy Account Balances API](https://apis.io/apis/cdr-energy/cdr-energy-energy-account-balances-api/) — Energy Account Balance endpoints
- [Consumer Data Right (Energy) Energy Account Billing API](https://apis.io/apis/cdr-energy/cdr-energy-energy-account-billing-api/) — Energy Account Billing endpoints
- [Consumer Data Right (Energy) Energy Accounts API](https://apis.io/apis/cdr-energy/cdr-energy-energy-accounts-api/) — Energy Account endpoints
- [Consumer Data Right (Energy) Energy Plans API](https://apis.io/apis/cdr-energy/cdr-energy-energy-plans-api/) — Energy Plan endpoints
- [Consumer Data Right (Energy) Register Data Holder discovery API](https://apis.io/apis/cdr-energy/cdr-energy-register-data-holder-discovery-api/) — Register Data Holder discovery endpoints
- [Consumer Data Right (Energy) Register Data Recipient discovery API](https://apis.io/apis/cdr-energy/cdr-energy-register-data-recipient-discovery-api/) — Register Data Recipient discovery endpoints
- [Consumer Data Right (Energy) Register Operations API](https://apis.io/apis/cdr-energy/cdr-energy-register-operations-api/) — Register Operations endpoints

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Cdr Energy Webhooks](https://apis.io/asyncapis/cdr-energy/cdr-energy-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [cdr-energy](https://apis.io/servers/cdr-energy/cdr-energy/)

#### Examples (5)

Example requests and responses.

- [Cdr Energy Discovery Outages Response Example](https://apis.io/examples/cdr-energy/cdr-energy-discovery-outages-response-example/)
- [Cdr Energy Discovery Status Response Example](https://apis.io/examples/cdr-energy/cdr-energy-discovery-status-response-example/)
- [Cdr Energy Plan Detail Response Example](https://apis.io/examples/cdr-energy/cdr-energy-plan-detail-response-example/)
- [Cdr Energy Plans Response Example](https://apis.io/examples/cdr-energy/cdr-energy-plans-response-example/)
- [Cdr Energy Register Data Holder Brands Summary Example](https://apis.io/examples/cdr-energy/cdr-energy-register-data-holder-brands-summary-example/)

#### Collections (6)

Postman and Open Collection request collections.

- [CDR Admin API](https://apis.io/collections/cdr-energy/open-cdr-admin/)
- [CDR Common API](https://apis.io/collections/cdr-energy/open-cdr-common/)
- [CDR Dynamic Client Registration API](https://apis.io/collections/cdr-energy/open-cdr-dcr/)
- [CDR Energy API](https://apis.io/collections/cdr-energy/open-cdr-energy/)
- [CDR Energy Secondary Data Holder API](https://apis.io/collections/cdr-energy/open-cdr-energy-sdh/)
- [CDR Register API](https://apis.io/collections/cdr-energy/open-cdr-register/)

#### Overlays (6)

OpenAPI overlays, including conversational phrasing for each operation.

- [Cdr Energy Admin Overlay](https://apis.io/overlays/cdr-energy/cdr-energy-admin-overlay/)
- [Cdr Energy Common Overlay](https://apis.io/overlays/cdr-energy/cdr-energy-common-overlay/)
- [Cdr Energy Dcr Overlay](https://apis.io/overlays/cdr-energy/cdr-energy-dcr-overlay/)
- [Cdr Energy Energy Overlay](https://apis.io/overlays/cdr-energy/cdr-energy-energy-overlay/)
- [Cdr Energy Energy Sdh Overlay](https://apis.io/overlays/cdr-energy/cdr-energy-energy-sdh-overlay/)
- [Cdr Energy Register Overlay](https://apis.io/overlays/cdr-energy/cdr-energy-register-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Cdr Energy Authentication](https://apis.io/security/cdr-energy/cdr-energy-authentication/)
- [Cdr Energy Domain Security](https://apis.io/security/cdr-energy/cdr-energy-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Cdr Energy Scopes](https://apis.io/scopes/cdr-energy/cdr-energy-scopes/)

#### Rate limits (1)

Published request limits.

- [Cdr Energy Rate Limits](https://apis.io/rate-limits/cdr-energy/cdr-energy-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.cdr.gov.au/)
- [Documentation](https://dsb.gov.au/consumer-data-right/data-standards)
- [Getting started](https://consumerdatastandardsaustralia.github.io/standards/#introduction)
- [API reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-energy-api-schemas)
- [Support](https://github.com/ConsumerDataStandardsAustralia/standards-maintenance)
- [Changelog](https://github.com/ConsumerDataStandardsAustralia/standards/releases)
- [Blog](https://dsb.gov.au/news-and-announcements)
- [Security](https://consumerdatastandardsaustralia.github.io/infosec/)
- [Compliance](https://consumerdatastandardsaustralia.github.io/standards-testing/)
- [GitHub](https://github.com/ConsumerDataStandardsAustralia)
- [Status](https://consumerdatastandardsaustralia.github.io/standards/#cdr-common-api-schemas)

## API Evangelist rating

**Kin Score 57.1** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 56.7 |
| Contract governance | 18.2 |
| Operational transparency | 97.4 |
| Developer ergonomics | 82.7 |
| Access clarity | 7.9 |

**Agent readiness 37.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.5** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/cdr-energy/](https://apis.io/providers/cdr-energy/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Consumer Data Right (Energy): the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/cdr-energy/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
