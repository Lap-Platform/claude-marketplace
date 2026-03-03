---
name: azurebridgeadminclient
description: "AzureBridgeAdminClient API skill. Use when working with AzureBridgeAdminClient for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureBridgeAdminClient
API version: 2016-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}/download -- create first download

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products | Return product name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName} | Return product name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}/download | Downloads a product from azure marketplace. |

## Enhanced Skill Content
## Question Mapping

- "What products are available in my Azure Bridge activation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products
- "List all marketplace products for a specific activation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products
- "Show me the products registered under activation {name}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products
- "Get details about a specific product in Azure Bridge?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}
- "What metadata does product {name} have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}
- "Is a specific product available in my activation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}
- "Download a product from Azure Bridge?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}/download
- "Start downloading a marketplace product to my Azure Stack?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/products/{productName}/download
- "How do I sync a product from Azure Marketplace to my disconnected environment?" -> POST .../products/{productName}/download
- "Which products are currently downloaded or pending?" -> GET .../products (filter response by provisioning or download status)
- "Can I check if a product download completed?" -> GET .../products/{productName} (check status after POST download)
- "How do I find and download a specific marketplace extension?" -> GET .../products then POST .../products/{productName}/download

## Response Tips

- **Product listing (GET .../products):** Response is typically a paginated array with `value` and `nextLink`; follow `nextLink` to retrieve all pages. Each item includes product metadata and availability status.
- **Product detail (GET .../products/{productName}):** Returns a single product object with nested `properties` containing display name, description, publisher, offer details, and provisioning state.
- **Product download (POST .../download):** A 200 means the download completed synchronously; a 202 means the operation is long-running -- check the `Location` or `Azure-AsyncOperation` header to poll for completion. Do not assume success until the async operation resolves.
- **Errors:** Standard Azure error envelope `{ "error": { "code": "...", "message": "..." } }`. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `ActivationNotFound`.

## Anomaly Flags

- **202 Accepted on download:** Surface this immediately -- the download is asynchronous. Provide the polling URL from response headers and remind the user to check status.
- **Empty product list:** If GET .../products returns zero items, flag that the activation may not be connected to Azure Marketplace or the bridge registration is incomplete.
- **Product not found (404):** Confirm the product name matches exactly (case-sensitive) and that it exists under the specified activation.
- **Auth failures (401/403):** OAuth2 token may be expired or the service principal lacks `AzureBridge.Admin` role assignments on the resource group.
- **Throttling (429):** Azure ARM rate limits apply. Surface the `Retry-After` header value and pause before retrying.
- **Stale provisioning state:** If a product detail shows `provisioningState` stuck in `Downloading` or `Failed`, proactively suggest retrying the download or checking Azure Stack health.

## Playbook

### 1. Discover and Download a Product

1. Call GET .../products to list all available products under the activation
2. Review the list to find the desired product by display name or publisher
3. Call GET .../products/{productName} to confirm details and current status
4. Call POST .../products/{productName}/download to initiate the download
5. If response is 202, extract the polling URL from the `Location` header
6. Poll the async operation URL until status is `Succeeded` or `Failed`

### 2. Audit Available Products

1. Call GET .../products to retrieve the first page of products
2. Follow `nextLink` pagination until all products are collected
3. For each product, note the `provisioningState` and `productKind`
4. Compile a summary of available vs already-downloaded vs failed products
5. Flag any products with unexpected states for investigation

### 3. Retry a Failed Download

1. Call GET .../products/{productName} to check current `provisioningState`
2. Confirm the state is `Failed` (do not retry if `Downloading` is still in progress)
3. Call POST .../products/{productName}/download to re-initiate
4. Monitor the async operation via the 202 polling URL
5. If failure persists, check Azure Stack connectivity and activation health

### 4. Verify Activation Connectivity

1. Call GET .../products with the activation name to list products
2. If the response is empty or returns an activation error, the bridge may be disconnected
3. Call GET .../products/{knownProductName} for a product you expect to exist
4. A 404 confirms the activation is not syncing from Azure Marketplace
5. Remediate by verifying the activation resource exists and the bridge endpoint is reachable


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
