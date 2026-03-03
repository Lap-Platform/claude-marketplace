---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2018-03-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Subscription/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Subscription/operations | Lists all of the available Microsoft.Subscription API operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Microsoft Subscription?" -> GET /providers/Microsoft.Subscription/operations
- "List all supported subscription management operations" -> GET /providers/Microsoft.Subscription/operations
- "What actions can I perform on Azure subscriptions?" -> GET /providers/Microsoft.Subscription/operations
- "Show me the resource provider operations for subscriptions" -> GET /providers/Microsoft.Subscription/operations
- "What permissions exist for the Subscription resource provider?" -> GET /providers/Microsoft.Subscription/operations
- "Which RBAC operations does Microsoft.Subscription expose?" -> GET /providers/Microsoft.Subscription/operations
- "Can I manage subscription aliases through this API?" -> GET /providers/Microsoft.Subscription/operations
- "What API version should I use for subscription operations?" -> GET /providers/Microsoft.Subscription/operations (use api-version=2018-03-01-preview)
- "Is there a cancel or rename operation available?" -> GET /providers/Microsoft.Subscription/operations (check returned operation list)
- "How do I discover what this API can do before calling other endpoints?" -> GET /providers/Microsoft.Subscription/operations

## Response Tips

- **Operations list (GET /providers/.../operations):** Returns an array of operation objects, each with `name` (e.g., `Microsoft.Subscription/subscriptions/write`), `display` (localized descriptions), and `isDataAction` flag. Paginated via `nextLink` -- follow it until absent. The `api-version` query parameter is mandatory on every request.

## Anomaly Flags

- **Missing api-version parameter:** All Azure ARM requests require `api-version`; omitting it returns 400. Agent should always inject `api-version=2018-03-01-preview` automatically.
- **Empty operations list:** If the response contains zero operations, the resource provider may not be registered in the tenant. Surface a suggestion to run `az provider register --namespace Microsoft.Subscription`.
- **401/403 responses:** OAuth2 token may lack sufficient scope or the tenant may restrict subscription management. Flag the required role (typically Reader or higher at tenant scope).
- **Preview API version:** `2018-03-01-preview` is a preview version -- behaviors may change without notice. Surface a warning when the user relies on this for production automation.
- **429 Too Many Requests:** Azure ARM enforces per-subscription throttling (typically 12,000 reads/hour). If `Retry-After` header appears, pause and surface the wait time to the user.
- **Deprecation headers:** Watch for `Sunset` or `x-ms-deprecation` headers in responses indicating the preview version is being retired.

## Playbook

### 1. Discover Available Subscription Operations

1. Call `GET /providers/Microsoft.Subscription/operations?api-version=2018-03-01-preview`
2. Parse the response body for the `value` array
3. List each operation's `name` and `display.description`
4. If `nextLink` is present, follow it to retrieve additional pages
5. Filter results by `isDataAction` to separate control-plane from data-plane operations

### 2. Check If a Specific Operation Exists

1. Call `GET /providers/Microsoft.Subscription/operations?api-version=2018-03-01-preview`
2. Collect all pages (follow `nextLink`)
3. Search the combined `value` array for the target operation name (e.g., `Microsoft.Subscription/subscriptions/write`)
4. If not found, inform the user the operation is unavailable at this API version

### 3. Audit RBAC Permissions for Subscription Management

1. Call `GET /providers/Microsoft.Subscription/operations?api-version=2018-03-01-preview`
2. Collect all operations across all pages
3. Group operations by resource type (split `name` on `/` to extract the resource segment)
4. For each group, list available actions (read, write, delete, action)
5. Cross-reference with the user's current role assignments to identify gaps

### 4. Validate API Connectivity and Auth

1. Obtain an OAuth2 token for scope `https://management.azure.com/.default`
2. Call `GET /providers/Microsoft.Subscription/operations?api-version=2018-03-01-preview` with `Authorization: Bearer <token>`
3. On 200: confirm connectivity and auth are working
4. On 401: token is expired or invalid -- refresh and retry
5. On 403: token lacks required permissions -- verify the service principal or user has at least Reader role at the tenant or subscription level


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
