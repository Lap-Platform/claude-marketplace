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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders | Get the list of delegatedProviders. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider} | Get the specified delegated provider. |

## Enhanced Skill Content
## Question Mapping

- "What delegated providers exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders
- "List all delegated providers for subscription abc-123" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders
- "Get details about a specific delegated provider" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}
- "Who has delegated access to my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders
- "Look up delegated provider by ID" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}
- "Is provider X a delegated provider in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}
- "How many delegated providers are configured?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders
- "Show the configuration of delegated provider foo" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}
- "Verify a delegated provider exists before assigning offers" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}
- "Audit all delegation relationships in my Azure Stack subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders
- "Check if a tenant has been granted delegated provider status" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}

## Response Tips

- **List endpoint**: Returns an array of delegated provider objects; check for a `nextLink` property for pagination across large tenants. Each item includes the provider's subscription ID and provisioning state.
- **Detail endpoint**: Returns a single delegated provider object; a 404 means the provider ID is invalid or not delegated. Inspect `properties.provisioningState` for readiness status.

## Anomaly Flags

- **404 on detail lookup**: The delegated provider ID does not exist or the delegation relationship has been removed -- surface this clearly rather than returning raw error.
- **Empty list response**: No delegated providers configured may indicate Azure Stack Hub is not set up for multi-tenancy -- flag this as a potential configuration gap.
- **OAuth2 token scope mismatch**: A 401/403 typically means the caller lacks the Admin subscription role -- recommend checking Azure RBAC assignments.
- **Stale provisioning state**: If a delegated provider shows a provisioning state other than `Succeeded` (e.g., `Creating`, `Failed`), flag it as potentially unhealthy.
- **API version deprecation**: This uses `2015-11-01` -- if Azure returns an `x-ms-deprecation` header or a newer `api-version` hint, surface it proactively.

## Playbook

### 1. Inventory All Delegated Providers

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders
2. Collect all items from the response array
3. If `nextLink` is present, follow it to retrieve additional pages
4. Summarize the count and list each provider's ID and provisioning state

### 2. Validate a Specific Delegated Provider

1. Obtain the delegated provider ID (from inventory or user input)
2. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProvider}
3. If 200, confirm the provider exists and report its provisioning state
4. If 404, inform the user the delegation relationship does not exist

### 3. Audit Delegation Health

1. List all delegated providers using the list endpoint
2. For each provider, call the detail endpoint to inspect `properties.provisioningState`
3. Flag any provider not in `Succeeded` state
4. Report a summary: total providers, healthy count, unhealthy count with details

### 4. Pre-Check Before Assigning Offers to a Delegated Provider

1. Confirm the target delegated provider exists by calling the detail endpoint
2. Verify `provisioningState` is `Succeeded`
3. If the provider is missing or unhealthy, abort and surface the issue
4. Proceed with offer assignment only after both checks pass


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
