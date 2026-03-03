---
name: computemanagementconvenienceclient
description: "ComputeManagementConvenienceClient API skill. Use when working with ComputeManagementConvenienceClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ComputeManagementConvenienceClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} | Create a named template deployment using a template. |

## Enhanced Skill Content
## Question Mapping

- "How do I deploy a resource to Azure?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "How do I create a new ARM deployment?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "How do I update an existing deployment?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "How do I deploy a VM to a resource group?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "How do I provision infrastructure in Azure using a template?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "How do I redeploy resources after a failure?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "How do I pass parameters to an ARM template deployment?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} (use `parameters` body)
- "How do I deploy resources to a specific subscription?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}
- "Can I create a deployment with a custom name?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} (set `deploymentName` path param)
- "How do I target a specific API version for deployments?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName} (set `api-version` query param to `2015-11-01`)
- "What fields are required to create a deployment?" -> PUT requires `resourceGroupName`, `deploymentName`, `api-version`, and `subscriptionId`

## Response Tips

- **Deployments (PUT):** A 200 response means the deployment was updated in place; a 201 means a new deployment was created. Both return the deployment resource object. Check `properties.provisioningState` for async status -- values include `Accepted`, `Running`, `Succeeded`, and `Failed`. Long-running operations return a `Location` or `Azure-AsyncOperation` header for polling.

## Anomaly Flags

- **201 vs 200 distinction:** Surface whether the deployment was newly created (201) or updated (200) so the user knows if they overwrote an existing deployment.
- **Provisioning state not Succeeded:** If the response body contains `properties.provisioningState` set to `Failed` or `Canceled`, flag immediately with the error details from `properties.error`.
- **Async operation headers:** If the response includes `Azure-AsyncOperation` or `Location` headers, alert the user that the deployment is long-running and provide the polling URL.
- **API version mismatch:** If the user omits or misconfigures `api-version`, the error response will reference supported versions -- surface these clearly.
- **Deprecated API version:** Version `2015-11-01` is legacy. Flag that newer API versions (2021-04-01+) offer more features and recommend upgrading unless there is a specific compatibility requirement.
- **Throttling (429):** Azure Resource Manager enforces per-subscription write limits. If a 429 response or `Retry-After` header appears, surface the wait time and suggest batching deployments.

## Playbook

### 1. Create a New ARM Template Deployment

1. Identify your `subscriptionId` and `resourceGroupName`.
2. Choose a unique `deploymentName` for tracking.
3. Build the request body with `properties.template` (inline ARM template) or `properties.templateLink` (URL to template), plus `properties.parameters` for template inputs.
4. Set `api-version=2015-11-01` as a query parameter.
5. Send PUT to `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}`.
6. Check the response: 201 confirms creation. Inspect `properties.provisioningState` for progress.
7. If async, poll the URL in the `Azure-AsyncOperation` header until state is `Succeeded` or `Failed`.

### 2. Update an Existing Deployment

1. Use the same `deploymentName` as the deployment you want to update.
2. Modify the `parameters` body with updated template or parameter values.
3. Send the PUT request -- a 200 response confirms the update was applied.
4. Verify `properties.provisioningState` reaches `Succeeded`.

### 3. Recover from a Failed Deployment

1. Review the failed deployment's error by checking `properties.error` in the response or by examining Azure portal logs.
2. Fix the template or parameters that caused the failure.
3. Resubmit the PUT with the same `deploymentName` and corrected body.
4. Monitor `provisioningState` until it resolves to `Succeeded`.
5. If throttled (429), wait for the duration in the `Retry-After` header before retrying.

### 4. Deploy Across Multiple Resource Groups

1. For each target resource group, prepare a separate PUT request with the appropriate `resourceGroupName`.
2. Use distinct `deploymentName` values to track each deployment independently.
3. Send requests in parallel where possible, but stay within Azure's per-subscription write throttle limits (800 deployments per resource group).
4. Collect all responses and verify each `provisioningState` reaches `Succeeded`.
5. If any deployment fails, address it individually using the recovery playbook above.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
