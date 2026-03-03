---
name: weatherbit-interactive-swagger-ui-documentation
description: "Weatherbit - Interactive Swagger UI Documentation API skill. Use when working with Weatherbit - Interactive Swagger UI Documentation for alerts, current, history. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# Weatherbit - Interactive Swagger UI Documentation
API version: 2.0.0

## Auth
ApiKey key in query

## Base URL
https://api.weatherbit.io/v2.0

## Setup
1. Set your API key in the appropriate header
2. GET /alerts -- verify access

## Endpoints

18 endpoints across 5 groups. See references/api-spec.lap for full details.

### alerts
| Method | Path | Description |
|--------|------|-------------|
| GET | /alerts | Returns severe weather alerts issued by meteorological agencies - Given a lat/lon. |

### current
| Method | Path | Description |
|--------|------|-------------|
| GET | /current | Returns a Current Observation - Given a lat/lon. |
| GET | /current/lightning | Returns nearest and most recent lightning observations - Given a lat/lon. |
| GET | /current/airquality | Returns current air quality conditions - Given a geolocation. |

### history
| Method | Path | Description |
|--------|------|-------------|
| GET | /history/lightning | Returns lightning data by lat/lon from a given date. |
| GET | /history/airquality | Returns 72 hours of historical air quality conditions - Given a geolocation. |
| GET | /history/agweather | Returns Historical Agweather - Given a lat/lon. |
| GET | /history/daily | Returns Historical Observations - Given a lat/lon. |
| GET | /history/hourly | Returns Historical Observations - Given a lat/lon. |
| GET | /history/subhourly | Returns Historical Observations - Given a lat/lon. |
| GET | /history/energy | Returns Energy API response  - Given a single lat/lon. |

### forecast
| Method | Path | Description |
|--------|------|-------------|
| GET | /forecast/daily | Returns a daily forecast - Given Lat/Lon. |
| GET | /forecast/minutely | Returns a 60 minute precipitation forecast - Given Lat/Lon. |
| GET | /forecast/airquality | Returns 72 hour (hourly) Air Quality forecast - Given a geolocation. |
| GET | /forecast/hourly | Returns an hourly forecast - Given a lat/lon. |
| GET | /forecast/agweather | Returns Agweather Forecast - Given a lat/lon. |
| GET | /forecast/energy | Returns Energy Forecast API response  - Given a single lat/lon. |

### normals
| Method | Path | Description |
|--------|------|-------------|
| GET | /normals | Returns Historical Climate Normals (Averages) - Given a lat/lon. |

## Enhanced Skill Content
## Question Mapping

- "What's the current weather in London?" -> GET /current
- "Are there any weather alerts for my area?" -> GET /alerts
- "What's the 7-day forecast for New York?" -> GET /forecast/daily
- "Will it rain in the next hour?" -> GET /forecast/minutely
- "What's the air quality in Beijing right now?" -> GET /current/airquality
- "Show me hourly weather for tomorrow in Paris." -> GET /forecast/hourly
- "What was the temperature last week in Chicago?" -> GET /history/daily
- "Were there lightning strikes near me recently?" -> GET /current/lightning
- "What are the climate normals for July in Denver?" -> GET /normals
- "Show historical air quality for Los Angeles last month." -> GET /history/airquality
- "What's the energy forecast for my solar panels?" -> GET /forecast/energy
- "Get sub-hourly historical weather data for a station." -> GET /history/subhourly
- "What agricultural weather conditions are expected this week?" -> GET /forecast/agweather
- "How many lightning events happened on a specific date?" -> GET /history/lightning
- "What was the heating degree day total last winter?" -> GET /history/energy

## Response Tips

