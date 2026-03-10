---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2019-08-08-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete -- create first undelete

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts | Returns a list of storage accounts. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId} | Returns the requested storage account. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete | Undelete a deleted storage account with new account name if the a new name is provided. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/reclaimStorageCapacity | Start reclaim storage capacity on deleted storage objects. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all storageAccounts?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts
- "Get storageAccount details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}
- "Create a undelete?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete
- "Create a reclaimStorageCapacity?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/reclaimStorageCapacity
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
