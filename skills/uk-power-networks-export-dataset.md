---
name: Bulk-export a UK Power Networks dataset
description: >-
  Pull a whole UK Power Networks dataset in one uncapped call — CSV, Parquet, GeoJSON, GPX or any of
  the fifteen declared formats — instead of paginating the records endpoint past its 10,000-row
  window. Includes retrieving dataset attachments.
api: openapi/uk-power-networks-explore-api-v2-1-openapi.json
base_url: https://ukpowernetworks.opendatasoft.com/api/explore/v2.1
operations:
  - listDatasetExportFormats
  - exportRecords
  - exportRecordsCSV
  - exportRecordsParquet
  - exportRecordsGPX
  - getDatasetAttachments
generated: '2026-06-20'
method: generated
---

# Bulk-export a UK Power Networks dataset

## When to use this

Whenever `total_count` from `getRecords` exceeds a few thousand, or whenever you want the whole
dataset. The records endpoint is capped — `limit` ≤ 100 and `offset+limit` < 10000 — and the spec
itself directs you here for anything larger. The exports endpoints have **no record limit**.

## Prerequisite

A `dataset_id` from `uk-power-networks-discover-datasets.md`. An API key if the dataset's
`data_visible` metadata is `false` (99 of 136 datasets).

## Steps

### 1. Confirm the formats — `listDatasetExportFormats`

```
GET /catalog/datasets/{dataset_id}/exports
```

The spec declares fifteen: `csv`, `fgb`, `geojson`, `gpx`, `json`, `jsonl`, `jsonld`, `kml`, `n3`,
`ov2`, `parquet`, `rdfxml`, `shp`, `turtle`, `xlsx`. Not every dataset supports every one — a
non-geospatial dataset will not export `shp` or `kml`.

### 2. Export — `exportRecords` (or a format-specific operation)

```
GET /catalog/datasets/ukpn-carbon-intensity/exports/parquet
GET /catalog/datasets/ukpn-live-faults/exports/csv
GET /catalog/datasets/ukpn-licence-boundaries/exports/geojson
```

Dedicated operations exist for three of them and behave identically to the generic form:
`exportRecordsCSV`, `exportRecordsParquet`, `exportRecordsGPX`.

**ODSQL still applies.** `where`, `select`, `order_by`, `refine` and `exclude` work on exports too, so
export a filtered slice rather than the whole thing when you only need part of it:

```
GET /catalog/datasets/ukpn-carbon-intensity/exports/csv?where=licence_area%3D%22LPN%22
```

### 3. Pick the right format

- **`parquet`** — the default choice for anything large or numeric. Columnar, typed, compact.
- **`csv`** — universal, but loses types and inflates timestamps.
- **`geojson`** — geospatial datasets. Note the geometry field name varies across the estate; the
  export normalises it.
- **`jsonld` / `turtle` / `n3` / `rdfxml`** — when you are feeding a triple store.
- **`xlsx`** — for handing to an analyst, not to a pipeline.

### 4. Collect attachments — `getDatasetAttachments`

```
GET /catalog/datasets/{dataset_id}/attachments
```

Returns non-tabular files bundled with the dataset — methodology notes, PDFs, supporting documents —
each with `href`, `id`, `mimetype` and `title`. Several UK Power Networks datasets carry their
methodology only as an attachment, so check here before concluding a field is undocumented.

## Rules

- One export call replaces hundreds of paged records calls. Against a 10,000-call daily budget that
  is the difference between a working pipeline and an exhausted quota.
- Exports are HTTP GETs and are safe to retry. Expect a long-running response on a large dataset —
  set a generous client timeout and stream to disk rather than buffering.
- Re-export only when the dataset's `metas.default.modified` timestamp has moved. Responses carry
  `cache-control: no-store` and no `ETag`, so `modified` is the only change signal available.
- A `403 ForbiddenAccess` on an export means the same thing it means on records: the dataset needs a
  key. Do not retry unauthenticated.

## Whole-catalogue variants

The same pattern exists one level up, over dataset *metadata* rather than records:
`exportDatasets`, `exportCatalogCSV`, and `exportCatalogDCAT` — see
`uk-power-networks-harvest-catalogue.md`.
