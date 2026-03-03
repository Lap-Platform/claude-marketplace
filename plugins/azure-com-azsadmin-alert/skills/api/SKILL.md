---
name: infrastructureinsightsmanagementclient
description: "InfrastructureInsightsManagementClient API skill. Use when working with InfrastructureInsightsManagementClient for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}/repair -- create first repair

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts | Returns the list of all alerts in a given region. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName} | Returns the requested an alert. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName} | Closes the given alert. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}/repair | Repairs an alert. |

## Enhanced Skill Content
## Question Mapping

- "What alerts are active in my Azure Stack region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts
- "Show me all infrastructure alerts for resource group X" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts
- "Get details on a specific infrastructure alert" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}
- "What is the severity of alert {alertName}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}
- "Close an infrastructure alert" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}
- "Update the state of an alert to dismissed" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}
- "Repair the issue causing an alert" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}/repair
- "Trigger remediation for a failed infrastructure component" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}/repair
- "Are there any critical alerts in location eastus?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts
- "How do I acknowledge an alert without repairing it?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.InfrastructureInsights.Admin/regionHealths/{location}/alerts/{alertName}
- "List all open alerts then repair the critical ones" -> GET .../alerts then POST .../alerts/{alertName}/repair (multi-step)
- "What alerts exist and which can be auto-repaired?" -> GET .../alerts followed by inspecting each alert's `remediation` field
- "Check if a repair action succeeded for a specific alert" -> POST .../alerts/{alertName}/repair (check 200 vs 202), then GET .../alerts/{alertName}

## Response Tips

- **Alert listings (GET .../alerts):** Returns a `value` array of alert objects. Check for `nextLink` property for pagination -- follow it until absent. Filter client-side by `properties.severity` (Critical, Warning, Informational) and `properties.state` (Active, Closed).
- **Single alert (GET .../alerts/{alertName}):** Returns a flat alert object with `properties` containing `title`, `severity`, `state`, `impactedResourceDisplayName`, `remediation`, and timestamps. Missing `remediation` means no auto-fix available.
- **Alert update (PUT .../alerts/{alertName}):** Requires the full alert object in the `alert` body parameter and a `user` parameter. Returns the updated alert. A 200 confirms immediate success.
- **Repair action (POST .../repair):** Returns 200 for synchronous completion or 202 for async (long-running). On 202, check the `Location` or `Azure-AsyncOperation` response header to poll for completion status.

## Anomaly Flags

- **202 on repair:** The repair is running asynchronously. Surface the async operation URL and remind the user to poll for completion rather than assuming success.
- **Critical severity alerts:** Proactively highlight any alert with `severity: Critical` when listing alerts -- these indicate service-impacting issues.
- **Stale alerts:** Flag alerts where `lastUpdatedTimestamp` is significantly older than `createdTimestamp` with state still Active -- these may be stuck or overlooked.
- **Repair without remediation:** If a user attempts repair on an alert whose `remediation` field is empty or null, warn that the alert may not support automated repair.
- **Throttling (429):** Azure ARM APIs enforce rate limits. Surface `Retry-After` header value and pause before retrying.
- **Alert state mismatch:** After a PUT to close an alert, if a subsequent GET still shows Active state, flag a potential sync delay or permission issue.

## Playbook

### 1. Triage All Active Alerts in a Region

1. Call GET .../regionHealths/{location}/alerts to retrieve all alerts
2. Filter the `value` array for entries where `properties.state` is `Active`
3. Sort by `properties.severity` (Critical first, then Warning, then Informational)
4. For each critical alert, call GET .../alerts/{alertName} to get full details including `remediation` guidance
5. Present a summary table: alert name, severity, impacted resource, and whether auto-repair is available

### 2. Repair a Failing Infrastructure Component

1. Call GET .../alerts/{alertName} to confirm the alert exists and is Active
2. Check `properties.remediation` to verify auto-repair is supported for this alert type
3. Call POST .../alerts/{alertName}/repair to trigger remediation
4. If response is 200: repair completed -- verify by re-fetching the alert with GET
5. If response is 202: extract the async operation URL from response headers, poll until the operation completes, then verify the alert state

### 3. Dismiss a Non-Critical Alert

1. Call GET .../alerts/{alertName} to retrieve the current alert object
2. Modify the alert's `properties.state` to `Closed` in the response body
3. Call PUT .../alerts/{alertName} with the `user` parameter (your identity) and the modified `alert` object as body
4. Confirm the response returns 200 with the updated alert showing `state: Closed`

### 4. Monitor and Respond to New Alerts

1. Call GET .../alerts and record all current alert names and their `lastUpdatedTimestamp`
2. On subsequent polling intervals, call GET .../alerts again
3. Diff the results: new entries in `value` that were not in the previous set are new alerts
4. For any new Critical alert, immediately fetch full details with GET .../alerts/{alertName}
5. If `remediation` is available, offer to trigger POST .../alerts/{alertName}/repair automatically

### 5. Bulk Close Resolved Alerts

1. Call GET .../alerts to list all alerts (follow `nextLink` for full pagination)
2. Filter for alerts where `properties.state` is `Active` but the underlying issue is resolved
3. For each alert to close, call GET .../alerts/{alertName} to get the full object
4. Modify `properties.state` to `Closed` and call PUT .../alerts/{alertName} with user context
5. Log each closure result and flag any that return non-200 for manual review


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
