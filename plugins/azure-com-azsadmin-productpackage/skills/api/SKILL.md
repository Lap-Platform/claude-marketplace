---
name: deploymentadminclient
description: "DeploymentAdminClient API skill. Use when working with DeploymentAdminClient for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages | Returns an array of product packages. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId} | Retrieves the specific product package details. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId} | Creates a new product package. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId} | Deletes a product package. |

## Enhanced Skill Content


## Question Mapping

- "What product packages are available in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages
- "List all deployment packages for subscription X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages
- "Get details about a specific product package" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "What's the status of package {packageId}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Create a new product package" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Update an existing product package" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Deploy a package with specific parameters" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Remove a product package from my subscription" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Delete package {packageId}" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Does a specific package exist in my deployment?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Replace the configuration of a product package" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
- "Clean up unused deployment packages" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId} (per package)

## Response Tips

- **List (GET collection):** 200 returns an array of package objects; check for `value` wrapper and `nextLink` for pagination in Azure-style responses.
- **Get single (GET by ID):** 200 returns the full package resource; a 404 means the package does not exist.
- **Create/Update (PUT):** 200 means completed synchronously; 202 means the operation is accepted and processing asynchronously -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Delete (DELETE):** 200 means deleted successfully; 204 means the resource was already gone (idempotent) -- both are success states.

## Anomaly Flags

- **202 on PUT**: The operation is long-running. Surface the async operation URL and remind the user to poll for completion status.
- **204 on DELETE**: The package was already absent. Flag this if the user expected the package to exist, as it may indicate a stale reference or prior deletion.
- **OAuth2 token expiry**: Surface proactively if repeated 401 responses occur -- the bearer token likely needs refresh.
- **Throttling (429)**: Azure ARM APIs enforce rate limits per subscription. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.
- **Missing required body on PUT**: If `ProductPackageParameters` map is empty or omitted, expect a 400. Flag the omission before sending the request.
- **Subscription-level errors (403)**: May indicate the Deployment Admin resource provider is not registered on the subscription. Surface a suggestion to run `az provider register --namespace Microsoft.Deployment.Admin`.

## Playbook

### 1. Inventory All Product Packages

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages
2. Parse the `value` array from the response
3. If `nextLink` is present, follow it to retrieve additional pages
4. Compile the full list of package IDs and their statuses

### 2. Deploy a New Product Package

1. Choose a `packageId` for the new package
2. Construct the `ProductPackageParameters` map with required configuration
3. Call PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
4. If 200: deployment completed -- verify by calling GET on the same package
5. If 202: extract the async operation URL from response headers and poll until the operation reaches a terminal state (Succeeded/Failed)

### 3. Update an Existing Package

1. Call GET on the specific package to retrieve its current configuration
2. Modify the desired fields in the `ProductPackageParameters` map
3. Call PUT with the updated parameters (PUT is a full replace, not a patch)
4. Handle 200 (immediate) or 202 (async) as in the deploy playbook
5. Call GET again to confirm the updated state

### 4. Remove a Product Package

1. Call GET on the package to confirm it exists and note any dependencies
2. Call DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
3. If 200: package deleted successfully
4. If 204: package was already absent -- no action needed
5. Optionally call GET on the collection to verify the package no longer appears

### 5. Check If a Package Exists Before Acting

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}
2. If 200: package exists -- proceed with update or other operations
3. If 404: package does not exist -- proceed with creation via PUT, or skip deletion


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
