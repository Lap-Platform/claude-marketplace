---
name: networkmanagementclient
description: "NetworkManagementClient API skill. Use when working with NetworkManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# NetworkManagementClient
API version: 2019-07-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/bastionHosts -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts/{bastionHostName} | Deletes the specified Bastion Host. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts/{bastionHostName} | Gets the specified Bastion Host. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts/{bastionHostName} | Creates or updates the specified Bastion Host. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network/bastionHosts | Lists all Bastion Hosts in a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts | Lists all Bastion Hosts in a resource group. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Delete a bastionHost?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts/{bastionHostName}
- "Get bastionHost details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts/{bastionHostName}
- "Update a bastionHost?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts/{bastionHostName}
- "List all bastionHosts?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/bastionHosts
- "List all bastionHosts?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/bastionHosts
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
