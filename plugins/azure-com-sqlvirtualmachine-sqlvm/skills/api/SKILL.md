---
name: sqlvirtualmachinemanagementclient
description: "SqlVirtualMachineManagementClient API skill. Use when working with SqlVirtualMachineManagementClient for subscriptions, providers. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# SqlVirtualMachineManagementClient
API version: 2017-03-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.SqlVirtualMachine/operations -- verify access

## Endpoints

18 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners/{availabilityGroupListenerName} | Gets an availability group listener. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners/{availabilityGroupListenerName} | Creates or updates an availability group listener. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners/{availabilityGroupListenerName} | Deletes an availability group listener. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners | Lists all availability group listeners in a SQL virtual machine group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName} | Gets a SQL virtual machine group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName} | Creates or updates a SQL virtual machine group. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName} | Deletes a SQL virtual machine group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName} | Updates SQL virtual machine group tags. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups | Gets all SQL virtual machine groups in a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups | Gets all SQL virtual machine groups in a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/sqlVirtualMachines | Gets the list of sql virtual machines in a SQL virtual machine group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines | Gets all SQL virtual machines in a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName} | Gets a SQL virtual machine. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName} | Creates or updates a SQL virtual machine. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName} | Deletes a SQL virtual machine. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName} | Updates a SQL virtual machine. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines | Gets all SQL virtual machines in a resource group. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.SqlVirtualMachine/operations | Lists all of the available SQL Rest API operations. |

## Enhanced Skill Content
## Question Mapping

- "How do I get details of a specific SQL virtual machine?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName}
- "List all SQL virtual machines in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines
- "List SQL VMs in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines
- "How do I register a new SQL virtual machine?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName}
- "How do I delete a SQL virtual machine registration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName}
- "Update settings on an existing SQL VM without full replacement" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName}
- "What SQL VM groups exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups
- "Create a new SQL virtual machine group for Always On availability" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}
- "How do I set up an availability group listener?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners/{availabilityGroupListenerName}
- "List all availability group listeners in a VM group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners
- "Which SQL VMs belong to a specific group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/sqlVirtualMachines
- "What operations are available for the SQL VM resource provider?" -> GET /providers/Microsoft.SqlVirtualMachine/operations
- "How do I remove an availability group listener?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}/availabilityGroupListeners/{availabilityGroupListenerName}
- "How do I get expanded details (like configuration assessments) for a SQL VM?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName} with $expand parameter

## Response Tips

- **SQL Virtual Machines (GET single):** Response includes provisioning state, SQL image details, and server configuration nested under `properties`; use `$expand` to retrieve additional assessment data.
- **SQL Virtual Machines (list endpoints):** Results are returned in a `value` array; check for `nextLink` to handle pagination across large inventories.
- **SQL VM Groups:** Response nests cluster configuration (WSFC domain, storage accounts, OU path) under `properties.wsfcDomainProfile`.
- **Availability Group Listeners:** Listener properties include `loadBalancerConfigurations` as a nested array -- each entry maps a load balancer to probe port and SQL VM instances.
- **PUT/create endpoints:** Return 200 if the resource already exists (updated) or 201 if newly created; always check the status code to distinguish create from update.
- **DELETE endpoints:** Return 200 (completed), 202 (accepted, still deleting), or 204 (already gone); a 202 means you should poll the operation until completion.
- **PATCH endpoints:** Return 200 with the full updated resource; only send the fields you want to change in the `parameters` body.
- **Operations list:** Returns a flat `value` array of available ARM operations with display metadata -- no pagination expected.

## Anomaly Flags

- **202 on DELETE responses:** The operation is long-running. Surface this to the user and recommend polling the Azure-AsyncOperation or Location header URL until the operation completes.
- **Provisioning state not "Succeeded":** If any GET response shows `properties.provisioningState` as "Failed", "Canceled", or "InProgress", flag this immediately -- the resource may be in an inconsistent state.
- **Missing or preview API version:** This API uses `2017-03-01-preview`. Flag that it is a preview version which may have breaking changes, limited SLA, and may not be suitable for production workloads without checking for a newer stable version.
- **$expand parameter only on single VM GET:** If the user attempts to use `$expand` on a list endpoint, warn that it is only supported on the individual SQL VM GET endpoint.
- **Empty value arrays on list calls:** If a list endpoint returns `{"value": []}`, proactively confirm the subscription ID, resource group, and resource provider registration -- the provider may not be registered in the subscription.
- **SQL VM group deletion with active members:** If a user attempts to delete a VM group that still has SQL VMs or listeners attached, surface a warning that dependent resources should be removed first to avoid orphaned configurations.

## Playbook

### 1. Register a SQL VM and verify its status

1. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName}` with the required `parameters` body (including `virtualMachineResourceId`, `sqlServerLicenseType`, and `location`).
2. Check the response status: 201 means created, 200 means an existing registration was updated.
3. Call GET on the same resource path to verify `properties.provisioningState` is "Succeeded".
4. If provisioning state is "InProgress", wait and poll the GET endpoint until it transitions to "Succeeded" or "Failed".

### 2. Set up an Always On availability group with a listener

1. Create a SQL VM group by calling PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups/{sqlVirtualMachineGroupName}` with WSFC domain profile configuration in the `parameters` body.
2. Verify the group is provisioned by calling GET on the group resource and checking `provisioningState`.
3. Register each participating SQL VM with the group by calling PUT on the individual SQL VM endpoints with `sqlVirtualMachineGroupResourceId` set in the parameters.
4. Create the availability group listener by calling PUT `/...sqlVirtualMachineGroups/{groupName}/availabilityGroupListeners/{listenerName}` with load balancer configuration, port, and SQL VM instance references.
5. Verify the listener by calling GET on the listener resource to confirm it is provisioned and reachable.

### 3. Inventory all SQL VMs across a subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines` to list all SQL VMs.
2. If the response contains a `nextLink`, follow it with additional GET requests until all pages are consumed.
3. For each VM requiring detailed configuration, call GET on the individual VM endpoint with `$expand` to retrieve extended properties.
4. Optionally, call GET `/subscriptions/{subscriptionId}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachineGroups` to cross-reference which VMs belong to availability groups.

### 4. Update SQL VM configuration without downtime

1. Call GET on the target SQL VM to retrieve its current configuration and `properties` values.
2. Build a PATCH body containing only the properties to change (e.g., `sqlManagement`, `autoPatchingSettings`, `autoBackupSettings`).
3. Call PATCH `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SqlVirtualMachine/sqlVirtualMachines/{sqlVirtualMachineName}` with the partial update body.
4. Verify the 200 response and confirm `provisioningState` is "Succeeded" in the returned resource.

### 5. Decommission a SQL VM group and its resources

1. List all availability group listeners in the group by calling GET `/...sqlVirtualMachineGroups/{groupName}/availabilityGroupListeners`.
2. Delete each listener by calling DELETE on its resource path; if 202 is returned, poll until the operation completes.
3. List all SQL VMs in the group by calling GET `/...sqlVirtualMachineGroups/{groupName}/sqlVirtualMachines`.
4. Disassociate each SQL VM from the group by calling PATCH on each VM to clear the `sqlVirtualMachineGroupResourceId` field.
5. Delete the SQL VM group by calling DELETE on the group resource; handle 202 responses by polling for completion.
6. Confirm cleanup by calling GET on the group path and expecting a 404 response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
