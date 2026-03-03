---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2019-08-08-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete -- create first undelete

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts | Returns a list of storage accounts. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId} | Returns the requested storage account. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete | Undelete a deleted storage account with new account name if the a new name is provided. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/reclaimStorageCapacity | Start reclaim storage capacity on deleted storage objects. |

## Enhanced Skill Content
## Question Mapping

- "List all storage accounts in a location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts
- "How do I filter storage accounts by a specific property?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts with $filter
- "Get a summary of storage accounts instead of full details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts with summary
- "Get details for a specific storage account?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}
- "Look up a storage account by its ID?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}
- "Recover a deleted storage account?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete
- "Undelete a storage account with a new name?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete with newAccountName
- "Restore a storage account that was accidentally deleted?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId}/undelete
- "Reclaim unused storage capacity in a location?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/reclaimStorageCapacity
- "Free up storage space across a region?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/reclaimStorageCapacity
- "What storage accounts exist in my subscription for a given region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts
- "How do I check the state of a specific storage account before restoring it?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/storageAccounts/{accountId} then POST .../undelete

## Response Tips

- **Account listing (GET .../storageAccounts):** Response may be paginated via `nextLink`; follow it until absent. Use `summary` param to reduce payload size when you only need counts or basic metadata.
- **Account detail (GET .../storageAccounts/{accountId}):** Returns a single resource object with `properties` nested under the top-level resource envelope; check `properties.provisioningState` and `properties.accountStatus` for current state.
- **Undelete (POST .../undelete):** A 200 means immediate completion; a 202 means the operation is async -- check the `Location` or `Azure-AsyncOperation` header to poll for completion status.
- **Reclaim capacity (POST .../reclaimStorageCapacity):** Same 200/202 pattern as undelete; 202 responses include a polling URL. No request body is needed.

## Anomaly Flags

- **202 Accepted without polling URL:** If an async operation returns 202 but omits both `Location` and `Azure-AsyncOperation` headers, surface this -- the client cannot track completion.
- **Preview API version:** This API uses version `2019-08-08-preview`. Flag that preview APIs may change or be deprecated without notice; recommend checking for a GA version.
- **Undelete window expiration:** If an undelete call returns 404 or an error indicating the account is no longer recoverable, proactively note that Azure has a limited soft-delete retention window.
- **Rate limiting (429 responses):** Surface `Retry-After` header values immediately and pause further calls. Azure ARM typically throttles at the subscription level.
- **Reclaim capacity with no effect:** If reclaim returns 200 but subsequent account listings show no change in capacity, flag that reclaim only targets internally reclaimable resources and may have no visible impact.
- **Filter syntax errors:** A 400 on the listing endpoint with `$filter` likely means an OData syntax issue -- surface the filter string for the user to review.

## Playbook

### 1. Audit Storage Accounts in a Region

1. Call `GET .../storageAccounts` with the target `subscriptionId` and `location`.
2. If `nextLink` is present in the response, follow it repeatedly until all pages are retrieved.
3. For each account, inspect `properties.accountStatus` and `properties.provisioningState`.
4. Optionally pass `summary=true` for a lightweight overview first, then fetch full details only for accounts of interest.

### 2. Recover a Deleted Storage Account

1. Call `GET .../storageAccounts` with `$filter` targeting deleted or soft-deleted status to identify recoverable accounts.
2. Note the `accountId` of the account to restore.
3. Call `POST .../storageAccounts/{accountId}/undelete`. Optionally include `newAccountName` if the original name is now taken.
4. If the response is 202, extract the polling URL from the `Location` or `Azure-AsyncOperation` header and poll until the operation completes.
5. Verify recovery by calling `GET .../storageAccounts/{accountId}` and confirming `provisioningState` is `Succeeded`.

### 3. Reclaim Storage Capacity

1. Call `POST .../reclaimStorageCapacity` for the target location.
2. If the response is 202, poll the async operation URL until completion.
3. Call `GET .../storageAccounts` to verify the updated capacity state across accounts in that location.

### 4. Investigate a Specific Storage Account

1. Call `GET .../storageAccounts/{accountId}` with the known account ID.
2. Inspect `properties.provisioningState` for operational status.
3. Check `properties.primaryEndpoints` and `properties.accountType` for configuration details.
4. If the account appears deleted, proceed with the recovery playbook above.

### 5. Filtered Search for Problem Accounts

1. Call `GET .../storageAccounts` with a `$filter` expression targeting the desired condition (e.g., accounts over quota, specific account type, or specific status).
2. Page through results using `nextLink` if present.
3. For each flagged account, call `GET .../storageAccounts/{accountId}` to retrieve full details.
4. Take corrective action: undelete if deleted, or note the account for manual remediation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
