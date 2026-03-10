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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.AlertsManagement/operations
- "List all alertsMetaData?" -> GET /providers/Microsoft.AlertsManagement/alertsMetaData
- "List all alerts?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts
- "Get alert details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}
- "Create a changestate?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/changestate
- "List all history?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alerts/{alertId}/history
- "List all alertsSummary?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AlertsManagement/alertsSummary
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
