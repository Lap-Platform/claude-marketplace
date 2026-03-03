---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/regeneratePrimaryKey -- create first regeneratePrimaryKey

## Endpoints

12 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName} | Tenant access metadata |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName} | Get tenant access information details |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName} | Update tenant access information details. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/regeneratePrimaryKey | Regenerate primary access key |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/regenerateSecondaryKey | Regenerate secondary access key |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git | Gets the Git access configuration for the tenant. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git/regeneratePrimaryKey | Regenerate primary access key for GIT. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git/regenerateSecondaryKey | Regenerate secondary access key for GIT. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/deploy | This operation applies changes from the specified Git branch to the configuration database. This is a long running operation and could take several minutes to complete. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/save | This operation creates a commit with the current configuration snapshot to the specified branch in the repository. This is a long running operation and could take several minutes to complete. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/validate | This operation validates the changes in the specified Git branch. This is a long running operation and could take several minutes to complete. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/syncState | Gets the status of the most recent synchronization between the configuration database and the Git repository. |

## Enhanced Skill Content
## Question Mapping

- "How do I check if tenant access is enabled for my API Management service?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}
- "What are the current tenant access settings?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}
- "How do I enable or disable tenant access?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}
- "How do I rotate the primary access key for tenant access?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/regeneratePrimaryKey
- "How do I regenerate the secondary key for tenant access?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/regenerateSecondaryKey
- "What are the Git access credentials for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git
- "How do I rotate the Git repository primary key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git/regeneratePrimaryKey
- "How do I rotate the Git repository secondary key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{accessName}/git/regenerateSecondaryKey
- "How do I deploy a Git configuration to my API Management service?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/deploy
- "How do I save the current service snapshot to the Git repository?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/save
- "How do I validate a Git configuration before deploying?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/validate
- "What is the current sync state between the service and Git?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tenant/{configurationName}/syncState
- "How do I do a safe Git-based configuration deployment?" -> POST .../validate then POST .../deploy (multi-step)
- "How do I rotate all tenant access keys at once?" -> POST .../regeneratePrimaryKey then POST .../regenerateSecondaryKey (multi-step)

## Response Tips

- **Tenant access GET/HEAD**: HEAD returns only headers (use to check existence without payload); GET returns the access info object with `enabled` flag and key properties. Check the `ETag` header for use with conditional PATCH requests.
- **Tenant access PATCH**: Returns 204 No Content on success -- no response body. Pass `If-Match` header with the ETag from GET to avoid conflicts.
- **Key regeneration (all 4 endpoints)**: Returns 204 No Content. The new key value is not returned in the response; follow up with a GET to retrieve the updated keys.
- **Git configuration deploy/save/validate**: May return 200 (completed synchronously) or 202 (long-running operation). On 202, check the `Location` or `Azure-AsyncOperation` header and poll until the operation completes.
- **Sync state GET**: Returns a sync status object including `commitId`, `isExport`, `isSynced`, `isGitEnabled`, and timestamp fields. Use `isSynced: false` to detect pending changes.

## Anomaly Flags

- **202 responses on deploy/save/validate**: These are async operations. Surface the operation URL and remind the user to poll for completion rather than assuming success.
- **ETag mismatch on PATCH**: A 412 Precondition Failed indicates the tenant access settings were modified since last read. Surface this and recommend re-fetching before retrying.
- **Sync state drift**: If `syncState` returns `isSynced: false` after a deploy or save, flag that the configuration may not have propagated. Suggest re-checking or re-deploying.
- **Key regeneration without backup**: When a user regenerates keys, warn that any clients using the old key will lose access immediately. Recommend updating dependent systems before or immediately after rotation.
- **Git not enabled**: If GET on the `/git` endpoint returns an error or empty credentials, surface that Git access may not be configured for this service instance.
- **Deploy without validate**: If a user calls deploy without first calling validate, proactively suggest running validation to catch configuration errors before they affect the live service.

## Playbook

### 1. Safe Git Configuration Deployment

1. GET `.../tenant/{configurationName}/syncState` to check current sync status
2. POST `.../tenant/{configurationName}/validate` with configuration parameters
3. If 202, poll the operation URL until validation completes; check for errors
4. If validation succeeds, POST `.../tenant/{configurationName}/deploy` with the same parameters
5. If 202, poll the operation URL until deployment completes
6. GET `.../tenant/{configurationName}/syncState` to confirm `isSynced: true`

### 2. Rotate All Tenant Access Keys

1. GET `.../tenant/{accessName}` to retrieve current access settings and note the ETag
2. Notify downstream consumers that keys will rotate
3. POST `.../tenant/{accessName}/regeneratePrimaryKey` to rotate the primary key
4. GET `.../tenant/{accessName}` to retrieve the new primary key and distribute to consumers
5. POST `.../tenant/{accessName}/regenerateSecondaryKey` to rotate the secondary key
6. GET `.../tenant/{accessName}` to confirm both keys have been updated

### 3. Save Current Configuration to Git

1. GET `.../tenant/{accessName}/git` to verify Git access is configured and credentials are valid
2. GET `.../tenant/{configurationName}/syncState` to check if there are unsaved changes
3. POST `.../tenant/{configurationName}/save` with a descriptive commit message in parameters
4. If 202, poll the operation URL until the save completes
5. GET `.../tenant/{configurationName}/syncState` to confirm the save succeeded and `isSynced: true`

### 4. Enable or Disable Tenant Access

1. GET `.../tenant/{accessName}` to retrieve current settings and the `ETag` header
2. PATCH `.../tenant/{accessName}` with `{ "enabled": true/false }` in parameters, passing the ETag in the `If-Match` header
3. Expect 204 No Content on success
4. HEAD `.../tenant/{accessName}` to confirm the change took effect

### 5. Rotate Git Repository Access Keys

1. GET `.../tenant/{accessName}/git` to verify current Git credentials
2. POST `.../tenant/{accessName}/git/regeneratePrimaryKey` to rotate the Git primary key
3. GET `.../tenant/{accessName}/git` to retrieve the new primary key
4. Update any CI/CD pipelines or local Git remotes using the old key
5. POST `.../tenant/{accessName}/git/regenerateSecondaryKey` to rotate the secondary key
6. GET `.../tenant/{accessName}/git` to confirm both Git keys are updated


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
