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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths | Returns a list of each resource's health under a service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths/{resourceRegistrationId} | Returns the requested health information about a resource. |

## Enhanced Skill Content
## Question Mapping

- "What resources are unhealthy in this region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths
- "List all resource health statuses for a service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths
- "Show me the health of a specific resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths/{resourceRegistrationId}
- "Is resource X healthy or degraded?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths/{resourceRegistrationId}
- "Get resource health details for a specific infrastructure component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths/{resourceRegistrationId}
- "How many resources are registered under this service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths
- "Are there any critical resource alerts in my region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths
- "What is the operational state of resource registration {id}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths/{resourceRegistrationId}
- "List all infrastructure resources for a service in eastus?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths
- "Check if a specific infrastructure resource needs attention?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths/{resourceRegistrationId}
- "Which resources under service X have warnings?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths
- "Get the full health report for all resources in a service registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceRegistrationId}/resourceHealths

## Response Tips

- **Resource health list**: Response contains a `value` array of resource health objects and a `nextLink` field for pagination; always check `nextLink` and follow it until null to get the complete set.
- **Single resource health**: Returns a flat resource object with `properties` containing `healthState`, `alertSummary`, and `resourceLocation`; check `healthState` for values like `Healthy`, `Warning`, `Critical`, or `Unknown`.
- **Errors**: Azure ARM returns `error.code` and `error.message` in the response body; common codes include `ResourceNotFound` (404), `ResourceGroupNotFound`, and `SubscriptionNotFound`.
- **api-version**: All requests require `?api-version=2016-05-01` as a query parameter; omitting it returns a `NoRegisteredProviderFound` error.

## Anomaly Flags

- **Degraded or Critical health state**: Surface immediately when any resource reports `healthState` other than `Healthy` -- especially `Critical` which indicates active outage.
- **Alert summary counts**: Flag when `alertSummary.criticalAlertCount` or `alertSummary.warningAlertCount` is non-zero, as these indicate unresolved infrastructure issues.
- **Unknown health state**: A resource reporting `Unknown` may indicate a monitoring gap or agent failure -- worth investigating.
- **Throttling (429)**: Azure ARM enforces per-subscription rate limits; surface `Retry-After` header value and pause before retrying.
- **Stale data**: If `registrationId` or `resourceType` fields appear empty or null on a resource, the registration may be incomplete or orphaned.
- **Large result sets**: If the list endpoint returns `nextLink` across many pages, flag the unusually high resource count as it may indicate provisioning sprawl.

## Playbook

### 1. Audit All Resource Health for a Service

1. Call GET `.../serviceHealths/{serviceRegistrationId}/resourceHealths?api-version=2016-05-01` with your subscription, resource group, and location.
2. Iterate through the `value` array in the response.
3. If `nextLink` is present, follow it with a GET request to retrieve the next page.
4. Repeat until `nextLink` is null.
5. Aggregate results by `healthState` to produce a summary (e.g., 12 Healthy, 2 Warning, 1 Critical).

### 2. Investigate a Specific Unhealthy Resource

1. From the list response, identify the resource with a non-Healthy `healthState` and note its `resourceRegistrationId`.
2. Call GET `.../resourceHealths/{resourceRegistrationId}?api-version=2016-05-01` to get full details.
3. Inspect `properties.alertSummary` for critical and warning alert counts.
4. Check `properties.resourceLocation` and `properties.resourceType` to understand what infrastructure component is affected.
5. Use the alert details to determine remediation steps or escalate.

### 3. Monitor Health Across Multiple Regions

1. Determine the list of regions (locations) to monitor.
2. For each region, call the resource health list endpoint with the appropriate `{location}` path parameter.
3. Collect all responses and compare `healthState` distributions across regions.
4. Flag any region where the ratio of non-Healthy resources exceeds your threshold.
5. For regions with issues, drill into individual resources using the single-resource endpoint.

### 4. Set Up a Periodic Health Check

1. Store your `subscriptionId`, `resourceGroupName`, `location`, and `serviceRegistrationId` as configuration.
2. On a schedule, call the resource health list endpoint.
3. Compare current results against the previous check's snapshot.
4. Surface any resources that transitioned from `Healthy` to `Warning` or `Critical` since the last run.
5. Log or alert on new degradations while ignoring already-known issues.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
