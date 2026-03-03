---
name: usagemanagementclient
description: "UsageManagementClient API skill. Use when working with UsageManagementClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# UsageManagementClient
API version: 2015-06-01-preview

## Auth
No authentication required.

## Base URL
https://management.azure.com

## Setup
1. No auth setup needed
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates | Query aggregated Azure subscription consumption data for a date range. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard | Enables you to query for the resource/meter metadata and related prices used in a given subscription by Offer ID, Currency, Locale and Region. The metadata associated with the billing meters, including but not limited to service names, types, resources, units of measure, and regions, is subject to change at any time and without notice. If you intend to use this billing data in an automated fashion, please use the billing meter GUID to uniquely identify each billable item. If the billing meter GUID is scheduled to change due to a new billing model, you will be notified in advance of the change. |

## Enhanced Skill Content
## Question Mapping

- "How much Azure resource usage did I have last month?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "What are the current rates for my Azure subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard
- "Show me daily usage aggregates for a specific date range" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "What is the hourly breakdown of my Azure consumption?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "Get pricing details for Pay-As-You-Go offer" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard
- "How do I page through large usage result sets?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "Show me usage with instance-level details" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "What meter rates apply to my subscription's offer?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard
- "Retrieve all usage records between two timestamps" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "How much did each resource cost over the last week?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates + GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard
- "What is the currency and locale for my rate card?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard
- "Get a summary view of usage without instance details" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/UsageAggregates
- "Are there any included quantities before metered billing starts?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce/RateCard

## Response Tips

- **UsageAggregates**: Results are paginated -- check for `continuationToken` in the response and pass it back to retrieve the next page. A 202 response means the request was accepted but data is still processing; retry after a short delay. Each usage record contains nested `properties` with meter IDs, quantities, and timestamps.
- **RateCard**: Returns a single object with `Meters` (array of rate entries with tiered pricing in `MeterRates`), `OfferTerms`, and `Currency`/`Locale`/`IsTaxIncluded` at the top level. The `$filter` parameter uses OData syntax and must specify `OfferDurableId`, `Currency`, `Locale`, and `RegionInfo`.

## Anomaly Flags

- **202 on UsageAggregates**: Data not yet ready. Surface this to the user and suggest retrying after 30-60 seconds rather than treating it as a final result.
- **Empty continuation pages**: If `continuationToken` is present but the next page returns zero records, aggregation may still be in progress.
- **Time range gaps**: If reported usage has missing intervals within the requested range, flag potential delayed ingestion or zero-usage periods.
- **Stale API version**: The spec uses `2015-06-01-preview` -- a preview version. Surface a warning that this may be deprecated in favor of Azure Cost Management APIs.
- **Rate card filter errors**: Malformed OData `$filter` values return opaque errors. Flag when the filter is missing required fields (`OfferDurableId`, `Currency`, `Locale`, `RegionInfo`).
- **Meter ID mismatches**: When correlating UsageAggregates with RateCard, flag any meter IDs in usage that have no matching entry in the rate card.

## Playbook

### 1. Calculate total cost for a date range

1. Call GET UsageAggregates with `reportedStartTime` and `reportedEndTime` for your range, `aggregationGranularity=Daily`
2. Page through all results using `continuationToken` until no more pages remain
3. Call GET RateCard with `$filter=OfferDurableId eq 'MS-AZR-0003P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'` (adjust to your offer/locale)
4. For each usage record, look up the `MeterId` in the RateCard `Meters` array
5. Multiply the usage `Quantity` by the applicable `MeterRates` tier to get line-item cost
6. Sum all line items for the total

### 2. Retrieve full usage history with pagination

1. Call GET UsageAggregates with the desired time range and `showDetails=true` for instance-level data
2. Check the response for a `continuationToken` field
3. If present, call the endpoint again with `continuationToken` set to that value
4. Repeat until no `continuationToken` is returned
5. Merge all pages into a single result set

### 3. Compare pricing across regions or offers

1. Call GET RateCard with `$filter` for Offer A (e.g., `OfferDurableId eq 'MS-AZR-0003P'`) and your target region/currency
2. Call GET RateCard again with `$filter` for Offer B (e.g., `OfferDurableId eq 'MS-AZR-0044P'`)
3. Align meters by `MeterId` across both responses
4. Compare `MeterRates` values for each meter to identify pricing differences
5. Surface meters with the largest rate deltas

### 4. Monitor for usage spikes

1. Call GET UsageAggregates with `aggregationGranularity=Hourly` for the last 24-48 hours
2. Group results by `MeterId` and compute per-hour quantities
3. Calculate a rolling average and standard deviation for each meter
4. Flag any hour where usage exceeds 2x the rolling average
5. Cross-reference flagged meters with RateCard to estimate cost impact

### 5. Handle 202 accepted responses gracefully

1. Call GET UsageAggregates with your desired parameters
2. If the response status is 202, wait 30-60 seconds before retrying
3. On retry, use the same parameters (the server processes the aggregation asynchronously)
4. If 202 persists after 3 retries, widen the time range slightly or reduce granularity
5. Once a 200 is returned, proceed with normal pagination and processing


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
