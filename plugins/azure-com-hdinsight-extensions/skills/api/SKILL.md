---
name: hdinsightmanagementclient
description: "HDInsightManagementClient API skill. Use when working with HDInsightManagementClient for subscriptions. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# HDInsightManagementClient
API version: 2018-06-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/clustermonitoring -- verify access

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/clustermonitoring | Enables the Operations Management Suite (OMS) on the HDInsight cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/clustermonitoring | Gets the status of Operations Management Suite (OMS) on the HDInsight cluster. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/clustermonitoring | Disables the Operations Management Suite (OMS) on the HDInsight cluster. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/azureMonitor | Enables the Azure Monitor on the HDInsight cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/azureMonitor | Gets the status of Azure Monitor on the HDInsight cluster. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/azureMonitor | Disables the Azure Monitor on the HDInsight cluster. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName} | Creates an HDInsight cluster extension. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName} | Gets the extension properties for the specified HDInsight cluster extension. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName} | Deletes the specified extension for HDInsight cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName}/azureAsyncOperations/{operationId} | Gets the async operation status. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all clustermonitoring?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/clustermonitoring
- "List all azureMonitor?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/azureMonitor
- "Update a extension?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName}
- "Get extension details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName}
- "Delete a extension?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName}
- "Get azureAsyncOperation details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/extensions/{extensionName}/azureAsyncOperations/{operationId}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
