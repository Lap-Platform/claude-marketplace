---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 25 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products -- verify access

## Endpoints

25 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products | Lists a collection of products in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId} | Gets the entity state (Etag) version of the product specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId} | Gets the details of the product specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId} | Creates or Updates a product. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId} | Update existing product details. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId} | Delete product. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis | Lists a collection of the APIs associated with a product. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis/{apiId} | Checks that API entity specified by identifier is associated with the Product entity. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis/{apiId} | Adds an API to the specified product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis/{apiId} | Deletes the specified API from the specified product. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/groups | Lists the collection of developer groups associated with the specified product. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/groups/{groupId} | Checks that Group entity specified by identifier is associated with the Product entity. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/groups/{groupId} | Adds the association between the specified developer group with the specified product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/groups/{groupId} | Deletes the association between the specified group and product. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/subscriptions | Lists the collection of subscriptions to the specified product. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies | Get the policy configuration at the Product level. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies/{policyId} | Get the ETag of the policy configuration at the Product level. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies/{policyId} | Get the policy configuration at the Product level. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies/{policyId} | Creates or updates policy configuration for the Product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies/{policyId} | Deletes the policy configuration at the Product. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/tags | Lists all Tags associated with the Product. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/tags/{tagId} | Gets the entity state version of the tag specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/tags/{tagId} | Get tag associated with the Product. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/tags/{tagId} | Assign tag to the Product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/tags/{tagId} | Detach the tag from the Product. |

## Enhanced Skill Content
## Question Mapping

- "What products exist in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products
- "Does a specific product exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}
- "Get details for a specific product" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}
- "How do I create a new product in API Management?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}
- "How do I update an existing product's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}
- "How do I delete a product and optionally its subscriptions?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}
- "Which APIs are associated with a product?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis
- "How do I add an API to a product?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis/{apiId}
- "How do I remove an API from a product?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/apis/{apiId}
- "Which groups have access to a product?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/groups
- "How do I grant a group access to a product?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/groups/{groupId}
- "Who is subscribed to a product?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/subscriptions
- "What policies are applied to a product?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies
- "How do I set or update a policy on a product?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/policies/{policyId}
- "What tags are assigned to a product?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/products/{productId}/tags

## Response Tips

- **Product listings** (GET .../products): Returns a paged collection. Check `nextLink` for additional pages. Use `$filter` (OData syntax), `expandGroups`, and `tags` query params to narrow results.
- **Product CRUD** (PUT/PATCH/DELETE .../products/{productId}): PUT returns 201 on create, 200 on replace. PATCH returns 204 with no body. DELETE accepts `deleteSubscriptions` flag to cascade-remove subscriptions; returns 200 or 204.
- **Sub-resource listings** (apis, groups, subscriptions, policies, tags): All return paged collections with `$filter` support. Expect `value` array and optional `nextLink`.
- **HEAD checks** (all HEAD endpoints): Return no body. 200 or 204 confirms existence; 404 means not found. Use these for lightweight existence checks before mutations.
- **Association endpoints** (PUT/DELETE .../apis/{apiId}, .../groups/{groupId}, .../tags/{tagId}): PUT with no body to create a link. 201 means newly associated, 200 means already existed. DELETE returns 200 or 204 on success.
- **Policy endpoints** (PUT .../policies/{policyId}): Requires `parameters` body with XML policy content. The `policyId` is typically the literal string `policy`.

## Anomaly Flags

- **Subscription cascade risk**: DELETE on a product with `deleteSubscriptions=true` permanently removes all developer subscriptions. Surface a warning before executing.
- **Preview API version**: This spec targets `2019-12-01-preview`. Flag that behavior may change in GA and responses may include experimental fields.
- **Silent 204 responses**: PATCH and several DELETE operations return 204 with no body. If an agent expects confirmation data, flag that success must be inferred from the status code alone.
- **Orphaned associations**: When deleting a product, APIs, groups, and tags are disassociated but not deleted. Flag if a product has active subscriptions or linked APIs that may become unreachable.
- **OData filter failures**: Invalid `$filter` syntax returns 400 errors. Surface malformed filter expressions proactively when constructing requests.
- **Missing If-Match headers**: PATCH and DELETE on products typically require `If-Match: *` or an ETag value. A 412 Precondition Failed indicates a stale or missing ETag -- surface this with remediation steps.

## Playbook

### 1. Create a product and configure it end-to-end

1. PUT .../products/{productId} with `parameters` body containing display name, description, state (published/notPublished), and approval/subscription requirements.
2. PUT .../products/{productId}/apis/{apiId} to associate one or more APIs with the product.
3. PUT .../products/{productId}/groups/{groupId} to grant access to developer groups (e.g., Developers, Guests).
4. PUT .../products/{productId}/policies/policy with XML policy body (rate-limit, quota, etc.).
5. PUT .../products/{productId}/tags/{tagId} to apply organizational tags.
6. GET .../products/{productId} to verify the final configuration.

### 2. Audit a product's access and subscriptions

1. GET .../products/{productId} to retrieve product details and state.
2. GET .../products/{productId}/groups to list all groups with access.
3. GET .../products/{productId}/subscriptions to list all active developer subscriptions.
4. GET .../products/{productId}/apis to confirm which APIs are exposed.
5. GET .../products/{productId}/policies to review applied rate limits and quotas.

### 3. Safely delete a product

1. GET .../products/{productId}/subscriptions to check for active subscriptions.
2. If subscriptions exist, decide whether to migrate or cascade-delete them.
3. GET .../products/{productId}/apis to document associated APIs (they will be disassociated, not deleted).
4. PATCH .../products/{productId} to set state to `notPublished` first (prevents new subscriptions).
5. DELETE .../products/{productId}?deleteSubscriptions=true (or false to reject if subscriptions remain).

### 4. Move an API between products

1. HEAD .../products/{sourceProductId}/apis/{apiId} to confirm the API is currently associated.
2. DELETE .../products/{sourceProductId}/apis/{apiId} to remove the association.
3. PUT .../products/{targetProductId}/apis/{apiId} to add the API to the target product.
4. HEAD .../products/{targetProductId}/apis/{apiId} to verify the new association (expect 204).

### 5. Bulk-tag products for organization

1. GET .../products with `$filter` to retrieve products matching a criteria (e.g., by name pattern or state).
2. For each product in the results, HEAD .../products/{productId}/tags/{tagId} to check if the tag already exists.
3. For products missing the tag, PUT .../products/{productId}/tags/{tagId} to apply it.
4. GET .../products?tags={tagId} to verify all target products now carry the tag.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
