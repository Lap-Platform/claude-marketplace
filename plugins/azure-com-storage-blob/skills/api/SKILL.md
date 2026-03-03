---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 16 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/setLegalHold -- create first setLegalHold

## Endpoints

16 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices | List blob services of storage account. It returns a collection of one object named default. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/{BlobServicesName} | Sets the properties of a storage account’s Blob service, including properties for Storage Analytics and CORS (Cross-Origin Resource Sharing) rules. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/{BlobServicesName} | Gets the properties of a storage account’s Blob service, including properties for Storage Analytics and CORS (Cross-Origin Resource Sharing) rules. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers | Lists all containers and does not support a prefix like data plane. Also SRP today does not return continuation token. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName} | Creates a new container under the specified account as described by request body. The container resource includes metadata and properties for that container. It does not include a list of the blobs contained by the container. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName} | Updates container properties as specified in request body. Properties not mentioned in the request will be unchanged. Update fails if the specified container doesn't already exist. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName} | Gets properties of a specified container. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName} | Deletes specified container under its account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/setLegalHold | Sets legal hold tags. Setting the same tag results in an idempotent operation. SetLegalHold follows an append pattern and does not clear out the existing tags that are not specified in the request. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/clearLegalHold | Clears legal hold tags. Clearing the same or non-existent tag results in an idempotent operation. ClearLegalHold clears out only the specified tags in the request. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/{immutabilityPolicyName} | Creates or updates an unlocked immutability policy. ETag in If-Match is honored if given but not required for this operation. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/{immutabilityPolicyName} | Gets the existing immutability policy along with the corresponding ETag in response headers and body. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/{immutabilityPolicyName} | Aborts an unlocked immutability policy. The response of delete has immutabilityPeriodSinceCreationInDays set to 0. ETag in If-Match is required for this operation. Deleting a locked immutability policy is not allowed, only way is to delete the container after deleting all blobs inside the container. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/default/lock | Sets the ImmutabilityPolicy to Locked state. The only action allowed on a Locked policy is ExtendImmutabilityPolicy action. ETag in If-Match is required for this operation. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/default/extend | Extends the immutabilityPeriodSinceCreationInDays of a locked immutabilityPolicy. The only action allowed on a Locked policy will be this action. ETag in If-Match is required for this operation. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/lease | The Lease Container operation establishes and manages a lock on a container for delete operations. The lock duration can be 15 to 60 seconds, or can be infinite. |

## Enhanced Skill Content
## Question Mapping

- "What blob services are available for my storage account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices
- "How do I configure blob service properties like soft delete or versioning?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/{BlobServicesName}
- "What are the current blob service settings for my account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/{BlobServicesName}
- "List all blob containers in my storage account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers
- "How do I create a new blob container?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}
- "How do I update metadata or access level on an existing container?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}
- "Get details about a specific blob container" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}
- "How do I delete a blob container?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}
- "How do I place a legal hold on a container?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/setLegalHold
- "How do I remove a legal hold from a container?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/clearLegalHold
- "How do I set an immutability policy on a container?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/{immutabilityPolicyName}
- "How do I lock an immutability policy so it can't be deleted?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/default/lock
- "How do I extend the retention period of a locked immutability policy?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/immutabilityPolicies/default/extend
- "How do I acquire or break a lease on a container?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers/{containerName}/lease
- "How do I filter containers by name prefix when listing?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/blobServices/default/containers (use `$filter` parameter)

## Response Tips

- **Blob Services (list/get/set):** Responses return a `properties` object with nested CORS rules, delete retention policy, and versioning settings; always check `properties.deleteRetentionPolicy.enabled` and `properties.isVersioningEnabled` for current state.
- **Container list:** Paginated via `nextLink` in the response body; pass the `$skipToken` from the URL to fetch subsequent pages, and use `$maxpagesize` to control batch size.
- **Container CRUD:** PUT returns 201 on create, 200 on update of an existing container; DELETE returns 200 on success and 204 if the container was already gone -- treat both as successful.
- **Legal hold:** Response includes a `tags` array showing all active hold tags; an empty array means no holds remain.
- **Immutability policies:** Response includes an `ETag` in the `If-Match` header -- you must capture and reuse this ETag for lock, extend, and delete operations.
- **Lease operations:** Response varies by action (acquire/renew/break/release); check the `leaseId` in the response for acquire/renew, and `leaseTimeSeconds` for break.
- **Errors:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; common codes are `ContainerBeingDeleted`, `ImmutabilityPolicyLocked`, and `LeaseAlreadyPresent`.

