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
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/checkNameAvailability | Checks that the storage account name is valid and is not already in use. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/locations/{location}/usages | Gets the current usage count and the limit for the resources of the location under the subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/skus | Lists the available SKUs supported by Microsoft.Storage for given subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage/storageAccounts | Lists all the storage accounts available under the subscription. Note that storage keys are not returned; use the ListKeys operation for this. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts | Lists all the storage accounts available under the given resource group. Note that storage keys are not returned; use the ListKeys operation for this. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | Deletes a storage account in Microsoft Azure. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | Returns the properties for the specified storage account including but not limited to name, SKU name, location, and account status. The ListKeys operation should be used to retrieve storage keys. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | The update operation can be used to update the SKU, encryption, access tier, or tags for a storage account. It can also be used to map the account to a custom domain. Only one custom domain is supported per storage account; the replacement/change of custom domain is not supported. In order to replace an old custom domain, the old value must be cleared/unregistered before a new value can be set. The update of multiple properties is supported. This call does not change the storage keys for the account. If you want to change the storage account keys, use the regenerate keys operation. The location and name of the storage account cannot be changed after creation. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName} | Asynchronously creates a new storage account with the specified parameters. If an account is already created and a subsequent create request is issued with different properties, the account properties will be updated. If an account is already created and a subsequent create or update request is issued with the exact same set of properties, the request will succeed. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListAccountSas | List SAS credentials of a storage account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListServiceSas | List service SAS credentials of a specific resource. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/failover | Failover request can be triggered for a storage account in case of availability issues. The failover occurs from the storage account's primary cluster to secondary cluster for RA-GRS accounts. The secondary cluster will become primary after failover. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/listKeys | Lists the access keys or Kerberos keys (if active directory enabled) for the specified storage account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Deletes the managementpolicy associated with the specified storage account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Gets the managementpolicy associated with the specified storage account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Sets the managementpolicy to the specified storage account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/regenerateKey | Regenerates one of the access keys or Kerberos keys for the specified storage account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/revokeUserDelegationKeys | Revoke user delegation keys. |

## Enhanced Skill Content
## Question Mapping

- "Is this storage account name available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage/checkNameAvailability
- "List all storage accounts in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/storageAccounts
- "List storage accounts in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts
- "Get details for a specific storage account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Create a new storage account" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Update storage account properties" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Delete a storage account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}
- "Get the access keys for a storage account" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/listKeys
- "Regenerate a storage account key" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/regenerateKey
- "Generate an account-level SAS token" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListAccountSas
- "Generate a service-level SAS token" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/ListServiceSas
- "What storage SKUs are available?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/skus
- "Check storage usage quotas for a region" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/locations/{location}/usages
- "Trigger a failover for a storage account" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/failover
- "Set up a lifecycle management policy" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}

## Response Tips

- **Account listings** (GET storageAccounts): Returns a `value` array; paginate using `nextLink` if present. Each item nests `properties` with `provisioningState`, `primaryEndpoints`, and `statusOfPrimary`.
- **Name availability** (POST checkNameAvailability): Returns `nameAvailable` (boolean), `reason`, and `message` -- check all three; `reason` distinguishes `AccountNameInvalid` from `AlreadyExists`.
- **Account create** (PUT): Returns 200 for synchronous completion or 202 for async -- on 202, poll the `Location` header URL until provisioning finishes.
- **Keys and SAS** (listKeys, ListAccountSas, ListServiceSas): Keys return in a `keys` array with `keyName`, `value`, and `permissions`. SAS returns `accountSasToken` or `serviceSasToken` as a query string.
- **Failover** (POST failover): Returns 202 accepted -- this is a long-running operation. Poll via `Azure-AsyncOperation` header; expect minutes of wait time.
- **Deletes** (DELETE): 200 means deleted, 204 means already gone -- treat both as success.
- **Management policies** (GET/PUT): Policy rules live inside `properties.policy.rules` array; each rule has `definition` with `filters` and `actions`.
- **Usages** (GET usages): Returns `value` array with `currentValue` and `limit` per quota; compare these to detect approaching limits.

