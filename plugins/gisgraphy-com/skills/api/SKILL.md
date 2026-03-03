---
name: gisgraphy-webservices
description: "Gisgraphy webservices API skill. Use when working with Gisgraphy webservices for geocoding, reversegeocoding, street. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Gisgraphy webservices
API version: 4.0.0

## Auth
ApiKey api_key in query

## Base URL
http://free.gisgraphy.com/

## Setup
1. Set your API key in the appropriate header
2. GET /geocoding/geocode -- verify access

## Endpoints

6 endpoints across 6 groups. See references/api-spec.lap for full details.

### geocoding
| Method | Path | Description |
|--------|------|-------------|
| GET | /geocoding/geocode | Geocode an address |

### reversegeocoding
| Method | Path | Description |
|--------|------|-------------|
| GET | /reversegeocoding/reversegeocode | Reverse geocode an address |

### street
| Method | Path | Description |
|--------|------|-------------|
| GET | /street/find | Geocode an address |

### geoloc
| Method | Path | Description |
|--------|------|-------------|
| GET | /geoloc/search | Geocode an address |

### fulltext
| Method | Path | Description |
|--------|------|-------------|
| GET | /fulltext/search | search for places by text around a GPS point |

### addressparser
| Method | Path | Description |
|--------|------|-------------|
| GET | /addressparser/parse | split a raw address into several parts |

## Enhanced Skill Content
## Question Mapping

- "What are the coordinates for this address?" -> GET /geocoding/geocode
- "Geocode an address in a specific country" -> GET /geocoding/geocode
- "What address is at these coordinates?" -> GET /reversegeocoding/reversegeocode
- "What location is at latitude X, longitude Y?" -> GET /reversegeocoding/reversegeocode
- "What streets are near this location?" -> GET /street/find
- "Find one-way streets within 500 meters" -> GET /street/find
- "What places are near these coordinates?" -> GET /geoloc/search
- "Find restaurants near latitude X, longitude Y" -> GET /geoloc/search
- "Search for a place by name" -> GET /fulltext/search
- "Find cities matching 'Springfield' in the US" -> GET /fulltext/search
- "Search with spell correction enabled" -> GET /fulltext/search
- "Break an address into its components" -> GET /addressparser/parse
- "Parse and geocode an address in one call" -> GET /addressparser/parse (with geocode option)
- "Get paginated street results near a point" -> GET /street/find (with from/to)
- "Standardize a messy address string" -> GET /addressparser/parse (with standardize option)

## Response Tips

- **Geocoding / Reverse Geocoding**: Results return coordinate pairs and address components; check that the result count matches expectations when using `from`/`to` pagination.
- **Street / Geoloc**: Distance-based results are ordered by proximity; always check the `distance` field to confirm results fall within your requested `radius`.
- **Fulltext Search**: Spellchecking may alter the query silently; inspect the response for corrected terms when `spellchecking` is enabled.
- **Address Parser**: Output fields vary by country format; the `geocode` option nests coordinate data inside the parsed result.
- **All endpoints**: Use `format` (common field) to control output shape; `callback` wraps responses in JSONP; pagination uses `from`/`to` (not offset/limit).

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry-after guidance; the free tier has strict rate limits.
- **412 Precondition Failed**: Indicates missing or malformed required parameters; surface the specific field that failed validation.
- **Empty result sets**: Flag when geocoding or reverse geocoding returns zero results, as this often means the input needs reformatting or the coordinates are in an ocean/unpopulated area.
- **Radius queries returning max results**: When `from`/`to` page is full, warn that results may be truncated and suggest narrowing the radius or paginating further.
- **401/403 Auth errors**: Surface API key issues proactively; remind user that `api_key` must be passed as a query parameter, not a header.
- **Spellcheck corrections**: Flag when fulltext search silently corrects the query term so the user knows results may not match their exact input.

## Playbook

### 1. Geocode an Address and Find Nearby Places

1. Call `GET /geocoding/geocode` with `address` (and optionally `country` for accuracy)
2. Extract `lat` and `lng` from the response
3. Call `GET /geoloc/search` with those coordinates and a `radius`
4. Optionally filter by `placetype` to narrow results

### 2. Reverse Geocode and Explore Surrounding Streets

1. Call `GET /reversegeocoding/reversegeocode` with `lat` and `lng`
2. Note the returned address for context
3. Call `GET /street/find` with the same coordinates and desired `radius`
4. Filter by `streettype` or `oneway` if needed
5. Paginate with `from`/`to` if results exceed one page

### 3. Parse, Standardize, and Geocode a Raw Address

1. Call `GET /addressparser/parse` with `address`, `standardize=true`, and `geocode=true`
2. Review the parsed components (street, city, postal code, country)
3. If geocode data is present, use the coordinates directly
4. If geocode failed, retry `GET /geocoding/geocode` with the standardized address and explicit `country`

### 4. Fuzzy Place Search with Geo-Bias

1. Call `GET /fulltext/search` with `q` (place name), `allwordsrequired=false`, and `spellchecking=true`
2. Add `lat`, `lng`, and `radius` to bias results toward a region
3. Use `country` and `lang` to further narrow and localize results
4. Paginate with `from`/`to` for large result sets
5. Check for spell-corrected terms in the response

### 5. Batch Address Validation

1. For each address, call `GET /addressparser/parse` with `standardize=true`
2. Compare parsed output to original fields; flag mismatches as potential errors
3. For addresses that parse cleanly, call `GET /geocoding/geocode` to confirm they resolve to valid coordinates
4. Surface any addresses returning empty geocode results as unverifiable
5. Respect rate limits (watch for 429s) by spacing requests or reducing batch size


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
