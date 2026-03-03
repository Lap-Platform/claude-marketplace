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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties | Lists a collection of properties defined within a service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId} | Gets the entity state (Etag) version of the property specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId} | Gets the details of the property specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId} | Creates or updates a property. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId} | Updates the specific property. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId} | Deletes specific property from the API Management service instance. |

## Enhanced Skill Content
## Question Mapping

- "What properties are configured on my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties
- "List all named values for my APIM instance" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties
- "Filter properties by display name or tags" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties (with $filter)
- "Does a specific property exist in my API Management service?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Get the details of a named value by its ID" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "What is the current value of a specific property?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Create a new named value in my APIM service" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Store an API key as a secret named value" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Replace an existing property entirely" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Update just the value of an existing named value without replacing it" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Change a property from plain text to secret" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "Remove a named value from my API Management service" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}
- "How do I rotate a secret stored in APIM properties?" -> PUT or PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/properties/{propId}

## Response Tips

- **List (GET collection):** Returns a paged array; follow `nextLink` for additional results. Use `$filter` with OData syntax (e.g., `substringof('name',properties/displayName)`) to narrow results.
- **Existence check (HEAD):** Returns 200 with no body if the property exists; expect 404 if it does not. Check the `ETag` response header for concurrency control.
- **Get single (GET by propId):** Response includes `properties.secret` boolean -- if true, the `value` field is redacted and will not be returned.
- **Create/Replace (PUT):** Returns 201 for newly created resources and 200 for updates to existing ones. Include `If-Match: *` header to force update or omit it to ensure create-only semantics.
- **Partial update (PATCH):** Returns 204 with no body on success. Requires `If-Match` header with the current ETag for optimistic concurrency.
- **Delete (DELETE):** Returns 200 or 204 on success. Requires `If-Match` header. A 412 response means the ETag is stale and the resource was modified since last read.

## Anomaly Flags

- **Secret value redaction:** If `properties.secret` is `true` on a GET response, the value is hidden. Surface this so the user knows the actual value cannot be retrieved via the API.
- **ETag mismatch (412 Precondition Failed):** Flag when PUT, PATCH, or DELETE returns 412 -- another process modified the resource. Recommend re-fetching to get the current ETag.
- **Missing If-Match header:** If a PATCH or DELETE call returns 400/412, check whether the `If-Match` header was included. This is a required header for mutation operations.
- **Pagination truncation:** If the list response contains a `nextLink` property, surface that not all results were returned and prompt to follow pagination.
- **Unexpected 404 on HEAD:** If a HEAD check returns 404 before a PUT, the property does not exist yet -- flag this as a create rather than update scenario.
- **Long-running operations:** If PUT returns a `Location` or `Azure-AsyncOperation` header, the operation is asynchronous. Surface this and recommend polling the provided URL for completion status.

## Playbook

### 1. Create a New Secret Named Value

1. Call HEAD on `/properties/{propId}` to confirm the property ID is not already taken.
2. If HEAD returns 404, call PUT on `/properties/{propId}` with a body containing `displayName`, `value`, and `secret: true`.
3. Verify the response is 201 (created). Store the returned `ETag` for future updates.
4. Call GET on `/properties/{propId}` to confirm creation -- note the value will be redacted since it is a secret.

### 2. Rotate a Secret Value

1. Call GET on `/properties/{propId}` to retrieve the current resource and its `ETag` header.
2. Call PATCH on `/properties/{propId}` with the new value in the body and `If-Match` set to the ETag from step 1.
3. Confirm the response is 204 (success).
4. If 412 is returned, re-fetch the resource (step 1) to get the latest ETag and retry.

### 3. Audit All Named Values

1. Call GET on `/properties` to list all named values (optionally with `$filter` to scope by tag or name).
2. If the response includes `nextLink`, follow it repeatedly until all pages are collected.
3. For each property, check `properties.secret` to identify which values are secrets (and therefore redacted).
4. Flag any properties without tags for organizational review.

### 4. Safely Delete a Named Value

1. Call GET on `/properties/{propId}` to confirm the property exists and retrieve its `ETag`.
2. Review the property details to ensure it is the correct resource (check `displayName` and `tags`).
3. Call DELETE on `/properties/{propId}` with `If-Match` set to the ETag.
4. Confirm the response is 200 or 204. If 412 is returned, the property was modified since your GET -- re-fetch and confirm before retrying.

### 5. Bulk List and Filter Properties

1. Call GET on `/properties` with `$filter=substringof('backend',properties/displayName)` to find properties matching a pattern.
2. Collect all pages by following `nextLink` until exhausted.
3. For each matching property, call GET on `/properties/{propId}` to retrieve full details.
4. Use the results to generate a report or feed into a configuration management pipeline.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
