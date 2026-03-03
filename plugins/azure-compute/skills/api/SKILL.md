---
name: computemanagementclient
description: "ComputeManagementClient API skill. Use when working with ComputeManagementClient for providers, subscriptions. Covers 109 endpoints."
version: 1.0.0
generator: lapsh
---

# ComputeManagementClient
API version: 2019-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Compute/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/logAnalytics/apiAccess/getRequestRateByInterval -- create first getRequestRateByInterval

## Endpoints

109 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Compute/operations | Gets a list of compute operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/availabilitySets | Lists all availability sets in a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/hostGroups | Lists all of the dedicated host groups in the subscription. Use the nextLink property in the response to get the next page of dedicated host groups. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/images | Gets the list of Images in the subscription. Use nextLink property in the response to get the next page of Images. Do this till nextLink is null to fetch all the Images. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/logAnalytics/apiAccess/getRequestRateByInterval | Export logs that show Api requests made by this subscription in the given time window to show throttling activities. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/logAnalytics/apiAccess/getThrottledRequests | Export logs that show total throttled Api requests for this subscription in the given time window. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers | Gets a list of virtual machine image publishers for the specified Azure location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmextension/types | Gets a list of virtual machine extension image types. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmextension/types/{type}/versions | Gets a list of virtual machine extension image versions. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmextension/types/{type}/versions/{version} | Gets a virtual machine extension image. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmimage/offers | Gets a list of virtual machine image offers for the specified location and publisher. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmimage/offers/{offer}/skus | Gets a list of virtual machine image SKUs for the specified location, publisher, and offer. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmimage/offers/{offer}/skus/{skus}/versions | Gets a list of all virtual machine image versions for the specified location, publisher, offer, and SKU. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmimage/offers/{offer}/skus/{skus}/versions/{version} | Gets a virtual machine image. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/usages | Gets, for the specified location, the current compute resource usage information as well as the limits for compute resources under the subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/virtualMachines | Gets all the virtual machines under the specified subscription for the specified location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/vmSizes | This API is deprecated. Use [Resources Skus](https://docs.microsoft.com/en-us/rest/api/compute/resourceskus/list) |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/proximityPlacementGroups | Lists all proximity placement groups in a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/virtualMachineScaleSets | Gets a list of all VM Scale Sets in the subscription, regardless of the associated resource group. Use nextLink property in the response to get the next page of VM Scale Sets. Do this till nextLink is null to fetch all the VM Scale Sets. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute/virtualMachines | Lists all of the virtual machines in the specified subscription. Use the nextLink property in the response to get the next page of virtual machines. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/availabilitySets | Lists all availability sets in a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/availabilitySets/{availabilitySetName} | Delete an availability set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/availabilitySets/{availabilitySetName} | Retrieves information about an availability set. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/availabilitySets/{availabilitySetName} | Update an availability set. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/availabilitySets/{availabilitySetName} | Create or update an availability set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/availabilitySets/{availabilitySetName}/vmSizes | Lists all available virtual machine sizes that can be used to create a new virtual machine in an existing availability set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups | Lists all of the dedicated host groups in the specified resource group. Use the nextLink property in the response to get the next page of dedicated host groups. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName} | Delete a dedicated host group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName} | Retrieves information about a dedicated host group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName} | Update an dedicated host group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName} | Create or update a dedicated host group. For details of Dedicated Host and Dedicated Host Groups please see [Dedicated Host Documentation] (https://go.microsoft.com/fwlink/?linkid=2082596) |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName}/hosts | Lists all of the dedicated hosts in the specified dedicated host group. Use the nextLink property in the response to get the next page of dedicated hosts. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName}/hosts/{hostName} | Delete a dedicated host. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName}/hosts/{hostName} | Retrieves information about a dedicated host. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName}/hosts/{hostName} | Update an dedicated host . |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/hostGroups/{hostGroupName}/hosts/{hostName} | Create or update a dedicated host . |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/images | Gets the list of images under a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/images/{imageName} | Deletes an Image. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/images/{imageName} | Gets an image. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/images/{imageName} | Update an image. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/images/{imageName} | Create or update an image. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/proximityPlacementGroups | Lists all proximity placement groups in a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/proximityPlacementGroups/{proximityPlacementGroupName} | Delete a proximity placement group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/proximityPlacementGroups/{proximityPlacementGroupName} | Retrieves information about a proximity placement group . |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/proximityPlacementGroups/{proximityPlacementGroupName} | Update a proximity placement group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/proximityPlacementGroups/{proximityPlacementGroupName} | Create or update a proximity placement group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets | Gets a list of all VM scale sets under a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{virtualMachineScaleSetName}/virtualMachines | Gets a list of all virtual machines in a VM scale sets. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName} | Deletes a VM scale set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName} | Display information about a virtual machine scale set. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName} | Update a VM scale set. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName} | Create or update a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/convertToSinglePlacementGroup | Converts SinglePlacementGroup property to false for a existing virtual machine scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/deallocate | Deallocates specific virtual machines in a VM scale set. Shuts down the virtual machines and releases the compute resources. You are not billed for the compute resources that this virtual machine scale set deallocates. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/delete | Deletes virtual machines in a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/extensionRollingUpgrade | Starts a rolling upgrade to move all extensions for all virtual machine scale set instances to the latest available extension version. Instances which are already running the latest extension versions are not affected. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/extensions | Gets a list of all extensions in a VM scale set. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/extensions/{vmssExtensionName} | The operation to delete the extension. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/extensions/{vmssExtensionName} | The operation to get the extension. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/extensions/{vmssExtensionName} | The operation to create or update an extension. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/forceRecoveryServiceFabricPlatformUpdateDomainWalk | Manual platform update domain walk to update virtual machines in a service fabric virtual machine scale set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/instanceView | Gets the status of a VM scale set instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/manualupgrade | Upgrades one or more virtual machines to the latest SKU set in the VM scale set model. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/osRollingUpgrade | Starts a rolling upgrade to move all virtual machine scale set instances to the latest available Platform Image OS version. Instances which are already running the latest available OS version are not affected. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/osUpgradeHistory | Gets list of OS upgrades on a VM scale set instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/performMaintenance | Perform maintenance on one or more virtual machines in a VM scale set. Operation on instances which are not eligible for perform maintenance will be failed. Please refer to best practices for more details: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-maintenance-notifications |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/poweroff | Power off (stop) one or more virtual machines in a VM scale set. Note that resources are still attached and you are getting charged for the resources. Instead, use deallocate to release resources and avoid charges. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/redeploy | Shuts down all the virtual machines in the virtual machine scale set, moves them to a new node, and powers them back on. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/reimage | Reimages (upgrade the operating system) one or more virtual machines in a VM scale set which don't have a ephemeral OS disk, for virtual machines who have a ephemeral OS disk the virtual machine is reset to initial state. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/reimageall | Reimages all the disks ( including data disks ) in the virtual machines in a VM scale set. This operation is only supported for managed disks. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/restart | Restarts one or more virtual machines in a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/rollingUpgrades/cancel | Cancels the current virtual machine scale set rolling upgrade. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/rollingUpgrades/latest | Gets the status of the latest virtual machine scale set rolling upgrade. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/skus | Gets a list of SKUs available for your VM scale set, including the minimum and maximum VM instances allowed for each SKU. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/start | Starts one or more virtual machines in a VM scale set. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId} | Deletes a virtual machine from a VM scale set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId} | Gets a virtual machine from a VM scale set. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId} | Updates a virtual machine of a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/deallocate | Deallocates a specific virtual machine in a VM scale set. Shuts down the virtual machine and releases the compute resources it uses. You are not billed for the compute resources of this virtual machine once it is deallocated. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/instanceView | Gets the status of a virtual machine from a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/performMaintenance | Performs maintenance on a virtual machine in a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/poweroff | Power off (stop) a virtual machine in a VM scale set. Note that resources are still attached and you are getting charged for the resources. Instead, use deallocate to release resources and avoid charges. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/redeploy | Shuts down the virtual machine in the virtual machine scale set, moves it to a new node, and powers it back on. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/reimage | Reimages (upgrade the operating system) a specific virtual machine in a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/reimageall | Allows you to re-image all the disks ( including data disks ) in the a VM scale set instance. This operation is only supported for managed disks. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/restart | Restarts a virtual machine in a VM scale set. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/start | Starts a virtual machine in a VM scale set. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines | Lists all of the virtual machines in the specified resource group. Use the nextLink property in the response to get the next page of virtual machines. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName} | The operation to delete a virtual machine. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName} | Retrieves information about the model view or the instance view of a virtual machine. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName} | The operation to update a virtual machine. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName} | The operation to create or update a virtual machine. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/capture | Captures the VM by copying virtual hard disks of the VM and outputs a template that can be used to create similar VMs. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/convertToManagedDisks | Converts virtual machine disks from blob-based to managed disks. Virtual machine must be stop-deallocated before invoking this operation. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/deallocate | Shuts down the virtual machine and releases the compute resources. You are not billed for the compute resources that this virtual machine uses. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions | The operation to get all extensions of a Virtual Machine. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/{vmExtensionName} | The operation to delete the extension. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/{vmExtensionName} | The operation to get the extension. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/{vmExtensionName} | The operation to update the extension. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/{vmExtensionName} | The operation to create or update the extension. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/generalize | Sets the state of the virtual machine to generalized. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/instanceView | Retrieves information about the run-time state of a virtual machine. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/performMaintenance | The operation to perform maintenance on a virtual machine. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/powerOff | The operation to power off (stop) a virtual machine. The virtual machine can be restarted with the same provisioned resources. You are still charged for this virtual machine. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/redeploy | Shuts down the virtual machine, moves it to a new node, and powers it back on. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/reimage | Reimages the virtual machine which has an ephemeral OS disk back to its initial state. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/restart | The operation to restart a virtual machine. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/start | The operation to start a virtual machine. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/vmSizes | Lists all available virtual machine sizes to which the specified virtual machine can be resized. |

## Enhanced Skill Content
## Question Mapping

- "What operations does the Azure Compute provider support?" -> GET /providers/Microsoft.Compute/operations
- "List all virtual machines in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute/virtualMachines
- "Show me VMs in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines
- "Get details for a specific VM" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}
- "How do I create or update a virtual machine?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}
- "Stop a VM without deallocating it" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/powerOff
- "Deallocate a VM to stop billing for compute" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/deallocate
- "What VM sizes are available in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/vmSizes
- "List all scale sets in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute/virtualMachineScaleSets
- "How do I scale down a VMSS by removing specific instances?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachineScaleSets/{vmScaleSetName}/delete
- "What VM images are available from a publisher?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/publishers/{publisherName}/artifacttypes/vmimage/offers
- "Check my compute resource usage in a region" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/usages
- "Get the throttled request log for my subscription" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Compute/locations/{location}/logAnalytics/apiAccess/getThrottledRequests
- "How do I capture a VM to create a custom image?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/capture
- "What extensions are installed on my VM?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions

