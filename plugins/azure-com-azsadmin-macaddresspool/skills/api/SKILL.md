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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool} | Returns the requested MAC address pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools | Returns a list of all MAC address pools at a location. |

## Enhanced Skill Content
## Question Mapping

- "What MAC address pools exist in this fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools
- "Get details for a specific MAC address pool" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}
- "Is the MAC address pool named X available?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}
- "How many MAC address pools are configured at this location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools
- "Does a MAC address pool exist in resource group Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}
- "List all fabric MAC pools for my subscription" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools
- "Show the properties of MAC pool Z" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}
- "Check if a MAC pool was provisioned successfully" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}
- "What MAC ranges are allocated at location L?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools
- "Verify a MAC address pool still exists after deletion" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}
- "Enumerate MAC pools across a specific fabric location for inventory" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools
- "What is the provisioning state of MAC pool X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/macAddressPools/{macAddressPool}

## Response Tips

- **Single resource (GET .../{macAddressPool}):** Response is an ARM resource object with `id`, `name`, `type`, `location`, and `properties` containing pool-specific fields (start/end MAC ranges, provisioning state). A 404 means the pool name is wrong or the pool was deleted.
- **List (GET .../macAddressPools):** Response wraps results in `{ "value": [...] }`. Check for a `nextLink` field for pagination -- if present, follow it with another GET to retrieve additional pages. An empty `value` array means no pools exist at that location, not an error.
- **All responses:** Expect standard ARM error format on failure: `{ "error": { "code": "...", "message": "..." } }`. The `code` field is machine-readable; `message` is human-friendly.

## Anomaly Flags

- **404 on a previously known pool:** Surface immediately -- the pool may have been deleted or the fabric location changed. Prompt user to verify resource group and location parameters.
- **Empty list response:** Flag when `value` is an empty array, as this may indicate the fabric location has no MAC pools configured or the location name is incorrect.
- **Provisioning state not "Succeeded":** If a pool's `properties.provisioningState` is `Failed`, `Deleting`, or `Updating`, alert the user proactively -- the resource may be in a transitional or broken state.
- **Throttling (429 or Retry-After header):** ARM APIs enforce rate limits per subscription. Surface any 429 responses or `Retry-After` headers and recommend waiting before retrying.
- **API version mismatch:** This spec uses `2016-05-01`. If responses contain `x-ms-deprecation` headers or unknown fields, flag that a newer API version may be available.
- **Subscription/RBAC errors (403):** Surface authorization failures clearly -- the OAuth token may lack `Microsoft.Fabric.Admin/fabricLocations/macAddressPools/read` permission.

## Playbook

### 1. Inventory All MAC Address Pools at a Fabric Location

1. Call GET `.../fabricLocations/{location}/macAddressPools` with your subscription, resource group, and location.
2. Parse the `value` array from the response.
3. If `nextLink` is present, follow it with another GET to retrieve the next page.
4. Repeat until no `nextLink` is returned.
5. Compile the full list of pool names and their provisioning states.

### 2. Verify a Specific MAC Address Pool Exists and Is Healthy

1. Call GET `.../macAddressPools/{macAddressPool}` with the pool name.
2. If 200, inspect `properties.provisioningState` -- confirm it reads `Succeeded`.
3. If 404, the pool does not exist at that location. Verify the pool name, resource group, and location are correct.
4. Optionally extract `properties.startMacAddress` and `properties.endMacAddress` to confirm the expected range.

### 3. Compare MAC Pools Across Multiple Fabric Locations

1. Identify the list of fabric locations to check (from your infrastructure documentation or another Azure API).
2. For each location, call GET `.../fabricLocations/{location}/macAddressPools`.
3. Collect and flatten all `value` arrays, tagging each pool with its source location.
4. Compare pool names and MAC ranges to detect overlaps or gaps across locations.
5. Flag any pools with non-`Succeeded` provisioning states.

### 4. Diagnose a Missing MAC Address Pool

1. Call GET `.../macAddressPools/{macAddressPool}` for the expected pool name.
2. If 404, call GET `.../macAddressPools` to list all pools at that location.
3. Check if the pool appears under a different name (typo, naming convention change).
4. If the list is empty, verify the fabric location name is correct by checking your ARM resource hierarchy.
5. Review Azure Activity Log for recent delete operations on the pool resource.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
