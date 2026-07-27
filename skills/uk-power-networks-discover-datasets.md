---
name: Discover UK Power Networks datasets and resolve their field schema
description: >-
  Find the right dataset among the 136 in the UK Power Networks Open Data catalogue, then read its
  runtime field schema before composing any query. This is the mandatory first skill — every other
  skill against this API depends on it, because field names are per-dataset and an unknown field
  fails the call.
api: openapi/uk-power-networks-explore-api-v2-1-openapi.json
base_url: https://ukpowernetworks.opendatasoft.com/api/explore/v2.1
operations:
  - getDatasets
  - getDatasetsFacets
  - getDataset
generated: '2026-06-20'
method: generated
---

# Discover UK Power Networks datasets

## When to use this

Before anything else. The UK Power Networks Open Data Portal serves one generic contract over 136
differently-shaped datasets. The contract types a record as an open object, so the real schema only
becomes knowable at runtime, from the dataset entity. Skipping this skill and guessing field names
produces `HTTP 400 ODSQLError`.

## Authentication

Optional for this skill. The whole catalogue surface — `getDatasets`, `getDatasetsFacets` and
`getDataset` — answers anonymously. Records do not: 99 of the 136 datasets return
`403 ForbiddenAccess` without a key. If you have one, append `apikey=<KEY>` to every request. See
`authentication/uk-power-networks-authentication.yml`.

## Steps

### 1. Narrow the catalogue with facets — `getDatasetsFacets`

```
GET /catalog/facets?facet=theme
GET /catalog/facets?facet=license
GET /catalog/facets?facet=keyword
```

Facets are the cheapest way to understand the shape of the catalogue before searching it. Themes
partition into Network Usage, Network Infrastructure and Supporting Information.

### 2. Search the catalogue — `getDatasets`

```
GET /catalog/datasets?where=search(%22carbon%20intensity%22)&limit=20&select=dataset_id
GET /catalog/datasets?refine=theme:Network%20Usage&limit=100&select=dataset_id
```

- `where` takes ODSQL. `search("...")` is a full-text match; `AND`, `OR`, `NOT` and comparison
  operators are available.
- `refine=<facet>:<value>` narrows by an exact facet value.
- `select` projects fields — use `select=dataset_id` when you only need identifiers.
- `limit` is capped at **100** without a `group_by`, and `offset+limit` must stay under **10000**.
  Read `total_count` from the response to decide whether to page.

Identifier convention: lowercase kebab-case, nearly always prefixed `ukpn-`. Republished
third-party data may differ, e.g. `ozev-ukpn-national-chargepoint-register`.

### 3. Read the field schema — `getDataset`

```
GET /catalog/datasets/ukpn-carbon-intensity
```

Take two things from the response:

- **`fields[]`** — `name`, `label`, `type`, `description`. These `name` values are the *only* legal
  identifiers in a `select`, `where`, `group_by` or `order_by` clause for this dataset. Nothing here
  is shared with any other dataset.
- **`metas.default`** — `title`, `license`, `modified`, `records_count`, `publisher`, and
  `data_visible`. If `data_visible` is `false`, records will return `403` without a key; decide now
  whether to authenticate rather than after the failed call.

Use `modified` as your freshness signal. The API is served with `cache-control: no-store` and emits
no `ETag`, so there is no conditional-request path — comparing `modified` is how you avoid refetching.

## Rules

- **Never compose a clause from a field name you have not seen in `fields[]`.** This is the single
  most common failure against this API.
- All three operations are HTTP GETs and therefore safe to retry. On `429`, back off to the
  `X-RateLimit-Reset` timestamp (an absolute time, not a delta). On `400` or `403`, do not retry —
  both are stable.
- The anonymous budget is 10,000 calls per day per domain. Facet and catalogue calls are cheap;
  spend the budget on records, not on rediscovery — cache the `dataset_id` and `fields[]` you resolve.

## Errors

| Status | `error_code` | Meaning | Action |
|---|---|---|---|
| 400 | `ODSQLError` | Unknown field or function in a clause | Re-read `fields[]`, rebuild the clause |
| 400 | `InvalidRESTParameterError` | `limit` or `offset` out of range | Keep `limit` ≤ 100, `offset+limit` < 10000 |
| 404 | `NotFoundResource` | `dataset_id` does not exist | Re-enumerate with `getDatasets?select=dataset_id` |
| 429 | numeric `errorcode` | Budget exhausted | Back off to `reset_time` |

Full catalogue: `errors/uk-power-networks-problem-types.yml`.

## Next

- `uk-power-networks-query-records.md` — query the records of a dataset you have resolved.
- `uk-power-networks-export-dataset.md` — pull a whole dataset without paginating.
