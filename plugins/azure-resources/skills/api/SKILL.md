---
name: resourcemanagementclient
description: "ResourceManagementClient API skill. Use when working with ResourceManagementClient for providers, subscriptions, {resourceId}. Covers 62 endpoints."
version: 1.0.0
generator: lapsh
---

# ResourceManagementClient
API version: 2019-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Resources/operations -- verify access
3. POST /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel -- create first cancel

## Endpoints

62 endpoints across 3 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/ | Get all the deployments for a management group. |
| DELETE | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| HEAD | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources at management group scope. |
| POST | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |
| GET | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| POST | /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| POST | /providers/Microsoft.Resources/calculateTemplateHash | Calculate the hash of the given template. |
| GET | /providers/Microsoft.Resources/operations | Lists all of the available Microsoft.Resources REST API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers | Gets all resource providers for a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/ | Get all the deployments for a subscription. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| HEAD | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources at subscription scope. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| GET | /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace} | Gets the specified resource provider. |
| POST | /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/register | Registers a subscription with a resource provider. |
| POST | /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/unregister | Unregisters a subscription from a resource provider. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/resources | Get all the resources for a resource group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/moveResources | Moves resources from one resource group to another resource group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/validateMoveResources | Validates whether resources can be moved from one resource group to another resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups | Gets all the resource groups for a subscription. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Deletes a resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Gets a resource group. |
| HEAD | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Checks whether a resource group exists. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Updates a resource group. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName} | Creates or updates a resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations | Gets all deployments operations for a deployment. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations/{operationId} | Gets a deployments operation. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/exportTemplate | Captures the specified resource group as a template. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/ | Get all the deployments for a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Deletes a deployment from the deployment history. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Gets a deployment. |
| HEAD | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Checks whether the deployment exists. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Deploys resources to a resource group. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel | Cancels a currently running template deployment. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate | Exports the template used for specified deployment. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/validate | Validates whether the specified template is syntactically correct and will be accepted by Azure Resource Manager.. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Deletes a resource. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Gets a resource. |
| HEAD | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Checks whether a resource exists. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Updates a resource. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName} | Creates a resource. |
| GET | /subscriptions/{subscriptionId}/resources | Get all the resources in a subscription. |
| GET | /subscriptions/{subscriptionId}/tagNames | Gets the names and values of all resource tags that are defined in a subscription. |
| DELETE | /subscriptions/{subscriptionId}/tagNames/{tagName} | Deletes a tag from the subscription. |
| PUT | /subscriptions/{subscriptionId}/tagNames/{tagName} | Creates a tag in the subscription. |
| DELETE | /subscriptions/{subscriptionId}/tagNames/{tagName}/tagValues/{tagValue} | Deletes a tag value. |
| PUT | /subscriptions/{subscriptionId}/tagNames/{tagName}/tagValues/{tagValue} | Creates a tag value. The name of the tag must already exist. |

### {resourceId}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{resourceId} | Deletes a resource by ID. |
| GET | /{resourceId} | Gets a resource by ID. |
| HEAD | /{resourceId} | Checks by ID whether a resource exists. |
| PATCH | /{resourceId} | Updates a resource by ID. |
| PUT | /{resourceId} | Create a resource by ID. |

## Enhanced Skill Content
## Question Mapping

- "List all deployments in a management group?" -> GET /providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/
- "What deployments exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/
- "List deployments in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/
- "Get details of a specific deployment?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Does a deployment exist?" -> HEAD /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Create or update a deployment in a resource group?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Cancel a running deployment?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/cancel
- "Export a deployment template?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/exportTemplate
- "Validate a deployment template before deploying?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}/validate
- "List all resource groups in a subscription?" -> GET /subscriptions/{subscriptionId}/resourcegroups
- "Move resources between resource groups?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{sourceResourceGroupName}/moveResources
- "Register a resource provider for my subscription?" -> POST /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/register
- "What operations happened during a deployment?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/deployments/{deploymentName}/operations
- "Get a resource by its full resource ID?" -> GET /{resourceId}
- "Calculate the hash of an ARM template?" -> POST /providers/Microsoft.Resources/calculateTemplateHash

## Response Tips

