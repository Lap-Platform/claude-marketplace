---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byApi -- verify access

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byApi | Lists report records by API. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byUser | Lists report records by User. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byOperation | Lists report records by API Operations. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byProduct | Lists report records by Product. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byGeo | Lists report records by geography. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/bySubscription | Lists report records by subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byTime | Lists report records by Time. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byRequest | Lists report records by Request. |

## Enhanced Skill Content
## Question Mapping

- "How is each API performing in my APIM instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byApi
- "Which users are consuming the most API calls?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byUser
- "Which operations have the highest error rate?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byOperation
- "How is traffic distributed across my API products?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byProduct
- "Where are my API calls coming from geographically?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byGeo
- "Which subscriptions are driving the most usage?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/bySubscription
- "How has API traffic changed over the past week in hourly intervals?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byTime
- "Show me the raw request log for debugging a specific failure." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/reports/byRequest
- "Which APIs had the highest latency yesterday?" -> GET .../reports/byApi with `$filter=timestamp ge datetime'...' and timestamp le datetime'...'` and `$orderby=apiTimeAvg desc`
- "Are any users hitting rate limits?" -> GET .../reports/byUser with `$filter` on callCountBlocked
- "What is the bandwidth consumption per product over the last 30 days?" -> GET .../reports/byProduct with `$filter` on timestamp range
- "Which operations are slowest for a specific API?" -> GET .../reports/byOperation with `$filter` on apiId and `$orderby=apiTimeAvg desc`
- "Give me a time-series breakdown of errors at 15-minute intervals." -> GET .../reports/byTime with `interval=PT15M` and `$filter` on timestamp range

## Response Tips

- **All report endpoints**: Responses are paged; look for `nextLink` in the response body and follow it to retrieve additional pages. Each page contains a `value` array of report records.
- **Metrics fields**: Records typically include `callCountSuccess`, `callCountBlocked`, `callCountFailed`, `callCountTotal`, `bandwidth`, `apiTimeAvg`, `apiTimeMin`, `apiTimeMax`, and `serviceTimeAvg` -- not all fields are populated for every report dimension.
- **byTime**: Each record maps to a time bucket; the `timestamp` field marks the bucket start. Missing buckets mean zero traffic for that interval.
- **byGeo**: The `region` field uses Azure region names (e.g., `West US`, `North Europe`), and `country` uses ISO 3166-1 alpha-2 codes.
- **byRequest**: Returns individual request-level entries rather than aggregates; expect larger payloads and always use `$filter` with a narrow time range.
- **Errors**: 400 typically means a malformed `$filter` or `$orderby` expression. 404 means the APIM service instance was not found. 401/403 indicate OAuth2 token issues or missing RBAC role (`API Management Service Reader` minimum).

## Anomaly Flags

- **High blocked-call ratio**: Surface when `callCountBlocked` exceeds 10% of `callCountTotal` for any user or subscription -- indicates rate-limit or quota saturation.
- **Elevated error rates**: Flag when `callCountFailed / callCountTotal` exceeds 5% on any API or operation, especially if it represents a sudden spike compared to the previous period.
- **Latency outliers**: Alert when `apiTimeAvg` for an operation exceeds 2x the service-wide average, or when `apiTimeMax` spikes above 10 seconds.
- **Zero-traffic APIs**: If a byApi report shows `callCountTotal = 0` for a previously active API, surface it as a potential misconfiguration or routing issue.
- **Geo anomalies**: Unexpected `country` or `region` values appearing in byGeo reports that were not seen in prior periods -- may indicate misuse or a new, unplanned deployment.
- **Pagination depth**: If retrieving more than 5 pages of `nextLink` results, warn that the query scope may be too broad and suggest tightening the `$filter`.
- **Preview API version**: This spec uses `2019-12-01-preview` -- flag that this is a preview version and may have breaking changes; recommend checking for GA availability.

## Playbook

### 1. Daily API Health Dashboard

1. Call **byApi** with `$filter=timestamp ge datetime'{yesterday}' and timestamp le datetime'{today}'` to get per-API aggregate metrics.
2. Sort by error rate: use `$orderby=callCountFailed desc` to surface problematic APIs first.
3. For any API with elevated errors, drill into **byOperation** with `$filter=apiId eq '{apiId}' and timestamp ge datetime'{yesterday}'` to pinpoint the failing operations.
4. Call **byTime** with `interval=PT1H` and the same date filter to chart hourly traffic trends across all APIs.
5. Summarize: total calls, success rate, top 3 error-producing APIs, and latency percentiles.

### 2. Investigate a Specific User's Activity

1. Call **byUser** with `$filter=timestamp ge datetime'{start}' and timestamp le datetime'{end}'` and `$orderby=callCountTotal desc` to identify the user.
2. Note the `userId` from the result.
3. Call **byRequest** with `$filter=userId eq '{userId}' and timestamp ge datetime'{start}' and timestamp le datetime'{end}'` to retrieve individual request entries.
4. Examine `responseCode`, `apiId`, and `operationId` on each request to understand usage patterns and failures.
5. Cross-reference with **bySubscription** filtering on the user's subscription key to check quota consumption.

### 3. Geographic Traffic Analysis

1. Call **byGeo** with `$filter=timestamp ge datetime'{start}' and timestamp le datetime'{end}'` to get traffic breakdown by region.
2. Identify top regions by `callCountTotal` and note any unexpected countries.
3. For the top region, call **byApi** with an additional region filter to see which APIs are popular in that geography.
4. Call **byTime** with `interval=PT1H` and a geo filter to identify peak hours per region (useful for capacity planning).

### 4. Product Usage and Billing Report

1. Call **byProduct** with `$filter=timestamp ge datetime'{monthStart}' and timestamp le datetime'{monthEnd}'` to get monthly aggregates per product.
2. Use `$orderby=callCountTotal desc` to rank products by volume.
3. Extract `bandwidth` totals per product for data-transfer billing estimates.
4. Call **bySubscription** with the same date filter to break product usage down by individual subscription keys.
5. Combine product and subscription data to generate per-customer billing line items.

### 5. Latency Regression Detection

1. Call **byOperation** with `$filter=timestamp ge datetime'{thisWeekStart}' and timestamp le datetime'{thisWeekEnd}'` and `$orderby=apiTimeAvg desc` for current-week latency.
2. Repeat the same call with the previous week's date range.
3. Compare `apiTimeAvg` and `apiTimeMax` per operation across both periods.
4. Flag any operation where average latency increased by more than 50%.
5. For flagged operations, call **byTime** with `interval=PT1H` and an operation filter to identify exactly when the regression started.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
