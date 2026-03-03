---
name: safe-place
description: "Safe Place API skill. Use when working with Safe Place for safety. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Safe Place
API version: 1.0.1

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /safety/safety-rated-locations -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### safety
| Method | Path | Description |
|--------|------|-------------|
| GET | /safety/safety-rated-locations | Returns safety rating for a given location and radius. |
| GET | /safety/safety-rated-locations/{safety-rated-locationId} | Retieve safety information of a location by its Id. |
| GET | /safety/safety-rated-locations/by-square | Returns the safety rating of a given area |

## Enhanced Skill Content


## Question Mapping

- "How safe is the area around these coordinates?" -> GET /safety/safety-rated-locations
- "What's the safety rating near latitude 48.8566, longitude 2.3522?" -> GET /safety/safety-rated-locations
- "Show me safety scores within 2km of my hotel" -> GET /safety/safety-rated-locations (with radius)
- "Get detailed safety info for a specific location ID" -> GET /safety/safety-rated-locations/{safety-rated-locationId}
- "Look up safety rating Q930402753" -> GET /safety/safety-rated-locations/{safety-rated-locationId}
- "What are the safety scores across downtown Paris?" -> GET /safety/safety-rated-locations/by-square
- "Show safety ratings for all locations within this bounding box" -> GET /safety/safety-rated-locations/by-square
- "Compare safety between two neighborhoods" -> GET /safety/safety-rated-locations (x2, different coordinates)
- "Is this area safe for tourists at night?" -> GET /safety/safety-rated-locations (check nighttime sub-scores)
- "Find the safest areas within a region" -> GET /safety/safety-rated-locations/by-square (then sort results)
- "What does each safety sub-score mean for this location?" -> GET /safety/safety-rated-locations/{safety-rated-locationId}
- "Get safety data for a rectangular area with pagination" -> GET /safety/safety-rated-locations/by-square (with page[limit])

## Response Tips

- **Location queries** (`/safety-rated-locations`, `/by-square`): Results return arrays; each item contains sub-scores (e.g., women safety, nighttime safety, theft) -- always present the breakdown, not just the overall score.
- **Single location** (`/{safety-rated-locationId}`): Returns one object; 404 means the ID is invalid or the location has no safety data -- suggest nearby coordinate search as fallback.
- **Pagination** (`/by-square`): Uses `page[limit]` parameter; watch for `meta.count` vs actual returned items to detect truncated results.
- **Errors (400)**: Typically malformed coordinates or out-of-range values -- surface the specific validation message from the response body.

## Anomaly Flags

- **Empty results for populated areas**: If a coordinate query returns zero results, flag that safety data coverage may not extend to that region -- suggest trying a larger radius.
- **All sub-scores identical**: Uniform scores across categories (e.g., all 40) may indicate low-confidence or interpolated data -- note this to the user.
- **Radius silently capped**: If the requested radius exceeds the API's maximum, results may cover a smaller area than expected -- compare requested vs effective coverage.
- **Rate limiting (429)**: Surface immediately with retry-after timing; batch coordinate lookups where possible.
- **Deprecated location IDs**: If a previously valid ID returns 404, the safety grid may have been re-indexed -- suggest re-querying by coordinates.
- **Bounding box too large**: Overly wide by-square queries may return paginated partial data -- warn if the area exceeds typical city-scale bounds.

## Playbook

### 1. Check Safety at a Destination

1. Get the destination's latitude and longitude (from user input or a geocoding step).
2. Call `GET /safety/safety-rated-locations?latitude={lat}&longitude={lng}` with an optional `radius` for broader coverage.
3. Review the returned safety sub-scores (overall, women, nighttime, theft, etc.).
4. Present a summary highlighting any notably low sub-scores.

### 2. Compare Safety Across a City

1. Define a bounding box covering the city: north, south, east, west coordinates.
2. Call `GET /safety/safety-rated-locations/by-square?north={n}&west={w}&south={s}&east={e}`.
3. If results are paginated, repeat with `page[limit]` adjustments until all locations are retrieved.
4. Sort locations by overall safety score to identify safest and least safe zones.
5. Present a ranked summary or group by neighborhood.

### 3. Deep Dive on a Specific Location

1. From a previous search result, extract the `safety-rated-locationId`.
2. Call `GET /safety/safety-rated-locations/{safety-rated-locationId}`.
3. If 404, fall back to a coordinate-based search near the original location.
4. Present the full sub-score breakdown with context on what each category measures.

### 4. Hotel Safety Check Before Booking

1. Obtain the hotel's coordinates.
2. Call `GET /safety/safety-rated-locations?latitude={lat}&longitude={lng}&radius=1` (1km around the hotel).
3. Aggregate scores from all returned locations to get an area average.
4. Flag any sub-scores below a threshold (e.g., nighttime safety < 30) as potential concerns.
5. Optionally compare against a second hotel's location using the same flow.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
