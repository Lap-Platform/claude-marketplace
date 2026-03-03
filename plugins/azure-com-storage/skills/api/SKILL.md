---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for providers, subscriptions. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2019-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Storage/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage/checkNameAvailability -- create first checkNameAvailability

## Endpoints

19 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Storage/operations | Lists all of the available Storage Rest API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/skus | Lists the available SKUs supported by Microsoft.Storage for given subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/checkNameAvailability | Checks that the storage account name is valid and is not already in use. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | Asynchronously creates a new storage account with the specified parameters. If an account is already created and a subsequent create request is issued with different properties, the account properties will be updated. If an account is already created and a subsequent create or update request is issued with the exact same set of properties, the request will succeed. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | Deletes a storage account in Microsoft Azure. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | Returns the properties for the specified storage account including but not limited to name, SKU name, location, and account status. The ListKeys operation should be used to retrieve storage keys. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | The update operation can be used to update the SKU, encryption, access tier, or tags for a storage account. It can also be used to map the account to a custom domain. Only one custom domain is supported per storage account; the replacement/change of custom domain is not supported. In order to replace an old custom domain, the old value must be cleared/unregistered before a new value can be set. The update of multiple properties is supported. This call does not change the storage keys for the account. If you want to change the storage account keys, use the regenerate keys operation. The location and name of the storage account cannot be changed after creation. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/storageAccounts | Lists all the storage accounts available under the subscription. Note that storage keys are not returned; use the ListKeys operation for this. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts | Lists all the storage accounts available under the given resource group. Note that storage keys are not returned; use the ListKeys operation for this. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/listKeys | Lists the access keys or Kerberos keys (if active directory enabled) for the specified storage account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/regenerateKey | Regenerates one of the access keys or Kerberos keys for the specified storage account. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/locations/{location}/usages | Gets the current usage count and the limit for the resources of the location under the subscription. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListAccountSas | List SAS credentials of a storage account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListServiceSas | List service SAS credentials of a specific resource. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/failover | Failover request can be triggered for a storage account in case of availability issues. The failover occurs from the storage account's primary cluster to secondary cluster for RA-GRS accounts. The secondary cluster will become primary after failover. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Gets the managementpolicy associated with the specified storage account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Sets the managementpolicy to the specified storage account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Deletes the managementpolicy associated with the specified storage account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/revokeUserDelegationKeys | Revoke user delegation keys. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Microsoft Storage?" -> GET /providers/Microsoft.Storage/operations
- "What storage SKUs can I use in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/skus
- "Is this storage account name available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage/checkNameAvailability
- "Create a new storage account" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Delete a storage account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Get details for a specific storage account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Update storage account settings" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "List all storage accounts in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/storageAccounts
- "List storage accounts in a resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts
- "Get the access keys for a storage account" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/listKeys
- "Rotate a storage account key" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/regenerateKey
- "How much storage quota am I using in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/locations/{location}/usages
- "Generate a shared access signature (SAS) for an account" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListAccountSas
- "Generate a service-level SAS token" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListServiceSas
- "Trigger a failover for a storage account" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/failover

## Response Tips

- **Operations/SKUs listing:** Results are returned as a `value` array; no pagination -- full list in a single response.
- **Account create (PUT) and failover (POST):** 202 means the operation is accepted but not complete -- poll the `Location` or `Azure-AsyncOperation` header URL until terminal state.
- **Account delete and management policy delete:** 204 means the resource was already gone; treat 200 and 204 both as success.
- **Name availability check:** Response contains `nameAvailable` (boolean) and `reason`/`message` when unavailable -- always check `reason` for `AccountNameInvalid` vs `AlreadyExists`.
- **List keys / regenerate key:** Response `keys` array contains objects with `keyName`, `value`, and `permissions` -- never log or persist key `value` in plaintext.
- **SAS generation:** Response contains `accountSasToken` or `serviceSasToken` as a query string fragment -- prepend `?` before appending to blob URLs.
- **Usages:** Each entry has `currentValue` and `limit` -- compute percentage to assess quota headroom.
- **Management policies:** The `properties.policy` object contains `rules` array -- each rule has `definition` with `filters` and `actions` sub-objects.
- **Account GET with $expand:** Use `$expand=geoReplicationStats` to include replication lag and status in the response; omit for faster responses.

