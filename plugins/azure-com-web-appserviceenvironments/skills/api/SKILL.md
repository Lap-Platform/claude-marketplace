---
name: appserviceenvironments-api-client
description: "AppServiceEnvironments API Client API skill. Use when working with AppServiceEnvironments API Client for subscriptions. Covers 42 endpoints."
version: 1.0.0
generator: lapsh
---

# AppServiceEnvironments API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/hostingEnvironments -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/changeVirtualNetwork -- create first changeVirtualNetwork

## Endpoints

42 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/hostingEnvironments | Get all App Service Environments for a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments | Get all App Service Environments in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name} | Get the properties of an App Service Environment. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name} | Create or update an App Service Environment. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name} | Delete an App Service Environment. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name} | Create or update an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/capacities/compute | Get the used, available, and total worker capacity an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/capacities/virtualip | Get IP addresses assigned to an App Service Environment. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/changeVirtualNetwork | Move an App Service Environment to a different VNET. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/diagnostics | Get diagnostic information for an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/diagnostics/{diagnosticsName} | Get a diagnostics item for an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/inboundNetworkDependenciesEndpoints | Get the network endpoints of all inbound dependencies of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/metricdefinitions | Get global metric definitions of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/metrics | Get global metrics of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools | Get all multi-role pools. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default | Get properties of a multi-role pool. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default | Create or update a multi-role pool. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default | Create or update a multi-role pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default/instances/{instance}/metricdefinitions | Get metric definitions for a specific instance of a multi-role pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default/instances/{instance}/metrics | Get metrics for a specific instance of a multi-role pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default/metricdefinitions | Get metric definitions for a multi-role pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default/metrics | Get metrics for a multi-role pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default/skus | Get available SKUs for scaling a multi-role pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default/usages | Get usage metrics for a multi-role pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/operations | List all currently running operations on the App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/outboundNetworkDependenciesEndpoints | Get the network endpoints of all outbound dependencies of an App Service Environment. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/reboot | Reboot all machines in an App Service Environment. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/resume | Resume an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/serverfarms | Get all App Service plans in an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/sites | Get all apps in an App Service Environment. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/suspend | Suspend an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/usages | Get global usage metrics of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools | Get all worker pools of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName} | Get properties of a worker pool. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName} | Create or update a worker pool. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName} | Create or update a worker pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/instances/{instance}/metricdefinitions | Get metric definitions for a specific instance of a worker pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/instances/{instance}/metrics | Get metrics for a specific instance of a worker pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/metricdefinitions | Get metric definitions for a worker pool of an App Service Environment. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/metrics | Get metrics for a worker pool of a AppServiceEnvironment (App Service Environment). |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/skus | Get available SKUs for scaling a worker pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/usages | Get usage metrics for a worker pool of an App Service Environment. |

## Enhanced Skill Content
## Question Mapping

- "List all App Service Environments in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/hostingEnvironments
- "What App Service Environments exist in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments
- "Get details for a specific App Service Environment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}
- "How do I create or update an App Service Environment?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}
- "How do I delete an App Service Environment?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}
- "What is the compute capacity of my ASE?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/capacities/compute
- "How do I suspend an App Service Environment?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/suspend
- "How do I resume a suspended ASE?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/resume
- "What apps are running in my App Service Environment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/sites
- "What worker pools are configured in my ASE?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools
- "How do I scale the front-end (multi-role) pool?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/multiRolePools/default
- "What are the outbound network dependencies for my ASE?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/outboundNetworkDependenciesEndpoints
- "How do I check resource usage in my ASE?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/usages
- "How do I move my ASE to a different virtual network?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/changeVirtualNetwork
- "What metrics are available for a specific worker pool instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName}/instances/{instance}/metrics

## Response Tips

