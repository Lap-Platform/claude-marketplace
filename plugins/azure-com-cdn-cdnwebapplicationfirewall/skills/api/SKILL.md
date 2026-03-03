---
name: azure-cdn-webapplicationfirewallmanagement
description: "Azure CDN WebApplicationFirewallManagement API skill. Use when working with Azure CDN WebApplicationFirewallManagement for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure CDN WebApplicationFirewallManagement
API version: 2019-06-15-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies | Lists all of the protection policies within a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName} | Retrieve protection policy with specified name within a resource group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName} | Create or update policy with specified rule set name within a resource group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName} | Update an existing CdnWebApplicationFirewallPolicy with the specified policy name under the specified subscription and resource group |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName} | Deletes Policy |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/CdnWebApplicationFirewallManagedRuleSets | Lists all available managed rule sets. |

## Enhanced Skill Content
## Question Mapping

- "What WAF policies exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies
- "Show me the details of a specific WAF policy." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "Create a new WAF policy for my CDN endpoint." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "Update an existing WAF policy's settings." -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "Replace a WAF policy with a new configuration." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "Delete a WAF policy I no longer need." -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "What managed rule sets are available for CDN WAF?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/CdnWebApplicationFirewallManagedRuleSets
- "Which OWASP rules can I apply to my CDN?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/CdnWebApplicationFirewallManagedRuleSets
- "Is my WAF policy still provisioning or is it active?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "How do I add a custom rule to block a specific IP range?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "Can I partially update just the custom rules without replacing the whole policy?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "How do I check if a WAF policy was successfully deleted?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies/{policyName}
- "List all WAF configurations across a specific resource group for audit." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/CdnWebApplicationFirewallPolicies

## Response Tips

- **Policy list (GET collection):** Response contains a `value` array of policy objects; check for `nextLink` property to paginate through large result sets.
- **Policy detail (GET single):** The `properties.provisioningState` field indicates deployment status; `properties.resourceState` shows if the policy is enabled or disabled.
- **Create/Replace (PUT):** Returns 200 if updated in-place, 201 if newly created, or 202 if accepted for async provisioning -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Partial update (PATCH):** Returns 200 for synchronous completion or 202 for async; the request body is a patch map so only include fields you want to change.
- **Delete:** Returns 200 on success or 204 if the resource was already gone; both are safe to treat as successful.
- **Managed rule sets (GET):** Returns a catalog of available rule sets (not your applied policies); use these identifiers when configuring `managedRules` in a PUT/PATCH.

## Anomaly Flags

- **202 Accepted on PUT/PATCH/DELETE:** The operation is running asynchronously. Surface this to the user and recommend polling the async operation URL from the response headers until provisioning completes.
- **provisioningState not "Succeeded":** After creating or updating a policy, if `provisioningState` is `Creating`, `Updating`, or `Failed`, flag it immediately -- the policy is not yet active or has errored.
- **resourceState "Disabled":** A policy exists but is not enforcing rules. Alert the user that their CDN traffic is unprotected by this policy.
- **Empty custom rules array:** If a policy has no custom rules and managed rules are in detection-only mode, the WAF is effectively not blocking anything -- worth surfacing.
- **API version drift:** This spec uses `2019-06-15-preview` (a preview version). Flag that newer stable API versions may exist and preview versions can have breaking changes or be retired.
- **204 on DELETE:** The resource was already absent. Surface this as an informational note -- the desired state is achieved but the policy may have been deleted by another process.
- **Rate limiting (429 responses):** Azure ARM has per-subscription throttling. If responses include `Retry-After` headers or 429 status, surface the wait time and recommend batching requests.

## Playbook

### 1. Create a WAF Policy with Custom IP Block Rule

1. GET the available managed rule sets to decide which baseline protections to include.
2. PUT a new policy with the desired `policyName`, including `customRules` with a match condition for the IP range and an action of `Block`, plus any `managedRules` referencing rule set IDs from step 1.
3. If the response is 202, poll the `Azure-AsyncOperation` URL until `provisioningState` is `Succeeded`.
4. GET the policy by name to verify the final configuration and confirm `resourceState` is `Enabled`.

### 2. Audit All WAF Policies in a Resource Group

1. GET the policy collection for the target resource group.
2. If the response includes `nextLink`, follow it to retrieve additional pages until all policies are collected.
3. For each policy, inspect `properties.provisioningState`, `properties.resourceState`, and the `managedRules`/`customRules` arrays.
4. Flag any policies with `resourceState: Disabled`, empty rule sets, or `provisioningState: Failed`.

### 3. Update a Policy to Add a Rate Limit Rule

1. GET the existing policy by name to retrieve its current configuration.
2. PATCH the policy with updated `customRules` array, appending a new rate limit rule while preserving existing rules. Use the patch map to send only the `customRules` field.
3. If the response is 202, poll for async completion.
4. GET the policy again to confirm the new rule appears and `provisioningState` is `Succeeded`.

### 4. Safely Delete a WAF Policy

1. GET the policy by name to confirm it exists and review what CDN endpoints reference it.
2. Ensure no active CDN endpoints depend on this policy (this requires checking CDN endpoint configurations outside this API).
3. DELETE the policy by name.
4. If the response is 200, deletion succeeded. If 204, it was already gone.
5. GET the policy collection to confirm the deleted policy no longer appears.

### 5. Upgrade Managed Rule Sets on an Existing Policy

1. GET the available managed rule sets to find the latest version identifiers.
2. GET the existing policy to see which rule set versions are currently applied.
3. PUT the policy with the full updated configuration, replacing the `managedRules` section with references to the newer rule set versions while keeping all other settings intact.
4. Monitor the async operation if a 202 is returned.
5. GET the policy to verify the updated rule set versions and confirm `provisioningState` is `Succeeded`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
