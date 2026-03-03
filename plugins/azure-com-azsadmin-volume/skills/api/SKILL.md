---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# FabricAdminClient
API version: 2019-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/volumes -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/volumes/{volume} | Return the requested a storage volume. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/volumes | Returns a list of all storage volumes at a location. |

## Enhanced Skill Content
## Question Mapping

- "What volumes exist in this storage subsystem?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/volumes
- "Get details for a specific volume" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/volumes/{volume}
- "Is a particular volume still available or has it been removed?" -> GET /...volumes/{volume} (check for 200 vs 404)
- "List all volumes under a scale unit's storage subsystem in a given region" -> GET /...volumes
- "How many volumes are attached to a storage subsystem?" -> GET /...volumes (count items in response)
- "Does volume X exist in my fabric location?" -> GET /...volumes/{volume} (200 means yes, 404 means no)
- "What API version should I use for volume queries?" -> Both endpoints require `api-version` param; use `2019-05-01`
- "Show me volumes for a different resource group" -> GET /...volumes (swap `resourceGroupName` path segment)
- "Compare volumes across two storage subsystems" -> GET /...volumes twice with different `storageSubSystem` values
- "Verify infrastructure after a scale-unit migration" -> GET /...volumes to confirm all expected volumes are present
- "Audit storage volumes across multiple fabric locations" -> GET /...volumes iterating over each `location`
- "Check if a volume was deleted during maintenance" -> GET /...volumes/{volume} and handle 404

## Response Tips

- **Single volume (GET .../volumes/{volume})**: Returns a resource object with `id`, `name`, `type`, `location`, and `properties` nested under the top level; key capacity and status fields live inside `properties`.
- **Volume list (GET .../volumes)**: Returns `{ "value": [...] }` array; if `nextLink` is present, follow it to paginate through remaining results.
- **404 errors**: Returned when the volume, storage subsystem, scale unit, or any parent resource in the path does not exist; check the error `code` and `message` in the response body to identify which segment is invalid.
- **Auth errors (401/403)**: Confirm the OAuth2 bearer token is valid and the identity has Reader or higher role on the target subscription/resource group.

## Anomaly Flags

- **404 on a previously known volume**: May indicate unexpected deletion or infrastructure drift; surface immediately.
- **Empty volume list**: A storage subsystem returning zero volumes is unusual and may signal a misconfiguration or completed decommission.
- **Throttling (429 responses)**: Azure Resource Manager enforces per-subscription rate limits; if received, back off and surface the `Retry-After` header value.
- **API version mismatch warnings**: If the response includes deprecation headers or unknown properties, flag that `2019-05-01` may be outdated for the target region.
- **Inconsistent resource hierarchy**: If a parent resource (scale unit, storage subsystem) returns 404 while siblings exist, flag potential partial deployment or teardown in progress.

## Playbook

### 1. Inventory All Volumes in a Storage Subsystem

1. Authenticate and obtain an OAuth2 bearer token with read access to the target subscription.
2. Call `GET /subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Fabric.Admin/fabricLocations/{loc}/scaleUnits/{su}/storageSubSystems/{ss}/volumes?api-version=2019-05-01`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it repeatedly until no more pages remain.
5. Compile the full list of volume names and their properties.

### 2. Verify a Specific Volume Exists

1. Construct the full resource path including the volume name.
2. Call `GET /...volumes/{volume}?api-version=2019-05-01`.
3. If 200: volume exists; inspect `properties` for health and capacity.
4. If 404: volume is missing; check the error body to confirm it is the volume (not a parent resource) that is absent.

### 3. Audit Volumes Across Multiple Fabric Locations

1. Obtain the list of fabric locations for the subscription (from a separate Fabric Admin endpoint or known config).
2. For each location, identify the scale units and storage subsystems.
3. Call the volume list endpoint for each storage subsystem.
4. Aggregate results and compare against the expected inventory.
5. Flag any locations with missing or unexpected volumes.

### 4. Post-Maintenance Volume Validation

1. Before maintenance, snapshot the volume list by calling `GET /...volumes` and storing the `value` array.
2. After maintenance completes, call the same endpoint again.
3. Diff the two lists: identify any volumes that disappeared (present before, 404 now) or appeared unexpectedly.
4. For each missing volume, call `GET /...volumes/{volume}` individually to confirm deletion vs transient error.
5. Report discrepancies for review.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
