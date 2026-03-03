---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 1 endpoint."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources | Lists a collection of resources associated with tags. |

## Enhanced Skill Content
## Question Mapping

- "What tag resources exist for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources
- "List all tagged entities in a specific APIM instance" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources
- "How do I filter tag resources by a specific tag name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources with $filter
- "Which APIs are associated with a particular tag?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources with $filter=aid eq '/apis/{apiId}'
- "Show me tag-to-operation mappings for my service" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources
- "Can I see tag resources for a different resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources (swap resourceGroupName)
- "How do I audit which products are tagged in APIM?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources with $filter on product properties
- "What filter expressions does the tagResources endpoint accept?" -> GET ...tagResources with $filter (supports OData: `contains`, `eq`, `ne`, `and`, `or`)
- "List tag resources across multiple APIM services" -> Call GET ...tagResources once per serviceName, then merge results client-side
- "Are there any untagged APIs in my service?" -> GET ...tagResources, then diff against the full API list to find gaps
- "How do I check tag assignments changed after a deployment?" -> GET ...tagResources before and after, compare snapshots

## Response Tips

- **Tag Resources listing**: Response is a paged collection with `value` array and optional `nextLink` for continuation. Each item nests `tag`, `api`, `operation`, and `product` objects -- check which sub-object is populated to determine the entity type. Always follow `nextLink` until absent to retrieve the full set.
- **Errors**: 4xx responses return an `error` object with `code` and `message`. Watch for `ResourceNotFound` (wrong service/resource group name) and `AuthorizationFailed` (missing RBAC role on the APIM resource).
- **Filtering**: `$filter` uses OData syntax. Invalid expressions return 400 with a parsing error -- surface the raw `message` field, it pinpoints the exact position.

## Anomaly Flags

- **Pagination truncation**: If `nextLink` is present but the agent stops after one page, flag that results are incomplete.
- **Empty results with valid service**: A 200 with an empty `value` array on a known-active service may indicate no tags have been applied yet -- suggest the user verify tag configuration.
- **Preview API version**: This spec uses `2019-12-01-preview`. Flag if a newer stable version is available, as preview versions may be deprecated without notice.
- **Throttling headers**: Surface `Retry-After` or `x-ms-ratelimit-remaining-subscription-reads` headers when they appear. Alert when remaining reads drop below 50.
- **Filter returning full set**: If a `$filter` parameter was provided but the result count matches an unfiltered call, the filter expression may be malformed or vacuously true.

## Playbook

### 1. List all tag resources for an APIM service

1. Authenticate via OAuth2 and obtain a Bearer token with `Microsoft.ApiManagement/service/tagResources/read` permission.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/tagResources`.
3. Parse the `value` array from the 200 response.
4. If `nextLink` is present, repeat the GET using that URL until no `nextLink` is returned.
5. Combine all pages into the final result set.

### 2. Filter tag resources by a specific tag

1. Identify the tag display name you want to filter on.
2. Construct the OData filter: `$filter=tag/name eq '{tagName}'`.
3. Call `GET ...tagResources?$filter=tag/name eq '{tagName}'`.
4. Follow `nextLink` pagination as above.
5. Inspect each item's `api`, `operation`, or `product` sub-object to see what entity the tag is attached to.

### 3. Audit tag coverage across APIs

1. Retrieve all tag resources (see Playbook 1).
2. Extract the set of API IDs from items where the `api` sub-object is populated.
3. Separately list all APIs via the APIM APIs endpoint.
4. Diff the two sets -- APIs missing from the tag resources list have no tags assigned.
5. Report untagged APIs for governance review.

### 4. Compare tag assignments before and after a change

1. Call `GET ...tagResources` and store the full result as the "before" snapshot.
2. Perform the deployment, import, or manual tag change.
3. Call `GET ...tagResources` again for the "after" snapshot.
4. Diff the two snapshots by item ID to identify added, removed, or changed tag assignments.
5. Log the delta for audit purposes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
