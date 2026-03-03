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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets | Lists a collection of API Version Sets in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId} | Gets the entity state (Etag) version of the Api Version Set specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId} | Gets the details of the Api Version Set specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId} | Creates or Updates a Api Version Set. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId} | Updates the details of the Api VersionSet specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId} | Deletes specific Api Version Set. |

## Enhanced Skill Content
## Question Mapping

- "What API version sets exist in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets
- "List all version sets with a filter?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets (use $filter)
- "Does a specific API version set exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "Get details of a specific API version set?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How do I create a new API version set?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How do I replace an existing API version set?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How do I update properties of an API version set without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How do I delete an API version set?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How can I check if a version set ID is already taken before creating one?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How do I rename or change the versioning scheme of an existing version set?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apiVersionSets/{versionSetId}
- "How do I migrate APIs from one version set to another?" -> GET the source version set, PUT a new version set, then reassign APIs individually
- "How do I list version sets filtered by display name?" -> GET /...apiVersionSets with $filter=properties/displayName eq 'name'
- "How do I clean up unused version sets?" -> GET all version sets, then DELETE each unused one

## Response Tips

- **List (GET collection):** Returns a paged array; check `nextLink` for continuation. Each item includes `id`, `name`, `type`, and `properties` nested object containing `displayName`, `versioningScheme`, `versionHeaderName`, and `versionQueryName`.
- **Get (GET single):** Returns the full resource with an `ETag` header -- capture this value for conditional updates via `If-Match` on PATCH/PUT/DELETE.
- **Head (existence check):** Returns 200 with no body if the resource exists; expect 404 if it does not. Use this to avoid heavier GET calls when you only need presence confirmation.
- **Create/Replace (PUT):** Returns 201 for newly created resources, 200 for replacements of existing ones. Inspect the status code to determine which occurred.
- **Update (PATCH):** Returns 204 No Content on success -- there is no response body. Re-fetch with GET if you need the updated state.
- **Delete (DELETE):** Returns 200 or 204 on success. A 404 may indicate the resource was already removed; treat this as idempotent.
- **Errors:** Azure ARM errors return a structured `error` object with `code` and `message`. Watch for `ResourceNotFound`, `ValidationError`, and `ConflictError`.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed):** The resource was modified between your GET and PUT/PATCH/DELETE. Surface this immediately and suggest re-reading the resource before retrying.
- **Throttling (429 Too Many Requests):** Azure ARM enforces per-subscription rate limits. Surface the `Retry-After` header value and pause before retrying.
- **404 on HEAD or GET single:** The version set may have been deleted externally. Flag this if it was expected to exist based on a prior list call.
- **Unexpected 409 Conflict on PUT:** The versionSetId is already in use. Suggest checking with HEAD first or choosing a different ID.
- **Preview API version (2019-12-01-preview):** This is a preview release -- flag that behaviors may change, and recommend checking for a GA version if stability is required.
- **Empty list with active $filter:** If the filtered collection returns zero results, surface whether the filter syntax may be incorrect (OData filter pitfalls).
- **Long nextLink chains:** If pagination exceeds 5 pages, flag the unusually large number of version sets as a potential governance concern.

## Playbook

### 1. Create a New API Version Set

1. Choose a `versionSetId` (lowercase alphanumeric, hyphens allowed).
2. HEAD `/...apiVersionSets/{versionSetId}` to confirm the ID is not already taken (expect 404).
3. PUT `/...apiVersionSets/{versionSetId}` with a body specifying `displayName`, `versioningScheme` (Segment, Query, or Header), and scheme-specific fields (`versionQueryName` or `versionHeaderName`).
4. Confirm a 201 response. Capture the returned `ETag` for future updates.

### 2. Update a Version Set's Display Name

1. GET `/...apiVersionSets/{versionSetId}` to retrieve the current state and `ETag`.
2. PATCH `/...apiVersionSets/{versionSetId}` with the `If-Match: {ETag}` header and a body containing only the changed `displayName`.
3. Confirm a 204 response.
4. Optionally GET the resource again to verify the change took effect.

### 3. Audit and Clean Up Unused Version Sets

1. GET `/...apiVersionSets` to list all version sets (follow `nextLink` pagination until exhausted).
2. For each version set, cross-reference against your known API assignments to identify orphaned sets.
3. For each orphaned version set, GET it to capture its `ETag`.
4. DELETE `/...apiVersionSets/{versionSetId}` with `If-Match: {ETag}`.
5. Confirm 200 or 204 for each deletion.

### 4. Check If a Version Set Exists Before Referencing It

1. HEAD `/...apiVersionSets/{versionSetId}` with the target ID.
2. If 200: the version set exists and can be referenced by APIs.
3. If 404: create it first using the "Create a New API Version Set" playbook above.

### 5. List and Filter Version Sets by Versioning Scheme

1. GET `/...apiVersionSets?$filter=properties/versioningScheme eq 'Query'` to find all query-parameter-based version sets.
2. Page through results using `nextLink` if present.
3. For each result, GET the individual version set if you need full details including associated API references.
4. Repeat with different scheme values (`Segment`, `Header`) to get a complete inventory by type.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
