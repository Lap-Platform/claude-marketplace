---
name: azure-alerts-management-service-resource-provider
description: "Azure Alerts Management Service Resource Provider API skill. Use when working with Azure Alerts Management Service Resource Provider for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Alerts Management Service Resource Provider
API version: 2019-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/microsoft.alertsManagement/smartDetectorAlertRules -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/microsoft.alertsManagement/smartDetectorAlertRules | List all the existing Smart Detector alert rules within the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules | List all the existing Smart Detector alert rules within the subscription and resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} | Get a specific Smart Detector alert rule. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} | Create or update a Smart Detector alert rule. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} | Patch a specific Smart Detector alert rule. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} | Delete an existing Smart Detector alert rule. |

## Enhanced Skill Content
## Question Mapping

- "What smart detector alert rules exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.alertsManagement/smartDetectorAlertRules
- "List all alert rules in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules
- "Show me the details of a specific alert rule?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName}
- "How do I create a new smart detector alert rule?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName}
- "How do I update an existing alert rule completely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName}
- "How do I partially update an alert rule without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName}
- "How do I delete an alert rule?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName}
- "Can I see the detector details attached to an alert rule?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} (with expandDetector=true)
- "Which resource groups have smart detector alert rules?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.alertsManagement/smartDetectorAlertRules (then extract unique resource groups from results)
- "Does a specific alert rule already exist before I create one?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName}
- "How do I move an alert rule from one configuration to another?" -> GET (read current) then PUT (write updated)
- "How do I disable an alert rule without deleting it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} (set state to Disabled in parameters)

## Response Tips

- **List endpoints (subscription/resource group):** Response contains a `value` array of alert rule objects. Check for `nextLink` property for pagination -- follow it with GET until absent.
- **Single rule GET:** Returns the full alert rule resource. The `properties` object holds state, severity, frequency, detector, actionGroups, and scope. Use `expandDetector=true` to inline detector metadata.
- **PUT (create/replace):** Returns 200 if the rule already existed and was updated, 201 if newly created. The response body is the full resource as stored.
- **PATCH (partial update):** Returns 200 with the merged resource. Only fields in `parameters` are changed; omitted fields are preserved.
- **DELETE:** Returns 200 if the rule was deleted, 204 if it did not exist (idempotent). No response body on 204.
- **Errors:** Azure ARM returns `error.code` and `error.message` in a JSON error envelope. Common codes: `ResourceNotFound`, `AuthorizationFailed`, `InvalidRequestContent`.

## Anomaly Flags

- **201 on PUT:** Surface when a PUT returns 201 instead of 200 -- this means a new rule was created rather than an existing one updated. Confirm this was intentional.
- **204 on DELETE:** Alert the user that the rule did not exist at deletion time. This may indicate a stale reference or prior deletion.
- **Missing nextLink awareness:** If a list response contains `nextLink`, proactively warn that results are paginated and additional pages exist.
- **expandDetector omitted:** When a user asks about detector details but the query omits `expandDetector=true`, suggest adding it to avoid a follow-up call.
- **OAuth token expiry:** If a 401 is returned, surface that the OAuth2 token may have expired and prompt for re-authentication.
- **Throttling (429):** Azure ARM enforces rate limits per subscription. Surface `Retry-After` header value and suggest backing off.
- **Deprecated API version:** If the response includes deprecation warnings or the `api-version` 2019-06-01 returns sunset headers, flag that a newer version may be available.

## Playbook

### 1. Create a New Smart Detector Alert Rule

1. Choose the target resource group and a unique alert rule name.
2. Build the `parameters` body with required properties: `detector`, `scope`, `actionGroups`, `severity`, `frequency`, and `state` (Enabled/Disabled).
3. Call PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.alertsManagement/smartDetectorAlertRules/{alertRuleName} with the parameters body.
4. Confirm a 201 response (new rule created). If 200, an existing rule with that name was overwritten.
5. Optionally call GET with `expandDetector=true` to verify the detector binding.

### 2. Audit All Alert Rules Across a Subscription

1. Call GET /subscriptions/{subscriptionId}/providers/microsoft.alertsManagement/smartDetectorAlertRules to list all rules.
2. Follow `nextLink` in the response to retrieve additional pages until no `nextLink` is present.
3. For each rule, inspect `properties.state` to identify Enabled vs Disabled rules.
4. Group results by `resourceGroup` (extracted from the resource `id` field) for a per-group summary.

### 3. Update an Alert Rule's Configuration

1. Call GET on the specific alert rule to retrieve its current configuration.
2. Identify the fields to change (e.g., severity, frequency, action groups).
3. Call PATCH with a `parameters` body containing only the changed fields.
4. Verify the 200 response body reflects the merged configuration.

### 4. Safely Delete an Alert Rule

1. Call GET on the alert rule to confirm it exists and inspect its current state.
2. If the rule is Enabled and actively firing, consider PATCHing its state to Disabled first.
3. Call DELETE on the alert rule.
4. If 200, deletion succeeded. If 204, the rule was already absent.
5. Optionally call GET again to confirm a `ResourceNotFound` error, verifying removal.

### 5. Compare Alert Rules Between Resource Groups

1. Call GET (list) on the first resource group to retrieve its alert rules.
2. Call GET (list) on the second resource group to retrieve its alert rules.
3. Compare rule names, detector types, severities, and frequencies between the two sets.
4. For rules that exist in both, call GET with `expandDetector=true` on each to compare full detector configurations.
5. Surface differences in state, scope, or action group bindings.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
