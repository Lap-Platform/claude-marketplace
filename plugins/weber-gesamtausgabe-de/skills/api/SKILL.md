---
name: wega-api
description: "WeGA API skill. Use when working with WeGA for documents, search, code. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# WeGA API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
http://localhost:8080/exist/apps/WeGA-WebApp/api/v1

## Setup
1. No auth setup needed
2. GET /documents -- verify access

## Endpoints

10 endpoints across 5 groups. See references/api-spec.lap for full details.

### documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /documents | Lists all documents |
| GET | /documents/{docID} | Returns documents by ID |
| GET | /documents/findByDate | Finds documents by date |
| GET | /documents/findByMention/{docID} | Finds documents by reference |
| GET | /documents/findByAuthor/{authorID} | Finds documents by author |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/entity | Search for a WeGA entity |

### code
| Method | Path | Description |
|--------|------|-------------|
| GET | /code/findByElement/{element} | Finds code samples by XML element |

### application
| Method | Path | Description |
|--------|------|-------------|
| GET | /application/status | Get status information about the running WeGA-WebApp |
| GET | /application/newID | Create a new WeGA ID |

### facets
| Method | Path | Description |
|--------|------|-------------|
| GET | /facets/{facet} | Returns facets |

## Enhanced Skill Content
## Question Mapping

- "What documents are available?" -> GET /documents
- "Show me letters in the archive" -> GET /documents?docType=letters
- "Get details for a specific document" -> GET /documents/{docID}
- "Find documents written between 1810 and 1820" -> GET /documents/findByDate?fromDate=1810-01-01&toDate=1820-12-31
- "What did Weber write?" -> GET /documents/findByAuthor/{authorID}
- "Which documents mention this person?" -> GET /documents/findByMention/{docID}
- "Search for an entity by name" -> GET /search/entity?q={name}
- "Find all diaries mentioning a keyword" -> GET /search/entity?q={keyword}&docType=diaries
- "What TEI elements are used in letters?" -> GET /code/findByElement/{element}?docType=letters
- "Is the API running?" -> GET /application/status
- "Generate a new document ID for a letter" -> GET /application/newID?docType=letters
- "Get facet values for a search scope" -> GET /facets/{facet}?scope={scope}&docType={docType}
- "List the next 20 documents after the first page" -> GET /documents?offset=20&limit=20
- "Find writings from a specific date onward" -> GET /documents/findByDate?fromDate={date}

## Response Tips

- **documents**: All list endpoints support `offset`/`limit` pagination; omit both to get defaults. Results are flat arrays -- check array length against `limit` to detect the last page.
- **search**: Entity search returns matches ranked by relevance; use `q` for free-text and `docType` to narrow scope.
- **code**: Element lookups return code snippets; filter by `namespace` (e.g., TEI) to avoid cross-schema noise.
- **application**: `/status` returns server health (watch for 500); `/newID` returns a single ID string and 403 if the docType is unauthorized.
- **facets**: Returns term-frequency pairs scoped to a collection; use `term` to filter within a facet.

## Anomaly Flags

- **500 from /application/status**: The backend (eXist-db) may be down or overloaded -- surface immediately and suggest retrying after a delay.
- **403 from /application/newID**: The requested docType is not permitted for ID generation -- flag the restriction and suggest checking allowed types.
- **Empty result sets**: If a paginated endpoint returns zero items but offset > 0, the offset has overshot -- warn the user and suggest resetting to offset=0.
- **Missing pagination params**: If a response is suspiciously short and no `limit` was set, the API default cap may be truncating results -- suggest explicitly setting `limit`.
- **Date format issues**: `fromDate`/`toDate` expect ISO dates; if results seem wrong, flag potential format mismatch.
- **Large offsets with no results**: Likely indicates data boundaries -- proactively report total available range if prior calls returned data.

## Playbook

### 1. Browse and Inspect a Document

1. `GET /documents?docType={type}&limit=10` to list available documents of a given type
2. Pick a `docID` from the results
3. `GET /documents/{docID}` to retrieve full document details
4. If cross-references are needed, `GET /documents/findByMention/{docID}` to find related documents

### 2. Research an Author's Output

1. Identify the `authorID` (use `GET /search/entity?q={name}` if unknown)
2. `GET /documents/findByAuthor/{authorID}` to list all works
3. Narrow with `docType` (e.g., letters, diaries, writings) if the list is large
4. Page through results using `offset` and `limit`

### 3. Date-Range Document Discovery

1. `GET /documents/findByDate?fromDate={start}&toDate={end}` for the target period
2. Filter by `docType` to focus on a specific category
3. Page through results with `offset`/`limit`
4. For each interesting result, `GET /documents/{docID}` for full content

### 4. Faceted Search Exploration

1. `GET /facets/{facet}?scope={scope}&docType={docType}` to retrieve available facet values
2. Use `term` to filter within the facet if the list is large
3. Pick a facet value and use it to refine a `GET /documents` or `GET /search/entity` query
4. Page through final results as needed

### 5. System Health Check and ID Generation

1. `GET /application/status` to confirm the API is responsive (expect 200)
2. If status is healthy, `GET /application/newID?docType={type}` to mint a new document ID
3. If `/status` returns 500, wait and retry before attempting other operations
4. If `/newID` returns 403, verify the docType is in the allowed set


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
