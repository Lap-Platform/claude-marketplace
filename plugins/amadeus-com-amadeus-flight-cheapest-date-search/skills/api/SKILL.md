---
name: flight-cheapest-date-search
description: "Flight Cheapest Date Search API skill. Use when working with Flight Cheapest Date Search for shopping. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Cheapest Date Search
API version: 1.0.6

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /shopping/flight-dates -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| GET | /shopping/flight-dates | Find the cheapest flight dates from an origin to a destination. |

## Enhanced Skill Content
## Question Mapping

- "What are the cheapest dates to fly from NYC to London?" -> GET /shopping/flight-dates
- "Find cheap flights from LAX to Tokyo in March" -> GET /shopping/flight-dates
- "What's the cheapest one-way ticket from SFO to CDG?" -> GET /shopping/flight-dates
- "Show me nonstop flight prices from JFK to MIA for next month" -> GET /shopping/flight-dates
- "Find round-trip flights under $500 from ORD to BCN" -> GET /shopping/flight-dates
- "What are the cheapest 7-day trip options from BOS to LIS?" -> GET /shopping/flight-dates
- "Compare flight prices by date from ATL to CUN" -> GET /shopping/flight-dates
- "Show cheapest flights grouped by week from DFW to LHR" -> GET /shopping/flight-dates
- "Are there any nonstop flights under $300 from SEA to HNL?" -> GET /shopping/flight-dates
- "What's the best departure date for a 10-day trip from IAD to FCO?" -> GET /shopping/flight-dates
- "Find the cheapest weekend getaway flights from EWR to MBJ" -> GET /shopping/flight-dates
- "Show me price trends for flights from PHX to NRT departing in June" -> GET /shopping/flight-dates
- "What does a flexible-date search look like for SFO to SYD?" -> GET /shopping/flight-dates

## Response Tips

- **Shopping results**: Response contains `data[]` with flight-date objects including `price.total` and `departureDate` -- always sort client-side if you need a specific order. Check `dictionaries` for currency codes and carrier names. Pagination may use `meta.links.next`; follow it until exhausted for full date ranges.
- **Errors (400)**: Inspect `errors[].detail` for invalid IATA codes, malformed dates, or conflicting params (e.g., `duration` with `oneWay=true`). Multiple errors can appear in a single response.
- **404**: No results found for the origin/destination/date combination -- not necessarily an API failure. Suggest broadening search (remove `nonStop`, raise `maxPrice`, widen date range).
- **500**: Amadeus upstream failure. Retry with exponential backoff, max 3 attempts.

## Anomaly Flags

- **Rate limit headers**: Surface `X-RateLimit-Remaining` when below 20% of limit -- recommend batching or throttling subsequent calls.
- **Empty results with 200**: A successful response with an empty `data[]` array likely means no availability, not an error. Flag this distinctly from 404.
- **Currency mismatch**: If `dictionaries.currencies` returns a currency the user didn't expect, surface it before they compare prices.
- **Stale pricing**: Flight prices are volatile. Flag if results are being cached or reused across sessions -- recommend a fresh call for booking decisions.
- **Deprecated fields**: Watch for any `warnings[]` array in the response; surface these verbatim as they indicate sunset timelines or changed behavior.
- **Large date ranges**: If the user omits `departureDate`, the API may return a broad range. Flag when results span more than 60 days so the user can narrow scope.

## Playbook

### 1. Find the Cheapest Travel Dates Between Two Cities

1. Call `GET /shopping/flight-dates` with `origin` and `destination` (IATA codes)
2. Omit `departureDate` to get the broadest date range
3. Set `viewBy=DATE` to see day-by-day pricing
4. Sort the `data[]` array by `price.total` ascending
5. Present the top 5 cheapest dates with prices and currency

### 2. Budget-Constrained Trip Planning

1. Call `GET /shopping/flight-dates` with `origin`, `destination`, and `maxPrice` set to the user's budget
2. Set `duration` to desired trip length (e.g., `7` for a week)
3. If results are empty, retry with `maxPrice` increased by 20% or `nonStop=false`
4. Present matching date ranges with total round-trip cost

### 3. Nonstop Flight Price Comparison

1. Call `GET /shopping/flight-dates` with `origin`, `destination`, `nonStop=true`
2. Call again with `nonStop=false` (or omit the param)
3. Compare the cheapest price from each result set
4. Surface the price difference and whether the nonstop premium is worth it
5. Flag if no nonstop options exist (empty first result)

### 4. One-Way vs Round-Trip Price Check

1. Call `GET /shopping/flight-dates` with `origin`, `destination`, `oneWay=true`
2. Call again with `oneWay=false` (default) and a reasonable `duration`
3. Compare: if two one-ways cost less than the round-trip, recommend booking separately
4. Note that one-way availability may differ from round-trip availability

### 5. Monthly Price Overview for Flexible Travelers

1. Call `GET /shopping/flight-dates` with `origin`, `destination`, and `departureDate` set to the target month (e.g., `2026-06`)
2. Set `viewBy=WEEK` for a summary view or `viewBy=DATE` for granular pricing
3. Identify the cheapest week or date cluster
4. If the user is fully flexible, repeat for adjacent months and compare
5. Present a simple price calendar or ranked list of cheapest periods


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
