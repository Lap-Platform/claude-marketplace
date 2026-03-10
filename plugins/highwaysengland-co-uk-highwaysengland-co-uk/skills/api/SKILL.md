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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all areas?" -> GET /v{version}/areas
- "Get area details?" -> GET /v{version}/areas/{area_Ids}
- "List all overall?" -> GET /v{version}/quality/overall
- "List all daily?" -> GET /v{version}/quality/daily
- "Get report details?" -> GET /v{version}/reports/{report_type}
- "Get to details?" -> GET /v{version}/reports/{start_date}/to/{end_date}/{report_type}
- "List all sites?" -> GET /v{version}/sites
- "Get site details?" -> GET /v{version}/sites/{site_Ids}
- "List all sitetypes?" -> GET /v{version}/sitetypes
- "List all sites?" -> GET /v{version}/sitetypes/{siteType_Id}/sites

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
