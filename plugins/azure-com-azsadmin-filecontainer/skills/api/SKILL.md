---
name: deploymentadminclient
description: "DeploymentAdminClient API skill. Use when working with DeploymentAdminClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# DeploymentAdminClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers | Returns an array of file containers. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId} | Retrieves the specific file container details. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId} | Creates a new file container. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId} | Deletes specified file container. |

## Enhanced Skill Content
## Question Mapping

- "What file containers exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers
- "List all deployment file containers" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers
- "Get details for a specific file container" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Show me file container {id}" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Does file container {id} exist?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Create a new file container" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Upload a file container with these parameters" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Update an existing file container" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Replace file container {id} configuration" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Delete file container {id}" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "Remove a deployment file container" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}
- "How do I clean up unused file containers?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers then DELETE for each
- "Verify a file container was created successfully" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}

## Response Tips

- **List (GET collection):** Returns 200 with an array of file container resources. Check for `value` array and `nextLink` for pagination if the result set is large.
- **Get (GET by ID):** Returns 200 with a single file container object. A 404 means the container does not exist -- use this to check existence before PUT or DELETE.
- **Create/Update (PUT):** Returns 200 for synchronous completion or 202 for accepted (async provisioning). On 202, check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Delete (DELETE):** Returns 200 for immediate deletion or 204 if the resource was already gone (idempotent). Treat both as success.

## Anomaly Flags

- **202 Accepted on PUT:** The file container creation is running asynchronously. Surface this to the user and suggest polling the operation URL from response headers until terminal state.
- **204 on DELETE:** The file container was already deleted or never existed. Flag if the user expected the resource to be present, as it may indicate a stale reference.
- **Authentication failures (401/403):** OAuth2 token may be expired or the service principal lacks `Microsoft.Deployment.Admin` permissions. Surface immediately with remediation steps.
- **Throttling (429):** Azure ARM has per-subscription rate limits. If encountered, surface the `Retry-After` header value and pause before retrying.
- **Missing subscriptionId:** All endpoints require `subscriptionId` in the path. Flag early if the subscription context is not set or looks malformed (should be a UUID).
- **Empty list response:** If GET collection returns zero file containers, proactively note this -- the subscription may not have Deployment Admin enabled or may be targeting the wrong region.

## Playbook

### 1. Create a New File Container

1. Choose a `fileContainerId` (unique identifier for the container).
2. Build the `fileContainerParameters` map with the required configuration (source URI, post-copy action, etc.).
3. Call PUT `/subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}` with the parameters in the request body.
4. If the response is 200, the container is ready. If 202, extract the async operation URL from response headers.
5. Poll the operation URL until the provisioning state is `Succeeded` or `Failed`.
6. Confirm by calling GET on the same `fileContainerId` to verify the final state.

### 2. List and Inspect All File Containers

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers` to retrieve all containers.
2. Iterate through the `value` array in the response.
3. If `nextLink` is present, follow it to fetch additional pages.
4. For detailed inspection of any container, call GET with the specific `fileContainerId`.

### 3. Delete a File Container Safely

1. Call GET on the target `fileContainerId` to confirm it exists and review its current state.
2. Verify no active deployments depend on the file container.
3. Call DELETE `/subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/fileContainers/{fileContainerId}`.
4. A 200 confirms deletion. A 204 means it was already removed.
5. Optionally call GET again to confirm a 404, verifying the container is fully removed.

### 4. Update a File Container

1. Call GET on the target `fileContainerId` to retrieve its current configuration.
2. Modify the relevant fields in the `fileContainerParameters` map.
3. Call PUT with the full updated parameters (PUT is a full replace, not a patch).
4. Handle 200 (immediate) or 202 (async) as in the creation playbook.
5. Call GET to verify the updated configuration is reflected.

### 5. Bulk Cleanup of File Containers

1. Call GET on the collection to list all file containers.
2. Filter the results to identify containers that are unused, stale, or in a failed provisioning state.
3. For each container to remove, call DELETE with its `fileContainerId`.
4. Collect results -- log any unexpected responses (e.g., 404 for containers that were listed moments ago, indicating concurrent deletion).
5. Call GET on the collection again to confirm the remaining set matches expectations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
