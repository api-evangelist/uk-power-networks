# UK Power Networks (uk-power-networks)

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

UK Power Networks is the distribution network operator for London, the South East and the East of England, running three electricity distribution licence areas — London Power Networks (LPN), South Eastern Power Networks (SPN) and Eastern Power Networks (EPN) — and the Distribution System Operator function that sits on top of them. It is a poles-and-wires business: it owns the substations, cables and overhead lines, holds the network capacity and connection queue, and handles more than 70,000 connection enquiries a year, but it does not sell electricity and has no retail customer relationship to expose. Its API posture is the exact inverse of the usual utility story. Britain never legislated a consumer energy data right — there is no CDR equivalent, no Green Button obligation, and the one thing the UK did mandate was infrastructure (the Smart DCC carrying smart-meter traffic under the Smart Energy Code), which produces no public API. What did produce an API was Ofgem's Data Best Practice and digitalisation obligation on network licensees, and UK Power Networks has actually implemented it: a live Opendatasoft-hosted Open Data Portal serving 136 datasets over a documented, versioned REST API with a real OpenAPI 3.0.3 contract published at its own domain, a DCAT-AP catalogue export, and an official open-source Python client (ukpyn) on PyPI.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/uk-power-networks/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/uk-power-networks/refs/heads/main/apis.yml)

## Tags

- Energy
- United Kingdom
- Utilities
- Electricity
- Grid
- Distribution Network
- Open Data
- Smart Metering
- DER
- EV Charging
- Carbon
- Energy Markets

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### UK Power Networks Open Data Explore API v2.1

The current read-only REST API behind the UK Power Networks Open Data Portal, served from the company's own opendatasoft.com subdomain under an Opendatasoft Explore API v2.1 contract. Sixteen GET endpoints cover catalogue search, dataset metadata, record query with an ODSQL where/select/group_by dialect, facets, attachments, and bulk exports in CSV, JSON, Parquet, GeoJSON, GPX and DCAT-AP. 136 UK Power Networks datasets are catalogued: live faults from the Distribution Network Management System, carbon intensity, the embedded capacity register, LTDS tables, flexibility dispatches and tenders, curtailment events, network losses, substation and LV-feeder smart meter aggregates, GIS asset and boundary layers, and the OZEV National Chargepoint Register. Catalogue metadata answers anonymously; records for most datasets require a free account API key passed as an `apikey` query parameter. Anonymous rate limit observed at 10,000 calls per day.

- **Human URL:** [https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/](https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/)
- **Base URL:** `https://ukpowernetworks.opendatasoft.com/api/explore/v2.1`

#### Tags

- Open Data
- Electricity
- Grid
- Network Infrastructure
- Network Usage
- Smart Metering
- Carbon
- EV Charging

#### Properties

- [OpenAPI](openapi/uk-power-networks-explore-api-v2-1-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://ukpowernetworks.opendatasoft.com/api/explore/v2.1/swagger.json)
- [Console](https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/)
- [Documentation](https://ukpowernetworks.opendatasoft.com/pages/home/)
- [Portal](https://ukpowernetworks.opendatasoft.com/)
- [SDK](https://github.com/UKPN-DSO/ukpyn)
- [Signup](https://ukpowernetworks.opendatasoft.com/signup/)
- [Authentication](https://ukpowernetworks.opendatasoft.com/account/api-keys/)
- [DCAT](https://ukpowernetworks.opendatasoft.com/api/explore/v2.1/catalog/exports/dcat)

### UK Power Networks Open Data Explore API v2.0

The previous version of the UK Power Networks Open Data Portal REST API, still live and still serving its own OpenAPI 3.0.3 contract at the company domain. Same sixteen endpoints and same catalogue as v2.1, distinguished by the version segment in the base URL; the platform advertises deprecation through an `ODS-Explore-API-Deprecation` response header. Recorded here because it is a real, reachable, separately-contracted surface, not because it is the one to build on.

- **Human URL:** [https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/](https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/)
- **Base URL:** `https://ukpowernetworks.opendatasoft.com/api/explore/v2.0`

#### Tags

- Open Data
- Electricity
- Grid
- Deprecated

#### Properties

- [OpenAPI](openapi/uk-power-networks-explore-api-v2-0-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://ukpowernetworks.opendatasoft.com/api/explore/v2.0/swagger.json)
- [Portal](https://ukpowernetworks.opendatasoft.com/)

## Common Properties

- [Website](https://www.ukpowernetworks.co.uk/)
- [GitHub Organization](https://github.com/UKPN-DSO)
- [Portal](https://ukpowernetworks.opendatasoft.com/)
- [Documentation](https://www.ukpowernetworks.co.uk/our-company/open-data-portal)
- [Console](https://ukpowernetworks.opendatasoft.com/api-console/explore/v2.1/)
- [Signup](https://ukpowernetworks.opendatasoft.com/signup/)
- [Login](https://ukpowernetworks.opendatasoft.com/login/)
- [Glossary](https://ukpowernetworks.opendatasoft.com/pages/glossary/)
- [Compliance](https://ukpowernetworks.opendatasoft.com/pages/data-best-practice/)
- [Regulation](https://www.ofgem.gov.uk/decision/decision-updates-data-best-practice-guidance-and-digitalisation-strategy-and-action-plan-guidance)
- [Data](https://ukpowernetworks.opendatasoft.com/explore/)
- [DSO](https://dso.ukpowernetworks.co.uk/)
- [SDK](https://pypi.org/project/ukpyn/)
- [Showcase](https://ukpowernetworks.opendatasoft.com/pages/reuses/)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
