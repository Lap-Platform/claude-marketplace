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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare} | Returns the requested fabric file share. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares | Returns a list of all fabric file shares at a certain location. |

## Enhanced Skill Content
## Question Mapping

- "What file shares exist in this fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares
- "Get details for a specific file share" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare}
- "Is file share X present in location Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare}
- "List all file shares in my resource group's fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares
- "Check if a file share exists before provisioning" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare}
- "What are the properties of file share {name}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare}
- "How many file shares are deployed in location {location}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares
- "Enumerate storage file shares for capacity planning" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares
- "Verify a file share still exists after a maintenance window" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare}
- "Audit all file shares across a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares
- "Get the configuration of a named file share for drift detection" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares/{fileShare}
- "Which file shares are available to assign to new tenants?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/fileShares

## Response Tips

- **Single file share (GET .../{fileShare})**: Response is a single resource object with `id`, `name`, `type`, `location`, and `properties` nested object containing share-specific config. A 404 means the share name is wrong or was deleted -- do not retry, verify the name.
- **File share list (GET .../fileShares)**: Response contains a `value` array of file share objects. May include a `nextLink` property for pagination -- follow it until absent. An empty `value` array (not 404) means the location has no shares.
- **General**: All responses use `api-version=2016-05-01` as a query parameter. Auth failures return 401/403 -- confirm the OAuth2 token has the `Microsoft.Fabric.Admin/fabricLocations/fileShares/read` permission.

## Anomaly Flags

- **404 on list endpoint**: Indicates the fabric location or resource group itself does not exist -- surface this distinction to the user rather than reporting "no file shares found."
- **Stale API version**: This API uses version `2016-05-01`. If Azure returns a `x-ms-deprecated` header or suggests a newer version in error details, flag it immediately.
- **Missing nextLink on large results**: If the list returns exactly a round number of items (e.g., 100) with no `nextLink`, warn that results may be silently truncated.
- **Throttling headers**: Watch for `Retry-After` or `x-ms-ratelimit-remaining-*` headers. Surface when remaining calls drop below 20% of the limit.
- **Unexpected properties shape**: If a file share's `properties` object is missing expected fields or contains `provisioningState: "Failed"`, proactively alert -- the share may be unhealthy.

## Playbook

### 1. Inventory All File Shares in a Location

1. Call GET `.../fabricLocations/{location}/fileShares` with the target subscription, resource group, and location.
2. Collect the `value` array from the response.
3. If `nextLink` is present, follow it and append results until no `nextLink` remains.
4. Report the total count and summarize share names and key properties.

### 2. Verify a Specific File Share Exists

1. Call GET `.../fileShares/{fileShare}` with the exact share name.
2. If 200, confirm existence and return key properties (provisioning state, capacity).
3. If 404, report the share does not exist at that location and suggest listing all shares to check for typos.

### 3. Pre-Provisioning Check

1. List all file shares via GET `.../fileShares` to understand current allocation.
2. Review each share's `properties` for capacity and utilization if available.
3. Identify whether existing shares have room or a new share is needed.
4. Present a summary table of shares with their status before the user provisions.

### 4. Post-Maintenance Validation

1. Before maintenance, call GET `.../fileShares` and cache the full list as a baseline.
2. After maintenance, call the same endpoint again.
3. Compare the two lists: flag any shares missing from the post-maintenance response.
4. For each share that still exists, call GET `.../fileShares/{fileShare}` individually and verify `provisioningState` is healthy.
5. Report any discrepancies or degraded shares.

### 5. Cross-Location File Share Audit

1. Identify all fabric locations for the resource group (via a separate fabric locations API or known list).
2. For each location, call GET `.../fabricLocations/{location}/fileShares`.
3. Aggregate results into a single inventory grouped by location.
4. Flag any locations returning 404 (misconfigured or decommissioned).
5. Present a consolidated report with share counts per location.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
