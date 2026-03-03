---
name: aws-performance-insights
description: "AWS Performance Insights API skill. Use when working with AWS Performance Insights for root. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Performance Insights
API version: 2018-02-27

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

13 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Creates a new performance analysis report for a specific time period for the DB instance. |
| POST | / | Deletes a performance analysis report. |
| POST | / | For a specific time period, retrieve the top N dimension keys for a metric.   Each response element returns a maximum of 500 bytes. For larger elements, such as SQL statements, only the first 500 bytes are returned. |
| POST | / | Get the attributes of the specified dimension group for a DB instance or data source. For example, if you specify a SQL ID, GetDimensionKeyDetails retrieves the full text of the dimension db.sql.statement associated with this ID. This operation is useful because GetResourceMetrics and DescribeDimensionKeys don't support retrieval of large SQL statement text. |
| POST | / | Retrieves the report including the report ID, status, time details, and the insights with recommendations. The report status can be RUNNING, SUCCEEDED, or FAILED. The insights include the description and recommendation fields. |
| POST | / | Retrieve the metadata for different features. For example, the metadata might indicate that a feature is turned on or off on a specific DB instance. |
| POST | / | Retrieve Performance Insights metrics for a set of data sources over a time period. You can provide specific dimension groups and dimensions, and provide filtering criteria for each group. You must specify an aggregate function for each metric.  Each response element returns a maximum of 500 bytes. For larger elements, such as SQL statements, only the first 500 bytes are returned. |
| POST | / | Retrieve the dimensions that can be queried for each specified metric type on a specified DB instance. |
| POST | / | Retrieve metrics of the specified types that can be queried for a specified DB instance. |
| POST | / | Lists all the analysis reports created for the DB instance. The reports are sorted based on the start time of each report. |
| POST | / | Retrieves all the metadata tags associated with Amazon RDS Performance Insights resource. |
| POST | / | Adds metadata tags to the Amazon RDS Performance Insights resource. |
| POST | / | Deletes the metadata tags from the Amazon RDS Performance Insights resource. |

## Enhanced Skill Content
## Question Mapping

- "What metrics are available for my RDS instance?" -> POST / (ListAvailableResourceMetrics)
- "Show me CPU utilization for the past 24 hours on my database" -> POST / (GetResourceMetrics)
- "Which SQL queries are causing the most wait events?" -> POST / (DescribeDimensionKeys)
- "Create a performance analysis report for my Aurora cluster" -> POST / (CreatePerformanceAnalysisReport)
- "What dimensions can I group db.load by?" -> POST / (ListAvailableResourceDimensions)
- "Get the details of my completed analysis report" -> POST / (GetPerformanceAnalysisReport)
- "List all performance analysis reports for my instance" -> POST / (ListPerformanceAnalysisReports)
- "What features does Performance Insights support for my resource?" -> POST / (GetResourceMetadata)
- "Delete an old analysis report I no longer need" -> POST / (DeletePerformanceAnalysisReport)
- "Get detail info about a specific wait event dimension" -> POST / (GetDimensionKeyDetails)
- "Tag my Performance Insights resource for cost tracking" -> POST / (TagResource)
- "What tags are on my Performance Insights resource?" -> POST / (ListTagsForResource)
- "Remove the environment tag from my PI resource" -> POST / (UntagResource)
- "Compare db.load across top SQL statements over a 1-hour window" -> POST / (DescribeDimensionKeys with GroupBy + Filter)
- "Get multiple metric time series in a single call for my dashboard" -> POST / (GetResourceMetrics with multiple MetricQueries)

## Response Tips

- **Metric queries**: `AlignedStartTime`/`AlignedEndTime` may differ from your request -- the service snaps to period boundaries. Always use the aligned values for display.
- **Dimension keys**: Results are paginated via `NextToken` + `MaxResults`; keep calling until `NextToken` is null. `PartitionKeys` maps partition indices to dimension values.
- **Analysis reports**: `Status` can be `RUNNING`, `SUCCEEDED`, or `FAILED` -- poll `GetPerformanceAnalysisReport` until terminal. `Insights` is a nested array with severity and recommendations.
- **Resource metadata**: `Features` is a map keyed by feature name (e.g., `"PerformanceInsights"`) with `FeatureMetadata` values describing enablement status.
- **Tagging**: Tag/Untag calls return no body on success (just 200). `ListTagsForResource` returns `Tags` as an array of `{Key, Value}` objects.

