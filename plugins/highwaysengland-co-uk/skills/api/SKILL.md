---
name: api
description: " API skill. Use when working with  for v{version}. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# 
API version: v1

## Auth
No authentication required.

## Base URL
https://webtris.highwaysengland.co.uk/api

## Setup
1. No auth setup needed
2. GET /v{version}/areas -- verify access

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### v{version}
| Method | Path | Description |
|--------|------|-------------|
| GET | /v{version}/areas | Returns list of areas |
| GET | /v{version}/areas/{area_Ids} | Returns details of selected area |
| GET | /v{version}/quality/overall | Get Site OverallQuality |
| GET | /v{version}/quality/daily | Get Site DailyQuality |
| GET | /v{version}/reports/{report_type} | Gets the daily report. |
| GET | /v{version}/reports/{start_date}/to/{end_date}/{report_type} | Gets the daily report. |
| GET | /v{version}/sites | Get a list of sites |
| GET | /v{version}/sites/{site_Ids} | Get selected sites |
| GET | /v{version}/sitetypes | Return list of site types |
| GET | /v{version}/sitetypes/{siteType_Id}/sites | Returns the layer metadata for the LayerId specified. |

## Enhanced Skill Content
## Question Mapping

- "What areas are available in the traffic system?" -> GET /v{version}/areas
- "Show me details for area 1" -> GET /v{version}/areas/{area_Ids}
- "What traffic monitoring sites exist?" -> GET /v{version}/sites
- "Get info on site 5688" -> GET /v{version}/sites/{site_Ids}
- "What types of monitoring sites are there?" -> GET /v{version}/sitetypes
- "Which sites belong to site type 1?" -> GET /v{version}/sitetypes/{siteType_Id}/sites
- "What is the overall data quality for sites 5688,5689 between January and March?" -> GET /v{version}/quality/overall
- "Show me daily data quality for site 5688 last month" -> GET /v{version}/quality/daily
- "Get a daily traffic report for site 5688 for the past week" -> GET /v{version}/reports/{report_type}
- "Show monthly traffic volumes between two dates" -> GET /v{version}/reports/{start_date}/to/{end_date}/{report_type}
- "How do I paginate through a large traffic report?" -> GET /v{version}/reports/{report_type} (use page and page_size params)
- "What sites are in a specific area?" -> GET /v{version}/areas/{area_Ids} then GET /v{version}/sites/{site_Ids}
- "Is the data reliable for a given site and date range?" -> GET /v{version}/quality/overall
- "Compare daily quality scores across a date range" -> GET /v{version}/quality/daily

## Response Tips

- **Areas/Sites/SiteTypes** (listing endpoints): Return flat arrays of objects. No pagination -- results are returned in full.
- **Reports**: Paginated via `page` and `page_size` params. Response includes `Header` metadata and `Rows` array. Always check total row count against page size to determine if more pages exist.
- **Quality endpoints**: `overall` returns aggregate quality percentage per site. `daily` returns one quality record per day. Scores are 0-100 where higher means more complete data.
- **Errors**: 400 indicates malformed parameters (bad date format, missing required fields). 500 is a server-side issue -- retry with backoff. 404 only applies to siteType lookups for nonexistent types.

## Anomaly Flags

- **Low data quality**: Surface a warning when quality scores drop below 80% -- traffic counts from those periods may be unreliable.
- **Empty result sets**: If a report returns zero rows for a date range that should have data, flag that the site may be decommissioned or offline.
- **404 on site types**: A siteType_Id returning 404 likely means the type was deprecated or removed -- suggest listing current types first.
- **Large date ranges**: Reports spanning more than 90 days with small page sizes will require many paginated requests -- warn the user and suggest increasing page_size.
- **Version parameter**: All endpoints use `{version}` (currently `v1`). If the API introduces v2, agents should flag version deprecation.

## Playbook

### 1. Discover available sites in an area

1. GET /v{version}/areas to list all geographic areas
2. Pick the target area_Id from the response
3. GET /v{version}/areas/{area_Ids} to get area details and associated site IDs
4. GET /v{version}/sites/{site_Ids} with the comma-separated site IDs to get full site metadata

### 2. Pull a traffic report with quality validation

1. GET /v{version}/quality/overall with your target sites and date range
2. Check quality scores -- if any site is below 80%, note the data may be incomplete
3. GET /v{version}/reports/{report_type} with sites, date range, page=1, page_size=100
4. If rows returned equals page_size, increment page and repeat until all data is fetched
5. Aggregate or present the validated report data

### 3. Explore site types and their members

1. GET /v{version}/sitetypes to list all monitoring site classifications
2. Pick the desired siteType_Id
3. GET /v{version}/sitetypes/{siteType_Id}/sites to get all sites of that type
4. Use the returned site IDs with /sites/{site_Ids} for full details

### 4. Daily quality audit for a specific site

1. GET /v{version}/sites/{site_Ids} to confirm the site exists and is active
2. GET /v{version}/quality/daily with the siteId and target date range
3. Review daily scores -- flag any days below 80% as potentially unreliable
4. Cross-reference flagged days against report data to assess impact on analysis

### 5. Date-scoped report comparison

1. GET /v{version}/reports/{start_date}/to/{end_date}/{report_type} for the first period (e.g., Jan-Mar) with target sites
2. Repeat with the second period (e.g., Apr-Jun)
3. Compare row counts and aggregated values across periods
4. Use quality/overall for both periods to ensure comparability of data


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
