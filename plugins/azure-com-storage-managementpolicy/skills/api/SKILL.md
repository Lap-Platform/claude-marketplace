---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2018-03-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Gets the data policy rules associated with the specified storage account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Sets the data policy rules associated with the specified storage account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName} | Deletes the data policy rules associated with the specified storage account. |

## Enhanced Skill Content
## Question Mapping

- "What lifecycle management policy is set on my storage account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Show the current blob tiering rules for a storage account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Does this storage account have a lifecycle policy configured?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Create a lifecycle management policy for my storage account" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Set up automatic blob tiering from hot to cool after 30 days" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Add a rule to delete blobs older than 365 days" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Update the existing lifecycle policy with a new rule" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Replace the management policy on my storage account" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Remove the lifecycle management policy from my storage account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Delete all blob tiering and expiration rules" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "How do I move blobs to archive tier automatically?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "Check if a specific management policy exists before creating one" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}
- "How do I configure auto-delete for snapshots?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}/managementPolicies/{managementPolicyName}

## Response Tips

- **GET (200):** Returns the full policy object with `properties.policy.rules[]` -- each rule contains `name`, `type`, `definition` with `filters` and `actions` (tierToCool, tierToArchive, delete with `daysAfterModificationGreaterThan`). A 404 means no policy exists yet, not an error.
- **PUT (200):** Returns the created or updated policy object. The `properties` body must include the complete rule set -- this is a full replace, not a merge. Omitting existing rules removes them.
- **DELETE (200/204):** 200 confirms deletion with a body; 204 means the policy was already absent. Both are success -- do not treat 204 as an error.

## Anomaly Flags

- **404 on GET:** No policy exists for this account. Surface this clearly rather than treating it as a failure -- the user may need to create one.
- **PUT silently drops rules:** Since PUT replaces the entire policy, warn the user if they are adding a rule to fetch the existing policy first and merge rules client-side, or they will lose existing rules.
- **managementPolicyName is always "default":** The Azure API only supports a single policy named `default`. Flag if the user attempts a different name -- it will fail.
- **Preview API version (2018-03-01-preview):** This is a preview version. Surface a note that behavior may change and recommend checking for GA versions.
- **Missing subscription/resource context:** If path parameters (subscriptionId, resourceGroupName, accountName) are not set, surface this early rather than letting the request fail with a generic error.
- **Rule definition errors:** If a PUT returns 400, it is almost always a malformed rule definition. Surface the `error.message` field, which typically pinpoints the invalid property.

## Playbook

### 1. Set Up Blob Lifecycle Tiering (Cool after 30 days, Archive after 90, Delete after 365)

1. GET the existing policy to check if one already exists (expect 404 if none)
2. PUT a new policy with `managementPolicyName` = `default` and a `properties` body containing rules:
   - Rule 1: `tierToCool` with `daysAfterModificationGreaterThan: 30`
   - Rule 2: `tierToArchive` with `daysAfterModificationGreaterThan: 90`
   - Rule 3: `delete` with `daysAfterModificationGreaterThan: 365`
3. GET the policy again to confirm the rules were applied correctly
4. Verify the response `properties.policy.rules` array contains all three actions

### 2. Add a Rule to an Existing Policy Without Losing Current Rules

1. GET the current policy to retrieve `properties.policy.rules[]`
2. Append the new rule to the existing rules array client-side
3. PUT the full policy back with all rules (existing + new) in the `properties` body
4. GET the policy to verify the new rule appears alongside the original rules

### 3. Remove All Lifecycle Rules from a Storage Account

1. GET the current policy to confirm it exists and review what will be deleted
2. DELETE the policy using `managementPolicyName` = `default`
3. Confirm the response is 200 or 204 (both indicate success)
4. Optionally GET to verify a 404 is returned, confirming the policy is gone

### 4. Audit Lifecycle Policies Across Multiple Storage Accounts

1. For each storage account, GET the management policy with `managementPolicyName` = `default`
2. Record whether a policy exists (200) or is absent (404)
3. For accounts with policies, extract and compare the rules definitions
4. Flag accounts missing policies or with rules that deviate from organizational standards (e.g., no deletion rule, overly short tiering windows)

### 5. Replace a Misconfigured Policy

1. GET the current policy to understand what is misconfigured
2. Construct the corrected `properties` body with the intended rule set
3. PUT the corrected policy -- this fully replaces the previous configuration
4. GET the policy to verify the corrected rules are in place
5. If the PUT returns 400, inspect `error.message` for rule definition issues and correct the request body


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
