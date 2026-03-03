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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}/reconnect -- create first reconnect

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends | Lists a collection of backends in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId} | Gets the entity state (Etag) version of the backend specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId} | Gets the details of the backend specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId} | Creates or Updates a backend. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId} | Updates an existing backend. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId} | Deletes the specified backend. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}/reconnect | Notifies the APIM proxy to create a new connection to the backend after the specified timeout. If no timeout was specified, timeout of 2 minutes is used. |

## Enhanced Skill Content


## Question Mapping

- "What backends are configured in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends
- "List all backends filtered by protocol type?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends (use $filter)
- "Does a specific backend exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "Get the configuration details for a backend?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I register a new backend in API Management?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I update an existing backend's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I remove a backend from my API Management service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I reconnect a backend that went offline?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}/reconnect
- "Can I check if a backend exists without fetching its full details?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I replace a backend's entire configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I partially modify backend credentials without replacing everything?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}
- "How do I force a backend reconnection after a circuit breaker trip?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backends/{backendId}/reconnect

## Response Tips

- **List (GET collection):** Response includes `value` array and optional `nextLink` for pagination -- follow `nextLink` until absent to retrieve all pages.
- **HEAD:** Returns 200 with no body if the backend exists; check `ETag` header for concurrency control on subsequent PUT/PATCH.
- **GET (single):** Returns the full backend entity; note the `properties` nested object contains url, protocol, credentials, and proxy details.
- **PUT (create/update):** Returns 201 for new resources, 200 for updates; include `If-Match: *` header to overwrite or a specific ETag for optimistic concurrency.
- **PATCH:** Returns 204 with no body on success; requires `If-Match` header with the current ETag value.
- **DELETE:** Returns 200 or 204; requires `If-Match` header -- use `*` to force delete regardless of version.
- **POST reconnect:** Returns 202 (accepted) -- the operation is asynchronous; no response body is guaranteed.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed):** Another process modified the backend since you last read it -- re-fetch and retry.
- **404 on single-resource operations:** The backendId does not exist or was recently deleted -- verify the ID before retrying.
- **Throttling (429 Too Many Requests):** Azure ARM rate limits are approaching; back off using the `Retry-After` header value.
- **202 on reconnect with no follow-up:** The reconnect is fire-and-forget; surface a reminder to verify backend health afterward.
- **Long paginated lists:** If `nextLink` appears in the list response, warn that results are incomplete and offer to fetch all pages.
- **Preview API version (2019-12-01-preview):** This is a preview version -- flag that behavior may change and recommend checking for GA availability.

## Playbook

### 1. Register a New Backend

1. Choose a unique `backendId` (e.g., `my-service-backend`).
2. PUT to `/backends/{backendId}` with a body containing `properties.url`, `properties.protocol` (http or soap), and optional credentials.
3. Check the response: 201 means created, 200 means it already existed and was replaced.
4. GET the backend to confirm the configuration is correct.

### 2. Update Backend Credentials

1. GET `/backends/{backendId}` and capture the `ETag` header from the response.
2. PATCH `/backends/{backendId}` with the `If-Match` header set to the captured ETag, sending only the changed credential fields in the body.
3. Confirm 204 response (success, no body).
4. GET the backend again to verify the updated credentials took effect.

### 3. Safely Delete a Backend

1. HEAD `/backends/{backendId}` to confirm the backend exists and capture the `ETag`.
2. DELETE `/backends/{backendId}` with `If-Match` set to the ETag (prevents accidental deletion of a modified resource).
3. Expect 200 or 204 on success.
4. GET the list of backends to confirm the resource is gone.

### 4. Reconnect an Unhealthy Backend

1. GET `/backends/{backendId}` to check the current backend status and properties.
2. POST `/backends/{backendId}/reconnect` with an optional body specifying reconnect parameters (e.g., a custom `after` duration).
3. Note the 202 response -- the reconnection is asynchronous.
4. After a short delay, GET the backend again to verify it has recovered.

### 5. Audit All Backends in a Service

1. GET `/backends` to list all backends (use `$filter` to narrow by protocol or other criteria).
2. If `nextLink` is present, follow it to retrieve subsequent pages.
3. For each backend, HEAD `/backends/{backendId}` to quickly confirm existence and capture ETags.
4. Compile results into a summary of backend IDs, protocols, URLs, and health status for review.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
