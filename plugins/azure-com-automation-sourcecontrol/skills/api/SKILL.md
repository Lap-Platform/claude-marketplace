---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2017-05-15-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName} | Create a source control. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName} | Update a source control. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName} | Delete the source control. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName} | Retrieve the source control identified by source control name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls | Retrieve a list of source controls. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a source control connection for my automation account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I link a GitHub repo to my Azure Automation account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I update the branch or repo URL on an existing source control?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I change the auto-sync setting on a source control?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I remove a source control integration from my automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I disconnect my repo from Azure Automation?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I get details about a specific source control?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "What repo is connected to my source control named X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "How do I list all source controls on my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls
- "How do I filter source controls by type?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls
- "How do I replace a source control config entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}
- "Does my automation account have any source controls configured?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls
- "How do I set up source control with a personal access token?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}

## Response Tips

- **PUT (Create/Replace):** Returns 200 for updates to existing source controls, 201 for newly created ones -- check the status code to confirm which occurred. Response body contains the full resource with `properties.repoUrl`, `properties.branch`, and `properties.sourceType`.
- **PATCH (Update):** Always returns 200; response contains the merged resource. Fields not included in the request body remain unchanged.
- **DELETE:** Returns 200 on success with no body. A 404 means the source control was already removed or never existed -- treat as idempotent.
- **GET (single):** Returns 200 with the full source control resource nested under `properties`. Security tokens are never returned in GET responses.
- **GET (list):** Returns 200 with a `value` array. Supports OData `$filter` for server-side filtering. Check for `nextLink` to handle pagination across large result sets.

## Anomaly Flags

- **201 vs 200 on PUT**: Surface when a PUT returns 201 (created) if the caller expected to update an existing resource -- this means a new source control was created, possibly due to a typo in `sourceControlName`.
- **Empty list results**: Flag when the list endpoint returns an empty `value` array, as it may indicate the automation account has no source controls configured or the `$filter` is too restrictive.
- **Missing properties fields**: Flag if the response is missing expected nested fields like `repoUrl` or `branch` -- may indicate a partially configured or corrupted source control.
- **Throttling (429)**: Azure ARM APIs enforce rate limits per subscription. Surface `Retry-After` header values and recommend exponential backoff.
- **Long-running operations**: If a PUT or DELETE returns 202 (Accepted) instead of 200/201, surface the `Azure-AsyncOperation` or `Location` header -- the operation requires polling.
- **API version mismatch**: This spec uses `2017-05-15-preview`. Flag if the caller is mixing calls with a different `api-version` query parameter, which can cause schema inconsistencies.

## Playbook

### 1. Connect a GitHub Repo to Azure Automation

1. Identify your `subscriptionId`, `resourceGroupName`, and `automationAccountName`.
2. Choose a `sourceControlName` (e.g., `my-github-repo`).
3. Call PUT with `parameters` containing `properties.repoUrl`, `properties.branch`, `properties.sourceType` (GitHub/VsoGit/VsoTfvc), and `properties.securityToken.accessToken`.
4. Confirm the response is 201 (created) or 200 (updated).
5. Call GET on the same source control name to verify the configuration is correct.

### 2. Update Source Control Branch

1. Call GET on the source control to retrieve its current configuration.
2. Call PATCH with `parameters` containing only `properties.branch` set to the new branch name.
3. Verify the 200 response shows the updated branch value.

### 3. Audit All Source Controls on an Automation Account

1. Call GET (list) with no `$filter` to retrieve all source controls.
2. If `nextLink` is present, follow it to retrieve additional pages.
3. For each source control in the `value` array, inspect `properties.sourceType` and `properties.autoSync` to build an audit summary.
4. Optionally call GET on individual source controls for full detail.

### 4. Safely Remove a Source Control Integration

1. Call GET on the source control to confirm it exists and note its current config.
2. Call DELETE to remove the source control.
3. Confirm the 200 response.
4. Call GET (list) to verify the source control no longer appears in the results.

### 5. Replace a Source Control Configuration

1. Call GET on the existing source control to capture its current state.
2. Call PUT with the complete new configuration in `parameters` -- this fully replaces the resource.
3. Check for 200 (replaced existing) vs 201 (created new -- indicates the original name may have been wrong).
4. Call GET to verify all fields match the intended configuration.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
