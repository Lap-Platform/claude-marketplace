---
name: azureanalysisservices
description: "AzureAnalysisServices API skill. Use when working with AzureAnalysisServices for subscriptions, providers. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureAnalysisServices
API version: 2017-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.AnalysisServices/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/suspend -- create first suspend

## Endpoints

16 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName} | Gets details about the specified Analysis Services server. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName} | Provisions the specified Analysis Services server based on the configuration specified in the request. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName} | Deletes the specified Analysis Services server. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName} | Updates the current state of the specified Analysis Services server. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/suspend | Suspends operation of the specified Analysis Services server instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/resume | Resumes operation of the specified Analysis Services server instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers | Gets all the Analysis Services servers for the given resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/servers | Lists all the Analysis Services servers for the given subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/skus | Lists eligible SKUs for Analysis Services resource provider. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/skus | Lists eligible SKUs for an Analysis Services resource. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/listGatewayStatus | Return the gateway status of the specified Analysis Services server instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/dissociateGateway | Dissociates a Unified Gateway associated with the server. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/locations/{location}/checkNameAvailability | Check the name availability in the target location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/locations/{location}/operationresults/{operationId} | List the result of the specified operation. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/locations/{location}/operationstatuses/{operationId} | List the status of operation. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.AnalysisServices/operations | Lists all of the available consumption REST API operations. |

## Enhanced Skill Content
## Question Mapping

- "How do I get details about a specific Analysis Services server?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}
- "How do I create a new Analysis Services server?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}
- "How do I delete an Analysis Services server?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}
- "How do I update or modify an existing Analysis Services server?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}
- "How do I pause or suspend a running server to save costs?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/suspend
- "How do I resume a suspended Analysis Services server?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/resume
- "How do I list all Analysis Services servers in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers
- "How do I list all Analysis Services servers across my entire subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/servers
- "What SKUs or pricing tiers are available for Analysis Services?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/skus
- "What SKUs can I scale my existing server to?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/skus
- "Is a specific server name available before I create it?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/locations/{location}/checkNameAvailability
- "What is the gateway status for my server?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/listGatewayStatus
- "How do I disconnect or remove a gateway from my server?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}/dissociateGateway
- "How do I check whether a long-running operation has completed?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/locations/{location}/operationstatuses/{operationId}
- "What operations does the Analysis Services resource provider support?" -> GET /providers/Microsoft.AnalysisServices/operations

## Response Tips

- **Server CRUD (GET/PUT/PATCH/DELETE server):** Response body contains the full server resource object with `properties.state` indicating provisioning status (Succeeded, Failed, Paused, etc.) and `sku` for the current tier. 201 on create means provisioning started; 202 on any mutation means the operation is asynchronous -- check the `Location` or `Azure-AsyncOperation` header for the polling URL.
- **List endpoints (servers, SKUs, operations):** Responses return a `value` array. There is no pagination for this API version -- all results are returned in a single response.
- **Async operations (suspend, resume, delete, create, update):** A 202 status means the operation is in progress. Poll the operation result or status endpoints using the `operationId` from the response headers until you receive a 200 with a terminal state.
- **Name availability check:** Returns a boolean `nameAvailable` field plus a `reason` and `message` when the name is taken or invalid.
- **Gateway endpoints:** `listGatewayStatus` returns connection status; `dissociateGateway` returns 200 with no body on success.
- **Error responses:** All endpoints return an `error` object with `code` and `message` fields on failure. Common codes: `ResourceNotFound`, `ResourceGroupNotFound`, `InvalidSubscriptionId`.

## Anomaly Flags

- **202 without polling headers:** If a create, update, suspend, resume, or delete returns 202 but no `Location` or `Azure-AsyncOperation` header, surface this immediately -- the operation cannot be tracked.
- **Server state stuck:** If polling an operation status repeatedly returns 202 beyond 10 minutes, flag the operation as potentially stalled.
- **Server in unexpected state:** Surface when `properties.state` is `Failed`, `Deleting`, or `Pausing` unexpectedly, especially after a create or resume call.
- **SKU mismatch after scale:** After a PATCH to change SKU, flag if the returned server object still shows the old SKU (indicates async scaling in progress).
- **Gateway disconnected:** If `listGatewayStatus` returns an error or a disconnected status, proactively warn before attempting data operations that depend on on-premises connectivity.
- **Name unavailable:** When `checkNameAvailability` returns `nameAvailable: false`, surface the `reason` (AlreadyExists vs Invalid) before the user attempts a create.
- **API version deprecation:** If any response includes a `x-ms-deprecation` header or warning, flag the api-version as approaching end-of-life.

## Playbook

### 1. Provision a New Analysis Services Server

1. Call `checkNameAvailability` with the desired server name and location to confirm the name is free.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/skus` to list available SKUs and select an appropriate tier.
3. Call `PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AnalysisServices/servers/{serverName}` with `serverParameters` including `location`, `sku`, and `properties` (e.g., `asAdministrators`).
4. If the response is 201 or 202, extract the operation URL from response headers.
5. Poll `GET .../operationstatuses/{operationId}` until the status is terminal (200 with Succeeded or Failed).
6. Call `GET .../servers/{serverName}` to confirm the server is in `Succeeded` state.

### 2. Suspend and Resume a Server to Manage Costs

1. Call `GET .../servers/{serverName}` to verify current state is `Succeeded` (running).
2. Call `POST .../servers/{serverName}/suspend` to pause the server.
3. Poll the operation status endpoint until complete (200).
4. When ready to use again, call `POST .../servers/{serverName}/resume`.
5. Poll the operation status endpoint until the server returns to `Succeeded` state.

### 3. Scale a Server to a Different SKU

1. Call `GET .../servers/{serverName}/skus` to list eligible target SKUs for the server.
2. Call `PATCH .../servers/{serverName}` with `serverUpdateParameters` containing the new `sku` object (name and tier).
3. If 202 is returned, poll the async operation until complete.
4. Call `GET .../servers/{serverName}` to confirm the SKU has been updated.

### 4. Audit All Servers Across a Subscription

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.AnalysisServices/servers` to list all servers.
2. For each server in the `value` array, inspect `properties.state` and `sku` to identify paused servers, underutilized tiers, or servers in a failed state.
3. For servers with gateways, call `POST .../listGatewayStatus` to verify gateway connectivity.
4. Compile findings: flag servers in `Failed` state, servers running on expensive SKUs with low usage, and disconnected gateways.

### 5. Decommission a Server Safely

1. Call `GET .../servers/{serverName}` to confirm the server exists and note its current state.
2. If the server has a gateway, call `POST .../dissociateGateway` to cleanly disconnect it.
3. Call `DELETE .../servers/{serverName}` to initiate deletion.
4. If 202 is returned, poll the operation status endpoint until the operation completes.
5. Call `GET .../servers/{serverName}` to confirm a 404 (ResourceNotFound) is returned, verifying full removal.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
