---
name: infrastructureinsightsmanagementclient
description: "InfrastructureInsightsManagementClient API skill. Use when working with InfrastructureInsightsManagementClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# InfrastructureInsightsManagementClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths | Returns the list of all health status for the region. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location} | Returns the requested health status of a region. |

## Enhanced Skill Content
## Question Mapping

- "What is the health status of all regions in my Azure Stack?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths
- "Is my Azure Stack region healthy?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}
- "List all region health reports for a resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths
- "Get health details for the local region" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}
- "Are there any infrastructure issues in my Azure Stack deployment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths
- "Show me the health summary for a specific Azure Stack location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}
- "How many regions are reporting unhealthy in my subscription?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths
- "Check if the 'local' stamp is experiencing problems" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/local
- "What infrastructure alerts are active across regions?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths
- "Get the current health state for my Azure Stack environment" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}
- "Compare health across all Azure Stack regions" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths
- "What does the infrastructure health look like for resource group 'system.local'?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths

## Response Tips

- **Region health list**: Returns a `value` array of region health objects; check for `nextLink` for pagination. Each item contains `properties.healthState` (Healthy, Warning, Critical, Unknown).
- **Single region health**: Returns one region health object; key fields are nested under `properties` -- look at `alertSummary`, `usageMetrics`, and `healthState` for a full picture.
- **Errors**: Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` format. Common codes: 404 if the location name is wrong, 403 if OAuth scope is missing `user_impersonation`.
- **API version**: Always pass `api-version=2016-05-01` as a query parameter -- omitting it returns a version-not-supported error.

## Anomaly Flags

- **Unhealthy regions**: Surface immediately when any region reports `healthState` other than `Healthy` -- this likely indicates active infrastructure issues requiring operator attention.
- **Critical alert count**: If `alertSummary.criticalAlertCount` > 0, flag it prominently -- critical alerts mean potential service impact.
- **Warning accumulation**: Flag when `alertSummary.warningAlertCount` exceeds a notable threshold (e.g., > 5), indicating degradation trends.
- **Unknown health state**: `healthState: "Unknown"` suggests telemetry gaps -- the monitoring pipeline itself may be impaired.
- **Throttling (429)**: Azure ARM enforces per-subscription rate limits; surface `Retry-After` header value and pause calls accordingly.
- **Stale data**: If the response `properties.lastUpdatedTimestamp` is more than 30 minutes old, flag potential monitoring delay.
- **Deprecated API version**: This API uses version `2016-05-01` -- if Azure returns deprecation headers or newer `api-version` suggestions, surface them.

## Playbook

### 1. Quick health check of all regions

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths?api-version=2016-05-01`
2. Iterate the `value` array in the response
3. For each item, read `properties.healthState`
4. Report any region where `healthState` is not `Healthy`
5. If `nextLink` is present, follow it to fetch additional pages

### 2. Deep-dive into a specific region

1. Identify the target location name (e.g., `local`) from the list endpoint or user input
2. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}?api-version=2016-05-01`
3. Inspect `properties.alertSummary` for critical and warning counts
4. Review `properties.usageMetrics` for capacity concerns
5. Summarize overall status from `properties.healthState` alongside the detailed metrics

### 3. Incident triage workflow

1. Call the list endpoint to identify which regions are unhealthy
2. For each unhealthy region, call the single-region endpoint to get detailed health data
3. Check `alertSummary.criticalAlertCount` to prioritize regions with critical alerts first
4. Note `lastUpdatedTimestamp` to confirm data freshness
5. Compile a summary: region name, health state, critical alert count, and last updated time

### 4. Periodic monitoring setup

1. Schedule the list endpoint call at a regular interval (e.g., every 15 minutes)
2. Compare `healthState` from the current response against the previous run
3. If any region transitions from `Healthy` to `Warning` or `Critical`, trigger an alert
4. If any region transitions back to `Healthy`, send a recovery notification
5. Log `alertSummary` counts over time to detect degradation trends


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
