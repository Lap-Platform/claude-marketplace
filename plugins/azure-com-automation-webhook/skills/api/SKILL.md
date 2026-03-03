---
name: automationmanagementclient
description: "AutomationManagementClient API skill. Use when working with AutomationManagementClient for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagementClient
API version: 2015-10-31

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/generateUri -- create first generateUri

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/generateUri | Generates a Uri for use in creating a webhook. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName} | Delete the webhook by name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName} | Retrieve the webhook identified by webhook name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName} | Create the webhook identified by webhook name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName} | Update the webhook identified by webhook name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks | Retrieve a list of webhooks. |

## Enhanced Skill Content
## Question Mapping

- "How do I generate a new webhook URI for my automation account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/generateUri
- "How do I create a webhook in Azure Automation?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName}
- "How do I delete a webhook?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName}
- "How do I get details about a specific webhook?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName}
- "How do I list all webhooks in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks
- "How do I update an existing webhook's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName}
- "How do I replace a webhook configuration entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName}
- "How do I filter webhooks by a specific runbook?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks (use `$filter` parameter)
- "How do I rotate a webhook URI without deleting the webhook?" -> POST .../webhooks/generateUri then PATCH .../webhooks/{webhookName}
- "How do I check if a webhook exists before creating it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName} (check for 404 vs 200)
- "How do I disable a webhook temporarily?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/webhooks/{webhookName} (set isEnabled to false in parameters)
- "How do I set up a new webhook end-to-end for a runbook?" -> POST .../generateUri then PUT .../webhooks/{webhookName}
- "How do I clean up all webhooks in an automation account?" -> GET .../webhooks then DELETE .../webhooks/{webhookName} for each

## Response Tips

- **generateUri (POST)**: Returns a single URI string -- store it immediately, as it cannot be retrieved again after creation.
- **Single webhook (GET/PUT/PATCH)**: Response contains a top-level `properties` object with `uri`, `isEnabled`, `expiryTime`, `runbook`, and `parameters` nested inside it.
- **List webhooks (GET)**: Returns a `value` array with `nextLink` for pagination -- keep fetching `nextLink` until it is null. The `$filter` param accepts OData syntax.
- **Create (PUT)**: Returns 200 if the webhook already existed (update), 201 if newly created -- check the status code to distinguish.
- **Delete (DELETE)**: Returns 200 on success with no body. A 404 means the webhook was already removed.
- **Errors**: Standard Azure error envelope `{ "error": { "code": "...", "message": "..." } }` -- always read `error.code` for programmatic handling and `error.message` for user-facing output.

## Anomaly Flags

- **URI shown only once**: The webhook URI from generateUri or PUT (201) is returned exactly once. If the agent detects the user did not capture it, surface a warning immediately.
- **Expired webhooks**: When GET returns a webhook with `expiryTime` in the past, flag it -- the webhook will silently reject incoming calls.
- **Disabled webhooks**: If `isEnabled` is false on a webhook the user expects to be active, surface this proactively.
- **PUT returning 200 instead of 201**: The user may think they are creating a new webhook but are actually overwriting an existing one. Flag the distinction.
- **Pagination truncation**: If the list response contains `nextLink`, warn the user that results are incomplete and additional pages exist.
- **OAuth token scope**: If a 403 is returned, flag that the service principal may lack `Microsoft.Automation/automationAccounts/webhooks/*` permissions on the target resource group.
- **API version drift**: This spec targets `2015-10-31`. If Azure returns errors suggesting a newer `api-version` is required, surface that the spec may be outdated.

## Playbook

### 1. Create a New Webhook for a Runbook

1. Call POST `.../webhooks/generateUri` to obtain a unique, one-time webhook URI.
2. Store the returned URI securely -- it will not be retrievable later.
3. Call PUT `.../webhooks/{webhookName}` with `parameters` containing the URI, target runbook name, `isEnabled: true`, and an `expiryTime`.
4. Verify the response status is 201 (created). If 200, a webhook with that name already existed and was overwritten.
5. Test the webhook by sending an HTTP POST to the URI and confirming the runbook executes.

### 2. Rotate a Webhook URI

1. Call POST `.../webhooks/generateUri` to get a fresh URI.
2. Call PATCH `.../webhooks/{webhookName}` with the new URI in `parameters`.
3. Confirm the response is 200 and the updated `properties.uri` reflects the change.
4. Update any external systems that call the old URI to use the new one.
5. Test the new URI to confirm end-to-end functionality.

### 3. Audit and Clean Up Expired Webhooks

1. Call GET `.../webhooks` to list all webhooks (follow `nextLink` pagination until exhausted).
2. For each webhook, check `properties.expiryTime` -- collect any where the expiry is in the past.
3. For each expired webhook, call DELETE `.../webhooks/{webhookName}`.
4. Confirm each DELETE returns 200.
5. Re-run the list call to verify only active webhooks remain.

### 4. Temporarily Disable and Re-enable a Webhook

1. Call GET `.../webhooks/{webhookName}` to confirm current state and that `isEnabled` is true.
2. Call PATCH `.../webhooks/{webhookName}` with `parameters` setting `isEnabled: false`.
3. Verify the response shows `properties.isEnabled` as false.
4. When ready to re-enable, call PATCH again with `isEnabled: true`.
5. Test the webhook URI to confirm it is accepting requests again.

### 5. List and Filter Webhooks by Criteria

1. Call GET `.../webhooks` with `$filter` set to an OData expression (e.g., `properties/runbook/name eq 'MyRunbook'`).
2. Parse the `value` array from the response.
3. If `nextLink` is present, fetch the next page by calling GET on the `nextLink` URL.
4. Repeat until `nextLink` is null.
5. Process the aggregated results for reporting or further operations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
