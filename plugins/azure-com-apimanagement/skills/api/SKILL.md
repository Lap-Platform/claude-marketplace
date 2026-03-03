---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2018-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies -- verify access

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies | Lists all the Global Policy definitions of the Api Management service. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Gets the entity state (Etag) version of the Global policy definition in the Api Management service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Get the Global policy definition of the Api Management service. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Creates or updates the global policy configuration of the Api Management service. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Deletes the global policy configuration of the Api Management Service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets | Lists all policy snippets. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions | Lists all azure regions in which the service exists. |

## Enhanced Skill Content
## Question Mapping

- "What policies are configured on my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies
- "List all policies scoped to a specific level?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies (with `scope` param)
- "Does a specific policy exist on my service?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Show me the details of a particular policy?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "How do I create a new policy on my API Management service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "How do I update an existing policy?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Remove a policy from my service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "What policy snippets are available for my service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets
- "What policy templates can I use at a given scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets (with `scope` param)
- "Which regions is my API Management service deployed to?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Check if a policy called 'policy' exists before I try to update it?" -> HEAD .../{policyId} then PUT .../{policyId}
- "Replace a policy only if I have the latest version?" -> DELETE .../{policyId} (requires `If-Match`) then PUT .../{policyId}
- "What scopes can I filter policies by?" -> GET .../policies (vary `scope` param) and GET .../policySnippets (vary `scope` param)

## Response Tips

- **Policy list/detail (GET policies):** Returns a collection with `value` array; each entry contains policy XML content, format, and scope metadata. Filter with `scope` to narrow results.
- **Policy existence (HEAD):** Returns 200 with no body if the policy exists; expect 404 if it does not. Use the `ETag` response header for subsequent conditional updates.
- **Policy create/update (PUT):** Returns 200 for updates, 201 for new creations. The response body contains the full policy resource. Always capture the returned `ETag` for future delete or update operations.
- **Policy delete (DELETE):** Returns 200 on successful deletion, 204 if already absent. Requires `If-Match` header -- pass `*` to skip concurrency checks or use the `ETag` from a prior GET/HEAD.
- **Policy snippets (GET):** Returns built-in policy templates as a collection; use `scope` to filter to relevant snippet categories.
- **Regions (GET):** Returns a flat list of region objects with `name` and metadata; no pagination expected for typical deployments.

## Anomaly Flags

- **ETag mismatch on DELETE:** A 412 Precondition Failed indicates the policy was modified since your last read -- re-fetch and confirm before retrying.
- **404 on policy GET after successful HEAD:** Race condition; another client may have deleted the policy between calls. Surface this to the user immediately.
- **201 vs 200 on PUT:** If the agent expected an update (200) but received 201, the policy did not previously exist -- flag this as unexpected creation.
- **Empty policy list with no scope filter:** The service may have no policies or they may all be scoped differently. Suggest retrying with explicit `scope` values.
- **Azure throttling (429):** Surface `Retry-After` header value and pause before retrying. Azure ARM APIs enforce per-subscription rate limits.
- **Deprecated api-version:** If the response includes `x-ms-deprecation` headers or warnings, alert the user to migrate to a newer API version.

## Playbook

### 1. Audit All Policies on a Service

1. GET `.../policies` to retrieve the full policy list
2. For each policy in the `value` array, note the `policyId` and `scope`
3. GET `.../policies/{policyId}` for each to inspect the full XML content
4. GET `.../regions` to understand which regions the policies apply to
5. Cross-reference policy scopes with regions for a complete audit view

### 2. Safely Update an Existing Policy

1. HEAD `.../policies/{policyId}` to confirm the policy exists
2. GET `.../policies/{policyId}` to retrieve current content and capture the `ETag` header
3. Modify the policy XML content locally
4. PUT `.../policies/{policyId}` with the updated `parameters` body
5. Verify the response is 200 (update) -- if 201, flag unexpected creation

### 3. Create a Policy from a Snippet Template

1. GET `.../policySnippets` with appropriate `scope` to list available templates
2. Select the desired snippet and adapt its XML content
3. HEAD `.../policies/{policyId}` to confirm the target policyId is not already taken
4. PUT `.../policies/{policyId}` with the adapted snippet as `parameters`
5. Verify 201 response confirming creation

### 4. Delete a Policy with Concurrency Safety

1. GET `.../policies/{policyId}` to retrieve the current resource and its `ETag`
2. DELETE `.../policies/{policyId}` with `If-Match` set to the retrieved `ETag`
3. If 200: deletion succeeded. If 204: policy was already absent. If 412: re-fetch and retry
4. GET `.../policies` to confirm the policy no longer appears in the list

### 5. Discover Service Topology and Policy Coverage

1. GET `.../regions` to list all deployment regions
2. GET `.../policies` without `scope` to get all policies
3. GET `.../policies?scope=Tenant` then `scope=Product` then `scope=Api` then `scope=Operation` to map policies by scope level
4. GET `.../policySnippets` to identify which built-in templates are available but not yet applied
5. Compile a coverage report showing regions, scopes with policies, and available unused snippets


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
