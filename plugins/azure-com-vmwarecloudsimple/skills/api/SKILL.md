---
name: vmwarecloudsimple
description: "VMwareCloudSimple API skill. Use when working with VMwareCloudSimple for providers, subscriptions. Covers 34 endpoints."
version: 1.0.0
generator: lapsh
---

# VMwareCloudSimple
API version: 2019-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.VMwareCloudSimple/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}/start -- create first start

## Endpoints

34 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.VMwareCloudSimple/operations | Implements list of available operations |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes | Implements list of dedicated cloud nodes within subscription method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices | Implements list of dedicatedCloudService objects within subscription method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/availabilities | Implements SkuAvailability List method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/operationResults/{operationId} | Implements get of async operation |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds | Implements private cloud list GET method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName} | Implements private cloud GET method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/customizationPolicies | Implements get of customization policies list |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/customizationPolicies/{customizationPolicyName} | Implements get of customization policy |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/resourcePools | Implements get of resource pools list |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/resourcePools/{resourcePoolName} | Implements get of resource pool |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/virtualMachineTemplates | Implements list of available VM templates |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/virtualMachineTemplates/{virtualMachineTemplateName} | Implements virtual machine template GET method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/virtualNetworks | Implements list available virtual networks within a subscription method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/virtualNetworks/{virtualNetworkName} | Implements virtual network GET method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/usages | Implements Usages List method |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/virtualMachines | Implements list virtual machine within subscription method |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes | Implements list of dedicated cloud nodes within RG method |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes/{dedicatedCloudNodeName} | Implements dedicated cloud node GET method |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes/{dedicatedCloudNodeName} | Implements dedicated cloud node PUT method |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes/{dedicatedCloudNodeName} | Implements dedicated cloud node DELETE method |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes/{dedicatedCloudNodeName} | Implements dedicated cloud node PATCH method |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices | Implements list of dedicatedCloudService objects within RG method |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices/{dedicatedCloudServiceName} | Implements dedicatedCloudService GET method |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices/{dedicatedCloudServiceName} | Implements dedicated cloud service PUT method |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices/{dedicatedCloudServiceName} | Implements dedicatedCloudService DELETE method |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices/{dedicatedCloudServiceName} | Implements dedicatedCloudService PATCH method |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines | Implements list virtual machine within RG method |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName} | Implements virtual machine GET method |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName} | Implements virtual machine PUT method |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName} | Implements virtual machine DELETE method |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName} | Implements virtual machine PATCH method |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}/start | Implements a start method for a virtual machine |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}/stop | Implements shutdown, poweroff, and suspend method for a virtual machine |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in VMware CloudSimple?" -> GET /providers/Microsoft.VMwareCloudSimple/operations
- "List all dedicated cloud nodes in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes
- "Show me virtual machines in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines
- "What private clouds exist in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds
- "How do I provision a new dedicated cloud node?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes/{dedicatedCloudNodeName}
- "Create a new virtual machine in CloudSimple" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}
- "Stop a running virtual machine" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}/stop
- "Start a stopped virtual machine" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}/start
- "What VM templates are available in my private cloud?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/virtualMachineTemplates
- "Check resource usage and quotas in a region" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/usages
- "What virtual networks exist in my private cloud?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/virtualNetworks
- "Delete a dedicated cloud service" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices/{dedicatedCloudServiceName}
- "What customization policies can I apply to VMs?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/privateClouds/{pcName}/customizationPolicies
- "Check the status of a long-running operation" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.VMwareCloudSimple/locations/{regionId}/operationResults/{operationId}
- "Update tags on a virtual machine" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{virtualMachineName}

## Response Tips

- **List endpoints** (nodes, services, VMs): Responses are paginated via `$skipToken`; if present in the response, pass it in the next request to fetch the next page. Use `$top` to control page size and `$filter` for OData filtering.
- **Single resource GET**: Returns the full resource object with `id`, `name`, `type`, `location`, and `properties` nested object containing resource-specific details.
- **PUT (create/update)**: Returns 200 for updates; VM creation may return 201 for new resources. The `Referer` header is required and used for async operation tracking.
- **DELETE**: Returns 204 (no content) on success for nodes and services. VM deletion returns 202 (accepted) for async deletion or 204 if already gone.
- **POST (start/stop)**: Returns 200 if completed synchronously or 202 if accepted for async processing. Poll the operation result endpoint to track completion.
- **Operation results**: Returns 200 when complete, 202 when still in progress, or 204 when the operation produced no result. Use the `Referer`-linked operation ID to poll.
- **Private cloud resources** (templates, networks, pools): Require both `regionId` and `pcName` path params; templates and networks additionally require `resourcePoolName` as a query parameter.

