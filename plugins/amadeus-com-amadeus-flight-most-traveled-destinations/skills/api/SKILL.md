---
name: flight-most-traveled-destinations
description: "Flight Most Traveled Destinations API skill. Use when working with Flight Most Traveled Destinations for travel. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Most Traveled Destinations
API version: 1.1.1

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /travel/analytics/air-traffic/traveled -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### travel
| Method | Path | Description |
|--------|------|-------------|
| GET | /travel/analytics/air-traffic/traveled | Returns a list of air traffic reports. |

## Enhanced Skill Content
## Question Mapping

- "What are the most traveled destinations from Paris?" -> GET /travel/analytics/air-traffic/traveled
- "Where did people fly most from NYC last month?" -> GET /travel/analytics/air-traffic/traveled
- "Show me top 5 destinations from London in 2025" -> GET /travel/analytics/air-traffic/traveled
- "What are the busiest air routes from LAX?" -> GET /travel/analytics/air-traffic/traveled
- "Which cities had the most flights from Madrid in January?" -> GET /travel/analytics/air-traffic/traveled
- "Sort destinations from Tokyo by traveler count" -> GET /travel/analytics/air-traffic/traveled
- "Get air traffic data for Berlin, limited to 3 results" -> GET /travel/analytics/air-traffic/traveled
- "Compare travel volume from two origin cities" -> GET /travel/analytics/air-traffic/traveled (call twice, compare results)
- "What destinations trended from Dubai over the last quarter?" -> GET /travel/analytics/air-traffic/traveled (call per month, aggregate)
- "Show only destination names from Chicago traffic data" -> GET /travel/analytics/air-traffic/traveled (use fields param)
- "Which routes from SFO are declining in popularity?" -> GET /travel/analytics/air-traffic/traveled (call across periods, diff)
- "List all tracked destinations from Sydney sorted descending" -> GET /travel/analytics/air-traffic/traveled

## Response Tips

- **Travel analytics results**: Response contains ranked destination entries with traveler counts. Use `max` to cap results and `sort` to control ordering. Nested objects include destination city codes and analytics scores -- always reference `originCityCode` to confirm context.
- **400 errors**: Triggered by invalid IATA city codes, malformed period format, or out-of-range values. Check that `originCityCode` is a valid 3-letter IATA code and `period` follows the expected date format (typically YYYY-MM).

## Anomaly Flags

- **Invalid city code**: Surface immediately if the user provides a full city name instead of an IATA code -- offer to map it before calling.
- **Empty results**: Flag when a valid origin returns zero destinations, which may indicate no data coverage for that city or period.
- **400 with detail array**: Parse the error detail to surface the specific invalid parameter rather than a generic failure message.
- **Period gaps**: If querying across months and a period returns significantly fewer results than adjacent months, flag possible data lag or seasonal anomaly.
- **Rate limiting**: Monitor response headers for rate limit indicators; warn the user before making batch comparison calls across many origins or periods.
- **Stale period data**: If the requested period is very recent (current or prior month), flag that data may be incomplete or preliminary.

## Playbook

### 1. Find Top Destinations from a City

1. Identify the origin city's IATA code (e.g., PAR for Paris, NYC for New York)
2. Choose a period in YYYY-MM format (e.g., 2025-06)
3. Call `GET /travel/analytics/air-traffic/traveled?originCityCode=PAR&period=2025-06`
4. Review ranked destinations in the response
5. Use `max=10` to limit results if the list is long

### 2. Compare Seasonal Travel Patterns

1. Pick an origin city code
2. Call the endpoint for each month in the range (e.g., 2025-01 through 2025-12)
3. Collect the top destinations and their scores from each response
4. Identify destinations that appear consistently vs. seasonally
5. Present a summary showing which destinations peak in which months

### 3. Narrow Results with Field Filtering and Sorting

1. Call with `fields` param to request only specific data points (reduces payload)
2. Use `sort` to order results by the desired metric
3. Combine with `max` to get a concise, targeted leaderboard
4. Example: `?originCityCode=LON&period=2025-08&max=5&sort=analytics.travelers.score`

### 4. Multi-City Route Analysis

1. Define a list of origin city codes to compare (e.g., PAR, LON, NYC)
2. Call the endpoint once per origin with the same period
3. Cross-reference results to find shared top destinations
4. Identify unique high-traffic routes per origin
5. Flag any origin returning empty or sparse results for follow-up

### 5. Validate an Unknown City Code

1. Attempt the call with the suspected IATA code and a known-good period
2. If a 400 error returns, inspect the error detail for the invalid parameter
3. Search for the correct IATA city code (not airport code -- e.g., NYC not JFK)
4. Retry with the corrected code
5. Confirm valid results before proceeding with further analysis


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
