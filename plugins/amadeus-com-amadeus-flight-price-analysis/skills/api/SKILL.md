---
name: flight-price-analysis-api
description: "Flight Price Analysis API skill. Use when working with Flight Price Analysis for analytics. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Price Analysis API
API version: 1.0.1

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /analytics/itinerary-price-metrics -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### analytics
| Method | Path | Description |
|--------|------|-------------|
| GET | /analytics/itinerary-price-metrics | GET itinerary price metric |

## Enhanced Skill Content
## Question Mapping

- "How much does a flight from Paris to New York cost?" -> GET /analytics/itinerary-price-metrics
- "What are the price metrics for flights between two cities?" -> GET /analytics/itinerary-price-metrics
- "What is the cheapest fare from JFK to LHR on a specific date?" -> GET /analytics/itinerary-price-metrics
- "Show me round-trip price analysis from LAX to NRT" -> GET /analytics/itinerary-price-metrics
- "What are one-way flight prices from CDG to SFO?" -> GET /analytics/itinerary-price-metrics
- "How do flight prices compare in USD for a given route?" -> GET /analytics/itinerary-price-metrics
- "What is the median fare from London to Tokyo next month?" -> GET /analytics/itinerary-price-metrics
- "Are flights from MIA to BCN expensive for this date?" -> GET /analytics/itinerary-price-metrics
- "Show price distribution for a domestic route on a given departure date" -> GET /analytics/itinerary-price-metrics
- "What is the price range for one-way flights in GBP?" -> GET /analytics/itinerary-price-metrics
- "Compare historical price metrics between two airports" -> GET /analytics/itinerary-price-metrics
- "Is it a good deal to fly from SIN to HND on this date?" -> GET /analytics/itinerary-price-metrics

## Response Tips

- **Price metrics**: Responses contain statistical price buckets (min, max, median, percentiles). Parse nested `priceMetrics` array -- each entry represents a fare tier (first, business, economy). Always check the `currencyCode` in the response to confirm it matches your request, as defaults apply.

## Anomaly Flags

- **400 errors with validation detail**: Surface the specific field that failed -- usually malformed IATA codes (must be 3 uppercase letters) or invalid date format (requires YYYY-MM-DD).
- **500 errors**: Amadeus upstream failures. Suggest retrying after a short delay; flag if repeated.
- **Empty or sparse price data**: If metrics return with very few data points, warn the user that the route may have limited service or the date is too far out for reliable pricing.
- **Currency mismatch**: If the response currency differs from what was requested, flag it -- the API defaults to EUR when an unsupported currency is passed.
- **One-way vs round-trip confusion**: If the user asks about one-way prices but `oneWay` defaults to `false`, proactively note that results reflect round-trip pricing unless explicitly set.
- **Rate limiting**: Amadeus test environment has strict rate limits. Surface `429` responses immediately and advise waiting before retrying.

## Playbook

### 1. Get Basic Price Analysis for a Route

1. Identify origin and destination IATA codes (e.g., CDG, JFK).
2. Choose a departure date in YYYY-MM-DD format.
3. Call `GET /analytics/itinerary-price-metrics?originIataCode=CDG&destinationIataCode=JFK&departureDate=2026-06-15`.
4. Parse the response for min, median, and max price values.
5. Present the price range to the user with the currency noted.

### 2. Compare One-Way vs Round-Trip Pricing

1. Call the endpoint with `oneWay=false` (default) for the desired route and date.
2. Note the round-trip price metrics.
3. Call the endpoint again with `oneWay=true` for the same route and date.
4. Compare the two result sets side by side.
5. Highlight whether one-way is more or less than half the round-trip fare.

### 3. Check Prices in a Specific Currency

1. Determine the user's preferred currency code (e.g., USD, GBP, JPY).
2. Call the endpoint with `currencyCode=USD` alongside the required route and date params.
3. Verify the response's currency matches the request.
4. If the currency was silently defaulted to EUR, inform the user and suggest checking supported currencies.

### 4. Assess Whether a Fare Is a Good Deal

1. Call the endpoint for the desired route and date.
2. Extract the median and percentile values from the response.
3. Compare the user's quoted fare against the distribution: below the 25th percentile is a strong deal, above the 75th is expensive.
4. If data points are sparse, caveat that the analysis may not be reliable for that route.

### 5. Handle Errors and Retry Gracefully

1. On a `400` error, read the error detail to identify the invalid parameter.
2. Fix the parameter (common issues: lowercase IATA codes, wrong date format, missing required fields).
3. On a `500` error, wait 5-10 seconds and retry once.
4. If the error persists, inform the user that the Amadeus service may be temporarily unavailable.
5. On a `429` rate limit, stop making requests and advise the user to wait before trying again.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
