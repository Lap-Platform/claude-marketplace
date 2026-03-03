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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}/logicalSubnets -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}/logicalSubnets/{logicalSubnet} | Returns the requested logical subnet. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}/logicalSubnets | Returns a list of all logical subnets. |

## Enhanced Skill Content
## Question Mapping

- "What logical subnets exist in this logical network?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}/logicalSubnets
- "Get details for a specific logical subnet" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}/logicalSubnets/{logicalSubnet}
- "Does logical subnet X exist in network Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/logicalNetworks/{logicalNetwork}/logicalSubnets/{logicalSubnet}
- "List all subnets for a fabric location's logical network" -> GET /...logicalNetworks/{logicalNetwork}/logicalSubnets
- "What IP address ranges are assigned to a logical subnet?" -> GET /...logicalSubnets/{logicalSubnet}
- "How many logical subnets are configured under a logical network?" -> GET /...logicalNetworks/{logicalNetwork}/logicalSubnets
- "Verify a logical subnet is properly provisioned" -> GET /...logicalSubnets/{logicalSubnet}
- "What metadata is associated with a logical subnet?" -> GET /...logicalSubnets/{logicalSubnet}
- "Enumerate networking topology for a fabric location" -> GET /...logicalNetworks/{logicalNetwork}/logicalSubnets (iterate per network)
- "Check if a logical network has any subnets configured" -> GET /...logicalNetworks/{logicalNetwork}/logicalSubnets
- "What is the provisioning state of a specific subnet?" -> GET /...logicalSubnets/{logicalSubnet}
- "Compare subnets across two logical networks" -> GET /...logicalSubnets (call twice with different logicalNetwork values)

## Response Tips

- **Subnet list** (`/logicalSubnets`): Returns a `value` array of subnet resources; check for `nextLink` property for pagination across large networks.
- **Subnet detail** (`/logicalSubnets/{logicalSubnet}`): Returns a single ARM resource object with `id`, `name`, `type`, `location`, and `properties`; key config lives inside `properties`.
- **Errors**: 404 means the logical network or subnet name does not exist in the specified fabric location -- verify the full resource path including subscriptionId, resourceGroup, and location.

## Anomaly Flags

- **404 on list endpoint**: The parent logical network likely does not exist; surface this rather than reporting "empty results."
- **Empty `value` array**: A valid logical network with zero subnets may indicate incomplete fabric provisioning -- flag for operator review.
- **Missing or null `properties` fields**: Subnet resources with incomplete properties may be mid-provisioning or in a failed state; check `provisioningState`.
- **ARM throttling (429)**: Azure Resource Manager enforces per-subscription read limits (12000/hour); surface `Retry-After` header value when approaching limits.
- **API version mismatch**: This spec targets `2016-05-01`; if the server returns an `error.code` of `NoRegisteredProviderFound` or `InvalidApiVersionParameter`, the Fabric Admin RP may require a newer version.

## Playbook

### 1. Audit All Logical Subnets in a Fabric Location

1. Identify the target subscription, resource group, and fabric location.
2. Obtain the list of logical networks (via the LogicalNetworks API, outside this spec).
3. For each logical network, call `GET /...logicalNetworks/{logicalNetwork}/logicalSubnets`.
4. Collect all subnet entries from the `value` arrays.
5. Follow any `nextLink` URLs until pagination is exhausted.
6. Compile a summary table of subnet names, IP ranges, and provisioning states.

### 2. Verify a Specific Subnet Exists and Is Healthy

1. Call `GET /...logicalSubnets/{logicalSubnet}` with the target subnet name.
2. If 404, report the subnet does not exist under the specified logical network.
3. If 200, inspect `properties.provisioningState` -- expect `Succeeded`.
4. Flag any state other than `Succeeded` (e.g., `Failed`, `Creating`) as requiring attention.

### 3. Compare Subnet Configurations Across Logical Networks

1. Call `GET /...logicalNetworks/{networkA}/logicalSubnets` for the first network.
2. Call `GET /...logicalNetworks/{networkB}/logicalSubnets` for the second network.
3. Normalize both result sets by subnet name.
4. Diff the `properties` objects to identify discrepancies in IP ranges, VLAN IDs, or metadata.
5. Report subnets present in one network but missing from the other.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
