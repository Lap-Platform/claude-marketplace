---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 2 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues | Lists a collection of issues in the specified service instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues/{issueId} | Gets API Management issue details |

## Enhanced Skill Content
## Question Mapping

- "What issues exist in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues
- "List all issues for a specific APIM instance" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues
- "Show me filtered issues using an OData expression" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues (with $filter)
- "Get details about a specific issue by ID" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues/{issueId}
- "What is the status of issue {issueId}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues/{issueId}
- "How many issues does my API Management service have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues
- "Are there any open issues in my APIM service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues (with $filter)
- "Show issues created by a specific user" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues (with $filter)
- "What details are available for issue {issueId}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues/{issueId}
- "List issues matching a specific state or title" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues (with $filter)
- "Does issue {issueId} still exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues/{issueId}
- "Which resource group contains my APIM issues?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues

## Response Tips

- **Issue list (200):** Returns a paged collection with `value` array and `nextLink` for pagination. Always check `nextLink` and follow it to retrieve all results. Each item contains `id`, `name`, `type`, and `properties` with issue details (title, description, state, createdDate, userId, apiId).
- **Issue detail (200):** Returns a single issue resource with full `properties` bag. Look for `state` (open/closed/proposed/removed), `createdDate`, and nested references to the originating API (`apiId`) and user (`userId`).
- **Errors:** Azure Resource Manager returns structured error objects with `error.code` and `error.message`. Common codes: `ResourceNotFound` (404 for bad issueId), `AuthorizationFailed` (403), `SubscriptionNotFound`. Always surface the inner `error.message` to the user.
- **Filtering:** The `$filter` parameter accepts OData expressions (e.g., `state eq 'open'`, `contains(title,'timeout')`). Invalid filter syntax returns 400 with a descriptive error message.

## Anomaly Flags

- **404 on issue detail:** The issueId may have been deleted or the resource path (subscription, resource group, service name) is incorrect. Surface the full resource path for the user to verify.
- **Empty issue list:** If `value` is an empty array, confirm the service name and resource group are correct before concluding there are no issues.
- **Pagination truncation:** If `nextLink` is present but the user only asked for a count or summary, warn that results are incomplete and offer to fetch all pages.
- **Preview API version (2019-12-01-preview):** This is a preview version. Flag that behavior may change and suggest checking for a GA version if stability is required.
- **Throttling (429):** Azure ARM enforces rate limits per subscription. If a 429 response is received, surface the `Retry-After` header value and wait before retrying.
- **Stale issue state:** If an issue shows `state: proposed` for an extended period (check `createdDate`), proactively note it may need triage.

## Playbook

### 1. Audit All Open Issues in a Service

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues` with `$filter=state eq 'open'`
2. Collect all items from `value` array
3. If `nextLink` is present, follow it repeatedly until no more pages remain
4. Summarize results: count, titles, creation dates, and associated APIs
5. Highlight any issues older than 30 days that may need attention

### 2. Investigate a Specific Issue

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/issues/{issueId}`
2. Extract `properties.title`, `properties.description`, `properties.state`, and `properties.createdDate`
3. Note the `properties.userId` to identify who reported the issue
4. Note the `properties.apiId` to identify which API is affected
5. Present a concise summary with state, age, reporter, and affected API

### 3. Compare Issue Volume Across Services

1. For each APIM service in the resource group, call GET `.../service/{serviceName}/issues`
2. Count total issues per service (follow all `nextLink` pages)
3. Optionally filter by `$filter=state eq 'open'` to focus on unresolved issues
4. Present a comparison table: service name, total issues, open issues
5. Flag any service with a disproportionately high issue count

### 4. Search Issues by Keyword

1. Call GET `.../issues` with `$filter=contains(title,'{keyword}')` to match titles
2. If no results, broaden to description: `$filter=contains(description,'{keyword}')`
3. Follow `nextLink` if results are paginated
4. Return matching issue IDs, titles, and states
5. Offer to fetch full details for any specific match

### 5. Verify an Issue Was Resolved

1. Call GET `.../issues/{issueId}` to retrieve the issue detail
2. Check `properties.state` -- expected value is `closed` or `removed`
3. If still `open` or `proposed`, inform the user it remains unresolved
4. Note the `createdDate` and calculate age to provide context
5. If the issue no longer exists (404), confirm it was deleted rather than resolved


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
