---
name: hdinsightmanagementclient
description: "HDInsightManagementClient API skill. Use when working with HDInsightManagementClient for subscriptions. Covers 6 endpoints."
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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/capabilities -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/checkNameAvailability -- create first checkNameAvailability

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/capabilities | Gets the capabilities for the specified location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/usages | Lists the usages for the specified location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/billingSpecs | Lists the billingSpecs for the specified subscription and location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/azureasyncoperations/{operationId} | Get the async operation status. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/checkNameAvailability | Check the cluster name is available or not. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/validateCreateRequest | Validate the cluster create request spec is valid or not. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all capabilities?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/capabilities
- "List all usages?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/usages
- "List all billingSpecs?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/billingSpecs
- "Get azureasyncoperation details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/azureasyncoperations/{operationId}
- "Create a checkNameAvailability?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/checkNameAvailability
- "Create a validateCreateRequest?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/validateCreateRequest
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
