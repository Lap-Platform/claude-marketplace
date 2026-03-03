---
name: flight-choice-prediction
description: "Flight Choice Prediction API skill. Use when working with Flight Choice Prediction for shopping. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Choice Prediction
API version: 2.0.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v2

## Setup
1. No auth setup needed
3. POST /shopping/flight-offers/prediction -- create first prediction

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| POST | /shopping/flight-offers/prediction | Predict the choice of flight offers. |

## Enhanced Skill Content
## Question Mapping

- "Which flight offer is most likely to be booked?" -> POST /shopping/flight-offers/prediction
- "Can you rank these flight offers by booking probability?" -> POST /shopping/flight-offers/prediction
- "What is the choice prediction score for my flight search results?" -> POST /shopping/flight-offers/prediction
- "How likely is a traveler to pick this flight?" -> POST /shopping/flight-offers/prediction
- "Which of these itineraries has the highest conversion rate?" -> POST /shopping/flight-offers/prediction
- "Sort flight offers by predicted traveler preference" -> POST /shopping/flight-offers/prediction
- "Add machine learning predictions to my flight search results" -> POST /shopping/flight-offers/prediction
- "Which cheap flight is actually worth recommending?" -> POST /shopping/flight-offers/prediction
- "Enrich flight offers with choice probability scores" -> POST /shopping/flight-offers/prediction
- "I have flight offers from a search -- which ones should I show first?" -> POST /shopping/flight-offers/prediction
- "What does the prediction model say about overnight vs direct flights?" -> POST /shopping/flight-offers/prediction
- "How do I filter flight offers to only high-probability choices?" -> POST /shopping/flight-offers/prediction (then filter client-side by `choiceProbability`)

## Response Tips

- **Prediction results**: Each flight offer in the response is enriched with a `choiceProbability` field (0.0-1.0). Higher means more likely to be booked. The original offer data is preserved alongside the prediction score.
- **Errors (400)**: Malformed request body or missing required flight offer fields. Check that the body matches the Flight Offers Search response schema -- the prediction endpoint expects the same structure returned by `GET /shopping/flight-offers`.
- **Errors (500)**: Amadeus server-side failure. Retry with exponential backoff; do not modify the request body.
- **No pagination**: This endpoint returns all enriched offers in a single response. Result count matches the number of offers submitted.

## Anomaly Flags

- **Low prediction spread**: If all offers return nearly identical `choiceProbability` values (variance < 0.05), the model has low confidence -- surface this to the user as "predictions are inconclusive for this route/date."
- **Rate limit headers**: Watch for `X-RateLimit-Remaining` dropping below 10. Proactively warn before hitting the Amadeus free-tier cap (especially on test environment).
- **Empty or truncated offers**: If the response contains fewer offers than submitted, flag missing entries -- the model may have silently dropped malformed offers.
- **Stale input data**: If flight offers passed to prediction were fetched more than 15 minutes ago, prices and availability may have shifted. Flag that predictions may not reflect current inventory.
- **HTTP 500 spikes**: If repeated 500s occur, the prediction model may be temporarily unavailable. Surface this rather than silently retrying indefinitely.

## Playbook

### 1. Search Flights Then Rank by Prediction

1. Call `GET /v2/shopping/flight-offers` with origin, destination, date, and traveler count
2. Take the full JSON response body (the `data` array of flight offers)
3. Pass it as the request body to `POST /v2/shopping/flight-offers/prediction`
4. Sort returned offers by `choiceProbability` descending
5. Present the top 3-5 results to the user

### 2. Filter to High-Confidence Recommendations Only

1. Obtain flight offers (via search or cache)
2. Submit to `POST /v2/shopping/flight-offers/prediction`
3. Filter results to only those with `choiceProbability >= 0.7`
4. If fewer than 2 offers pass the threshold, lower it to 0.5 and re-filter
5. Present filtered results with the prediction score shown as a percentage

### 3. Compare Direct vs Connecting Flight Preference

1. Search flight offers ensuring results include both direct and 1-stop itineraries
2. Submit all offers to `POST /v2/shopping/flight-offers/prediction`
3. Group results by number of stops (segments count minus one)
4. Compare average `choiceProbability` across groups
5. Report which flight type the model predicts travelers prefer for this route

### 4. Batch Prediction for Multiple Routes

1. For each origin-destination pair, call the flight offers search endpoint
2. Collect all offer sets
3. Submit each set separately to `POST /v2/shopping/flight-offers/prediction` (one call per route -- the endpoint does not support mixed routes)
4. Aggregate top-scoring offers across all routes into a single ranked list
5. Present cross-route recommendations sorted by prediction score


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
