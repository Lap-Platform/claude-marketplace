---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 6 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics | Lists all diagnostics of the API Management service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId} | Gets the entity state (Etag) version of the Diagnostic specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId} | Gets the details of the Diagnostic specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId} | Creates a new Diagnostic or updates an existing one. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId} | Updates the details of the Diagnostic specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId} | Deletes the specified Diagnostic. |

## Enhanced Skill Content
## Question Mapping

- "What diagnostics are configured on my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics
- "List all diagnostics filtered by name or type?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics (with $filter)
- "Does a specific diagnostic exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "Get the details of a specific diagnostic?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "How do I enable Application Insights logging on my API Management instance?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "Create a new diagnostic configuration for my APIM service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "How do I update the sampling rate on an existing diagnostic?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "Change which logger a diagnostic sends data to?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "Remove a diagnostic from my API Management service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "How do I check if a diagnostic was already created before creating a duplicate?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "How do I replace an entire diagnostic configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "How do I disable logging without deleting the diagnostic?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/diagnostics/{diagnosticId}
- "What diagnostics exist across all my resource groups?" -> Iterate GET /diagnostics per resource group (multi-step)

## Response Tips

- **List (GET collection):** Returns a paged array; check `nextLink` for continuation and pass it as the next request URL to retrieve all results. Use `$filter` (OData syntax) to narrow results server-side.
- **Existence check (HEAD):** Returns 200 with no body if the diagnostic exists; a 404 means it does not. Use this as a lightweight pre-check before PUT to avoid accidental overwrites.
- **Detail (GET by ID):** Returns the full diagnostic entity including `properties.loggerId`, `properties.sampling`, and `properties.frontend`/`properties.backend` pipeline config. The `ETag` header is needed for safe updates.
- **Create/Replace (PUT):** Returns 201 on create, 200 on replace. Always include the `If-Match` header with the current ETag when replacing to prevent conflicts. The response body contains the final state of the resource.
- **Partial Update (PATCH):** Returns 204 with no body on success. Requires `If-Match` header. Only the fields you include in the request body are modified.
- **Delete (DELETE):** Returns 200 or 204 on success. A 404 likely means the resource was already deleted. Requires `If-Match: *` or a specific ETag.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed):** Another process modified the diagnostic since you last read it. Re-fetch and retry.
- **404 on GET/PATCH/DELETE by ID:** The diagnostic may have been deleted externally or the `diagnosticId` is misspelled. Surface this immediately rather than retrying silently.
- **201 vs 200 on PUT:** If the caller expected an update but received 201, the diagnostic did not previously exist -- flag that a new resource was created unexpectedly.
- **Empty diagnostics list:** If GET collection returns zero results, the APIM instance may have no logging configured at all. Proactively suggest creating an `applicationinsights` or `azuremonitor` diagnostic.
- **Throttling (429 Too Many Requests):** Azure ARM endpoints enforce rate limits per subscription. Surface `Retry-After` header value and pause before retrying.
- **Long-running operations:** If any response returns 202 with an `Azure-AsyncOperation` header, poll the provided URL until the operation completes.
- **Deprecated API version:** If the response includes a `Sunset` or deprecation warning header, alert the user to migrate to a newer `api-version`.

## Playbook

### 1. Enable Application Insights Logging on an APIM Service

1. Confirm the APIM service exists and note the `subscriptionId`, `resourceGroupName`, and `serviceName`.
2. HEAD `/diagnostics/applicationinsights` to check if the diagnostic already exists.
3. If 404, PUT `/diagnostics/applicationinsights` with the `parameters` body containing `loggerId` (the ARM resource ID of your Application Insights logger) and desired sampling/verbosity settings.
4. Verify creation by GET `/diagnostics/applicationinsights` and confirm the returned `properties.loggerId` matches.

### 2. Update Sampling Rate on an Existing Diagnostic

1. GET `/diagnostics/{diagnosticId}` to retrieve the current configuration and capture the `ETag` response header.
2. PATCH `/diagnostics/{diagnosticId}` with the `If-Match` header set to the ETag, and a body containing only the updated `properties.sampling.percentage` value.
3. Confirm 204 response. Re-fetch with GET to verify the new sampling rate is applied.

### 3. Safely Replace a Diagnostic Configuration

1. GET `/diagnostics/{diagnosticId}` to retrieve the full current entity and its `ETag`.
2. Modify the desired fields in the response body (e.g., change `loggerId`, adjust `frontend`/`backend` pipeline settings).
3. PUT `/diagnostics/{diagnosticId}` with the `If-Match` header set to the ETag and the modified body.
4. If 412 (Precondition Failed), re-fetch the entity, re-apply changes, and retry the PUT.
5. Confirm the response is 200 (updated) and review the returned entity.

### 4. Audit and Clean Up Unused Diagnostics

1. GET `/diagnostics` (with no filter) to list all diagnostics on the service.
2. For each diagnostic, GET `/diagnostics/{diagnosticId}` to inspect its logger reference and sampling configuration.
3. Cross-reference each `loggerId` to verify the target logger resource still exists.
4. For any diagnostic pointing to a deleted or orphaned logger, DELETE `/diagnostics/{diagnosticId}` with `If-Match: *`.
5. Confirm deletion with HEAD to verify 404.

### 5. Migrate from One Logger to Another

1. GET `/diagnostics` to list all diagnostics currently using the old logger.
2. Filter results client-side where `properties.loggerId` matches the old logger's ARM resource ID.
3. For each matching diagnostic, GET the full entity and capture its `ETag`.
4. PATCH each diagnostic with the new `loggerId` value using the captured `If-Match` header.
5. After all patches return 204, verify by listing diagnostics again and confirming all references point to the new logger.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
