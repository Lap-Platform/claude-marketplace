---
name: networkmanagementclient
description: "NetworkManagementClient API skill. Use when working with NetworkManagementClient for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# NetworkManagementClient
API version: 2019-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName} | Gets the specified ipGroups. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName} | Creates or updates an ipGroups in a specified resource group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName} | Updates tags of an IpGroups resource. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName} | Deletes the specified ipGroups. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups | Gets all IpGroups in a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network/ipGroups | Gets all IpGroups in a subscription. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get ipGroup details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName}
- "Update a ipGroup?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName}
- "Partially update a ipGroup?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName}
- "Delete a ipGroup?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups/{ipGroupsName}
- "List all ipGroups?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/ipGroups
- "List all ipGroups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/ipGroups
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
