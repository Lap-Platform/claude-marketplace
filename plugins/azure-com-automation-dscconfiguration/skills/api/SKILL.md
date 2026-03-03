---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 6 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}/content -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName} | Delete the dsc configuration identified by configuration name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName} | Retrieve the configuration identified by configuration name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName} | Create the configuration identified by configuration name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName} | Create the configuration identified by configuration name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}/content | Retrieve the configuration script identified by configuration name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations | Retrieve a list of configurations. |

## Enhanced Skill Content
## Question Mapping

- "What DSC configurations exist in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations
- "Show me the details of a specific configuration" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}
- "How do I create a new DSC configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}
- "How do I update an existing configuration's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}
- "Delete a configuration I no longer need" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}
- "Download the raw script content of a configuration" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/configurations/{configurationName}/content
- "List only the first 10 configurations" -> GET /...configurations?$top=10
- "Filter configurations by provisioning state" -> GET /...configurations?$filter=provisioningState eq 'Succeeded'
- "How many configurations are in my account?" -> GET /...configurations?$inlinecount=allpages
- "Page through a large list of configurations" -> GET /...configurations?$top=N&$skip=M
- "Replace a configuration with a new version of the script" -> PUT /...configurations/{configurationName}
- "Change just the description or tags on a configuration" -> PATCH /...configurations/{configurationName}
- "Check if a configuration exists before creating it" -> GET /...configurations/{configurationName} (expect 200 or 404)
- "Remove a configuration and verify it was deleted" -> DELETE /...configurations/{configurationName} (expect 200 or 204)

## Response Tips

- **List endpoint (GET .../configurations):** Returns a paged array in `value[]`. Check `nextLink` for additional pages. Use `$inlinecount=allpages` to get `totalCount` alongside results. Each item includes `properties.state`, `properties.provisioningState`, and `location`.
- **Single configuration (GET .../configurations/{name}):** Returns the full resource object. Key fields are nested under `properties` -- look for `source`, `parameters`, `provisioningState`, and `lastModifiedTime`.
- **Content endpoint (GET .../content):** Returns raw PowerShell DSC script text (not JSON). Handle `Content-Type: text/powershell` or `application/octet-stream` accordingly.
- **Create/Update (PUT, PATCH):** PUT returns 200 (updated) or 201 (created) -- distinguish to know if a new resource was made. PATCH returns 200 only. Both return the full resource object in the body.
- **Delete (DELETE):** Returns 200 (deleted) or 204 (already gone / no content). Neither is an error -- both mean the resource is absent afterward.

## Anomaly Flags

- **204 on DELETE:** The configuration was already absent. Surface this so the user knows they may have targeted the wrong name or it was previously removed.
- **Provisioning state stuck:** If `properties.provisioningState` is not `Succeeded` after a PUT, flag that compilation or processing may have failed.
- **Empty configuration list with no filter:** If GET .../configurations returns zero results without a `$filter`, flag that the automation account may be misconfigured or the subscription/resource group path is wrong.
- **Missing `nextLink` with `$top` set:** If the response has exactly `$top` items but no `nextLink`, there may be more results than expected -- surface a warning to paginate explicitly.
- **OAuth token expiry:** Since this API uses OAuth2, watch for 401 responses mid-workflow and flag that token refresh is needed before retrying.
- **Throttling (429):** Azure ARM APIs enforce rate limits. Surface `Retry-After` header value and pause before continuing.

## Playbook

### 1. Create and Verify a New DSC Configuration

1. PUT /...configurations/{configurationName} with the `parameters` body containing `source.content` (the PowerShell DSC script) and `location`.
2. Check the response code: 201 means created, 200 means an existing config was replaced.
3. GET /...configurations/{configurationName} to confirm `provisioningState` is `Succeeded`.
4. GET /...configurations/{configurationName}/content to verify the uploaded script matches expectations.

### 2. List, Filter, and Page Through Configurations

1. GET /...configurations?$top=25&$inlinecount=allpages to get the first page and total count.
2. If `totalCount` exceeds 25, GET /...configurations?$top=25&$skip=25 for the next page.
3. Repeat incrementing `$skip` by `$top` until all results are retrieved.
4. Optionally add `$filter` to narrow results (e.g., by state or name prefix).

### 3. Update Configuration Metadata Without Replacing the Script

1. GET /...configurations/{configurationName} to retrieve current properties.
2. PATCH /...configurations/{configurationName} with only the fields to change (e.g., `tags`, `description`) in the `parameters` body.
3. Confirm the 200 response contains the updated values.

### 4. Safely Remove a Configuration

1. GET /...configurations/{configurationName} to verify the configuration exists and confirm its name/details.
2. DELETE /...configurations/{configurationName}.
3. If 200: deletion succeeded. If 204: it was already gone.
4. GET /...configurations/{configurationName} to confirm a 404, verifying full removal.

### 5. Export a Configuration Script for Backup

1. GET /...configurations to list all configurations in the account.
2. For each configuration, GET /...configurations/{configurationName}/content to retrieve the raw script.
3. Store each script locally, keyed by configuration name and `lastModifiedTime` from the metadata.
4. Use PATCH to tag configurations with a `lastBackedUp` timestamp after successful export.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
