---
name: city-of-surrey-traffic-loop-count-api
description: "City of Surrey Traffic Loop Count API. API skill. Use when working with City of Surrey Traffic Loop Count API. for TrafficLoops.fmw, TrafficLoopCounts.fmw. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# City of Surrey Traffic Loop Count API.
API version: 0.1

## Auth
No authentication required.

## Base URL
http://gis.surrey.ca:8080/fmedatastreaming/TrafficLoopCount

## Setup
1. No auth setup needed
2. GET /TrafficLoops.fmw -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### TrafficLoops.fmw
| Method | Path | Description |
|--------|------|-------------|
| GET | /TrafficLoops.fmw | Provides all the traffic loops maintained by the City of Surrey in GeoJSON format. LANE_DIRECTION indicates the heading of the traffic (NB, SB, EB, WB). INTERSECTION_ID corresponds to the INTID field in the intersections dataset which can be found on the Surrey Open Data site. ROAD_FACILITYID indicates which road segment the loop is located on.  This corresponds to the FACILITYID in the Road Centrelines dataset on the City of Surrey Open Data site. |

### TrafficLoopCounts.fmw
| Method | Path | Description |
|--------|------|-------------|
| GET | /TrafficLoopCounts.fmw | Provides traffic loop counts for the input time interval. The LOOP_ID and DATETIME combinations are unique in the output. The output timestamp will contain the time zone offset, either -08 (PST) or -07 (PDT) depending on whether daylight savings time was observed at the output datetime. In order to work with local time you may omit the time zone offset from the input and truncate it from the output. |

## Enhanced Skill Content


## Question Mapping

- "What traffic loops are available in Surrey?" -> GET /TrafficLoops.fmw
- "Show me all traffic sensor locations" -> GET /TrafficLoops.fmw
- "Get traffic loop data in a specific coordinate system" -> GET /TrafficLoops.fmw?proj_epsg={epsg_code}
- "What are the traffic counts for today?" -> GET /TrafficLoopCounts.fmw
- "How much traffic was there between two dates?" -> GET /TrafficLoopCounts.fmw?startdatetime={start}&enddatetime={end}
- "Get historical traffic volume for last week" -> GET /TrafficLoopCounts.fmw?startdatetime={7_days_ago}&enddatetime={now}
- "Which intersections have traffic sensors?" -> GET /TrafficLoops.fmw
- "Get traffic counts in EPSG:4326 projection" -> GET /TrafficLoops.fmw?proj_epsg=4326
- "What does the traffic look like for a specific month?" -> GET /TrafficLoopCounts.fmw?startdatetime={month_start}&enddatetime={month_end}
- "List all loop detectors with their coordinates" -> GET /TrafficLoops.fmw
- "Compare traffic volumes across different time periods" -> GET /TrafficLoopCounts.fmw (multiple calls with different date ranges)
- "Get traffic data without any date filter" -> GET /TrafficLoopCounts.fmw

## Response Tips

- **TrafficLoops.fmw**: Returns spatial data (loop locations/geometry). When `proj_epsg` is omitted, coordinates use the server default projection. Responses are likely GeoJSON or FME-structured feature collections.
- **TrafficLoopCounts.fmw**: Returns time-series count data. When date parameters are omitted, the server may return all available data or a default range -- watch for large payloads. Datetime format likely follows ISO 8601 or FME server conventions.

## Anomaly Flags

- **Large unbounded responses**: Calling `/TrafficLoopCounts.fmw` without date filters may return massive datasets. Always suggest date ranges to the user.
- **FME Server availability**: This runs on an FME Data Streaming service (port 8080). Surface connection timeouts or 503 errors promptly -- the FME engine may be restarting or at capacity.
- **HTTP (not HTTPS)**: The base URL uses unencrypted HTTP. Flag this if the user is sending sensitive parameters or if the connection is refused (firewall/network restrictions).
- **Unexpected datetime formats**: If the API rejects date parameters, surface the issue -- FME servers vary in accepted datetime formats.
- **Empty result sets**: If counts return empty for a date range where data is expected, flag that the loops may be inactive or the date format may be wrong.

## Playbook

### 1. Discover All Traffic Loop Locations

1. Call `GET /TrafficLoops.fmw` to retrieve all loop sensor positions
2. Optionally add `?proj_epsg=4326` for WGS84 lat/lng coordinates
3. Parse the response to extract loop IDs, names, and coordinates
4. Use loop IDs to correlate with count data from the counts endpoint

### 2. Pull Traffic Counts for a Date Range

1. Determine the desired date range and format as the API expects (try ISO 8601: `YYYY-MM-DD` or `YYYY-MM-DDTHH:mm:ss`)
2. Call `GET /TrafficLoopCounts.fmw?startdatetime={start}&enddatetime={end}`
3. If the response is empty or errors, try alternate datetime formats (e.g., `MM/DD/YYYY`)
4. Aggregate counts by loop ID or time interval as needed

### 3. Analyze Traffic Trends Over Multiple Periods

1. Define the comparison periods (e.g., week-over-week, month-over-month)
2. For each period, call `GET /TrafficLoopCounts.fmw` with the corresponding `startdatetime` and `enddatetime`
3. Normalize the data by loop ID and time granularity
4. Compare volumes across periods to identify trends, peaks, or anomalies

### 4. Map Traffic Sensors with Their Volumes

1. Call `GET /TrafficLoops.fmw?proj_epsg=4326` to get sensor locations in lat/lng
2. Call `GET /TrafficLoopCounts.fmw?startdatetime={start}&enddatetime={end}` for count data
3. Join the two datasets on the loop identifier field
4. Render or present the combined location + volume data for spatial analysis


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