## Anomaly Flags

- **ETag mismatch on immutability operations:** If a lock, extend, or delete call fails with 412 Precondition Failed, the `If-Match` ETag is stale -- surface this and suggest re-fetching the policy before retrying.
- **Legal hold accumulation:** If a `setLegalHold` response shows more than 5 active tags, flag that the container has many holds which will block deletion even after immutability policy expiry.
- **Immutability policy already locked:** Attempting to delete or shorten retention on a locked policy returns an error -- surface that locked policies can only be extended, never reduced or removed.
- **Container lease conflicts:** If container delete or update fails with `LeaseAlreadyPresent` (409), flag that a lease must be broken or released first before the operation can proceed.
- **Pagination not followed:** If a container list response contains `nextLink` but the caller stops after the first page, flag that results are incomplete.
- **Soft delete disabled:** When reading blob service properties, if `deleteRetentionPolicy.enabled` is false, surface a warning that accidental deletions are not recoverable.
- **API version drift:** This spec targets `2019-04-01`; if newer features are needed (e.g., object replication, blob inventory), flag that a newer API version may be required.

## Playbook

### 1. Create a Container with Immutability Protection

1. PUT the container at `.../containers/{containerName}` with desired access level in the `blobContainer` body.
2. Confirm 201 response (container created).
3. PUT an immutability policy at `.../containers/{containerName}/immutabilityPolicies/{policyName}` with the desired retention period in `parameters`.
4. Capture the `ETag` from the response headers.
5. POST to `.../immutabilityPolicies/default/lock` with the captured `ETag` in the `If-Match` header to make the policy permanent.
6. Verify the lock by GET on the immutability policy and confirming `state` is `Locked`.

### 2. Apply and Manage Legal Holds

1. POST to `.../containers/{containerName}/setLegalHold` with a `LegalHold` body containing the `tags` array (e.g., `["investigation-2024"]`).
2. Confirm the response shows your tag in the active tags list.
3. When the hold is no longer needed, POST to `.../containers/{containerName}/clearLegalHold` with the same tag(s) in the `LegalHold` body.
4. Verify the response shows an empty `tags` array (or the specific tag removed).

### 3. Safely Delete a Container

1. GET the container at `.../containers/{containerName}` to check `leaseState` and `hasLegalHold`.
2. If `leaseState` is `Leased`, POST to `.../containers/{containerName}/lease` with a break action to release the lease.
3. If `hasLegalHold` is true, POST to `.../clearLegalHold` to remove all active hold tags.
4. If an immutability policy exists and is unlocked, DELETE it at `.../immutabilityPolicies/{policyName}` with the current `ETag`.
5. DELETE the container at `.../containers/{containerName}`.
6. Accept either 200 (deleted) or 204 (already gone) as success.

### 4. Enable Soft Delete and Versioning on Blob Services

1. GET the current blob service properties at `.../blobServices/{BlobServicesName}` (typically `default`).
2. In the response body, note the current `properties` values to avoid overwriting settings.
3. PUT to the same endpoint with updated `parameters` body setting `deleteRetentionPolicy.enabled: true`, `deleteRetentionPolicy.days: 30`, and `isVersioningEnabled: true`.
4. Confirm 200 response and verify the returned properties match your intended configuration.

### 5. Extend Retention on a Locked Immutability Policy

1. GET the immutability policy at `.../immutabilityPolicies/{policyName}` to read the current retention days and capture the `ETag`.
2. POST to `.../immutabilityPolicies/default/extend` with the `If-Match` header set to the captured `ETag` and a `parameters` body containing the new (longer) retention period.
3. Confirm 200 response and verify `immutabilityPeriodSinceCreationInDays` reflects the extended value.
4. Note: you can only increase retention, never decrease it on a locked policy.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
