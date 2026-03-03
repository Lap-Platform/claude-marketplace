---
name: advisormanagementclient
description: "AdvisorManagementClient API skill. Use when working with AdvisorManagementClient for providers, subscriptions, {resourceUri}. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# AdvisorManagementClient
API version: 2017-04-19

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Advisor/metadata -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations -- create first generateRecommendations

## Endpoints

15 endpoints across 3 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Advisor/metadata/{name} | Gets the metadata entity. |
| GET | /providers/Microsoft.Advisor/metadata | Gets the list of metadata entities. |
| GET | /providers/Microsoft.Advisor/operations | Lists all the available Advisor REST API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/configurations | Retrieve Azure Advisor configurations. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/configurations | Create/Overwrite Azure Advisor configuration. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Advisor/configurations | Retrieve Azure Advisor configurations. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Advisor/configurations | Create/Overwrite Azure Advisor configuration. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations | Initiates the recommendation generation or computation process for a subscription. This operation is asynchronous. The generated recommendations are stored in a cache in the Advisor service. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations/{operationId} | Retrieves the status of the recommendation computation or generation process. Invoke this API after calling the generation recommendation. The URI of this API is returned in the Location field of the response header. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/recommendations | Obtains cached recommendations for a subscription. The recommendations are generated or computed by invoking generateRecommendations. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/suppressions | Retrieves the list of snoozed or dismissed suppressions for a subscription. The snoozed or dismissed attribute of a recommendation is referred to as a suppression. |

### {resourceUri}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId} | Obtains details of a cached recommendation. |
| GET | /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name} | Obtains the details of a suppression. |
| PUT | /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name} | Enables the snoozed or dismissed attribute of a recommendation. The snoozed or dismissed attribute is referred to as a suppression. Use this API to create or update the snoozed or dismissed status of a recommendation. |
| DELETE | /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name} | Enables the activation of a snoozed or dismissed recommendation. The snoozed or dismissed attribute of a recommendation is referred to as a suppression. |

## Enhanced Skill Content
## Question Mapping

- "What metadata is available for Azure Advisor?" -> GET /providers/Microsoft.Advisor/metadata
- "Get details about a specific Advisor metadata entity?" -> GET /providers/Microsoft.Advisor/metadata/{name}
- "What operations does Azure Advisor support?" -> GET /providers/Microsoft.Advisor/operations
- "How is Advisor configured for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/configurations
- "Update the Advisor configuration for my subscription?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/configurations
- "What is the Advisor configuration for a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Advisor/configurations
- "Set Advisor configuration at the resource group level?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Advisor/configurations
- "Generate fresh Advisor recommendations for my subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations
- "Is my recommendation generation job finished?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations/{operationId}
- "List all Advisor recommendations for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/recommendations
- "Get a specific recommendation for a resource?" -> GET /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}
- "Snooze or suppress a recommendation?" -> PUT /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name}
- "Check if a recommendation is already suppressed?" -> GET /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name}
- "Remove a suppression so a recommendation reappears?" -> DELETE /{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name}
- "List all active suppressions across my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Advisor/suppressions

## Response Tips

- **Metadata & Operations (GET /providers/...):** Returns JSON arrays; iterate `.value[]` for each metadata entity or operation definition.
- **Configurations (GET/PUT):** GET returns a list of config objects; PUT returns 204 No Content on success -- check status code only, no body. 400 means the `configContract` payload was malformed.
- **Generate Recommendations (POST + GET):** POST returns 202 with a `Location` header containing the `operationId` polling URL. The GET status endpoint returns 202 while in progress and 204 when complete.
- **Recommendations (GET):** Paginated via `$skipToken`; check `nextLink` in the response to retrieve additional pages. Use `$top` to control page size and `$filter` for category/impact filtering.
- **Suppressions (GET/PUT/DELETE):** GET and PUT return the suppression object (200). DELETE returns 204 with no body. The subscription-level list supports `$top` and `$skipToken` pagination.

## Anomaly Flags

- **202 persisting on generation status:** If the generation status endpoint keeps returning 202 after several minutes, surface a warning that recommendation generation may be stalled or the subscription has an unusually large resource set.
- **404 on metadata lookup:** The metadata entity name may be misspelled or deprecated; suggest listing all metadata first via the collection endpoint.
- **400 on configuration PUT:** Surface the full error body -- it typically contains field-level validation details that pinpoint the malformed property in `configContract`.
- **Empty recommendations list:** If GET recommendations returns zero results after a fresh generation completes, flag that the subscription may have no applicable recommendations or the `$filter` is too restrictive.
- **Pagination token loops:** If `$skipToken` values repeat across pages, flag a potential API-side pagination bug and stop iterating.
- **Suppression on nonexistent recommendation:** A PUT suppression returning an unexpected error may indicate the `recommendationId` is stale; recommend re-listing recommendations first.

## Playbook

### 1. Generate and Retrieve Fresh Recommendations

1. POST `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations` to kick off generation.
2. Extract the `operationId` from the `Location` response header.
3. Poll GET `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/generateRecommendations/{operationId}` until it returns 204 (complete).
4. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/recommendations` to retrieve the full list.
5. Page through results using `$skipToken` from `nextLink` until all recommendations are collected.

### 2. Suppress a Noisy Recommendation

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/recommendations` to find the target recommendation and note its `recommendationId` and `resourceUri`.
2. PUT `/{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name}` with a `suppressionContract` body specifying the suppression TTL.
3. Verify by GET on the same suppression path to confirm it was created.
4. Optionally list all suppressions via GET `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/suppressions` to confirm it appears.

### 3. Configure Advisor at Subscription and Resource Group Levels

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/configurations` to review current subscription-level settings.
2. PUT `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/configurations` with updated `configContract` (e.g., exclude certain resource types or change low-impact threshold).
3. Confirm 204 response.
4. For resource-group overrides, PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Advisor/configurations` with group-specific settings.
5. Verify by GET on the resource group configuration endpoint.

### 4. Audit and Clean Up Stale Suppressions

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/suppressions` to list all active suppressions, paging with `$skipToken` as needed.
2. For each suppression, check whether the underlying recommendation still exists via GET `/{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}`.
3. DELETE `/{resourceUri}/providers/Microsoft.Advisor/recommendations/{recommendationId}/suppressions/{name}` for any suppression tied to a stale or resolved recommendation.
4. Re-list suppressions to confirm cleanup.

### 5. Explore Available Advisor Capabilities

1. GET `/providers/Microsoft.Advisor/operations` to discover all supported API operations and their descriptions.
2. GET `/providers/Microsoft.Advisor/metadata` to list all metadata entities (recommendation categories, impact levels, etc.).
3. GET `/providers/Microsoft.Advisor/metadata/{name}` for detailed info on a specific entity.
4. Use the metadata to inform `$filter` values when querying recommendations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
