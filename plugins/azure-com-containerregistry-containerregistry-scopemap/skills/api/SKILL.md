---
name: containerregistrymanagementclient
description: "ContainerRegistryManagementClient API skill. Use when working with ContainerRegistryManagementClient for subscriptions. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# ContainerRegistryManagementClient
API version: 2019-05-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/generateCredentials -- create first generateCredentials

## Endpoints

11 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName} | Gets the properties of the specified scope map. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName} | Creates a scope map for a container registry with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName} | Deletes a scope map from a container registry. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName} | Updates a scope map with the specified parameters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps | Lists all the scope maps for the specified container registry. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName} | Gets the properties of the specified token. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName} | Creates a token for a container registry with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName} | Deletes a token from a container registry. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName} | Updates a token with the specified parameters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens | Lists all the tokens for the specified container registry. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/generateCredentials | Generate keys for a token of a specified container registry. |

## Enhanced Skill Content
## Question Mapping

- "What scope maps exist in my container registry?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps
- "Get details of a specific scope map?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName}
- "How do I create a new scope map for repository permissions?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName}
- "How do I update the actions on an existing scope map?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName}
- "How do I delete a scope map I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scopeMaps/{scopeMapName}
- "What tokens are configured for my registry?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens
- "Get the properties of a specific token?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName}
- "How do I create a token linked to a scope map?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName}
- "How do I change which scope map a token uses?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName}
- "How do I revoke a token?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tokens/{tokenName}
- "How do I generate passwords/credentials for a token?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/generateCredentials
- "How do I set up fine-grained pull-only access for a CI pipeline?" -> PUT scopeMap (with read actions) then PUT token then POST generateCredentials
- "How do I rotate credentials for an existing token?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/generateCredentials

## Response Tips

- **Scope Map & Token lists** (GET .../scopeMaps, GET .../tokens): Results are paginated via `nextLink`; follow it until absent to retrieve all items.
- **Create/Update operations** (PUT, PATCH): A 200 means completed synchronously; a 201 means the resource was created but may still be provisioning -- check `provisioningState` in the response body.
- **Delete operations** (DELETE): A 200 means deleted, 202 means deletion accepted but still in progress (poll the resource until 404), 204 means the resource did not exist.
- **Credential generation** (POST .../generateCredentials): A 200 returns passwords immediately; a 202 means async -- use the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Error responses**: All endpoints return an `error` object with `code` and `message` fields; pay attention to `code` values like `ScopeMapInUse` (cannot delete a scope map referenced by tokens).

## Anomaly Flags

- **Long-running operations**: Surface 202 responses explicitly -- the user should know the operation is not yet complete and needs polling.
- **Scope map still in use**: Flag when a DELETE on a scope map fails because tokens reference it; suggest listing tokens first.
- **Token with no credentials**: After creating a token via PUT, credentials are not automatically generated -- flag if the user does not follow up with POST generateCredentials.
- **Disabled tokens**: When a GET on a token shows `status: disabled`, proactively note that the token will not authenticate until re-enabled via PATCH.
- **Provisioning failures**: If `provisioningState` is `Failed` in any create/update response, surface immediately with the error details.
- **API version mismatch**: This spec uses `2019-05-01-preview`; flag if the user references GA features that require a newer api-version.

## Playbook

### 1. Grant a CI Pipeline Read-Only Access to a Repository

1. Create a scope map with read-only actions: PUT .../scopeMaps/{scopeMapName} with `actions: ["repositories/myrepo/content/read", "repositories/myrepo/metadata/read"]`
2. Create a token linked to the scope map: PUT .../tokens/{tokenName} with `scopeMapId` pointing to the scope map resource ID and `status: enabled`
3. Generate credentials for the token: POST .../generateCredentials with `tokenId` set to the token resource ID and `passwords: [{"name": "password1"}]`
4. Use the returned username and password in the CI pipeline's docker login command

### 2. Rotate Credentials for an Existing Token

1. Retrieve the token to confirm its resource ID: GET .../tokens/{tokenName}
2. Generate new credentials: POST .../generateCredentials with `tokenId` and `passwords: [{"name": "password1"}]` (or `password2` to rotate the alternate slot)
3. Update the CI/CD system with the new password from the response
4. Optionally regenerate the other password slot to invalidate the old credential entirely

### 3. Audit and Clean Up Unused Scope Maps

1. List all tokens: GET .../tokens -- note which `scopeMapId` values are referenced
2. List all scope maps: GET .../scopeMaps
3. Compare the two lists to identify scope maps not referenced by any token
4. Delete each unused scope map: DELETE .../scopeMaps/{scopeMapName}
5. Confirm deletion completed (handle 202 by polling until 404)

### 4. Restrict a Token to Fewer Repositories

1. Retrieve the current scope map used by the token: GET .../tokens/{tokenName} to find `scopeMapId`, then GET .../scopeMaps/{scopeMapName}
2. Update the scope map actions: PATCH .../scopeMaps/{scopeMapName} with the reduced `actions` array (removing repositories no longer needed)
3. Verify the update: GET .../scopeMaps/{scopeMapName} and confirm `provisioningState: Succeeded`
4. Existing credentials remain valid -- no credential rotation needed for scope changes

### 5. Temporarily Disable and Re-enable a Token

1. Disable the token: PATCH .../tokens/{tokenName} with `status: disabled`
2. Confirm the token is disabled: GET .../tokens/{tokenName} and check `status` field
3. When ready to restore access: PATCH .../tokens/{tokenName} with `status: enabled`
4. Existing credentials remain valid -- no regeneration needed after re-enabling


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