- **Current/Forecast endpoints**: Data array is nested under a `data` key; each element represents one observation or forecast period. A 204 means no data available for the location -- do not treat as an error.
- **History endpoints**: Require `start_date` and `end_date` (YYYY-MM-DD). Response data is chronologically ordered. Large date ranges may return many records.
- **Lightning endpoints**: Results support `skip`/`limit` pagination and `sort` ordering. Use `search_distance_km` to control the geographic radius.
- **Air quality endpoints**: Pollutant values (PM2.5, O3, etc.) are nested inside each data object. Index scales vary by region.
- **Normals endpoint**: Requires `start_day`/`end_day` (MM-DD format) and `series_year` for the baseline period. Returns statistical averages, not observations.
- **Energy endpoints**: Use `threshold` for degree-day calculations and `tp` for temporal granularity. Forecast and history share the same response shape.
- **Alerts endpoint**: Returns structured alert objects with severity, timing, and regions. A 204 means no active alerts (good news).

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry guidance. Weatherbit enforces strict rate limits per API tier -- warn the user before making bulk requests.
- **204 No Content**: Flag when a location query returns no data. This often means the location identifier is invalid or outside coverage areas.
- **403 Forbidden**: Indicates the API key lacks access to the requested endpoint tier (e.g., history endpoints require a paid plan). Surface the plan upgrade requirement.
- **Missing `key` parameter**: All requests require the API key in the query string. Surface auth errors early rather than letting them cascade.
- **Large date ranges on history endpoints**: Warn when `start_date` to `end_date` spans more than 30 days, as this may hit response size limits or slow performance.
- **Unit inconsistencies**: If `units` parameter is omitted, defaults vary. Flag when mixing metric and imperial across related calls in a workflow.
- **Deprecated or empty fields**: If response objects contain null or missing fields that were previously populated, surface as potential API changes.

## Playbook

### 1. Get a Complete Weather Overview for a City

1. Call `GET /current?city={name}&country={code}&key={key}` for current conditions.
2. Call `GET /forecast/daily?city={name}&country={code}&days=7&key={key}` for the week ahead.
3. Call `GET /current/airquality?city={name}&country={code}&key={key}` for air quality.
4. Call `GET /alerts?city={name}&country={code}&key={key}` for active warnings.
5. Combine results into a unified summary: current temp, forecast trend, AQI, and any alerts.

### 2. Analyze Historical Weather for a Date Range

1. Determine the location using `lat`/`lon` or `city`/`country` parameters.
2. Call `GET /history/daily?start_date={start}&end_date={end}&lat={lat}&lon={lon}&key={key}` for daily summaries.
3. If hourly granularity is needed, call `GET /history/hourly` with the same date range.
4. For sub-hourly precision (e.g., station data), use `GET /history/subhourly`.
5. Compare against climate baselines using `GET /normals?start_day={MM-DD}&end_day={MM-DD}&tp=monthly&series_year={year}&lat={lat}&lon={lon}&key={key}`.

### 3. Monitor Severe Weather and Lightning

1. Call `GET /alerts?lat={lat}&lon={lon}&key={key}` to check for active alerts.
2. Call `GET /current/lightning?lat={lat}&lon={lon}&search_distance_km=50&key={key}` for nearby strikes.
3. If strikes are detected, call `GET /forecast/minutely?lat={lat}&lon={lon}&key={key}` for precipitation timing.
4. For historical context, call `GET /history/lightning?lat={lat}&lon={lon}&date={YYYY-MM-DD}&key={key}`.
5. Surface alert severity levels and lightning proximity proactively.

### 4. Agricultural Weather Planning

1. Call `GET /forecast/agweather?lat={lat}&lon={lon}&start_date={start}&end_date={end}&key={key}` for upcoming conditions.
2. Review soil temperature, evapotranspiration, and precipitation forecasts in the response.
3. Call `GET /history/agweather?lat={lat}&lon={lon}&start_date={start}&end_date={end}&tp=daily&key={key}` for historical comparison.
4. Use `GET /normals` with the same location to compare against long-term averages.
5. Flag any forecast anomalies (frost risk, drought indicators) against the normals.

### 5. Energy Demand Forecasting

1. Call `GET /forecast/energy?lat={lat}&lon={lon}&threshold=65&units=I&key={key}` for heating/cooling degree day projections.
2. Adjust `threshold` based on the building's balance point temperature.
3. Call `GET /history/energy?lat={lat}&lon={lon}&start_date={start}&end_date={end}&threshold=65&key={key}` for historical energy-relevant weather data.
4. Compare forecast against historical patterns to identify demand spikes.
5. Use `tp` parameter to switch between hourly and daily aggregation as needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
