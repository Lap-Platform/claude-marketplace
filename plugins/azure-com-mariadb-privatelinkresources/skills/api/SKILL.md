---
name: mariadbmanagementclient
description: "MariaDBManagementClient API skill. Use when working with MariaDBManagementClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# MariaDBManagementClient
API version: 2018-06-01-privatepreview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/privateLinkResources -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/privateLinkResources | Gets the private link resources for MariaDB server. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/privateLinkResources/{groupName} | Gets a private link resource for MariaDB server. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all privateLinkResources?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/privateLinkResources
- "Get privateLinkResource details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/privateLinkResources/{groupName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
