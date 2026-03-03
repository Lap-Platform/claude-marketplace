---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 8 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/Shutdown -- create first Shutdown

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/Shutdown | Shutdown a scale unit node. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/PowerOff | Power off a scale unit node. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/PowerOn | Power on a scale unit node. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/StartMaintenanceMode | Start maintenance mode for a scale unit node. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/StopMaintenanceMode | Stop maintenance mode for a scale unit node. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/Repair | Repairs a node of the cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode} | Return the requested scale unit node. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes | Returns a list of all scale unit nodes in a location. |

## Enhanced Skill Content
## Question Mapping

- "How do I shut down a scale unit node?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/Shutdown
- "How do I power off a specific node?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/PowerOff
- "How do I power on a scale unit node?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/PowerOn
- "How do I put a node into maintenance mode?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/StartMaintenanceMode
- "How do I take a node out of maintenance mode?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/StopMaintenanceMode
- "How do I repair a faulty scale unit node?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}/Repair
- "What is the status of a specific scale unit node?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode}
- "List all scale unit nodes in a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes
- "What's the difference between shutdown and power off?" -> Shutdown performs a graceful OS shutdown then powers off; PowerOff cuts power immediately without graceful shutdown
- "How do I safely decommission a node for hardware servicing?" -> First StartMaintenanceMode, then Shutdown or PowerOff, perform servicing, then PowerOn, then StopMaintenanceMode
- "How do I check if a node exists before operating on it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes/{scaleUnitNode} (404 means not found)
- "How do I trigger a bare-metal repair on a node?" -> POST .../Repair with the `bareMetalNode` map in the request body specifying the bare-metal node details
- "Which nodes are available in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/scaleUnitNodes

## Response Tips

- **Power/Maintenance/Repair actions (POST):** 200 means the operation completed synchronously; 202 means the operation was accepted and is running asynchronously -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Node detail (GET single):** 200 returns the node resource object with properties like power state, maintenance status, and model; 404 means the node name or path is wrong.
- **Node listing (GET collection):** 200 returns a `value` array of node resources; check for a `nextLink` property to handle pagination across large scale units. 404 means the fabric location path is invalid.
- **All endpoints:** Errors follow the standard Azure error envelope (`{ "error": { "code": "...", "message": "..." } }`). Always check `error.code` for machine-readable classification.

## Anomaly Flags

- **202 without async tracking headers:** If a POST returns 202 but no `Location` or `Azure-AsyncOperation` header, the operation may be untrackable -- surface this immediately.
- **Repeated 202s on the same node:** Multiple pending async operations on one node suggest conflicting actions (e.g., PowerOn while a Shutdown is still in progress). Warn the user about potential race conditions.
- **404 on a previously valid node:** The node may have been removed from the scale unit or the fabric location was reconfigured. Flag for investigation.
- **Repair called without maintenance mode:** Calling Repair on a node that has not been placed in maintenance mode first may cause workload disruption. Proactively suggest StartMaintenanceMode before Repair.
- **OAuth token expiration:** All endpoints require OAuth2. If responses suddenly return 401, surface that the token has expired and needs refresh before retrying.
- **Throttling (429):** Azure ARM has per-subscription rate limits. If 429 responses appear, surface the `Retry-After` header value and pause bulk operations.

## Playbook

### 1. Graceful Node Shutdown for Planned Maintenance

1. Call GET `.../scaleUnitNodes/{node}` to confirm the node exists and check its current state.
2. Call POST `.../StartMaintenanceMode` to drain workloads off the node.
3. Poll the node (GET) until the maintenance state reflects that drain is complete.
4. Call POST `.../Shutdown` for a graceful OS-level shutdown.
5. If 202 is returned, poll the async operation URL until the shutdown completes.
6. Perform physical maintenance.
7. Call POST `.../PowerOn` to bring the node back.
8. Call POST `.../StopMaintenanceMode` to return the node to the active pool.

### 2. Emergency Power Cycle a Stuck Node

1. Call GET `.../scaleUnitNodes/{node}` to verify the node's current state.
2. Call POST `.../PowerOff` to force an immediate power cut (no graceful shutdown).
3. Wait for the operation to complete (200 immediate or poll on 202).
4. Call POST `.../PowerOn` to restart the node.
5. Call GET `.../scaleUnitNodes/{node}` to verify the node has returned to a healthy running state.

### 3. Bare-Metal Repair of a Failed Node

1. Call POST `.../StartMaintenanceMode` to remove the node from active rotation.
2. Call POST `.../Shutdown` to power down the node cleanly.
3. Call POST `.../Repair` with the `bareMetalNode` map body containing the bare-metal node configuration (BMC address, MAC, model, etc.).
4. Poll the async operation until repair completes.
5. Call GET `.../scaleUnitNodes/{node}` to verify the node is healthy post-repair.
6. Call POST `.../StopMaintenanceMode` to return the node to the pool.

### 4. Inventory All Nodes in a Fabric Location

1. Call GET `.../scaleUnitNodes` to list all nodes.
2. If the response contains a `nextLink`, follow it with another GET to retrieve the next page.
3. Repeat until no `nextLink` is present.
4. For each node, inspect properties like power state, maintenance mode, and model to build a full inventory.

### 5. Validate Node Health Before Workload Deployment

1. Call GET `.../scaleUnitNodes` to retrieve all nodes.
2. For each node, check that its power state is "Running" and it is not in maintenance mode.
3. If any node is powered off, call POST `.../PowerOn`.
4. If any node is in maintenance mode unexpectedly, call POST `.../StopMaintenanceMode`.
5. Re-query GET `.../scaleUnitNodes/{node}` for each remediated node to confirm healthy state before proceeding with deployment.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
