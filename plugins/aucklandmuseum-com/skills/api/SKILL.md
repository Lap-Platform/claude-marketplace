---
name: auckland-museum-api
description: "Auckland Museum API skill. Use when working with Auckland Museum for search, id, sparql. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Auckland Museum API
API version: 2.0.0

## Auth
No authentication required.

## Base URL
https://api.aucklandmuseum.com

## Setup
1. No auth setup needed
2. GET /sparql -- verify access
3. POST /search/{index}/{operation} -- create first search

## Endpoints

6 endpoints across 3 groups. See references/api-spec.lap for full details.

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/{index}/{operation} | Perform simple search queries over Auckland Museum Collections and Cenotaph data |
| POST | /search/{index}/{operation} | Perform complex search queries over Auckland Museum Collections and Cenotaph data |

### id
| Method | Path | Description |
|--------|------|-------------|
| GET | /id/{identifier} | Explore details about a given subject node |
| GET | /id/media/{path} | Retrieve media associated with Collections and Cenotaph subjects in Auckland Museum |

### sparql
| Method | Path | Description |
|--------|------|-------------|
| GET | /sparql | Auckland Museum SPARQL endpoint |
| POST | /sparql | Auckland Museum SPARQL endpoint |

## Enhanced Skill Content
## Question Mapping

- "How do I search for artifacts in the museum collection?" -> GET /search/{index}/{operation}
- "Can I run a full-text search with a query string?" -> GET /search/{index}/{operation} (with `q` param)
- "How do I perform an advanced search with filters?" -> POST /search/{index}/{operation} (with body)
- "How do I look up a specific object by its ID?" -> GET /id/{identifier}
- "How do I retrieve an image or media file for an object?" -> GET /id/media/{path}
- "Can I get a thumbnail or different size of a media asset?" -> GET /id/media/{path} (with `rendering` param)
- "How do I run a SPARQL query against the museum's linked data?" -> GET /sparql
- "How do I execute a complex SPARQL query that's too long for a URL?" -> POST /sparql
- "Can I get JSONP-wrapped SPARQL results for a browser widget?" -> GET /sparql (with `callback` param)
- "How do I search with reasoning/inference enabled on the knowledge graph?" -> GET /sparql (with `infer` param)
- "How do I find all objects related to a specific topic and then get their images?" -> GET /search/{index}/{operation} then GET /id/media/{path}
- "What search indexes are available in the museum API?" -> GET /search/{index}/{operation} (try known indexes)
- "How do I get the full record for a search result?" -> GET /search/{index}/{operation} then GET /id/{identifier}

## Response Tips

- **search**: Results come back as collections; inspect the response for `totalResults` or equivalent count fields and iterate with pagination parameters in the body or query string.
- **id**: Single-object responses; a 404 means the identifier doesn't exist in the collection -- verify the ID format before retrying.
- **id/media**: Returns binary content (image/audio/video), not JSON; check `Content-Type` header and handle the response as a blob or stream.
- **sparql**: Returns RDF-style result sets (typically `application/sparql-results+json`); parse the `bindings` array inside `results` for actual data rows.

## Anomaly Flags

- **404 on search**: Surface when both `index` and `operation` return 404 -- likely an invalid index name rather than empty results.
- **400 on search**: Malformed query syntax; surface the error body which typically contains parsing details.
- **Large SPARQL results**: Warn when SPARQL queries lack `LIMIT` clauses, as unbounded queries may time out or return excessive data.
- **Missing media renderings**: Flag when `rendering` param is ignored (response size matches original) -- the requested rendering may not exist.
- **SPARQL inference impact**: Note when `infer=true` is used, as it can significantly increase response time and change result sets compared to `infer=false`.
- **Deprecated or empty fields**: Surface any response fields that return null/empty across multiple objects, as they may indicate retired data attributes.

## Playbook

### 1. Search the Collection and Retrieve Full Records

1. Call `GET /search/{index}/{operation}` with your index (e.g., `catalogues`) and operation (e.g., `_search`), passing your query in `q`.
2. Parse the response to extract object identifiers from the results.
3. For each identifier of interest, call `GET /id/{identifier}` to retrieve the full record.
4. If the record references media, call `GET /id/media/{path}` to fetch associated images or files.

### 2. Run an Advanced Filtered Search

1. Call `POST /search/{index}/{operation}` with a JSON body containing your Elasticsearch-style query (bool, match, range filters).
2. Include pagination parameters (`from`, `size`) in the body to control result windows.
3. Parse the hits array and total count from the response.
4. Repeat with incremented `from` values to paginate through all results.

### 3. Query Linked Data with SPARQL

1. Write your SPARQL query (SELECT, DESCRIBE, or CONSTRUCT).
2. For short queries, call `GET /sparql?query={encoded_query}`.
3. For longer queries, call `POST /sparql` with the query in the request body.
4. Optionally set `infer=true` to enable reasoning over the knowledge graph.
5. Parse the `results.bindings` array to extract variable values from each row.

### 4. Retrieve and Render Media Assets

1. Obtain an object record via `GET /id/{identifier}`.
2. Extract media references (paths) from the object metadata.
3. Call `GET /id/media/{path}` to retrieve the default rendering.
4. To get a specific size or format, add the `rendering` parameter (e.g., `thumbnail`, `preview`).
5. Handle the binary response according to its `Content-Type` header.

### 5. Build a JSONP Widget from SPARQL Data

1. Construct a SPARQL query that returns the data your widget needs.
2. Call `GET /sparql?query={encoded_query}&callback={functionName}` to get a JSONP-wrapped response.
3. Embed the API call as a script tag in your HTML, with the callback function defined to process and render the data.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