## Anomaly Flags

- **202 Accepted on VM operations**: Start, stop, delete, and create return 202 for async processing. Surface this to the user and suggest polling the operation results endpoint with the returned operation ID.
- **Referer header required**: PUT/DELETE/POST on VMs and PUT on nodes require a `Referer` header. Missing it will cause failures -- flag any request to these endpoints without it.
- **$skipToken in response**: If a list response includes `$skipToken`, there are more pages. Alert the user that results are incomplete and offer to fetch the next page.
- **204 on operation results**: A 204 from the operation results endpoint means the operation completed with no output. This is normal for deletes but unexpected for creates -- flag the latter.
- **Usage approaching limits**: When the usages endpoint shows current values near the limit, proactively warn about quota exhaustion before provisioning new resources.
- **$filter on resourcePoolName**: The virtualMachineTemplates and virtualNetworks endpoints require `resourcePoolName` as a query parameter despite being under a private cloud path. Flag if missing, as it silently returns incomplete results.
- **API version pinned to 2019-04-01**: This is a legacy API version. Surface this if the user expects features from newer Azure VMware Solution APIs.

## Playbook

### 1. Provision a New Virtual Machine

1. List available private clouds: GET `/subscriptions/{sub}/providers/Microsoft.VMwareCloudSimple/locations/{region}/privateClouds`
2. Get resource pools in the target private cloud: GET `...privateClouds/{pcName}/resourcePools`
3. List available VM templates: GET `...privateClouds/{pcName}/virtualMachineTemplates?resourcePoolName={pool}`
4. List virtual networks: GET `...privateClouds/{pcName}/virtualNetworks?resourcePoolName={pool}`
5. Create the VM: PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{vmName}` with the template, resource pool, and network references in the request body. Include the `Referer` header.
6. If response is 200/201, the VM is ready. If 202, poll the operation results endpoint until it returns 200 or 204.

### 2. Stop and Restart a Virtual Machine

1. Stop the VM: POST `...virtualMachines/{vmName}/stop` with `Referer` header. Optionally set `mode` to control shutdown behavior (e.g., graceful vs hard).
2. If 202, poll operation results until complete.
3. Confirm the VM state by fetching it: GET `...virtualMachines/{vmName}` and check the `properties.status` field.
4. Start the VM: POST `...virtualMachines/{vmName}/start` with `Referer` header.
5. If 202, poll operation results. Confirm running state with another GET.

### 3. Inventory All CloudSimple Resources

1. List all dedicated cloud nodes across the subscription: GET `/subscriptions/{sub}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes`. Page through using `$skipToken`.
2. List all dedicated cloud services: GET `/subscriptions/{sub}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudServices`. Page through similarly.
3. List all virtual machines: GET `/subscriptions/{sub}/providers/Microsoft.VMwareCloudSimple/virtualMachines`. Page through similarly.
4. For each resource group of interest, optionally drill down with the resource-group-scoped list endpoints for more granular views.
5. Check regional usage: GET `...locations/{region}/usages` to see quota consumption.

### 4. Set Up a Dedicated Cloud Node

1. Check availability in the target region: GET `...locations/{regionId}/availabilities` with optional `skuId` filter.
2. Create the dedicated cloud node: PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.VMwareCloudSimple/dedicatedCloudNodes/{nodeName}` with `Referer` header and the node configuration in the request body.
3. If 200, the node is provisioned. Poll operation results if you received a different status.
4. Verify by fetching the node: GET `...dedicatedCloudNodes/{nodeName}`.
5. Optionally tag or update the node: PATCH `...dedicatedCloudNodes/{nodeName}` with updated properties.

### 5. Apply a Customization Policy to a VM

1. List customization policies for the private cloud: GET `...privateClouds/{pcName}/customizationPolicies`. Optionally filter with `$filter`.
2. Get details of a specific policy: GET `...customizationPolicies/{policyName}` to review its configuration.
3. Update the VM with the policy reference: PATCH `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.VMwareCloudSimple/virtualMachines/{vmName}` including the customization policy ID in the request body.
4. Verify the update: GET `...virtualMachines/{vmName}` and confirm the policy is reflected in properties.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