## Response Tips

- **List endpoints** (VMs, VMSS, images, availability sets): Responses use `value` array with `nextLink` for pagination; always follow `nextLink` until null to get all results.
- **Single resource GETs**: Return the full resource object; use `$expand=instanceView` where supported to include runtime status inline.
- **Async operations** (POST actions returning 202): Response includes `Azure-AsyncOperation` or `Location` header; poll the URL until `provisioningState` is `Succeeded`, `Failed`, or `Canceled`.
- **PUT/PATCH create-or-update**: 200 means updated, 201 means created; the response body contains the full resource with `provisioningState` indicating progress.
- **DELETE operations**: 200 means completed, 202 means accepted (still in progress), 204 means resource already gone; no response body on 204.
- **Log analytics POSTs**: Return a `LogAnalyticsOperationResult` with a SAS URI to download the CSV report; 202 means the report is still generating.
- **Marketplace browsing** (publishers, offers, skus, versions): Hierarchical drill-down; each level returns a flat array, not paginated.

## Anomaly Flags

- **202 without completion polling**: When any power action, delete, or image operation returns 202, surface the async operation URL and remind the user to poll for completion status.
- **Throttling detected**: If `getThrottledRequests` returns non-empty results, proactively warn about API rate limit pressure and suggest spacing out calls or requesting quota increases.
- **Usage near limits**: When `usages` endpoint shows `currentValue` approaching `limit` for any resource type (cores, VMs, availability sets), flag it before the user hits a hard cap.
- **provisioningState not Succeeded**: On any PUT/PATCH/POST response where `provisioningState` is `Failed` or `Canceled`, immediately surface the error details from `error.code` and `error.message`.
- **skipShutdown usage**: When a user powers off a VM or VMSS instance with `skipShutdown=true`, warn that this is a hard stop equivalent to pulling the power cord and risks data loss.
- **Delete with 204 response**: Surface that the resource was already deleted or never existed, so the operation was a no-op.
- **API version mismatch**: This spec uses `2019-03-01`; if the user references features from newer API versions (spot VMs, ephemeral OS disks, capacity reservations), flag that they need a newer `api-version` parameter.

