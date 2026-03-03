---
name: analytics-api
description: "Analytics API skill. Use when working with Analytics for customer_service_metric, seller_standards_profile, traffic_report. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Analytics API
API version: 1.3.2

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /seller_standards_profile -- verify access

## Endpoints

4 endpoints across 3 groups. See references/api-spec.lap for full details.

### customer_service_metric
| Method | Path | Description |
|--------|------|-------------|
| GET | /customer_service_metric/{customer_service_metric_type}/{evaluation_type} | Use this method to retrieve a seller's performance and rating for the customer service metric.  <br><br>Control the response from the <b>getCustomerServiceMetric</b> method using the following path and query parameters: <ul><li><b>customer_service_metric_type</b> controls the type of customer service transactions evaluated for the metric rating.</li> <li><b>evaluation_type</b> controls the period you want to review.</li> <li><b>evaluation_marketplace_id</b> specifies the target marketplace for the evaluation.</li></ul> Currently, metric data is returned for only peer benchmarking. For details on the workings of peer benchmarking, see <a href="https://www.ebay.com/help/policies/selling-policies/seller-performance-policy/service-metrics-policy?id=4769" title="eBay Help pages" target="_blank">Service metrics policy</a>.  <br><br>For details on using and understanding the response from this method, see <a href="/api-docs/sell/static/performance/customer-service-metric.html" title="Selling Integration Guide">Interpreting customer service metric ratings</a>. |

### seller_standards_profile
| Method | Path | Description |
|--------|------|-------------|
| GET | /seller_standards_profile | This call retrieves all the standards profiles for the associated seller.  <br><br>A <i>standards profile </i> is a set of eBay seller metrics and the seller's associated compliance values (either <code>TOP_RATED</code>, <code>ABOVE_STANDARD</code>, or <code>BELOW_STANDARD</code>).  <br><br>A seller's multiple profiles are distinguished by two criteria, a "program" and a "cycle." A profile's <i>program </i> is one of three regions where the seller may have done business, or <code>PROGRAM_GLOBAL</code> to indicate all marketplaces where the seller has done business. The <i>cycle</i> value specifies whether the standards compliance values were determined at the last official eBay evaluation or at the time of the request. |
| GET | /seller_standards_profile/{program}/{cycle} | This call retrieves a single standards profile for the associated seller.  <br><br>A <i>standards profile </i> is a set of eBay seller metrics and the seller's associated compliance values (either <code>TOP_RATED</code>, <code>ABOVE_STANDARD</code>, or <code>BELOW_STANDARD</code>).  <br><br>A seller can have multiple profiles distinguished by two criteria, a "program" and a "cycle." A profile's <i>program </i> is one of three regions where the seller may have done business, or <code>PROGRAM_GLOBAL</code> to indicate all marketplaces where the seller has done business. The <i>cycle</i> value specifies whether the standards compliance values were determined at the last official eBay evaluation (<code>CURRENT</code>) or at the time of the request (<code>PROJECTED</code>). Both cycle and a program values are required URI parameters for this method. |

### traffic_report
| Method | Path | Description |
|--------|------|-------------|
| GET | /traffic_report | This method returns a report that details the user traffic received by a seller's listings. <br><br>A traffic report gives sellers the ability to review how often their listings appeared on eBay, how many times their listings are viewed, and how many purchases were made. The report also returns the report's start and end dates, and the date the information was last updated.  <br><br>For more information, see <a href="/api-docs/sell/static/performance/traffic-report.html" target="_blank">Traffic report details</a> |

## Enhanced Skill Content
## Question Mapping

