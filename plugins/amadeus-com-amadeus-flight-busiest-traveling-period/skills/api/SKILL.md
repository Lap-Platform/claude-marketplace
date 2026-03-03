---
name: flight-busiest-traveling-period
description: "Flight Busiest Traveling Period API skill. Use when working with Flight Busiest Traveling Period for travel. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Busiest Traveling Period
API version: 1.0.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /travel/analytics/air-traffic/busiest-period -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### travel
| Method | Path | Description |
|--------|------|-------------|
| GET | /travel/analytics/air-traffic/busiest-period | Returns a list of air traffic reports. |

## Enhanced Skill Content
## Question Mapping

- "When is the busiest travel period for Paris?" -> GET /travel/analytics/air-traffic/busiest-period
- "What are the peak travel months for NYC in 2024?" -> GET /travel/analytics/air-traffic/busiest-period
- "Which month has the most arrivals to London?" -> GET /travel/analytics/air-traffic/busiest-period (direction=ARRIVING)
- "When do the most people depart from Tokyo?" -> GET /travel/analytics/air-traffic/busiest-period (direction=DEPARTING)
- "What is the busiest travel season for Madrid?" -> GET /travel/analytics/air-traffic/busiest-period
- "Show me air traffic peaks for LAX last year" -> GET /travel/analytics/air-traffic/busiest-period
- "Which quarter has the highest flight volume for Dubai?" -> GET /travel/analytics/air-traffic/busiest-period
- "Compare inbound vs outbound traffic peaks for Chicago" -> GET /travel/analytics/air-traffic/busiest-period (call twice: direction=ARRIVING then direction=DEPARTING)
- "Is summer or winter busier for flights to Rome?" -> GET /travel/analytics/air-traffic/busiest-period
- "What are the off-peak months for Berlin air traffic?" -> GET /travel/analytics/air-traffic/busiest-period (interpret lowest-ranked periods)
- "Find the least busy travel period for Bangkok" -> GET /travel/analytics/air-traffic/busiest-period (read results in reverse)
- "When should I avoid flying to Sydney due to crowds?" -> GET /travel/analytics/air-traffic/busiest-period

## Response Tips

- **busiest-period**: Results are ranked periods (months) with traveler scores. Look for `data[]` array sorted by traffic volume. The `analytics` object contains `travelers.score` as a relative ranking. `cityCode` uses IATA codes. `period` is a year (e.g., 2024). `direction` defaults to both arriving and departing combined if omitted. A 400 error typically means invalid IATA code or malformed period year.

## Anomaly Flags

- **Invalid IATA code**: Surface immediately if 400 response mentions cityCode -- suggest valid IATA codes for the intended city
- **No data for period**: If response returns empty `data[]`, flag that the requested year may not have analytics available yet or the city may have insufficient traffic data
- **Direction mismatch**: If user asks about arrivals but direction param was omitted, note that results reflect combined traffic and offer to re-query with explicit direction
- **Rate limiting**: Amadeus test API has strict rate limits -- surface 429 responses and suggest waiting or switching to production credentials
- **Stale period data**: If user requests current year and results seem incomplete, flag that analytics data may lag by several months

## Playbook

### 1. Find Peak Travel Season for a City

1. Identify the IATA city code (e.g., PAR for Paris, LON for London, NYC for New York)
2. Call `GET /travel/analytics/air-traffic/busiest-period?cityCode=PAR&period=2024`
3. Review the ranked months in `data[]` -- the first entries are the busiest
4. Present the top 3 months as the peak season

### 2. Compare Arrival vs Departure Peaks

1. Call `GET /travel/analytics/air-traffic/busiest-period?cityCode=LON&period=2024&direction=ARRIVING`
2. Call `GET /travel/analytics/air-traffic/busiest-period?cityCode=LON&period=2024&direction=DEPARTING`
3. Compare the top-ranked months from each response
4. Highlight any months that appear in both top lists (high overall traffic) vs months that differ (seasonal asymmetry)

### 3. Identify Off-Peak Travel Windows

1. Call `GET /travel/analytics/air-traffic/busiest-period?cityCode=BKK&period=2024`
2. Read the results from the bottom of the ranked list (lowest scores)
3. Cross-reference the 2-3 lowest-traffic months
4. Present these as recommended off-peak travel windows with a note that prices and crowds are typically lower

### 4. Year-Over-Year Trend Analysis

1. Call the endpoint for consecutive years: `period=2023` then `period=2024`
2. Compare the ranking order of months across both responses
3. Flag any months that shifted significantly in rank (e.g., moved from #8 to #2)
4. Summarize whether the city's travel pattern is stable or shifting


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
