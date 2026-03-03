---
name: location-score
description: "Location Score API skill. Use when working with Location Score for location. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Location Score
API version: 1.0.3

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /location/analytics/category-rated-areas -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### location
| Method | Path | Description |
|--------|------|-------------|
| GET | /location/analytics/category-rated-areas | GET category rated areas |

## Enhanced Skill Content
## Question Mapping

- "What's the safety score for this location?" -> GET /location/analytics/category-rated-areas
- "How does this neighborhood rate for nightlife?" -> GET /location/analytics/category-rated-areas
- "Is this area good for sightseeing?" -> GET /location/analytics/category-rated-areas
- "What are the category ratings near these coordinates?" -> GET /location/analytics/category-rated-areas
- "Rate the area around latitude 48.85 and longitude 2.35" -> GET /location/analytics/category-rated-areas
- "How walkable is the area at this GPS position?" -> GET /location/analytics/category-rated-areas
- "Compare safety and nightlife scores for a location" -> GET /location/analytics/category-rated-areas
- "What categories are rated for the area near my hotel?" -> GET /location/analytics/category-rated-areas
- "Get location analytics for downtown Paris" -> GET /location/analytics/category-rated-areas (resolve coords first)
- "Is the neighborhood around 40.7128, -74.0060 tourist-friendly?" -> GET /location/analytics/category-rated-areas
- "What's the shopping score near this address?" -> GET /location/analytics/category-rated-areas (resolve coords first)
- "Show all category ratings within the area of these coordinates" -> GET /location/analytics/category-rated-areas

## Response Tips

- **Category-rated areas**: Response contains rated area objects with category scores (e.g., safety, nightlife, shopping, sightseeing). Scores are typically numeric scales. Check the `categoryScores` or equivalent nested object for per-category breakdowns. No pagination -- single location query returns one result set.
- **Errors (400)**: Indicates invalid or missing coordinates. Verify `latitude` is between -90 and 90, `longitude` between -180 and 180, and both are numeric.
- **Errors (500)**: Server-side issue. Retry with exponential backoff; do not modify the request.

## Anomaly Flags

- **Invalid coordinates**: Surface immediately if latitude/longitude are outside valid ranges before making the call.
- **Empty category scores**: If the response returns successfully but contains no rated categories, flag that the location may lack sufficient data coverage.
- **500 errors on retry**: If repeated 500s occur, alert the user that the Amadeus analytics service may be experiencing downtime.
- **Test vs production base URL**: The spec uses `test.api.amadeus.com` -- flag if the user appears to need production data, as test environment data may be limited or synthetic.
- **Missing categories**: If expected categories (safety, nightlife) are absent from the response, note that not all locations have full category coverage.

## Playbook

### 1. Score a Known Location by Coordinates

1. Confirm you have numeric latitude and longitude values.
2. Call `GET /location/analytics/category-rated-areas?latitude={lat}&longitude={lng}`.
3. Parse the response for category scores.
4. Present scores grouped by category (safety, nightlife, shopping, sightseeing, etc.).

### 2. Score a Location by Name or Address

1. Resolve the place name or address to coordinates using a geocoding service or Amadeus location API.
2. Extract latitude and longitude from the geocoding result.
3. Call `GET /location/analytics/category-rated-areas?latitude={lat}&longitude={lng}`.
4. Present the category ratings alongside the resolved address for confirmation.

### 3. Compare Two Locations

1. Gather coordinates for both locations (resolve from names if needed).
2. Call `GET /location/analytics/category-rated-areas` for location A.
3. Call `GET /location/analytics/category-rated-areas` for location B.
4. Align category scores side by side.
5. Highlight which location scores higher in each category and summarize the tradeoffs.

### 4. Evaluate a Hotel or Venue's Surroundings

1. Obtain the venue's GPS coordinates.
2. Call `GET /location/analytics/category-rated-areas?latitude={lat}&longitude={lng}`.
3. Focus on categories relevant to the stay (safety for hotels, nightlife for entertainment venues).
4. Flag any categories with notably low scores as potential concerns.

### 5. Handle Errors Gracefully

1. If a 400 error is returned, check that both `latitude` and `longitude` are provided and within valid numeric ranges.
2. Correct any out-of-range or missing values and retry.
3. If a 500 error is returned, wait 2-5 seconds and retry once.
4. If the 500 persists, inform the user that the service is temporarily unavailable and suggest trying again later.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
