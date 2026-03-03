---
name: flight-inspiration-search
description: "Flight Inspiration Search API skill. Use when working with Flight Inspiration Search for shopping. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Inspiration Search
API version: 1.0.6

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /shopping/flight-destinations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| GET | /shopping/flight-destinations | Find the cheapest destinations where you can fly to. |

## Enhanced Skill Content
## Question Mapping

- "Where can I fly from London?" -> GET /shopping/flight-destinations
- "What are the cheapest destinations from JFK?" -> GET /shopping/flight-destinations
- "Find nonstop flights from LAX under $500" -> GET /shopping/flight-destinations
- "Where can I go from Paris for a week in August?" -> GET /shopping/flight-destinations
- "Show me one-way flight deals from SFO" -> GET /shopping/flight-destinations
- "What round-trip destinations are available from CDG for 3-5 days?" -> GET /shopping/flight-destinations
- "Find flight inspiration from MIA departing next month" -> GET /shopping/flight-destinations
- "What destinations can I reach from ORD grouped by destination?" -> GET /shopping/flight-destinations
- "Show the cheapest weekend getaways from BOS" -> GET /shopping/flight-destinations
- "Are there any nonstop deals from ATL under 200 euros?" -> GET /shopping/flight-destinations
- "Where can I fly from DFW on December 15th?" -> GET /shopping/flight-destinations
- "Find destinations from FCO viewed by date" -> GET /shopping/flight-destinations
- "What are the best deals from NRT with flexible dates?" -> GET /shopping/flight-destinations

## Response Tips

- **Flight destinations**: Results return as a `data` array of destination objects containing `destination`, `departureDate`, `returnDate`, and `price` fields. Check `meta` for result count. The `dictionaries` object maps IATA codes to location details. A 404 means no deals found for the given origin/filters, not an invalid request. Prices reflect the cheapest available fare and may change rapidly.

## Anomaly Flags

- **404 with valid origin**: No deals exist for the given criteria -- suggest relaxing filters (remove `maxPrice`, `nonStop`, or broaden `duration`)
- **400 errors**: Likely malformed IATA code for `origin`, invalid date format, or `duration` outside accepted range -- surface the specific error detail from the response body
- **Empty results array**: The origin is valid but current inventory has no matching deals -- flag this distinctly from a 404
- **Price currency mismatch**: Prices may return in different currencies depending on the origin market -- surface the currency field so users don't compare across currencies unknowingly
- **500 errors**: Amadeus upstream issue -- recommend retry after a short delay; if persistent, flag as a service degradation
- **Rate limiting**: Amadeus test environment has strict rate limits -- surface 429 responses immediately and advise waiting before retrying
- **Stale departure dates**: If `departureDate` is in the past relative to today, the API may still accept it but return no results -- proactively warn before sending the request

## Playbook

### 1. Find the Cheapest Getaway from a City

1. Call `GET /shopping/flight-destinations` with `origin` set to the IATA code (e.g., `JFK`)
2. Omit all optional parameters to get the broadest results
3. Sort the returned `data` array by `price.total` ascending
4. Present the top 3-5 destinations with price, dates, and destination code
5. Use the `dictionaries` object to resolve IATA codes to city/country names

### 2. Search for Weekend Trips with Constraints

1. Call `GET /shopping/flight-destinations` with `origin`, `duration=2` (or `1,3` if ranges are supported), and `nonStop=true`
2. Optionally set `maxPrice` to cap the budget
3. Filter results for Friday/Saturday departures client-side if the API doesn't support day-of-week filtering
4. Present results grouped by destination with departure/return dates and price

### 3. Explore Destinations by Date Flexibility

1. Call `GET /shopping/flight-destinations` with `origin` and `viewBy=DATE`
2. Review results organized by departure date rather than destination
3. Identify the cheapest travel dates across all destinations
4. If a specific destination stands out, follow up with `viewBy=DESTINATION` and `departureDate` set to the cheapest date range

### 4. Compare One-Way vs Round-Trip Deals

1. Call `GET /shopping/flight-destinations` with `origin` and `oneWay=false` (default round-trip)
2. Note the prices and destinations returned
3. Call the same endpoint with `oneWay=true`
4. Compare prices for overlapping destinations to determine if separate one-way bookings offer savings
5. Flag any destinations that appear only in one-way results as potential positioning-flight deals

### 5. Narrow Down Results When Too Many Options Return

1. Start with a broad call: `GET /shopping/flight-destinations?origin=LHR`
2. If results are overwhelming, add `maxPrice` to cap budget
3. Add `nonStop=true` to reduce to direct flights only
4. Set `duration` to match available vacation days
5. Finally, set `departureDate` to a specific month or date to finalize options


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
