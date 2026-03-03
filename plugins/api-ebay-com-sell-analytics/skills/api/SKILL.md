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

- "How is my customer service performance?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "What are my customer service metrics for a specific marketplace?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "Show me my current seller standards profile" -> GET /seller_standards_profile
- "What is my seller level rating?" -> GET /seller_standards_profile
- "How do I check my standards for a specific program and cycle?" -> GET /seller_standards_profile/{program}/{cycle}
- "Am I meeting eBay's seller standards?" -> GET /seller_standards_profile/{program}/{cycle}
- "What does my listing traffic look like?" -> GET /traffic_report
- "Which listings are getting the most views?" -> GET /traffic_report
- "How do I compare traffic across different dimensions?" -> GET /traffic_report
- "What are my click-through rates?" -> GET /traffic_report
- "Has my seller level changed this evaluation cycle?" -> GET /seller_standards_profile/{program}/{cycle}
- "What customer service issues are affecting my metrics?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "Show me traffic trends sorted by impressions" -> GET /traffic_report
- "When was my last seller evaluation?" -> GET /seller_standards_profile

## Response Tips

- **customer_service_metric**: Response nests `dimensionMetrics` as an array of maps -- iterate to extract individual metric breakdowns. The `evaluationCycle` object contains date range and type; use `evaluationDate` as the authoritative timestamp.
- **seller_standards_profile (list)**: Returns `standardsProfiles` as a top-level array; each entry represents a different program/cycle combination.
- **seller_standards_profile (detail)**: A 204 means the profile exists but has no data for that program/cycle -- do not treat as an error. The `standardsLevel` field indicates the seller's current tier. `metrics` is an array of maps with varying keys per metric type.
- **traffic_report**: Contains parallel structures: `header.dimensionKeys` and `header.metrics` define columns, while `records` holds the row data. Check `warnings` array for data quality notes. `lastUpdatedDate` indicates freshness -- traffic data may lag by 24-48 hours.

## Anomaly Flags

- **204 on seller standards**: Surface when a program/cycle query returns no content -- the seller may not be enrolled in that program.
- **Warnings in traffic reports**: Always surface the `warnings` array contents; these indicate partial data, sampling, or date range issues.
- **Stale traffic data**: Flag if `lastUpdatedDate` is more than 48 hours behind the current date.
- **Standards level changes**: If `standardsLevel` is "BELOW_STANDARD", proactively alert the seller -- this impacts visibility and fees.
- **Evaluation cycle boundaries**: Flag when `evaluationCycle.endDate` is approaching or has just passed, as metrics may shift.
- **Error 409 on customer service metrics**: This conflict status is unique to this endpoint -- surface it as a possible concurrent evaluation issue.
- **Default program flag**: When `defaultProgram` is `false` on a standards profile, note that the seller is being evaluated under a non-default program.

## Playbook

### 1. Full Seller Health Check

1. Call GET /seller_standards_profile to retrieve all program profiles
2. For each profile in `standardsProfiles`, note the program and cycle
3. Call GET /seller_standards_profile/{program}/{cycle} for detailed metrics on each
4. Call GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type} with the marketplace ID from each profile
5. Summarize: standards level, key metrics, and any areas flagged as below standard

### 2. Traffic Performance Analysis

1. Call GET /traffic_report with `dimension` set to your desired grouping (e.g., by listing or category)
2. Set `metric` to the KPIs you care about (impressions, clicks, conversion)
3. Use `sort` to rank results by the primary metric
4. Check `warnings` for any data quality caveats
5. Compare `startDate`/`endDate` to confirm the reporting window matches expectations

### 3. Customer Service Issue Investigation

1. Identify the metric type to investigate (e.g., item-not-received, return-rate)
2. Call GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type} with the target marketplace
3. Iterate through `dimensionMetrics` to find which dimensions are underperforming
4. Cross-reference with GET /seller_standards_profile to see if the issue is impacting your seller level

### 4. Monitoring Seller Standards Across Programs

1. Call GET /seller_standards_profile to list all enrolled programs
2. For each program, call GET /seller_standards_profile/{program}/{cycle} for both current and projected cycles
3. Compare `standardsLevel` between cycles to detect upcoming changes
4. If `evaluationReason` indicates a downgrade risk, flag for immediate attention
5. Repeat periodically around `evaluationCycle.evaluationDate` boundaries


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
