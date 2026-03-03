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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance} | Returns the requested software load balancer multiplexer instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances | Returns a list of all software load balancer instances at a location. |

## Enhanced Skill Content
## Question Mapping

- "What SLB mux instances exist in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances
- "Get details for a specific SLB mux instance" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}
- "Is a particular SLB mux instance running?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}
- "List all software load balancer multiplexers in a region" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances
- "Does SLB mux instance X exist in my fabric?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}
- "How many SLB mux instances are deployed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances
- "What is the configuration of mux instance Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}
- "Check the health of all SLB mux instances" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances
- "Verify a mux instance exists before referencing it in automation" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}
- "Enumerate infrastructure components in my Azure Stack fabric" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances
- "What fabric location is mux instance Z associated with?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}
- "Audit all SLB mux instances across a resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances

## Response Tips

- **Single instance (GET .../{slbMuxInstance})**: Response is a single ARM resource object with `id`, `name`, `type`, `location`, and `properties` containing instance-specific config and state. A 404 means the instance name is wrong or it does not exist at that fabric location.
- **List instances (GET .../slbMuxInstances)**: Response wraps results in a `value` array. Check for a `nextLink` field for pagination -- if present, follow it to retrieve additional pages. An empty `value` array means no mux instances are deployed at that location.
- **Errors**: Both endpoints return 404 when the resource group, fabric location, or instance is not found. The error body follows ARM format: `{"error": {"code": "...", "message": "..."}}`. Always check `error.code` for machine-readable classification.

## Anomaly Flags

- **404 on list endpoint**: Indicates the fabric location path itself is invalid or the resource provider is not registered -- surface this as a configuration issue, not just "no results."
- **Empty `value` array**: No SLB mux instances at the location. Flag if this is unexpected for a production Azure Stack deployment, as it may indicate a provisioning gap.
- **API version drift**: This spec uses `2016-05-01`. If calls fail with version-related errors, flag that a newer api-version may be required and suggest checking Azure docs.
- **Missing `properties` fields**: If a returned instance lacks expected properties (e.g., state, configuration), flag potential schema changes or partial provisioning.
- **Throttling (429)**: Although not explicitly listed, ARM APIs enforce rate limits. If encountered, surface the `Retry-After` header value and pause automation accordingly.
- **OAuth token expiry**: Auth is OAuth2. Surface 401 responses proactively with a reminder to refresh the bearer token.

## Playbook

### 1. Inventory All SLB Mux Instances at a Fabric Location

1. Authenticate and obtain an OAuth2 bearer token for Azure Resource Manager.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances` with `api-version=2016-05-01`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it repeatedly until no more pages remain.
5. Compile the full list of instance names and their properties for reporting.

### 2. Verify a Specific SLB Mux Instance Exists

1. Authenticate with OAuth2.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/slbMuxInstances/{slbMuxInstance}`.
3. If 200: instance exists -- extract `properties` for status details.
4. If 404: instance does not exist at that location. Verify the instance name and fabric location are correct.

### 3. Health Check Across All Mux Instances

1. List all instances using the list endpoint (see Playbook 1).
2. For each instance in the `value` array, inspect `properties` for health or state indicators.
3. Flag any instance where the state is not healthy or expected fields are missing.
4. Output a summary: total count, healthy count, and any flagged instances.

### 4. Cross-Location Audit

1. Determine all fabric locations in scope (from your Azure Stack topology or a separate fabric locations API call).
2. For each location, call the list endpoint to retrieve all SLB mux instances.
3. Aggregate results across locations into a single inventory.
4. Compare against expected deployment baselines and flag discrepancies (missing instances, unexpected extras).

### 5. Pre-Automation Validation

1. Before referencing an SLB mux instance in a deployment script or template, call the single-instance GET endpoint to confirm it exists.
2. Validate that the returned `properties` match expected configuration (e.g., correct virtual server references).
3. If 404 or mismatched config, abort automation and surface the issue rather than proceeding with stale references.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
