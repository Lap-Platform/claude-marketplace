---
name: bc-geographical-names-web-service-rest-api
description: "BC Geographical Names Web Service - REST API skill. Use when working with BC Geographical Names Web Service - REST for names, features, featureClasses. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# BC Geographical Names Web Service - REST API
API version: 3.x.x

## Auth
No authentication required.

## Base URL
https://apps.gov.bc.ca/pub/bcgnws

## Setup
1. No auth setup needed
2. GET /names/search -- verify access

## Endpoints

14 endpoints across 6 groups. See references/api-spec.lap for full details.

### names
| Method | Path | Description |
|--------|------|-------------|
| GET | /names/search | Search by name |
| GET | /names/official/search | Search by name, limit to official names only |
| GET | /names/notOfficial/search | Search by name, limit to unofficial names only |
| GET | /names/inside | Search in a geographic area |
| GET | /names/near | Search near to a geographic point |
| GET | /names/decisions/recent | Search for names affected by recent naming decision |
| GET | /names/decisions/year | Search for names affected by naming decisions in a given year |
| GET | /names/changes | Search for names with metadata changes in a given period |
| GET | /names/{nameId}.{outputFormat} | Get a name by its nameId |

### features
| Method | Path | Description |
|--------|------|-------------|
| GET | /features/{featureId} | Get a feature by its featureId |

### featureClasses
| Method | Path | Description |
|--------|------|-------------|
| GET | /featureClasses | Get all feature classes |

### featureCategories
| Method | Path | Description |
|--------|------|-------------|
| GET | /featureCategories | Get all feature categories |

### featureTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /featureTypes | Get all feature types |

### nameAuthorities
| Method | Path | Description |
|--------|------|-------------|
| GET | /nameAuthorities | Get all name authorities |

## Enhanced Skill Content
## Question Mapping

- "Search for a place name in BC?" -> GET /names/search
- "Find the official name of a mountain or lake?" -> GET /names/official/search
- "Are there any unofficial or alternate names for this place?" -> GET /names/notOfficial/search
- "What geographical features are inside this bounding box?" -> GET /names/inside
- "What named places are within 10km of these coordinates?" -> GET /names/near
- "What naming decisions were made in the last 30 days?" -> GET /names/decisions/recent
- "What geographical names were decided in 2024?" -> GET /names/decisions/year
- "What name changes happened between two dates?" -> GET /names/changes
- "Get full details for a specific name by ID?" -> GET /names/{nameId}.{outputFormat}
- "Look up a feature by its feature ID?" -> GET /features/{featureId}
- "What feature classes exist in the system?" -> GET /featureClasses
- "List all feature categories?" -> GET /featureCategories
- "What types of features can I filter by?" -> GET /featureTypes
- "Which naming authorities govern BC geographical names?" -> GET /nameAuthorities
- "Find all lakes near a coordinate, sorted by name?" -> GET /names/near (with featureType=lake, sortBy=name)

## Response Tips

- **Name searches** (`/names/*`): Results are paginated via `itemsPerPage` (default 20) and `startIndex` (1-based). Use `outputStyle=detail` for full geometry and metadata; `summary` omits coordinates. Check total result count in the response envelope to know if more pages exist.
- **Single name/feature lookups** (`/names/{id}`, `/features/{id}`): Return a single object, not an array. A 404 means the ID does not exist -- do not retry, surface to user.
- **Reference lists** (`/featureClasses`, `/featureCategories`, `/featureTypes`, `/nameAuthorities`): Return complete unpaginated arrays. Cache these locally since they rarely change.
- **All endpoints**: 400 errors indicate malformed parameters (bad SRS code, missing required field, invalid bbox format). Parse the error body for the specific field that failed.

## Anomaly Flags

- **Empty result sets**: If a name search returns zero results, suggest relaxing `exactSpelling=0`, broadening `featureClass`/`featureType`, or checking for typos before concluding the name does not exist.
- **Large pagination gaps**: If `startIndex` exceeds total results, the response will be empty -- flag this as a pagination overshoot rather than "no results found."
- **Unusual SRS codes**: If the user requests `outputSRS=3005` (BC Albers) or other projected systems, note that coordinates will not be in lat/lon and downstream tools expecting WGS84 may break.
- **Stale decision queries**: If `/names/decisions/recent` with default `days=30` returns nothing, proactively suggest increasing the window to 90 or 180 days.
- **Date format mismatches on `/names/changes`**: The `fromDate` and `toDate` are typed as `int` -- flag if the user passes ISO date strings instead of numeric timestamps.
- **KML/CSV output**: When `outputFormat=kml` or `csv`, response Content-Type changes and may not be directly parseable as structured data -- alert the user if they attempt to JSON-parse it.

## Playbook

### 1. Find all official lakes near a location

1. Call `GET /featureTypes?outputFormat=json` to confirm the exact `featureType` value for lakes.
2. Call `GET /names/official/search?outputFormat=json&name=Lake&featurePoint=POINT(-123.1 49.2)&distance=50&featureType=Lake&outputStyle=detail&itemsPerPage=50` -- or use `GET /names/near` with the same spatial params.
3. Page through results by incrementing `startIndex` by `itemsPerPage` until no more results are returned.
4. For any name of interest, call `GET /names/{nameId}.json` for the full record.

### 2. Track recent naming decisions

1. Call `GET /names/decisions/recent?outputFormat=json&days=90&outputStyle=summary` to get a broad view of recent activity.
2. Filter client-side by `featureCategory` or `featureType` if needed, or pass them as query params to narrow server-side.
3. For each decision of interest, fetch full detail via `GET /names/{nameId}.json`.
4. To monitor ongoing changes, periodically call `/names/changes?fromDate={lastCheck}&toDate={now}` using numeric date values.

### 3. Explore features within a map viewport

1. Determine the bounding box from the current map extent as `minLong,minLat,maxLong,maxLat`.
2. Call `GET /names/inside?outputFormat=json&bbox=-123.5,48.5,-122.5,49.5&outputStyle=summary&itemsPerPage=50`.
3. Page through all results to build a complete list.
4. To drill down, call `GET /features/{featureId}` for geometry and linked names on any feature of interest.
5. Optionally re-request with `outputFormat=kml` for direct map overlay.

### 4. Build a reference data cache

1. Call `GET /featureClasses?outputFormat=json` and store the result.
2. Call `GET /featureCategories?outputFormat=json` and store the result.
3. Call `GET /featureTypes?outputFormat=json` and store the result.
4. Call `GET /nameAuthorities?outputFormat=json` and store the result.
5. Use these cached lists to populate filter dropdowns and validate user input before making search calls.

### 5. Compare official vs. unofficial names for a place

1. Call `GET /names/official/search?outputFormat=json&name={placeName}&exactSpelling=1&outputStyle=detail`.
2. Call `GET /names/notOfficial/search?outputFormat=json&name={placeName}&exactSpelling=0&outputStyle=detail`.
3. Cross-reference results by `featureId` to find names that refer to the same physical feature.
4. Present both official and alternate names side-by-side, noting the naming authority and decision date for each.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
