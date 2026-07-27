# UK Power Networks (uk-power-networks)

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
