---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# FabricAdminClient
API version: 2018-10-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem} | Return the requested storage subsystem. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems | Returns a list of all storage subsystems for a location. |

## Enhanced Skill Content
## Question Mapping

- "What storage subsystems exist in my scale unit?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems
- "Get details for a specific storage subsystem" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}
- "List all storage subsystems at a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems
- "Is a specific storage subsystem still available?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}
- "How many storage subsystems are attached to this scale unit?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems
- "Check the health of a storage subsystem" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}
- "Does storage subsystem X exist in my fabric?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}
- "Enumerate infrastructure storage for capacity planning" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems
- "Verify a storage subsystem after provisioning" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}
- "What api-version should I use for storage subsystem queries?" -> Both endpoints require `api-version=2018-10-01`
- "Get storage subsystem properties like total and used capacity" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems/{storageSubSystem}
- "Audit all storage backing a specific scale unit" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/storageSubSystems

## Response Tips

- **List endpoint**: Returns an ARM `value` array; check for `nextLink` to paginate through large deployments. Each item contains `id`, `name`, `type`, `location`, and `properties`.
- **Get endpoint**: Returns a single ARM resource object; a 404 means the subsystem name is wrong or it has been removed from the scale unit.
- **Common shape**: All responses follow Azure Resource Manager conventions -- metadata at the top level, domain data nested under `properties`.
- **Errors**: 404 is the only documented error; unexpected 400/403/500 responses indicate bad path parameters, missing RBAC roles, or service issues respectively.

## Anomaly Flags

- **404 on a previously known subsystem**: The storage subsystem may have been decommissioned or migrated -- surface this immediately as a potential infrastructure change.
- **Empty list response**: A scale unit returning zero storage subsystems is abnormal and may indicate a misconfigured fabric location or incorrect path parameters.
- **Throttling headers**: Watch for `Retry-After` or HTTP 429 responses; Azure ARM applies per-subscription rate limits that can block subsequent calls.
- **api-version mismatch**: If the caller omits or uses a different `api-version` than `2018-10-01`, expect 400 errors or unexpected response schemas.
- **Stale capacity data**: If storage subsystem properties show utilization above 90%, flag proactively for capacity planning action.
- **Deprecated API version**: Microsoft may sunset `2018-10-01` -- surface any response headers indicating deprecation or newer available versions.

## Playbook

### 1. Inventory All Storage Subsystems for a Scale Unit

1. Identify your `subscriptionId`, `resourceGroupName`, `location`, and `scaleUnit` values.
2. Call `GET .../storageSubSystems?api-version=2018-10-01` to list all subsystems.
3. If the response contains a `nextLink`, follow it to retrieve additional pages.
4. Collect `name` and key `properties` (capacity, health) from each item.
5. Summarize total count and aggregate capacity.

### 2. Verify a Specific Storage Subsystem Exists

1. Obtain the `storageSubSystem` name you want to verify.
2. Call `GET .../storageSubSystems/{storageSubSystem}?api-version=2018-10-01`.
3. If 200, the subsystem exists -- inspect `properties` for status and health.
4. If 404, the subsystem does not exist at that path -- double-check the scale unit and location.

### 3. Cross-Location Storage Audit

1. List all fabric locations for the subscription (via the parent FabricLocations API).
2. For each location, list scale units (via the parent ScaleUnits API).
3. For each scale unit, call `GET .../storageSubSystems` to enumerate storage.
4. Aggregate results into a report grouped by location and scale unit.
5. Flag any scale units with zero subsystems or subsystems showing degraded health.

### 4. Capacity Planning Check

1. List all storage subsystems for the target scale unit.
2. For each subsystem, call the GET detail endpoint to retrieve full `properties`.
3. Extract capacity metrics (total, used, available) from the properties payload.
4. Calculate utilization percentages and flag any subsystem above 80%.
5. Recommend scaling actions for subsystems approaching capacity limits.

### 5. Post-Provisioning Validation

1. After provisioning a new storage subsystem, wait for the operation to complete.
2. Call `GET .../storageSubSystems/{newSubSystem}?api-version=2018-10-01`.
3. Confirm a 200 response and that `properties` reflect expected configuration.
4. Call the list endpoint to verify the new subsystem appears alongside existing ones.
5. If the subsystem returns 404 or unexpected properties, investigate provisioning logs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
