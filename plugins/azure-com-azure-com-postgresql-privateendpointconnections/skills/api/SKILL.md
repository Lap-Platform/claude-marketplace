---
name: postgresqlmanagementclient
description: "PostgreSQLManagementClient API skill. Use when working with PostgreSQLManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# PostgreSQLManagementClient
API version: 2018-06-01-privatepreview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName} | Gets a private endpoint connection. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName} | Approve or reject a private endpoint connection with a given name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName} | Deletes a private endpoint connection with a given name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName} | Updates tags on private endpoint connection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections | Gets all private endpoint connections on a server. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get privateEndpointConnection details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Update a privateEndpointConnection?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Delete a privateEndpointConnection?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Partially update a privateEndpointConnection?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections/{privateEndpointConnectionName}
- "List all privateEndpointConnections?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{serverName}/privateEndpointConnections
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
