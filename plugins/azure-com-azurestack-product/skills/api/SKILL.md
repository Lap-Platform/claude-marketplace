---
name: azurestack-azure-bridge-client
description: "AzureStack Azure Bridge Client API skill. Use when working with AzureStack Azure Bridge Client for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureStack Azure Bridge Client
API version: 2017-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/listDetails -- create first listDetails

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products | Returns a list of products. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName} | Returns the specified product. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/listDetails | Returns the extended properties of a product. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/listProducts | Returns a list of products. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/getProducts | Returns a list of products. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/getProduct | Returns the specified product. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/uploadProductLog | Returns the specified product. |

## Enhanced Skill Content
## Question Mapping

- "What products are available in my AzureStack registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products
- "Show me details for a specific AzureStack product" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}
- "What are the extended details of an AzureStack marketplace product?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/listDetails
- "List all product variants for a given device configuration" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/listProducts
- "Which products are compatible with my device configuration?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/getProducts
- "Get a single product scoped to my device configuration" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/getProduct
- "How do I upload a product log for troubleshooting?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/products/{productName}/uploadProductLog
- "How do I enumerate everything in my AzureStack marketplace?" -> GET .../products (then iterate with nextLink pagination)
- "What is the difference between listProducts and getProducts for a product?" -> POST .../listProducts returns a collection filtered by device config; POST .../getProducts returns the same but may include additional platform metadata
- "How do I check if a specific product exists before downloading?" -> GET .../products/{productName} and check for 404
- "How do I audit marketplace activity by uploading logs?" -> POST .../uploadProductLog with marketplaceProductLogUpdate body
- "Can I filter products by device hardware profile?" -> POST .../listProducts or POST .../getProducts with deviceConfiguration in the request body

## Response Tips

- **Product listings** (GET .../products): Returns a paginated array with a `nextLink` property; keep following `nextLink` until it is absent to retrieve all pages.
- **Single product** (GET .../products/{productName}): Returns a flat resource object; check `properties.productKind` and `properties.compatibility` for deployment eligibility.
- **Detail/list POST endpoints** (listDetails, listProducts, getProducts, getProduct): These return 200 even on empty results; always check the `value` array length rather than relying on status code alone.
- **Upload log** (uploadProductLog): Returns 200 on success with no meaningful body; treat any non-200 as a failure and inspect the `error.code` and `error.message` fields in the JSON response.
- **Error responses**: Follow standard Azure error format -- look for `error.code` (string) and `error.details[]` for nested validation failures.

## Anomaly Flags

- **404 on product name**: Surface immediately -- the product may have been delisted or the registration name is incorrect; suggest verifying with the list endpoint first.
- **Throttling (429)**: Azure ARM uses per-subscription rate limits; surface the `Retry-After` header value and recommend exponential backoff.
- **Stale API version**: This spec targets `2017-06-01`; if responses include `x-ms-deprecation` headers or documentation references newer api-versions, flag that the client should upgrade.
- **Empty product lists**: If GET .../products returns zero results, proactively check whether the registration name and resource group are correct -- an empty marketplace usually indicates misconfiguration.
- **Missing deviceConfiguration**: When calling listProducts/getProducts/getProduct without `deviceConfiguration`, results may be unfiltered and overly broad; warn the user if they omit it.
- **Large pagination depth**: If more than 5 pages are returned when listing products, flag the count so the user can narrow scope or apply filters.

## Playbook

### 1. Enumerate All Marketplace Products

1. Call GET .../products to retrieve the first page of products.
2. Read the `nextLink` property from the response.
3. If `nextLink` is present, call GET on that URL to fetch the next page.
4. Repeat until `nextLink` is absent.
5. Aggregate all `value[]` arrays into a single product list.

### 2. Inspect a Product Before Deployment

1. Call GET .../products/{productName} to retrieve the product resource.
2. Check `properties.compatibility` to confirm it matches your AzureStack stamp version.
3. Call POST .../listDetails with the product name to get extended metadata (download URIs, dependencies).
4. Review the `galleryItemIdentity` and `productKind` fields to confirm the resource type.

### 3. Get Device-Specific Product Information

1. Prepare a `deviceConfiguration` object describing the target hardware (CPU family, memory, storage).
2. Call POST .../getProduct with both `productName` and `deviceConfiguration` in the body.
3. Inspect the response for device-specific download links and compatibility notes.
4. If you need all compatible products (not just one), use POST .../getProducts instead for a filtered collection.

### 4. Upload Product Logs for Support

1. Collect the marketplace product log from the AzureStack stamp.
2. Construct a `marketplaceProductLogUpdate` object containing the log payload.
3. Call POST .../uploadProductLog with the product name and log body.
4. Confirm a 200 response; any non-200 indicates the upload failed.
5. Reference the product name and timestamp when opening a support ticket.

### 5. Verify Registration Health

1. Call GET .../products to confirm the registration returns data (non-empty `value[]`).
2. Pick a known product name and call GET .../products/{productName} to verify individual lookups work.
3. Call POST .../listDetails on the same product to confirm extended metadata is accessible.
4. If any step returns 404 or an empty result, the registration may be expired or misconfigured -- check the registration resource in the Azure portal.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
