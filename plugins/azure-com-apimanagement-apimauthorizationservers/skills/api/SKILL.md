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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}/listSecrets -- create first listSecrets

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers | Lists a collection of authorization servers defined within a service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid} | Gets the entity state (Etag) version of the authorizationServer specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid} | Gets the details of the authorization server specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid} | Creates new authorization server or updates an existing authorization server. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid} | Updates the details of the authorization server specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid} | Deletes specific authorization server instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}/listSecrets | Gets the client secret details of the authorization server. |

## Enhanced Skill Content
## Question Mapping

- "What authorization servers are configured in my API Management instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers
- "List all OAuth2 providers for my APIM service with a filter?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers
- "Does authorization server {authsid} exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "Get the details of a specific authorization server?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "How is authorization server {authsid} configured?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "Create a new OAuth2 authorization server in my APIM instance?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "Replace the configuration of an existing authorization server?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "Update specific properties of an authorization server without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "Change the token endpoint or client credentials on an auth server?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "Remove an authorization server from my API Management service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}
- "What are the client secrets for an authorization server?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}/listSecrets
- "Retrieve the client ID and client secret for an OAuth2 provider?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}/listSecrets
- "How do I verify an authorization server is still present before updating it?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/authorizationServers/{authsid}

## Response Tips

- **List (GET collection):** Returns a paged array; check `nextLink` for additional pages. Use the `$filter` OData parameter to narrow results. Response wraps items in a `value` array.
- **Existence check (HEAD):** Returns 200 with no body if the resource exists; expect 404 if not. Use the `ETag` header from the response for conditional updates.
- **Single resource (GET by id):** Returns the full resource object. Capture the `ETag` header -- it is required as `If-Match` for PATCH and DELETE calls.
- **Create/Replace (PUT):** Returns 201 for new resources, 200 for replacements. Always supply the full resource definition in the request body.
- **Partial update (PATCH):** Returns 204 with no body on success. Requires `If-Match` header with the current ETag to prevent conflicting writes.
- **Delete (DELETE):** Returns 200 or 204 on success. Requires `If-Match` header. A 404 after deletion confirms the resource is gone.
- **Secrets (POST listSecrets):** Returns 200 with sensitive credential data. Treat the response as confidential and avoid logging it.

## Anomaly Flags

- **Missing ETag on GET responses:** If a GET response lacks an `ETag` header, flag it -- subsequent PATCH and DELETE calls will fail without a valid `If-Match` value.
- **409 Conflict on PUT/PATCH:** Indicates a concurrent modification. Surface this immediately and suggest re-fetching the resource to get the latest ETag.
- **404 on HEAD check before mutation:** If a HEAD returns 404 but the caller expects the resource to exist, alert before proceeding with PUT/PATCH/DELETE.
- **Secrets exposure in listSecrets:** Proactively warn when `listSecrets` is called that the response contains sensitive client credentials that should not be stored in logs or chat history.
- **Throttling (429 Too Many Requests):** Azure ARM APIs enforce per-subscription rate limits. Surface `Retry-After` header value and pause before retrying.
- **Deprecated api-version:** If the response includes deprecation warnings or the `Sunset` header, flag that `2019-12-01-preview` is a preview version and recommend checking for a GA release.
- **Partial filter results:** When using `$filter` on the list endpoint, flag if the result set is empty -- the filter syntax may be incorrect rather than there being no matches.

## Playbook

### 1. Register a New OAuth2 Authorization Server

1. Decide on an `authsid` identifier (e.g., `my-oauth-provider`).
2. PUT to `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.ApiManagement/service/{svc}/authorizationServers/my-oauth-provider` with the full configuration (display name, grant types, authorization endpoint, token endpoint, client ID, client credentials).
3. Confirm the response is 201 (created) or 200 (replaced existing).
4. GET the resource back to verify all fields and capture the `ETag`.

### 2. Rotate Client Credentials on an Authorization Server

1. POST to `.../authorizationServers/{authsid}/listSecrets` to retrieve the current client secret.
2. GET `.../authorizationServers/{authsid}` to fetch the full resource and its `ETag`.
3. PATCH `.../authorizationServers/{authsid}` with the new client secret in the body and the `ETag` in the `If-Match` header.
4. Confirm 204 response.
5. POST to `listSecrets` again to verify the new secret is active.

### 3. Audit All Authorization Servers in a Service

1. GET `.../authorizationServers` (no filter) to list all configured servers.
2. If `nextLink` is present, follow it to retrieve additional pages.
3. For each server, GET `.../authorizationServers/{authsid}` to inspect grant types, scopes, and endpoint URLs.
4. Flag any servers using implicit grant or lacking PKCE support.

### 4. Safely Delete an Authorization Server

1. HEAD `.../authorizationServers/{authsid}` to confirm the resource exists.
2. GET `.../authorizationServers/{authsid}` to capture the current `ETag` and review which APIs depend on it.
3. DELETE `.../authorizationServers/{authsid}` with the `ETag` in the `If-Match` header.
4. Confirm 200 or 204 response.
5. HEAD the same path again to verify the resource returns 404.

### 5. Conditionally Update an Authorization Server (Optimistic Concurrency)

1. GET `.../authorizationServers/{authsid}` and store the `ETag` from the response header.
2. Prepare the PATCH body with only the fields to change (e.g., token endpoint URL).
3. PATCH with `If-Match: {stored-etag}`.
4. If 204, the update succeeded.
5. If 409 (conflict), re-fetch the resource to get the latest ETag, merge changes, and retry the PATCH.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
