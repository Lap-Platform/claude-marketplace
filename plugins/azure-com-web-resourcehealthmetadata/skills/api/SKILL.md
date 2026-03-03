---
name: resourcehealthmetadata-api-client
description: "ResourceHealthMetadata API Client API skill. Use when working with ResourceHealthMetadata API Client for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# ResourceHealthMetadata API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/resourceHealthMetadata -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/resourceHealthMetadata | List all ResourceHealthMetadata for all sites in the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/resourceHealthMetadata | List all ResourceHealthMetadata for all sites in the resource group in the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata | Gets the category of ResourceHealthMetadata to use for the given site as a collection |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata/default | Gets the category of ResourceHealthMetadata to use for the given site |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/slots/{slot}/resourceHealthMetadata | Gets the category of ResourceHealthMetadata to use for the given site as a collection |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/slots/{slot}/resourceHealthMetadata/default | Gets the category of ResourceHealthMetadata to use for the given site |

## Enhanced Skill Content
## Question Mapping

- "What resource health metadata exists across my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/resourceHealthMetadata
- "List all health metadata for resources in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/resourceHealthMetadata
- "What is the health metadata for a specific web app?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata
- "Get the default health metadata entry for my site?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata/default
- "What health metadata is associated with a deployment slot?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/slots/{slot}/resourceHealthMetadata
- "Get the default health metadata for a specific slot?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/slots/{slot}/resourceHealthMetadata/default
- "Is my web app reporting any health issues?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata/default
- "Compare health metadata between production and staging slots?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/slots/{slot}/resourceHealthMetadata/default (call twice with different slot values)
- "Which sites in my resource group have health metadata registered?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/resourceHealthMetadata
- "Does a particular deployment slot have health monitoring enabled?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/slots/{slot}/resourceHealthMetadata/default
- "Audit all resource health metadata across my entire subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/resourceHealthMetadata
- "Get health metadata for my app before and after a slot swap?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata/default (call before and after swap)

## Response Tips

- **Subscription/resource group list endpoints**: Return paginated `value` arrays with `nextLink` for continuation; always follow `nextLink` until null to get complete results.
- **Site-level list endpoints**: Return `value` arrays scoped to a single site or slot; typically small result sets but still check for `nextLink`.
- **Default (singleton) endpoints**: Return a single resource object with `id`, `name`, `type`, and `properties`; a 404 means no health metadata is configured for that resource.
- **All endpoints**: Require `api-version=2018-02-01` as a query parameter; omitting it returns a descriptive error with supported versions.
- **Error responses**: Follow Azure standard format with `error.code` and `error.message`; watch for `ResourceNotFound`, `ResourceGroupNotFound`, and `AuthorizationFailed`.

## Anomaly Flags

- **404 on default endpoint**: The site or slot has no resource health metadata configured -- surface this as a monitoring gap that may need attention.
- **Empty `value` arrays at subscription scope**: No Web Apps in the subscription have health metadata, which is unusual for production subscriptions and worth flagging.
- **Throttling (429 responses)**: Azure ARM has per-subscription rate limits; if encountered, surface the `Retry-After` header value and pause further calls.
- **Mismatched metadata between slot and production**: When comparing slot vs. production health metadata, flag any differences in the `properties` section as potential configuration drift.
- **Stale `api-version`**: The spec uses `2018-02-01`; if Azure returns a warning header suggesting a newer API version, surface it to the user.
- **Authorization errors (403)**: Often indicates the service principal or user lacks the `Microsoft.Web/sites/resourceHealthMetadata/read` permission -- surface the specific missing role.

## Playbook

### 1. Audit Health Metadata Across a Subscription

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/resourceHealthMetadata` to list all health metadata entries.
2. Follow any `nextLink` values to paginate through the full result set.
3. Group results by resource group (parse from the `id` field).
4. Flag any resource groups with zero entries as potential monitoring gaps.
5. Summarize total count and distribution across resource groups.

### 2. Check Health Metadata for a Specific Web App

1. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{name}/resourceHealthMetadata/default` to get the singleton entry.
2. If 404, report that no health metadata is configured for this app.
3. If 200, inspect `properties` for the health category and signal status.
4. Optionally compare against other apps in the same resource group by calling the resource-group-scoped list endpoint.

### 3. Compare Health Metadata Between Deployment Slots

1. Call the default endpoint for the production site: `GET .../sites/{name}/resourceHealthMetadata/default`.
2. Call the default endpoint for the target slot: `GET .../sites/{name}/slots/{slot}/resourceHealthMetadata/default`.
3. Diff the `properties` objects from both responses.
4. Flag any discrepancies as configuration drift that should be resolved before a slot swap.

### 4. Validate Health Monitoring After a Deployment

1. Before deploying, call the site-level default endpoint and save the response as a baseline.
2. Perform the deployment or slot swap.
3. After deployment completes, call the same endpoint again.
4. Compare the pre and post responses; flag any changes in health metadata properties.
5. If metadata disappeared (404), alert that health monitoring may have been disrupted.

### 5. Enumerate All Monitored Resources in a Resource Group

1. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/resourceHealthMetadata`.
2. Follow `nextLink` pagination until all results are collected.
3. Extract site names and slot names from the `id` field of each entry.
4. Cross-reference against the full list of sites in the resource group (via Microsoft.Web/sites API) to identify unmonitored apps.
5. Report coverage percentage and list any gaps.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
