---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 6 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders | Lists a collection of Identity Provider configured in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName} | Gets the entity state (Etag) version of the identityProvider specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName} | Gets the configuration details of the identity Provider configured in specified service instance. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName} | Creates or Updates the IdentityProvider configuration. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName} | Updates an existing IdentityProvider configuration. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName} | Deletes the specified identity provider configuration. |

## Enhanced Skill Content
## Question Mapping

- "What identity providers are configured for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders
- "Does a specific identity provider exist on my APIM instance?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Get the details of the AAD identity provider configuration" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "How do I add a new identity provider to API Management?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Set up Google as an identity provider for my developer portal" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Configure Azure AD B2C for my API Management service" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Update the client secret for an existing identity provider" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Change the allowed tenants on my AAD identity provider" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Remove an identity provider from my APIM instance" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "Check if Facebook login is already configured before adding it" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "List all social login providers on my developer portal" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders
- "Replace the entire configuration for an identity provider" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}
- "How do I rotate credentials for a configured identity provider?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/identityProviders/{identityProviderName}

## Response Tips

- **List (GET collection):** Returns a paged array under `value`; check `nextLink` for continuation and follow it until null to retrieve all providers.
- **HEAD (existence check):** Returns 200 with no body if the provider exists; check the `ETag` header for use in subsequent conditional updates (If-Match).
- **GET (single):** Returns the full identity provider contract; `clientSecret` may be redacted -- use the dedicated secrets endpoint if available.
- **PUT (create/update):** Returns 201 on creation and 200 on replacement; always include `If-Match: *` for upsert or the current ETag for safe replacement.
- **PATCH (partial update):** Returns 204 with no body on success; requires `If-Match` header with the current ETag -- fetch the resource first to obtain it.
- **DELETE:** Returns 200 or 204 on success; requires `If-Match` header -- a 412 Precondition Failed means the ETag is stale and the resource was modified.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed):** The resource was modified since last read. Refetch and retry with the updated ETag before proceeding.
- **Provider already exists (409 Conflict):** A PUT for an identity provider that already exists without `If-Match` may conflict. Surface this and suggest using PATCH or providing `If-Match: *`.
- **Missing client secret on GET:** If `clientSecret` is empty or masked in the response, warn the user that secrets are write-only and cannot be retrieved after creation.
- **Deprecated identity provider names:** If the user targets a provider name that Azure has deprecated (e.g., legacy Microsoft Account), flag it and suggest the modern equivalent (e.g., `aad` or `aadB2C`).
- **Throttling (429 Too Many Requests):** Surface the `Retry-After` header value and pause before retrying. Alert the user if multiple 429s occur in sequence.
- **Long-running operation (202 Accepted):** If Azure returns an async operation header (`Azure-AsyncOperation` or `Location`), notify the user that the change is not yet applied and poll the status URL.

## Playbook

### 1. Add a New Social Identity Provider (e.g., Google)

1. List existing providers with GET on the collection endpoint to confirm the provider is not already configured.
2. Prepare the request body with `clientId`, `clientSecret`, and provider-specific settings (e.g., allowed tenants).
3. Send PUT to `/identityProviders/google` with the parameters body.
4. Verify 201 Created in the response. Capture the returned ETag for future updates.
5. Confirm by calling GET on the new provider to validate the stored configuration.

### 2. Rotate Credentials for an Existing Provider

1. GET the identity provider to retrieve the current ETag and configuration.
2. Prepare a PATCH body containing only the updated `clientSecret` (and `clientId` if rotating both).
3. Send PATCH with the `If-Match` header set to the ETag from step 1.
4. Confirm 204 No Content. If 412 is returned, re-fetch the resource and retry.
5. Test the developer portal login flow to validate the new credentials are working.

### 3. Safely Remove an Identity Provider

1. GET the identity provider to confirm it exists and capture its ETag.
2. List any dependent policies or products that reference this provider (outside this API -- check portal or policy API).
3. Send DELETE with the `If-Match` header set to the current ETag.
4. Confirm 200 or 204. If 409 is returned, resolve dependencies first.
5. List all providers again to verify the provider no longer appears.

### 4. Audit All Configured Identity Providers

1. GET the identity providers collection endpoint.
2. Follow `nextLink` pagination until all results are collected.
3. For each provider, GET the individual resource to retrieve full details (type, allowed tenants, authority URL).
4. Flag any providers with outdated or deprecated types.
5. Compile the results into a summary including provider name, type, and configuration status.

### 5. Conditional Create (Idempotent Upsert)

1. HEAD the target identity provider name to check existence without fetching the full body.
2. If 200 is returned, the provider exists -- decide whether to PATCH (partial update) or PUT with `If-Match` (full replace).
3. If the HEAD returns an error (404), proceed with PUT to create the provider fresh (no `If-Match` needed).
4. Verify the response: 201 for new creation, 200 for replacement.
5. Capture the ETag from the response for any subsequent operations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
