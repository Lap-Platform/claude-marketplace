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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools/{edgeGatewayPool} | Returns the requested edge gateway pool object. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools | Returns a list of all edge gateway pool objects at a location. |

## Enhanced Skill Content


## Question Mapping

- "How do I get details about a specific edge gateway pool?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools/{edgeGatewayPool}
- "How do I list all edge gateway pools in a fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools
- "What edge gateway pools exist in my Azure Stack region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools
- "Can I check if a specific edge gateway pool exists?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools/{edgeGatewayPool} (check for 200 vs 404)
- "What are the properties of edge gateway pool X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools/{edgeGatewayPool}
- "How do I enumerate infrastructure pools for a given location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools
- "Which edge gateways are associated with a pool?" -> GET /.../{edgeGatewayPool} then inspect the response for gateway references
- "How do I verify my subscription has fabric admin access?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools (a 404 or auth error indicates missing access)
- "What location identifiers are valid for fabric admin?" -> List edge gateway pools across known locations; valid locations return 200
- "How do I monitor edge gateway pool health?" -> GET /.../{edgeGatewayPool} periodically and compare response properties over time
- "Can I filter edge gateway pools by name?" -> GET /...edgeGatewayPools (list all), then filter client-side -- no server-side filter parameter available
- "What happens if I request a non-existent edge gateway pool?" -> GET /.../{edgeGatewayPool} returns 404

## Response Tips

- **Single resource (GET .../{edgeGatewayPool})**: Response is an ARM resource object with `id`, `name`, `type`, `location`, and `properties` nested object containing pool-specific details.
- **List endpoint (GET .../edgeGatewayPools)**: Returns `{ "value": [...] }` array. Check for `nextLink` field for pagination -- if present, follow it with another GET to retrieve additional pages.
- **Errors**: 404 means the resource, resource group, or location does not exist. Check path parameters carefully. Auth failures (401/403) indicate OAuth2 token issues or missing RBAC role assignments.

## Anomaly Flags

- **404 on list endpoint**: The fabric location or resource group may not exist or the Fabric Admin resource provider is not registered on the subscription -- surface this to the user rather than silently returning empty results.
- **Empty `value` array**: No edge gateway pools configured in the location. Flag if this is unexpected for a production environment.
- **Missing `nextLink` on large results**: If the list returns many items without pagination, note this as potentially truncated.
- **Unexpected properties in response**: ARM API versions evolve. Flag any unknown fields or deprecated properties (e.g., fields not matching the 2016-05-01 schema).
- **Slow responses or timeouts**: Azure management plane has throttling (read: 15,000 requests per hour per subscription). Surface if response headers show `x-ms-ratelimit-remaining-subscription-reads` dropping below 1,000.
- **API version mismatch warnings**: If Azure returns `x-ms-api-version` header differing from the requested `2016-05-01`, flag it as the endpoint may behave differently.

## Playbook

### 1. Inventory All Edge Gateway Pools in a Location

1. Authenticate and obtain an OAuth2 bearer token with Azure management scope.
2. GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools`
3. Parse the `value` array from the response.
4. If `nextLink` is present, GET that URL and append results.
5. Repeat until no `nextLink` remains.

### 2. Inspect a Specific Edge Gateway Pool

1. Obtain the pool name from the inventory list (Playbook 1) or from known configuration.
2. GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGatewayPools/{edgeGatewayPool}`
3. If 404, verify the pool name, location, and resource group are correct.
4. Inspect `properties` for pool configuration, associated gateways, and status.

### 3. Validate Fabric Admin Setup for a Subscription

1. Confirm the `Microsoft.Fabric.Admin` resource provider is registered: call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Fabric.Admin` (outside this API scope but necessary).
2. List edge gateway pools (Playbook 1) -- a successful 200 confirms the fabric location and resource group are correctly configured.
3. If 404, check that the resource group exists and that the fabric location identifier matches your Azure Stack stamp.

### 4. Monitor Edge Gateway Pool Changes Over Time

1. Run Playbook 1 to get the baseline list of pools.
2. For each pool, run Playbook 2 and store the `properties` snapshot.
3. Schedule periodic re-checks (e.g., every 15 minutes).
4. Diff the `properties` between runs and alert on changes to status, capacity, or gateway membership.
5. Watch `x-ms-ratelimit-remaining-subscription-reads` header to stay within throttling limits.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
