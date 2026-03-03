---
name: airport-nearest-relevant
description: "Airport Nearest Relevant API skill. Use when working with Airport Nearest Relevant for reference-data. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Airport Nearest Relevant
API version: 1.1.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /reference-data/locations/airports -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/locations/airports | Returns a list of relevant airports near to a given point. |

## Enhanced Skill Content
## Question Mapping

- "What airports are near me?" -> GET /reference-data/locations/airports
- "Find airports close to latitude 40.7128 and longitude -74.0060" -> GET /reference-data/locations/airports
- "What's the nearest airport to Paris?" -> GET /reference-data/locations/airports
- "Show airports within 100 km of my location" -> GET /reference-data/locations/airports
- "Which airports are closest to these coordinates?" -> GET /reference-data/locations/airports
- "Sort nearby airports by distance" -> GET /reference-data/locations/airports
- "Find airports within a 50-mile radius of downtown Chicago" -> GET /reference-data/locations/airports
- "What major airports are near latitude 51.5, longitude -0.12?" -> GET /reference-data/locations/airports
- "List airports sorted by relevance near Tokyo" -> GET /reference-data/locations/airports
- "Are there any airports near this GPS coordinate?" -> GET /reference-data/locations/airports
- "What's the closest international airport to a cruise port at lat/lng?" -> GET /reference-data/locations/airports
- "Find the best airport to fly into for a trip to the mountains at these coordinates" -> GET /reference-data/locations/airports

## Response Tips

- **Airport results**: Response contains an array of airport objects with IATA codes, names, distances, and relevance scores. Check `data[]` for the list and `meta` for result count. Distance units depend on the `radius` parameter format.
- **400 errors**: Returned when latitude/longitude are missing, out of range (lat: -90 to 90, lng: -180 to 180), or when `radius`/`sort` contain invalid values. Parse `errors[]` for specific field-level detail.

## Anomaly Flags

- **Missing coordinates**: Surface immediately if the user provides a city name instead of lat/lng -- this API requires numeric coordinates, not text search. Suggest geocoding first.
- **Empty results**: Flag when the response returns zero airports, which likely means the radius is too small or the coordinates point to a remote area (ocean, desert). Suggest increasing the radius.
- **400 validation errors**: Surface the specific field that failed validation so the user can correct input without guessing.
- **Rate limiting (429)**: Amadeus test environment has strict rate limits. Proactively warn if multiple rapid calls are planned.
- **Test vs production base URL**: The spec uses `test.api.amadeus.com` -- flag this if the user appears to need production data, as test environment may return limited or synthetic results.

## Playbook

### 1. Find the Nearest Airport to a Known Location

1. Obtain the latitude and longitude for the target location (use a geocoding service if starting from a city name)
2. Call `GET /reference-data/locations/airports?latitude={lat}&longitude={lng}`
3. The first result in the response is typically the nearest airport
4. Extract the IATA code, airport name, and distance from the response

### 2. Search Within a Custom Radius

1. Determine your center coordinates (latitude, longitude)
2. Choose a radius value appropriate to your needs (e.g., 200 for a wider search)
3. Call `GET /reference-data/locations/airports?latitude={lat}&longitude={lng}&radius={value}`
4. Review all returned airports and compare distances
5. If no results are returned, increase the radius and retry

### 3. Get Airports Sorted by Relevance vs Distance

1. Call with `sort=relevance` to get results ordered by traffic volume and importance: `GET /reference-data/locations/airports?latitude={lat}&longitude={lng}&sort=relevance`
2. Compare with `sort=distance` to see the geographically closest options
3. Use relevance sorting when the user wants major hubs; use distance sorting when proximity matters most

### 4. Plan a Trip to an Unfamiliar Region

1. Look up the GPS coordinates of the destination (hotel, landmark, or city center)
2. Search with a generous radius: `GET /reference-data/locations/airports?latitude={lat}&longitude={lng}&radius=500`
3. Review the full list of airports returned
4. Cross-reference IATA codes with flight search APIs to check route availability
5. Pick the airport that balances proximity with flight options


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
