---
name: compute-admin-client
description: "Compute Admin Client API skill. Use when working with Compute Admin Client for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Compute Admin Client
API version: 2015-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage | Returns all platform images. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version} | Returns the requested platform image. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version} | Creates a platform image. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version} | Deletes a platform image matching publisher, offer, skus and version |

## Enhanced Skill Content


## Question Mapping

- "What platform images are available in my region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage
- "List all platform images for a specific location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage
- "Get details of a specific platform image version?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "What versions exist for a given publisher, offer, and SKU?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "How do I add a new platform image to the marketplace?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "How do I register a custom VM image for tenants?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "Update an existing platform image version?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "Remove a platform image from the marketplace?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "Delete a deprecated image version?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "Which publishers have images in my location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage
- "Can I replace a platform image by re-uploading it?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "How do I verify a platform image was created successfully?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}
- "How do I clean up unused platform images?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/platformImage/publishers/{publisher}/offers/{offer}/skus/{sku}/versions/{version}

## Response Tips

- **List (GET collection):** Returns an array of platform image objects. Check for a `value` wrapper array typical of Azure ARM responses. No pagination indicated in this API version.
- **Get detail (GET single):** Returns the full platform image resource including provisioning state. Inspect `properties.provisioningState` for readiness.
- **Create/Update (PUT):** Returns 200 (updated), 201 (created), or 202 (accepted/async). A 202 means the operation is long-running -- check the `Azure-AsyncOperation` or `Location` header to poll for completion.
- **Delete (DELETE):** Returns 200 on success. May also return 202 for async deletion or 204 if the resource was already removed.

## Anomaly Flags

- **202 Accepted on PUT:** The image creation is asynchronous. Surface this to the user and recommend polling the async operation URL from response headers until terminal state.
- **Preview API version (2015-12-01-preview):** This is a preview API. Flag that behavior may change and endpoints could be deprecated without standard lifecycle notices.
- **Missing required fields:** The PUT endpoint requires `offer`, `sku`, and `newImage` (map). Surface a clear error if any are omitted before making the request.
- **OAuth2 token expiration:** Auth is OAuth2-based. Proactively flag when tokens are near expiry or when 401 responses indicate a refresh is needed.
- **Inconsistent delete states:** If a DELETE returns 200 but a subsequent GET still returns the image, flag that deletion may be async or cached.
- **Deep path hierarchy:** The 5-level nesting (publisher/offer/sku/version) is error-prone. Flag if any path segment appears empty or malformed.

## Playbook

### 1. Add a New Platform Image to the Marketplace

1. List existing images with GET on the collection endpoint to confirm the image does not already exist
2. Construct the `newImage` map with the required image metadata (OS type, disk URI, publisher, offer, SKU, version)
3. Call PUT with the full publisher/offer/sku/version path and the `newImage` body
4. If the response is 202, extract the async operation URL from the `Azure-AsyncOperation` header
5. Poll the async URL until `provisioningState` reaches `Succeeded` or `Failed`
6. Verify by calling GET on the specific image version to confirm it is registered

### 2. Audit and Clean Up Deprecated Images

1. Call GET on the collection endpoint to list all platform images in the target location
2. Filter results by age, usage, or naming convention to identify candidates for removal
3. For each candidate, call GET on the specific version to confirm its details and provisioning state
4. Call DELETE on each confirmed deprecated image
5. Re-list images with GET to verify the deletions took effect

### 3. Rotate a Platform Image Version

1. Call GET on the specific existing image version to capture its current configuration
2. Call PUT with the new version path and updated `newImage` body (new disk URI, updated metadata)
3. Wait for 200/201 or poll the 202 async operation to completion
4. Verify the new version with GET on the new version path
5. Call DELETE on the old version to remove it from the marketplace
6. Confirm removal by listing images via GET on the collection endpoint

### 4. Inventory All Images Across Locations

1. Determine the list of target locations for the subscription
2. For each location, call GET on the collection endpoint to retrieve all platform images
3. Aggregate results, noting publisher, offer, SKU, and version for each entry
4. Cross-reference against expected images to identify gaps or unexpected entries
5. Flag any images in preview or failed provisioning states for follow-up


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
