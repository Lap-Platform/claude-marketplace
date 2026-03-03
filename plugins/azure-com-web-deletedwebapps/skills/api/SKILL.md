---
name: deletedwebapps-api-client
description: "DeletedWebApps API Client API skill. Use when working with DeletedWebApps API Client for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# DeletedWebApps API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites | Get all deleted apps for a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites | Get all deleted apps for a subscription at location |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites/{deletedSiteId} | Get deleted app for a subscription at location. |

## Enhanced Skill Content


## Question Mapping

- "What web apps have been deleted in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites
- "List all deleted sites across my Azure subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites
- "What deleted web apps exist in a specific region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites
- "Show me deleted sites in the East US location" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites
- "Get details about a specific deleted web app" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites/{deletedSiteId}
- "Can I find a deleted app by its ID?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites/{deletedSiteId}
- "How many web apps were recently deleted?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites
- "Is there a deleted app in West Europe I can recover?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites
- "What information is available about a deleted site before restoring it?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites/{deletedSiteId}
- "Which locations have deleted web apps?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites
- "Verify a specific deleted site still exists before attempting recovery" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites/{deletedSiteId}
- "Do I have any deleted apps that might be consuming soft-delete retention?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites

## Response Tips

- **List endpoints** (subscription-wide and location-scoped): Responses are paginated via `nextLink` -- follow it until absent to retrieve all results. Each item in the `value` array contains the deleted site resource with properties nested under `properties`.
- **Detail endpoint** (by deletedSiteId): Returns a single resource object. Key fields are under `properties` including `deletedSiteId`, `deletedTimestamp`, `slot`, `kind`, and `resourceGroup`. A 404 means the site has already been purged or the ID is invalid.
- **All endpoints**: Require `api-version` as a query parameter (use `2018-02-01`). OAuth2 bearer token must be included. Standard Azure error responses use `error.code` and `error.message` structure.

## Anomaly Flags

- **Pagination truncation**: If `nextLink` is present but returns an error on follow-up, surface this as a potential throttling or transient issue.
- **Empty results in known locations**: If a location-scoped query returns empty but the subscription-wide list showed sites in that location, flag a possible timing/replication delay.
- **Approaching soft-delete retention limit**: If `deletedTimestamp` on any site is close to the 30-day retention window, proactively warn that the site will be permanently purged soon.
- **Deprecated api-version**: If the service returns warnings or unexpected fields, flag that `2018-02-01` may be outdated and suggest checking for a newer API version.
- **Throttling (429 responses)**: Surface `Retry-After` header value and pause before retrying. Azure ARM typically throttles at subscription scope.
- **Large deleted site counts**: If the subscription-wide list returns an unusually high number of deleted sites, flag potential cleanup needed to avoid resource quota issues.

## Playbook

### 1. Inventory All Deleted Web Apps

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites` with your subscription ID and `api-version=2018-02-01`.
2. Parse the `value` array from the response.
3. If `nextLink` is present, follow it with a GET request and append results.
4. Repeat until no `nextLink` remains.
5. Compile the full list with `deletedSiteId`, `deletedSiteName`, `resourceGroup`, `location`, and `deletedTimestamp` for each entry.

### 2. Find a Specific Deleted App for Recovery

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites` to get all deleted sites.
2. Filter results by name, resource group, or location to identify the target app.
3. Note the `location` and `deletedSiteId` from the matching entry.
4. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites/{deletedSiteId}` to confirm it still exists and review its full properties.
5. Use the returned details (resource group, slot, kind) to proceed with a restore operation via the appropriate recovery API.

### 3. Audit Deleted Sites by Region

1. Identify the target Azure region (e.g., `eastus`, `westeurope`).
2. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/deletedSites` with the region as `{location}`.
3. Follow any `nextLink` pagination to collect all results.
4. Review `deletedTimestamp` on each entry to understand deletion timelines.
5. Cross-reference with activity logs if you need to determine who deleted each app.

### 4. Monitor Expiring Deleted Sites

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/deletedSites` to list all deleted sites.
2. For each site, parse the `deletedTimestamp` field.
3. Calculate days remaining until the 30-day soft-delete retention expires.
4. Flag any sites with fewer than 7 days remaining.
5. For critical sites nearing expiration, retrieve full details via the location-scoped detail endpoint and initiate recovery immediately.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
