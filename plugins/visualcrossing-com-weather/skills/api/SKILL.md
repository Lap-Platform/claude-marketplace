---
name: visual-crossing-weather-api
description: "Visual Crossing Weather API skill. Use when working with Visual Crossing Weather for VisualCrossingWebServices. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Visual Crossing Weather API
API version: 4.6

## Auth
Requires API key (key parameter)

## Base URL
https://weather.visualcrossing.com

## Setup
1. Include your API key via the key parameter
2. GET /VisualCrossingWebServices/rest/services/weatherdata/forecast -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### VisualCrossingWebServices
| Method | Path | Description |
|--------|------|-------------|
| GET | /VisualCrossingWebServices/rest/services/timeline/{location} | Historical and Forecast Weather API |
| GET | /VisualCrossingWebServices/rest/services/timeline/{location}/{startdate} | Historical and Forecast Weather API |
| GET | /VisualCrossingWebServices/rest/services/timeline/{location}/{startdate}/{enddate} | Historical and Forecast Weather API |
| GET | /VisualCrossingWebServices/rest/services/weatherdata/forecast | Weather Forecast API |
| GET | /VisualCrossingWebServices/rest/services/weatherdata/history | Retrieves hourly or daily historical weather records. |

## Enhanced Skill Content
## Question Mapping

- "What's the current weather in London?" -> GET /VisualCrossingWebServices/rest/services/timeline/{location}
- "What will the weather be like in Tokyo next week?" -> GET /VisualCrossingWebServices/rest/services/timeline/{location}/{startdate}/{enddate}
- "Was it raining in New York on January 5th 2024?" -> GET /VisualCrossingWebServices/rest/services/timeline/{location}/{startdate}
- "Give me a 15-day forecast for Paris" -> GET /VisualCrossingWebServices/rest/services/timeline/{location}
- "What was the temperature range in Chicago between March 1 and March 15?" -> GET /VisualCrossingWebServices/rest/services/timeline/{location}/{startdate}/{enddate}
- "Get historical weather data for multiple locations" -> GET /VisualCrossingWebServices/rest/services/weatherdata/history
- "Show me an aggregated daily forecast for Berlin" -> GET /VisualCrossingWebServices/rest/services/weatherdata/forecast
- "What are the normal temperatures for Miami in December?" -> GET /VisualCrossingWebServices/rest/services/weatherdata/history (with includeNormals=true)
- "Get weather in metric units for Sydney" -> GET /VisualCrossingWebServices/rest/services/timeline/{location} (with unitGroup=metric)
- "What's the hourly forecast for tomorrow in Denver?" -> GET /VisualCrossingWebServices/rest/services/timeline/{location}/{startdate} (with include=hours)
- "Compare weather history across several cities" -> GET /VisualCrossingWebServices/rest/services/weatherdata/history (with locations=comma-separated)
- "Get only precipitation and wind data for Seattle" -> GET /VisualCrossingWebServices/rest/services/timeline/{location} (with include=days and parse specific fields)
- "What were weather station contributions for this reading?" -> GET /VisualCrossingWebServices/rest/services/weatherdata/history (with collectStationContributions=true)

## Response Tips

- **Timeline endpoints**: Response nests `days[]` each containing `hours[]`. Top-level fields hold resolved address, latitude, longitude, and timezone. Always check `resolvedAddress` to confirm the API matched the intended location.
- **Forecast endpoint**: When `allowAsynch=true`, response may return a task ID instead of data -- poll until complete. `aggregateHours` controls granularity (1=hourly, 24=daily).
- **History endpoint**: Same async pattern applies. `shortColumnNames=true` returns abbreviated keys -- map them using the API docs. `includeNormals=true` adds statistical baselines alongside actuals.
- **All endpoints**: `contentType=json` (default) returns JSON; `csv` returns flat tabular data. Errors return HTTP 200 with an `errorCode` field in the body -- always check for this before processing.

## Anomaly Flags

- **Resolved address mismatch**: Surface when `resolvedAddress` differs significantly from the requested location -- the API may have geocoded to an unexpected place.
- **Partial data periods**: Flag when date ranges include future dates mixed with historical -- the response silently blends forecast and observed data.
- **API key quota**: The API returns 429 when daily query limits are exceeded. Surface remaining quota warnings if response headers include rate limit info.
- **Async task pending**: When `allowAsynch=true` and the response contains a task reference instead of weather data, alert the user that results require polling.
- **Missing hours array**: Some days may lack hourly breakdowns (sparse station data). Flag when `hours[]` is empty or absent for requested days.
- **Unit group defaulting**: If `unitGroup` is omitted, the API defaults to US units. Surface this when the user's context suggests metric expectations.

## Playbook

### 1. Get a Full Week Forecast for a City

1. Call `GET /timeline/{location}` with `key`, `unitGroup=metric`, and `include=days`
2. Parse the `days[]` array from the response
3. For each day, extract `datetime`, `tempmax`, `tempmin`, `conditions`, and `precipprob`
4. Check `resolvedAddress` to confirm correct city was matched

### 2. Compare Historical Weather Across Cities

1. Call `GET /weatherdata/history` with `locations` set to comma-separated city names
2. Set `startDateTime` and `endDateTime` for the period of interest
3. Set `aggregateHours=24` for daily summaries
4. Parse each location's data block from the response
5. Align by date and compare temperature, precipitation, or other fields side by side

### 3. Check if It Rained on a Specific Past Date

1. Call `GET /timeline/{location}/{startdate}` with the target date in `YYYY-MM-DD` format
2. Inspect the single entry in `days[]`
3. Check `precip` (total precipitation) and `preciptype` (rain, snow, etc.)
4. For hourly detail, re-request with `include=hours` and scan each hour's `precip` value

### 4. Build a Hourly Temperature Chart for Today

1. Call `GET /timeline/{location}` with `include=hours` and `unitGroup=metric`
2. Extract `days[0].hours[]` from the response (today's data)
3. From each hour object, pull `datetime` and `temp`
4. Plot the 24 data points as time vs temperature
5. Optionally include `humidity` or `windspeed` as secondary axes

### 5. Retrieve Climate Normals for Trip Planning

1. Call `GET /weatherdata/history` with `includeNormals=true`
2. Set `locations` to the destination, `startDateTime` and `endDateTime` spanning the travel dates (use a past year)
3. Set `aggregateHours=24` for daily granularity
4. Extract normal high, normal low, and normal precipitation from the response
5. Use these baselines to advise on packing and activity planning


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
