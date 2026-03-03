---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2018-06-30

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName} | Delete the python 2 package by name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName} | Retrieve the python 2 package identified by package name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName} | Create or Update the python 2 package identified by package name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName} | Update the python 2 package identified by package name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages | Retrieve a list of python 2 packages. |

## Enhanced Skill Content
## Question Mapping

- "How do I install a Python 2 package in my automation account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "What Python 2 packages are installed in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages
- "How do I check if a specific Python 2 package exists?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "How do I remove a Python 2 package from my automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "How do I update properties of an existing Python 2 package?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "Can I replace a Python 2 package with a newer version?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "How do I list all packages to audit what is installed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages
- "How do I get the provisioning state of a specific package?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "How do I add multiple Python 2 packages at once?" -> PUT (call sequentially per package)
- "How do I clean up unused Python 2 packages?" -> GET (list all) then DELETE (per package)
- "What version of a Python 2 package is currently installed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}
- "How do I change the content URI of a Python 2 package?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/python2Packages/{packageName}

## Response Tips

- **List packages (GET collection):** Response contains a `value` array of package objects plus an optional `nextLink` for pagination -- follow `nextLink` until absent to get all results.
- **Get/Put/Patch single package:** Response is a single package object with `properties.provisioningState` indicating install progress (`Creating`, `ContentValidated`, `ConnectionTypeImported`, `Running`, `Succeeded`, `Failed`).
- **Create package (PUT):** Returns 201 for new creation and 200 for update of existing package -- check status code to distinguish between the two.
- **Delete package (DELETE):** Returns 200 on success with no meaningful body -- a 404 means the package was already removed or never existed.
- **Error responses:** Azure returns `CloudError` objects with `error.code` and `error.message` -- always surface the `message` field to the user.

## Anomaly Flags

- **Provisioning failures:** If `properties.provisioningState` is `Failed` after a PUT or PATCH, surface immediately with the error details -- the package did not install correctly.
- **Stale provisioning state:** If `provisioningState` stays in `Creating` or `Running` for more than a few minutes after creation, flag as potentially stuck.
- **404 on GET/DELETE:** May indicate the automation account itself was deleted, not just the package -- suggest verifying the account still exists.
- **Pagination truncation:** If the list response contains `nextLink` but the agent only processed the first page, warn the user that results are incomplete.
- **Python 2 deprecation:** Python 2 reached end-of-life in January 2020. Proactively note that these are legacy packages and suggest evaluating Python 3 package endpoints if available.
- **201 vs 200 on PUT:** If the user intended to create a new package but received 200, flag that an existing package was overwritten rather than created fresh.
- **Rate limiting (429):** Azure ARM APIs enforce throttling -- if a 429 response is received, surface the `Retry-After` header value and pause before retrying.

## Playbook

### 1. Install a New Python 2 Package

1. Confirm the automation account exists by constructing the full resource path with `subscriptionId`, `resourceGroupName`, and `automationAccountName`.
2. Prepare the `parameters` body with `properties.contentLink.uri` pointing to the package source (e.g., a PyPI wheel URL).
3. Call PUT on `/python2Packages/{packageName}` with the parameters.
4. Check the response: 201 means created, 200 means an existing package was updated.
5. Poll the GET endpoint for the same package and monitor `properties.provisioningState` until it reaches `Succeeded` or `Failed`.

### 2. Audit and Clean Up Unused Packages

1. Call GET on `/python2Packages` to list all installed packages.
2. Follow any `nextLink` pagination to collect the complete list.
3. Review each package's `properties.provisioningState` and last-modified metadata.
4. Identify packages that are no longer referenced by any runbook.
5. For each unused package, call DELETE on `/python2Packages/{packageName}` and confirm 200 response.

### 3. Update an Existing Package Version

1. Call GET on `/python2Packages/{packageName}` to verify the package exists and note the current version.
2. Use PATCH on the same path with updated `properties` (e.g., new `contentLink.uri` pointing to the updated version).
3. Monitor `properties.provisioningState` via GET until it reaches `Succeeded`.
4. If provisioning fails, retrieve the error details from the GET response and consider rolling back by PUTting the previous version URI.

### 4. Bulk Package Provisioning

1. Prepare a list of package names and their corresponding content URIs.
2. For each package, call PUT on `/python2Packages/{packageName}` with the appropriate parameters.
3. Collect all package names that returned 201 (new) or 200 (updated).
4. Poll GET for each package in parallel, checking `provisioningState`.
5. Report a summary: count of succeeded, failed, and still-in-progress packages. Retry any failures after investigating error messages.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
