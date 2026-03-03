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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks | Get a list of all virtual networks. |

## Enhanced Skill Content
## Question Mapping

- "What admin virtual networks exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "List all virtual networks managed by the network admin?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "How many admin virtual networks are configured?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Show me the network topology for subscription X?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Are there any admin virtual networks provisioned?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "What is the status of admin virtual networks in this subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Which virtual networks does the admin provider manage?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Can I see the admin-level network configuration?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "What network resources exist under Microsoft.Network.Admin?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Get virtual network details for my Azure Stack subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Do I have any admin virtual networks set up yet?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks
- "Audit all admin-level virtual network resources?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks

## Response Tips

- **Admin Virtual Networks listing**: Response is an Azure ARM-style collection. Expect a `value` array of resource objects, each containing `id`, `name`, `type`, `location`, and `properties`. Check for a `nextLink` field for pagination -- if present, follow it to retrieve additional pages. Empty `value` array means no admin virtual networks exist, not an error.

## Anomaly Flags

- **Empty results**: If `value` is an empty array, surface this proactively -- the operator may not have provisioned any admin virtual networks yet.
- **Throttling (429)**: Azure ARM endpoints enforce rate limits. If you receive a 429, check the `Retry-After` header and wait before retrying. Surface the throttle event to the user.
- **Authorization failures (401/403)**: OAuth2 tokens may be expired or lack the `Microsoft.Network.Admin` provider permissions. Flag immediately -- this usually means the user's role assignment is insufficient or the token needs refresh.
- **404 on subscription**: The subscriptionId may be invalid or the Microsoft.Network.Admin resource provider may not be registered. Surface both possibilities.
- **Unexpected `provisioningState`**: If any returned virtual network has a `provisioningState` other than `Succeeded` (e.g., `Failed`, `Updating`, `Deleting`), flag it -- the resource may be in a transitional or broken state.
- **Deprecation headers**: Watch for `Sunset` or `Deprecation` headers in the response. This is an older API version (2015-06-15) and may be superseded.

## Playbook

### 1. List All Admin Virtual Networks

1. Obtain a valid OAuth2 token with permissions for the Microsoft.Network.Admin provider.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminVirtualNetworks` with `api-version=2015-06-15`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it with a GET request to retrieve the next page.
5. Repeat until no `nextLink` is returned.

### 2. Verify Admin Network Provisioning Status

1. Retrieve the list of admin virtual networks (see Playbook 1).
2. For each entry in `value`, inspect `properties.provisioningState`.
3. Flag any resource not in `Succeeded` state.
4. Report a summary: total count, healthy count, and any resources needing attention.

### 3. Audit Subscription Network Resources

1. Confirm the subscription ID is valid and the Microsoft.Network.Admin provider is registered.
2. List all admin virtual networks using the GET endpoint.
3. For each network, extract `name`, `location`, and key properties (address space, subnets).
4. Cross-reference with expected configuration or compliance baseline.
5. Surface any discrepancies or missing networks.

### 4. Troubleshoot Access Denied Errors

1. Attempt the GET call to list admin virtual networks.
2. If a 401 is returned, refresh the OAuth2 token and retry.
3. If a 403 is returned, verify the user's RBAC role includes read access to `Microsoft.Network.Admin/adminVirtualNetworks`.
4. Check that the Microsoft.Network.Admin resource provider is registered on the subscription (`az provider show --namespace Microsoft.Network.Admin`).
5. If the provider is not registered, register it and retry the request.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
