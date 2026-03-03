---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2019-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}/restore -- create first restore

## Endpoints

9 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices | List all file services in storage accounts |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/{FileServicesName} | Sets the properties of file services in storage accounts, including CORS (Cross-Origin Resource Sharing) rules. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/{FileServicesName} | Gets the properties of file services in storage accounts, including CORS (Cross-Origin Resource Sharing) rules. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares | Lists all shares. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName} | Creates a new share under the specified account as described by request body. The share resource includes metadata and properties for that share. It does not include a list of the files contained by the share. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName} | Updates share properties as specified in request body. Properties not mentioned in the request will not be changed. Update fails if the specified share does not already exist. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName} | Gets properties of a specified share. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName} | Deletes specified share under its account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}/restore | Restore a file share within a valid retention days if share soft delete is enabled |

## Enhanced Skill Content


## Question Mapping

- "What file services are available on my storage account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices
- "How do I configure file services for a storage account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/{FileServicesName}
- "What are the current file service properties?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/{FileServicesName}
- "How do I list all file shares in a storage account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares
- "How do I create a new file share?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}
- "How do I update an existing file share's quota or metadata?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}
- "What are the properties of a specific file share?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}
- "How do I delete a file share?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}
- "How do I restore a deleted file share?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/fileServices/default/shares/{shareName}/restore
- "Can I filter file shares by a specific condition?" -> GET .../shares with `$filter` query parameter
- "How do I page through a large list of file shares?" -> GET .../shares with `$maxpagesize` query parameter
- "How do I see share stats like usage?" -> GET .../shares/{shareName} with `$expand=stats`
- "Does a specific file share exist?" -> GET .../shares/{shareName} (check for 200 vs error)
- "How do I enable soft delete for file shares?" -> PUT .../fileServices/{FileServicesName} with delete retention policy in parameters

## Response Tips

- **File Services (list/get/put):** Response is a single resource object or a `value` array. Properties are nested under `properties` -- look there for CORS rules, delete retention policy, and protocol settings.
- **File Shares (list):** Returns a `value` array with `nextLink` for pagination. Use `$maxpagesize` to control page size and follow `nextLink` until null. The `$expand=deleted` option includes soft-deleted shares.
- **File Shares (CRUD):** PUT returns 201 on create, 200 on update. DELETE returns 200 on success, 204 if already gone. Share properties like quota, access tier, and metadata are nested under `properties`.
- **Restore:** Returns 200 on success. Requires the `deletedShare` body with the deleted share's version to restore.

## Anomaly Flags

- **204 on DELETE**: Share was already deleted or not found -- not an error, but worth noting to the user.
- **201 vs 200 on PUT share**: 201 means a new share was created; 200 means an existing one was updated. Surface this distinction.
- **Missing `nextLink` awareness**: If listing shares returns a `nextLink` and the agent stops after one page, flag incomplete results.
- **Soft-delete not enabled**: If a restore call fails, check whether the file service has `deleteRetentionPolicy.enabled` set to true.
- **Quota exceeded or throttling**: Azure ARM APIs return 429 with `Retry-After` header. Surface the retry delay and pause before retrying.
- **Deprecated API version**: If the response includes warnings about API version deprecation, flag it and suggest updating `api-version`.
- **`$expand` not applied**: If a user asks for stats but forgets `$expand=stats`, proactively suggest adding it.

## Playbook

### 1. Create and Configure a New File Share

1. GET `.../fileServices` to confirm file services exist on the storage account.
2. PUT `.../fileServices/default` with desired properties (e.g., enable soft delete with `deleteRetentionPolicy`).
3. PUT `.../shares/{shareName}` with `fileShare` body including `properties.shareQuota` and `properties.accessTier`.
4. GET `.../shares/{shareName}` to verify creation and confirm settings.

### 2. List and Inspect File Shares with Pagination

1. GET `.../shares` with optional `$maxpagesize` (e.g., 10) and `$filter` if narrowing results.
2. Parse the `value` array from the response.
3. If `nextLink` is present, GET that URL to fetch the next page.
4. Repeat until `nextLink` is null.
5. For detailed info on a specific share, GET `.../shares/{shareName}?$expand=stats`.

### 3. Update a File Share (Quota or Tier Change)

1. GET `.../shares/{shareName}` to retrieve current properties.
2. PATCH `.../shares/{shareName}` with only the fields to change (e.g., `properties.shareQuota: 500`).
3. GET `.../shares/{shareName}` to confirm the update took effect.

### 4. Delete and Restore a File Share

1. Verify soft delete is enabled: GET `.../fileServices/default` and check `properties.shareDeleteRetentionPolicy.enabled`.
2. DELETE `.../shares/{shareName}`. Expect 200 (success) or 204 (already deleted).
3. To restore: GET `.../shares?$expand=deleted` to find the deleted share version.
4. POST `.../shares/{shareName}/restore` with `deletedShare` body containing `deletedShareName` and `deletedShareVersion`.
5. GET `.../shares/{shareName}` to confirm the share is restored.

### 5. Configure File Service Properties (CORS, Soft Delete)

1. GET `.../fileServices/default` to review current configuration.
2. PUT `.../fileServices/default` with updated `parameters` body, for example:
   - Set `properties.shareDeleteRetentionPolicy.enabled: true` and `days: 14`.
   - Add CORS rules under `properties.cors.corsRules`.
3. GET `.../fileServices/default` to verify the configuration was applied.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
