---
name: networkadminmanagementclient
description: "NetworkAdminManagementClient API skill. Use when working with NetworkAdminManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# NetworkAdminManagementClient
API version: 2015-06-15

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers | Get a list of all load balancers. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all admin load balancers?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "What load balancers exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "Can I check the status of admin load balancers?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "How do I audit network infrastructure for a subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "What admin-level network resources are provisioned?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "How do I verify load balancer deployment in Azure Stack?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "Are there any load balancers configured for my tenant?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "How do I get load balancer details for a specific subscription ID?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "What network admin resources can I query?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers
- "How do I monitor admin load balancer provisioning state?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers

## Response Tips

- **Admin Load Balancers (GET list)**: Response is typically an object with a `value` array of load balancer resources. Each resource includes `id`, `name`, `type`, `location`, `properties` (containing `provisioningState`, frontend/backend configs). Check for an empty `value` array rather than a 404 when no load balancers exist. If `nextLink` is present, paginate by following it.

## Anomaly Flags

- **API version staleness**: This spec uses `2015-06-15` -- flag if Azure returns `x-ms-request-id` headers with deprecation warnings or if responses include `api-deprecated` markers. This is an older Azure Stack Admin API version.
- **Empty results**: Surface when `value` array is empty, as it may indicate the Network resource provider is not registered on the subscription.
- **Provisioning failures**: Flag any load balancer where `properties.provisioningState` is `Failed` or `Deleting`.
- **OAuth token expiry**: Surface 401 responses proactively -- Azure OAuth2 tokens expire (typically 1 hour), and the agent should prompt for re-authentication.
- **Throttling (429)**: Azure ARM applies rate limits per subscription. Surface `Retry-After` header values and back off accordingly.
- **Subscription-level errors (403/404)**: A 403 may indicate the caller lacks Network Admin privileges. A 404 on the subscription path means the subscription ID is invalid.

## Playbook

### 1. List All Admin Load Balancers for a Subscription

1. Obtain a valid OAuth2 token with Network Admin scope
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers`
3. Parse the `value` array from the 200 response
4. If `nextLink` is present, repeat the GET using that URL until no more pages
5. Summarize count and provisioning states of all returned load balancers

### 2. Audit Network Admin Infrastructure Health

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers`
2. Iterate through each load balancer in the `value` array
3. Check `properties.provisioningState` for each -- flag any that are not `Succeeded`
4. Report unhealthy or misconfigured load balancers with their `id` and `name`

### 3. Verify Load Balancer Exists After Deployment

1. Deploy a load balancer through your infrastructure tooling
2. Wait for provisioning to complete
3. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers`
4. Search the `value` array for the expected load balancer by `name`
5. Confirm `provisioningState` is `Succeeded` -- if missing or failed, flag for investigation

### 4. Cross-Subscription Load Balancer Inventory

1. Enumerate all subscription IDs the caller has access to (via Azure Subscriptions API)
2. For each subscription, call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminLoadBalancers`
3. Aggregate results across subscriptions
4. Produce a consolidated inventory with subscription ID, load balancer name, and state


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