- **Deployment lists**: Paginated via `nextLink` in response body; follow it until absent. Use `$filter` (OData) and `$top` to limit results server-side.
- **Deployment details (GET/PUT)**: Response includes nested `properties` object with `provisioningState`, `outputs`, `dependencies`, and `template` -- check `provisioningState` for terminal states (`Succeeded`, `Failed`, `Canceled`).
- **HEAD endpoints**: Return no body -- 204 means the resource exists, 404 means it does not. Use these for cheap existence checks instead of full GETs.
- **Async operations (DELETE, PUT, move)**: 202 means accepted but not complete -- poll the `Location` or `Azure-AsyncOperation` header URL until the operation finishes.
- **Validation (POST .../validate)**: 200 means valid, 400 returns structured error details in `error.details[]` with per-resource failure reasons.
- **Resource groups**: GET returns `id`, `name`, `location`, `tags`, and `properties.provisioningState`. PATCH merges tags -- send only changed tags, not the full set.
- **Generic resource endpoints (/{resourceId})**: Require `api-version` as a query param matching the resource provider's version, not the ARM version.

## Anomaly Flags

- **`provisioningState` stuck in non-terminal state**: Surface when a deployment stays in `Running`, `Accepted`, or `Deleting` for longer than expected -- it may be hung.
- **202 without polling headers**: If a DELETE or PUT returns 202 but no `Location` or `Azure-AsyncOperation` header, flag it -- the client has no way to track completion.
- **Validation returns 400**: Proactively display the full `error.details[]` array -- individual resource errors are buried in nested objects and easy to miss.
- **409 on validateMoveResources**: Indicates a resource lock or policy conflict blocking the move -- surface the `error.code` (e.g., `ScopeLocked`, `PolicyViolation`) before the user attempts the actual move.
- **$top silently capped**: Azure may return fewer results than `$top` requests without indicating truncation; if the response includes `nextLink` despite a small `$top`, flag that more pages exist.
- **api-version mismatch**: The spec uses `2019-05-01` globally, but generic resource endpoints (`/{resourceId}`) need the resource provider's own api-version -- flag if the user passes the wrong one.
- **204 on DELETE**: Could mean "deleted" or "already didn't exist" -- surface which case it is when the user may care about idempotency.
- **Unregistered provider**: If a deployment fails with `MissingSubscriptionRegistration`, proactively suggest the register endpoint.

## Playbook

### 1. Deploy an ARM Template to a Resource Group

1. Validate the template first: `POST /subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.Resources/deployments/{name}/validate` with the deployment parameters body.
2. If validation returns 200, create the deployment: `PUT /subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.Resources/deployments/{name}` with the same parameters.
3. If PUT returns 201, the deployment is in progress. Poll with `GET /subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.Resources/deployments/{name}` until `properties.provisioningState` is `Succeeded` or `Failed`.
4. If failed, inspect deployment operations: `GET .../deployments/{name}/operations` to find which resource caused the failure.
5. Export the final template for auditing: `POST .../deployments/{name}/exportTemplate`.

### 2. Move Resources Between Resource Groups

1. Validate the move: `POST /subscriptions/{sub}/resourceGroups/{source}/validateMoveResources` with `{ "resources": [...ids], "targetResourceGroup": "/subscriptions/{sub}/resourceGroups/{target}" }`.
2. Poll the 202 response's `Location` header until it returns 204 (valid) or 409 (conflict).
3. If valid, execute the move: `POST /subscriptions/{sub}/resourceGroups/{source}/moveResources` with the same body.
4. Poll the 202 response until 204 -- moves can take several minutes.
5. Verify by listing resources in the target group: `GET /subscriptions/{sub}/resourceGroups/{target}/resources`.

### 3. Set Up a New Resource Group with Tags

1. Check if the resource group exists: `HEAD /subscriptions/{sub}/resourcegroups/{rg}` -- 204 means it exists, 404 means it does not.
2. Create or update: `PUT /subscriptions/{sub}/resourcegroups/{rg}` with `{ "location": "eastus", "tags": { "env": "prod", "team": "platform" } }`.
3. Confirm creation: response 201 means newly created, 200 means updated in place.
4. To add tags later without overwriting: `PATCH /subscriptions/{sub}/resourcegroups/{rg}` with only the new tags in the body.

### 4. Register a Resource Provider and Deploy

1. List available providers: `GET /subscriptions/{sub}/providers` to find the namespace.
2. Check registration state: `GET /subscriptions/{sub}/providers/{namespace}` and inspect `registrationState`.
3. If not registered: `POST /subscriptions/{sub}/providers/{namespace}/register`.
4. Poll the provider GET endpoint until `registrationState` is `Registered`.
5. Proceed with deployment as in Playbook 1.

### 5. Clean Up a Failed Deployment

1. Cancel the deployment if still running: `POST .../deployments/{name}/cancel` -- returns 204 on success.
2. Review what happened: `GET .../deployments/{name}/operations` with `$top=100` to see all operations.
3. Inspect each failed operation's `properties.statusMessage` for root cause.
4. Delete the failed deployment record: `DELETE .../deployments/{name}` -- returns 202 (async deletion) or 204 (already gone).
5. Fix the template issues and redeploy with a new deployment name.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
