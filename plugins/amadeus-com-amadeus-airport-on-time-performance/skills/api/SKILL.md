---
name: airport-on-time-performance
description: "Airport On-Time Performance API skill. Use when working with Airport On-Time Performance for airport. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Airport On-Time Performance
API version: 1.0.4

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /airport/predictions/on-time -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### airport
| Method | Path | Description |
|--------|------|-------------|
| GET | /airport/predictions/on-time | Returns a percentage of on-time flight departures from a given airport. |

## Enhanced Skill Content
## Question Mapping

- "What is the on-time performance prediction for JFK?" -> GET /airport/predictions/on-time
- "How likely is my flight from LAX to be on time tomorrow?" -> GET /airport/predictions/on-time
- "Which airports have the best on-time ratings for a given date?" -> GET /airport/predictions/on-time (loop over airport codes)
- "Is there a delay risk at O'Hare on 2026-03-15?" -> GET /airport/predictions/on-time
- "What's the punctuality forecast for Heathrow next Monday?" -> GET /airport/predictions/on-time
- "Compare on-time performance between SFO and SJC for a date" -> GET /airport/predictions/on-time (two calls, compare results)
- "Should I book a connection through ATL or CLT based on delay risk?" -> GET /airport/predictions/on-time (two calls, compare)
- "What on-time score does CDG have today?" -> GET /airport/predictions/on-time
- "Get delay predictions for all major US hub airports on a date" -> GET /airport/predictions/on-time (batch calls)
- "Is NRT a reliable airport for connections next Friday?" -> GET /airport/predictions/on-time
- "How does seasonal performance vary for DEN?" -> GET /airport/predictions/on-time (multiple date calls)
- "What happens if I pass an invalid airport code?" -> GET /airport/predictions/on-time (expect 400)

## Response Tips

- **On-time predictions**: Response contains a probability/score object -- surface the percentage or category (e.g., high/medium/low) directly rather than raw nested data. Check for `data.result` or `data.prediction` keys.
- **400 errors**: Typically indicate malformed `airportCode` (must be 3-letter IATA) or invalid `date` format (use YYYY-MM-DD). Parse `errors[].detail` for actionable messages.
- **No pagination**: Single-resource endpoint returns one prediction per call -- no cursor or offset handling needed.

## Anomaly Flags

- **Invalid IATA code**: If a 400 response mentions the airport code, proactively suggest the correct 3-letter IATA code or offer to look it up.
- **Date out of range**: Surface when the requested date falls outside the API's supported prediction window (typically near-term only).
- **Low confidence scores**: If the prediction confidence or probability is unusually low, flag it so the user can factor uncertainty into decisions.
- **Rate limiting (429)**: Surface rate limit headers (`X-RateLimit-Remaining`) proactively when approaching thresholds -- Amadeus test environment has strict quotas.
- **Test vs production base URL**: The spec uses `test.api.amadeus.com` -- flag if the user appears to need production data, as test responses may use synthetic data.
- **Authentication failures (401/403)**: Amadeus requires OAuth2 bearer tokens -- surface token expiry proactively if calls start failing.

## Playbook

### 1. Check On-Time Performance for a Single Airport

1. Confirm the 3-letter IATA airport code (e.g., JFK, LAX, LHR).
2. Determine the target date in YYYY-MM-DD format.
3. Call `GET /airport/predictions/on-time?airportCode=JFK&date=2026-03-10`.
4. Extract the on-time probability or category from the response.
5. Present the result with context (e.g., "JFK has an 82% on-time rating for March 10").

### 2. Compare Two Airports for Connection Planning

1. Identify both candidate airport codes (e.g., ATL and CLT).
2. Set the travel date.
3. Call `GET /airport/predictions/on-time` for each airport in parallel.
4. Compare the on-time scores side by side.
5. Recommend the airport with the higher on-time probability, noting any caveats about confidence.

### 3. Batch-Check Multiple Airports

1. Define a list of target airports (e.g., top 10 US hubs).
2. Set the target date.
3. Loop through the list, calling `GET /airport/predictions/on-time` for each.
4. Collect and sort results by on-time score, highest first.
5. Present a ranked summary table.

### 4. Handle and Recover from Errors

1. Make the prediction request.
2. If a 400 is returned, parse the error detail from the response body.
3. Check for common issues: invalid IATA code (must be exactly 3 uppercase letters), malformed date (must be YYYY-MM-DD), or date out of supported range.
4. Correct the parameter and retry.
5. If errors persist, verify API authentication is valid and the test environment is reachable.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