- "How is my customer service performing?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "What's my customer service metric for a specific marketplace?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "Show me my seller standards profile" -> GET /seller_standards_profile
- "What are all my seller standards across programs?" -> GET /seller_standards_profile
- "What's my seller level for a specific program and cycle?" -> GET /seller_standards_profile/{program}/{cycle}
- "Am I a Top Rated Seller this cycle?" -> GET /seller_standards_profile/{program}/{cycle}
- "Show me my listing traffic report" -> GET /traffic_report
- "How many page views did my listings get?" -> GET /traffic_report
- "What are my impression and click-through metrics?" -> GET /traffic_report
- "How does my traffic break down by listing?" -> GET /traffic_report
- "Am I meeting eBay's seller standards?" -> GET /seller_standards_profile
- "What was my customer service evaluation for last cycle?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "Sort my traffic data by clicks descending" -> GET /traffic_report
- "Compare my seller standards across programs" -> GET /seller_standards_profile (then) GET /seller_standards_profile/{program}/{cycle}

## Response Tips

- **customer_service_metric**: Response contains `dimensionMetrics` as an array of maps -- iterate to extract individual metric breakdowns. The `evaluationCycle` object includes date range and type; use `evaluationDate` as the authoritative timestamp.
- **seller_standards_profile (list)**: Returns `standardsProfiles` array -- each entry represents a different program/cycle combination. Unwrap the array even for single-program sellers.
- **seller_standards_profile (detail)**: A 204 response means the profile exists but has no data for that program/cycle -- do not treat as an error. The `standardsLevel` field indicates the seller tier (e.g., Top Rated, Above Standard, Below Standard).
- **traffic_report**: The `header` object defines the schema for `records` -- match `dimensionKeys` and `metrics` arrays positionally to interpret record values. Check `warnings` array for data quality or completeness issues. `lastUpdatedDate` indicates data freshness.

## Anomaly Flags

- **204 on seller profile detail**: Silently empty result -- surface to user that no data exists for the requested program/cycle rather than showing a blank response.
- **Warnings in traffic_report**: The `warnings` array may contain data staleness or partial-data notices -- always surface these to the user.
- **Data freshness**: Compare `lastUpdatedDate` in traffic reports against the current date; flag if data is more than 48 hours stale.
- **Evaluation cycle boundaries**: The `evaluationCycle.endDate` may be in the future for current-cycle metrics -- note that results are provisional and may change.
- **409 Conflict on customer_service_metric**: Unusual for a GET endpoint -- indicates a state conflict (e.g., evaluation in progress). Surface this explicitly rather than retrying.
- **standardsLevel degradation**: If `standardsLevel` is "Below Standard", proactively warn the user about potential selling restrictions.
- **defaultProgram flag**: When `defaultProgram` is false on a seller profile, the seller may be enrolled in a non-standard program -- flag for awareness.

## Playbook

### 1. Full Seller Health Check

1. Call GET /seller_standards_profile to retrieve all standards profiles
2. For each entry in `standardsProfiles`, note the program and cycle
3. Call GET /seller_standards_profile/{program}/{cycle} for detailed metrics on each
4. Call GET /customer_service_metric/{metric_type}/{evaluation_type} with the relevant marketplace ID
5. Summarize: seller level, key metrics, and any areas flagged as below threshold

### 2. Traffic Analysis for a Date Range

1. Call GET /traffic_report with `filter` set to the desired date range
2. Set `dimension` to the desired breakdown (e.g., by listing or category)
3. Set `metric` to the KPIs of interest (impressions, clicks, conversion)
4. Parse the `header` to understand the record structure
5. Check `warnings` for any data gaps before presenting results

### 3. Monitor Customer Service Performance Across Marketplaces

1. Identify target marketplaces by their marketplace IDs
2. For each marketplace, call GET /customer_service_metric/{type}/{evaluation_type} with `evaluation_marketplace_id`
3. Extract `dimensionMetrics` from each response
4. Compare metrics side by side across marketplaces
5. Flag any marketplace where metrics fall below acceptable thresholds

### 4. Track Seller Standards Over Time

1. Call GET /seller_standards_profile to get current profiles
2. Call GET /seller_standards_profile/{program}/{cycle} for the current cycle
3. Record the `standardsLevel` and key `metrics` values
4. Repeat for previous cycles (adjusting `cycle` parameter) to build a trend
5. Surface any downward trends in level or individual metrics


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
