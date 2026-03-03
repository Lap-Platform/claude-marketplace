---
name: mixed-reality
description: "Mixed Reality API skill. Use when working with Mixed Reality for subscriptions. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Mixed Reality
API version: 2019-12-02-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.MixedReality/spatialAnchorsAccounts -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}/keys -- create first keys

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.MixedReality/spatialAnchorsAccounts | List Spatial Anchors Accounts by Subscription |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts | List Resources by Resource Group |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName} | Delete a Spatial Anchors Account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName} | Retrieve a Spatial Anchors Account. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName} | Updating a Spatial Anchors Account |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName} | Creating or Updating a Spatial Anchors Account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}/keys | Get Both of the 2 Keys of a Spatial Anchors Account |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}/keys | Regenerate specified Key of a Spatial Anchors Account |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all spatialAnchorsAccounts?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.MixedReality/spatialAnchorsAccounts
- "List all spatialAnchorsAccounts?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts
- "Delete a spatialAnchorsAccount?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}
- "Get spatialAnchorsAccount details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}
- "Partially update a spatialAnchorsAccount?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}
- "Update a spatialAnchorsAccount?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}
- "List all keys?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}/keys
- "Create a key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MixedReality/spatialAnchorsAccounts/{accountName}/keys
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
