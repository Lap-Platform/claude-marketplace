---
name: streamanalyticsmanagementclient
description: "StreamAnalyticsManagementClient API skill. Use when working with StreamAnalyticsManagementClient for subscriptions. Covers 3 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} | Creates a transformation or replaces an already existing transformation under an existing streaming job. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} | Updates an existing transformation under an existing streaming job. This can be used to partially update (ie. update one or two properties) a transformation without affecting the rest the job or transformation definition. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} | Gets details about the specified transformation. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a transformation for my Stream Analytics job?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "How do I replace an existing transformation?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "How do I update a transformation without replacing it entirely?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "How do I change the query on an existing transformation?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "How do I get the details of a transformation?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "What streaming units does my transformation use?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "Can I create a transformation only if it doesn't already exist?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} (use If-None-Match: *)
- "How do I conditionally update a transformation based on its ETag?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} (use If-Match header)
- "How do I verify my transformation was created successfully?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "How do I set up a SELECT query transformation for my job?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "How do I scale my transformation's streaming units?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName}
- "Can I replace a transformation only if it already exists?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/transformations/{transformationName} (use If-Match header)

## Response Tips

- **PUT (create/replace)**: Returns 201 for newly created transformations and 200 for replacements. Check the response status to confirm which occurred. The response body includes the full transformation resource with an ETag header for subsequent conditional operations.
- **PATCH (update)**: Always returns 200 on success. The response body reflects the merged state after partial update. Capture the updated ETag from the response header for future conditional writes.
- **GET (retrieve)**: Returns 200 with the full transformation resource. The ETag header on the response is essential for safe concurrent updates via If-Match on PUT/PATCH.
- **Error responses**: Expect standard Azure error format with `error.code` and `error.message` fields. Common codes: 412 (precondition failed for If-Match/If-None-Match), 404 (job or transformation not found), 409 (conflict).

## Anomaly Flags

- **412 Precondition Failed**: Surface immediately when If-Match or If-None-Match conditions fail, indicating a concurrent modification conflict that requires re-fetching the resource.
- **404 on parent job**: If a transformation request returns 404, clarify whether the streaming job itself is missing versus the transformation, since both produce 404.
- **201 vs 200 on PUT**: Flag when a PUT returns 201 (created) if the caller expected to update an existing resource, as this means a new transformation was created unexpectedly.
- **Missing ETag in response**: Warn if a response lacks an ETag header, as this breaks the optimistic concurrency workflow for subsequent conditional updates.
- **api-version mismatch**: Flag if the user specifies an api-version other than 2016-03-01, as the behavior may differ or fail silently with unsupported versions.
- **Stale If-Match value**: If a PATCH or PUT with If-Match fails repeatedly, suggest re-fetching the resource to obtain the current ETag before retrying.

## Playbook

### 1. Create a New Transformation for a Streaming Job

1. Decide on the transformation name, query, and streaming units.
2. Call PUT with the `transformation` body containing `properties.query` (the SQL-like query) and `properties.streamingUnits`.
3. Optionally set `If-None-Match: *` to ensure the transformation does not already exist.
4. Confirm the response is 201 (created).
5. Save the ETag from the response header for future updates.

### 2. Safely Update a Transformation (Optimistic Concurrency)

1. Call GET to retrieve the current transformation and its ETag.
2. Prepare the partial update body with only the changed fields (e.g., updated query or streaming units).
3. Call PATCH with the `If-Match` header set to the ETag from step 1.
4. If 200, the update succeeded. Capture the new ETag.
5. If 412 (Precondition Failed), another process modified the resource. Return to step 1 and retry.

### 3. Inspect and Verify a Transformation Configuration

1. Call GET with the subscription, resource group, job name, and transformation name.
2. Inspect `properties.query` to verify the transformation SQL logic.
3. Check `properties.streamingUnits` to confirm the allocated compute capacity.
4. Note the ETag for any subsequent modifications.

### 4. Replace a Transformation Entirely

1. Call GET to confirm the transformation exists and to capture its ETag.
2. Construct the full replacement `transformation` body with all desired properties.
3. Call PUT with `If-Match` set to the current ETag to prevent overwriting concurrent changes.
4. Verify the response is 200 (replaced, not 201 which would indicate it was recreated after deletion).
5. Store the new ETag from the response.

### 5. Scale Streaming Units on a Transformation

1. Call GET to retrieve the current transformation and its ETag.
2. Call PATCH with body `{ "properties": { "streamingUnits": <new_value> } }` and `If-Match` set to the current ETag.
3. Confirm 200 response and verify `properties.streamingUnits` in the response body matches the requested value.
4. Monitor the streaming job to ensure the scaling takes effect without errors.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
