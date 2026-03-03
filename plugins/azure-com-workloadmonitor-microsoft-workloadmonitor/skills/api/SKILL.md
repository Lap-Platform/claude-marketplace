---
name: workload-monitor-api
description: "Workload Monitor API skill. Use when working with Workload Monitor for subscriptions, providers. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# Workload Monitor API
API version: 2018-08-31-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.WorkloadMonitor/operations -- verify access

## Endpoints

13 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors | Get list of a monitors of a resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors/{monitorId} | Get details of a single monitor. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors/{monitorId} | Update a Monitor's configuration. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/components | Get list of components for a resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/components/{componentId} | Get details of a component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitorInstances | Get list of monitor instances for a resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitorInstances/{monitorInstanceId} | Get details of a monitorInstance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/notificationSettings | Get list of notification settings for a resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/notificationSettings/{notificationSettingName} | Get a of notification setting for a resource. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/notificationSettings/{notificationSettingName} | Update notification settings for a resource. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.WorkloadMonitor/componentsSummary | Get subscription wide details of components. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.WorkloadMonitor/monitorInstancesSummary | Get subscription wide health instances. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.WorkloadMonitor/operations | Gets the details of all operations possible on the resource provider. |

## Enhanced Skill Content
## Question Mapping

- "What monitors are configured for my virtual machine?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors
- "Show me details for a specific monitor." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors/{monitorId}
- "How do I update a monitor's configuration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors/{monitorId}
- "What components are being tracked on this resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/components
- "Get health details for a specific component." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/components/{componentId}
- "List all monitor instances for a resource." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitorInstances
- "What is the current state of a specific monitor instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitorInstances/{monitorInstanceId}
- "What notification settings exist for my resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/notificationSettings
- "How do I configure alert notifications for workload monitoring?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/notificationSettings/{notificationSettingName}
- "Give me a subscription-wide summary of component health." -> GET /subscriptions/{subscriptionId}/providers/Microsoft.WorkloadMonitor/componentsSummary
- "Show me all unhealthy monitor instances across my subscription." -> GET /subscriptions/{subscriptionId}/providers/Microsoft.WorkloadMonitor/monitorInstancesSummary
- "What operations does the Workload Monitor resource provider support?" -> GET /providers/Microsoft.WorkloadMonitor/operations
- "How do I filter monitors to only show critical ones?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.WorkloadMonitor/monitors with `$filter` parameter
- "Can I page through a large list of components?" -> GET .../components with `$skiptoken` parameter from previous response's `nextLink`
- "How do I get an expanded view of monitor instances with related details?" -> GET .../monitorInstances with `$expand` parameter

## Response Tips

- **Monitors**: List responses return a `value` array of monitor objects; single-item GETs return the object directly. Use `$filter` for server-side filtering and `$skiptoken` from `nextLink` for pagination.
- **Components**: Support rich OData queries (`$select`, `$filter`, `$apply`, `$orderby`, `$expand`, `$top`). Use `$select` to reduce payload size when you only need specific fields. `$apply` enables aggregation for summary views.
- **Monitor Instances**: Same OData query support as components. The instance object contains point-in-time health state -- check for nested health criteria and child monitor references.
- **Notification Settings**: Simpler paginated list (`$skiptoken` only). PUT replaces the entire notification setting -- always GET the current value first to avoid overwriting fields.
- **Subscription Summaries**: Aggregate views across all resource groups. These endpoints support the full OData query set -- use `$filter` and `$apply` to build dashboard-level health rollups without fetching per-resource data.
- **Operations**: Returns available API operations for RBAC and discoverability. Paginated via `$skiptoken`.
- **Errors**: All endpoints return 200 on success. Expect standard Azure error response bodies (`error.code`, `error.message`) on 4xx/5xx. Always include `api-version=2018-08-31-preview` as a query parameter.

## Anomaly Flags

- **Preview API version**: This API uses `2018-08-31-preview` -- surface a warning that this is a preview version that may have breaking changes or be deprecated without notice.
- **Stale preview date**: The spec dates to 2018, which is notably old for a preview API. Flag that the user should verify this API version is still supported in their Azure subscription.
- **Health state transitions**: When polling monitor instances, flag any state change from healthy to warning/critical between calls.
- **Pagination truncation**: If a response includes `nextLink`, proactively note that results are incomplete and more pages are available -- do not silently return partial data.
- **Empty monitor lists**: If a resource returns zero monitors or components, flag that Workload Monitor may not be enabled or supported for that resource type.
- **PATCH side effects**: When updating a monitor, warn that changes may affect dependent monitor instances and notification behavior.
- **Missing required path segments**: All resource-scoped endpoints need `resourceNamespace`, `resourceType`, and `resourceName` -- surface clear errors early if any are missing rather than letting Azure return a generic 404.
- **Throttling**: Azure ARM APIs enforce per-subscription rate limits. Surface HTTP 429 responses and `Retry-After` headers proactively.

## Playbook

### 1. Assess workload health for a specific VM

1. Identify the target resource's subscription ID, resource group, namespace (`Microsoft.Compute`), type (`virtualMachines`), and name.
2. GET `.../providers/Microsoft.WorkloadMonitor/monitors` to list all monitors on the VM.
3. For any monitor showing a non-healthy state, GET `.../monitors/{monitorId}` to retrieve detailed configuration and state.
4. GET `.../monitorInstances` with `$filter` to find instances in warning or critical state.
5. GET `.../components` to understand which OS/application components are being tracked and their health.

### 2. Set up notification settings for a resource

1. GET `.../notificationSettings` to check existing notification configurations.
2. If a setting exists, GET `.../notificationSettings/{notificationSettingName}` to retrieve its current configuration.
3. Construct the full notification setting body (include action groups, email targets, severity thresholds).
4. PUT `.../notificationSettings/{notificationSettingName}` with the complete body to create or replace the setting.
5. GET the setting back to confirm it was applied correctly.

### 3. Build a subscription-wide health dashboard

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.WorkloadMonitor/componentsSummary` with `$apply=groupby(...)` to aggregate component health by state.
2. GET `/subscriptions/{subscriptionId}/providers/Microsoft.WorkloadMonitor/monitorInstancesSummary` with `$filter` to isolate unhealthy instances.
3. Use `$top` and `$orderby` to rank the most critical issues first.
4. Follow pagination via `$skiptoken` if the result set is large.
5. For any critical instance in the summary, drill into the resource-level monitor instance endpoint to get full diagnostics.

### 4. Update monitor thresholds on a resource

1. GET `.../monitors` to list all monitors and identify the target monitor by name or type.
2. GET `.../monitors/{monitorId}` to retrieve the current configuration including thresholds.
3. Construct a PATCH body containing only the fields to update (threshold values, enabled state).
4. PATCH `.../monitors/{monitorId}` with the update body.
5. GET the monitor again to verify changes took effect, then check `.../monitorInstances` to confirm the new thresholds are reflected in instance evaluations.

### 5. Investigate a specific failing component

1. GET `.../components` with `$filter` to narrow down components in an error or warning state.
2. GET `.../components/{componentId}` with `$expand` to retrieve the component and its related monitor details in a single call.
3. GET `.../monitorInstances` with `$filter` scoped to instances related to that component.
4. GET `.../monitors` to understand which monitors govern the failing component and review their threshold configuration.
5. If thresholds need adjustment, PATCH the relevant monitor. If notifications are needed, PUT a notification setting targeting the appropriate severity.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
