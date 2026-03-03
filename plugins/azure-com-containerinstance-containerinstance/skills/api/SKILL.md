---
name: containerinstancemanagementclient
description: "ContainerInstanceManagementClient API skill. Use when working with ContainerInstanceManagementClient for subscriptions, providers. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# ContainerInstanceManagementClient
API version: 2018-10-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.ContainerInstance/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/restart -- create first restart

## Endpoints

16 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/containerGroups | Get a list of container groups in the specified subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups | Get a list of container groups in the specified subscription and resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName} | Get the properties of the specified container group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName} | Create or update container groups. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName} | Update container groups. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName} | Delete the specified container group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/restart | Restarts all containers in a container group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/stop | Stops all containers in a container group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/start | Starts all containers in a container group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/locations/{location}/usages | Get the usage for a subscription |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/containers/{containerName}/logs | Get the logs for a specified container instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/containers/{containerName}/exec | Executes a command in a specific container instance. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}/subnets/{subnetName}/providers/Microsoft.ContainerInstance/serviceAssociationLinks/default | Delete the container instance service association link for the subnet. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/locations/{location}/cachedImages | Get the list of cached images. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/locations/{location}/capabilities | Get the list of capabilities of the location. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.ContainerInstance/operations | List the operations for Azure Container Instance service. |

## Enhanced Skill Content
## Question Mapping

- "List all my container groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/containerGroups
- "What container groups are in resource group X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups
- "Get details for container group Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}
- "Create a new container group?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}
- "Update tags or properties on a container group?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}
- "Delete a container group?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}
- "Restart a container group?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/restart
- "Stop a running container group?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/stop
- "Start a stopped container group?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/start
- "View logs for a specific container?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/containers/{containerName}/logs
- "Execute a command inside a running container?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups/{containerGroupName}/containers/{containerName}/exec
- "What container instance operations are available?" -> GET /providers/Microsoft.ContainerInstance/operations
- "Check my container quota usage in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/locations/{location}/usages
- "What cached images are available in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/locations/{location}/cachedImages
- "What VM sizes and capabilities are supported in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerInstance/locations/{location}/capabilities

## Response Tips

- **Container group lists** (GET .../containerGroups): Paginated via `nextLink` field -- follow it until absent to retrieve all groups. Each item includes `properties.provisioningState` and `properties.instanceView` for runtime status.
- **Container group detail** (GET/PUT/PATCH single group): Returns full resource object; check `properties.provisioningState` (Succeeded, Failed, Creating, Updating) and `properties.containers[].properties.instanceView.currentState` for per-container health.
- **Create/Update** (PUT returns 200 or 201): 200 means updated existing, 201 means created new. The response body is the full resource; poll `provisioningState` if not yet Succeeded.
- **Lifecycle actions** (restart/stop/start): Return 204 with no body on success -- verify state by fetching the container group afterward.
- **Delete** (DELETE): 200 means deletion completed, 204 means resource was already gone. Both are success states.
- **Logs** (GET .../logs): Returns `content` string; use `tail` query parameter to limit line count. Empty `content` means the container has not produced output yet.
- **Exec** (POST .../exec): Returns `webSocketUri` and `password` for an interactive WebSocket session; these are short-lived.
- **Usages/Cached Images/Capabilities**: Return arrays in `value`; no pagination. Usages include `currentValue` and `limit` for quota tracking.

## Anomaly Flags

- **Provisioning failures**: Surface immediately when `properties.provisioningState` is `Failed` -- include `properties.instanceView.events` for root cause.
- **Quota approaching limits**: After checking usages, flag when `currentValue` exceeds 80% of `limit` for any resource type (CPU cores, memory, container groups).
- **Containers in unhealthy states**: Flag containers where `instanceView.currentState.state` is `Terminated` or `Waiting` with a non-zero exit code or restart count above threshold.
- **Long-running provisioning**: If a container group stays in `Creating` or `Updating` state for more than 5 minutes, surface as potentially stuck.
- **Delete returning 204**: Warn the user that the resource was already absent -- the delete was a no-op, which may indicate a stale reference or prior deletion.
- **Missing logs**: When log content is empty for a container that should be running, flag that the container may have crashed before producing output.
- **API version deprecation**: The spec uses `2018-10-01`; flag if Azure returns warnings or errors suggesting a newer api-version is required.

## Playbook

### 1. Deploy a New Container Group

1. Check regional capabilities: GET .../locations/{location}/capabilities to confirm desired VM size is supported.
2. Check cached images: GET .../locations/{location}/cachedImages to see if your image is pre-cached (faster cold start).
3. Check quota: GET .../locations/{location}/usages to ensure you have headroom.
4. Create the container group: PUT .../containerGroups/{containerGroupName} with the full `containerGroup` resource body (image, ports, CPU/memory, restart policy).
5. Poll the created resource: GET .../containerGroups/{containerGroupName} until `provisioningState` is `Succeeded` or `Failed`.
6. Retrieve logs: GET .../containers/{containerName}/logs to verify the application started correctly.

### 2. Troubleshoot a Failing Container

1. Get container group details: GET .../containerGroups/{containerGroupName}.
2. Inspect `properties.instanceView.events` for error messages and `properties.containers[].properties.instanceView.currentState` for exit codes.
3. Pull container logs: GET .../containers/{containerName}/logs with `tail=200` for recent output.
4. If the container is running but misbehaving, exec into it: POST .../containers/{containerName}/exec with `{"command": "/bin/sh", "terminalSize": {"rows": 24, "cols": 80}}`.
5. If needed, restart the group: POST .../containerGroups/{containerGroupName}/restart and re-check logs.

### 3. Stop, Update, and Restart a Container Group

1. Stop the container group: POST .../containerGroups/{containerGroupName}/stop (returns 204).
2. Confirm stopped: GET .../containerGroups/{containerGroupName} and verify state is `Stopped`.
3. Update configuration: PATCH .../containerGroups/{containerGroupName} with the changed properties (e.g., tags, image version).
4. Start the group: POST .../containerGroups/{containerGroupName}/start (returns 204).
5. Verify running: GET .../containerGroups/{containerGroupName} until `provisioningState` is `Succeeded`.

### 4. Clean Up Container Resources

1. List all container groups in a resource group: GET .../resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerInstance/containerGroups.
2. For each group to remove, delete it: DELETE .../containerGroups/{containerGroupName}.
3. If the group used a VNet, clean up the service association link: DELETE .../virtualNetworks/{vnet}/subnets/{subnet}/providers/Microsoft.ContainerInstance/serviceAssociationLinks/default.
4. Verify deletion: re-list container groups and confirm the targets are gone.

### 5. Monitor Quota and Plan Capacity

1. List all subscriptions' container groups: GET .../providers/Microsoft.ContainerInstance/containerGroups for a full inventory.
2. For each target region, check usage: GET .../locations/{location}/usages.
3. Compare `currentValue` against `limit` for CPU, memory, and group count.
4. Check capabilities: GET .../locations/{location}/capabilities to identify alternative regions or SKUs if current region is near capacity.
5. Surface any usage above 80% as a capacity warning.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
