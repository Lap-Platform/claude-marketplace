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

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Storage Admin?" -> GET /providers/Microsoft.Storage.Admin/operations
- "List all storage services in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/storageServices
- "Show storage services in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices
- "Get details for a specific storage service" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}
- "Create a new storage service" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}
- "Update an existing storage service configuration" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}
- "Check the status of a long-running storage operation" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/asyncOperations/{asyncOperationId}
- "Is my storage provisioning operation complete?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/asyncOperations/{asyncOperationId}
- "What storage services exist across all my resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/storageServices
- "Does a specific storage service already exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}
- "Set up storage infrastructure in a resource group" -> PUT .../{serviceName} (after checking with GET .../{serviceName})
- "Compare storage services between two resource groups" -> GET .../storageServices (call twice with different resourceGroup values)
- "Which API version should I use for Storage Admin?" -> All endpoints require `api-version=2019-08-08-preview` as a query parameter

## Response Tips

- **Operations** (`/providers/.../operations`): Returns an array of available operations with display metadata; useful for RBAC audits and documentation, not paginated.
- **Storage services lists** (`/storageServices`): May return paginated results via `nextLink`; follow `nextLink` until absent to collect all items. Each item nests properties under a `properties` object.
- **Storage service detail** (`/storageServices/{serviceName}`): Returns a single resource object; check `properties.provisioningState` for current lifecycle status (e.g., `Succeeded`, `Creating`, `Failed`).
- **Storage service create/update** (PUT): Returns the resource representation on 200; a 201 or 202 may indicate async creation -- check response headers for `Azure-AsyncOperation` or `Location` URLs.
- **Async operations** (`/asyncOperations/{asyncOperationId}`): Returns a status object with `status` field (`InProgress`, `Succeeded`, `Failed`); poll until terminal state.

## Anomaly Flags

- **`api-version` is a preview release** (`2019-08-08-preview`): Surface a warning that this API version may have breaking changes or be deprecated. Recommend checking for GA versions.
- **Async operation stuck in `InProgress`**: If polling an async operation returns `InProgress` for more than 10 minutes, flag it -- provisioning may be stalled.
- **Async operation `Failed` status**: Immediately surface the error code and message from the response body; do not silently continue.
- **PUT returning 202 (Accepted)**: The operation is long-running. Extract the `asyncOperationId` from response headers and begin polling -- do not assume the resource is ready.
- **HTTP 409 (Conflict)**: A storage service with that name likely already exists or is being modified; surface the conflict and suggest a GET to check current state before retrying.
- **HTTP 429 (Too Many Requests)**: Azure ARM throttling is active. Surface the `Retry-After` header value and pause before retrying.
- **Missing or empty `nextLink` on large subscriptions**: If a list call returns many items with no `nextLink`, results may be truncated by a server-side cap; flag this for manual verification.

## Playbook

### 1. Provision a New Storage Service

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}` to check if the service already exists.
2. If 404, call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}` with the desired configuration body.
3. If the PUT returns 202, extract the `asyncOperationId` from the `Azure-AsyncOperation` header.
4. Poll GET `/subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/asyncOperations/{asyncOperationId}` until `status` is `Succeeded` or `Failed`.
5. On success, confirm by fetching the service detail with GET.

### 2. Inventory All Storage Services Across a Subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/storageServices` with the required `api-version` query parameter.
2. Collect all items from the `value` array in the response.
3. If `nextLink` is present, follow it with a GET request and append results.
4. Repeat until no `nextLink` is returned.
5. Aggregate results by resource group using the `id` field to extract group names.

### 3. Monitor a Long-Running Operation

1. After initiating a PUT (create/update), capture the `asyncOperationId` from the response headers.
2. Determine the `location` from the resource's region or the operation URL.
3. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/asyncOperations/{asyncOperationId}`.
4. If `status` is `InProgress`, wait the interval suggested by `Retry-After` (or default to 15 seconds) and poll again.
5. On `Succeeded`, proceed with next steps. On `Failed`, extract and surface the error details from `error.code` and `error.message`.

### 4. Audit Available Admin Operations

1. Call GET `/providers/Microsoft.Storage.Admin/operations` to retrieve all supported operations.
2. Parse the response array; each entry includes `name` (e.g., `Microsoft.Storage.Admin/storageServices/read`) and a `display` object.
3. Cross-reference with your Azure RBAC role assignments to verify which operations your service principal can perform.
4. Flag any operations your workflows depend on that are not covered by current permissions.

### 5. Update Storage Service Configuration

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Storage.Admin/storageServices/{serviceName}` to retrieve the current configuration.
2. Modify the desired fields in the returned resource body (preserve `etag` if present for optimistic concurrency).
3. Call PUT with the full modified resource body to the same path.
4. If 200, the update was synchronous -- verify the returned properties match expectations.
5. If 202, follow the async operation polling playbook (Playbook 3) to confirm completion.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
