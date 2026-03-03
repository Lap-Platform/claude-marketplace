---
name: appserviceplans-api-client
description: "AppServicePlans API Client API skill. Use when working with AppServicePlans API Client for subscriptions. Covers 29 endpoints."
version: 1.0.0
generator: lapsh
---

# AppServicePlans API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/serverfarms -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionNamespaces/{namespaceName}/relays/{relayName}/listKeys -- create first listKeys

## Endpoints

29 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/serverfarms | Get all App Service plans for a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms | Get all App Service plans in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name} | Get an App Service plan. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name} | Creates or updates an App Service Plan. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name} | Delete an App Service plan. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name} | Creates or updates an App Service Plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/capabilities | List all capabilities of an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionNamespaces/{namespaceName}/relays/{relayName} | Retrieve a Hybrid Connection in use in an App Service plan. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionNamespaces/{namespaceName}/relays/{relayName} | Delete a Hybrid Connection in use in an App Service plan. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionNamespaces/{namespaceName}/relays/{relayName}/listKeys | Get the send key name and value of a Hybrid Connection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionNamespaces/{namespaceName}/relays/{relayName}/sites | Get all apps that use a Hybrid Connection in an App Service Plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionPlanLimits/limit | Get the maximum number of Hybrid Connections allowed in an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionRelays | Retrieve all Hybrid Connections in use in an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/metricdefinitions | Get metrics that can be queried for an App Service plan, and their definitions. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/metrics | Get metrics for an App Service plan. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/restartSites | Restart all apps in an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/sites | Get all apps associated with an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/skus | Gets all selectable SKUs for a given App Service Plan |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/usages | Gets server farm usage information |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections | Get all Virtual Networks associated with an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName} | Get a Virtual Network associated with an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/gateways/{gatewayName} | Get a Virtual Network gateway. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/gateways/{gatewayName} | Update a Virtual Network gateway. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes | Get all routes that are associated with a Virtual Network in an App Service plan. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes/{routeName} | Get a Virtual Network route in an App Service plan. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes/{routeName} | Create or update a Virtual Network route in an App Service plan. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes/{routeName} | Delete a Virtual Network route in an App Service plan. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes/{routeName} | Create or update a Virtual Network route in an App Service plan. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/workers/{workerName}/reboot | Reboot a worker machine in an App Service plan. |

## Enhanced Skill Content
## Question Mapping

- "What App Service Plans exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/serverfarms
- "List all App Service Plans in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms
- "Get details for a specific App Service Plan?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}
- "Create or replace an App Service Plan?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}
- "Delete an App Service Plan?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}
- "Update properties on an existing App Service Plan without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}
- "What apps are running on a given App Service Plan?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/sites
- "How do I restart all sites in an App Service Plan?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/restartSites
- "What metrics are available for an App Service Plan?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/metricdefinitions
- "Show current resource usage for an App Service Plan?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/usages
- "What SKU options can I scale this plan to?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/skus
- "List hybrid connections configured on an App Service Plan?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/hybridConnectionRelays
- "What VNet integrations does my App Service Plan have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections
- "How do I add a route to a VNet connection on my plan?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes/{routeName}
- "Reboot a specific worker instance in my plan?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/workers/{workerName}/reboot

## Response Tips

- **Plan listings** (GET .../serverfarms): Returns a `value` array with `nextLink` for pagination; pass `detailed=true` at subscription level for extended properties including site counts.
- **Single plan** (GET/PUT/PATCH .../serverfarms/{name}): Returns the full resource object; PUT returns 200 (updated), 201 (created), or 202 (provisioning async) -- check `provisioningState` in the body if 202.
- **Delete operations** (DELETE): 200 means deleted, 204 means already gone or no-op; both are success -- do not treat 204 as an error.
- **Sites listing** (GET .../sites): Supports server-side filtering via `$filter`, `$top` for page size, and `$skipToken` for cursor-based pagination -- always check for `nextLink` in the response.
- **Metrics and usages** (GET .../metrics, .../usages): Results are nested under `value` with individual metric objects containing `name`, `unit`, and `timeseries`; use `$filter` for OData time-range expressions.
- **Hybrid connections**: `listKeys` (POST) returns `sendKeyName`, `sendKeyValue`, `primaryConnectionString` -- these are secrets; handle accordingly.
- **VNet routes** (PUT/PATCH): 400 indicates malformed route configuration (e.g., invalid address prefix); 404 means the VNet or route does not exist.
- **Capabilities** (GET .../capabilities): Returns a flat array of `{name, value, description}` objects describing what the plan's SKU supports.

