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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName} | Delete the connection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName} | Retrieve the connection identified by connection name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName} | Create or update a connection. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName} | Update a connection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections | Retrieve a list of connections. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all connections in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections
- "How do I get details for a specific connection?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I create a new connection in Azure Automation?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I delete a connection from my automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I update an existing connection's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I check if a specific connection exists?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I replace a connection with new configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I rename a connection?" -> DELETE old + PUT new (multi-step: connections are keyed by name, so delete the old and create with the new name)
- "How do I verify a connection's credentials are still valid?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I rotate credentials on a connection?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections/{connectionName}
- "How do I audit which connections exist across my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connections
- "How do I remove an unused connection safely?" -> GET the connection first, then DELETE it
- "How do I clone a connection to another automation account?" -> GET from source, then PUT to target account

## Response Tips

- **List connections (GET .../connections):** Response is paginated via `nextLink`; follow it until absent. Each item contains `name`, `properties.connectionType`, and `properties.fieldDefinitionValues`.
- **Single connection (GET .../connections/{name}):** Returns the full connection object. A 404 means the connection does not exist -- do not confuse with auth errors (401/403).
- **Create (PUT):** Returns 201 for new connections, 200 if it replaced an existing one. The `parameters` body must include `connectionType` and `fieldDefinitionValues`.
- **Update (PATCH):** Returns 200 on success. Only fields included in the request body are modified; omitted fields remain unchanged.
- **Delete (DELETE):** Returns 200 on successful deletion, 204 if the connection was already absent. Both are success states -- do not treat 204 as an error.

## Anomaly Flags

- **204 on DELETE**: The connection was already gone before the delete call -- surface this so the user knows it was a no-op.
- **PUT returning 200 instead of 201**: The connection already existed and was overwritten. Alert the user that existing configuration was replaced, not created fresh.
- **Throttling (429)**: Azure ARM APIs enforce per-subscription rate limits. If you receive 429 with a `Retry-After` header, surface the wait time and pause before retrying.
- **Async provisioning**: If any response returns 202 with a `Location` or `Azure-AsyncOperation` header, the operation is not yet complete. Poll the provided URL until terminal state.
- **Deprecated api-version**: If the response includes a `Sunset` or `Deprecation` header, flag that the 2015-10-31 API version may be retiring and recommend checking for newer versions.
- **Missing connectionType on GET**: If a connection's `properties.connectionType` is null or empty, this is abnormal and may indicate a corrupted resource.

## Playbook

### 1. Create a New Automation Connection

1. Confirm the automation account exists: ensure you have `subscriptionId`, `resourceGroupName`, and `automationAccountName`.
2. Build the request body with `name`, `properties.connectionType` (e.g., `Azure`, `AzureServicePrincipal`), and `properties.fieldDefinitionValues` containing the credential fields.
3. Call PUT .../connections/{connectionName} with the parameters body.
4. Verify the response: 201 means created, 200 means an existing connection was replaced.
5. Call GET .../connections/{connectionName} to confirm the connection is fully provisioned.

### 2. Rotate Credentials on an Existing Connection

1. Call GET .../connections/{connectionName} to retrieve current connection details and its `connectionType`.
2. Prepare a PATCH body containing only the updated `fieldDefinitionValues` (e.g., new certificate thumbprint, new password).
3. Call PATCH .../connections/{connectionName} with the update body.
4. Verify the response is 200 and the returned `fieldDefinitionValues` reflect the new credentials.
5. Test the connection from a runbook to confirm it works with the new credentials.

### 3. Audit and Clean Up Unused Connections

1. Call GET .../connections to list all connections in the automation account.
2. Follow `nextLink` pagination until all connections are retrieved.
3. For each connection, cross-reference with runbook source code or job history to determine usage.
4. For connections identified as unused, call DELETE .../connections/{connectionName}.
5. Log whether each delete returned 200 (deleted) or 204 (already absent) for audit trail.

### 4. Migrate a Connection Between Automation Accounts

1. Call GET .../connections/{connectionName} on the source automation account to retrieve full configuration.
2. Extract the `connectionType` and `fieldDefinitionValues` from the response.
3. Build a PUT request body using the extracted values, targeting the destination automation account.
4. Call PUT .../connections/{connectionName} on the destination account.
5. Verify with GET on the destination account, then optionally DELETE from the source account.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
