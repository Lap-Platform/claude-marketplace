---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans -- verify access

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans | List all plans across all subscriptions. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans | Get the list of plans under a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} | Get the specified plan. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} | Create or update the plan. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} | Delete the specified plan. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metrics | Get the metrics of the specified plan. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metricDefinitions | Get the metric definitions of the specified plan. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all plans?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans
- "List all plans?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans
- "Get plan details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "Update a plan?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "Delete a plan?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "List all metrics?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metrics
- "List all metricDefinitions?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metricDefinitions
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
