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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses | List of public IP addresses. |

## Enhanced Skill Content
## Question Mapping

- "What public IP addresses are allocated in my network admin subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "How do I list all admin public IPs for a given subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "Are there any public IP addresses provisioned by the network administrator?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "Can I audit which public IPs are currently in use across my admin network?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "How do I check the allocation status of admin public IP addresses?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "What is the current inventory of public IP addresses in my Azure Stack network?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "How many admin public IPs exist under subscription X?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "Which public IPs are available for tenant allocation?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "I need to verify public IP capacity before provisioning new tenants -- how?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "How do I monitor public IP pool exhaustion in Azure Stack?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses
- "What API version should I use for network admin public IP queries?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses (use api-version=2015-06-15)

## Response Tips

- **Admin Public IP Addresses**: Expect a JSON object with a `value` array of IP address resources. Each entry includes `id`, `name`, `type`, `location`, and `properties` (containing allocation state, IP pool, and usage metadata). Check for a `nextLink` field for pagination -- if present, follow it to retrieve additional pages. Always pass `api-version=2015-06-15` as a query parameter.

## Anomaly Flags

- **IP pool exhaustion**: Surface a warning when the total count of allocated public IPs approaches the pool capacity, indicating tenants may fail to acquire new addresses.
- **Unexpected empty response**: If `value` is an empty array when IPs are expected, flag potential misconfiguration or permission issues.
- **Stale API version**: This spec uses `2015-06-15` -- flag if Azure documentation references a newer api-version for this resource provider, as the endpoint may be deprecated.
- **OAuth token expiry**: Surface 401 responses proactively; the OAuth2 token may have expired or lack the `Microsoft.Network.Admin/adminPublicIpAddresses/read` permission.
- **Throttling (429)**: If Azure returns 429 Too Many Requests, surface the `Retry-After` header value and pause before retrying.
- **Missing subscription access**: A 403 response likely means the authenticated principal lacks access to the target subscription -- flag immediately rather than retrying.

## Playbook

### 1. Audit All Admin Public IPs in a Subscription

1. Authenticate via OAuth2 to obtain a bearer token with Network Admin read permissions.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminPublicIpAddresses?api-version=2015-06-15`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it to retrieve the next page; repeat until no `nextLink` remains.
5. Compile the full list of IP addresses with their allocation states.

### 2. Check Public IP Capacity Before Tenant Onboarding

1. Retrieve all admin public IPs using the endpoint above.
2. Count entries where `properties.allocationMethod` or allocation state indicates "available" vs "allocated".
3. Compare available count against the number of IPs the new tenant requires.
4. If insufficient capacity, flag for the operator to expand the IP pool before proceeding.

### 3. Investigate a Missing or Unresponsive Public IP

1. List all admin public IPs for the subscription.
2. Search the `value` array for the specific IP address or resource name in question.
3. Inspect the `properties` block for provisioning state (e.g., `Succeeded`, `Failed`, `Updating`).
4. If the IP is missing from results, verify the correct subscription ID and that the caller has sufficient permissions.
5. If the IP shows a non-succeeded state, escalate based on the reported provisioning error.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
