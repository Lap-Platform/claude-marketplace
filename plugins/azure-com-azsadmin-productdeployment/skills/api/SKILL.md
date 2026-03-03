---
name: deploymentadminclient
description: "DeploymentAdminClient API skill. Use when working with DeploymentAdminClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# DeploymentAdminClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/bootstrap -- create first bootstrap

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments | Invokes bootstrap action on the product deployment |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId} | Invokes bootstrap action on the product deployment |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/bootstrap | Invokes bootstrap action on the product deployment |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/deploy | Invokes deploy action on the product |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/remove | Invokes remove action on the product deployment |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/rotateSecrets | Invokes rotate secrets action on the product deployment |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/executeRunner | Invokes execute runner action on the product deployment |

## Enhanced Skill Content
## Question Mapping

- "What products are deployed in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments
- "Show me details for a specific product deployment" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}
- "How do I bootstrap a product before deploying it?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/bootstrap
- "Deploy a product to my Azure Stack environment" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/deploy
- "Remove a product deployment from my subscription" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/remove
- "Rotate secrets for a deployed product" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/rotateSecrets
- "Run a custom action against a product deployment" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId}/executeRunner
- "Is my product deployment still in progress?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments/{productId} (check provisioning state)
- "How do I do a full redeploy of a product?" -> POST .../bootstrap then POST .../deploy (two-step)
- "Can I remove a product and redeploy it cleanly?" -> POST .../remove then POST .../bootstrap then POST .../deploy
- "What parameters does executeRunner need?" -> POST .../executeRunner (requires `executeRunnerActionParameter` map in body)
- "How do I list all product IDs available for deployment?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productDeployments (extract productId from each item)

## Response Tips

- **List/Get endpoints (200):** Response is an Azure ARM resource or resource list; look for `value[]` array on list calls and `properties.provisioningState` on individual resources.
- **Async actions (202):** A 202 means the operation was accepted but not complete; check the `Location` or `Azure-AsyncOperation` header to poll for completion status.
- **Remove endpoint (204):** A 204 means the resource was already gone or successfully deleted with no content returned -- treat as success.
- **Error responses:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; surface the `code` and `message` fields directly.
- **All POST actions:** Even 200 responses may contain an intermediate provisioning state -- always check `properties.provisioningState` for terminal values (`Succeeded`, `Failed`, `Canceled`).

## Anomaly Flags

- **Long-running operation stuck:** If an async operation (202) has not reached a terminal state after polling for more than 15 minutes, surface a warning with the last known status.
- **Unexpected 200 on async endpoints:** Bootstrap, deploy, rotateSecrets, and executeRunner typically return 202; a 200 may indicate a no-op or idempotent repeat -- flag this if the user expected a fresh operation.
- **Remove returning 204 vs 200:** If the user explicitly requested removal and gets 204, clarify that the resource may have already been absent.
- **ProvisioningState: Failed:** Proactively surface failure details from `properties.error` whenever `provisioningState` is `Failed` on any GET or action response.
- **Missing executeRunnerActionParameter:** The executeRunner endpoint requires a body map; flag immediately if the user attempts to call it without parameters.
- **Authentication scope:** All endpoints require OAuth2; surface a clear message if a 401/403 is returned, suggesting the token may lack the `Microsoft.Deployment.Admin` resource provider permissions.

## Playbook

### 1. Deploy a New Product End-to-End

1. GET `.../productDeployments` to list available product deployments and confirm the target `productId` exists.
2. GET `.../productDeployments/{productId}` to check current state -- ensure it is not already mid-operation.
3. POST `.../productDeployments/{productId}/bootstrap` to initialize the product. Capture the `Azure-AsyncOperation` header.
4. Poll the async operation URL until `provisioningState` is `Succeeded`.
5. POST `.../productDeployments/{productId}/deploy` to execute the deployment. Capture the async header.
6. Poll until `provisioningState` is `Succeeded`. Confirm with a final GET on the product.

### 2. Rotate Secrets for a Running Deployment

1. GET `.../productDeployments/{productId}` to verify the product is in `Succeeded` state.
2. POST `.../productDeployments/{productId}/rotateSecrets` to initiate secret rotation.
3. If 202 is returned, poll the async operation URL until complete.
4. GET `.../productDeployments/{productId}` to confirm the product is still healthy after rotation.

### 3. Cleanly Remove and Redeploy a Product

1. GET `.../productDeployments/{productId}` to capture current configuration details.
2. POST `.../productDeployments/{productId}/remove` to tear down the deployment.
3. Poll until complete (or handle 204 as immediate success).
4. POST `.../productDeployments/{productId}/bootstrap` to re-initialize.
5. Poll until bootstrap completes, then POST `.../deploy` and poll again.
6. GET the product to verify `provisioningState` is `Succeeded`.

### 4. Execute a Custom Runner Action

1. Prepare the `executeRunnerActionParameter` map with the required key-value pairs for the action.
2. POST `.../productDeployments/{productId}/executeRunner` with the parameter map in the request body.
3. If 202, poll the async operation header URL until the action reaches a terminal state.
4. GET `.../productDeployments/{productId}` to verify the product state was not adversely affected.

### 5. Audit All Product Deployments

1. GET `.../productDeployments` to retrieve the full list of deployments in the subscription.
2. For each item in the `value[]` array, inspect `properties.provisioningState`.
3. Flag any deployments in `Failed` or non-terminal states.
4. For deployments in `Succeeded` state, optionally GET each by `productId` for detailed property inspection.
5. Compile a summary of product names, states, and any error details.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
