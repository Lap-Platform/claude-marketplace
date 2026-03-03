---
name: digitalnz-api
description: "DigitalNZ API skill. Use when working with DigitalNZ for records.{format}, records. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# DigitalNZ API
API version: 3

## Auth
ApiKey api_key in query

## Base URL
https://api.digitalnz.org

## Setup
1. Set your API key in the appropriate header
2. GET /records.{format} -- verify access

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### records.{format}
| Method | Path | Description |
|--------|------|-------------|
| GET | /records.{format} | Run queries against DigitalNZ metadata search service. |

### records
| Method | Path | Description |
|--------|------|-------------|
| GET | /records/{record_id}.{format} | View metadata associated with a single record. |
| GET | /records/{record_id}/more_like_this.{format} | The "More Like This" call returns similar records to the specified ID. |

## Enhanced Skill Content
## Question Mapping

- "Search for records about Maori art?" -> GET /records.json
- "Find records near a specific location?" -> GET /records.json (with geo_bbox)
- "Get details for a specific record?" -> GET /records/{record_id}.json
- "Find records similar to this one?" -> GET /records/{record_id}/more_like_this.json
- "What collections are available?" -> GET /records.json (with facets=collection)
- "List records sorted by newest first?" -> GET /records.json (with sort=syndication_date&direction=desc)
- "How many records match my search?" -> GET /records.json (check result_count in response)
- "Get records in XML format?" -> GET /records.xml
- "Browse the second page of search results?" -> GET /records.json (with page=2)
- "What categories exist for a topic?" -> GET /records.json (with facets=category)
- "Get only the title and thumbnail for records?" -> GET /records.json (with fields=title,thumbnail_url)
- "Who created a specific record?" -> GET /records/{record_id}.json (check creator field)
- "What are the copyright terms for a record?" -> GET /records/{record_id}.json (check usage, copyright, rights fields)
- "Find more records like record 12345?" -> GET /records/12345/more_like_this.json

## Response Tips

- **Search (GET /records.{format})**: Paginated via `page` and `per_page` (default 20, page 1). Use `result_count` to calculate total pages. `records` is a flat array of maps; `facets` is a nested map keyed by facet name. Facets have their own pagination via `facets_page`/`facets_per_page`.
- **Record detail (GET /records/{record_id}.{format})**: Returns a single flat object with many array fields (`content_partner`, `collection`, `category`, `creator`, `subject`, `date`, `copyright`, `rights_url`, `locations`). Always check for empty arrays rather than null.
- **More like this (GET /records/{record_id}/more_like_this.{format})**: Same paginated envelope as search. Use `mlt_fields` to tune similarity matching; `filtering` to narrow scope.
- **Errors**: 400 means malformed query parameters. 403 means missing or invalid API key. 404 means the record_id does not exist.

## Anomaly Flags

- **403 on any request**: API key is missing, expired, or invalid. Surface immediately -- all subsequent calls will also fail.
- **result_count: 0**: Search returned no results. Suggest broadening the query, removing filters, or checking spelling.
- **Empty facets map**: Facets were requested but none returned. May indicate the facet name is invalid or no data matches.
- **Missing thumbnail_url or large_thumbnail_url**: Record exists but has no image. Surface when the user likely needs visual content.
- **Empty rights or usage arrays**: Licensing info unavailable. Flag before the user attempts to reuse content.
- **Pagination overflow**: Requested `page` exceeds `ceil(result_count / per_page)`. Returns empty records array silently -- surface that the user has gone past the last page.
- **geo_bbox malformed**: Returns 400. Surface the expected format (south-west lat,lng to north-east lat,lng).

## Playbook

### 1. Search and Browse Records

1. Call `GET /records.json?text=<query>&api_key=<key>` to perform an initial search
2. Check `result_count` to understand how many results exist
3. If too many results, narrow with `facets=category` to discover available categories
4. Add filters or adjust `text` to refine
5. Page through results using `page=2`, `page=3`, etc. (up to `ceil(result_count / per_page)`)

### 2. Get Full Record Details with Related Content

1. Search for a record using `GET /records.json?text=<query>&api_key=<key>`
2. Pick a record and note its `id` from the search results
3. Call `GET /records/<id>.json?api_key=<key>` to get full metadata
4. Call `GET /records/<id>/more_like_this.json?api_key=<key>` to find similar records
5. Optionally use `mlt_fields` to control what "similar" means (e.g., match on subject or creator)

### 3. Explore Collections via Facets

1. Call `GET /records.json?text=*&facets=collection&facets_per_page=50&api_key=<key>`
2. Read the `facets.collection` map to see available collections and their counts
3. If more than 50 collections exist, increment `facets_page` to paginate through them
4. Search within a specific collection by adding it as a filter parameter

### 4. Geographic Discovery

1. Determine the bounding box for your area of interest (SW lat,lng to NE lat,lng)
2. Call `GET /records.json?geo_bbox=<sw_lat>,<sw_lng>,<ne_lat>,<ne_lng>&api_key=<key>`
3. Check `result_count` to see how many geolocated records fall within the box
4. Retrieve full details for records of interest using `GET /records/<id>.json`
5. Inspect the `locations` array on each record for precise coordinates

### 5. Export Minimal Record Data

1. Identify the fields you need (e.g., `title,landing_url,thumbnail_url,category`)
2. Call `GET /records.json?text=<query>&fields=<comma-separated>&per_page=100&api_key=<key>`
3. Iterate through pages until `page * per_page >= result_count`
4. Collect the trimmed records from each page into your dataset


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
