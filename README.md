# UK Power Networks

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

UK Power Networks is the distribution network operator for London, the South East and the East of England, running three electricity distribution licence areas — London Power Networks (LPN), South Eastern Power Networks (SPN) and Eastern Power Networks (EPN) — and the Distribution System Operator function that sits on top of them. It is a poles-and-wires business: it owns the substations, cables and overhead lines, holds the network capacity and connection queue, and handles more than 70,000 connection enquiries a year, but it does not sell electricity and has no retail customer relationship to expose. Its API posture is the exact inverse of the usual utility story. Britain never legislated a consumer energy data right — there is no CDR equivalent, no Green Button obligation, and the one thing the UK did mandate was infrastructure (the Smart DCC carrying smart-meter traffic under the Smart Energy Code), which produces no public API. What did produce an API was Ofgem's Data Best Practice and digitalisation obligation on network licensees, and UK Power Networks has actually implemented it: a live Opendatasoft-hosted Open Data Portal serving 136 datasets over a documented, versioned REST API with a real OpenAPI 3.0.3 contract published at its own domain, a DCAT-AP catalogue export, and an official open-source Python client (ukpyn) on PyPI. So the split is unusually sharp and unusually positive on one side: market and network data is genuinely open and genuinely queryable — live faults, carbon intensity, embedded capacity register, substation and feeder-level smart meter aggregates, LTDS tables, flexibility dispatches, curtailment events — while consumer data is not merely closed but absent, because as a DNO it holds no billable customer account to hand over. The gate is free and self-serve rather than open: the catalogue and 36 of 136 datasets answer anonymously, but the other 99 return HTTP 403 until you register a free account and mint an API key.

**Areas:** Energy · United Kingdom · Utilities · Electricity · Grid · Distribution Network · Open Data · Smart Metering · DER · EV Charging · Carbon · Energy Markets

## UK Power Networks on APIs.io

Everything profiled for UK Power Networks is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/uk-power-networks/](https://apis.io/providers/uk-power-networks/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [UK Power Networks Catalog API](https://apis.io/apis/uk-power-networks/uk-power-networks-catalog-api/) — API to enumerate datasets
- [UK Power Networks Dataset API](https://apis.io/apis/uk-power-networks/uk-power-networks-dataset-api/) — API to work on records

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [uk-power-networks](https://apis.io/servers/uk-power-networks/uk-power-networks/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Uk Power Networks Agentic Access](https://apis.io/agentic-access/uk-power-networks/uk-power-networks-agentic-access/)

#### Examples (5)

Example requests and responses.

- [Uk Power Networks Getdataset Live Faults Response](https://apis.io/examples/uk-power-networks/uk-power-networks-getDataset-live-faults-response/)
- [Uk Power Networks Getdatasets Response](https://apis.io/examples/uk-power-networks/uk-power-networks-getDatasets-response/)
- [Uk Power Networks Getdatasetsfacets Response](https://apis.io/examples/uk-power-networks/uk-power-networks-getDatasetsFacets-response/)
- [Uk Power Networks Getrecords Carbon Intensity Response](https://apis.io/examples/uk-power-networks/uk-power-networks-getRecords-carbon-intensity-response/)
- [Uk Power Networks Getrecords Live Faults Response](https://apis.io/examples/uk-power-networks/uk-power-networks-getRecords-live-faults-response/)

#### Collections (2)

Postman and Open Collection request collections.

- [Explore API](https://apis.io/collections/uk-power-networks/open-uk-power-networks-explore-api-v2-0/)
- [Explore API](https://apis.io/collections/uk-power-networks/open-uk-power-networks-explore-api-v2-1/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Uk Power Networks Explore Api V2 0 Overlay](https://apis.io/overlays/uk-power-networks/uk-power-networks-explore-api-v2-0-overlay/)
- [Uk Power Networks Explore Api V2 1 Overlay](https://apis.io/overlays/uk-power-networks/uk-power-networks-explore-api-v2-1-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Uk Power Networks Authentication](https://apis.io/security/uk-power-networks/uk-power-networks-authentication/)
- [Uk Power Networks Domain Security](https://apis.io/security/uk-power-networks/uk-power-networks-domain-security/)
- [Uk Power Networks Vulnerability Disclosure](https://apis.io/security/uk-power-networks/uk-power-networks-vulnerability-disclosure/)

#### Rate limits (1)

Published request limits.

- [Uk Power Networks Rate Limits](https://apis.io/rate-limits/uk-power-networks/uk-power-networks-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.ukpowernetworks.co.uk/)
- [Documentation](https://www.ukpowernetworks.co.uk/our-company/open-data-portal)
- [Getting started](https://ukpn-dso.github.io/ukpyn/getting-started/)
- [API reference](https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/)
- [Sign up](https://ukpowernetworks.opendatasoft.com/signup/)
- [Support](https://github.com/UKPN-DSO/ukpyn/issues)
- [Security](https://github.com/UKPN-DSO/ukpyn/blob/main/SECURITY.md)
- [Compliance](https://ukpowernetworks.opendatasoft.com/pages/data-best-practice/)
- [Terms of service](https://legal.huwise.com/en/terms-of-use.html)
- [Privacy policy](https://legal.huwise.com/en/privacy-policy.html)
- [GitHub](https://github.com/UKPN-DSO)

## API Evangelist rating

**Kin Score 61.7** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 54.2 |
| Contract governance | 33.3 |
| Operational transparency | 57.9 |
| Developer ergonomics | 87.5 |
| Access clarity | 42.1 |

**Agent readiness 37.3** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | na |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | na |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.1** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/uk-power-networks/](https://apis.io/providers/uk-power-networks/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for UK Power Networks: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/uk-power-networks/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
