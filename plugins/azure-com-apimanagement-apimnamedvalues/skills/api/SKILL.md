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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}/listValue -- create first listValue

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues | Lists a collection of NamedValues defined within a service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId} | Gets the entity state (Etag) version of the NamedValue specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId} | Gets the details of the NamedValue specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId} | Creates or updates a NamedValue. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId} | Updates the specific NamedValue. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId} | Deletes specific NamedValue from the API Management service instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}/listValue | Gets the secret value of the NamedValue. |

## Enhanced Skill Content
## Question Mapping

- "What named values exist in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues
- "List all named values filtered by display name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues (use $filter)
- "Does a specific named value exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "Get details of a named value by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "How do I create a new named value?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "How do I store a secret in API Management?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId} (set secret=true in parameters)
- "Update the value of an existing named value?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "Rename a named value's display name?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "Delete a named value from my service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "Retrieve the actual secret value of a named value?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}/listValue
- "How do I check if a named value ID is already taken before creating one?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "How do I rotate a secret stored in named values?" -> GET then PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues/{namedValueId}
- "What named values are tagged as secrets?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/namedValues (use $filter)

## Response Tips

- **List (GET collection):** Response is paginated via `nextLink` property; keep following `nextLink` until absent. Results are in the `value` array. Each item includes `id`, `name`, and `properties` with display name, value, secret flag, and tags.
- **HEAD (existence check):** Returns 200 with no body if the named value exists; expect 404 if it does not. Check the `ETag` header for concurrency control.
- **GET (single item):** Returns the full named value resource. Secret values are masked in the `properties.value` field -- use the `listValue` POST to retrieve actual secrets.
- **PUT (create/replace):** Returns 201 for new resources, 200 for replacements, and 202 for long-running operations. Check the `Azure-AsyncOperation` or `Location` header when you get 202.
- **PATCH (update):** Returns 200 for immediate completion, 202 for async, and 204 for no-content success. Include `If-Match` with the ETag for optimistic concurrency.
- **DELETE:** Returns 200 or 204 on success; 204 means the resource was already absent. Idempotent -- safe to retry.
- **listValue (POST):** Returns the unmasked secret value in the response body. Treat this response as sensitive and avoid logging it.

## Anomaly Flags

- **Long-running operations (202 responses):** Surface when PUT or PATCH returns 202 instead of 200/201 -- the agent should poll the async operation URL until completion before proceeding.
- **ETag mismatch (412 Precondition Failed):** Flag concurrent modification conflicts immediately; recommend re-fetching the resource and retrying the update.
- **Secret value exposure:** Warn when `listValue` is called, since it returns unmasked secrets -- confirm the user intends to retrieve sensitive data.
- **Missing named value (404 on GET/HEAD):** Proactively suggest creating the named value if a dependent operation assumes it exists.
- **Throttling (429 Too Many Requests):** Surface rate limit headers (`Retry-After`) and recommend backing off before retrying.
- **Preview API version:** This API version (`2019-12-01-preview`) is a preview -- flag that behavior may change and recommend checking for GA versions.
- **Pagination truncation:** Warn if list response contains `nextLink` but the user only processes the first page, since they may be missing named values.

## Playbook

### 1. Create a New Secret Named Value

1. Call HEAD on the target `namedValueId` to verify it does not already exist (expect 404).
2. Call PUT with `parameters` including `displayName`, `value`, `secret: true`, and optional `tags`.
3. If the response is 202, extract the async operation URL from the `Azure-AsyncOperation` header.
4. Poll the async operation URL until status is `Succeeded`.
5. Call GET on the named value to confirm it was created with the correct properties.

### 2. Rotate a Secret Value

1. Call GET on the named value to retrieve current metadata and the `ETag` header.
2. Call PATCH with the new `value` in `parameters` and include `If-Match: <ETag>` for concurrency safety.
3. If 412 is returned, re-fetch the resource and retry with the updated ETag.
4. If 202 is returned, poll the async operation until complete.
5. Call POST on `listValue` to verify the secret was updated to the new value.

### 3. Audit All Named Values in a Service

1. Call GET on the named values collection (no filter) to list all entries.
2. Follow `nextLink` pagination until all pages are retrieved.
3. For each named value, note whether `properties.secret` is true or false.
4. For secret named values, call POST `listValue` only if auditing requires inspecting actual values.
5. Compile results into a report grouping by tags, secret status, and last-modified date.

### 4. Safely Delete a Named Value

1. Call GET on the named value to confirm it exists and retrieve its `ETag`.
2. Verify the named value is not referenced in any API Management policies (check outside this API).
3. Call DELETE with `If-Match: <ETag>` to prevent deleting a concurrently modified resource.
4. Confirm deletion by calling HEAD on the named value (expect 404).

### 5. Bulk Update Named Values by Filter

1. Call GET on the collection with `$filter` to narrow results (e.g., by tag or display name pattern).
2. Follow pagination to collect all matching named values.
3. For each match, call GET to retrieve the current ETag.
4. Call PATCH with updated `parameters` and the matching `If-Match` header.
5. Track 202 responses and poll each async operation to completion before reporting success.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
