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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation} | Returns the requested fabric location. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations | Returns a list of all fabric locations. |

## Enhanced Skill Content
## Question Mapping

- "What fabric locations are available in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations
- "Get details for a specific fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}
- "Does fabric location X exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}
- "List all fabric infrastructure locations for resource group Y" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations
- "Check if a fabric location is valid before deploying" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}
- "How many fabric locations are configured?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations
- "What properties does fabric location Z have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}
- "Enumerate fabric locations across my subscription" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations
- "Verify a fabric location name resolves to a real resource" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}
- "What is the configuration of my fabric infrastructure?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations
- "Retrieve metadata for a fabric location by name" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}

## Response Tips

- **Single location (GET .../{fabricLocation})**: Returns a resource object with `id`, `name`, `type`, and `properties`. A 404 means the location name is invalid or does not exist in that resource group -- do not retry, prompt the user to verify the name.
- **Location list (GET .../fabricLocations)**: Returns a `value` array of location objects. If `nextLink` is present, follow it to retrieve additional pages. An empty `value` array is valid and means no fabric locations are configured.
- **All endpoints**: Require `api-version=2016-05-01` as a query parameter. OAuth2 bearer tokens must include the `https://management.azure.com/.default` scope.

## Anomaly Flags

- **404 on location lookup**: Surface immediately -- the fabric location name may be misspelled or the resource group may not have Fabric Admin provisioned.
- **Empty location list**: Flag when the list endpoint returns zero results, as this likely means Fabric Admin is not deployed in the target resource group.
- **Throttling (429 or Retry-After header)**: Azure Resource Manager enforces per-subscription rate limits. Surface the retry delay and suggest spacing requests.
- **API version mismatch**: If the response includes warnings or unexpected schema, flag that `2016-05-01` is a legacy API version and a newer version may be available.
- **Authorization errors (401/403)**: Surface with guidance to check OAuth2 token scope and RBAC role assignments on the resource group.

## Playbook

### 1. Discover All Fabric Locations

1. Identify your `subscriptionId` and `resourceGroupName`.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations` with `api-version=2016-05-01`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it to get the next page. Repeat until no `nextLink`.
5. Present the full list of location names and their properties.

### 2. Validate a Fabric Location Exists

1. Obtain the target `fabricLocation` name from the user.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{fabricLocation}`.
3. If 200: confirm the location exists and display its properties.
4. If 404: inform the user the location was not found and suggest listing all locations to find the correct name.

### 3. Audit Fabric Infrastructure Across Resource Groups

1. List all resource groups in the subscription (via Azure Resource Manager `GET /subscriptions/{subscriptionId}/resourceGroups`).
2. For each resource group, call the fabric locations list endpoint.
3. Aggregate results into a summary showing which resource groups have fabric locations and how many.
4. Flag any resource groups with zero fabric locations if the user expects infrastructure there.

### 4. Pre-Deployment Location Check

1. Before deploying fabric resources, call the list endpoint to get available locations.
2. Confirm the desired deployment location appears in the results.
3. If found, retrieve the specific location details to verify its properties meet requirements.
4. If not found, surface the issue and suggest the user provision the fabric location first or choose from the available options.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
