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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/queryTexts -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/resetQueryPerformanceInsightData -- create first resetQueryPerformanceInsightData

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/queryTexts/{queryId} | Retrieve the Query-Store query texts for the queryId. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/queryTexts | Retrieve the Query-Store query texts for specified queryIds. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/topQueryStatistics/{queryStatisticId} | Retrieve the query statistic for specified identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/topQueryStatistics | Retrieve the Query-Store top queries for specified metric and aggregation. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/waitStatistics/{waitStatisticsId} | Retrieve wait statistics for specified identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/waitStatistics | Retrieve wait statistics for specified aggregation window. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/resetQueryPerformanceInsightData | Reset data for Query Performance Insight. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get queryText details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/queryTexts/{queryId}
- "List all queryTexts?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/queryTexts
- "Get topQueryStatistic details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/topQueryStatistics/{queryStatisticId}
- "List all topQueryStatistics?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/topQueryStatistics
- "Get waitStatistic details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/waitStatistics/{waitStatisticsId}
- "List all waitStatistics?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/waitStatistics
- "Create a resetQueryPerformanceInsightData?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DBforMariaDB/servers/{serverName}/resetQueryPerformanceInsightData
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
