---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName} | Delete the connection type. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName} | Retrieve the connection type identified by connection type name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName} | Create a connection type. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes | Retrieve a list of connection types. |

## Enhanced Skill Content
## Question Mapping

- "What connection types are available in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes
- "Get details for a specific connection type" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "How do I create a new connection type?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Delete a connection type I no longer need" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Does a particular connection type exist in my account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "List all connection types for a resource group's automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes
- "Register a custom connection type with field definitions" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Remove a deprecated connection type from my automation account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Why did my connection type creation fail with a conflict?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Check what field definitions a connection type has before deleting it" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Replace a connection type by deleting and recreating it" -> DELETE then PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes/{connectionTypeName}
- "Audit which connection types are configured across my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/connectionTypes

## Response Tips

- **List endpoint (GET .../connectionTypes):** Response may be paginated via `nextLink`; follow it until absent to retrieve all results.
- **Get single (GET .../connectionTypes/{name}):** Returns the full connection type definition including field definitions; a 404 means the name does not exist.
- **Create (PUT):** Returns 201 on success; a 409 Conflict means a connection type with that name already exists -- you must delete it first or choose a different name.
- **Delete:** Returns 200 if the resource was deleted, 204 if it did not exist (idempotent); treat both as success.

## Anomaly Flags

- **409 Conflict on PUT**: Surface immediately -- the connection type already exists. Prompt the user to delete first or use a different name.
- **204 on DELETE**: Inform the user the connection type was already absent; no action was needed.
- **Pagination present**: If `nextLink` appears in a list response, warn that results are incomplete and offer to fetch the next page.
- **OAuth2 token expiry**: If any call returns 401, surface that the token may have expired and re-authentication is required.
- **Missing required `parameters` body on PUT**: The `parameters` field is required for creation; flag if the user attempts a PUT without providing field definitions.
- **API version drift**: This spec targets `2015-10-31`; surface a note if the user references newer features that may require a later api-version.

## Playbook

### 1. Inventory All Connection Types

1. Call GET .../connectionTypes to list all connection types in the automation account.
2. If the response contains a `nextLink`, follow it to get the next page.
3. Repeat until no `nextLink` is returned.
4. Compile the full list of names and their field definitions.

### 2. Create a New Connection Type

1. Call GET .../connectionTypes/{connectionTypeName} to check if the name is already taken.
2. If it returns 200, either choose a different name or delete the existing one first (see Playbook 4).
3. Construct the `parameters` body with the connection type's field definitions (name, type, isEncrypted, isOptional).
4. Call PUT .../connectionTypes/{connectionTypeName} with the parameters.
5. Confirm a 201 response indicating successful creation.

### 3. Inspect a Connection Type Before Use

1. Call GET .../connectionTypes/{connectionTypeName}.
2. Review the `fieldDefinitions` in the response to understand required fields.
3. Note which fields are marked `isEncrypted` (sensitive) and `isOptional`.
4. Use this information to populate connection assets correctly.

### 4. Replace an Existing Connection Type

1. Call GET .../connectionTypes/{connectionTypeName} to capture the current definition.
2. Call DELETE .../connectionTypes/{connectionTypeName} and confirm a 200 or 204 response.
3. Modify the field definitions as needed in the parameters body.
4. Call PUT .../connectionTypes/{connectionTypeName} with the updated parameters.
5. Confirm a 201 response, then verify with a final GET to validate the new definition.

### 5. Clean Up Unused Connection Types

1. Call GET .../connectionTypes to list all connection types.
2. Identify connection types that are no longer referenced by any runbook or connection asset.
3. For each unused connection type, call DELETE .../connectionTypes/{connectionTypeName}.
4. Confirm 200 or 204 for each deletion.
5. Re-list with GET .../connectionTypes to verify the cleanup is complete.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
