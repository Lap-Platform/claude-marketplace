---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 10 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/activities -- verify access

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/activities/{activityName} | Retrieve the activity in the module identified by module name and activity name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/activities | Retrieve a list of activities in the module identified by module name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName} | Delete the module by name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName} | Retrieve the module identified by module name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName} | Create or Update the module identified by module name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName} | Update the module identified by module name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules | Retrieve a list of modules. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/objectDataTypes/{typeName}/fields | Retrieve a list of fields of a given type identified by module name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/objectDataTypes/{typeName}/fields | Retrieve a list of fields of a given type across all accessible modules. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/types/{typeName}/fields | Retrieve a list of fields of a given type identified by module name. |

## Enhanced Skill Content
## Question Mapping

- "What modules are installed in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules
- "Get details about a specific module" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}
- "What activities are available in a module?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/activities
- "Get details for a specific activity in a module" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/activities/{activityName}
- "How do I install or create a new module?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}
- "How do I update an existing module's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}
- "Remove a module from my automation account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}
- "What fields does a type expose within a module?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/objectDataTypes/{typeName}/fields
- "What fields does a type have at the account level?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/objectDataTypes/{typeName}/fields
- "List type fields using the /types/ path for a module" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/types/{typeName}/fields
- "Is a specific module already installed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}
- "What parameters does a runbook activity accept?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}/activities/{activityName}
- "Replace a module with a newer version?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/modules/{moduleName}

## Response Tips

- **Module listings** (GET .../modules): Returns a paginated `value` array with `nextLink` for continuation; each item includes `properties.provisioningState` indicating install progress.
- **Single module** (GET/PUT/PATCH .../modules/{moduleName}): Returns the full resource object; check `properties.provisioningState` for Created, Running, Succeeded, or Failed before using.
- **Activities** (GET .../activities): Returns a `value` array of activity definitions; each entry contains `properties.definition` with parameter sets and output types.
- **Type fields** (GET .../fields): Returns a `value` array of field descriptors with `fieldName` and `fieldType`; three endpoints return the same shape -- pick the one matching your scope (module-scoped objectDataTypes, account-scoped objectDataTypes, or module-scoped types).
- **Create/Update** (PUT returns 200 or 201): 201 means newly created, 200 means replaced existing; both return the resource body.
- **Delete** (DELETE .../modules/{moduleName}): Returns 200 on success with no body; a 404 means the module was already absent.
- **Errors**: Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; watch for ResourceNotFound (404) and AuthorizationFailed (403).

## Anomaly Flags

- **provisioningState != Succeeded**: After PUT/PATCH, if the module's `properties.provisioningState` is `Failed` or stays at `Running` for more than a few minutes, surface this immediately -- the module is not usable until provisioning completes.
- **HTTP 429 (Too Many Requests)**: Azure ARM enforces throttling; surface `Retry-After` header value and pause before retrying.
- **404 on module GET after PUT**: A race condition where provisioning hasn't registered the resource yet; flag and suggest a short retry.
- **Empty activities list**: If a module returns zero activities, flag that the module may still be provisioning or may be a data-only module with no cmdlets.
- **Deprecated api-version**: This spec uses `2015-10-31`; if Azure returns warnings or `x-ms-deprecated` headers, surface them -- a newer API version may be available.
- **Mismatched field endpoints**: Three endpoints return type fields with subtly different scopes (objectDataTypes vs types); flag if results differ for the same typeName, as it may indicate module version conflicts.

## Playbook

### 1. Install a new PowerShell module

1. PUT to `.../modules/{moduleName}` with `parameters` body containing `properties.contentLink.uri` pointing to the module .zip package URL.
2. Poll GET `.../modules/{moduleName}` until `properties.provisioningState` returns `Succeeded`.
3. Verify available cmdlets by calling GET `.../modules/{moduleName}/activities`.

### 2. Update an existing module

1. GET `.../modules/{moduleName}` to confirm the module exists and note its current version.
2. PATCH `.../modules/{moduleName}` with `parameters` containing only the properties to update (e.g., new `contentLink.uri` for a version upgrade).
3. Poll GET `.../modules/{moduleName}` until `provisioningState` is `Succeeded`.
4. List activities again (GET `.../modules/{moduleName}/activities`) to confirm new cmdlets are available.

### 3. Audit all modules and their activities

1. GET `.../modules` to list all installed modules; follow `nextLink` for pagination.
2. For each module in the response, GET `.../modules/{moduleName}/activities` to enumerate available activities.
3. Optionally inspect activity details by calling GET `.../activities/{activityName}` for parameter definitions.
4. Compile results into a manifest of module names, versions, provisioning states, and activity counts.

### 4. Inspect type schema for a module's output types

1. GET `.../modules/{moduleName}/activities/{activityName}` to identify output types used by the activity.
2. GET `.../modules/{moduleName}/objectDataTypes/{typeName}/fields` to retrieve field definitions for that type.
3. If you need account-level type resolution (not scoped to a module), use GET `.../objectDataTypes/{typeName}/fields` instead.

### 5. Safely remove a module

1. GET `.../modules/{moduleName}/activities` to check if any activities are referenced by existing runbooks (manual verification step).
2. DELETE `.../modules/{moduleName}` to remove it.
3. Confirm removal by calling GET `.../modules/{moduleName}` -- expect a 404 response.
4. If 200 is returned instead, the module may still be deprovisioning; wait and retry the GET.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
