---
name: points-of-interest
description: "Points of Interest API skill. Use when working with Points of Interest for reference-data. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Points of Interest
API version: 1.1.1

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /reference-data/locations/pois -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/locations/pois | Returns points of interest for a given location and radius. |
| GET | /reference-data/locations/pois/{poisId} | Retieve one point of interest by its Id. |
| GET | /reference-data/locations/pois/by-square | Returns points of interest for a given area |

## Enhanced Skill Content
## Question Mapping

- "What points of interest are near this location?" -> GET /reference-data/locations/pois
- "Find restaurants near latitude 41.397 and longitude 2.160" -> GET /reference-data/locations/pois (with categories filter)
- "What attractions are within 5 km of me?" -> GET /reference-data/locations/pois (with radius)
- "Get details for a specific point of interest" -> GET /reference-data/locations/pois/{poisId}
- "Look up POI with ID 123ABC" -> GET /reference-data/locations/pois/{poisId}
- "What's in this area on the map?" -> GET /reference-data/locations/pois/by-square
- "Find all sights between these four coordinates" -> GET /reference-data/locations/pois/by-square
- "Show me nightlife spots in downtown Barcelona" -> GET /reference-data/locations/pois (with categories)
- "Are there any POIs in this bounding box? Limit to 10 results" -> GET /reference-data/locations/pois/by-square (with page[limit])
- "What categories of POI are available near the Eiffel Tower?" -> GET /reference-data/locations/pois (inspect category values in response)
- "I have a POI ID from a previous search, give me full details" -> GET /reference-data/locations/pois/{poisId}
- "Compare points of interest across two neighborhoods" -> GET /reference-data/locations/pois/by-square (call twice, compare results)
- "Find shopping near coordinates 48.858, 2.294 within 2 km" -> GET /reference-data/locations/pois (with radius + categories)

## Response Tips

- **Radius search** (`/pois`): Results are distance-sorted from the center point. Check the `categories` field on each result to filter client-side if needed.
- **Single POI** (`/pois/{poisId}`): Returns one object. A 404 means the ID is stale or invalid -- prompt the user to re-search.
- **Bounding box** (`/pois/by-square`): Supports pagination via `page[limit]`. Inspect response metadata for total count and next-page links. Results are not distance-sorted since there is no center point.
- **Errors (400)**: Typically malformed coordinates (out-of-range lat/lng, north < south in bounding box). Surface the specific validation message from the error body.

## Anomaly Flags

- **400 on coordinate input**: Proactively validate latitude (-90 to 90) and longitude (-180 to 180) before calling. Flag if north < south or if the bounding box spans an unreasonably large area.
- **Empty results**: If a radius or bounding box search returns zero POIs, suggest widening the radius or expanding the box. Note that coverage varies by region.
- **404 on POI lookup**: The POI ID may have been retired or is from a different environment (test vs production). Flag this and suggest re-searching by location.
- **Rate limiting**: Amadeus test environment has strict rate limits. If responses slow down or return 429, surface this immediately and suggest backing off or switching to production keys.
- **Test vs production base URL**: The spec uses `test.api.amadeus.com`. Flag if the user appears to need production data, as test environment data may be limited or stale.
- **Large bounding box queries**: If the coordinate span is very wide, warn that results may be truncated by default pagination limits.

## Playbook

### 1. Find nearby attractions for a traveler

1. Obtain the user's coordinates (latitude, longitude)
2. Call `GET /reference-data/locations/pois` with `latitude`, `longitude`, and optionally `radius` (default unit is km)
3. Optionally filter by `categories` (e.g., SIGHTS, RESTAURANT, SHOPPING)
4. Present results sorted by proximity
5. For any POI the user wants more detail on, call `GET /reference-data/locations/pois/{poisId}`

### 2. Explore a neighborhood on a map

1. Determine the bounding box from the visible map area (north, south, east, west)
2. Call `GET /reference-data/locations/pois/by-square` with all four coordinates
3. Set `page[limit]` to control density (e.g., 20 for overview, 50 for detail)
4. Plot results on the map using returned coordinates
5. If the user pans/zooms, recalculate the bounding box and re-query

### 3. Get full details for a known POI

1. Take the `poisId` from a previous search result or saved reference
2. Call `GET /reference-data/locations/pois/{poisId}`
3. If 404 is returned, inform the user the POI may no longer exist and offer to re-search by location
4. Present name, category, coordinates, and any additional metadata

### 4. Compare POIs across two areas

1. Define bounding boxes for both areas (e.g., two neighborhoods)
2. Call `GET /reference-data/locations/pois/by-square` for each area in parallel
3. Group results by category and count
4. Present a side-by-side summary (e.g., "Area A has 12 restaurants, Area B has 5")
5. Drill into specific POIs with `GET /reference-data/locations/pois/{poisId}` as needed

### 5. Category-filtered local search

1. Collect the user's location and desired category (e.g., NIGHTLIFE, SHOPPING)
2. Call `GET /reference-data/locations/pois` with `latitude`, `longitude`, and `categories`
3. If no results, widen the `radius` parameter and retry once
4. If still empty, flag that POI coverage may be limited in this region
5. Return matching POIs with distance context


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
