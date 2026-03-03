---
name: azurebridgeadminclient
description: "AzureBridgeAdminClient API skill. Use when working with AzureBridgeAdminClient for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts | Get a list of downloaded products. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName} | Get a downloaded product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName} | Delete a downloaded product. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName} | Creates a downloaded product. |

## Enhanced Skill Content
## Question Mapping

- "What products have been downloaded for this activation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts
- "List all downloaded products in my Azure Bridge activation" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts
- "Get details about a specific downloaded product" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Is a particular product already downloaded in my activation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Remove a downloaded product from my activation" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Delete a marketplace product from Azure Bridge" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Download a new product to my activation" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Create or update a downloaded product entry" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "How do I replace a downloaded product with a newer version?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Which resource group contains my Azure Bridge products?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts
- "Check the provisioning state of a downloaded product" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}
- "Clean up unused downloaded products from my activation" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}/downloadedProducts/{productName}

## Response Tips

- **List endpoints (GET collection):** Response contains a `value` array of product objects; check for `nextLink` to handle pagination across large product catalogs.
- **Detail endpoints (GET single):** Returns a single product resource object; key fields are nested under `properties` (e.g., `properties.provisioningState`, `properties.productKind`).
- **Delete endpoints:** 200 means immediate deletion, 202 means deletion accepted and processing asynchronously (poll the `Location` or `Azure-AsyncOperation` header), 204 means the product was already gone -- all three are success cases.
- **Create/Update endpoints (PUT):** 200 means synchronous completion, 202 means the operation is long-running -- follow the `Azure-AsyncOperation` header URL to poll for completion status.

## Anomaly Flags

- **202 Accepted without completion:** Surface when PUT or DELETE returns 202 -- the agent should remind the user to poll the async operation URL and warn that the resource is in a transitional state.
- **Provisioning failures:** After a PUT, if the product's `properties.provisioningState` is anything other than `Succeeded` (e.g., `Failed`, `Canceled`), flag this immediately with the error details.
- **404 on GET single:** If a specific product lookup returns 404, proactively suggest listing all products to verify the exact product name and activation name.
- **Stale product catalog:** When listing products, flag if any items show a `provisioningState` of `Failed` or `Deleting` -- these may need manual cleanup.
- **Missing required body on PUT:** If a user attempts to create/update without the `downloadedProduct` body payload, intercept before sending and prompt for the required fields.
- **API version mismatch:** This spec targets `2016-01-01` -- flag if the user references newer features that may require a different api-version query parameter.

## Playbook

### 1. Inventory All Downloaded Products

1. Identify your `subscriptionId`, `resourceGroupName`, and `activationName`.
2. Call GET on the downloadedProducts collection endpoint.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it repeatedly until no more pages remain.
5. Compile the full list of product names and their provisioning states.

### 2. Download a New Marketplace Product

1. Call GET on the downloadedProducts collection to confirm the product is not already present.
2. Construct the `downloadedProduct` request body with the required product metadata.
3. Call PUT with the product name and the request body.
4. If the response is 200, the product is ready immediately.
5. If the response is 202, extract the `Azure-AsyncOperation` header URL and poll it at intervals until the status shows `Succeeded` or `Failed`.

### 3. Remove an Unwanted Product

1. Call GET on the specific product to confirm it exists and note its current state.
2. Call DELETE on the product endpoint.
3. If the response is 200 or 204, deletion is complete -- no further action needed.
4. If the response is 202, poll the async operation URL until the deletion finalizes.
5. Optionally call GET on the product to confirm it returns 404 (fully removed).

### 4. Update an Existing Downloaded Product

1. Call GET on the specific product to retrieve its current configuration.
2. Modify the relevant fields in the returned product object.
3. Call PUT with the updated `downloadedProduct` body.
4. Monitor the response: 200 means done, 202 means poll for completion.
5. Call GET again to verify the product reflects the updated values.

### 5. Audit and Clean Up Failed Products

1. Call GET on the downloadedProducts collection to list all products.
2. Filter results for any product where `properties.provisioningState` is `Failed`, `Canceled`, or `Deleting`.
3. For each problematic product, decide whether to retry (PUT with corrected config) or remove (DELETE).
4. Execute the chosen action for each product and track async operations.
5. Re-list all products to confirm the catalog is in a clean state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
