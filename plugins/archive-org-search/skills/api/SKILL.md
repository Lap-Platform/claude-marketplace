---
name: search-services
description: "Search Services API skill. Use when working with Search Services for search. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Search Services
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://api.archive.org/

## Setup
1. No auth setup needed
2. GET /search/v1/scrape -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/v1/scrape | Scrape search results from Internet Archive, allowing a scrolling cursor |
| GET | /search/v1/organic | Return relevance-based results from search queries |
| GET | /search/v1/fields | Fields that can be requested |

## Enhanced Skill Content
## Question Mapping

- "Search the Internet Archive for items matching a query?" -> GET /search/v1/scrape
- "How do I paginate through large result sets?" -> GET /search/v1/scrape (use `cursor` param)
- "Get just the total count of matching items without returning results?" -> GET /search/v1/scrape (set `total_only`)
- "What fields can I search or return from the Archive?" -> GET /search/v1/fields
- "Search for items sorted by date or relevance?" -> GET /search/v1/scrape (use `sort` param)
- "Run a simple keyword search without pagination?" -> GET /search/v1/organic
- "Limit the number of results returned?" -> GET /search/v1/scrape or GET /search/v1/organic (use `size` param)
- "Get results as JSONP for a browser callback?" -> GET /search/v1/scrape or GET /search/v1/organic (use `callback` param)
- "Which endpoint should I use for scripted bulk data retrieval?" -> GET /search/v1/scrape (cursor-based pagination scales)
- "Search for items and only return specific metadata fields?" -> GET /search/v1/scrape (use `field` param)
- "What is the difference between scrape and organic search?" -> GET /search/v1/scrape (cursor pagination, sorting) vs GET /search/v1/organic (simpler, no cursor/sort)
- "Retrieve the next page of search results?" -> GET /search/v1/scrape (pass `cursor` from previous response)
- "How do I build an advanced query with boolean operators?" -> GET /search/v1/scrape (use `q` with Archive advanced query syntax)

## Response Tips

- **Scrape search** (`/search/v1/scrape`): Returns items array plus a `cursor` string for the next page. When `cursor` is absent or empty, you have reached the last page. Use `total_only` to get just the count without item data.
- **Organic search** (`/search/v1/organic`): Returns a flat list of results without cursor. Best for small one-shot queries; no built-in pagination beyond `size`.
- **Fields** (`/search/v1/fields`): Returns the list of available field names. Use these values in the `field` and `sort` parameters of search endpoints.
- **JSONP**: When `callback` is provided, all endpoints wrap the JSON response in a function call. Parse accordingly in non-browser contexts.

## Anomaly Flags

- **Missing cursor in scrape response**: If the response lacks a `cursor` but you expected more results, the result set may have been truncated by server-side limits. Surface this to the user.
- **Empty results with 200 status**: A valid query can return zero items. Flag when the query syntax looks well-formed but yields nothing, as it may indicate a malformed `q` value or overly restrictive filter.
- **Large total vs small size**: When `total_only` shows a very large count, warn the user that iterating with `/scrape` will require many cursor-paginated requests.
- **Unknown field names**: If the user passes a `field` or `sort` value not present in `/search/v1/fields`, the API may silently ignore it. Cross-check against the fields list proactively.
- **Rate limiting / 429 or 503 responses**: The Archive may throttle heavy scrape usage. Surface any non-200 status immediately and suggest adding delays between paginated requests.

## Playbook

### 1. Basic keyword search

1. Call `GET /search/v1/organic?q=YOUR_QUERY&size=10` for a quick result set.
2. Parse the response items array.
3. If you need specific fields only, add `&field=title&field=identifier` to reduce payload.

### 2. Paginated bulk retrieval

1. Call `GET /search/v1/scrape?q=YOUR_QUERY&size=100` to get the first page.
2. Extract the `cursor` value from the response.
3. Call `GET /search/v1/scrape?q=YOUR_QUERY&size=100&cursor=CURSOR_VALUE` for the next page.
4. Repeat step 2-3 until no `cursor` is returned (end of results).
5. If only the count is needed first, add `&total_only=true` to estimate the total before iterating.

### 3. Discovering available search fields

1. Call `GET /search/v1/fields` to retrieve all searchable/returnable field names.
2. Pick fields relevant to your use case (e.g., `title`, `creator`, `date`, `mediatype`).
3. Use them as `field` params in scrape or organic search to narrow the returned metadata.
4. Use them as `sort` values in scrape search to order results (e.g., `sort=date asc`).

### 4. Counting items without downloading data

1. Call `GET /search/v1/scrape?q=YOUR_QUERY&total_only=true`.
2. Read the total count from the response.
3. Decide whether to proceed with full retrieval based on the volume.

### 5. Sorted search with specific fields

1. Call `GET /search/v1/fields` to confirm valid sort field names.
2. Call `GET /search/v1/scrape?q=YOUR_QUERY&sort=date+desc&field=identifier&field=title&size=25`.
3. Parse the items, using `cursor` if more pages are needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
