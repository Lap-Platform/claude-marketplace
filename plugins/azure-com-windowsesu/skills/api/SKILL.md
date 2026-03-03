---
name: windowsesu
description: "windowsesu API skill. Use when working with windowsesu for providers, subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# windowsesu
API version: 2019-09-16-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.WindowsESU/operations -- verify access

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.WindowsESU/operations | List all available Windows.ESU provider operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.WindowsESU/multipleActivationKeys | List all Multiple Activation Keys (MAK) created for a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys | List all Multiple Activation Keys (MAK) in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName} | Get a MAK key. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName} | Create a MAK key. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName} | Update a MAK key. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName} | Delete a MAK key. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Windows ESU?" -> GET /providers/Microsoft.WindowsESU/operations
- "List all multiple activation keys in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.WindowsESU/multipleActivationKeys
- "Show activation keys in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys
- "Get details for a specific multiple activation key" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName}
- "Create a new multiple activation key" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName}
- "Replace an existing activation key configuration" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName}
- "Update tags or properties on an activation key" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName}
- "Delete a multiple activation key" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName}
- "How many ESU keys exist across all my resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.WindowsESU/multipleActivationKeys (then count results)
- "Does a specific activation key exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName} (check for 200 vs 404)
- "Move an activation key to a different resource group" -> DELETE from old group, then PUT to new group
- "What can I do with the Windows ESU resource provider?" -> GET /providers/Microsoft.WindowsESU/operations
- "Rename an activation key" -> PUT new key with same config, then DELETE old key (keys are named resources, no rename endpoint)

## Response Tips

- **Operations (providers):** Returns a list of available ARM operations; each entry includes `name`, `display`, and `isDataAction` -- use these to check RBAC permissions before calling other endpoints.
- **Key listings (subscription/resource group):** Responses return a `value` array of MAK resources; check for a `nextLink` property to handle pagination across large sets.
- **Single key GET:** Returns the full ARM resource envelope (`id`, `name`, `type`, `location`, `properties`, `tags`); activation status and key details live inside `properties`.
- **PUT (create/update):** Returns 200 for update-in-place or 201 for newly created; always check the status code to confirm which occurred.
- **PATCH (partial update):** Returns 200 with the updated resource; only the fields you send in `multipleActivationKey` are modified, others are preserved.
- **DELETE:** Returns 200 if the resource was deleted or 204 if it was already gone; both are success -- do not treat 204 as an error.

## Anomaly Flags

- **201 on PUT when 200 was expected:** Agent should flag that a new key was created rather than updating an existing one -- the named key did not previously exist.
- **204 on DELETE:** Surface that the resource was already absent; this may indicate a stale inventory or duplicate deletion attempt.
- **Missing `nextLink` with large result sets:** If a subscription-level listing returns many keys without pagination, flag potential truncation.
- **Provisioning state not "Succeeded":** After PUT or PATCH, check `properties.provisioningState` -- if it shows "Failed" or "Updating", surface the async operation status.
- **404 on GET for a key that was recently created:** Flag possible eventual consistency delay or incorrect resource group/key name.
- **API version mismatch:** This spec uses `2019-09-16-preview` -- agent should warn if a newer stable API version is available, as preview versions may be deprecated.
- **Throttling (429 responses):** Surface rate limit headers and recommend backoff before retrying; Azure ARM typically returns `Retry-After`.

## Playbook

### 1. Provision a New Multiple Activation Key

1. Call GET /providers/Microsoft.WindowsESU/operations to confirm you have the required permissions.
2. Call PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName} with the `multipleActivationKey` body containing location, OS type, and support type.
3. Check the response: 201 confirms creation, 200 means a key with that name already existed and was updated.
4. Verify `properties.provisioningState` is "Succeeded" in the response body.

### 2. Audit All ESU Keys Across a Subscription

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.WindowsESU/multipleActivationKeys to retrieve all keys.
2. If `nextLink` is present in the response, follow it to retrieve additional pages until no `nextLink` remains.
3. For each key, inspect `properties.expirationDate` and `properties.provisioningState` to identify expired or failed keys.
4. Group results by `resourceGroup` (parsed from the resource `id`) for a per-group summary.

### 3. Update Tags on an Existing Key

1. Call GET on the specific key to retrieve its current state and confirm it exists.
2. Call PATCH with a `multipleActivationKey` body containing only the `tags` field with the desired tag map.
3. Confirm the 200 response includes the updated tags in the returned resource.

### 4. Safely Delete an Activation Key

1. Call GET on the target key to confirm it exists and capture its current configuration for backup.
2. Call DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsESU/multipleActivationKeys/{multipleActivationKeyName}.
3. If 200 is returned, the key was successfully deleted. If 204, it was already absent.
4. Call GET again to verify the key returns 404, confirming deletion.

### 5. Migrate a Key to a Different Resource Group

1. Call GET on the source key to capture its full configuration (location, properties, tags).
2. Call PUT to the target resource group path with the same key name and the captured configuration as the body.
3. Confirm 201 (created) on the PUT response.
4. Call DELETE on the original key in the source resource group.
5. Verify with GET on both paths: new location returns 200, old location returns 404.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
