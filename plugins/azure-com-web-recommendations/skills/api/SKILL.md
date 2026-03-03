---
name: recommendations-api-client
description: "Recommendations API Client API skill. Use when working with Recommendations API Client for subscriptions. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Recommendations API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations/reset -- create first reset

## Endpoints

15 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations | List all recommendations for a subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations/reset | Reset all recommendation opt-out settings for a subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations/{name}/disable | Disables the specified rule so it will not apply to a subscription in the future. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendationHistory | Get past recommendations for an app, optionally specified by the time range. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations | Get all recommendations for an app. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations/disable | Disable all recommendations for an app. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations/reset | Reset all recommendation opt-out settings for an app. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations/{name} | Get a recommendation rule for an app. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations/{name}/disable | Disables the specific rule for a web site permanently. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendationHistory | Get past recommendations for an app, optionally specified by the time range. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations | Get all recommendations for an app. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/disable | Disable all recommendations for an app. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/reset | Reset all recommendation opt-out settings for an app. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/{name} | Get a recommendation rule for an app. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/{name}/disable | Disables the specific rule for a web site permanently. |

## Enhanced Skill Content
## Question Mapping

- "What recommendations exist for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations
- "Show me only featured recommendations for my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations (with `featured=true`)
- "How do I reset all recommendation opt-outs for my subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations/reset
- "How do I disable a specific recommendation at the subscription level?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations/{name}/disable
- "What recommendations does my App Service site have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations
- "Show me the recommendation history for my web app" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendationHistory
- "Show only expired recommendations for my site" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendationHistory (with `expiredOnly=true`)
- "Get details on a specific recommendation for my site" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/{name}
- "Disable a recommendation for a specific web app" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/{name}/disable
- "Reset all disabled recommendations for my web app" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/recommendations/reset
- "What recommendations apply to my App Service Environment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations
- "Show recommendation history for my ASE" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendationHistory
- "Disable all recommendations for my hosting environment" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations/disable
- "Mark a specific ASE recommendation as seen and get its details" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{hostingEnvironmentName}/recommendations/{name} (with `updateSeen=true`)

## Response Tips

- **Recommendation lists** (GET .../recommendations): Returns paginated arrays; check for `nextLink` to retrieve additional pages. Each item includes rule name, severity, and action details.
- **Recommendation history** (GET .../recommendationHistory): Filtered by `expiredOnly` and `$filter` (OData); results are time-ordered. Empty arrays are valid when no historical entries exist.
- **Single recommendation** (GET .../recommendations/{name}): Returns a single object, not an array. Use `updateSeen=true` to mark it read as a side effect. The optional `recommendationId` disambiguates when multiple rules share a name.
- **Disable endpoints** (POST .../disable): Subscription-level disable returns 200 with the disabled rule object; site-level and ASE-level disable also return 200. Hosting environment bulk disable returns 204 with no body.
- **Reset endpoints** (POST .../reset): Always return 204 No Content with an empty body -- a successful reset has no response payload to parse.

## Anomaly Flags

- **204 vs 200 inconsistency**: Subscription-level disable returns 200 while ASE-level bulk disable returns 204. Agent should normalize this so callers do not assume a uniform response shape.
- **Missing `environmentName` parameter**: The ASE disable and reset endpoints require both `hostingEnvironmentName` (path) and `environmentName` (body/query). If only the path param is provided, the call will fail. Surface a warning when `environmentName` is omitted.
- **OAuth token expiry**: All endpoints require OAuth2. Agent should flag 401 responses and prompt for token refresh before retrying.
- **OData `$filter` errors**: Malformed filter strings return 400. Agent should surface the filter expression that failed and suggest valid OData syntax.
- **Stale recommendations after reset**: After calling a reset endpoint, previously cached recommendation lists are stale. Agent should proactively re-fetch recommendations.
- **Rate limiting (429)**: Azure ARM enforces per-subscription throttling. Agent should surface `Retry-After` headers and pause automatically.

## Playbook

### 1. Audit and triage all recommendations for a web app

1. GET `/subscriptions/{subscriptionId}/resourceGroups/{rg}/providers/Microsoft.Web/sites/{site}/recommendations` with `featured=true` to see high-priority items first.
2. Review each recommendation's severity and category.
3. GET `.../recommendations/{name}` with `updateSeen=true` for each item you want to investigate, marking it as read.
4. For recommendations you want to suppress, POST `.../recommendations/{name}/disable`.
5. Periodically GET `.../recommendationHistory` with `expiredOnly=true` to review what has lapsed.

### 2. Bulk reset disabled recommendations after a configuration change

1. Make your infrastructure or app configuration change.
2. POST `/subscriptions/{subscriptionId}/resourceGroups/{rg}/providers/Microsoft.Web/sites/{site}/recommendations/reset` to clear all previous opt-outs.
3. GET `.../recommendations` to fetch the fresh recommendation set reflecting the new configuration.
4. Review and selectively disable any that remain irrelevant.

### 3. Compare recommendations across subscription, site, and ASE scopes

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/recommendations` for the subscription-wide view.
2. GET `.../sites/{site}/recommendations` for site-specific recommendations.
3. GET `.../hostingEnvironments/{ase}/recommendations` for ASE-specific recommendations.
4. Diff the three result sets by recommendation `name` to identify scope-specific vs. shared recommendations.
5. Disable duplicates at the narrowest applicable scope to avoid alert noise.

### 4. Investigate a specific recommendation in an App Service Environment

1. GET `.../hostingEnvironments/{ase}/recommendations` to list all active ASE recommendations.
2. Identify the target recommendation by name.
3. GET `.../hostingEnvironments/{ase}/recommendations/{name}` with `updateSeen=true` and the `recommendationId` if available.
4. If the recommendation is not actionable, POST `.../hostingEnvironments/{ase}/recommendations/{name}/disable`.
5. Verify the disable took effect by re-fetching the recommendation list.

### 5. Monitor recommendation churn over time

1. GET `.../sites/{site}/recommendationHistory` periodically (e.g., daily) without `expiredOnly` to capture the full history.
2. Store results externally and compare across runs to detect new, resolved, or recurring recommendations.
3. GET `.../sites/{site}/recommendationHistory?expiredOnly=true` to isolate recommendations that have aged out.
4. Use `$filter` to narrow by date range (e.g., `creationTime ge 2026-02-01`) for focused analysis.
5. Surface any recommendation that keeps reappearing after resets as a persistent issue needing root-cause investigation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
