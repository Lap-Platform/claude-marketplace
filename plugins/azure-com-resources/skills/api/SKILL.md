---
name: resourcemanagementclient
description: "ResourceManagementClient API skill. Use when working with ResourceManagementClient for providers, {scope}, subscriptions. Covers 86 endpoints."
version: 1.0.0
generator: lapsh
---

# ResourceManagementClient
API version: 2019-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Resources/operations -- verify access
3. POST /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel -- create first cancel

## Endpoints

86 endpoints across 4 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Resources/operations | Lists all of the available Microsoft.Resources REST API operations. |
| DELETE | /providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| HEAD | /providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources at tenant scope. |
| GET | /providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| POST | /providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| POST | /providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /providers/Microsoft.Resources/deployments/ | Get all the deployments at the tenant scope. |
| DELETE | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| HEAD | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources at management group scope. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| POST | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| POST | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/ | Get all the deployments for a management group. |
| GET | /providers | Gets all resource providers for the tenant. |
| GET | /providers/{resourceProviderNamespace} | Gets the specified resource provider at the tenant level. |
| GET | /providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| GET | /providers/Microsoft.Resources/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |
| POST | /providers/Microsoft.Resources/calculateTemplateHash | Calculate the hash of the given template. |

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| HEAD | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources at a given scope. |
| GET | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| POST | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| POST | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /{scope}/providers/Microsoft.Resources/deployments/ | Get all the deployments at the given scope. |
| GET | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| GET | /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| HEAD | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources at subscription scope. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/whatIf | Returns changes that will be made by the deployment if executed at the scope of the subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/ | Get all the deployments for a subscription. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| HEAD | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources to a resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/whatIf | Returns changes that will be made by the deployment if executed at the scope of the resource group. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/ | Get all the deployments for a resource group. |
| POST | /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/unregister | Unregisters a subscription from a resource provider. |
| POST | /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/register | Registers a subscription with a resource provider. |
| GET | /subscriptions/{subscriptionId}/providers | Gets all resource providers for a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace} | Gets the specified resource provider. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/resources | Get all the resources for a resource group. |
| HEAD | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Checks whether a resource group exists. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Creates or updates a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Deletes a resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Gets a resource group. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Updates a resource group. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/exportTemplate | Captures the specified resource group as a template. |
| GET | /subscriptions/{subscriptionId}/resourcegroups | Gets all the resource groups for a subscription. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/moveResources | Moves resources from one resource group to another resource group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/validateMoveResources | Validates whether resources can be moved from one resource group to another resource group. |
| GET | /subscriptions/{subscriptionId}/resources | Get all the resources in a subscription. |
| HEAD | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Checks whether a resource exists. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Deletes a resource. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Creates a resource. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Updates a resource. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Gets a resource. |
| DELETE | /subscriptions/{subscriptionId}/tagNames/{tagName}/tagValues/{tagValue} | Deletes a tag value. |
| PUT | /subscriptions/{subscriptionId}/tagNames/{tagName}/tagValues/{tagValue} | Creates a tag value. The name of the tag must already exist. |
| PUT | /subscriptions/{subscriptionId}/tagNames/{tagName} | Creates a tag in the subscription. |
| DELETE | /subscriptions/{subscriptionId}/tagNames/{tagName} | Deletes a tag from the subscription. |
| GET | /subscriptions/{subscriptionId}/tagNames | Gets the names and values of all resource tags that are defined in a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |

