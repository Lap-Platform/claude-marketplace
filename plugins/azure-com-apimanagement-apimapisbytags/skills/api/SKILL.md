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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags | Lists a collection of apis associated with tags. |

## Enhanced Skill Content
## Question Mapping

- "What APIs are available in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags
- "How do I list APIs grouped by their tags?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags
- "Which APIs have a specific tag assigned?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags with $filter
- "How do I find untagged APIs in my service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags with includeNotTaggedApis=true
- "Can I filter APIs by display name or tag?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags with $filter
- "How do I audit which APIs lack proper tagging?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags with includeNotTaggedApis=true
- "What tags are in use across my API Management instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags (extract unique tags from response)
- "How do I get APIs for a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags (set resourceGroupName)
- "How many APIs are associated with each tag?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags (aggregate tag counts from response)
- "Are there APIs in my service that have no tag and might be missed in governance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags with includeNotTaggedApis=true, then filter for untagged entries
- "How do I compare tagged vs untagged API counts?" -> Call endpoint twice (with and without includeNotTaggedApis) and diff the results
- "What OData filter expressions can I use to narrow API results?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags with $filter (supports OData syntax)

## Response Tips

- **APIs by Tags (200):** Response is a paged collection with `value` array and optional `nextLink` for pagination. Each item contains both `tag` and `api` nested objects. Always check for `nextLink` and follow it to retrieve all pages. When `includeNotTaggedApis=true`, untagged APIs appear with an empty or absent `tag` property. The `$filter` parameter uses OData syntax (e.g., `name eq 'my-api'`). Non-200 responses follow Azure standard `ErrorResponse` with `error.code` and `error.message`.

## Anomaly Flags

- **Untagged APIs detected:** When `includeNotTaggedApis=true` returns APIs with no tag association, flag these as governance gaps that may indicate APIs bypassing tagging policy.
- **Large result sets / excessive pagination:** If `nextLink` appears repeatedly, the service may have an unusually high number of APIs -- surface this as a potential cost or management concern.
- **Throttling (429):** Azure ARM endpoints enforce rate limits. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.
- **Authorization failures (401/403):** Flag immediately -- the OAuth2 token may be expired, scoped incorrectly, or the caller may lack `Microsoft.ApiManagement/service/apis/read` permission.
- **Preview API version:** This spec uses `2019-12-01-preview`. Surface a warning that preview APIs may change without notice and recommend checking for a GA version.
- **Empty results with no error:** If `value` is an empty array, flag that the service name, resource group, or subscription may be incorrect rather than silently returning nothing.

## Playbook

### 1. Inventory All APIs by Tag

1. Authenticate and obtain an OAuth2 bearer token with `https://management.azure.com/.default` scope.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/apisByTags` with `includeNotTaggedApis=true`.
3. Parse the `value` array. Each entry contains a `tag` object (name, id) and an `api` object (name, displayName, path, protocols).
4. If `nextLink` is present in the response, follow it with a GET request to retrieve the next page.
5. Repeat until no `nextLink` is returned.
6. Group results by `tag.name` to produce a complete tag-to-API mapping.

### 2. Find and Report Untagged APIs

1. Call the endpoint with `includeNotTaggedApis=true`.
2. Filter the results for entries where the `tag` property is null or empty.
3. Collect the `api.name` and `api.displayName` for each untagged API.
4. Present the list to the user as a governance action item -- these APIs may need tags for discoverability and policy compliance.

### 3. Filter APIs by a Specific Criterion

1. Determine the OData filter expression (e.g., `$filter=name eq 'petstore'` or `$filter=apiRevision eq '2'`).
2. URL-encode the filter value and pass it as the `$filter` query parameter.
3. Call the endpoint and inspect the `value` array for matching results.
4. If results are empty, suggest broadening the filter or verifying the field name against Azure API Management documentation.

### 4. Monitor Tag Coverage Over Time

1. Call the endpoint with `includeNotTaggedApis=true` and page through all results.
2. Count total APIs and total untagged APIs.
3. Compute the tag coverage percentage: `(total - untagged) / total * 100`.
4. Compare against previous runs (store results externally) to track whether tagging discipline is improving or regressing.
5. Flag if coverage drops below an acceptable threshold (e.g., 80%).


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
