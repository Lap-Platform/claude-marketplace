---
name: enanomapper-federated-search
description: "eNanoMapper federated search API skill. Use when working with eNanoMapper federated search for select, enm. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# eNanoMapper federated search
API version: 1.0

## Auth
No authentication required.

## Base URL
https://api.ideaconsult.net/enanomapper

## Setup
1. No auth setup needed
2. GET /select -- verify access
3. POST /select -- create first select

## Endpoints

13 endpoints across 2 groups. See references/api-spec.lap for full details.

### select
| Method | Path | Description |
|--------|------|-------------|
| GET | /select | Apache Solr powered search |
| POST | /select | Apache Solr powered search |

### enm
| Method | Path | Description |
|--------|------|-------------|
| GET | /enm/{db}/investigation | Details of multiple studies |
| GET | /enm/{db}/substance | List substances |
| GET | /enm/{db}/substance/{uuid} | Get a substance |
| GET | /enm/{db}/substance/{uuid}/study | get substance study |
| GET | /enm/{db}/substance/{uuid}/composition | Substance composition |
| GET | /enm/{db}/substance/{uuid}/structures | Get substance composition as a dataset |
| GET | /enm/{db}/substance/{uuid}/studySummary | Get study summary for the substance |
| GET | /enm/{db}/query/study | Search endpoint summary |
| GET | /enm/{db}/query/compound/{term}/{representation} | Exact chemical structure search |
| GET | /enm/{db}/query/smarts | Substructure search |
| GET | /enm/{db}/query/similarity | Exact similarity search |

## Enhanced Skill Content
## Question Mapping

- "Search for nanomaterials by keyword?" -> GET /select
- "Find all substances in the nanoreg1 database?" -> GET /enm/{db}/substance
- "Look up a specific substance by UUID?" -> GET /enm/{db}/substance/{uuid}
- "What studies exist for a given nanomaterial?" -> GET /enm/{db}/substance/{uuid}/study
- "What is the chemical composition of a substance?" -> GET /enm/{db}/substance/{uuid}/composition
- "Find substances by InChIKey or SMILES structure?" -> GET /enm/{db}/query/compound/{term}/{representation}
- "Run a substructure search using SMARTS?" -> GET /enm/{db}/query/smarts
- "Find structurally similar compounds above a threshold?" -> GET /enm/{db}/query/similarity
- "Get a summary of all study categories for a substance?" -> GET /enm/{db}/substance/{uuid}/studySummary
- "List investigations filtered by assay or provider?" -> GET /enm/{db}/investigation
- "Which databases contain toxicology data for a substance?" -> GET /enm/{db}/substance/{uuid}/study (with `top=TOX`, iterate across db values)
- "Run a faceted Solr query with custom field selection?" -> POST /select
- "Get structural representations (names, CAS, InChI) for a substance?" -> GET /enm/{db}/substance/{uuid}/structures
- "Browse available study endpoints across a database?" -> GET /enm/{db}/query/study

## Response Tips

- **select endpoints**: Responses wrap results in `response.docs` array; check `response.numFound` vs `rows` to know if more pages exist. Use `start` for offset-based pagination.
- **substance endpoints**: Results nest under a `substance` map; individual substance lookups return the same wrapper. Pagination uses `page`/`pagesize` (0-indexed pages).
- **study/studySummary endpoints**: Study data nests measurement values across `loValue`, `upValue`, `unit`, and qualifier fields -- all may be null. `studySummary` returns faceted counts under `facet`.
- **compound/smarts/similarity endpoints**: Responses split into `dataEntry` (matched records), `feature` (property definitions), and `query` (echo of search params). Cross-reference feature URIs to interpret data entries.
- **investigation endpoint**: Returns flat records with `_childDocuments_` for nested measurements. Fields like `loQualifier`/`upQualifier` use comparison operators (=, >, <).
- **error responses**: All `enm` endpoints return only 404; `select` endpoints return a broad range (400-510) -- check `responseHeader.status` for Solr-level errors even on HTTP 200.

## Anomaly Flags

- **Large result sets without pagination**: Surface a warning when `response.numFound` greatly exceeds `rows` (select) or when substance lists exceed `pagesize`, indicating the user is only seeing a fraction of results.
- **Empty docs with 200 status**: The API returns HTTP 200 with `numFound: 0` for no-match queries -- flag this explicitly rather than silently returning nothing.
- **Solr internal errors on 200**: `responseHeader.status` can be non-zero even on HTTP 200 responses -- always check this field and surface non-zero values.
- **Database selection mismatch**: If the user queries a database (e.g., `calibrate`) that has minimal or no data for their search type, flag that they may want to try `nanoreg1` or `enanomapper` (larger datasets).
- **Missing measurement units**: Study results may have `loValue`/`upValue` populated but `unit` empty -- flag incomplete measurement records.
- **HTTP 503/510 from select**: These indicate Solr cluster issues (503) or extended search policy violations (510) -- surface as service-level problems, not user errors.
- **Threshold ignored in similarity**: If a similarity search returns unexpectedly many results, flag that the `threshold` parameter may need to be raised (default can be permissive).

## Playbook

### 1. Full substance profile retrieval

1. Search for the substance: `GET /enm/nanoreg1/substance?search=TiO2&type=name`
2. Extract the substance `uuid` from the response
3. Get composition: `GET /enm/nanoreg1/substance/{uuid}/composition`
4. Get all studies: `GET /enm/nanoreg1/substance/{uuid}/study`
5. Get study summary for a high-level overview: `GET /enm/nanoreg1/substance/{uuid}/studySummary`
6. Get structural identifiers: `GET /enm/nanoreg1/substance/{uuid}/structures`

### 2. Cross-database substance comparison

1. Pick the target substance and note its name or InChIKey
2. Query each database: `GET /enm/{db}/substance?search={name}&type=name` for each db value (nanoreg1, enanomapper, marina, etc.)
3. Collect UUIDs from databases that return results
4. For each hit, fetch study summaries: `GET /enm/{db}/substance/{uuid}/studySummary`
5. Compare available endpoint categories and measurement counts across databases

### 3. Structure-based nanomaterial discovery

1. Start with a known structure (SMILES or InChIKey)
2. Exact match: `GET /enm/enanomapper/query/compound/search/smiles?search={SMILES}`
3. Substructure search: `GET /enm/enanomapper/query/smarts?search={SMARTS}&filterBySubstance=true`
4. Similarity search: `GET /enm/enanomapper/query/similarity?search={SMILES}&threshold=0.8`
5. For each matched compound, follow up with substance and study lookups using the UUIDs from results

### 4. Toxicology data extraction for a substance class

1. Search investigations by study type: `GET /enm/nanoreg1/investigation?type=bystudytype&search=TOX`
2. Browse available tox categories: `GET /enm/nanoreg1/query/study?top=TOX`
3. List substances: `GET /enm/nanoreg1/substance?type=substancetype&search={material_type}`
4. For each substance, pull tox studies: `GET /enm/nanoreg1/substance/{uuid}/study?top=TOX`
5. Paginate through results using `page` and `pagesize` until all records are collected

### 5. Faceted Solr search for advanced filtering

1. Use `POST /select` with a facet configuration to explore available filter values
2. Set `params.fl` to limit returned fields to only what you need
3. Apply `fq` filters via `GET /select?fq=topcategory:TOX&fq=owner_name:ACME`
4. Use `start` and `rows` to paginate through large result sets
5. Switch `wt=json` for programmatic consumption (default is XML)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