## Anomaly Flags

- **Report stuck in RUNNING**: If an analysis report `Status` remains `RUNNING` for more than 15 minutes, surface a warning -- it may have stalled.
- **Empty metric results**: When `MetricList` or `Keys` comes back empty for a valid identifier, flag that Performance Insights may not be enabled on the resource.
- **Aligned time drift**: If `AlignedStartTime`/`AlignedEndTime` differ significantly from the requested window, alert the user that their period granularity caused time range expansion.
- **Pagination truncation**: When `NextToken` is present in the response, proactively note that results are partial and additional pages exist.
- **Missing dimensions**: If `ListAvailableResourceDimensions` returns fewer `MetricDimensions` than expected, flag that the instance type or engine may not support all dimension groups.
- **ServiceType mismatch**: All calls require `ServiceType` (typically `"RDS"`) -- surface an error immediately if a non-RDS value is passed, as it will likely fail.

## Playbook

### 1. Diagnose a Database Performance Issue

1. Call **GetResourceMetadata** with your `Identifier` to confirm Performance Insights is enabled and check supported features.
2. Call **ListAvailableResourceMetrics** with `MetricTypes: ["os", "db"]` to discover which metrics are available.
3. Call **GetResourceMetrics** with `MetricQueries` for `db.load` over the problem time window (set `PeriodInSeconds` to 60 for granularity).
4. If load is high, call **DescribeDimensionKeys** with `Metric: "db.load"` and `GroupBy: {Group: "db.wait_event"}` to identify top wait events.
5. Drill into the top wait event using **GetDimensionKeyDetails** to understand contributing dimensions.

### 2. Generate and Review an Analysis Report

1. Call **CreatePerformanceAnalysisReport** with the target `Identifier`, `StartTime`, and `EndTime` for the period of interest. Save the returned `AnalysisReportId`.
2. Poll **GetPerformanceAnalysisReport** with the `AnalysisReportId` until `Status` is `SUCCEEDED` (or `FAILED`).
3. Parse the `Insights` array from the completed report -- each insight contains a description, severity, and actionable recommendations.
4. If the report is no longer needed, call **DeletePerformanceAnalysisReport** to clean up.

### 3. Build a Custom Metrics Dashboard

1. Call **ListAvailableResourceMetrics** to discover all available OS and database metrics for your instance.
2. Call **ListAvailableResourceDimensions** for key metrics (e.g., `db.load`) to find valid grouping dimensions.
3. Construct a **GetResourceMetrics** call with multiple `MetricQueries` covering your desired metrics, using `PeriodInSeconds: 300` for 5-minute rollups.
4. Paginate through results using `NextToken` until all data points are collected.
5. Use `AlignedStartTime`/`AlignedEndTime` from the response as your canonical time axis.

### 4. Identify Top SQL by Wait Event

1. Call **DescribeDimensionKeys** with `Metric: "db.load"`, `GroupBy: {Group: "db.wait_event"}` to find the top wait events in a time range.
2. Pick the dominant wait event and call **DescribeDimensionKeys** again with `GroupBy: {Group: "db.sql"}` and `Filter: {"db.wait_event.name": "<event>"}` to find the SQL statements driving that wait.
3. Use **GetDimensionKeyDetails** on the top SQL `GroupIdentifier` to retrieve full SQL text and additional attributes.
4. Call **GetResourceMetrics** with a `MetricQuery` filtered to that specific SQL to chart its load contribution over time.

### 5. Manage Resource Tags for Cost Allocation

1. Call **ListTagsForResource** with the `ResourceARN` to see existing tags.
2. Call **TagResource** with new or updated `Tags` (e.g., `[{Key: "Environment", Value: "Production"}]`).
3. To remove tags, call **UntagResource** with `TagKeys` listing the keys to delete.
4. Verify by calling **ListTagsForResource** again to confirm the final tag state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
