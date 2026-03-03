---
name: mariadbmanagementclient
description: "MariaDBManagementClient API skill. Use when working with MariaDBManagementClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# MariaDBManagementClient
API version: 2018-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/createRecommendedActionSession -- create first createRecommendedActionSession

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName} | Get a recommendation action advisor. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors | List recommendation action advisors. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/createRecommendedActionSession | Create recommendation action session for the advisor. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/recommendedActions/{recommendedActionName} | Retrieve recommended actions from the advisor. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/recommendedActions | Retrieve recommended actions from the advisor. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DBforMariaDB/locations/{locationName}/recommendedActionSessionsAzureAsyncOperation/{operationId} | Recommendation action session operation status. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DBforMariaDB/locations/{locationName}/recommendedActionSessionsOperationResults/{operationId} | Recommendation action session operation result. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get advisor details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}
- "List all advisors?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors
- "Create a createRecommendedActionSession?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/createRecommendedActionSession
- "Get recommendedAction details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/recommendedActions/{recommendedActionName}
- "List all recommendedActions?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/advisors/{advisorName}/recommendedActions
- "Get recommendedActionSessionsAzureAsyncOperation details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DBforMariaDB/locations/{locationName}/recommendedActionSessionsAzureAsyncOperation/{operationId}
- "Get recommendedActionSessionsOperationResult details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DBforMariaDB/locations/{locationName}/recommendedActionSessionsOperationResults/{operationId}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
