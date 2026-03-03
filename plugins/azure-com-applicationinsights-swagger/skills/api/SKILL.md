---
name: application-insights-data-plane
description: "Application Insights Data Plane API skill. Use when working with Application Insights Data Plane for subscriptions. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Application Insights Data Plane
API version: 2018-04-20

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query -- verify access
3. POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query -- create first query

## Endpoints

9 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query | Execute an Analytics query |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query | Execute an Analytics query |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metadata | Gets metadata information |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metadata | Gets metadata information |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metrics/{metricId} | Retrieve metric data |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metrics/metadata | Retrieve metric metadata |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/{eventType} | Execute OData query |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/{eventType}/{eventId} | Get an event |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/$metadata | Get OData metadata |

## Enhanced Skill Content
## Question Mapping

- "How do I query Application Insights data?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query
- "Can I run a query using GET instead of POST?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query
- "What tables and columns are available in my Application Insights resource?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metadata
- "How do I refresh the schema metadata after deploying new telemetry?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metadata
- "How do I retrieve a specific metric like request duration or failure rate?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metrics/{metricId}
- "What metrics are available for my application?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metrics/metadata
- "How do I list recent exceptions or failed requests?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/{eventType}
- "How do I get details for a specific event by ID?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/{eventType}/{eventId}
- "What event types and fields does the events endpoint support?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/$metadata
- "How do I filter events by time range?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/{eventType} (use `timespan` and `$filter` params)
- "How do I paginate through large event result sets?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/events/{eventType} (use `$skip` and `$top` params)
- "How do I segment a metric by cloud role or browser?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/metrics/{metricId} (use `segment` param)
- "How do I run a complex KQL query with joins across tables?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/components/{applicationName}/query (pass KQL in request body)

## Response Tips

- **Query endpoints (POST/GET query):** Response contains a `tables` array, each with `name`, `columns` (with type info), and `rows`. Rows are positional arrays matching column order -- always map by index, not by name.
- **Metadata endpoints:** Return schema objects describing available tables, columns, and data types. Use these to validate KQL queries before execution.
- **Metrics endpoints:** Responses include `value` with nested `segments` when segmentation is requested. The `interval` field in the response confirms the actual granularity used, which may differ from what was requested. Watch for null data points in sparse time ranges.
- **Events endpoints:** Support OData conventions -- `$count` returns total count, `$skip`/`$top` handle pagination, and `$apply` enables server-side aggregation. Results are wrapped in a `value` array.
- **Events by ID:** Returns a single event object (not wrapped in an array). Returns 404 if the event has aged out of retention.
- **All endpoints:** HTTP 200 is the only documented success code. Errors follow Azure's standard `{ error: { code, message } }` structure.

## Anomaly Flags

- **Throttling (429):** Surface rate limit headers (`Retry-After`) immediately. Azure applies per-app and per-subscription throttling on query endpoints -- agents should implement exponential backoff.
- **Partial results:** Query responses may include a `render` or `truncation` indicator when result sets exceed the 500K row / 64MB limit. Flag when rows appear truncated.
- **Timespan gaps:** If the requested timespan extends beyond the application's data retention period (default 90 days), results silently return only available data. Flag when the effective timespan is shorter than requested.
- **Deprecated event types:** If `eventType` returns empty results for types that previously had data, surface a warning -- the telemetry source may have stopped reporting.
- **Metric granularity coercion:** When the requested `interval` is finer than what is stored, Azure silently rounds up. Flag when the response interval differs from the requested interval.
- **Query timeout:** Complex KQL queries can hit the 3-minute server timeout. Surface partial failure indicators and suggest simplifying the query or narrowing the timespan.

## Playbook

### 1. Investigate a spike in failed requests

1. GET metrics metadata to confirm `requests/failed` metric is available.
2. GET `/metrics/requests%2Ffailed` with `timespan=PT24H` and `interval=PT1H` to see the hourly failure trend.
3. GET `/events/requests` with `$filter=success eq false` and `$top=50&$orderby=timestamp desc` to retrieve the latest failed requests.
4. For each suspicious event, GET `/events/requests/{eventId}` to inspect full details (URL, response code, duration, exception chain).
5. POST a KQL query joining `requests` and `exceptions` tables to correlate failures with exception stack traces.

### 2. Explore available telemetry on a new Application Insights resource

1. GET metadata to discover all available tables and their columns.
2. GET events `$metadata` to understand the OData model and supported event types.
3. GET metrics metadata to list all pre-aggregated metrics and their supported aggregations.
4. POST a KQL query: `requests | take 5` to verify data is flowing and inspect sample records.
5. POST a KQL query: `union * | summarize count() by $table | order by count_ desc` to understand data volume by table.

### 3. Build a performance dashboard query

1. GET metrics metadata to identify relevant metrics (e.g., `requests/duration`, `dependencies/duration`).
2. GET `/metrics/requests%2Fduration` with `aggregation=avg,p95` and `interval=PT1H&timespan=P7D` for request latency trends.
3. GET `/metrics/requests%2Fduration` with `segment=request/name&top=10&orderby=avg/requests/duration desc` to find the slowest endpoints.
4. POST a KQL query for custom analysis: `requests | summarize percentile(duration, 50), percentile(duration, 95), percentile(duration, 99) by bin(timestamp, 1h), name | order by timestamp desc`.

### 4. Set up event search with pagination

1. GET `/events/{eventType}` with `$top=100&$count=true` to get the first page and total count.
2. Note the total from `@odata.count` in the response.
3. GET subsequent pages using `$skip=100&$top=100`, incrementing `$skip` by page size.
4. Apply `$filter`, `$search`, and `$orderby` to narrow results before paginating for efficiency.
5. Use `$select` to return only needed fields and reduce payload size.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
