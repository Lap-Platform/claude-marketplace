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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags | Lists a collection of tags defined within a service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId} | Gets the entity state version of the tag specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId} | Gets the details of the tag specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId} | Creates a tag. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId} | Updates the details of the tag specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId} | Deletes specific tag of the API Management service instance. |

## Enhanced Skill Content


## Question Mapping

- "What tags exist on my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags
- "How do I filter tags by name or scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags (use $filter and scope params)
- "Does a specific tag exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId}
- "Get details for a specific tag" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId}
- "How do I create a new tag?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId}
- "How do I rename or update a tag?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId}
- "How do I delete a tag?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId}
- "Can I check if a tag exists without fetching its full body?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tags/{tagId}
- "How do I list tags scoped to a specific API or product?" -> GET .../tags with scope parameter
- "How do I create a tag only if it doesn't already exist?" -> HEAD .../tags/{tagId} then conditionally PUT
- "What tags match a specific OData filter expression?" -> GET .../tags with $filter parameter
- "How do I bulk-update multiple tags?" -> Loop PATCH .../tags/{tagId} per tag (no bulk endpoint)
- "How do I replace a tag's properties entirely?" -> PUT .../tags/{tagId} with full parameters body

## Response Tips

- **List (GET .../tags):** Returns a paged collection; check `nextLink` for continuation URLs and loop until absent. Results may be filtered server-side via `$filter` OData syntax.
- **Existence check (HEAD):** 200 means the tag exists; 404 means it does not. No response body is returned -- rely solely on the status code.
- **Single resource (GET .../tags/{tagId}):** Returns the full tag entity with `id`, `name`, and `properties`. The `ETag` header can be used for conditional updates.
- **Create (PUT):** 201 indicates a new tag was created; 200 indicates an existing tag was updated. Inspect the status code to distinguish.
- **Update (PATCH):** 204 with no body on success. Pass `If-Match: *` or a specific ETag to avoid mid-air collisions.
- **Delete (DELETE):** 200 or 204 both indicate success. 404 means the tag was already gone.

## Anomaly Flags

- **Rate limiting:** Azure ARM throttles at 1200 reads and 1200 writes per hour per subscription. Surface `x-ms-ratelimit-remaining-subscription-reads` and `x-ms-ratelimit-remaining-subscription-writes` headers when values drop below 100.
- **ETag mismatch:** A 412 Precondition Failed on PATCH or DELETE means the resource was modified since last read. Prompt the user to re-fetch before retrying.
- **404 on targeted operations:** A 404 on GET/PATCH/DELETE for a specific tagId may indicate the tag was deleted externally or the tagId is misspelled. Surface this explicitly rather than silently failing.
- **Unexpected 409 Conflict:** On PUT, a 409 may indicate a naming collision or concurrent creation. Flag and suggest checking existing tags.
- **Deprecation headers:** Watch for `Sunset` or `Deprecation` headers in responses, signaling the 2019-12-01-preview API version is being retired.
- **Long $filter result sets:** If a filtered list returns a `nextLink`, warn that the filter may be too broad.

## Playbook

### 1. Create a new tag safely (check-then-create)

1. Call HEAD .../tags/{tagId} to check if the tag already exists.
2. If 200, the tag exists -- decide whether to skip or update via PATCH.
3. If 404, call PUT .../tags/{tagId} with the `parameters` body containing the display name.
4. Confirm creation by checking for a 201 status code in the response.

### 2. List and filter tags for a service

1. Call GET .../tags to retrieve the first page of tags.
2. Optionally pass `$filter` (e.g., `displayName eq 'production'`) or `scope` to narrow results.
3. If the response includes a `nextLink` property, call GET on that URL to fetch the next page.
4. Repeat until no `nextLink` is present.

### 3. Update a tag with concurrency protection

1. Call GET .../tags/{tagId} to retrieve the current tag and its `ETag` header.
2. Call PATCH .../tags/{tagId} with the updated `parameters` body and `If-Match` set to the retrieved ETag.
3. If 204, the update succeeded.
4. If 412, re-fetch the tag (step 1) and retry with the new ETag.

### 4. Delete a tag with pre-validation

1. Call HEAD .../tags/{tagId} to confirm the tag exists (200).
2. If 404, report that the tag is already absent -- no action needed.
3. Call DELETE .../tags/{tagId} with `If-Match: *` to force deletion regardless of version.
4. Confirm success via 200 or 204 status code.

### 5. Audit all tags across a service

1. Call GET .../tags (no filter) to retrieve all tags, paginating through `nextLink`.
2. For each tag, call GET .../tags/{tagId} to retrieve full details including properties.
3. Compile results into an inventory, flagging any tags with empty display names or unexpected property values.
4. Surface the total count and any anomalies to the user.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
