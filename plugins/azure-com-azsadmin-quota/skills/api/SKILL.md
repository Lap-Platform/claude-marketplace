---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas | Get the list of quotas at a location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota} | Gets a quota by name. |

## Enhanced Skill Content
## Question Mapping

- "What quotas are available in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas
- "List all subscription quotas for a specific location" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas
- "What are the resource limits for my Azure subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas
- "Get details about a specific quota" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota}
- "How much of my quota have I used?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota}
- "Check if I'm near my subscription limit" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota}
- "What quotas exist in the eastus region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas
- "Show me quota details by name" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota}
- "Are there any quotas configured for this location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas
- "What is the current value of a specific subscription quota?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota}
- "Compare quotas across locations" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas (call per location)
- "Audit all quota allocations for my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas

## Response Tips

- **Quota listings** (`/quotas`): Returns an array in a `value` property; may include `nextLink` for pagination -- follow it until absent. Each item contains `id`, `name`, `type`, and `properties` with quota-specific details.
- **Single quota** (`/quotas/{quota}`): Returns a flat object with `properties` nested inside; check `properties.allowedCustomRegistrationKeySize` and similar fields for actual limits vs. usage.
- **Errors**: Azure ARM returns `error.code` and `error.message` in the body; watch for `SubscriptionNotFound`, `LocationNotFound`, and `QuotaNotFound` as common codes. HTTP 404 means the quota name or location is invalid.

## Anomaly Flags

- **404 on quota lookup**: The quota name or location may be misspelled or unsupported in that region -- surface the valid location list to the user.
- **Empty quota list**: A location returning zero quotas likely means the Subscriptions.Admin resource provider is not registered -- prompt the user to register it.
- **Throttling (HTTP 429)**: Azure ARM enforces per-subscription rate limits; surface `Retry-After` header value and pause before retrying.
- **Deprecated API version**: If the response includes `x-ms-deprecation` headers or warnings, flag that `2015-11-01` is an older API version and suggest checking for a newer one.
- **Authentication failures (401/403)**: OAuth2 token may have expired or lack the `Microsoft.Subscriptions.Admin/quotas/read` permission -- surface the required RBAC role.

## Playbook

### 1. List All Quotas for a Location

1. Set `subscriptionId` to the target Azure subscription ID.
2. Set `location` to the Azure region (e.g., `eastus`, `westeurope`).
3. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas`.
4. Parse the `value` array from the response.
5. If `nextLink` is present, follow it with another GET until no `nextLink` remains.

### 2. Inspect a Specific Quota

1. List all quotas (Playbook 1) to find the exact quota name.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/quotas/{quota}` with the quota name.
3. Read `properties` for current limits, usage, and configuration details.

### 3. Audit Quotas Across Multiple Regions

1. Define a list of target locations (e.g., `eastus`, `westus`, `westeurope`).
2. For each location, call the list quotas endpoint.
3. Aggregate results into a comparison table keyed by quota name.
4. Flag any quotas that exist in some regions but not others.
5. Flag any quotas where usage is above 80% of the limit.

### 4. Verify Resource Provider Registration

1. Attempt to list quotas for the target location.
2. If the response is empty or returns a `ResourceProviderNotRegistered` error, register the provider: `POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/register` (outside this API scope).
3. Wait for registration to propagate (typically under 1 minute).
4. Retry the quota listing to confirm quotas are now visible.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
