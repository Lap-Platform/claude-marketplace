---
name: streamanalyticsmanagementclient
description: "StreamAnalyticsManagementClient API skill. Use when working with StreamAnalyticsManagementClient for subscriptions. Covers 6 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs -- verify access
3. POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}/test -- create first test

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName} | Creates an input or replaces an already existing input under an existing streaming job. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName} | Updates an existing input under an existing streaming job. This can be used to partially update (ie. update one or two properties) an input without affecting the rest the job or input definition. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName} | Deletes an input from the streaming job. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName} | Gets details about the specified input. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs | Lists all of the inputs under the specified streaming job. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}/test | Tests whether an input’s datasource is reachable and usable by the Azure Stream Analytics service. |

## Enhanced Skill Content


## Question Mapping

- "How do I add a new input to my Stream Analytics job?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}
- "How do I update an existing input's configuration?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}
- "How do I remove an input from a streaming job?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}
- "How do I get details about a specific input?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}
- "How do I list all inputs for a streaming job?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs
- "How do I test if an input connection is working?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}/test
- "Can I create an input only if it doesn't already exist?" -> PUT .../{inputName} (use `If-None-Match: *` header)
- "How do I update an input only if it hasn't changed since I last read it?" -> PATCH .../{inputName} (use `If-Match` header with ETag)
- "How do I replace an input configuration entirely?" -> PUT .../{inputName} (use `If-Match` header for conditional replace)
- "How do I filter which properties are returned when listing inputs?" -> GET .../inputs (use `$select` query parameter)
- "How do I verify my Event Hub input is reachable before starting the job?" -> POST .../{inputName}/test
- "How do I check if a specific input exists in my job?" -> GET .../{inputName} (check for 200 vs 404)
- "How do I switch an input from Blob Storage to Event Hub?" -> PUT .../{inputName} with new input body and `If-Match` header

## Response Tips

- **PUT (Create/Replace):** Returns 200 for updates, 201 for newly created resources. Always capture the ETag from response headers for subsequent conditional operations.
- **PATCH (Update):** Returns 200 with the full updated resource. Partial payloads are merged with existing config -- omitted fields are not deleted.
- **DELETE:** Returns 200 if the resource was deleted, 204 if it did not exist. Both are success -- do not treat 204 as an error.
- **GET (Single):** Returns 200 with full input definition including nested `properties` object containing datasource type and serialization settings.
- **GET (List):** Returns 200 with a `value` array. Use `$select` to reduce payload size. Watch for `nextLink` if pagination is present.
- **POST (Test):** Returns 200 with immediate test results, or 202 if the test is asynchronous -- poll the `Location` header URL for completion.

## Anomaly Flags

- **202 on test endpoint:** The connection test is running asynchronously. Surface this to the user and suggest polling the Location header rather than assuming success.
- **ETag mismatch (412 Precondition Failed):** The resource was modified by another process since last read. Alert the user to re-fetch before retrying.
- **DELETE returning 204:** The input did not exist. Flag if the user expected it to be present -- may indicate a naming mismatch or prior deletion.
- **Test failures:** If POST /test returns a status indicating connection failure, proactively surface datasource configuration issues (wrong connection string, missing permissions, unreachable endpoint).
- **Missing `api-version` parameter:** All endpoints require it as a common field. Flag immediately if omitted -- requests will fail with 400.
- **OAuth token expiry:** Auth is OAuth2. Surface token refresh needs if requests start returning 401.

## Playbook

### 1. Add and Verify a New Input

1. PUT `/subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.StreamAnalytics/streamingjobs/{job}/inputs/{inputName}` with the full input body (datasource config, serialization)
2. Confirm a 201 response (created) and capture the ETag from response headers
3. POST `.../inputs/{inputName}/test` to verify the connection
4. If 202 is returned, poll the Location header until the test completes
5. Check the test result status -- resolve any connectivity issues before starting the job

### 2. Safely Update an Existing Input

1. GET `.../inputs/{inputName}` to retrieve the current configuration and ETag
2. PATCH `.../inputs/{inputName}` with only the changed properties, passing `If-Match: {etag}` header
3. If 412 is returned, re-fetch the input (step 1) and retry with the new ETag
4. POST `.../inputs/{inputName}/test` to confirm the updated configuration still connects

### 3. Replace an Input Source Type

1. GET `.../inputs/{inputName}` to retrieve the current ETag
2. PUT `.../inputs/{inputName}` with the complete new input definition (e.g., switching from Blob to Event Hub), passing `If-Match: {etag}`
3. Confirm 200 response and capture the new ETag
4. POST `.../inputs/{inputName}/test` to validate the new datasource connection

### 4. Audit All Inputs on a Job

1. GET `.../inputs` with `$select` to list all inputs (optionally filter returned properties)
2. For each input in the `value` array, POST `.../inputs/{inputName}/test`
3. Collect test results, flagging any inputs with failed connections
4. Report summary: total inputs, passing, failing, and any returning 202 (still testing)

### 5. Clean Up Unused Inputs

1. GET `.../inputs` to list all inputs on the job
2. Identify inputs to remove based on naming convention or datasource type
3. For each target, DELETE `.../inputs/{inputName}`
4. Confirm 200 (deleted) or 204 (already absent) for each
5. GET `.../inputs` again to verify the final input list matches expectations


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
