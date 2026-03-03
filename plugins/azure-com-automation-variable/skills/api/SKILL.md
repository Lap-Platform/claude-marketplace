---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2015-10-31

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName} | Create a variable. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName} | Update a variable. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName} | Delete the variable. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName} | Retrieve the variable identified by variable name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables | Retrieve a list of variables. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new automation variable?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I update an existing automation variable's value?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I rename or reconfigure a variable without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I delete an automation variable?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I get the details of a specific variable?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I list all variables in an automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables
- "How do I check if a variable already exists before creating it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I create an encrypted variable to store a secret?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I change just the description of a variable without touching its value?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I replace a variable completely with new properties?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I audit which variables exist across my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables
- "How do I remove a variable that is no longer used by any runbook?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables/{variableName}
- "How do I bulk-inspect variables to find which ones are encrypted?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/variables

## Response Tips

- **PUT (create/replace):** Returns 200 for updates to existing variables, 201 for newly created ones -- check the status code to confirm which occurred. Response body contains the full variable resource including `properties.isEncrypted` and `properties.value` (null for encrypted variables).
- **PATCH (update):** Returns 200 only. If the variable does not exist, expect a 404 error rather than an implicit creation -- PATCH is not an upsert.
- **DELETE:** Returns 200 on success with no meaningful body. A 404 means the variable was already absent -- treat this as idempotent in automation scripts.
- **GET (single):** Returns the full variable object. The `properties.value` field is null for encrypted variables -- this is normal, not an error.
- **GET (list):** Response wraps results in a `value` array. Watch for a `nextLink` property indicating pagination -- follow it to retrieve remaining variables.

## Anomaly Flags

- **201 vs 200 on PUT**: Surface when a PUT returns 201 (created) if the caller expected to update an existing variable -- may indicate a typo in the variable name that silently created a new resource.
- **Encrypted variable value is null**: When GET returns `properties.value: null`, proactively note that this is expected for encrypted variables, not a data loss issue.
- **Pagination present on list**: If `nextLink` appears in a list response, warn that results are incomplete and additional pages must be fetched.
- **404 on PATCH**: Flag that PATCH does not auto-create -- suggest using PUT instead if the intent is create-or-update.
- **API version drift**: This spec targets `2015-10-31`. If Azure returns errors about unsupported API versions or deprecated features, flag that a newer `api-version` query parameter may be required.
- **Throttling (429)**: Azure ARM APIs enforce rate limits per subscription. Surface `Retry-After` headers immediately and suggest backing off before retrying.
- **Mismatched encryption state**: If a user attempts to PATCH an encrypted variable's value in plain text (or vice versa), flag the potential security concern.

## Playbook

### 1. Create a New Encrypted Variable

1. Call GET on the target variable name to confirm it does not already exist (expect 404).
2. Call PUT with the variable name and set `properties.isEncrypted` to `true` and `properties.value` to the secret string.
3. Confirm the response is 201 (created). Note: the returned `properties.value` will be null since encrypted values are write-only.
4. Call GET to verify the variable appears with `isEncrypted: true`.

### 2. Safely Update a Variable Value

1. Call GET on the variable to retrieve its current properties (description, encryption state).
2. Verify the variable exists (200 response). If 404, decide whether to create it instead.
3. Call PATCH with only the changed fields in the `properties` block (e.g., new `value`).
4. Confirm the 200 response and validate the returned properties match expectations.

### 3. Audit and Clean Up Unused Variables

1. Call GET (list) to retrieve all variables in the automation account.
2. If `nextLink` is present, follow pagination until all variables are collected.
3. Cross-reference variable names against runbook source code or known usage.
4. For each unused variable, call DELETE to remove it.
5. Re-run the list GET to confirm the cleanup is complete.

### 4. Migrate a Variable from Plaintext to Encrypted

1. Call GET on the existing plaintext variable to capture its current value and description.
2. Call DELETE to remove the plaintext variable.
3. Call PUT with the same variable name, setting `properties.isEncrypted` to `true` and `properties.value` to the captured value.
4. Confirm 201 response. The value is now stored encrypted and will return null on subsequent reads.

### 5. Bulk-Create Variables from a Configuration Map

1. Prepare a list of variable name/value pairs from your configuration source.
2. For each entry, call PUT with the variable name and `parameters` body containing `properties.value` and optionally `properties.description`.
3. Check each response: 201 means created, 200 means an existing variable was replaced -- log which occurred.
4. Call GET (list) to verify all expected variables are present and correct.
5. If any PUT failed (e.g., 409 conflict or 429 throttle), retry those entries after a backoff.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
