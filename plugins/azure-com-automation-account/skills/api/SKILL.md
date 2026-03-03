---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions, providers. Covers 10 endpoints."
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
2. GET /providers/Microsoft.Automation/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/listKeys -- create first listKeys

## Endpoints

10 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName} | Update an automation account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName} | Create or update automation account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName} | Delete an automation account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName} | Get information about an Automation Account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts | Retrieve a list of accounts within a given resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Automation/automationAccounts | Lists the Automation Accounts within an Azure subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/statistics | Retrieve the statistics for the account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/usages | Retrieve the usage for the account id. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/listKeys | Retrieve the automation keys for an account. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Automation/operations | Lists all of the available Automation REST API operations. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new automation account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}
- "How do I update an existing automation account?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}
- "How do I delete an automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}
- "How do I get details of a specific automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}
- "How do I list all automation accounts in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts
- "How do I list all automation accounts in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Automation/automationAccounts
- "What operations are available for the Automation provider?" -> GET /providers/Microsoft.Automation/operations
- "How do I get usage data for an automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/usages
- "How do I view statistics for an automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/statistics
- "Can I filter statistics by date or type?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/statistics (use $filter query param)
- "How do I retrieve the keys for an automation account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/listKeys
- "How do I rename an automation account?" -> DELETE the old account, then PUT a new one (no rename endpoint exists)
- "How do I check if an automation account exists before creating it?" -> GET the specific account; 404 means it does not exist, then PUT to create

## Response Tips

- **Account CRUD (GET/PUT/PATCH/DELETE):** Responses wrap the account resource in a standard Azure envelope with `id`, `name`, `type`, `location`, and `properties`. PUT returns 201 on creation, 200 on update -- check the status code to distinguish. DELETE returns 200 on success, 204 if already gone.
- **List endpoints:** Results come as `{ value: [...] }` arrays. Watch for `nextLink` for pagination -- keep following it until absent.
- **Statistics/Usages:** Returns arrays of metric objects inside `value`. Statistics supports OData `$filter` for narrowing results by counter name or time range.
- **listKeys:** Returns key objects directly. Treat these as secrets -- do not log or persist in plain text.
- **Operations:** Returns the full provider operation catalog; useful for RBAC and audit tooling, not day-to-day use.

## Anomaly Flags

- **204 on DELETE:** The account was already deleted or never existed. Surface this so the caller knows the operation was a no-op.
- **PUT returning 200 instead of 201:** The account already existed and was overwritten rather than freshly created. Flag when the caller expected a new resource.
- **Throttling (429 or Retry-After header):** Azure ARM applies rate limits per subscription. Surface immediately with the retry interval.
- **$filter ignored:** If statistics return unfiltered results despite a filter, the expression may be malformed. Warn the caller.
- **Empty value arrays on list calls:** Could mean the resource group or subscription has no automation accounts, or the caller lacks read permissions. Suggest checking IAM assignments.
- **Stale keys after rotation:** If listKeys is called and the returned keys do not match cached values, proactively flag that key rotation has occurred.
- **Long-running operations:** If PUT or DELETE returns a 202 with an `Azure-AsyncOperation` header, the operation is not yet complete. Surface the polling URL and expected wait time.

## Playbook

### 1. Provision a New Automation Account

1. Call GET on the specific account path to confirm it does not already exist (expect 404).
2. Call PUT with the account name, location, and desired SKU in the request body.
3. Confirm a 201 response indicating successful creation.
4. Call GET on the account to verify properties are set correctly.
5. Call POST /listKeys to retrieve the initial access keys for runbook authentication.

### 2. Audit All Automation Accounts Across a Subscription

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Automation/automationAccounts to list all accounts.
2. Follow any `nextLink` values to paginate through the full set.
3. For each account, call GET /statistics with a `$filter` on the last 24 hours to spot idle or overloaded accounts.
4. Call GET /usages for each account to check quota consumption.
5. Compile results into a summary, flagging accounts with zero recent activity or usage near limits.

### 3. Rotate Automation Account Keys

1. Call POST /listKeys to retrieve the current primary and secondary keys.
2. Update all dependent runbooks and integrations to use the secondary key.
3. Call PATCH on the automation account or use the key regeneration mechanism (outside this API surface) to rotate the primary key.
4. Call POST /listKeys again to confirm the new primary key value.
5. Update integrations back to the new primary key once confirmed.

### 4. Tear Down an Automation Account

1. Call GET on the specific account to confirm it exists and note its current state.
2. Call GET /statistics and GET /usages to capture final metrics for archival.
3. Call POST /listKeys and revoke or decommission any keys in external systems.
4. Call DELETE on the account. Expect 200 for successful deletion.
5. Call GET again to verify a 404, confirming the account is fully removed.

### 5. Discover Available Automation Operations for RBAC Planning

1. Call GET /providers/Microsoft.Automation/operations to retrieve the full operation catalog.
2. Parse each operation's `name` field (e.g., `Microsoft.Automation/automationAccounts/read`) to map to Azure RBAC action strings.
3. Group operations by resource type (accounts, runbooks, schedules) to identify required permissions per role.
4. Cross-reference with your existing custom role definitions to find gaps or excessive grants.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
