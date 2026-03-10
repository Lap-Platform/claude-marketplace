---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for providers, subscriptions. Covers 6 endpoints."
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
2. GET /providers/Microsoft.Storage.Admin/operations -- verify access

## Endpoints

6 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Storage.Admin/operations | Get the list of support rest operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/asyncOperations/{asyncOperationId} | Returns the async operation specified by asyncOperationId. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices | Returns the storage services list under the specified resource group and subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/storageServices | Returns the storage services list under the specified subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName} | Returns the specified storage service. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName} | Create the specified storage resource. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.Storage.Admin/operations
- "Get asyncOperation details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/asyncOperations/{asyncOperationId}
- "List all storageServices?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices
- "List all storageServices?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/storageServices
- "Get storageService details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}
- "Update a storageService?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
