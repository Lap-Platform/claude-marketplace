---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2015-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys -- create first ApiKeys

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys | Gets a list of API keys of an Application Insights component. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys | Create an API Key of an Application Insights component. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId} | Delete an API Key of an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId} | Get the API Key for this key id. |

## Enhanced Skill Content
## Question Mapping

- "What API keys exist for my Application Insights resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys
- "List all keys for a specific App Insights component" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys
- "Create a new API key for Application Insights" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys
- "Generate a read-only key for my telemetry data" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys
- "How do I revoke an Application Insights API key?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId}
- "Remove a compromised API key from my component" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId}
- "Get details about a specific API key" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId}
- "Check if a particular key ID is still valid" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId}
- "How many API keys does my resource currently have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys
- "Rotate an Application Insights API key" -> POST (create new) then DELETE (remove old) /subscriptions/.../ApiKeys + /APIKeys/{keyId}
- "What permissions does a specific API key have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/APIKeys/{keyId}
- "Set up programmatic access to my App Insights data" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/ApiKeys

## Response Tips

- **List keys (GET .../ApiKeys):** Returns an array of key objects; each includes `id`, `name`, and linked permissions -- the actual secret value is NOT returned after creation.
- **Create key (POST .../ApiKeys):** The response is the only time the full `apiKey` secret is returned; store it immediately as it cannot be retrieved again.
- **Delete key (DELETE .../APIKeys/{keyId}):** Returns 200 on success; a 404 means the key was already deleted or the keyId is wrong -- both are safe to treat as "removed."
- **Get key (GET .../APIKeys/{keyId}):** Returns key metadata but not the secret value; use this to verify a key exists and inspect its permissions.

## Anomaly Flags

- **Key secret shown only once:** After POST create, the `apiKey` field in the response is the only opportunity to capture the secret. Surface a prominent warning if the agent detects the value was not stored or echoed.
- **404 on delete or get:** Could indicate the keyId has a casing mismatch (note: the spec path uses `APIKeys` for single-key operations vs `ApiKeys` for the collection). Flag the casing difference if a 404 occurs.
- **Path casing inconsistency:** The collection endpoint uses `ApiKeys` while individual key endpoints use `APIKeys` -- agents should normalize carefully and flag if a request fails due to this.
- **Excessive key count:** If a list operation returns a large number of keys, surface a recommendation to audit and rotate unused keys.
- **Missing APIKeyProperties on create:** The `APIKeyProperties` map is required for POST; flag immediately if the caller omits it rather than letting the request fail with a 400.
- **OAuth2 token expiry:** All endpoints require OAuth2; proactively flag if a 401 response suggests the bearer token has expired mid-workflow.

## Playbook

### 1. Audit existing API keys

1. Call GET `.../components/{resourceName}/ApiKeys` to list all keys.
2. Review each key's `name` and `linkedReadProperties`/`linkedWriteProperties` for permission scope.
3. For any key with unclear purpose, call GET `.../APIKeys/{keyId}` to inspect metadata.
4. Flag keys with overly broad permissions or no recent usage for removal.

### 2. Create a new API key for read-only access

1. Prepare `APIKeyProperties` with a descriptive `name` and `linkedReadProperties` set to the desired data categories (e.g., telemetry, analytics).
2. Call POST `.../components/{resourceName}/ApiKeys` with the properties payload.
3. Immediately capture and securely store the `apiKey` value from the response -- it will not be retrievable again.
4. Verify the key exists by calling GET `.../APIKeys/{keyId}` using the returned key ID.

### 3. Rotate a compromised API key

1. Call POST `.../components/{resourceName}/ApiKeys` with the same permissions as the key being replaced to create a replacement.
2. Store the new `apiKey` secret securely and update all dependent services to use it.
3. Verify dependent services are working with the new key.
4. Call DELETE `.../APIKeys/{keyId}` with the old key's ID to revoke it.
5. Call GET `.../ApiKeys` to confirm the old key no longer appears in the list.

### 4. Clean up unused API keys

1. Call GET `.../components/{resourceName}/ApiKeys` to retrieve all keys.
2. Cross-reference each key's `name` and `id` against known active integrations.
3. For each unrecognized or unused key, call DELETE `.../APIKeys/{keyId}` to remove it.
4. Call GET `.../ApiKeys` again to confirm the final key inventory matches expectations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
