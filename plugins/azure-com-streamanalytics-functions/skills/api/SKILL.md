---
name: streamanalyticsmanagementclient
description: "StreamAnalyticsManagementClient API skill. Use when working with StreamAnalyticsManagementClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# StreamAnalyticsManagementClient
API version: 2016-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions -- verify access
3. POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/test -- create first test

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName} | Creates a function or replaces an already existing function under an existing streaming job. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName} | Updates an existing function under an existing streaming job. This can be used to partially update (ie. update one or two properties) a function without affecting the rest the job or function definition. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName} | Deletes a function from the streaming job. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName} | Gets details about the specified function. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions | Lists all of the functions under the specified streaming job. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/test | Tests if the information provided for a function is valid. This can range from testing the connection to the underlying web service behind the function or making sure the function code provided is syntactically correct. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/retrieveDefaultDefinition | Retrieves the default definition of a function based on the parameters specified. |

## Enhanced Skill Content


## Question Mapping

- "How do I create a new function in my Stream Analytics job?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}
- "How do I update an existing Stream Analytics function?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}
- "How do I replace a function definition entirely?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}
- "How do I delete a function from my streaming job?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}
- "How do I get the details of a specific function?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}
- "How do I list all functions in a Stream Analytics job?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions
- "How do I test if a function's connection works?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/test
- "How do I get the default definition for a function type?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/retrieveDefaultDefinition
- "How do I filter which properties are returned when listing functions?" -> GET .../functions with `$select` query parameter
- "How do I conditionally update a function only if it hasn't changed?" -> PATCH .../functions/{functionName} with `If-Match` header (ETag)
- "How do I create a function only if it doesn't already exist?" -> PUT .../functions/{functionName} with `If-None-Match: *` header
- "How do I verify my Azure ML function binding is valid before deploying?" -> POST .../functions/{functionName}/test
- "How do I scaffold a new function from a template?" -> POST .../functions/{functionName}/retrieveDefaultDefinition

## Response Tips

- **PUT (create/replace):** 200 means updated in place, 201 means newly created. Check the response status to distinguish between create and update operations.
- **PATCH (update):** Always returns 200 on success. The response body contains the full updated function definition, not just the patched fields.
- **DELETE:** 200 means the function was deleted; 204 means it was already gone (idempotent). Both are success states.
- **GET (single):** Returns the full function resource. Check `properties.type` to determine if it's a scalar, UDF, or Azure ML function.
- **GET (list):** Response includes a `value` array. Use `$select` to reduce payload size. Watch for `nextLink` if pagination is present.
- **POST test:** 200 means the test completed inline with results in the body. 202 means the test is running asynchronously -- poll the `Location` header URL for results.
- **POST retrieveDefaultDefinition:** Returns a 200 with a pre-populated function definition template suitable for passing directly to PUT.

## Anomaly Flags

- **202 on test endpoint:** The function test is running asynchronously. Surface the `Location` header and remind the user to poll for completion.
- **ETag mismatch (412 Precondition Failed):** The function was modified by another process since last read. Surface the conflict and suggest re-fetching before retrying.
- **204 on DELETE:** The function didn't exist. Flag this if the user expected it to be present -- it may indicate a naming mismatch or prior deletion.
- **Missing `api-version` parameter:** All endpoints require this common field. Flag immediately if omitted, as it will produce a 400 error.
- **Rate limiting (429):** Azure ARM has subscription-level throttling. Surface `Retry-After` header and recommend exponential backoff.
- **201 vs 200 on PUT:** If the user intended to update (not create), a 201 signals an unexpected new resource was created -- possibly a typo in `functionName`.

## Playbook

### 1. Create a new UDF from a default template

1. Call POST `.../functions/{functionName}/retrieveDefaultDefinition` with the desired function type parameters to get a scaffold.
2. Modify the returned definition with your custom binding, inputs, and output.
3. Call PUT `.../functions/{functionName}` with the modified definition and `If-None-Match: *` to ensure you don't overwrite an existing function.
4. Confirm the response is 201 (created).

### 2. Safely update a function without conflicts

1. Call GET `.../functions/{functionName}` to retrieve the current definition and its ETag.
2. Modify the properties you need to change in the response body.
3. Call PATCH `.../functions/{functionName}` with the changes and set `If-Match` to the ETag from step 1.
4. If you get 412, re-fetch and retry. On 200, the update succeeded.

### 3. Test and validate a function binding

1. Call GET `.../functions/{functionName}` to confirm the function exists and review its current configuration.
2. Call POST `.../functions/{functionName}/test` to validate connectivity.
3. If you receive 202, poll the URL in the `Location` header until you get a terminal result.
4. Check the test result for `status: "TestSucceeded"` or inspect error details.

### 4. Audit and clean up unused functions

1. Call GET `.../functions` with `$select` to list all functions in the job (use a narrow projection for efficiency).
2. For each function, call GET `.../functions/{functionName}` to inspect its full configuration and determine if it's in use.
3. For functions to remove, call DELETE `.../functions/{functionName}`.
4. Verify each DELETE returns 200. Log any 204 responses as already-absent.

### 5. Migrate a function definition between jobs

1. Call GET `.../functions/{functionName}` on the source job to export the full function definition.
2. Strip read-only properties (e.g., `id`, `name`, `type` at the resource level) from the response.
3. Call PUT `.../functions/{functionName}` on the target job with the cleaned definition.
4. Call POST `.../functions/{functionName}/test` on the target job to verify the binding works in the new context.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