## Anomaly Flags

- **202 Accepted on PUT or failover:** Long-running operation in progress -- surface the async operation URL and recommend polling until completion.
- **Name unavailability reason is `AccountNameInvalid`:** The chosen name violates naming rules (3-24 chars, lowercase alphanumeric only) -- flag before the user retries with the same pattern.
- **Storage quota usage above 80%:** When `currentValue / limit > 0.8` on any usage metric, proactively warn about approaching quota limits.
- **Key regeneration without connection string rotation:** After `regenerateKey`, surface a reminder that applications using the old key will lose access and need updated connection strings.
- **Failover on non-RA-GRS accounts:** Failover only works with geo-redundant replication -- flag if the account's `sku.name` does not include `RAGRS` or `GZRS`.
- **SAS token expiry:** When generating SAS tokens, flag if the requested `signedExpiry` exceeds 24 hours or has no explicit expiry set.
- **Management policy returning 204 on delete:** The policy was already absent -- surface this as an idempotent no-op rather than a successful deletion.
- **Revoke user delegation keys:** This invalidates all active user delegation SAS tokens -- flag the blast radius before executing.

## Playbook

### 1. Provision a New Storage Account

1. Check name availability: `POST /subscriptions/{id}/providers/Microsoft.Storage/checkNameAvailability` with `{"accountName": "mystorageacct", "type": "Microsoft.Storage/storageAccounts"}`.
2. If `nameAvailable` is false, adjust the name and retry step 1.
3. Create the account: `PUT /subscriptions/{id}/resourceGroups/{rg}/providers/Microsoft.Storage/storageAccounts/mystorageacct` with SKU, kind, and location in the request body.
4. If response is 202, poll the `Azure-AsyncOperation` header URL until `status` is `Succeeded`.
5. Retrieve the new account details: `GET /subscriptions/{id}/resourceGroups/{rg}/providers/Microsoft.Storage/storageAccounts/mystorageacct`.
6. Fetch access keys: `POST .../listKeys` and store them securely.

### 2. Rotate Access Keys with Zero Downtime

1. List current keys: `POST .../listKeys` -- note which key (`key1` or `key2`) your applications use.
2. Update all applications to use the alternate key (e.g., switch from `key1` to `key2`).
3. Regenerate the now-unused key: `POST .../regenerateKey` with `{"keyName": "key1"}`.
4. Verify by listing keys again to confirm the regenerated key has a new value.
5. Optionally, repeat the process in reverse to rotate the second key.

### 3. Set Up Lifecycle Management Policies

1. Get the current policy (if any): `GET .../managementPolicies/default` -- a 404 means no policy exists yet.
2. Define the policy rules (e.g., move blobs to cool tier after 30 days, delete after 365 days).
3. Apply the policy: `PUT .../managementPolicies/default` with the full policy object in the request body.
4. Verify by reading it back: `GET .../managementPolicies/default` and confirming the rules match.

### 4. Initiate Account Failover for Disaster Recovery

1. Confirm the account uses geo-redundant replication: `GET .../storageAccounts/{name}` and check `sku.name` includes `RAGRS` or `GZRS`.
2. Check replication status: use `$expand=geoReplicationStats` to verify `geoReplicationStats.status` is `Live` and review `lastSyncTime`.
3. Trigger failover: `POST .../failover` -- this returns 202.
4. Poll the async operation URL until the failover completes (can take up to an hour).
5. After completion, the secondary becomes the new primary -- verify with a fresh GET on the account.

### 5. Generate Scoped SAS Tokens for External Access

1. Determine scope: use `ListAccountSas` for account-wide access or `ListServiceSas` for a specific service (blob, file, queue, table).
2. Build the parameters: set `signedServices`, `signedPermissions`, `signedExpiry`, and `signedResourceTypes` as appropriate.
3. Call the corresponding POST endpoint with the parameters.
4. Extract the SAS token from the response (`accountSasToken` or `serviceSasToken`).
5. Construct the full URL: `https://{accountName}.blob.core.windows.net/{container}/{blob}?{sasToken}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
