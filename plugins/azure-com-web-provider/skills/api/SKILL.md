---
name: provider-api-client
description: "Provider API Client API skill. Use when working with Provider API Client for providers, subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Provider API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Web/availableStacks -- verify access

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Web/availableStacks | Get available application frameworks and their versions |
| GET | /providers/Microsoft.Web/operations | Gets all available operations for the Microsoft.Web resource provider. Also exposes resource metric definitions |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks | Get available application frameworks and their versions |

## Enhanced Skill Content
## Question Mapping

- "What web app stacks are available on Azure?" -> GET /providers/Microsoft.Web/availableStacks
- "Which runtime stacks can I use for Linux web apps?" -> GET /providers/Microsoft.Web/availableStacks (with osTypeSelected=Linux)
- "Show me the available Windows hosting stacks" -> GET /providers/Microsoft.Web/availableStacks (with osTypeSelected=Windows)
- "What operations does the Microsoft.Web resource provider support?" -> GET /providers/Microsoft.Web/operations
- "List all API actions available for Azure App Service" -> GET /providers/Microsoft.Web/operations
- "What stacks are available in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks
- "Can I deploy a Node.js app on Azure App Service?" -> GET /providers/Microsoft.Web/availableStacks (check response for Node entries)
- "Which Python versions are supported for Linux web apps in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks (with osTypeSelected=Linux)
- "Does Azure App Service support .NET 8?" -> GET /providers/Microsoft.Web/availableStacks (inspect version lists in response)
- "What's the difference between global stacks and my subscription's stacks?" -> GET /providers/Microsoft.Web/availableStacks then GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks (compare both)
- "Is a specific operation like sites/restart permitted by the Web provider?" -> GET /providers/Microsoft.Web/operations (search results for the action name)
- "What RBAC actions exist for Azure Web Apps?" -> GET /providers/Microsoft.Web/operations
- "Show me Java stack options filtered by OS type for my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks (with osTypeSelected)

## Response Tips

- **availableStacks (both global and subscription):** Response contains a `value` array of stack objects, each with nested `majorVersions` and `minorVersions` arrays -- drill into these to find specific runtime versions. Filter by `osTypeSelected` query param rather than post-filtering to reduce payload size.
- **operations:** Returns a `value` array of operation objects with `name` (e.g., `Microsoft.Web/sites/restart/action`), `display.provider`, `display.resource`, `display.operation`, and `display.description`. Use the `name` field for RBAC and policy references.
- **All endpoints:** Require `api-version=2018-02-01` as a query parameter. Omitting it returns a 400 with a list of supported versions. Azure ARM responses wrap results in `{ "value": [...] }` -- always read from `.value`, not the root.

## Anomaly Flags

- **Missing api-version parameter:** Azure returns a 400 with an error body listing valid versions. Surface this immediately with the suggested version string.
- **Empty value arrays:** If `availableStacks` returns an empty `value`, flag that the subscription may have regional restrictions or the osTypeSelected filter excluded all results.
- **Subscription-scoped vs global differences:** If the subscription endpoint returns fewer stacks than the global endpoint, proactively note that some stacks may be disabled or unavailable in the subscription's region or SKU tier.
- **Deprecated runtime versions:** If stack entries include `isDeprecated: true` or an `endOfLifeDate` in the past, flag these to prevent deploying on unsupported runtimes.
- **Throttling (429 responses):** Azure ARM enforces per-subscription read limits (typically 12,000/hour). If a 429 is returned, surface the `Retry-After` header value and pause further calls.
- **Authentication failures (401/403):** Surface whether the token is expired (401) vs the principal lacks `Microsoft.Web/availableStacks/read` permission (403), since the fix differs.

## Playbook

### 1. Choose a Runtime Stack for a New Web App

1. Call GET `/providers/Microsoft.Web/availableStacks?api-version=2018-02-01&osTypeSelected=Linux` (or Windows)
2. Parse the `value` array and identify the desired runtime (e.g., Node, Python, .NET)
3. Drill into `majorVersions` to find supported major versions
4. Check `minorVersions` within each major for the latest stable release
5. Confirm the chosen version is not marked deprecated
6. Use the stack name and version when creating or updating the App Service site configuration

### 2. Audit Available RBAC Actions for App Service

1. Call GET `/providers/Microsoft.Web/operations?api-version=2018-02-01`
2. Collect all entries from the `value` array
3. Group operations by the second segment of `name` (e.g., `sites`, `serverfarms`, `certificates`)
4. For each group, list the available actions (read, write, delete, custom actions)
5. Cross-reference against your custom RBAC role definitions to verify least-privilege alignment

### 3. Compare Global vs Subscription-Specific Stack Availability

1. Call GET `/providers/Microsoft.Web/availableStacks?api-version=2018-02-01` to get the global baseline
2. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks?api-version=2018-02-01` for your subscription
3. Diff the two `value` arrays by stack name and version
4. Flag any stacks present globally but missing from the subscription (potential policy or regional restriction)
5. Report findings so the team can adjust deployment targets or request access

### 4. Verify a Specific Runtime Before Deployment

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/availableStacks?api-version=2018-02-01&osTypeSelected=Linux`
2. Search the `value` array for the target runtime (e.g., `python`)
3. Check that the desired version exists in `majorVersions[].minorVersions[]`
4. Confirm `isDeprecated` is false and `endOfLifeDate` (if present) is in the future
5. Proceed with deployment or raise an alert if the version is missing or end-of-life


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
