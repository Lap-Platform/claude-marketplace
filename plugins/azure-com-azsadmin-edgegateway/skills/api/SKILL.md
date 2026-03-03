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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGateways -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGateways/{edgeGateway} | Returns the requested edge gateway. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGateways | Returns the list of all edge gateways at a certain location. |

## Enhanced Skill Content


## Question Mapping

- "How do I get details about a specific edge gateway?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGateways/{edgeGateway}
- "List all edge gateways in a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGateways
- "Does a particular edge gateway exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/edgeGateways/{edgeGateway} (check for 404)
- "What edge gateways are deployed in my resource group?" -> GET .../edgeGateways
- "How do I verify an edge gateway is reachable at a given location?" -> GET .../edgeGateways/{edgeGateway} and inspect status fields
- "Can I enumerate edge gateways across different fabric locations?" -> GET .../edgeGateways (repeat per location)
- "What properties does an edge gateway expose?" -> GET .../edgeGateways/{edgeGateway} and examine the response body
- "How do I check the health of an edge gateway?" -> GET .../edgeGateways/{edgeGateway} and look for state/status properties
- "Is there a way to filter edge gateways by location?" -> GET .../edgeGateways with the target location in the path
- "What happens if I request a non-existent edge gateway?" -> GET .../edgeGateways/{edgeGateway} returns 404
- "How do I find the edge gateway name to use in other API calls?" -> GET .../edgeGateways to list all, extract names from results

## Response Tips

- **Single resource (GET .../{edgeGateway}):** Returns an ARM resource object with `id`, `name`, `type`, `location`, and `properties` nested object containing gateway-specific fields. A 404 means the gateway does not exist at that location.
- **List resources (GET .../edgeGateways):** Returns `{ "value": [...] }` array. May include `nextLink` for pagination -- follow it with subsequent GET requests until `nextLink` is absent.
- **Errors:** 404 is the documented error; also expect standard ARM error envelopes (`{ "error": { "code", "message" } }`) for auth failures (401/403) and throttling (429).

## Anomaly Flags

- **404 on a previously known gateway:** The resource may have been deleted or moved -- surface this as a potential infrastructure change.
- **429 Too Many Requests:** Azure ARM throttling is active. Back off using the `Retry-After` header value. Proactively warn when multiple 429s occur in sequence.
- **Pagination truncation:** If the list response contains `nextLink` but the agent stops early, flag that results are incomplete.
- **Missing `properties` block:** If a gateway resource returns without a `properties` object, flag it as an unexpected schema deviation.
- **OAuth token expiry:** If calls start returning 401 after a period of success, surface that the bearer token likely needs refresh.

## Playbook

### 1. Inventory all edge gateways in a location

1. Set `subscriptionId`, `resourceGroupName`, and `location` variables.
2. Call GET .../fabricLocations/{location}/edgeGateways.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it with GET until no more pages.
5. Compile the full list of gateway names and statuses.

### 2. Check if a specific edge gateway exists

1. Set the `edgeGateway` name you want to verify.
2. Call GET .../edgeGateways/{edgeGateway}.
3. If 200: gateway exists -- inspect `properties` for current state.
4. If 404: gateway does not exist at this location. Optionally repeat for other locations.

### 3. Monitor edge gateway health across locations

1. Define the list of fabric locations to scan.
2. For each location, call GET .../edgeGateways to list all gateways.
3. For each gateway, call GET .../edgeGateways/{edgeGateway} to get full details.
4. Extract health/status fields from `properties`.
5. Flag any gateway with a degraded or offline state.

### 4. Resolve a missing edge gateway

1. Call GET .../edgeGateways/{edgeGateway} with the expected name.
2. If 404, call GET .../edgeGateways to list all gateways at that location.
3. Check if the gateway was renamed by comparing properties of listed gateways.
4. If not found in the current location, repeat the list call across other known fabric locations.
5. Report findings: deleted, renamed, or relocated.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
