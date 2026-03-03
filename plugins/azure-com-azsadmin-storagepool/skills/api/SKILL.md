---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# FabricAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}/storagePools -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}/storagePools/{storagePool} | Return the requested a storage pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}/storagePools | Returns a list of all storage pools for a location. |

## Enhanced Skill Content
## Question Mapping

- "What storage pools exist in this storage subsystem?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}/storagePools
- "Get details for a specific storage pool" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}/storagePools/{storagePool}
- "Does storage pool X exist in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}/storagePools/{storagePool}
- "List all storage pools for a given resource group and location" -> GET .../storagePools
- "Check the status of a storage pool" -> GET .../storagePools/{storagePool}
- "How many storage pools are in my storage subsystem?" -> GET .../storagePools
- "Verify a storage pool was provisioned correctly" -> GET .../storagePools/{storagePool}
- "Which storage pools are available at fabric location Y?" -> GET .../storagePools
- "Is storage pool Z returning a 404 (missing or deleted)?" -> GET .../storagePools/{storagePool}
- "Enumerate infrastructure pools before a maintenance window" -> GET .../storagePools
- "Get the properties and configuration of a named storage pool" -> GET .../storagePools/{storagePool}
- "Audit storage pool inventory across a storage subsystem" -> GET .../storagePools

## Response Tips

- **Single resource (GET .../storagePools/{storagePool})**: Returns a JSON object with `id`, `name`, `type`, `location`, and `properties` nested under the top-level resource. A 404 means the pool name is wrong or it was deleted -- check the `storagePool` path segment and confirm the parent `storageSubSystem` exists.
- **List endpoint (GET .../storagePools)**: Returns a JSON object with a `value` array. Azure ARM APIs may include a `nextLink` field for pagination -- if present, follow it with another GET to retrieve the next page. An empty `value` array means no pools exist under that subsystem, not an error.

## Anomaly Flags

- **404 on a previously known pool**: Surface immediately -- the storage pool may have been deleted or the parent storage subsystem/fabric location path is incorrect.
- **Empty list response**: Flag when `value` array is empty, as this may indicate a misconfigured path hierarchy (wrong subscriptionId, resourceGroupName, location, or storageSubSystem).
- **OAuth2 token expiry**: If a 401 is returned, proactively note that the OAuth2 bearer token may have expired and suggest re-authentication.
- **Throttling (429 responses)**: Azure ARM APIs enforce rate limits per subscription. Surface any 429 with the `Retry-After` header value and recommend backing off.
- **Unexpected properties shape**: If `properties` is null or missing expected fields on a 200 response, flag as a possible API version mismatch -- this spec targets `2016-05-01`.

## Playbook

### 1. Inventory All Storage Pools in a Subsystem

1. Authenticate and obtain an OAuth2 bearer token for `https://management.azure.com`.
2. Call `GET .../storagePools` with the full path including subscriptionId, resourceGroupName, location, and storageSubSystem.
3. Parse the `value` array from the response.
4. If `nextLink` is present, issue a GET to that URL and append results.
5. Repeat until no `nextLink` remains.

### 2. Inspect a Specific Storage Pool

1. Obtain the pool name from a prior list call or known configuration.
2. Call `GET .../storagePools/{storagePool}` with the pool name.
3. If 200, inspect `properties` for capacity, status, and configuration details.
4. If 404, verify the storagePool name spelling and confirm the parent storageSubSystem still exists by listing pools.

### 3. Validate Storage Subsystem Health

1. Call `GET .../storagePools` to list all pools under the target subsystem.
2. For each pool in the `value` array, call `GET .../storagePools/{storagePool}` to fetch full details.
3. Check each pool's `properties` for health indicators or provisioning state.
4. Flag any pools returning 404 (deleted out-of-band) or with unexpected property values.

### 4. Pre-Maintenance Audit

1. List all storage pools via `GET .../storagePools`.
2. Record the count and names as a baseline.
3. After maintenance, re-list and compare against the baseline.
4. For any missing pools, attempt a direct GET to confirm 404 vs. transient error.
5. Document discrepancies for the operations team.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
