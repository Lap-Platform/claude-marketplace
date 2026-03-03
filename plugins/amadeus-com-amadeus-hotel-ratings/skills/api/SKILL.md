---
name: hotel-ratings
description: "Hotel Ratings API skill. Use when working with Hotel Ratings for e-reputation. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Hotel Ratings
API version: 1.0.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v2

## Setup
1. No auth setup needed
2. GET /e-reputation/hotel-sentiments -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### e-reputation
| Method | Path | Description |
|--------|------|-------------|
| GET | /e-reputation/hotel-sentiments | Get sentiments by Amadeus Hotel Ids |

## Enhanced Skill Content
## Question Mapping

- "What are the guest ratings for this hotel?" -> GET /e-reputation/hotel-sentiments
- "How do travelers feel about hotel ABC123?" -> GET /e-reputation/hotel-sentiments
- "Get sentiment scores for multiple hotels" -> GET /e-reputation/hotel-sentiments
- "Compare ratings between two hotels" -> GET /e-reputation/hotel-sentiments (pass multiple hotelIds)
- "What is the overall guest satisfaction for a property?" -> GET /e-reputation/hotel-sentiments
- "Show me the e-reputation data for a hotel chain" -> GET /e-reputation/hotel-sentiments (batch by hotelIds)
- "Which hotel has better reviews, X or Y?" -> GET /e-reputation/hotel-sentiments (compare results)
- "Are there any negative sentiment signals for this hotel?" -> GET /e-reputation/hotel-sentiments
- "What do guests say about the service at hotel X?" -> GET /e-reputation/hotel-sentiments
- "Pull sentiment breakdown by category for a property" -> GET /e-reputation/hotel-sentiments
- "Check if a hotel ID returns valid rating data" -> GET /e-reputation/hotel-sentiments
- "Get ratings for a list of Amadeus hotel codes" -> GET /e-reputation/hotel-sentiments

## Response Tips

- **hotel-sentiments**: Response contains sentiment objects keyed by category (overall, service, facilities, etc.) with numeric scores. Look for `overallRating` as the primary indicator. When querying multiple `hotelIds`, results return as an array -- match each entry back to its `hotelId` field. Empty arrays mean no sentiment data exists for those IDs, not an error.

## Anomaly Flags

- **401 Unauthorized**: OAuth token expired or missing -- agent should prompt to refresh the access token via the Amadeus auth endpoint before retrying.
- **400 Bad Request**: Likely malformed or missing `hotelIds` parameter -- surface the exact validation error from the response body.
- **Empty results for valid IDs**: Some hotels have no aggregated sentiment data yet; flag this to the user rather than silently returning nothing.
- **Rate limiting (429)**: Amadeus test environment has strict rate limits -- if responses slow down or return 429, surface a cooldown recommendation.
- **Mixed results in batch queries**: When some hotelIds return data and others don't, proactively list which IDs had no sentiment data available.

## Playbook

### 1. Look Up Sentiment for a Single Hotel

1. Obtain a valid OAuth token from the Amadeus auth endpoint.
2. Call `GET /v2/e-reputation/hotel-sentiments?hotelIds=HOTEL_ID` with the Bearer token.
3. Parse the response for overall rating and category breakdowns.
4. Present the sentiment summary to the user.

### 2. Compare Ratings Across Multiple Hotels

1. Collect the list of Amadeus hotel IDs to compare.
2. Call `GET /v2/e-reputation/hotel-sentiments?hotelIds=ID1,ID2,ID3` in a single request.
3. Map each result entry back to its `hotelId`.
4. Rank or tabulate the hotels by `overallRating` or a specific category score.
5. Flag any IDs that returned no data.

### 3. Monitor a Hotel's Reputation Over Time

1. Store a baseline sentiment result for the target hotel.
2. Periodically call `GET /v2/e-reputation/hotel-sentiments?hotelIds=HOTEL_ID`.
3. Diff the new scores against the baseline.
4. Surface any category where the score changed by more than a defined threshold.

### 4. Handle Authentication Failures Gracefully

1. Attempt the sentiment request with the current Bearer token.
2. If a 401 is returned, request a new token from `POST /v1/security/oauth2/token`.
3. Retry the original request with the fresh token.
4. If 401 persists, surface a credentials misconfiguration warning to the user.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
