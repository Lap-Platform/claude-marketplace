---
name: azure-alerts-management-service-resource-provider
description: "Azure Alerts Management Service Resource Provider API skill. Use when working with Azure Alerts Management Service Resource Provider for providers, subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Alerts Management Service Resource Provider
API version: 2019-05-05-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.AlertsManagement/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/changestate -- create first changestate

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.AlertsManagement/operations | List all operations available through Azure Alerts Management Resource Provider. |
| GET | /providers/Microsoft.AlertsManagement/alertsMetaData | List alerts meta data information based on value of identifier parameter. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts | List all existing alerts, where the results can be filtered on the basis of multiple parameters (e.g. time range). The results can then be sorted on the basis specific fields, with the default being lastModifiedDateTime. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId} | Get a specific alert. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/changestate | Change the state of an alert. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/history | Get the history of an alert, which captures any monitor condition changes (Fired/Resolved) and alert state changes (New/Acknowledged/Closed). |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alertsSummary | Get a summarized count of your alerts grouped by various parameters (e.g. grouping by 'Severity' returns the count of alerts for each severity). |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Alerts Management API?" -> GET /providers/Microsoft.AlertsManagement/operations
- "What alert metadata is available?" -> GET /providers/Microsoft.AlertsManagement/alertsMetaData
- "List all alerts in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts
- "Show me only critical severity alerts" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts (with severity filter)
- "Get alerts for a specific resource group" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts (with targetResourceGroup filter)
- "Get details for a specific alert" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}
- "Acknowledge this alert" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/changestate
- "Close an alert with a comment" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/changestate (with comment body)
- "Show the history of changes for an alert" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/history
- "Give me a summary of alerts grouped by severity" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alertsSummary (groupby=severity)
- "How many alerts are in each state?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alertsSummary (groupby=alertState)
- "Show alerts from the last hour" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts (with timeRange=1h)
- "Filter alerts by a specific monitor service" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts (with monitorService filter)
- "Are there any alerts linked to a specific smart group?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts (with smartGroupId filter)

## Response Tips

- **Operations & Metadata** (`/providers/...`): Returns flat lists; operations include display descriptions useful for building dynamic UIs.
- **Alert Listings** (`/alerts`): Paginated via `pageCount` and `nextLink` in the response body -- follow `nextLink` until absent to retrieve all pages.
- **Single Alert** (`/alerts/{alertId}`): Returns a deeply nested object; key fields live under `properties` (essentials, context, egressConfig). Check `includeContext=true` if context is empty.
- **Change State** (`/alerts/{alertId}/changestate`): Returns the updated alert object; verify `properties.essentials.alertState` matches your requested `newState`.
- **Alert History** (`/alerts/{alertId}/history`): Returns chronological modification events; each entry includes `modifiedBy`, `modifiedAt`, and `description` for audit trails.
- **Alerts Summary** (`/alertsSummary`): Shape varies by `groupby` parameter; response nests counts under `properties.smartGroups` and `properties.values`.

## Anomaly Flags

- **Throttling**: Surface HTTP 429 responses immediately; Azure ARM enforces per-subscription read/write limits (typically 12000 reads/hour). Back off using the `Retry-After` header.
- **Stale API Version**: The spec uses `2019-05-05-preview` (a preview version). Flag if Azure returns `InvalidApiVersionParameter` -- a newer stable version may be required.
- **Large Alert Volumes**: If the initial page returns `nextLink` and `pageCount` is not set, warn the user that full enumeration may be slow. Suggest adding filters (severity, timeRange, alertState).
- **State Transition Failures**: If `changestate` returns 409 Conflict, the alert is likely already in the target state or has been auto-resolved. Surface the current state from the error body.
- **Empty Context**: If `properties.context` is null on a detail fetch, remind the user to retry with `includeContext=true` -- context is omitted by default to reduce payload size.
- **Deprecated Monitor Services**: If `monitorService` filter returns zero results, flag that the service name may have been renamed or deprecated in newer API versions.

## Playbook

### 1. Triage New Alerts

1. List all alerts filtered to "New" state: `GET /alerts?alertState=New&sortBy=lastModifiedDateTime&sortOrder=desc`
2. Review each alert's details: `GET /alerts/{alertId}` with `includeContext=true`
3. Acknowledge actionable alerts: `POST /alerts/{alertId}/changestate?newState=Acknowledged` with a triage comment
4. Close false positives: `POST /alerts/{alertId}/changestate?newState=Closed` with a justification comment

### 2. Investigate a Specific Alert

1. Fetch alert details: `GET /alerts/{alertId}`
2. Review the full modification history: `GET /alerts/{alertId}/history`
3. Check related alerts by filtering on the same target resource: `GET /alerts?targetResource={resourceId}`
4. If part of a smart group, list sibling alerts: `GET /alerts?smartGroupId={smartGroupId}`

### 3. Generate an Executive Summary

1. Get alert counts grouped by severity: `GET /alertsSummary?groupby=severity`
2. Get alert counts grouped by state: `GET /alertsSummary?groupby=alertState`
3. Optionally narrow by time window: add `timeRange=1d` for a daily report
4. Combine both summaries to present a severity-by-state matrix

### 4. Monitor a Specific Resource Group

1. List alerts scoped to the resource group: `GET /alerts?targetResourceGroup={rgName}&timeRange=1d`
2. Summarize by severity: `GET /alertsSummary?groupby=severity&targetResourceGroup={rgName}`
3. Identify recurring alert rules: `GET /alertsSummary?groupby=alertRule&targetResourceGroup={rgName}`
4. Acknowledge or close resolved alerts in bulk by iterating and calling `POST /alerts/{alertId}/changestate`

### 5. Audit Alert State Changes

1. Identify the alert to audit: `GET /alerts/{alertId}`
2. Pull the full history: `GET /alerts/{alertId}/history`
3. Review each history entry for `modifiedBy` (user or system), timestamp, and old/new state values
4. Flag any unexpected transitions (e.g., alerts closed without comments, or state changes by unrecognized principals)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
