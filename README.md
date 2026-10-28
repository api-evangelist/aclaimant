# Aclaimant

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

Aclaimant is a Chicago-based risk management information system (RMIS) used by policyholders, insurance brokers, carriers and third-party administrators to run incident reporting and first notice of loss (FNOL), claims management and analytics, safety and loss control, OSHA logs, policy management, and assets and exposures from one workflow platform. Its machine-readable surface is the Aclaimant Platform API — a Swagger 2.0 contract published at api.aclaimant.com/api with a live Swagger UI console — which lets integrators create and upsert answer bundles, incidents, claims, claim reports, events, files, companies, policies, policy programs, exposures and exposure summations, including bulk jobs with a status endpoint. A separate Partner / Third-party API at api.aclaimant.com/partner lets carriers, TPAs and brokers acknowledge claim receipt and post loss-run claim financial updates back into Aclaimant.

**Areas:** Risk Management · Insurance · Claims Management · Incident Management · Safety · RMIS · Workers Compensation · OSHA · Enterprise Risk Management · Insurtech

## Aclaimant on APIs.io

Everything profiled for Aclaimant is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/aclaimant/](https://apis.io/providers/aclaimant/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [Aclaimant Partner / Third-party API](https://apis.io/apis/aclaimant/aclaimant-partner-third-party-api/) — Callback API for TPAs, carriers, brokers and other Aclaimant partners working claims on behalf of an Aclaimant customer. Base URL…
- [Aclaimant Answers API](https://apis.io/apis/aclaimant/aclaimant-answers-api/) — The answers API from Aclaimant — 15 operation(s) for answers.
- [Aclaimant Bulk API](https://apis.io/apis/aclaimant/aclaimant-bulk-api/) — The bulk API from Aclaimant — 8 operation(s) for bulk.
- [Aclaimant Companies API](https://apis.io/apis/aclaimant/aclaimant-companies-api/) — The companies API from Aclaimant — 1 operation(s) for companies.
- [Aclaimant Exposures API](https://apis.io/apis/aclaimant/aclaimant-exposures-api/) — The exposures API from Aclaimant — 2 operation(s) for exposures.
- [Aclaimant Incidents API](https://apis.io/apis/aclaimant/aclaimant-incidents-api/) — The incidents API from Aclaimant — 1 operation(s) for incidents.
- [Aclaimant Policies API](https://apis.io/apis/aclaimant/aclaimant-policies-api/) — The policies API from Aclaimant — 2 operation(s) for policies.
- [Aclaimant Policy Programs API](https://apis.io/apis/aclaimant/aclaimant-policy-programs-api/) — The policy-programs API from Aclaimant — 2 operation(s) for policy-programs.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [aclaimant-mcp.yml](https://apis.io/servers/aclaimant/aclaimant-mcp-yml/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Aclaimant Platform Api Overlay](https://apis.io/overlays/aclaimant/aclaimant-platform-api-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Aclaimant Authentication](https://apis.io/security/aclaimant/aclaimant-authentication/)
- [Aclaimant Domain Security](https://apis.io/security/aclaimant/aclaimant-domain-security/)
- [Aclaimant Trust Center](https://apis.io/security/aclaimant/aclaimant-trust-center/)
- [Aclaimant Vulnerability Disclosure](https://apis.io/security/aclaimant/aclaimant-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Aclaimant Plans Pricing](https://apis.io/plans/aclaimant/aclaimant-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Aclaimant Rate Limits](https://apis.io/rate-limits/aclaimant/aclaimant-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.aclaimant.com/)
- [Documentation](https://developer.aclaimant.com/)
- [API reference](https://api.aclaimant.com/api/index.html)
- [Pricing](https://www.aclaimant.com/plans-and-pricing)
- [Support](https://support.aclaimant.com/hc/en-us)
- [Changelog](https://support.aclaimant.com/hc/en-us/sections/4406733144859-Product-Updates-Releases)
- [Blog](https://www.aclaimant.com/blog)
- [Security](https://www.aclaimant.com/responsible-disclosure)
- [Trust centre](https://trust.aclaimant.com/)
- [Terms of service](https://www.aclaimant.com/service-agreement)
- [Privacy policy](https://www.aclaimant.com/privacy-policy)
- [GitHub](https://github.com/aclaimant)
- [Status](https://status.aclaimant.com/)

## API Evangelist rating

**Kin Score 54.5** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 36.5 |
| Contract governance | 4.5 |
| Operational transparency | 44.7 |
| Developer ergonomics | 54.2 |
| Access clarity | 85.5 |

**Agent readiness 27.0** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | derived (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 31.6** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/aclaimant/](https://apis.io/providers/aclaimant/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Aclaimant: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/aclaimant/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
