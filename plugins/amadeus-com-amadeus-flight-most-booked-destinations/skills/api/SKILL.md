---
name: flight-most-booked-destinations
description: "Flight Most Booked Destinations API skill. Use when working with Flight Most Booked Destinations for travel. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Most Booked Destinations
API version: 1.1.1

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /travel/analytics/air-traffic/booked -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### travel
| Method | Path | Description |
|--------|------|-------------|
| GET | /travel/analytics/air-traffic/booked | Returns a list of air traffic reports. |

## Enhanced Skill Content
## Question Mapping

- "What are the most booked flight destinations from Paris?" -> GET /travel/analytics/air-traffic/booked
- "Show top booked destinations from NYC for January 2024" -> GET /travel/analytics/air-traffic/booked
- "Which cities have the most flight bookings originating from London?" -> GET /travel/analytics/air-traffic/booked
- "Get the top 5 booked destinations from LAX" -> GET /travel/analytics/air-traffic/booked
- "What destinations are trending from Tokyo sorted by analytics?" -> GET /travel/analytics/air-traffic/booked
- "Compare booked destinations from two origin cities" -> GET /travel/analytics/air-traffic/booked (x2, one per origin)
- "Show booked destination rankings from Madrid for Q1 2024" -> GET /travel/analytics/air-traffic/booked (call per month)
- "What are the least booked destinations from Chicago?" -> GET /travel/analytics/air-traffic/booked (use sort param)
- "Return only destination names from Dubai bookings" -> GET /travel/analytics/air-traffic/booked (use fields param)
- "Are there any booked flights from an invalid city code?" -> GET /travel/analytics/air-traffic/booked (expect 400)
- "Show monthly booking trends from Berlin over the past year" -> GET /travel/analytics/air-traffic/booked (x12, one per month)
- "What is the single most booked route from Sydney?" -> GET /travel/analytics/air-traffic/booked (max=1)

## Response Tips

- **Booked destinations (200):** Results are an array of destination objects ranked by booking volume. Use `max` to limit result count and `fields` to trim payload size. Sort order defaults to popularity; override with `sort`.
- **Validation errors (400):** Returned when `originCityCode` is not a valid IATA city code or `period` format is incorrect. Check the `detail` field in the error response for the specific parameter that failed.
- **Period format:** The `period` param typically expects YYYY-MM format. Passing a full date or invalid string triggers a 400.

## Anomaly Flags

- **400 on valid-looking city codes:** Some IATA city codes differ from airport codes (e.g., NYC vs JFK, LON vs LHR). Surface a suggestion to try the city code variant.
- **Empty results array:** If 200 returns zero destinations, flag that the origin city may have insufficient booking data for the requested period.
- **Unusually low max values:** If the user sets `max=1`, confirm they want only the single top result and not a broader ranking.
- **Stale period data:** Amadeus analytics data may lag by several weeks. If the user requests the current month, warn that results may be incomplete or unavailable.
- **Rate limiting (429):** Amadeus test environment has strict rate limits. Surface approaching limits and suggest spacing requests when running trend analyses across multiple months.

## Playbook

### 1. Get Top Booked Destinations from a City

1. Identify the IATA city code for the origin (e.g., PAR for Paris, NYC for New York)
2. Choose a period in YYYY-MM format (e.g., 2024-06)
3. Call `GET /travel/analytics/air-traffic/booked?originCityCode=PAR&period=2024-06`
4. Parse the response array, each entry contains a destination code and booking score
5. Present results as a ranked list with destination names

### 2. Analyze Monthly Booking Trends

1. Pick an origin city code and a date range (e.g., 12 months)
2. Loop through each month, calling `GET /travel/analytics/air-traffic/booked?originCityCode=LON&period=YYYY-MM&max=10`
3. Collect the top destinations and their scores per month
4. Aggregate results to identify seasonal patterns or emerging destinations
5. Flag any months returning empty results as data gaps

### 3. Compare Two Origin Cities

1. Select two origin city codes (e.g., NYC and LAX)
2. Call the endpoint for each with the same `period` and `max` values
3. Cross-reference destination lists to find shared and unique destinations
4. Highlight destinations that rank highly from one origin but not the other
5. Present a side-by-side comparison

### 4. Find Underserved or Niche Routes

1. Call with a smaller origin city code and a recent period
2. Set `max=25` to get a broader set of destinations
3. Set `sort` to surface lower-volume destinations
4. Filter results for destinations with low booking scores relative to the top entry
5. Flag these as potential niche or underserved routes worth investigating


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