## Playbook

### 1. Provision a New Virtual Machine

1. List available VM sizes in the target region: GET `.../locations/{location}/vmSizes`
2. Browse marketplace images: GET `.../locations/{location}/publishers` then drill into offers, skus, and versions
3. Create or ensure a resource group exists (use Resource Management API, outside this spec)
4. Create the VM: PUT `.../resourceGroups/{rg}/providers/Microsoft.Compute/virtualMachines/{vmName}` with `parameters` body including `hardwareProfile`, `storageProfile`, `osProfile`, and `networkProfile`
5. Poll the `Azure-AsyncOperation` URL from the response header until `provisioningState` is `Succeeded`
6. Verify the VM is running: GET `.../virtualMachines/{vmName}?$expand=instanceView` and check `instanceView.statuses` for `PowerState/running`

### 2. Stop and Deallocate VMs to Save Costs

1. List VMs in the resource group: GET `.../resourceGroups/{rg}/providers/Microsoft.Compute/virtualMachines`
2. For each target VM, deallocate (stops billing): POST `.../virtualMachines/{vmName}/deallocate`
3. If you get 202, poll the async operation URL until complete
4. Confirm status: GET `.../virtualMachines/{vmName}/instanceView` and verify `PowerState/deallocated`
5. To resume later: POST `.../virtualMachines/{vmName}/start` and poll until running

