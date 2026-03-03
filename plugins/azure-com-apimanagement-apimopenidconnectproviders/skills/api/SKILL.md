---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}/listSecrets -- create first listSecrets

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders | Lists of all the OpenId Connect Providers. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid} | Gets the entity state (Etag) version of the openIdConnectProvider specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid} | Gets specific OpenID Connect Provider. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid} | Creates or updates the OpenID Connect Provider. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid} | Updates the specific OpenID Connect Provider. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid} | Deletes specific OpenID Connect Provider of the API Management service instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}/listSecrets | Gets the client secret details of the OpenID Connect Provider. |

## Enhanced Skill Content


## Question Mapping

- "What OpenID Connect providers are configured for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders
- "Does a specific OpenID Connect provider exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}
- "Get the details of an OpenID Connect provider by ID" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}
- "How do I register a new OpenID Connect provider?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}
- "How do I update the client ID or metadata endpoint on an existing provider?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}
- "Remove an OpenID Connect provider from my service" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}
- "What are the client secrets for my OpenID Connect provider?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/openidConnectProviders/{opid}/listSecrets
- "Filter OpenID Connect providers by display name" -> GET /...openidConnectProviders with $filter parameter
- "Check if a provider still exists before updating it" -> HEAD /...openidConnectProviders/{opid} (then PATCH)
- "Replace an OpenID Connect provider's entire configuration" -> PUT /...openidConnectProviders/{opid} (full replace, not PATCH)
- "How do I rotate client secrets for an OpenID Connect provider?" -> POST /...openidConnectProviders/{opid}/listSecrets (retrieve current), then PATCH to update
- "List all providers and get secrets for each one" -> GET /...openidConnectProviders, then POST /.../{opid}/listSecrets per result

## Response Tips

- **List (GET collection):** Returns a paged array; check `nextLink` for continuation. Use `$filter` OData expressions to narrow results server-side.
- **HEAD:** Returns only headers (no body). A 200 confirms existence; use the `ETag` header value for conditional updates via `If-Match`.
- **GET (single):** Response includes the full provider resource with `properties.clientId`, `properties.metadataEndpoint`, and `properties.displayName`. Secrets are NOT included -- use listSecrets.
- **PUT (create/replace):** Returns 201 on create, 200 on replace. The response body contains the full created/updated resource.
- **PATCH:** Returns 204 No Content on success -- no body returned. Re-fetch with GET if you need the updated state.
- **DELETE:** Returns 200 or 204 on success. Both indicate the provider was removed; do not treat 204 as an error.
- **listSecrets (POST):** Returns the client secret(s) in the response body. This is the only way to retrieve secrets -- they are omitted from GET responses.

## Anomaly Flags

- **ETag mismatch on PATCH/DELETE:** A 412 Precondition Failed means the resource was modified since your last read. Re-fetch and retry with the new ETag.
- **404 on single-resource operations:** The provider ID (`opid`) does not exist. Surface this clearly -- the user may have a typo or the provider was already deleted.
- **201 vs 200 on PUT:** Flag when a PUT returns 201 (created new) if the caller expected to update an existing provider -- they may have misspelled the opid.
- **Preview API version:** This uses `2019-12-01-preview`. Warn users that preview APIs may change or be deprecated without notice. Check for a GA version.
- **Empty secrets from listSecrets:** If the response contains no client secret, flag that the provider may be misconfigured or secrets were never set.
- **Throttling (429):** Azure ARM enforces rate limits per subscription. Surface `Retry-After` header value and back off accordingly.
- **$filter returning empty results:** If the filter syntax is valid but returns zero items, alert the user that the filter may be too restrictive rather than silently returning nothing.

## Playbook

### 1. Register a New OpenID Connect Provider

1. Confirm the API Management service exists and note `subscriptionId`, `resourceGroupName`, and `serviceName`
2. Choose a unique provider identifier for `{opid}` (alphanumeric, hyphens allowed)
3. PUT to `/...openidConnectProviders/{opid}` with `parameters` body containing `properties.displayName`, `properties.clientId`, `properties.clientSecret`, and `properties.metadataEndpoint`
4. Verify the response is 201 (created) and store the returned `ETag` for future updates

### 2. Rotate Client Secrets

1. POST to `/...openidConnectProviders/{opid}/listSecrets` to retrieve the current client secret
2. Generate or obtain the new client secret from your identity provider
3. GET `/...openidConnectProviders/{opid}` to obtain the current `ETag`
4. PATCH `/...openidConnectProviders/{opid}` with `If-Match: {ETag}` header and body containing the new `properties.clientSecret`
5. Confirm 204 response, then POST listSecrets again to verify the new secret is active

### 3. Audit All Configured Providers

1. GET `/...openidConnectProviders` to list all providers (follow `nextLink` for pagination)
2. For each provider, record `opid`, `displayName`, `clientId`, and `metadataEndpoint`
3. POST `/.../{opid}/listSecrets` for each provider to verify secrets are configured
4. Flag any providers with missing secrets or unreachable metadata endpoints

### 4. Safely Delete an OpenID Connect Provider

1. HEAD `/...openidConnectProviders/{opid}` to confirm the provider exists (200 = exists)
2. GET `/...openidConnectProviders/{opid}` to review its configuration and note the `ETag`
3. Verify no active APIs or products reference this provider as an authorization server
4. DELETE `/...openidConnectProviders/{opid}` with `If-Match: {ETag}` header
5. Confirm 200 or 204 response; HEAD again to verify it returns 404

### 5. Find and Update a Provider by Display Name

1. GET `/...openidConnectProviders` with `$filter=displayName eq 'My Provider'` to locate the provider
2. Extract the `opid` from the matching result
3. GET `/...openidConnectProviders/{opid}` to retrieve the full resource and current `ETag`
4. PATCH `/...openidConnectProviders/{opid}` with `If-Match: {ETag}` and the updated properties
5. Confirm 204, then GET again to verify the changes took effect


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
