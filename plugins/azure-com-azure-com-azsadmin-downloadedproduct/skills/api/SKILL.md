---
name: azurebridgeadminclient
description: "AzureBridgeAdminClient API skill. Use when working with AzureBridgeAdminClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureBridgeAdminClient
API version: 2016-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts | Get a list of downloaded products. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName} | Get a downloaded product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName} | Delete a downloaded product. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName} | Creates a downloaded product. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all downloadedProducts?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts
- "Get downloadedProduct details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Delete a downloadedProduct?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Update a downloadedProduct?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
