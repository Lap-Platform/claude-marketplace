---
name: airport-city-search
description: "Airport & City Search API skill. Use when working with Airport & City Search for reference-data. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Airport & City Search
API version: 1.2.3

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /reference-data/locations -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/locations | Returns a list of airports and cities matching a given keyword. |
| GET | /reference-data/locations/{locationId} | Returns a specific airports or cities based on its id. |

## Enhanced Skill Content
## Question Mapping

- "Find airports near Paris?" -> GET /reference-data/locations
- "What is the IATA code for Los Angeles airport?" -> GET /reference-data/locations
- "Search for cities matching 'New York'?" -> GET /reference-data/locations
- "List airports in Germany?" -> GET /reference-data/locations
- "Get details for location ID ALHR?" -> GET /reference-data/locations/{locationId}
- "What airports match the keyword 'LON'?" -> GET /reference-data/locations
- "Find all airports in a specific country?" -> GET /reference-data/locations
- "Look up a specific airport by its ID?" -> GET /reference-data/locations/{locationId}
- "Search for cities and airports together?" -> GET /reference-data/locations
- "Sort airport search results by analytics?" -> GET /reference-data/locations
- "Get the full detail view of a location?" -> GET /reference-data/locations/{locationId}
- "Which airports match a partial name like 'frank'?" -> GET /reference-data/locations
- "Verify an airport code exists?" -> GET /reference-data/locations/{locationId}

## Response Tips

- **Search results** (`GET /locations`): Results are in a `data` array. Each item includes `type`, `subType` (AIRPORT or CITY), `name`, `iataCode`, and nested `address`/`geoCode` objects. Use the `view` param (`LIGHT` or `FULL`) to control response detail level.
- **Single location** (`GET /locations/{id}`): Returns a single object in `data`. A 404 means the location ID does not exist -- check for typos in the IATA/location code.

## Anomaly Flags

- **400 errors**: Surface the `detail` field from error responses -- usually indicates missing `subType` or `keyword` params, which are both required for search.
- **404 on location lookup**: Proactively suggest verifying the location ID format and checking for common IATA code confusion (city code vs airport code, e.g., `NYC` vs `JFK`).
- **Empty results**: If a search returns an empty `data` array, suggest broadening the keyword or checking `countryCode` filter.
- **Rate limits**: Amadeus test environment has strict rate limits. Surface `X-RateLimit-Remaining` headers when available and warn when approaching zero.
- **Auth expiry**: Amadeus OAuth tokens expire (typically 1799s). Flag `401` responses and prompt re-authentication.

## Playbook

### 1. Search for Airports in a Country

1. Call `GET /reference-data/locations` with `subType=AIRPORT`, `keyword` matching your search term, and `countryCode` set to the ISO country code (e.g., `DE` for Germany).
2. Review the `data` array for matching airports.
3. Use `sort=analytics.travelers.score` to rank by popularity if needed.
4. For full address and geo coordinates, add `view=FULL`.

### 2. Look Up a Specific Location by Code

1. Identify the location ID (typically the IATA code, e.g., `ALHR`).
2. Call `GET /reference-data/locations/{locationId}` with the ID.
3. Parse the `data` object for name, coordinates, city, and country info.
4. If you get a 404, fall back to a keyword search via `GET /reference-data/locations`.

### 3. Find the Nearest Airport to a City

1. Call `GET /reference-data/locations` with `subType=CITY,AIRPORT` and `keyword` set to the city name.
2. Filter results where `subType` is `AIRPORT`.
3. Use the `distance` or `geoCode` fields from `FULL` view to determine proximity.
4. Pick the result with the highest `analytics.travelers.score` for the busiest option.

### 4. Autocomplete an Airport Search Field

1. As the user types, call `GET /reference-data/locations` with `subType=AIRPORT,CITY` and `keyword` set to the current input (minimum 1 character).
2. Display `name` and `iataCode` from each result.
3. On selection, call `GET /reference-data/locations/{locationId}` to fetch full details.
4. Cache frequent lookups to reduce API calls against rate limits.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
