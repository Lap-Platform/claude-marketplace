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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers | Lists a collection of loggers in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId} | Gets the entity state (Etag) version of the logger specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId} | Gets the details of the logger specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId} | Creates or Updates a logger. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId} | Updates an existing logger. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId} | Deletes the specified logger. |

## Enhanced Skill Content


## Question Mapping

- "What loggers are configured for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers
- "How do I filter loggers by type?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers (use $filter)
- "Does a specific logger exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "Get the details of a specific logger" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I create a new Application Insights logger?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I create an Event Hub logger?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I update a logger's credentials?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I change the description on an existing logger?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I delete a logger?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I force-delete a logger even if diagnostics reference it?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId} (use force=true)
- "How do I check if a logger name is already taken before creating one?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I replace a logger's entire configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers/{loggerId}
- "How do I list all Event Hub loggers only?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/loggers (use $filter=loggerType eq 'azureEventHub')

## Response Tips

- **List (GET collection):** Returns a paged result with `value` array and `nextLink` for pagination. Follow `nextLink` until absent to retrieve all loggers. The `$filter` param accepts OData syntax (e.g., `loggerType eq 'applicationInsights'`).
- **Existence check (HEAD):** Returns 200 with no body if the logger exists; expect 404 if it does not. Use this as a lightweight pre-check before create/update.
- **Get detail (GET single):** Returns the full logger entity including `properties.loggerType`, `properties.description`, and `properties.credentials`. Check the `ETag` header for concurrency control.
- **Create/Replace (PUT):** Returns 201 for newly created loggers and 200 for replaced ones. Inspect the status code to distinguish create vs update. Include `If-Match: *` header to force replace.
- **Partial update (PATCH):** Returns 204 with no body on success. Requires `If-Match` header with the current ETag value for optimistic concurrency.
- **Delete (DELETE):** Returns 200 or 204 on success. A 409 may occur if the logger is referenced by a diagnostic -- use `force=true` to override.

## Anomaly Flags

- **ETag mismatch on PATCH/DELETE:** A 412 Precondition Failed indicates another process modified the logger since you last read it. Re-fetch and retry.
- **API version deprecation:** This spec uses `2019-12-01-preview`. Watch for `Sunset` or `Deprecation` headers in responses signaling migration to a GA version.
- **Dangling logger references:** Deleting a logger without `force=true` that is still referenced by a diagnostic setting will return 409 Conflict. Surface this to the user with guidance to either remove the diagnostic binding first or use force.
- **Pagination overflow:** If the list endpoint returns `nextLink` repeatedly, flag unusually large logger counts (e.g., >100) as a potential misconfiguration.
- **Missing credentials in response:** Logger GET responses may redact sensitive fields in `properties.credentials`. Flag when credential values return as null or empty so the user knows they cannot be read back.
- **Throttling (429):** Azure ARM APIs enforce rate limits per subscription. Surface `Retry-After` header value and pause before retrying.

## Playbook

### 1. Set Up a New Application Insights Logger

1. Confirm the target API Management service exists and note its `subscriptionId`, `resourceGroupName`, and `serviceName`.
2. Choose a `loggerId` (e.g., `appinsights-prod`).
3. HEAD the logger path to verify the name is not already taken (expect 404).
4. PUT the logger with `parameters` body containing `loggerType: "applicationInsights"`, `description`, and `credentials.instrumentationKey`.
5. Confirm 201 response. Store the returned `ETag` for future updates.

### 2. Rotate Logger Credentials

1. GET the specific logger to retrieve its current configuration and `ETag`.
2. PATCH the logger with updated `credentials` object (e.g., new `instrumentationKey` or Event Hub connection string). Include `If-Match` header with the current ETag.
3. Confirm 204 response.
4. GET the logger again to verify the update took effect (note: credential values may be redacted).

### 3. Audit and Clean Up Unused Loggers

1. GET the full logger collection (follow `nextLink` for pagination).
2. For each logger, note its `loggerId` and `loggerType`.
3. Cross-reference with diagnostic settings to identify loggers not attached to any diagnostic.
4. For each unused logger, DELETE it (no `force` needed since it has no references).
5. Confirm 200 or 204 for each deletion.

### 4. Migrate from Event Hub to Application Insights Logger

1. GET the existing Event Hub logger to capture its `loggerId` and current `ETag`.
2. PUT the same `loggerId` with new `parameters` body setting `loggerType: "applicationInsights"` and the Application Insights `instrumentationKey`. Include `If-Match` with the current ETag.
3. Confirm 200 response (update of existing resource).
4. Verify by GET that `loggerType` now reads `applicationInsights`.
5. Update any diagnostic settings referencing this logger if the expected payload format changed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
