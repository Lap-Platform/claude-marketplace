---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 6 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/PowerOff -- create first PowerOff

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/PowerOff | Power off an infrastructure role instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/PowerOn | Power on an infrastructure role instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/Shutdown | Shut down an infrastructure role instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/Reboot | Reboot an infrastructure role instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance} | Return the requested infrastructure role instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances | Returns a list of all infrastructure role instances at a location. |

## Enhanced Skill Content
## Question Mapping

- "How do I power off an infrastructure role instance?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/PowerOff
- "How do I power on an infrastructure role instance?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/PowerOn
- "How do I shut down a fabric infrastructure node?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/Shutdown
- "How do I reboot an infrastructure role instance?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}/Reboot
- "How do I get details about a specific infrastructure role instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances/{infraRoleInstance}
- "How do I list all infrastructure role instances in a fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoleInstances
- "What infrastructure nodes are running in my Azure Stack fabric?" -> GET .../infraRoleInstances
- "How do I gracefully stop a fabric node without data loss?" -> POST .../infraRoleInstances/{infraRoleInstance}/Shutdown
- "How do I force restart an unresponsive infrastructure role instance?" -> POST .../infraRoleInstances/{infraRoleInstance}/Reboot
- "How do I check the current power state of an infrastructure node?" -> GET .../infraRoleInstances/{infraRoleInstance}
- "How do I perform a rolling restart of all fabric infrastructure nodes?" -> GET .../infraRoleInstances then POST .../Reboot for each
- "What is the difference between PowerOff and Shutdown?" -> POST .../PowerOff (hard stop) vs POST .../Shutdown (graceful stop)
- "How do I bring a powered-off node back online?" -> POST .../infraRoleInstances/{infraRoleInstance}/PowerOn

## Response Tips

- **Power actions (PowerOff, PowerOn, Shutdown, Reboot):** 200 means completed synchronously; 202 means accepted as a long-running operation -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Single instance GET:** Returns the full resource object with properties including power state, node size, and scale unit; 404 means the instance name is wrong or does not exist at that fabric location.
- **List instances GET:** Returns an array (possibly within a `value` wrapper) of all infra role instances for the location; 404 means the fabric location or resource group was not found.

## Anomaly Flags

- **202 without completion polling:** If a power action returns 202, surface this to the user -- the operation is still in progress and requires polling the async operation URL.
- **Repeated 404 on known instances:** May indicate the fabric location path is wrong or the infrastructure has been decommissioned. Prompt the user to verify the resource group and location values.
- **Sequential power conflicts:** Flag if the user attempts PowerOn immediately after Shutdown or PowerOff on the same instance without confirming the prior operation completed (risk of conflicting async operations).
- **Bulk operations without inventory:** If the user requests operations across multiple instances without first listing them, recommend running the list endpoint to confirm targets.
- **OAuth token expiry:** Since all endpoints require OAuth2, surface token refresh needs proactively if requests start returning 401.

## Playbook

### 1. Gracefully restart a specific infrastructure role instance

1. GET `.../infraRoleInstances/{infraRoleInstance}` to confirm the instance exists and check its current state.
2. POST `.../infraRoleInstances/{infraRoleInstance}/Shutdown` to gracefully stop the instance.
3. If response is 202, poll the async operation URL until completion.
4. POST `.../infraRoleInstances/{infraRoleInstance}/PowerOn` to bring the instance back online.
5. If response is 202, poll until the power-on operation completes.
6. GET `.../infraRoleInstances/{infraRoleInstance}` to verify the instance is running.

### 2. Inventory all infrastructure role instances

1. GET `.../infraRoleInstances` to retrieve the full list of instances at the fabric location.
2. For each instance in the response, note the instance name and power state.
3. Optionally GET `.../infraRoleInstances/{infraRoleInstance}` for detailed properties on any instance of interest.

### 3. Emergency reboot of an unresponsive node

1. GET `.../infraRoleInstances/{infraRoleInstance}` to confirm the target instance identity.
2. POST `.../infraRoleInstances/{infraRoleInstance}/Reboot` to force a reboot.
3. If response is 202, poll the async operation URL until the reboot completes.
4. GET `.../infraRoleInstances/{infraRoleInstance}` to verify the instance has returned to a healthy running state.

### 4. Rolling power cycle across all instances

1. GET `.../infraRoleInstances` to list all instances.
2. For each instance (one at a time to maintain availability):
   a. POST `.../Shutdown` and wait for completion.
   b. POST `.../PowerOn` and wait for completion.
   c. GET `.../infraRoleInstances/{infraRoleInstance}` to confirm healthy state before proceeding to the next.
3. After all instances have been cycled, run the list endpoint again to verify all are running.

### 5. Power off a decommissioned node

1. GET `.../infraRoleInstances/{infraRoleInstance}` to confirm the instance exists and review its current state.
2. POST `.../infraRoleInstances/{infraRoleInstance}/Shutdown` for a graceful stop (preferred) or POST `.../PowerOff` for an immediate hard stop.
3. Wait for async completion if 202 is returned.
4. GET `.../infraRoleInstances/{infraRoleInstance}` to confirm the instance is in a powered-off state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
