---
name: streamanalyticsmanagementclient
description: "StreamAnalyticsManagementClient API skill. Use when working with StreamAnalyticsManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# StreamAnalyticsManagementClient
API version: 2016-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas | Retrieves the subscription's current quota information in a particular region. |

## Enhanced Skill Content
## Question Mapping

- "What are my Stream Analytics quotas?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "How many streaming units can I use in East US?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "Am I near my Stream Analytics resource limits?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "What is the maximum number of streaming jobs allowed in West Europe?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "Check Stream Analytics capacity for my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "What quotas apply to Stream Analytics in a specific region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "Can I provision more streaming units in this location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "Compare quotas across regions" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas (call per region)
- "What are the subscription-level limits for Stream Analytics?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "How much Stream Analytics capacity is available before I hit a limit?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "Show quota usage for all Azure regions where I run Stream Analytics" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas (iterate regions)

## Response Tips

- **Quotas**: Response contains a `value` array of quota objects. Each object includes `properties.currentCount` (in use) and `properties.maxCount` (limit). Always compare both to determine remaining capacity. The `name` field identifies the quota type (e.g., streaming units count). Expect `api-version` to be `2016-03-01` -- omitting it or using a wrong version returns 400.

## Anomaly Flags

- **Quota nearing capacity**: Surface a warning when `currentCount` reaches 80% or more of `maxCount` for any quota type.
- **Deprecated API version**: This API uses version `2016-03-01`. If Azure returns a `Sunset` or `Deprecation` header, flag it immediately and suggest checking for a newer API version.
- **Unexpected 404**: A 404 may indicate the location string is invalid or Stream Analytics is not available in that region -- surface the exact location value used.
- **Throttling (429)**: Azure ARM APIs enforce rate limits per subscription. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.
- **Zero quotas returned**: If the `value` array is empty, flag that Stream Analytics may not be registered or available in the specified location.

## Playbook

### 1. Check Quotas for a Single Region

1. Identify your `subscriptionId` (from Azure portal or `az account show`).
2. Choose the target `location` (e.g., `eastus`, `westeurope`).
3. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas?api-version=2016-03-01`.
4. Inspect each entry in the `value` array: compare `properties.currentCount` against `properties.maxCount`.
5. If nearing limits, consider requesting a quota increase via Azure Support.

### 2. Audit Quotas Across All Active Regions

1. List all regions where you have Stream Analytics resources deployed.
2. For each region, call the quotas endpoint with the corresponding `location` value.
3. Aggregate results into a table: region, quota name, current count, max count, utilization percentage.
4. Flag any region where utilization exceeds 80%.

### 3. Pre-Deployment Capacity Check

1. Before deploying a new Stream Analytics job, determine the target region.
2. Call the quotas endpoint for that region.
3. Verify that `properties.currentCount` is below `properties.maxCount` for the relevant quota (typically streaming units).
4. If insufficient capacity, either choose an alternate region or request a quota increase before proceeding with deployment.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
