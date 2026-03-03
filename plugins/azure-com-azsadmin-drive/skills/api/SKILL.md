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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/drives -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/drives/{drive} | Return the requested a storage drive. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/drives | Returns a list of all storage drives at a location. |

## Enhanced Skill Content
## Question Mapping

- "What drives are in this storage subsystem?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/drives
- "Get details for a specific drive" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}/drives/{drive}
- "List all drives in scale unit storage?" -> GET .../storageSubSystems/{storageSubSystem}/drives
- "Is a particular drive healthy?" -> GET .../drives/{drive} (check status/health fields in response)
- "How many drives does a storage subsystem have?" -> GET .../drives (count items in response)
- "Does this drive exist?" -> GET .../drives/{drive} (200 = yes, 404 = no)
- "What is the capacity of a specific drive?" -> GET .../drives/{drive}
- "Show me all drives for a given fabric location and scale unit" -> GET .../drives
- "What drive types are deployed in my storage subsystem?" -> GET .../drives (inspect type field per item)
- "Check if a drive is still operational" -> GET .../drives/{drive} (inspect operational status properties)
- "Enumerate storage hardware in a subsystem" -> GET .../drives
- "Verify a drive exists before performing maintenance" -> GET .../drives/{drive} (404 means not found)

## Response Tips

- **Drive detail (single):** Response is a single resource object with `id`, `name`, `type`, `location`, and `properties` nested object containing drive-specific metadata (capacity, health, model, serial number). Always check `properties` for operational state.
- **Drive list:** Response follows Azure ARM pattern with a `value` array of drive objects. Check for `nextLink` field for pagination -- if present, follow it to retrieve additional pages. An empty `value` array means no drives exist in that subsystem.
- **Errors:** 404 indicates the resource path is invalid -- the drive, storage subsystem, scale unit, fabric location, resource group, or subscription does not exist. Inspect the error `code` and `message` fields to determine which segment is wrong.

## Anomaly Flags

- **404 on a previously known drive:** May indicate hardware removal, decommissioning, or a renamed resource -- surface this to the user immediately.
- **Degraded or unhealthy drive status:** If `properties` contains health/state fields showing non-operational values (e.g., "Lost", "Degraded", "UnResponsive"), flag proactively as potential hardware failure.
- **Empty drive list for an active subsystem:** A storage subsystem returning zero drives is unusual and may indicate a configuration issue or access problem.
- **Throttling (429 responses):** Azure ARM APIs enforce rate limits per subscription. If encountered, surface the `Retry-After` header value and pause requests accordingly.
- **Missing api-version parameter:** Both endpoints require `api-version`. Omitting it produces opaque errors -- always default to `2019-05-01` if the user does not specify.
- **Unexpected capacity values:** Drives reporting 0 capacity or negative values should be flagged as potential data integrity issues.

## Playbook

### 1. Inventory All Drives in a Storage Subsystem

1. Identify the subscription ID, resource group, fabric location, scale unit, and storage subsystem name.
2. Call `GET .../storageSubSystems/{storageSubSystem}/drives?api-version=2019-05-01`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it repeatedly until no more pages remain.
5. Compile the full list of drives with their names and statuses.

### 2. Check Health of a Specific Drive

1. Obtain the drive identifier (from inventory or known name).
2. Call `GET .../drives/{drive}?api-version=2019-05-01`.
3. If 404 is returned, the drive does not exist -- verify the resource path.
4. On 200, inspect `properties` for health and operational state fields.
5. Surface any non-healthy status to the user with recommended action.

### 3. Validate Drive Existence Before Maintenance

1. Call `GET .../drives/{drive}?api-version=2019-05-01` for the target drive.
2. If 200, confirm the drive exists and capture its current state for a pre-maintenance snapshot.
3. If 404, abort the maintenance workflow and notify the user the drive was not found.
4. Record the drive properties (serial number, model, capacity) for maintenance logs.

### 4. Compare Drive Fleet Across Storage Subsystems

1. For each storage subsystem in the scale unit, call `GET .../drives?api-version=2019-05-01`.
2. Aggregate drive counts, types, and health statuses per subsystem.
3. Identify subsystems with fewer drives than expected or with degraded drives.
4. Present a summary table comparing subsystem health side by side.

### 5. Diagnose a Missing Drive

1. Call `GET .../drives/{drive}?api-version=2019-05-01` for the suspected missing drive.
2. If 404, call `GET .../drives?api-version=2019-05-01` to list all drives in the subsystem.
3. Search the list for drives with similar names or serial numbers (possible rename).
4. If not found in any subsystem, escalate as a potential hardware removal or failure event.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