## Anomaly Flags

- **Approaching storage quota**: Surface when `currentValue` exceeds 80% of `limit` in usage responses.
- **Provisioning failures**: Flag any storage account where `properties.provisioningState` is not `Succeeded` (e.g., `Failed`, `Canceled`, `Creating` stuck for extended periods).
- **Long-running operation stalls**: If a 202 response (create or failover) has not resolved after polling for more than 15 minutes, alert the user.
- **Secondary region status**: Flag when `statusOfSecondary` is `unavailable` -- indicates geo-replication health issues.
- **Key rotation overdue**: After listing keys, note if the user has not called regenerateKey recently -- suggest periodic rotation as a security hygiene measure.
- **Deprecated API version**: If a response returns `x-ms-deprecation` headers or the request uses a version older than `2019-04-01`, surface an upgrade notice.
- **Management policy conflicts**: Flag overlapping lifecycle rules (e.g., two rules targeting the same blob prefix with conflicting actions).
- **Failover implications**: Before triggering failover, warn that it makes the current primary the new secondary and may cause data loss for RA-GRS accounts with un-replicated writes.

## Playbook

### 1. Provision a New Storage Account

1. Check name availability: `POST /subscriptions/{subscriptionId}/providers/Microsoft.Storage/checkNameAvailability` with `accountName` and `type: "Microsoft.Storage/storageAccounts"`.
2. Confirm `nameAvailable` is `true`. If not, choose a different name based on the `reason` field.
3. Review available SKUs: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/skus` and pick an appropriate `name` (e.g., `Standard_LRS`).
4. Create the account: `PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}` with `parameters` including `sku`, `kind`, `location`, and `properties`.
5. If 202 returned, poll the `Location` or `Azure-AsyncOperation` URL until `provisioningState` is `Succeeded`.
6. Retrieve access keys: `POST .../listKeys` to get connection strings for the new account.

### 2. Rotate Storage Account Keys

1. List current keys: `POST .../storageAccounts/{accountName}/listKeys` to see `key1` and `key2` values.
2. Update all applications to use `key2` (the key you are not rotating).
3. Regenerate `key1`: `POST .../regenerateKey` with `keyName: "key1"`.
4. Confirm new keys: `POST .../listKeys` again to verify `key1` has changed.
5. Update applications to use the new `key1`, then repeat the cycle for `key2` if desired.

### 3. Set Up Blob Lifecycle Management

1. Get the current policy (if any): `GET .../managementPolicies/default`. A 404 means no policy exists yet.
2. Define lifecycle rules with filters (blobTypes, prefixMatch) and actions (tierToCool, tierToArchive, delete) with day thresholds.
3. Create or update the policy: `PUT .../managementPolicies/default` with the `properties.policy.rules` array.
4. Verify by reading the policy back: `GET .../managementPolicies/default` and confirm rules match expectations.

### 4. Initiate Geo-Failover

1. Get account details: `GET .../storageAccounts/{accountName}` and confirm `kind` supports failover (GPv2, Blob storage) and `statusOfSecondary` is `available`.
2. Warn the user: failover makes the secondary the new primary; any un-replicated writes to the original primary may be lost.
3. Trigger failover: `POST .../storageAccounts/{accountName}/failover`. Expect a 202 response.
4. Poll the `Azure-AsyncOperation` URL until completion -- this can take up to an hour.
5. Verify: `GET .../storageAccounts/{accountName}` and check that `primaryLocation` and `secondaryLocation` have swapped.

### 5. Audit and Clean Up Storage Accounts

1. List all accounts across the subscription: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage/storageAccounts`.
2. For each account, check `properties.provisioningState` and `properties.lastGeoFailoverTime` for health.
3. Check regional usage: `GET .../locations/{location}/usages` to identify regions near quota limits.
4. Identify unused accounts (no recent activity, no management policies, empty containers) and confirm with the user.
5. Delete confirmed accounts: `DELETE .../storageAccounts/{accountName}` and verify 200 or 204 response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
