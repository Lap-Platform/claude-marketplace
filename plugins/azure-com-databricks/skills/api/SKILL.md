---
name: databricksclient
description: "DatabricksClient API skill. Use when working with DatabricksClient for subscriptions, providers. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# DatabricksClient
API version: 2018-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Databricks/operations -- verify access

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName} | Gets the workspace. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName} | Deletes the workspace. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName} | Creates a new workspace. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName} | Updates a workspace. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces | Gets all the workspaces within a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Databricks/workspaces | Gets all the workspaces within a subscription. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Databricks/operations | Lists all of the available RP operations. |

## Enhanced Skill Content
## Question Mapping

- "What are the details of my Databricks workspace?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Get the configuration of a specific workspace" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Delete a Databricks workspace" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Remove a workspace from my resource group" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Create a new Databricks workspace" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Deploy a Databricks workspace in a resource group" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Update properties on an existing workspace" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "Change the tags on my Databricks workspace" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName}
- "List all Databricks workspaces in a resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces
- "Show every workspace in my resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces
- "List all Databricks workspaces in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Databricks/workspaces
- "How many Databricks workspaces do I have across all resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Databricks/workspaces
- "What operations are available for the Databricks resource provider?" -> GET /providers/Microsoft.Databricks/operations
- "Which API actions can I perform on Databricks resources?" -> GET /providers/Microsoft.Databricks/operations

## Response Tips

- **Workspace GET/PUT/PATCH (single):** Response is a Workspace object with `properties.provisioningState` indicating deployment status -- check for `Succeeded`, `Failed`, `Deleting`, `Accepted`, or `Creating`.
- **Workspace DELETE:** 200/204 means completed immediately; 202 means deletion is async -- poll the resource URL until you get 404 to confirm removal.
- **Workspace PUT (create):** 200 means the workspace already existed and was updated; 201 means a new workspace was created -- both may return a provisioning state that requires polling.
- **Workspace list endpoints:** Response contains a `value` array of Workspace objects and may include a `nextLink` URL for pagination -- follow `nextLink` until absent to retrieve all results.
- **Operations list:** Returns a `value` array of available operations with `name`, `display`, and `isDataAction` fields -- useful for RBAC planning.

## Anomaly Flags

- **Provisioning stuck:** Surface a warning if `properties.provisioningState` stays in `Creating`, `Updating`, or `Deleting` for more than 10 minutes when polling.
- **202 Accepted without Location header:** Flag if a DELETE or PATCH returns 202 but no `Location` or `Azure-AsyncOperation` header -- the client has no URL to poll for completion.
- **Throttling (429):** Azure ARM returns 429 with a `Retry-After` header -- surface the wait time and remaining quota from `x-ms-ratelimit-remaining-subscription-reads`/`writes` headers.
- **Unexpected 409 Conflict:** Indicates a concurrent operation on the workspace -- flag it and suggest retrying after the active operation completes.
- **Deprecated api-version:** If the response includes a `Sunset` header or the error body mentions version deprecation, proactively warn and suggest upgrading to a newer API version.
- **Missing required parameters:** If `subscriptionId` or `resourceGroupName` is empty/placeholder, flag before sending the request to avoid a 400.

## Playbook

### 1. Provision a new Databricks workspace

1. Call GET /providers/Microsoft.Databricks/operations to confirm your principal has the `Microsoft.Databricks/workspaces/write` permission.
2. Call PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces/{workspaceName} with a `parameters` body including `location`, `sku`, and `properties.managedResourceGroupId`.
3. Check the response: 201 means creation started, 200 means an existing workspace was updated.
4. Poll the same GET endpoint until `properties.provisioningState` returns `Succeeded`.
5. Verify the workspace URL in `properties.workspaceUrl` is accessible.

### 2. Safely delete a workspace

1. Call GET on the workspace to confirm it exists and note its current `provisioningState`.
2. If `provisioningState` is not `Succeeded`, wait for any in-flight operation to complete before deleting.
3. Call DELETE on the workspace.
4. If 202 is returned, poll the workspace GET endpoint until you receive a 404 (deleted) or an error.
5. If 200 or 204 is returned, deletion is complete.

### 3. Audit all workspaces across a subscription

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Databricks/workspaces to list all workspaces.
2. Follow any `nextLink` in the response to paginate through all results.
3. For each workspace, inspect `properties.provisioningState`, `sku.name`, and `properties.workspaceUrl`.
4. Flag any workspaces in `Failed` or `Deleting` state for investigation.

### 4. Update workspace tags without redeployment

1. Call GET on the target workspace to retrieve its current configuration.
2. Call PATCH with a `parameters` body containing only the `tags` field with the desired key-value pairs.
3. If 200 is returned, the update applied immediately -- verify by reading the workspace again.
4. If 202 is returned, poll until `provisioningState` returns to `Succeeded`.

### 5. Compare workspaces across resource groups

1. List all resource groups in the subscription using the Azure Resource Management API.
2. For each resource group, call GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Databricks/workspaces.
3. Aggregate results and compare `sku.name`, `location`, and `properties` across workspaces.
4. Surface any inconsistencies in SKU tier or region placement.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
