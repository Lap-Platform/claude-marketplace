---
name: faretrotter-travel-api
description: "Faretrotter Travel API skill. Use when working with Faretrotter Travel for places, routes. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Faretrotter Travel API
API version: 2.0

## Auth
ApiKey ApiKeyAuth in header

## Base URL
https://api.faretrotter.com/v2.0/{apikey}

## Setup
1. Set your API key in the appropriate header
2. GET /places -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### places
| Method | Path | Description |
|--------|------|-------------|
| GET | /places | Returns possible modes of transportation between two cities. |

### routes
| Method | Path | Description |
|--------|------|-------------|
| GET | /routes |  |

## Enhanced Skill Content
## Question Mapping

- "What places are available?" -> GET /places
- "Search for destinations" -> GET /places
- "Find airports or cities I can travel to" -> GET /places
- "How do I get from New York to London?" -> GET /routes
- "What routes exist between two coordinates?" -> GET /routes
- "Find flights from latitude 40.7 longitude -74.0 to latitude 51.5 longitude -0.1" -> GET /routes
- "What travel options connect these two locations?" -> GET /routes
- "Show me routes from San Francisco to Tokyo" -> GET /places (resolve names) then GET /routes (with coordinates)
- "What are the cheapest ways to travel between two cities?" -> GET /places (lookup) then GET /routes
- "List all supported travel destinations" -> GET /places
- "Can I get route pricing between coordinates?" -> GET /routes
- "What places match a search query?" -> GET /places
- "Plan a trip from one city to another" -> GET /places (resolve both) then GET /routes

## Response Tips

- **Places**: Expect a list of location objects with coordinates; use these lat/lng values as inputs to /routes.
- **Routes**: Returns travel options between two coordinate pairs; look for nested price, duration, and carrier details within each route object.
- **Errors 400/404**: Likely malformed coordinates or no results found -- check that lat/lng are valid decimal numbers within range.
- **Error 401/403**: API key is missing, invalid, or lacks permissions -- verify the key is passed correctly in the header and URL path.
- **Error 402**: Payment or quota issue -- check account billing status.
- **Error 429**: Rate limit exceeded -- back off and retry after the interval indicated in response headers.
- **Errors 501/502**: Server-side issues -- retry with exponential backoff; do not assume the request was malformed.

## Anomaly Flags

- **Rate limiting (429)**: Surface immediately when hit; recommend the user wait before retrying and consider batching requests.
- **Payment required (402)**: Flag proactively -- this likely means the API key's quota or billing is exhausted.
- **Empty results**: If /places or /routes returns 200 but with zero results, alert the user that the query may be too narrow or the locations unsupported.
- **Coordinate validation**: Flag if origin and destination coordinates are identical, reversed (lat/lng swapped), or outside valid ranges (-90 to 90 lat, -180 to 180 lng).
- **Server errors (501/502)**: Surface upstream instability; suggest retrying later rather than adjusting request parameters.
- **Deprecated fields**: If any response contains `deprecated`, `sunset`, or `warning` headers/fields, surface them to the user immediately.

## Playbook

### 1. Find Routes Between Two Cities by Name

1. Call `GET /places` with a search query for the origin city.
2. Extract `origin_lat` and `origin_lng` from the matching place result.
3. Call `GET /places` with a search query for the destination city.
4. Extract `destination_lat` and `destination_lng` from the matching place result.
5. Call `GET /routes` with all four coordinate parameters.
6. Present the returned routes sorted by price or duration as needed.

### 2. Browse All Available Destinations

1. Call `GET /places` with no filters to retrieve the full list.
2. Parse the response for place names, coordinates, and any metadata (country, type).
3. Present results grouped by region or country if that data is available.

### 3. Compare Routes from One Origin to Multiple Destinations

1. Call `GET /places` to resolve the origin city to coordinates.
2. Call `GET /places` to get a list of candidate destinations.
3. For each destination, call `GET /routes` with the origin coordinates and destination coordinates.
4. Collect all route results and compare by price, duration, or number of stops.
5. Present a summary table of the best option per destination.

### 4. Handle Rate Limit Gracefully During Bulk Lookups

1. Before starting, note the rate limit threshold (429 responses).
2. Issue `GET /routes` calls sequentially or in small batches.
3. If a 429 response is received, pause for the duration indicated in the `Retry-After` header (or default to 60 seconds).
4. Resume remaining requests after the cooldown.
5. Log which requests succeeded and which need retry.

### 5. Validate API Key and Connectivity

1. Call `GET /places` as a lightweight health check.
2. If 200, the API key and network are working.
3. If 401 or 403, the API key is invalid or unauthorized -- prompt the user to check their key.
4. If 402, the account has a billing issue -- direct the user to their Faretrotter dashboard.
5. If 502, the service is temporarily unavailable -- retry after a short delay.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
