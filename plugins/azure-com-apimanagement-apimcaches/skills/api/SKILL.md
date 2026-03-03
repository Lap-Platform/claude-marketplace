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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches | Lists a collection of all external Caches in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId} | Gets the entity state (Etag) version of the Cache specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId} | Gets the details of the Cache specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId} | Creates or updates an External Cache to be used in Api Management instance. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId} | Updates the details of the cache specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId} | Deletes specific Cache. |

## Enhanced Skill Content


## Question Mapping

- "What caches are configured in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches
- "Does a specific cache exist in my APIM instance?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "Get the details of a specific external cache." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "How do I add a new external cache to my API Management service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "How do I register a Redis cache with APIM?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "Update the connection string on an existing cache." -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "Change the description or resource ID of an external cache." -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "Remove an external cache from my APIM service." -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "Is my cache still reachable before I update its config?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "List all external caches then delete a specific one." -> GET .../caches then DELETE .../caches/{cacheId}
- "Replace an external cache configuration entirely." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches/{cacheId}
- "How many external caches does my service have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/caches

## Response Tips

- **List (GET .../caches):** Returns a paged collection; check `nextLink` for additional pages. Each item includes `id`, `name`, `type`, and `properties` with connection details.
- **Get (GET .../caches/{cacheId}):** Returns a single cache resource. The `ETag` header is required for subsequent PATCH/DELETE -- always capture it.
- **Head (HEAD .../caches/{cacheId}):** Returns only headers, no body. A 200 confirms existence; non-200 means the cache is missing or misconfigured.
- **Create/Update (PUT):** Returns 201 for new resources, 200 for updates to existing ones. Both return the full cache object.
- **Patch (PATCH):** Returns 204 with no body on success. Must include `If-Match` header with the current ETag.
- **Delete (DELETE):** Returns 200 or 204 on success. A 200 may include the deleted resource; 204 means no content returned.

## Anomaly Flags

- **Missing ETag on write operations:** PATCH and DELETE require `If-Match` headers. Surface a warning if the agent attempts these without first retrieving the current ETag via GET or HEAD.
- **Stale cache reference:** If a HEAD check returns a non-200 status before an update, flag that the cache may have been deleted or renamed by another process.
- **201 vs 200 on PUT:** If a PUT returns 200 when the agent expected to create a new cache, flag that an existing cache was overwritten -- this may be unintentional.
- **Pagination truncation:** If `nextLink` is present in a list response and the agent does not follow it, flag that results are incomplete.
- **Connection string exposure:** Cache parameters contain connection strings with credentials. Flag if these are being logged or stored in plain text.
- **Throttling (429):** Azure ARM endpoints enforce rate limits. Surface retry-after headers immediately and back off before retrying.

## Playbook

### 1. Register a New External Cache

1. Confirm the APIM service exists by listing current caches: GET .../caches
2. Choose a `cacheId` name (e.g., `westus-redis`)
3. Build the request body with `connectionString`, `description`, and optionally `resourceId` pointing to the Azure Cache for Redis resource
4. Create the cache: PUT .../caches/{cacheId} with the parameters body
5. Verify creation by checking for a 201 response and inspecting the returned resource

### 2. Update a Cache Connection String

1. Retrieve the current cache details: GET .../caches/{cacheId}
2. Capture the `ETag` header from the response
3. Build a PATCH body containing only the updated `connectionString`
4. Send the update: PATCH .../caches/{cacheId} with `If-Match: {ETag}` header
5. Confirm success with a 204 response

### 3. Audit and Clean Up Unused Caches

1. List all caches: GET .../caches (follow `nextLink` until all pages are retrieved)
2. For each cache, inspect `properties.description` and `properties.resourceId` to identify unused or orphaned entries
3. For each cache to remove, retrieve its ETag: HEAD .../caches/{cacheId}
4. Delete the cache: DELETE .../caches/{cacheId} with `If-Match: {ETag}`
5. Verify deletion by listing caches again to confirm removal

### 4. Verify Cache Existence Before Policy Assignment

1. Check if the target cache exists: HEAD .../caches/{cacheId}
2. If 200, proceed to assign the cache in an API Management caching policy
3. If non-200, create the cache first using the registration playbook above
4. After policy assignment, test the API endpoint to confirm cache hits are occurring

### 5. Replace a Cache Configuration Entirely

1. Retrieve the current cache: GET .../caches/{cacheId} and note the ETag
2. Build a complete replacement body with the new `connectionString`, `description`, and `resourceId`
3. Submit: PUT .../caches/{cacheId} with `If-Match: {ETag}` and the full parameters
4. Check for a 200 response (confirming replacement, not new creation)
5. Validate the new configuration by fetching: GET .../caches/{cacheId}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
