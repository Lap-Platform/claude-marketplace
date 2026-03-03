---
name: gallerymanagementclient
description: "GalleryManagementClient API skill. Use when working with GalleryManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# GalleryManagementClient
API version: 2015-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems -- verify access
3. POST /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems -- create first galleryItems

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems | Lists gallery items. |
| POST | /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems | Uploads a provider gallery item to the storage. |
| GET | /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName} | Get a specific gallery item. |
| DELETE | /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName} | Delete a specific gallery item. |

## Enhanced Skill Content
## Question Mapping

- "What gallery items are available in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems
- "List all marketplace items for subscription X" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems
- "How do I add a new gallery item?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems
- "Upload a gallery package to the marketplace" -> POST /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems
- "Register a new marketplace extension" -> POST /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems
- "Get details for a specific gallery item" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}
- "Does gallery item X exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}
- "Remove a gallery item from the marketplace" -> DELETE /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}
- "Delete gallery item X" -> DELETE /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}
- "Check if a gallery item was already deleted" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}
- "Replace an existing gallery item with a new version" -> POST /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems
- "How do I verify a gallery item uploaded correctly?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}
- "Clean up all gallery items I no longer need" -> GET /subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems + DELETE for each

## Response Tips

- **List (GET collection):** Returns 200 with an array of gallery items; check for empty arrays rather than errors when no items exist.
- **Create (POST):** 200 means the item was updated in place; 201 means a new item was created -- distinguish these to confirm whether you overwrote an existing entry.
- **Get (GET single):** 404 means the item does not exist -- use this for existence checks before delete or update operations.
- **Delete (DELETE):** 200 means the item was found and removed; 204 means the request succeeded but the item was already absent -- both are success states, do not retry on 204.

## Anomaly Flags

- **404 on GET single:** Surface immediately -- the gallery item name may be misspelled or the item was already deleted by another process.
- **200 vs 201 on POST:** Flag when a POST returns 200 instead of 201, as this means an existing item was overwritten rather than a new one created. Confirm this was intentional.
- **Empty list response:** If GET collection returns zero items for a subscription that previously had items, warn the user -- items may have been bulk-deleted or the subscription ID may be wrong.
- **OAuth token expiry:** Auth is OAuth2; surface any 401/403 responses proactively and prompt for token refresh before retrying.
- **204 on DELETE:** Inform the user the item was already gone -- no action was needed. This prevents confusion in cleanup scripts.

## Playbook

### 1. Publish a New Gallery Item

1. Prepare the gallery item URI payload as a map containing the package location.
2. Call POST `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems` with the `galleryItemUriPayload` body.
3. Check the response: 201 confirms creation, 200 means an existing item was replaced.
4. Verify by calling GET `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}` with the new item's name.

### 2. Check and Delete a Gallery Item

1. Call GET `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}` to confirm the item exists.
2. If 404, stop -- the item is already gone.
3. If 200, call DELETE `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}`.
4. Expect 200 (deleted) or 204 (already absent).

### 3. Audit All Gallery Items in a Subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems` to retrieve the full list.
2. For each item, call GET `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}` to fetch full details.
3. Record item names, versions, and metadata for your audit report.
4. Flag any items that return unexpected data or are missing expected fields.

### 4. Replace a Gallery Item with a New Version

1. Call GET `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems/{galleryItemName}` to confirm the current item exists and note its details.
2. Prepare the updated `galleryItemUriPayload` pointing to the new package.
3. Call POST `/subscriptions/{subscriptionId}/providers/microsoft.gallery.admin/galleryItems` with the new payload.
4. Confirm the response is 200 (replaced) rather than 201 (new item created under a different name).
5. Verify by fetching the item again with GET to confirm the update took effect.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
