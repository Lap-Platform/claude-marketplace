---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# MonitorManagementClient
API version: 2016-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName} | Creates or updates a classic metric alert rule. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName} | Deletes a classic metric alert rule |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName} | Gets a classic metric alert rule |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName} | Updates an existing classic metric AlertRuleResource. To update other fields use the CreateOrUpdate method. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules | List the classic metric alert rules within a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/alertrules | List the classic metric alert rules within a subscription. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Update a alertrule?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName}
- "Delete a alertrule?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName}
- "Get alertrule details?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName}
- "Partially update a alertrule?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules/{ruleName}
- "List all alertrules?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Insights/alertrules
- "List all alertrules?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/alertrules
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
