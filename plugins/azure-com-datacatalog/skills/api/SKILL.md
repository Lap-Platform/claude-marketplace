---
name: azure-data-catalog-resource-provider
description: "Azure Data Catalog Resource Provider API skill. Use when working with Azure Data Catalog Resource Provider for providers, subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Data Catalog Resource Provider
API version: 2016-03-30

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DataCatalog/operations -- verify access

## Endpoints

6 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.DataCatalog/operations | Lists all the available Azure Data Catalog service operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs | List catalogs in Resource Group (GET Resources) |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName} | Create or Update Azure Data Catalog service (PUT Resource) |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName} | Get Azure Data Catalog service (GET Resources) |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName} | Delete Azure Data Catalog Service (DELETE Resource) |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName} | Update Azure Data Catalog Service (PATCH Resource) |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Azure Data Catalog?" -> GET /providers/Microsoft.DataCatalog/operations
- "List all data catalogs in my resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs
- "Create a new data catalog" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}
- "Get details of a specific data catalog" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}
- "Delete a data catalog" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}
- "Update properties on an existing catalog" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}
- "Replace an entire catalog configuration" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}
- "Does a specific catalog exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}
- "How do I rename or move a catalog?" -> DELETE old + PUT new (multi-step)
- "What permissions does the Data Catalog provider support?" -> GET /providers/Microsoft.DataCatalog/operations
- "Remove a catalog and confirm it is gone" -> DELETE then GET (multi-step)
- "Change the SKU or admin settings on my catalog" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}

## Response Tips

- **Operations (providers):** 200 returns an array of operation objects with `name`, `display` and `isDataAction` fields. No pagination -- the list is small and complete.
- **List catalogs:** 200 returns a `value` array of catalog resources. Check for an empty array rather than a 404 when no catalogs exist.
- **Create/Update (PUT):** 200 means the catalog already existed and was updated; 201 means a new catalog was created. Inspect the status code to know which occurred.
- **Get catalog:** 200 returns the full resource envelope with `id`, `name`, `type`, `location`, `tags`, and nested `properties`.
- **Delete catalog:** 200 means deleted synchronously; 202 means deletion is in progress (check the `Location` or `Azure-AsyncOperation` header to poll); 204 means the catalog was already gone.
- **Patch catalog:** 200 returns the merged resource. Only fields included in the request body are changed; omitted fields are left untouched.

## Anomaly Flags

- **202 on DELETE:** Deletion is asynchronous. Surface the async operation URL and remind the user to poll until completion before assuming the resource is gone.
- **Repeated 409 Conflict:** Indicates a concurrent modification or a catalog name collision. Flag immediately and suggest retrying with a fresh GET to reconcile state.
- **Missing `api-version` query parameter:** All requests require `api-version=2016-03-30`. If a 400 response mentions api-version, surface the fix proactively.
- **OAuth token expiry:** 401 responses mid-workflow likely mean the bearer token expired. Flag and suggest re-authentication before retrying.
- **Stale API version (2016-03-30):** This is a legacy API version. If Azure returns deprecation headers (`Sunset`, `Deprecation`), surface them and recommend checking for a newer API version.
- **Empty catalog list vs. wrong resource group:** If listing returns an empty `value` array, confirm the subscriptionId and resourceGroupName are correct before assuming no catalogs exist.

## Playbook

### 1. Provision a New Data Catalog

1. Call GET /providers/Microsoft.DataCatalog/operations to confirm the provider is available in your subscription.
2. Call PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName} with the required `properties` body (location, SKU, admin list).
3. Check the response: 201 confirms creation, 200 means a catalog with that name already existed and was updated.
4. Call GET on the same catalog path to verify the final state matches expectations.

### 2. Update Catalog Configuration

1. Call GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName} to retrieve current properties.
2. Identify the fields to change (e.g., admins, enableAutomaticUnitAdjustment).
3. Call PATCH on the same path with only the changed fields in the request body.
4. Confirm the 200 response contains the merged configuration.

### 3. Safely Delete a Catalog

1. Call GET on the catalog to confirm it exists and capture its current state for reference.
2. Call DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs/{catalogName}.
3. If 200: deletion is complete. If 202: extract the async operation URL from the response headers and poll until the operation completes. If 204: the catalog was already deleted.
4. Call GET on the catalog path to confirm a 404, verifying removal.

### 4. Audit All Catalogs in a Resource Group

1. Call GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataCatalog/catalogs to list all catalogs.
2. For each catalog in the `value` array, inspect `properties` for admin configuration, SKU tier, and provisioning state.
3. Flag any catalog with a `provisioningState` other than `Succeeded` or with an unexpected SKU.
4. Optionally call GET /providers/Microsoft.DataCatalog/operations to cross-reference which operations the current identity is permitted to perform.

### 5. Replace a Catalog (Recreate with New Settings)

1. Call GET on the existing catalog to capture its current configuration.
2. Call DELETE to remove the catalog. Wait for completion (handle 202 async if needed).
3. Call PUT with the same catalog name but updated `properties` to recreate it with new settings.
4. Verify the 201 response and confirm the new configuration with a follow-up GET.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
