---
name: flight-delay-prediction
description: "Flight Delay Prediction API skill. Use when working with Flight Delay Prediction for travel. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Delay Prediction
API version: 1.0.6

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /travel/predictions/flight-delay -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### travel
| Method | Path | Description |
|--------|------|-------------|
| GET | /travel/predictions/flight-delay | Return the delay segment where the flight is likely to lay. |

## Enhanced Skill Content
## Question Mapping

- "Will my flight be delayed?" -> GET /travel/predictions/flight-delay
- "What is the delay probability for flight AA123?" -> GET /travel/predictions/flight-delay
- "How likely is a delay flying from JFK to LAX tomorrow?" -> GET /travel/predictions/flight-delay
- "Predict delay for a 3-hour flight on Boeing 737" -> GET /travel/predictions/flight-delay
- "What are the chances my evening departure gets delayed?" -> GET /travel/predictions/flight-delay
- "Is carrier DL likely to be on time for flight 456?" -> GET /travel/predictions/flight-delay
- "Compare delay risk for morning vs afternoon departures" -> GET /travel/predictions/flight-delay (call twice, vary departureTime)
- "Which arrival time has the lowest delay probability?" -> GET /travel/predictions/flight-delay (call multiple times, compare results)
- "How does aircraft type affect delay prediction for this route?" -> GET /travel/predictions/flight-delay (call with different aircraftCode values)
- "Get delay forecast for a short-haul domestic flight" -> GET /travel/predictions/flight-delay
- "What delay category is most likely for my redeye flight?" -> GET /travel/predictions/flight-delay
- "Should I expect my connecting flight to be delayed?" -> GET /travel/predictions/flight-delay (call per leg)

## Response Tips

- **Predictions**: Response contains probability buckets by delay category (e.g., on-time, 15-30 min, 30-60 min, 60+ min) -- surface the highest-probability category first and present all tiers so the user can assess risk.
- **Errors (400)**: Bad request typically means a missing or malformed required parameter -- all 10 parameters are mandatory, so check each before retrying.

## Anomaly Flags

- **All parameters required**: If any of the 10 required fields is missing, the call will fail with 400. Pre-validate before sending.
- **Date/time mismatches**: Flag if arrivalDate is before departureDate, or arrivalTime implies a negative duration relative to departureTime (accounting for timezone differences).
- **Duration inconsistency**: Surface a warning if the supplied `duration` does not roughly match the time delta between departure and arrival.
- **Unusual aircraft codes**: Flag if `aircraftCode` is not a recognized IATA aircraft type (e.g., typos like "7X7" instead of "737").
- **Test vs production base URL**: The spec uses `test.api.amadeus.com` -- remind the user this is the sandbox environment, not live data.
- **Auth token expiry**: Amadeus APIs use OAuth2 tokens that expire quickly (typically 1799s) -- surface a reminder to refresh if calls start returning 401.

## Playbook

### 1. Predict Delay for a Known Flight

1. Gather flight details: carrier code, flight number, departure/arrival airports, dates, times, aircraft type, and duration.
2. Format dates as YYYY-MM-DD and times as HH:MM:SS.
3. Call `GET /travel/predictions/flight-delay` with all 10 required parameters.
4. Read the prediction result and identify the highest-probability delay bucket.
5. Present the full probability distribution to the user with the most likely outcome highlighted.

### 2. Compare Delay Risk Across Multiple Flights

1. Collect details for each candidate flight (e.g., different carriers or times on the same route).
2. Call `GET /travel/predictions/flight-delay` once per flight option.
3. Extract the on-time probability from each response.
4. Rank flights from lowest to highest delay risk.
5. Present a comparison table showing each flight's delay probability breakdown.

### 3. Assess Delay Risk for a Multi-Leg Itinerary

1. Break the itinerary into individual flight legs.
2. Call `GET /travel/predictions/flight-delay` for each leg with its specific parameters.
3. Identify any legs with high delay probability (e.g., >40% chance of 30+ min delay).
4. Flag legs where a delay could cause a missed connection based on layover time.
5. Summarize overall itinerary risk and recommend buffer time for tight connections.

### 4. Evaluate Time-of-Day Impact on Delays

1. Pick a fixed route, carrier, flight number, and aircraft type.
2. Call `GET /travel/predictions/flight-delay` varying `departureTime` and `arrivalTime` across morning, afternoon, and evening slots (adjust `duration` if needed).
3. Collect the on-time probability for each time slot.
4. Present results showing which departure window has the best on-time performance.
5. Recommend the optimal departure window to the user.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
