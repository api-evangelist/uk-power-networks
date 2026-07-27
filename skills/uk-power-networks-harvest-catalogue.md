---
name: Harvest the UK Power Networks catalogue as DCAT-AP
description: >-
  Pull the whole 136-dataset UK Power Networks Open Data catalogue as machine-readable metadata —
  DCAT-AP RDF for a data portal or triple store, CSV for a spreadsheet — and use the licence and
  visibility facets to work out what you can actually reach before you build against it.
api: openapi/uk-power-networks-explore-api-v2-1-openapi.json
base_url: https://ukpowernetworks.opendatasoft.com/api/explore/v2.1
operations:
  - exportCatalogDCAT
  - exportCatalogCSV
  - exportDatasets
  - listExportFormats
  - getDatasetsFacets
  - getDatasets
generated: '2026-06-20'
method: generated
---

# Harvest the UK Power Networks catalogue

## When to use this

You are federating UK Power Networks into another data portal, building a cross-DNO index, or doing
a coverage assessment. This is metadata harvesting, not data extraction — for the data itself see
`uk-power-networks-export-dataset.md`.

## Authentication

None needed. The entire catalogue surface answers anonymously, including the DCAT export. Only
records are gated.

## Steps

### 1. Harvest DCAT-AP — `exportCatalogDCAT`

```
GET /catalog/exports/dcat
```

Returns `application/rdf+xml` with `dcat:` and `dcatap:` (`data.europa.eu/r5r`) namespaces declared
at the document root. This is the standards-conformant route and the one to use for federation —
every dataset arrives as a `dcat:Dataset` with title, description, publisher, licence, keywords and
distributions already mapped.

Verified HTTP 200 on 2026-07-27.

### 2. Or harvest tabular metadata — `exportCatalogCSV` / `exportDatasets`

```
GET /catalog/exports/csv
GET /catalog/exports/{format}
```

`listExportFormats` (`GET /catalog/exports`) enumerates what the catalogue level supports. Use CSV
when you want a quick inventory rather than RDF.

### 3. Profile the catalogue before building — `getDatasetsFacets`

```
GET /catalog/facets?facet=license
GET /catalog/facets?facet=theme
GET /catalog/facets?facet=publisher
```

Licence counts read live on 2026-07-27: CC BY 4.0 — 122; Open Government Licence v3.0 — 6; UK Power
Networks Shared Data Licence (Connections) — 5; Shared Dataset Agreement — 2; UK Power Networks
Shared Data Licence (Common Information Model) — 1. Themes: Network Usage 68, Network Infrastructure
41, Supporting Information 38. Publisher is uniform: UK Power Networks, company number 3870728.

### 4. Establish what is actually reachable — `getDatasets` + a probe

Licence does **not** predict access here, and this is the trap in this catalogue. Enumerate the
identifiers, then test reachability directly:

```
GET /catalog/datasets?limit=100&select=dataset_id
GET /catalog/datasets?limit=100&offset=100&select=dataset_id
```

then for each `dataset_id`:

```
GET /catalog/datasets/{dataset_id}/records?limit=1
```

Measured anonymously on 2026-07-27: **36** returned HTTP 200, **99** returned
`403 ForbiddenAccess`. The blocked ones expose `"data_visible": false` in their own metadata, so you
can also read the flag from `getDataset` instead of probing — cheaper, and it costs one call rather
than 136. CC BY 4.0 datasets are among the blocked; do not infer access from licence.

## Rules

- Harvest the DCAT export rather than paginating `getDatasets` when you want everything — one call
  against a 10,000-per-day budget.
- Re-harvest on a schedule, not continuously. The catalogue changes when datasets are added or
  renamed; dataset IDs have been renamed before without a portal notice (the `ukpn-` prefix migration
  recorded in `changelog/uk-power-networks-changelog.yml`), so pin nothing and re-resolve identifiers
  on each harvest.
- Record `metas.default.modified` per dataset — it is the only per-dataset change signal available.
- Preserve attribution. 122 datasets are CC BY 4.0 and 6 are OGL v3.0; both require it. Six further
  datasets sit under bespoke UK Power Networks shared-data licences that are not open licences at
  all — treat those separately in any republication.

## Companion vocabulary

`vocabulary/uk-power-networks-business-glossary.yml` carries the 94 terms UK Power Networks
publishes as `ukpn-business-glossary`, harvested through this same API. Use it to interpret field
labels — Bulk Supply Point, Already Allocated Capacity, Busbar and the rest.