### 3. Scale Out a VM Scale Set and Manage Instances

1. Get current VMSS config: GET `.../virtualMachineScaleSets/{vmScaleSetName}`
2. Update capacity by PATCHing the VMSS with new `sku.capacity` value: PATCH `.../virtualMachineScaleSets/{vmScaleSetName}`
3. List instances in the scale set: GET `.../virtualMachineScaleSets/{vmScaleSetName}/virtualMachines`
4. Check individual instance health: GET `.../virtualMachineScaleSets/{vmScaleSetName}/virtualmachines/{instanceId}/instanceView`
5. To remove specific unhealthy instances: POST `.../virtualMachineScaleSets/{vmScaleSetName}/delete` with `vmInstanceIDs` body containing the instance IDs to remove

### 4. Install and Manage VM Extensions

1. List existing extensions on the VM: GET `.../virtualMachines/{vmName}/extensions`
2. Install a new extension: PUT `.../virtualMachines/{vmName}/extensions/{vmExtensionName}` with `extensionParameters` specifying `publisher`, `type`, `typeHandlerVersion`, and `settings`
3. Poll the async operation if you receive 202; check for 201 (created) or 200 (updated)
4. Verify extension status: GET `.../virtualMachines/{vmName}/extensions/{vmExtensionName}?$expand=instanceView`
5. To update settings: PATCH `.../virtualMachines/{vmName}/extensions/{vmExtensionName}` with modified `extensionParameters`
6. To remove: DELETE `.../virtualMachines/{vmName}/extensions/{vmExtensionName}` and poll until complete

### 5. Capture a VM as a Custom Image for Reuse

1. Stop and deallocate the source VM: POST `.../virtualMachines/{vmName}/deallocate` and wait for completion
2. Generalize the VM (marks it as sysprepped): POST `.../virtualMachines/{vmName}/generalize`
3. Capture the VM: POST `.../virtualMachines/{vmName}/capture` with `parameters` specifying `vhdPrefix` and `destinationContainerName`
4. Poll the async operation; the result contains the VHD template URI
5. Optionally, create a managed image resource: PUT `.../images/{imageName}` pointing to the captured VHD
6. The original VM is no longer usable after generalization; delete it or create new VMs from the captured image


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