## Anomaly Flags

- **Async provisioning (202 on PUT/PATCH)**: Surface when a create or update returns 202 -- the plan is still provisioning. Prompt the user to poll the resource until `provisioningState` becomes `Succeeded` or `Failed`.
- **Plan not found (404)**: On GET for a specific plan, VNet, or route, flag clearly that the resource does not exist rather than retrying silently.
- **Hybrid connection limit reached**: After fetching `.../hybridConnectionPlanLimits/limit`, compare current count against max and warn if utilization exceeds 80%.
- **Usage approaching quota**: When `.../usages` returns values near their `limit`, proactively alert the user (e.g., CPU percentage, memory, site slots).
- **Invalid route config (400)**: On VNet route PUT/PATCH, surface the error body immediately -- it typically contains a `message` field explaining which property is invalid.
- **Stale API version**: This spec uses `api-version=2018-02-01`. Flag if the user is building new integrations, as newer API versions may be available with additional features.
- **Soft restart vs hard restart**: When calling `restartSites`, note whether `softRestart=true` was passed; a hard restart (default) causes brief downtime for all apps on the plan.
- **Secret exposure**: When `listKeys` is called for hybrid connections, flag that the response contains connection strings and keys that should not be logged or stored in plaintext.

## Playbook

### 1. Create and configure a new App Service Plan

1. List existing plans in the resource group: GET `.../resourceGroups/{rg}/providers/Microsoft.Web/serverfarms`
2. Check available SKUs for reference (optional): GET `.../serverfarms/{existingPlan}/skus`
3. Create the plan: PUT `.../resourceGroups/{rg}/providers/Microsoft.Web/serverfarms/{name}` with `appServicePlan` body specifying `location`, `sku`, and `properties`
4. If response is 202, poll GET `.../serverfarms/{name}` until `provisioningState` is `Succeeded`
5. Verify capabilities: GET `.../serverfarms/{name}/capabilities`

### 2. Monitor plan health and resource usage

1. Fetch metric definitions: GET `.../serverfarms/{name}/metricdefinitions`
2. Query specific metrics with a time filter: GET `.../serverfarms/{name}/metrics?$filter=name.value eq 'CpuPercentage' and startTime ge '...' and endTime le '...'`
3. Check resource usage and quotas: GET `.../serverfarms/{name}/usages`
4. List all sites on the plan: GET `.../serverfarms/{name}/sites`
5. If CPU or memory is high, consider scaling: PATCH `.../serverfarms/{name}` to update the SKU tier or worker count

### 3. Set up VNet integration with custom routing

1. List current VNet connections: GET `.../serverfarms/{name}/virtualNetworkConnections`
2. Get details for a specific VNet: GET `.../serverfarms/{name}/virtualNetworkConnections/{vnetName}`
3. Check existing routes: GET `.../serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes`
4. Create a new route: PUT `.../serverfarms/{name}/virtualNetworkConnections/{vnetName}/routes/{routeName}` with `route` body containing `startAddress`, `endAddress`, and `routeType`
5. Update the VNet gateway if needed: PUT `.../serverfarms/{name}/virtualNetworkConnections/{vnetName}/gateways/{gatewayName}`

### 4. Manage hybrid connections

1. List all hybrid connection relays: GET `.../serverfarms/{name}/hybridConnectionRelays`
2. Check the plan's hybrid connection limit: GET `.../serverfarms/{name}/hybridConnectionPlanLimits/limit`
3. Get details for a specific relay: GET `.../serverfarms/{name}/hybridConnectionNamespaces/{ns}/relays/{relay}`
4. Retrieve connection keys: POST `.../serverfarms/{name}/hybridConnectionNamespaces/{ns}/relays/{relay}/listKeys`
5. List which sites use this relay: GET `.../serverfarms/{name}/hybridConnectionNamespaces/{ns}/relays/{relay}/sites`
6. Remove a relay when no longer needed: DELETE `.../serverfarms/{name}/hybridConnectionNamespaces/{ns}/relays/{relay}`

### 5. Restart or reboot plan workers

1. Soft restart all sites (minimal disruption): POST `.../serverfarms/{name}/restartSites?softRestart=true`
2. If issues persist, hard restart all sites: POST `.../serverfarms/{name}/restartSites` (no `softRestart` parameter)
3. For a targeted fix, reboot a single worker: POST `.../serverfarms/{name}/workers/{workerName}/reboot`
4. Verify recovery by checking metrics: GET `.../serverfarms/{name}/metrics`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
