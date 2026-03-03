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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests | Get a list of all manifests. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName} | Get the specified manifest. |

## Enhanced Skill Content
## Question Mapping

- "What manifests are available for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests
- "List all subscription admin manifests" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests
- "Get details for a specific manifest" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}
- "Does manifest X exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}
- "What providers are registered in my subscription manifests?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests
- "Show me the configuration of manifest Y" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}
- "How many manifests are registered?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests
- "Check if a specific resource provider manifest is deployed" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}
- "What endpoints does manifest Z expose?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}
- "Audit all registered provider manifests" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests
- "Compare two manifests" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName} (call twice, diff results)
- "Verify my subscription has the expected manifests" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests

## Response Tips

- **Manifest list** (`/manifests`): Response wraps results in a `value` array. Check for `nextLink` property for pagination -- iterate until absent. Each item contains manifest metadata but may omit full configuration details.
- **Single manifest** (`/manifests/{manifestName}`): Returns the complete manifest object directly (not wrapped in `value`). A 404 means the manifest name is invalid or not registered -- surface this clearly rather than failing silently.
- **General**: All responses follow Azure Resource Manager conventions. Look for `id`, `name`, `type`, and `properties` at the top level. Error responses use the standard `{ "error": { "code": "...", "message": "..." } }` shape.

## Anomaly Flags

- **404 on manifest lookup**: The manifest name may be misspelled or the provider may not be registered -- prompt the user to list all manifests first to verify available names.
- **401/403 responses**: The OAuth2 token may be expired or the subscription may lack `Microsoft.Subscriptions.Admin` permissions -- suggest re-authenticating or checking RBAC role assignments.
- **Empty manifest list**: A subscription returning zero manifests is unusual in Azure Stack environments -- flag this as potentially misconfigured.
- **429 Too Many Requests**: Azure ARM enforces per-subscription throttling (typically 12,000 reads/hour) -- surface remaining quota from `x-ms-ratelimit-remaining-subscription-reads` response header.
- **Deprecated `api-version`**: This spec uses `2015-11-01` -- if Azure returns a `Sunset` header or newer `api-version` suggestion in response headers, flag the deprecation proactively.
- **Unexpected manifest properties**: If a manifest contains `provisioningState` values other than `Succeeded` (e.g., `Failed`, `Deleting`), surface immediately as it may indicate an infrastructure issue.

## Playbook

### 1. Inventory All Registered Manifests

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests` with your subscription ID.
2. Parse the `value` array from the response.
3. If `nextLink` is present, follow it to retrieve additional pages.
4. Compile the list of manifest names and their provisioning states.
5. Flag any manifests not in `Succeeded` state.

### 2. Inspect a Specific Manifest

1. List all manifests (Playbook 1) to confirm the exact manifest name.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}` with the confirmed name.
3. Review the `properties` object for configuration details, registered resource types, and endpoint URIs.
4. Validate that expected resource types and extensions are present.

### 3. Verify Provider Registration Health

1. Retrieve all manifests using the list endpoint.
2. For each manifest in the `value` array, check `properties.provisioningState`.
3. For any manifest not in `Succeeded` state, fetch its full details via the single-manifest endpoint.
4. Compile a health report: total manifests, healthy count, unhealthy count with details.
5. Surface any manifests in `Failed` or transitional states as actionable items.

### 4. Compare Manifest Configurations

1. Fetch manifest A: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestA}`.
2. Fetch manifest B: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestB}`.
3. Diff the `properties` objects, focusing on registered resource types, supported API versions, and endpoint definitions.
4. Report added, removed, and changed fields between the two manifests.

### 5. Troubleshoot Missing Manifest

1. Call the list endpoint to get all registered manifests.
2. Search the results for the expected manifest name (case-sensitive match).
3. If not found, confirm the subscription ID is correct and the user has `Microsoft.Subscriptions.Admin` read permissions.
4. Check if the provider needs to be registered at the subscription level via Azure Resource Manager.
5. If the manifest exists but returns unexpected data, fetch its full details and inspect `provisioningState` for errors.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
