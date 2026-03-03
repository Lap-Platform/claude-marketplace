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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths | Returns the list of all resource provider health states. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth} | Returns the requested service health object. |

## Enhanced Skill Content
## Question Mapping

- "What services are running in my region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths
- "Is the compute service healthy?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth}
- "List all service health statuses for eastus" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths
- "Get details on a degraded service" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth}
- "Which infrastructure services have alerts?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths
- "What is the health state of the storage service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth}
- "Show me all unhealthy services in my Azure Stack region" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths
- "How many active alerts does the network service have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth}
- "Check if any services need attention in my resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths
- "Get the infrastructure health summary for a specific service" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth}
- "Are there any critical service health issues in my region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths
- "What is the alert summary for the capacity service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/serviceHealths/{serviceHealth}

## Response Tips

- **Service health list**: Returns a `value` array of service health resources; each entry includes `properties.healthState`, `properties.alertSummary`, and `properties.displayName`. Check for a `nextLink` field for pagination across large deployments.
- **Single service health**: Returns one resource object with nested `properties` containing `healthState` (Healthy, Warning, Critical, Unknown), `alertSummary` with `criticalAlertCount` and `warningAlertCount`, and `infraURI` for drill-down. A 404 means the service name is invalid for that region.
- **Errors**: Azure ARM errors return `{ "error": { "code": "...", "message": "..." } }`. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `SubscriptionNotFound` (404).

## Anomaly Flags

- **Degraded health state**: Surface immediately when any service reports `healthState` other than `Healthy` -- especially `Critical`.
- **Non-zero critical alerts**: Flag when `alertSummary.criticalAlertCount > 0` on any service, even if overall state still shows `Healthy`.
- **Warning accumulation**: Alert the user when `warningAlertCount` exceeds 5 on a single service, suggesting investigation.
- **Unknown health state**: A service reporting `Unknown` may indicate a monitoring gap or connectivity issue -- surface proactively.
- **OAuth token expiry**: Since this API uses OAuth2, flag 401 responses as a token refresh issue rather than a permissions problem.
- **API version deprecation**: This spec uses `api-version=2016-05-01`; if Azure returns deprecation headers or `x-ms-deprecation` warnings, surface them immediately.

## Playbook

### 1. Full region health audit

1. Call the list endpoint with your subscription, resource group, and location to retrieve all service healths.
2. Iterate the `value` array; group services by `properties.healthState`.
3. For any service not in `Healthy` state, call the single service endpoint to get detailed alert counts.
4. Compile a summary: total services, healthy count, warning count, critical count.
5. If `nextLink` is present in the list response, follow it to retrieve additional pages.

### 2. Investigate a specific degraded service

1. Call the single service health endpoint with the service name (e.g., `compute`, `storage`, `network`).
2. Check `properties.healthState` for current status.
3. Review `properties.alertSummary` for `criticalAlertCount` and `warningAlertCount`.
4. Use the `properties.infraURI` if present to navigate to deeper infrastructure details.
5. Cross-reference with the region health endpoint to see if degradation is isolated or widespread.

### 3. Continuous monitoring dashboard setup

1. Call the list endpoint on a schedule (e.g., every 5 minutes) for your target region.
2. Cache previous `healthState` values per service.
3. On each poll, compare current vs. cached state; flag any transitions (e.g., Healthy to Warning).
4. Track `alertSummary` counts over time to detect trends (rising warning counts).
5. Emit notifications when any service transitions to `Critical` or `Unknown`.

### 4. Multi-region health comparison

1. Identify all region locations in your Azure Stack deployment.
2. For each region, call the list service healths endpoint.
3. Normalize results into a table: region, service name, health state, critical alerts, warning alerts.
4. Compare across regions to identify if a service issue is localized or systemic.
5. Flag any region where more than one service is degraded simultaneously.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
