---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2015-07-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators | Gets service administrator, account administrator, and co-administrators for the subscription. |

## Enhanced Skill Content
## Question Mapping

- "Who are the classic administrators on my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "List all co-administrators for subscription X?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Does user X have classic admin access?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "How many classic administrators are assigned to my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "What roles do the classic administrators hold?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Is the service administrator different from the account administrator?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Which email addresses have classic admin privileges?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Are there any co-admin accounts I should clean up?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Show me the admin roster for subscription {id}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "What classic RBAC assignments exist before I migrate to Azure RBAC?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Audit legacy administrator access on this subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators
- "Do I still have classic administrators that should be converted to RBAC roles?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators

## Response Tips

- **Classic Administrators list**: Response returns a `value` array of `ClassicAdministrator` objects; each entry contains `properties.emailAddress` and `properties.role` (ServiceAdministrator, CoAdministrator, or AccountAdministrator). Check `nextLink` for pagination when the subscription has many admins. A 200 with an empty `value` array means no classic admins are assigned, not an error.

## Anomaly Flags

- **Deprecation warning**: Classic administrators are a legacy Azure concept; surface a reminder that Microsoft recommends migrating to Azure RBAC role assignments. Flag when any classic admin is found as a prompt to audit.
- **High co-admin count**: If the response contains more than 5 co-administrators, flag as a potential security concern -- excessive classic admin access increases attack surface.
- **Stale service administrator**: If the service administrator email domain does not match the organization's primary domain, flag for review.
- **API version age**: This spec uses api-version `2015-07-01` -- surface a note that newer authorization API versions may be available with richer RBAC features.
- **Auth token scope**: If a 401 or 403 is returned, flag that the calling identity needs `Microsoft.Authorization/classicAdministrators/read` permission on the target subscription.
- **Rate limiting (429)**: Surface Azure Resource Manager throttling headers (`x-ms-ratelimit-remaining-subscription-reads`) when remaining reads drop below 100.

## Playbook

### 1. Audit Classic Administrators for a Subscription

1. Obtain a valid OAuth2 token with `Microsoft.Authorization/classicAdministrators/read` scope.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/classicAdministrators` with `api-version=2015-07-01`.
3. Parse the `value` array; note each administrator's `role` and `emailAddress`.
4. If `nextLink` is present, follow it to retrieve additional pages.
5. Report the total count and flag any co-administrators whose email addresses are outside the organization's domain.

### 2. Pre-Migration Inventory Before Moving to Azure RBAC

1. List classic administrators using the endpoint above.
2. For each classic admin, record their role type (ServiceAdministrator, CoAdministrator, AccountAdministrator).
3. Map each classic role to the equivalent Azure RBAC role (e.g., CoAdministrator maps roughly to Contributor or Owner).
4. Cross-reference with current RBAC assignments via the Role Assignments API to identify overlaps.
5. Produce a migration checklist showing which classic admins need RBAC equivalents and which are redundant.

### 3. Security Review of Co-Administrator Access

1. Retrieve all classic administrators for the subscription.
2. Filter results to entries where `properties.role` equals `CoAdministrator`.
3. Verify each co-admin email against your organization's active directory or identity provider.
4. Flag any co-admin accounts tied to external vendors, former employees, or generic mailboxes.
5. Recommend removal of unnecessary co-admins and document findings for compliance.

### 4. Multi-Subscription Admin Sweep

1. Retrieve a list of all subscription IDs the caller has access to (via the Subscriptions API).
2. For each subscription, call the classic administrators endpoint.
3. Aggregate results into a single report grouped by subscription.
4. Highlight subscriptions with unusually high co-admin counts or admins not seen in other subscriptions.
5. Export the consolidated report for stakeholder review.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
