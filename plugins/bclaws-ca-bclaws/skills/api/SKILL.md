---
name: bc-laws
description: "BC Laws API skill. Use when working with BC Laws for content, document, search. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# BC Laws
API version: 1.0.0

## Auth
No authentication required.

## Base URL
http://www.bclaws.ca/civix

## Setup
1. No auth setup needed
2. GET /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/xml -- verify access

## Endpoints

7 endpoints across 3 groups. See references/api-spec.lap for full details.

### content
| Method | Path | Description |
|--------|------|-------------|
| GET | /content/{aspectId} | Describes the documents and directories available within a specific 'aspect' (content group) of the BCLaws library |
| GET | /content/{aspectId}/{civixDocumentId} | Lists the metadata available for the specified index or directory from the BCLaws legislative respository |

### document
| Method | Path | Description |
|--------|------|-------------|
| GET | /document/id/{aspectId}/{civixIndexId}/{civixDocumentId} | Retrieves a specific document from the BCLaws legislative repository (HTML format) |
| GET | /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/xml | Retrieves a specific document from the BCLaws legislative repository (XML format) |
| GET | /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/search/{searchString} | Retrieves a specific document from the BCLaws legislative repository with search text highlighted (HTML format) |
| GET | /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/xml/search/{searchString} | Retrieves a specific document from the BCLaws legislative repository with search text highlighted (XML format) |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/{aspectId}/fullsearch | A listing of metadata available for the specified aspect and search term from the BCLaws legislative repository |

## Enhanced Skill Content
## Question Mapping

- "What content is available in the BC Laws registry?" -> GET /content/{aspectId}
- "Show me the table of contents for BC corporate registry documents" -> GET /content/corpreg
- "What documents exist under a specific content category?" -> GET /content/{aspectId}/{civixDocumentId}
- "List all statutes and regulations in the complete collection" -> GET /content/complete/statreg
- "Get the full text of a specific BC law document" -> GET /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}
- "Show me the XML source of a specific regulation" -> GET /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/xml
- "Search within a specific statute for mentions of 'water'" -> GET /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/search/{searchString}
- "Find all references to 'carbon tax' in the XML of a specific act" -> GET /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/xml/search/{searchString}
- "Search all BC laws for a keyword" -> GET /search/{aspectId}/fullsearch
- "Find the first 20 results mentioning 'housing' across all legislation" -> GET /search/complete/fullsearch?q=housing&s=0&e=20&nFrag=5&lFrag=100
- "Search only BC Gazette Part 1 for a term" -> GET /search/bcgaz1/fullsearch
- "Browse orders in council content" -> GET /content/oic
- "What is the document structure under the 'arch_oic' aspect?" -> GET /content/arch_oic
- "Get a paginated search for 'environmental' starting from result 40" -> GET /search/complete/fullsearch?q=environmental&s=40&e=20&nFrag=5&lFrag=100

## Response Tips

- **Content endpoints** (`/content/...`): Returns hierarchical directory listings; traverse nested items by following `civixDocumentId` values into deeper content calls.
- **Document endpoints** (`/document/id/...`): Returns full document bodies; the non-XML variant returns rendered HTML while `/xml` returns raw legislative XML markup.
- **Document search endpoints** (`/document/.../search/...`): Returns the document with matching fragments highlighted; results are scoped to that single document only.
- **Full search endpoint** (`/search/.../fullsearch`): Paginated via `s` (start offset) and `e` (page size); `nFrag` and `lFrag` control snippet count and length -- always check if more results exist beyond `s + e`.
- **All endpoints**: Responses are XML-based by default (not JSON); parse accordingly and check for empty result sets which return valid XML with zero child elements rather than error codes.

## Anomaly Flags

- **Invalid aspectId**: The API silently accepts unknown aspect IDs but returns empty structures -- surface a warning if the response body contains no document entries.
- **Missing documents**: If a `civixDocumentId` or `civixIndexId` returns a 404 or empty body, flag it as a potentially repealed, renamed, or consolidated statute.
- **Search returning zero results**: Alert the user and suggest broadening the query, trying alternate aspect IDs, or checking spelling -- the search does not appear to support fuzzy matching.
- **Pagination exhaustion**: When `s + e` exceeds total results, proactively inform the user they have reached the end of available results rather than returning an empty page silently.
- **Large fragment settings**: If `nFrag` or `lFrag` are set unusually high, warn that response size may be large and slow to return.
- **Aspect scope mismatch**: If the user searches a narrow aspect (e.g., `bcgaz2`) but expects broad legislative results, suggest switching to `complete`.

## Playbook

### 1. Browse and Read a Specific Statute

1. Call `GET /content/complete` to list top-level content categories.
2. Identify the relevant category and call `GET /content/complete/{civixDocumentId}` to drill into it (e.g., `statreg`).
3. Continue navigating with content calls until you find the target document's `civixIndexId` and `civixDocumentId`.
4. Call `GET /document/id/complete/{civixIndexId}/{civixDocumentId}` to retrieve the full document text.

### 2. Full-Text Search Across All BC Legislation

1. Call `GET /search/complete/fullsearch?q={term}&s=0&e=20&nFrag=5&lFrag=100` with the desired search term.
2. Parse the result set for document references and highlight fragments.
3. If more results exist, increment `s` by `e` (e.g., `s=20`) and repeat.
4. For any promising result, retrieve the full document via `GET /document/id/complete/{civixIndexId}/{civixDocumentId}`.

### 3. Search Within a Known Document

1. Obtain the document's `civixIndexId` and `civixDocumentId` (from browsing or a prior search).
2. Call `GET /document/id/complete/{civixIndexId}/{civixDocumentId}/search/{searchString}` to find matches within that document.
3. For structured processing, use the `/xml/search/` variant instead to get highlighted XML.

### 4. Compare Legislation Across Gazette Types

1. Call `GET /content/bcgaz1` and `GET /content/bcgaz2` to list gazette entries for Part 1 and Part 2.
2. Use `GET /search/bcgaz1/fullsearch?q={term}&s=0&e=20&nFrag=5&lFrag=100` for Part 1 results.
3. Repeat with `bcgaz2` for Part 2 results.
4. Cross-reference document IDs between results to identify related gazette entries.

### 5. Retrieve Raw XML for Automated Processing

1. Navigate to the target document using content endpoints as in Playbook 1.
2. Call `GET /document/id/{aspectId}/{civixIndexId}/{civixDocumentId}/xml` to get the raw XML.
3. Parse the XML structure to extract sections, clauses, definitions, or other legislative elements programmatically.
4. Optionally combine with `/xml/search/{searchString}` to get pre-filtered XML with match annotations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