- **List endpoints** (subscriptions-level, resource-group-level, sites, worker pools, server farms): Responses return paginated arrays with a `nextLink` property; follow `nextLink` until null to retrieve all items.
- **Create/Update (PUT, PATCH)**: Return 200 for synchronous completion or 202 for long-running operations; on 202 check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Delete**: Returns 202 (accepted, still deleting) or 204 (already gone); treat both as success but poll on 202 if you need confirmation.
- **Metrics and metric definitions**: Responses contain nested `value[]` arrays; metric definitions list `metricAvailabilities` with supported time grains you must match when querying metrics.
- **Capacities and usages**: Return nested objects with `name.value`, `currentValue`, and `limit` fields -- compare `currentValue` to `limit` to assess remaining headroom.
- **Error responses** (400, 404, 409): Body contains a `code` and `message` in a nested `error` object; 409 typically indicates a conflicting ongoing operation.

## Anomaly Flags

- **Long-running operation stuck**: If a PUT, DELETE, PATCH, suspend, resume, or changeVirtualNetwork returns 202 and the async operation poll does not reach a terminal state within 15 minutes, surface a warning.
- **Capacity near limits**: When `usages` endpoint shows `currentValue` exceeding 80% of `limit` for any resource, flag it as approaching exhaustion.
- **409 Conflict on mutations**: Indicates another operation is already in progress on the ASE; surface this and advise the user to check `/operations` before retrying.
- **Deprecated API version**: The spec uses `api-version=2018-02-01`; if Azure returns a `Warning` header or a response hint about deprecation, proactively notify the user to migrate.
- **Inbound/outbound dependency changes**: If network dependency endpoints return new or removed entries compared to a prior call, flag it -- this may indicate platform-side networking changes affecting the ASE.
- **Suspended state**: If a GET on the ASE returns a `status` of `Suspended`, proactively warn before any mutation that the environment must be resumed first.
- **Delete with forceDelete**: Surface a confirmation prompt when `forceDelete` is set, since this bypasses graceful shutdown of running apps.

## Playbook

### 1. Provision a New App Service Environment

1. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments to verify no naming collision exists.
2. PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name} with `hostingEnvironmentEnvelope` containing virtual network subnet, worker pool config, and location.
3. Expect 202; extract the `Azure-AsyncOperation` or `Location` header URL.
4. Poll the operation URL until status is `Succeeded` (provisioning typically takes 1-2 hours).
5. GET the ASE to confirm it is in a `Ready` state.
6. GET `.../capacities/virtualip` to retrieve the assigned VIP and configure DNS accordingly.

### 2. Scale a Worker Pool

1. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName} to inspect current `workerCount` and `workerSize`.
2. GET `.../workerPools/{workerPoolName}/skus` to see available SKUs and validate the target size.
3. GET `.../workerPools/{workerPoolName}/usages` to check current utilization before scaling.
4. PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/workerPools/{workerPoolName} with updated `workerPoolEnvelope` (new count or size).
5. On 202, poll the async operation until complete; verify with a follow-up GET on the worker pool.

### 3. Diagnose Network Connectivity Issues

1. GET `.../diagnostics` to list available diagnostic reports for the ASE.
2. GET `.../diagnostics/{diagnosticsName}` for the specific report relevant to networking.
3. GET `.../inboundNetworkDependenciesEndpoints` to review all inbound dependency addresses and ports.
4. GET `.../outboundNetworkDependenciesEndpoints` to review all outbound dependency addresses and ports.
5. Cross-reference results against NSG/firewall rules to identify blocked traffic.

### 4. Suspend and Resume an ASE to Save Costs

1. GET the ASE to confirm current `status` is `Ready`.
2. GET `.../sites` to inventory running apps that will be affected.
3. POST `.../suspend` -- expect 202; poll until the ASE status transitions to `Suspended`.
4. Verify suspension: GET the ASE and confirm `status` is `Suspended`.
5. To bring it back: POST `.../resume` -- expect 202; poll until `status` returns to `Ready`.
6. GET `.../sites` to confirm all apps are back online.

### 5. Monitor ASE Health and Performance

1. GET `.../metricdefinitions` to discover which metrics are available (CPU, memory, disk, etc.).
2. GET `.../metrics` with `$filter`, `startTime`, `endTime`, and `timeGrain` parameters to pull time-series data.
3. GET `.../multiRolePools/default/metrics` and `.../workerPools/{workerPoolName}/metrics` for pool-level granularity.
4. GET `.../usages` to check resource consumption against quota limits.
5. GET `.../operations` to review any in-flight operations that may be affecting performance.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
