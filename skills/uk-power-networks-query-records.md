---
name: Query and aggregate UK Power Networks dataset records
description: >-
  Filter, sort, aggregate and page the records of a UK Power Networks dataset using the ODSQL query
  dialect — the everyday working skill for live faults, carbon intensity, flexibility dispatches,
  the embedded capacity register and every other dataset on the portal.
api: openapi/uk-power-networks-explore-api-v2-1-openapi.json
base_url: https://ukpowernetworks.opendatasoft.com/api/explore/v2.1
operations:
  - getRecords
  - getRecord
  - getRecordsFacets
generated: '2026-06-20'
method: generated
---

# Query UK Power Networks dataset records

## Prerequisite

Run `uk-power-networks-discover-datasets.md` first. You need the `dataset_id` **and** the `fields[]`
array from `getDataset`. Field names are per-dataset and unshared; an unknown one fails the call.

## Authentication

Records for **36** of the 136 datasets answer anonymously. The other **99** return
`403 ForbiddenAccess` regardless of licence — including CC BY 4.0 datasets. Registration is free and
self-serve at `https://ukpowernetworks.opendatasoft.com/signup/`; mint a key at
`https://ukpowernetworks.opendatasoft.com/account/api-keys/` and pass it as `apikey=<KEY>`.

The key rides in the **query string**, so it lands in server logs, browser history and `Referer`
headers. Do not paste a URL containing it into a shared document or an issue tracker.

## Steps

### 1. Filter and page — `getRecords`

```
GET /catalog/datasets/ukpn-live-faults/records?limit=100
GET /catalog/datasets/ukpn-carbon-intensity/records?where=licence_area%3D%22EPN%22&limit=100
GET /catalog/datasets/ukpn-carbon-intensity/records?order_by=-half_hour_period&limit=10
```

- `where` — ODSQL predicate. Supports `=`, `>`, `<`, `LIKE`, `IN`, `AND`/`OR`/`NOT`, `search("…")`
  full text, date ranges and geo filters.
- `order_by` — comma-separated field list; prefix with `-` (or suffix ` desc`) for descending.
- `select` — projection and computed expressions, e.g. `select=size * 2 as bigger_size`.
- `refine=<field>:<value>` / `exclude=<field>:<value>` — facet-value narrowing.
- `timezone` — defaults to UTC; set it before comparing timestamps.
- `limit` ≤ 100 and `offset+limit` < 10000 for a plain query.

Read `total_count` from the response. If it exceeds the paging window, stop paginating and switch to
`uk-power-networks-export-dataset.md`.

### 2. Aggregate — `getRecords` with `group_by`

```
GET /catalog/datasets/ukpn-carbon-intensity/records?group_by=licence_area&select=avg(licence_area_average_carbon_intensity)%20as%20mean_ci
```

With a `group_by` clause the ceiling changes: `limit` may go to **20000** and `offset+limit` must
stay under 20000. Aggregating server-side is almost always cheaper than pulling rows and reducing
locally, and it keeps you inside the daily call budget.

### 3. Explore value distributions — `getRecordsFacets`

```
GET /catalog/datasets/ukpn-live-faults/facets?facet=powercuttype
```

Use this to learn the legal values of a categorical field before writing a `where` clause against it.

### 4. Fetch one record — `getRecord`

```
GET /catalog/datasets/{dataset_id}/records/{record_id}
```

`record_id` comes from a prior `getRecords` response.

## Rules

- Resolve `fields[]` before composing any clause. Always.
- URL-encode ODSQL. Quotes, spaces and parentheses in `where`, `select` and `group_by` all need it.
- Every operation is a safe HTTP GET — retry freely on `429` and `5xx`. Never retry `400` or `403`.
- Geometry is not consistently named across the estate; a geospatial dataset may carry it as
  `geo_shape`, `spatial_coordinates`, `geo_point_2d`, `geo_point` or `geopoint`. Check `fields[]`.
- The portal occasionally emits `NaN` in numeric fields, which is invalid JSON. Use a tolerant
  parser or the official `ukpyn` client, which sanitises it to `None`.
- Watch the budget: `X-RateLimit-Remaining` on every response, 10,000/day anonymous, reset at
  midnight UTC as an absolute timestamp in `X-RateLimit-Reset`. A separate per-dataset budget is
  signalled through the `X-RateLimit-dataset-*` headers.

## Anonymously readable starting points

Verified answering without a key on 2026-07-27: `ukpn-live-faults`, `ukpn-carbon-intensity`,
`ozev-ukpn-national-chargepoint-register`, `ukpn-smart-meter-installation-volumes`,
`ukpn-licence-boundaries`, `ukpn-network-statistics`, `ukpn-business-glossary`.

Worked responses are saved in `examples/`.

## Errors

See `errors/uk-power-networks-problem-types.yml`. The two you will actually hit are `400 ODSQLError`
(field name wrong) and `403 ForbiddenAccess` (dataset needs a key). Neither is retryable.
