---
name: customproviders
description: "customproviders API skill. Use when working with customproviders for providers, subscriptions, {scope}. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# customproviders
API version: 2018-09-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.CustomProviders/operations -- verify access

## Endpoints

11 endpoints across 3 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.CustomProviders/operations | The list of operations provided by Microsoft CustomProviders. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName} | Creates or updates the custom resource provider. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName} | Deletes the custom resource provider. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName} | Gets the custom resource provider manifest. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName} | Updates an existing custom resource provider. The only value that can be updated via PATCH currently is the tags. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders | Gets all the custom resource providers within a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CustomProviders/resourceProviders | Gets all the custom resource providers within a subscription. |

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| PUT | /{scope}/providers/Microsoft.CustomProviders/associations/{associationName} | Create or update an association. |
| DELETE | /{scope}/providers/Microsoft.CustomProviders/associations/{associationName} | Delete an association. |
| GET | /{scope}/providers/Microsoft.CustomProviders/associations/{associationName} | Get an association. |
| GET | /{scope}/providers/Microsoft.CustomProviders/associations | Gets all association for the given scope. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Custom Providers?" -> GET /providers/Microsoft.CustomProviders/operations
- "How do I create a custom resource provider?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}
- "How do I delete a custom resource provider?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}
- "Get details of a specific custom resource provider" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}
- "How do I update or patch a custom resource provider?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}
- "List all custom resource providers in a resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders
- "List all custom resource providers in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomProviders/resourceProviders
- "How do I associate a custom provider with a resource?" -> PUT /{scope}/providers/Microsoft.CustomProviders/associations/{associationName}
- "Remove an association from a resource" -> DELETE /{scope}/providers/Microsoft.CustomProviders/associations/{associationName}
- "Get details of a specific association" -> GET /{scope}/providers/Microsoft.CustomProviders/associations/{associationName}
- "List all associations for a given scope" -> GET /{scope}/providers/Microsoft.CustomProviders/associations
- "How do I set up a custom resource provider and then associate it with a resource?" -> PUT /subscriptions/.../resourceProviders/{name} then PUT /{scope}/providers/Microsoft.CustomProviders/associations/{associationName}
- "Check if a custom resource provider exists before deleting it" -> GET /subscriptions/.../resourceProviders/{name} then DELETE /subscriptions/.../resourceProviders/{name}

## Response Tips

- **Operations (providers):** Returns a flat list of available operations; no pagination. Check the `value` array for operation names and descriptions.
- **Resource Providers (subscriptions):** PUT returns 200 (updated) or 201 (created); DELETE returns 200 (done), 202 (accepted, still deleting), or 204 (already gone). List endpoints return a `value` array with optional `nextLink` for pagination -- follow `nextLink` until absent.
- **Associations ({scope}):** Same create/delete status code pattern as resource providers. GET returns the full association object; list returns `value` array with optional `nextLink`.
- **All endpoints:** Errors follow Azure standard format with `error.code` and `error.message` nested fields. Always include `api-version=2018-09-01-preview` as a query parameter.

## Anomaly Flags

- **202 on DELETE:** The resource is being deleted asynchronously. Surface the `Location` or `Azure-AsyncOperation` header so the user can poll for completion.
- **204 on DELETE:** The resource was already absent. Flag this if the user expected it to exist -- it may indicate a naming mismatch or prior deletion.
- **Missing `nextLink` after large result sets:** If list endpoints return many items but no `nextLink`, the full set was returned. If fewer items than expected appear, flag possible filtering or permission issues.
- **`api-version` mismatch:** This spec targets `2018-09-01-preview`. If the user passes a different version, warn that behavior may differ or the endpoint may not exist.
- **Long-running operations:** PUT returning 201 may include a provisioning state of `Creating` or `Accepted`. Surface `provisioningState` values that are not `Succeeded` so the user knows the resource is not yet ready.
- **Scope format errors:** The `{scope}` parameter must be a valid Azure resource ID. Flag malformed scope values early before making the request.

## Playbook

### 1. Create a Custom Resource Provider and Verify

1. PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}` with the `resourceProvider` body containing actions, resource types, and validations.
2. Check the response: 200 means updated in place, 201 means newly created.
3. If `provisioningState` is not `Succeeded`, poll with GET on the same path until it reaches `Succeeded` or fails.
4. GET the resource provider to confirm its configuration matches expectations.

### 2. Associate a Custom Provider with a Resource

1. GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}` to retrieve the provider's resource ID.
2. PUT `/{scope}/providers/Microsoft.CustomProviders/associations/{associationName}` with the body containing `targetResourceId` pointing to the provider.
3. Verify with GET `/{scope}/providers/Microsoft.CustomProviders/associations/{associationName}` to confirm the association is active.

### 3. Clean Up: Remove Association then Delete Provider

1. DELETE `/{scope}/providers/Microsoft.CustomProviders/associations/{associationName}`.
2. If response is 202, poll the `Location` header URL until deletion completes (200) or the GET returns 404.
3. DELETE `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}`.
4. If response is 202, poll similarly until the provider is fully removed.
5. Confirm with GET on both resources -- expect 404 for both.

### 4. Audit All Custom Providers and Associations in a Subscription

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.CustomProviders/resourceProviders` to list all providers across all resource groups.
2. Follow `nextLink` if present to retrieve all pages.
3. For each provider, note its resource ID and use it as `{scope}`.
4. GET `/{scope}/providers/Microsoft.CustomProviders/associations` for each provider to list all associations.
5. Compile the full inventory of providers and their associations.

### 5. Update a Custom Resource Provider's Configuration

1. GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomProviders/resourceProviders/{resourceProviderName}` to retrieve current configuration.
2. PATCH the same path with `patchableResource` body containing only the fields to change (e.g., updating tags or modifying action endpoints).
3. Verify the 200 response contains the updated configuration.
4. If associations depend on the changed configuration, GET each association to confirm they still resolve correctly.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
