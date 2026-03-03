---
name: tours-and-activities
description: "Tours and Activities API skill. Use when working with Tours and Activities for shopping. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Tours and Activities
API version: 1.0.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /shopping/activities -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| GET | /shopping/activities | Returns Activities around a given location |
| GET | /shopping/activities/by-square | Returns Activities around a given location |
| GET | /shopping/activities/{activityId} | Retrieve one activity by its id |

## Enhanced Skill Content
## Question Mapping

- "What tours and activities are available near me?" -> GET /shopping/activities
- "Find things to do within 10km of the Eiffel Tower" -> GET /shopping/activities
- "What activities are near latitude 48.8566, longitude 2.3522?" -> GET /shopping/activities
- "Show me tours in a specific geographic area" -> GET /shopping/activities/by-square
- "What activities are available in downtown Barcelona (bounding box)?" -> GET /shopping/activities/by-square
- "Find experiences between these four coordinates" -> GET /shopping/activities/by-square
- "Get details for activity ABC123" -> GET /shopping/activities/{activityId}
- "What's included in this specific tour?" -> GET /shopping/activities/{activityId}
- "Search for activities near a hotel at these coordinates with a 5km radius" -> GET /shopping/activities
- "Compare activities available in two different neighborhoods" -> GET /shopping/activities/by-square (x2)
- "Is activity XYZ still available?" -> GET /shopping/activities/{activityId}
- "What can I do within walking distance of my location?" -> GET /shopping/activities (small radius)
- "Plan a day of activities in a city district" -> GET /shopping/activities/by-square, then GET /shopping/activities/{activityId} for each result

## Response Tips

- **Point search** (`/activities`): Results are distance-sorted from the given coordinates. Default radius applies when `radius` is omitted -- check the `meta` object for the effective search radius used.
- **Square search** (`/activities/by-square`): Returns all activities within the bounding box. Ensure `north > south` and coordinates form a valid rectangle or expect a 400 error.
- **Activity detail** (`/activities/{activityId}`): Returns a single activity object, not an array. A 404 means the activity ID is invalid or the listing has been removed.
- **All endpoints**: Responses use Amadeus's standard envelope -- look for `data` (results array or object) and `meta` (count, links). Errors return a `errors[]` array with `detail`, `status`, and `code` fields.

## Anomaly Flags

- **400 with coordinate errors**: Surface immediately -- likely swapped lat/lng or out-of-range values (lat must be -90 to 90, lng -180 to 180).
- **Empty results**: Flag when a populated area returns zero activities -- may indicate an API data gap for that region rather than a user error.
- **404 on activity detail**: Proactively note that the activity may have been delisted or the ID may be from a stale cache.
- **Rate limiting (429)**: Amadeus enforces per-second and per-month quotas. Surface remaining quota from response headers and warn before limits are hit.
- **OAuth token expiry**: Amadeus uses short-lived OAuth2 tokens. Surface 401 responses as token refresh needed, not a credentials problem.
- **Large bounding boxes**: Warn if the north/south/east/west span covers an unusually large area -- results may be truncated or slow.

## Playbook

### Find Activities Near a Location

1. Obtain the latitude and longitude for the desired location (from user input or a geocoding service).
2. Call `GET /shopping/activities?latitude={lat}&longitude={lng}` with an optional `radius` in km.
3. Review the `data` array for available activities, noting names, descriptions, and pricing.
4. For any activity of interest, call `GET /shopping/activities/{activityId}` for full details.

### Explore a City District

1. Define the bounding box: determine the `north`, `south`, `east`, and `west` coordinates of the target area.
2. Call `GET /shopping/activities/by-square?north={n}&west={w}&south={s}&east={e}`.
3. Parse the `data` array and group results by category or rating.
4. Retrieve details for top picks via `GET /shopping/activities/{activityId}`.

### Compare Two Neighborhoods

1. Define bounding boxes for both neighborhoods (two sets of north/south/east/west).
2. Call `GET /shopping/activities/by-square` for each area in parallel.
3. Compare result counts, activity types, and price ranges across the two responses.
4. Fetch details for standout activities from either area using `GET /shopping/activities/{activityId}`.

### Build a Day Itinerary

1. Start with `GET /shopping/activities?latitude={lat}&longitude={lng}&radius=5` centered on the user's hotel or starting point.
2. Review returned activities for time-of-day suitability (morning tours, afternoon experiences, evening events).
3. Call `GET /shopping/activities/{activityId}` for each candidate to check duration, availability, and booking details.
4. Arrange selected activities by time and proximity, flagging any scheduling conflicts.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