### {resourceId}
| Method | Path | Description |
|--------|------|-------------|
| HEAD | /{resourceId} | Checks by ID whether a resource exists. |
| DELETE | /{resourceId} | Deletes a resource by ID. |
| PUT | /{resourceId} | Create a resource by ID. |
| PATCH | /{resourceId} | Updates a resource by ID. |
| GET | /{resourceId} | Gets a resource by ID. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.Resources/operations
- "Delete a deployment?" -> DELETE /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Update a deployment?" -> PUT /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Get deployment details?" -> GET /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Create a cancel?" -> POST /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel
- "Create a validate?" -> POST /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/validate
- "Create a exportTemplate?" -> POST /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate
- "List all deployments?" -> GET /{scope}/providers/Microsoft.Resources/deployments/
- "Delete a deployment?" -> DELETE /providers/Microsoft.Resources/deployments/{deploymentName}
- "Update a deployment?" -> PUT /providers/Microsoft.Resources/deployments/{deploymentName}
- "Get deployment details?" -> GET /providers/Microsoft.Resources/deployments/{deploymentName}
- "Create a cancel?" -> POST /providers/Microsoft.Resources/deployments/{deploymentName}/cancel
- "Create a validate?" -> POST /providers/Microsoft.Resources/deployments/{deploymentName}/validate
- "Create a exportTemplate?" -> POST /providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate
- "List all deployments?" -> GET /providers/Microsoft.Resources/deployments/
- "Delete a deployment?" -> DELETE /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Update a deployment?" -> PUT /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Get deployment details?" -> GET /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Create a cancel?" -> POST /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel
- "Create a validate?" -> POST /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/validate
- "Create a exportTemplate?" -> POST /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate
- "List all deployments?" -> GET /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/
- "Delete a deployment?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Update a deployment?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Get deployment details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Create a cancel?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel
- "Create a validate?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/validate
- "Create a whatIf?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/whatIf
- "Create a exportTemplate?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate
- "List all deployments?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/
- "Delete a deployment?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Update a deployment?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Get deployment details?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Create a cancel?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel
- "Create a validate?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/validate
- "Create a whatIf?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/whatIf
- "Create a exportTemplate?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate
- "List all deployments?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/
- "Create a unregister?" -> POST /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/unregister
- "Create a register?" -> POST /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/register
- "List all providers?" -> GET /subscriptions/{subscriptionId}/providers
- "List all providers?" -> GET /providers
- "Get provider details?" -> GET /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}
- "Get provider details?" -> GET /providers/{resourceProviderNamespace}
- "List all resources?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/resources
- "Update a resourcegroup?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}
- "Delete a resourcegroup?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}
- "Get resourcegroup details?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}
- "Partially update a resourcegroup?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}
- "Create a exportTemplate?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/exportTemplate
- "List all resourcegroups?" -> GET /subscriptions/{subscriptionId}/resourcegroups
- "Create a moveResource?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/moveResources
- "Create a validateMoveResource?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/validateMoveResources
- "List all resources?" -> GET /subscriptions/{subscriptionId}/resources
- "Delete a provider?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}
- "Update a provider?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}
- "Partially update a provider?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}
- "Get provider details?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}
- "Delete a tagValue?" -> DELETE /subscriptions/{subscriptionId}/tagNames/{tagName}/tagValues/{tagValue}
- "Update a tagValue?" -> PUT /subscriptions/{subscriptionId}/tagNames/{tagName}/tagValues/{tagValue}
- "Update a tagName?" -> PUT /subscriptions/{subscriptionId}/tagNames/{tagName}
- "Delete a tagName?" -> DELETE /subscriptions/{subscriptionId}/tagNames/{tagName}
- "List all tagNames?" -> GET /subscriptions/{subscriptionId}/tagNames
- "Get operation details?" -> GET /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId}
- "List all operations?" -> GET /{scope}/providers/Microsoft.Resources/deployments/{deploymentName}/operations
- "Get operation details?" -> GET /providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId}
- "List all operations?" -> GET /providers/Microsoft.Resources/deployments/{deploymentName}/operations
- "Get operation details?" -> GET /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId}
- "List all operations?" -> GET /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations
- "Get operation details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId}
- "List all operations?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations
- "Get operation details?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations/{operationId}
- "List all operations?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations
- "Create a calculateTemplateHash?" -> POST /providers/Microsoft.Resources/calculateTemplateHash
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
