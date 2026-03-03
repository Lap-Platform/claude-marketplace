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
https://api.ideaconsult.net/nanoreg1

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

- "Search for nanomaterials by name?" -> GET /enm/{db}/substance with `search` and `type=name`
- "Find all substances in the nanoreg1 database?" -> GET /enm/{db}/substance with `db=nanoreg1`
- "Get details for a specific substance by UUID?" -> GET /enm/{db}/substance/{uuid}
- "What studies exist for a given nanomaterial?" -> GET /enm/{db}/substance/{uuid}/study
- "What is the chemical composition of a substance?" -> GET /enm/{db}/substance/{uuid}/composition
- "Find substances by InChIKey?" -> GET /enm/{db}/query/compound/{term}/{representation} with `term=inchikey`
- "Search for structurally similar compounds?" -> GET /enm/{db}/query/similarity with `search` and `threshold`
- "Run a SMARTS substructure query?" -> GET /enm/{db}/query/smarts with `search` or `b64search`
- "List investigations filtered by assay type?" -> GET /enm/{db}/investigation with `type=byassay`
- "Get a study summary for toxicology endpoints?" -> GET /enm/{db}/substance/{uuid}/studySummary with `top=TOX`
- "Run a free-text Solr query across the index?" -> GET /select with `q` parameter
- "Perform a faceted search with field filters?" -> POST /select with `facet` map in body
- "Find all substances from a specific data owner?" -> GET /enm/{db}/substance with `type=owner_name` and `search`
- "Look up a compound by CAS number?" -> GET /enm/{db}/query/compound/{term}/{representation} with `term=search`, `representation=cas`
- "Browse studies by endpoint category (e.g., ecotoxicity)?" -> GET /enm/{db}/query/study with `top=ECOTOX`

## Response Tips

- **select endpoints**: Responses wrap results in `responseHeader` (check `status` for errors, `QTime` for performance) and `response` (use `numFound` for total count, `start` for offset-based pagination, `docs` array for actual records).
- **substance list/detail**: Results nest under a `substance` map; paginate with `page` and `pagesize` params -- there are no next/prev links, so track page index manually.
- **study & studySummary**: Study data returns deeply nested maps with qualifier fields (`loQualifier`, `upQualifier`, `errQualifier`) alongside numeric values -- always check qualifiers before interpreting `loValue`/`upValue`.
- **composition & structures**: Responses split data across `composition`/`dataEntry` and a separate `feature` map that defines property URIs -- join them by feature URI keys.
- **compound queries (compound, smarts, similarity)**: Results share the same shape (`query`, `dataEntry`, `model_uri`, `feature`) -- `dataEntry` contains matched compounds and `feature` maps property identifiers to human-readable labels.

## Anomaly Flags

- **HTTP 503 (Service Unavailable)**: The Solr/ZooKeeper backend may be down -- surface immediately and suggest retrying after a delay.
- **`zkConnected: false` in responseHeader**: The search cluster has lost ZooKeeper coordination; results may be stale or incomplete.
- **`QTime` exceeding 5000ms**: Query performance is degraded -- suggest narrowing filters or reducing `rows`/`pagesize`.
- **HTTP 415 (Unsupported Media Type)**: The `wt` format parameter is invalid -- flag and suggest switching to `json` or `xml`.
- **HTTP 510 (Not Extended)**: Unusual status code specific to this API -- likely indicates a missing required extension or parameter; surface the full error body.
- **Empty `docs` array with `numFound > 0`**: Pagination offset (`start`) exceeds available results -- alert the user that they have paged past the data.
- **`loValue`/`upValue` present without qualifiers**: Measurement data may be ambiguous without `loQualifier`/`upQualifier` context -- flag for review.
- **Database parameter mismatch**: If the user targets a `db` value not in the allowed enum (13 databases), the 404 may be unclear -- proactively validate before sending.

## Playbook

### 1. Discover and Profile a Nanomaterial

1. `GET /enm/nanoreg1/substance?search=TiO2&type=name` to find matching substances.
2. Pick a substance UUID from the results.
3. `GET /enm/nanoreg1/substance/{uuid}` to retrieve full metadata.
4. `GET /enm/nanoreg1/substance/{uuid}/composition` to see chemical composition.
5. `GET /enm/nanoreg1/substance/{uuid}/structures` to get structural representations.

### 2. Review All Safety Studies for a Substance

1. `GET /enm/nanoreg1/substance/{uuid}/studySummary?top=TOX` to get a toxicology overview.
2. `GET /enm/nanoreg1/substance/{uuid}/study?top=TOX&pagesize=100` to list individual studies.
3. Filter by `category` if a specific endpoint (e.g., genotoxicity) is needed.
4. Cross-reference `document_uuid` and `reference` fields against published literature.
5. Repeat with `top=ECOTOX` or `top=ENV FATE` for environmental safety data.

### 3. Structure-Based Substance Search

1. `GET /enm/nanoreg1/query/compound/search/smiles?search=O` to find compounds by SMILES.
2. For substructure matching, use `GET /enm/nanoreg1/query/smarts?search=[SMARTS_PATTERN]`.
3. For similarity, use `GET /enm/nanoreg1/query/similarity?search=[SMILES]&threshold=0.8`.
4. From results, extract substance UUIDs in `dataEntry` and look up details via `GET /enm/nanoreg1/substance/{uuid}`.

### 4. Cross-Database Investigation Search

1. `GET /enm/nanoreg1/investigation?type=bysubstance_name&search=silver` to find investigations in nanoreg1.
2. Repeat with `db=enanomapper`, `db=marina`, etc. to search across databases.
3. Compare `topcategory` and `endpointcategory` fields to find overlapping study types.
4. Use `investigation` field values to group related records.

### 5. Full-Text Federated Search with Faceting

1. `GET /select?q=zinc+oxide&wt=json&rows=10` for a quick keyword search.
2. Review `numFound` to gauge total matches.
3. `POST /select` with a `facet` map to break results down by category, owner, or study type.
4. Use `fq` (filter query) on subsequent `GET /select` calls to narrow by specific facet values.
5. Paginate with `start` parameter (offset-based, not cursor-based).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
