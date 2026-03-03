---
name: hdinsightmanagementclient
description: "HDInsightManagementClient API skill. Use when working with HDInsightManagementClient for subscriptions. Covers 13 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/roles/{roleName}/resize -- create first resize

## Endpoints

13 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName} | Creates a new HDInsight cluster with the specified parameters. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName} | Patch HDInsight cluster with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName} | Deletes the specified HDInsight cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName} | Gets the specified cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters | Lists the HDInsight clusters in a resource group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/roles/{roleName}/resize | Resizes the specified HDInsight cluster to the specified size. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/roles/{roleName}/autoscale | Updates the Autoscale Configuration for HDInsight cluster. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/clusters | Lists all the HDInsight clusters under the subscription. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/rotatediskencryptionkey | Rotate disk encryption key of the specified HDInsight cluster. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/getGatewaySettings | Gets the gateway settings for the specified cluster. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/updateGatewaySettings | Configures the gateway settings on the specified cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/azureasyncoperations/{operationId} | The the async operation status. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/updateClusterIdentityCertificate | Updates the cluster identity certificate. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Update a cluster?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}
- "Partially update a cluster?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}
- "Delete a cluster?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}
- "Get cluster details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}
- "List all clusters?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters
- "Create a resize?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/roles/{roleName}/resize
- "Create a autoscale?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/roles/{roleName}/autoscale
- "List all clusters?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/clusters
- "Create a rotatediskencryptionkey?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/rotatediskencryptionkey
- "Create a getGatewaySetting?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/getGatewaySettings
- "Create a updateGatewaySetting?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/updateGatewaySettings
- "Get azureasyncoperation details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/azureasyncoperations/{operationId}
- "Create a updateClusterIdentityCertificate?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clusterName}/updateClusterIdentityCertificate
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
