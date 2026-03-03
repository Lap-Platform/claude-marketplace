---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/scaleOut -- create first scaleOut

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/scaleOut | Scales out a scale unit. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/createFromJson | Add a new scale unit. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit} | Returns the requested scale unit. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits | Returns a list of all scale units at a location. |

## Enhanced Skill Content


## Question Mapping

- "How do I scale out a fabric scale unit?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/scaleOut
- "How do I add a new node to my scale unit?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/scaleOut
- "How do I create a scale unit from a JSON definition?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/createFromJson
- "How do I provision a new scale unit with custom configuration?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/createFromJson
- "How do I get details about a specific scale unit?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}
- "What is the current status of my scale unit?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}
- "How do I list all scale units in a fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits
- "What scale units exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits
- "How do I check if a scale unit exists before scaling out?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit} then POST .../scaleOut
- "How do I expand capacity for a specific fabric location?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/scaleOut
- "Can I create a scale unit from an exported template?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}/createFromJson
- "How do I verify a scale-out operation completed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnits/{scaleUnit}

## Response Tips

- **Scale unit GET (single):** Returns the full scale unit resource object. A 404 means the scale unit name or fabric location is wrong -- check both path segments.
- **Scale unit GET (list):** Returns a `value` array of scale unit resources. No pagination indicated in spec -- expect all results in one response. Empty array means no scale units at that location.
- **Scale-out POST:** 200 means synchronous completion; 202 means the operation is async -- check the `Location` or `Azure-AsyncOperation` response header to poll for completion.
- **CreateFromJson POST:** Same 200/202 pattern as scale-out. The `creationData` map must contain the full JSON definition. Validation errors typically surface as 400 with detail in the response body.

## Anomaly Flags

- **202 without polling headers:** If a scale-out or createFromJson returns 202 but lacks `Location` or `Azure-AsyncOperation` headers, flag this -- the operation may be untrackable.
- **Repeated 404 on known scale units:** Could indicate a fabric location mismatch, subscription permission change, or resource deletion by another process.
- **Long-running async operations:** If polling an async operation exceeds 30 minutes without terminal status, surface a warning -- scale operations can hang.
- **OAuth token expiry during async workflows:** Scale operations are long-running; flag if the token will expire before the expected completion window.
- **Unexpected 200 on POST (instead of 202):** If scale-out returns 200 when the operation is known to take time, verify the response body -- it may indicate a no-op (already at target scale).

## Playbook

### 1. Scale Out an Existing Scale Unit

1. **List scale units** -- GET `.../scaleUnits` to confirm the target scale unit exists and note its current state.
2. **Get scale unit details** -- GET `.../scaleUnits/{scaleUnit}` to review current node count and configuration.
3. **Prepare node parameters** -- Build the `scaleUnitNodeParameters` map with the new node details.
4. **Trigger scale-out** -- POST `.../scaleUnits/{scaleUnit}/scaleOut` with the `scaleUnitNodeParameters` body.
5. **Poll for completion** -- If 202 returned, use the `Azure-AsyncOperation` header URL to poll until status is `Succeeded` or `Failed`.
6. **Verify** -- GET `.../scaleUnits/{scaleUnit}` again to confirm the new node count.

### 2. Create a Scale Unit from JSON Definition

1. **Prepare the JSON definition** -- Assemble the full scale unit configuration as a `creationData` map (node definitions, network config, storage).
2. **Check for conflicts** -- GET `.../scaleUnits/{scaleUnit}` to verify the target name does not already exist (expect 404).
3. **Create the scale unit** -- POST `.../scaleUnits/{scaleUnit}/createFromJson` with the `creationData` body.
4. **Track provisioning** -- Poll the async operation header if 202 is returned.
5. **Validate deployment** -- GET `.../scaleUnits/{scaleUnit}` to confirm the resource was created with the expected configuration.

### 3. Inventory All Scale Units in a Location

1. **List all scale units** -- GET `.../scaleUnits` for the target fabric location.
2. **Iterate and inspect** -- For each scale unit in the `value` array, GET `.../scaleUnits/{scaleUnit}` for full details.
3. **Record state** -- Note provisioning state, node count, and any anomalies for each unit.

### 4. Pre-flight Check Before Infrastructure Changes

1. **Authenticate** -- Obtain a valid OAuth2 token with sufficient scope for the target subscription and resource group.
2. **Validate location** -- GET `.../scaleUnits` to confirm the fabric location path is correct (404 means bad location).
3. **Inspect target unit** -- GET `.../scaleUnits/{scaleUnit}` to confirm it exists and is in a healthy/ready state.
4. **Proceed with operation** -- Only trigger scale-out or createFromJson after confirming the target is in the expected state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
