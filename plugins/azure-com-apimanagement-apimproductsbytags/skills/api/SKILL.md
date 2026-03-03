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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags | Lists a collection of products associated with tags. |

## Enhanced Skill Content
## Question Mapping

- "What products are available in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags
- "How do I list products by tags in API Management?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags
- "Which products are tagged in my APIM instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags
- "How do I filter products by a specific tag?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags with $filter
- "Can I see products that have no tags assigned?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags with includeNotTaggedProducts=true
- "How do I find all untagged products in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags with includeNotTaggedProducts=true
- "What OData filters can I use on productsByTags?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags with $filter
- "How do I list products across a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags
- "How do I audit which tags are applied to which products?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags
- "What products exist under a given APIM service name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags
- "How do I get a combined view of tagged and untagged products?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags with includeNotTaggedProducts=true and no $filter
- "Can I search products by tag name in API Management?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags with $filter

## Response Tips

- **productsByTags**: Returns a paged collection of TagResourceContract objects. Each entry nests a `tag` object and a `product` object. Follow `nextLink` for pagination. Empty results return 200 with an empty `value` array, not 404. OData `$filter` errors surface as 400 with detailed error messages in the `error.details` array.

## Anomaly Flags

- **Pagination truncation**: If `nextLink` is present, the result set is incomplete. Surface this so the caller does not assume they have all products.
- **Empty tag associations**: If all returned items have null or empty `tag` fields, flag that tagging may not be configured on this service instance.
- **includeNotTaggedProducts omission**: When the caller asks about "all products" but omits `includeNotTaggedProducts=true`, warn that untagged products are excluded by default.
- **Throttling (429)**: Azure ARM APIs enforce per-subscription rate limits. If a 429 or `Retry-After` header appears, surface the wait duration and suggest backing off.
- **Preview API version**: This spec uses `2019-12-01-preview`. Flag that this is a preview version -- behavior may change, and callers should check for a GA release.
- **Subscription/resource mismatch (404)**: A 404 usually means the service name, resource group, or subscription ID is wrong rather than "no products found." Surface the distinction.

## Playbook

### 1. List All Products (Tagged and Untagged)

1. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/productsByTags` with `includeNotTaggedProducts=true`.
2. Parse the `value` array from the response.
3. Check for `nextLink` in the response body.
4. If `nextLink` exists, follow it with a GET request and append results.
5. Repeat until `nextLink` is absent.

### 2. Find Products with a Specific Tag

1. Identify the tag name you want to filter by.
2. Call the productsByTags endpoint with `$filter=tag/name eq '{tagName}'`.
3. Iterate through `value` entries; each contains both `tag` and `product` details.
4. Follow `nextLink` if present to collect all matches.

### 3. Audit Untagged Products

1. Call productsByTags with `includeNotTaggedProducts=true`.
2. Call productsByTags without `includeNotTaggedProducts` (defaults to false, returns only tagged).
3. Compare the two result sets -- products present in the first but absent in the second are untagged.
4. Surface untagged products for governance review.

### 4. Validate Service Configuration

1. Confirm the subscription ID, resource group name, and service name are correct by calling the endpoint with no filters.
2. If you get a 404, verify the resource exists in the Azure portal or via `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}`.
3. If you get a 200 with an empty `value` array and no `nextLink`, the service exists but has no tagged products. Retry with `includeNotTaggedProducts=true` to confirm whether any products exist at all.

### 5. Export Product-Tag Mapping

1. Call productsByTags with `includeNotTaggedProducts=true` to get the full set.
2. Follow all `nextLink` pages to collect every entry.
3. For each item in `value`, extract `tag.name` (or "untagged") and `product.name`.
4. Group results into a tag-to-products mapping for reporting or downstream automation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
