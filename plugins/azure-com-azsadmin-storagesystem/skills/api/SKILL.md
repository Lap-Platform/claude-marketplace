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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem} | Return the requested storage subsystem. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems | Returns a list of all storage subsystems for a location. |

## Enhanced Skill Content
## Question Mapping

- "What storage subsystems exist at this fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems
- "Get details for a specific storage subsystem" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}
- "Is storage subsystem X present in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}
- "List all storage infrastructure in resource group Y" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems
- "Check if a storage subsystem was removed or doesn't exist" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}
- "How many storage subsystems are at location Z?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems
- "What are the properties of storage subsystem X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}
- "Verify a storage subsystem exists before updating infrastructure" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}
- "Enumerate storage backends for capacity planning" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems
- "Which storage subsystem handles location eastus?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems
- "Audit all storage subsystems across a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems
- "Get the resource ID for a named storage subsystem" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}

## Response Tips

- **Single resource (GET by ID):** Returns an ARM resource object with `id`, `name`, `type`, `location`, and `properties` -- the subsystem details live nested under `properties`.
- **List endpoint:** Returns `{ "value": [...] }` array of resource objects; check for `nextLink` field to handle pagination across large result sets.
- **404 errors:** Returned when the subscription, resource group, fabric location, or storage subsystem name does not exist -- inspect the `error.code` and `error.message` fields in the response body to identify which path segment is invalid.
- **Auth failures:** A 401 or 403 with `AuthenticationFailed` or `AuthorizationFailed` code means the OAuth2 bearer token is missing, expired, or lacks the required RBAC role on the target scope.

## Anomaly Flags

- **404 on a previously known subsystem:** May indicate infrastructure was decommissioned or renamed -- surface this to the user immediately.
- **Empty list response:** If `value` is an empty array, flag that the fabric location may not have storage configured or the location name may be incorrect.
- **Throttling (429):** Azure ARM enforces per-subscription read rate limits (typically 12000/hour) -- if response includes `Retry-After` header, surface the wait time and remaining quota.
- **Unexpected `provisioningState`:** If a subsystem's properties show a state other than `Succeeded` (e.g., `Failed`, `Updating`), proactively alert the user that the resource may be unstable.
- **Missing `nextLink` truncation:** If the list returns exactly the ARM default page size (typically 100 items) with no `nextLink`, warn that results may be silently truncated.
- **Deprecated API version:** The `2016-05-01` API version is old -- if Azure returns a `Warning` header or `x-ms-deprecation` indicator, flag that the user should migrate to a newer API version.

## Playbook

### 1. Inventory all storage subsystems at a fabric location

1. Authenticate and obtain an OAuth2 bearer token with `Reader` role (minimum) on the target subscription.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it with another GET to retrieve the next page; repeat until no `nextLink` remains.
5. Compile the full list of subsystem names and their provisioning states.

### 2. Verify a specific storage subsystem exists

1. Obtain the exact `storageSubSystem` name (case-sensitive).
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageSubSystems/{storageSubSystem}`.
3. If 200: the subsystem exists -- inspect `properties` for current state.
4. If 404: the subsystem does not exist at that location -- verify the location and name are correct before concluding it was removed.

### 3. Capacity planning audit across locations

1. Identify all fabric locations in the resource group (use the fabric locations list endpoint if available).
2. For each location, call the list storage subsystems endpoint.
3. Collect `properties` details (capacity, usage, health) from each subsystem.
4. Aggregate results into a summary table grouped by location.
5. Flag any subsystems with non-`Succeeded` provisioning state or abnormal capacity utilization.

### 4. Troubleshoot a missing storage subsystem

1. Call the list endpoint to see all subsystems at the expected fabric location.
2. If the target subsystem is absent from the list, try the GET-by-ID endpoint to confirm a 404.
3. Check that the `location`, `resourceGroupName`, and `subscriptionId` path parameters are correct.
4. Verify RBAC permissions -- a 403 can masquerade as "not found" if the caller lacks read access to the specific resource.
5. Review Azure activity logs for recent delete operations on the subsystem resource ID.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
