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
https://api.ebay.com/sell/analytics/v1

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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get customer_service_metric details?" -> GET /customer_service_metric/{customer_service_metric_type}/{evaluation_type}
- "List all seller_standards_profile?" -> GET /seller_standards_profile
- "Get seller_standards_profile details?" -> GET /seller_standards_profile/{program}/{cycle}
- "List all traffic_report?" -> GET /traffic_report
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
