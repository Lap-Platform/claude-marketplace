---
name: trip-purpose-prediction
description: "Trip Purpose Prediction API skill. Use when working with Trip Purpose Prediction for travel. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Trip Purpose Prediction
API version: 1.1.4

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /travel/predictions/trip-purpose -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### travel
| Method | Path | Description |
|--------|------|-------------|
| GET | /travel/predictions/trip-purpose | Returns the forecast purpose of a trip |

## Enhanced Skill Content
## Question Mapping

- "Will this trip be for business or leisure?" -> GET /travel/predictions/trip-purpose
- "What is the predicted purpose of a flight from JFK to CDG?" -> GET /travel/predictions/trip-purpose
- "Is a round trip from London to Tokyo in December likely business travel?" -> GET /travel/predictions/trip-purpose
- "Predict trip purpose for a same-day return flight" -> GET /travel/predictions/trip-purpose
- "How confident is the prediction for my upcoming trip?" -> GET /travel/predictions/trip-purpose
- "What purpose does a weekend getaway from LAX to CUN suggest?" -> GET /travel/predictions/trip-purpose
- "Check if a two-week trip from SFO to BKK looks like vacation" -> GET /travel/predictions/trip-purpose
- "Predict purpose for a Monday-to-Friday trip between business hubs" -> GET /travel/predictions/trip-purpose
- "What does the model predict for a long-haul one-week trip?" -> GET /travel/predictions/trip-purpose
- "Can I get a trip purpose prediction using a custom search date?" -> GET /travel/predictions/trip-purpose
- "Compare predicted purposes for short vs long stays at the same destination" -> GET /travel/predictions/trip-purpose (x2, vary returnDate)
- "What trip purpose is predicted if I depart tomorrow and return next month?" -> GET /travel/predictions/trip-purpose

## Response Tips

- **Predictions**: Response contains a `data` object with `result` (LEISURE or BUSINESS) and `probability` (0-1 float). Always surface both the label and confidence score -- a 0.52 prediction is very different from a 0.98 one.
- **Errors (400)**: Returned when location codes are invalid, dates are malformed (use YYYY-MM-DD), returnDate precedes departureDate, or required parameters are missing. Parse `errors[].detail` for the specific validation failure.

## Anomaly Flags

- **Low confidence predictions**: Surface a warning when probability is below 0.6 -- the prediction is near a coin flip and should not drive decisions.
- **Past dates submitted**: Flag if departureDate or returnDate is in the past, as the API may reject or return unreliable predictions.
- **returnDate before departureDate**: Catch this client-side before calling; the API will return 400 but the error message may be vague.
- **Unusual duration patterns**: Flag trips shorter than 1 day or longer than 90 days -- predictions may be less reliable at extremes.
- **Rate limit headers**: Monitor `X-RateLimit-Remaining` in response headers. Alert when below 10% of quota.
- **Deprecated fields**: Watch for any `warnings` array in responses indicating sunset fields or version changes.

## Playbook

### 1. Predict Trip Purpose for a Single Itinerary

1. Collect origin IATA code (e.g., JFK), destination IATA code (e.g., CDG), departure date, and return date.
2. Call `GET /travel/predictions/trip-purpose?originLocationCode=JFK&destinationLocationCode=CDG&departureDate=2026-06-15&returnDate=2026-06-22`.
3. Read `data.result` for the prediction (BUSINESS or LEISURE).
4. Check `data.probability` -- report high confidence (>0.8) vs. uncertain (<0.6).

### 2. Compare Business vs. Leisure Likelihood Across Date Ranges

1. Define the origin and destination pair.
2. Call the endpoint with a short stay (e.g., Mon-Wed) to get the first prediction.
3. Call again with a longer stay (e.g., Fri-Sun+1 week) for comparison.
4. Present both predictions side by side with probabilities to show how trip duration and day-of-week affect the model.

### 3. Batch Purpose Prediction for Multiple Routes

1. Prepare a list of origin-destination-date combinations.
2. Call `GET /travel/predictions/trip-purpose` for each combination sequentially (no batch endpoint exists).
3. Collect results into a summary table: route, dates, predicted purpose, confidence.
4. Flag any routes where confidence is below 0.6 for manual review.
5. Respect rate limits -- pause between calls if `X-RateLimit-Remaining` drops low.

### 4. Validate Inputs Before Prediction

1. Confirm origin and destination are valid 3-letter IATA airport codes.
2. Verify departureDate and returnDate are in YYYY-MM-DD format and in the future.
3. Ensure returnDate is on or after departureDate.
4. Optionally set searchDate to simulate a past booking scenario (defaults to today).
5. Call the endpoint only after all validations pass to avoid unnecessary 400 errors.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
