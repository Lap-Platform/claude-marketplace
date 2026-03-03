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
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs -- verify access
3. POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}/test -- create first test

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName} | Creates an output or replaces an already existing output under an existing streaming job. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName} | Updates an existing output under an existing streaming job. This can be used to partially update (ie. update one or two properties) an output without affecting the rest the job or output definition. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName} | Deletes an output from the streaming job. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName} | Gets details about the specified output. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs | Lists all of the outputs under the specified streaming job. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}/test | Tests whether an output’s datasource is reachable and usable by the Azure Stream Analytics service. |

## Enhanced Skill Content


## Question Mapping

- "How do I create a new output for my Stream Analytics job?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}
- "How do I update an existing output configuration?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}
- "How do I delete an output from my streaming job?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}
- "How do I get details about a specific output?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}
- "How do I list all outputs for a Stream Analytics job?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs
- "How do I test if an output connection is working?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/outputs/{outputName}/test
- "Can I create an output only if it doesn't already exist?" -> PUT .../outputs/{outputName} (use `If-None-Match: *` header)
- "How do I update an output only if it hasn't changed since I last read it?" -> PATCH .../outputs/{outputName} (use `If-Match` with ETag value)
- "How do I replace an output configuration entirely?" -> PUT .../outputs/{outputName} (use `If-Match` with ETag for safe overwrite)
- "How do I filter which properties are returned when listing outputs?" -> GET .../outputs (use `$select` query parameter)
- "How do I verify my Blob Storage output sink is configured correctly?" -> POST .../outputs/{outputName}/test
- "How do I check if a specific output exists before modifying it?" -> GET .../outputs/{outputName} (check for 200 vs 404)
- "How do I remove all outputs from a job?" -> GET .../outputs then DELETE each output individually

## Response Tips

- **PUT/Create**: 200 means updated existing, 201 means created new -- check status to confirm which occurred. Response body contains the full output resource with ETag.
- **PATCH/Update**: Always returns 200 with the merged resource. Compare returned ETag with your `If-Match` value to confirm the update took effect.
- **DELETE**: 200 means successfully deleted, 204 means the output was already gone -- both are success. No response body.
- **GET single**: Returns the full output resource including `properties.datasource` (sink config), `properties.serialization`, and `properties.etag`. Use the ETag for conditional operations.
- **GET list**: Returns a `value` array of output resources. May include `nextLink` for pagination -- follow it until absent. Use `$select` to reduce payload size.
- **POST test**: 200 means test completed (check `properties.status` for pass/fail), 202 means test is running asynchronously -- poll the `Location` header URL for results.

## Anomaly Flags

- **202 on test endpoint**: The connection test is running asynchronously. Surface the `Location` header and remind the user to poll for completion rather than assuming success.
- **ETag mismatch (412 Precondition Failed)**: Another process modified the output since it was last read. Surface this immediately -- the user needs to re-fetch before retrying.
- **204 on DELETE**: The output did not exist. Flag this if the user expected it to be present, as it may indicate a naming mismatch or prior deletion.
- **PUT returning 200 instead of 201**: The output already existed and was overwritten. If the user intended to create a new output, warn that they replaced an existing one.
- **Test result with error status**: Even when the POST returns 200, the test itself may report a failure in the response body. Always inspect `properties.error` or `properties.status`.
- **Missing `nextLink` awareness**: When listing outputs, if results seem incomplete, verify pagination was followed to completion.

## Playbook

### 1. Create and Validate a New Output

1. PUT `/subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.StreamAnalytics/streamingjobs/{job}/outputs/{outputName}` with the output definition body and `If-None-Match: *` to avoid overwriting an existing output
2. Confirm you receive a 201 (created) rather than 200 (replaced existing)
3. POST `.../outputs/{outputName}/test` to validate the connection
4. If you get 202, poll the `Location` header URL until the test completes
5. Check the test result for `properties.status` -- resolve any errors before starting the job

### 2. Safely Update an Output Configuration

1. GET `.../outputs/{outputName}` to retrieve the current configuration and its ETag
2. PATCH `.../outputs/{outputName}` with only the changed properties, passing the ETag in `If-Match`
3. If you receive 412, re-fetch the output and reapply your changes against the latest version
4. POST `.../outputs/{outputName}/test` to verify the updated configuration still connects successfully

### 3. Audit and Clean Up Unused Outputs

1. GET `.../outputs` to list all outputs for the job (follow `nextLink` for pagination)
2. For each output, review `properties.datasource.type` and connection settings
3. DELETE `.../outputs/{outputName}` for any outputs that are no longer needed
4. Confirm each delete returns 200 (verify no 204s indicating already-missing outputs)

### 4. Migrate an Output to a New Destination

1. GET `.../outputs/{outputName}` to capture the full current configuration
2. POST `.../outputs/{outputName}/test` to confirm the existing output still works (for baseline)
3. PATCH `.../outputs/{outputName}` with the new datasource properties, using `If-Match` with the current ETag
4. POST `.../outputs/{outputName}/test` to validate the new destination
5. If the test fails, PATCH back to the original configuration using the saved data from step 1

### 5. Replace an Output Entirely

1. GET `.../outputs/{outputName}` to capture the current ETag
2. PUT `.../outputs/{outputName}` with the complete new output definition and `If-Match` set to the current ETag
3. Confirm you receive 200 (replaced) -- if 201, the original was unexpectedly missing
4. POST `.../outputs/{outputName}/test` to verify the replacement output connects correctly


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
