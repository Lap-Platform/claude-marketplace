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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork} | Returns the requested logical network. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks | Returns a list of all logical networks at a location. |

## Enhanced Skill Content
## Question Mapping

- "What logical networks exist in this fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks
- "Get details for a specific logical network" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}
- "Is logical network X configured in location Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}
- "List all logical networks in my resource group's fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks
- "Does a logical network named 'production-vlan' exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}
- "How many logical networks are in fabric location eastus?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks
- "Show me the configuration of a logical network" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}
- "What subnets are defined on logical network X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}
- "Verify a logical network exists before assigning it to a VM" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}
- "Compare logical networks across my fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks
- "Which logical networks have metadata indicating they are enabled?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks
- "Audit all networking resources in my fabric admin deployment" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks

## Response Tips

- **Logical network detail (GET .../logicalNetworks/{name})**: Response is a single ARM resource object with `id`, `name`, `type`, `location`, and `properties`. Check `properties` for subnet definitions, network configuration, and metadata. A 404 means the network name is wrong or the fabric location is incorrect.
- **Logical network list (GET .../logicalNetworks)**: Response wraps results in a `value` array. If `nextLink` is present, follow it for additional pages. An empty `value` array means no logical networks exist in that fabric location -- not an error. A 404 here means the fabric location itself does not exist.
- **All endpoints**: Responses follow the Azure ARM envelope. Always check for `error` object in non-200 responses -- it contains `code` and `message` fields with actionable details.

## Anomaly Flags

- **404 on list endpoint**: The fabric location or resource group does not exist -- surface this distinction rather than just saying "not found"
- **Empty `value` array on list**: No logical networks configured -- may indicate the fabric location has not been provisioned for networking
- **API version 2016-05-01**: This is a legacy API version; surface a note that newer API versions may be available and that some fields could be deprecated
- **OAuth2 token expiry**: If repeated 401 responses occur, proactively suggest token refresh rather than retrying
- **Missing `properties` on a returned resource**: Indicates a partially provisioned or corrupted logical network -- flag for admin attention
- **Throttling (429 or Retry-After header)**: Azure ARM has per-subscription rate limits; surface the retry interval and suggest batching if listing across many locations

## Playbook

### 1. Discover All Logical Networks in a Fabric Location

1. Authenticate and obtain an OAuth2 bearer token for the Azure management scope
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks`
3. Parse the `value` array from the response
4. If `nextLink` is present, follow it to retrieve additional pages
5. Compile the full list of logical network names and their configurations

### 2. Verify a Logical Network Exists Before Use

1. Identify the logical network name you intend to reference
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}`
3. If 200, the network exists -- inspect `properties` for subnets and settings
4. If 404, the network does not exist in that location -- check for typos in the name or confirm the correct fabric location

### 3. Audit Logical Network Configuration

1. List all logical networks using the list endpoint
2. For each network in the `value` array, call the detail endpoint to get full `properties`
3. Extract subnet definitions, VLAN IDs, and metadata from each response
4. Flag any networks with missing or empty `properties` as potentially misconfigured
5. Produce a summary comparing configurations across all networks

### 4. Troubleshoot a Missing Logical Network

1. Call the list endpoint to see all networks in the target fabric location
2. If the list returns 404, the fabric location or resource group is invalid -- verify both names
3. If the list returns 200 but the expected network is absent, confirm the network was created in the correct location
4. Try the detail endpoint with the exact network name to rule out case sensitivity issues
5. Check Azure Activity Log for recent delete operations on the logical network resource


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
