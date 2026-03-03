---
name: storage-cache-mgmt-client
description: "Storage Cache Mgmt Client API skill. Use when working with Storage Cache Mgmt Client for providers, subscriptions. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# Storage Cache Mgmt Client
API version: 2019-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com/

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.StorageCache/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/flush -- create first flush

## Endpoints

17 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.StorageCache/operations | Lists all of the available Resource Provider operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StorageCache/skus | Get the list of StorageCache.Cache SKUs available to this subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StorageCache/usageModels | Get the list of Cache Usage Models available to this subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StorageCache/caches | Returns all Caches the user has access to under a subscription. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches | Returns all Caches the user has access to under a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName} | Schedules a Cache for deletion. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName} | Returns a Cache. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName} | Create or update a Cache. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName} | Update a Cache instance. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/flush | Tells a Cache to write all dirty data to the Storage Target(s). During the flush, clients will see errors returned until the flush is complete. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/start | Tells a Stopped state Cache to transition to Active state. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/stop | Tells an Active Cache to transition to Stopped state. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/storageTargets | Returns a list of Storage Targets for the specified Cache. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/storageTargets/{storageTargetName} | Removes a Storage Target from a Cache. This operation is allowed at any time, but if the Cache is down or unhealthy, the actual removal of the Storage Target may be delayed until the Cache is healthy again. Note that if the Cache has data to flush to the Storage Target, the data will be flushed before the Storage Target will be deleted. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/storageTargets/{storageTargetName} | Returns a Storage Target from a Cache. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/storageTargets/{storageTargetName} | Create or update a Storage Target. This operation is allowed at any time, but if the Cache is down or unhealthy, the actual creation/modification of the Storage Target may be delayed until the Cache is healthy again. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/upgrade | Upgrade a Cache's firmware if a new version is available. Otherwise, this operation has no effect. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Azure Storage Cache?" -> GET /providers/Microsoft.StorageCache/operations
- "What cache SKUs can I use in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StorageCache/skus
- "What usage models are available for storage caches?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StorageCache/usageModels
- "List all storage caches in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StorageCache/caches
- "List caches in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches
- "Get details of a specific cache" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}
- "Create a new storage cache" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}
- "Update an existing cache's configuration" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}
- "Delete a storage cache" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}
- "Flush cache data to storage targets" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/flush
- "Start a stopped cache" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/start
- "Stop a running cache" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/stop
- "Upgrade a cache's firmware" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/upgrade
- "List all storage targets attached to a cache" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/storageTargets
- "Add or replace a storage target on a cache" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StorageCache/caches/{cacheName}/storageTargets/{storageTargetName}

## Response Tips

- **Operations/SKUs/Usage Models (GET list endpoints):** Responses contain a `value` array and optional `nextLink` for pagination -- follow `nextLink` until null to retrieve all results.
- **Cache CRUD (GET/PUT/PATCH single resource):** Returns the full cache object with nested `properties` containing `provisioningState`, `health`, and `subnet`; check `provisioningState` for async completion.
- **Async actions (DELETE/flush/start/stop/upgrade):** 202 means the operation was accepted but not complete -- poll the `Location` or `Azure-AsyncOperation` header URL until terminal state. 204 means the resource was already gone (DELETE) or no action needed.
- **Create/Update (PUT returning 201):** 201 indicates a new resource was created; 200 indicates an existing resource was updated in place.
- **Error responses:** All endpoints return a `CloudError` object with `error.code` and `error.message` -- surface these directly to the user.

## Anomaly Flags

- **Provisioning stuck:** If a cache's `provisioningState` remains in `Creating`, `Updating`, or `Deleting` for more than 20 minutes after a mutation, surface a warning.
- **Degraded health:** When `properties.health.state` is anything other than `Healthy` (e.g., `Degraded`, `Down`, `Transitioning`), proactively alert the user.
- **202 without async header:** If a delete, flush, start, stop, or upgrade returns 202 but no `Azure-AsyncOperation` or `Location` header, flag that the operation cannot be tracked.
- **SKU capacity limits:** When listing SKUs, flag any SKU where `restrictions` is non-empty -- these indicate regional or quota-based limitations.
- **Stale api-version:** If the response includes `x-ms-deprecation` headers or the error code is `InvalidApiVersionParameter`, advise upgrading the `api-version` query parameter.
- **Storage target count:** If a cache has 10+ storage targets, note that this approaches typical per-cache limits and may affect performance.

## Playbook

### 1. Provision a New Cache End-to-End

1. List available SKUs: GET `/subscriptions/{sub}/providers/Microsoft.StorageCache/skus` to pick a valid cache size and tier.
2. List usage models: GET `/subscriptions/{sub}/providers/Microsoft.StorageCache/usageModels` to select the read/write pattern that matches your workload.
3. Create the cache: PUT `/subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.StorageCache/caches/{name}` with the `cache` body containing SKU, subnet, and cache size.
4. Poll the cache: GET the same cache URL and check `properties.provisioningState` until it reaches `Succeeded`.
5. Add a storage target: PUT `/subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.StorageCache/caches/{name}/storageTargets/{targetName}` with NFS or blob target details.

### 2. Safely Decommission a Cache

1. Flush the cache: POST `.../caches/{name}/flush` to ensure all dirty data is written to backend storage targets.
2. Poll for flush completion using the `Azure-AsyncOperation` header URL until status is `Succeeded`.
3. Stop the cache: POST `.../caches/{name}/stop` and wait for 200 or poll 202 to completion.
4. Delete each storage target: DELETE `.../storageTargets/{targetName}` for each target (list them first via GET).
5. Delete the cache: DELETE `.../caches/{name}` and confirm with a 200 or 204 response.

### 3. Perform a Cache Firmware Upgrade

1. Get current cache state: GET `.../caches/{name}` and check `properties.upgradeStatus` for available firmware version.
2. Flush the cache: POST `.../caches/{name}/flush` to ensure data consistency before upgrade.
3. Trigger upgrade: POST `.../caches/{name}/upgrade` -- expect 201 or 202.
4. Monitor progress: Poll the cache GET endpoint and watch `provisioningState` and `upgradeStatus` until the upgrade completes.

### 4. Replace a Storage Target

1. Get the current storage target: GET `.../storageTargets/{targetName}` to capture existing configuration.
2. Flush the cache: POST `.../caches/{name}/flush` to write back pending data.
3. Delete the old target: DELETE `.../storageTargets/{targetName}` and wait for completion.
4. Create the new target: PUT `.../storageTargets/{newTargetName}` with updated backend storage details.
5. Verify: GET the new target and confirm `provisioningState` is `Succeeded`.

### 5. Inventory All Caches Across Resource Groups

1. List all caches subscription-wide: GET `/subscriptions/{sub}/providers/Microsoft.StorageCache/caches`.
2. Follow `nextLink` pagination until all caches are collected.
3. For each cache, inspect `properties.health.state` and `provisioningState` to build a health summary.
4. For caches in non-healthy states, GET `.../caches/{name}/storageTargets` to check if storage target issues are the root cause.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
