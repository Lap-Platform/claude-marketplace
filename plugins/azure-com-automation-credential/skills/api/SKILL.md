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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName} | Delete the credential. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName} | Retrieve the credential identified by credential name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName} | Create a credential. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName} | Update a credential. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials | Retrieve a list of credentials. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all credentials in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials
- "How do I get details for a specific credential?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I create a new credential in my automation account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I update an existing credential's description or username?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I delete a credential from my automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I rotate a credential's password?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "Does a specific credential exist in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I replace a credential entirely with new parameters?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I audit which credentials are configured for a given automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials
- "How do I remove a compromised credential immediately?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I rename a credential?" -> PUT (create new) + DELETE (remove old) on /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}
- "How do I check if a credential update succeeded?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/credentials/{credentialName}

## Response Tips

- **List credentials (GET .../credentials):** Response may be paginated via `nextLink`; follow it until absent to retrieve all credentials. Each entry includes metadata but never exposes the password value.
- **Single credential (GET .../credentials/{name}):** Returns the full credential object with `properties.userName` and `properties.description`, but `properties.password` is always omitted for security. A 404 means the credential does not exist.
- **Create (PUT):** Returns 201 for new credentials, 200 if one with that name already existed and was replaced. The `parameters` body must include `properties.userName` and `properties.password`.
- **Update (PATCH):** Returns 200 on success. Only the fields provided in `parameters` are modified; omitted fields remain unchanged.
- **Delete (DELETE):** Returns 200 on success with no body. A 404 indicates the credential was already removed or never existed.

## Anomaly Flags

- **404 on GET/DELETE:** Surface immediately -- the credential name may be misspelled or already deleted. Suggest listing all credentials to verify.
- **200 instead of 201 on PUT:** Warn the user that an existing credential was overwritten, not created fresh. This may be unintentional.
- **Password never returned:** If the user expects to read back a stored password, proactively explain that Azure never exposes credential passwords in GET responses -- this is by design, not an error.
- **OAuth2 token expiry:** If a 401 is returned on any call, flag that the bearer token may have expired and prompt re-authentication.
- **Throttling (429):** Azure Resource Manager enforces rate limits per subscription. Surface retry-after headers and suggest spacing requests when listing large numbers of credentials.
- **API version mismatch:** This spec targets `2015-10-31`. If the user references newer credential features (e.g., managed identities), flag that a newer api-version may be required.

## Playbook

### 1. Create a New Credential

1. Confirm the subscription ID, resource group, and automation account name.
2. Choose a credential name (must be unique within the automation account).
3. Send PUT to `.../credentials/{credentialName}` with a body containing `properties.userName` and `properties.password`.
4. Verify creation by checking for a 201 response.
5. Optionally, GET the credential to confirm `userName` and `description` are stored correctly (password will not be returned).

### 2. Rotate a Credential's Password

1. GET the existing credential to confirm its current `userName` and `description`.
2. Send PATCH to `.../credentials/{credentialName}` with `properties.password` set to the new value.
3. Confirm a 200 response indicating the update succeeded.
4. Test downstream runbooks or configurations that depend on this credential to ensure they work with the new password.

### 3. Audit All Credentials in an Automation Account

1. Send GET to `.../credentials` to list all credentials.
2. Follow any `nextLink` values to paginate through the full list.
3. For each credential, note the `userName`, `description`, and `lastModifiedTime`.
4. Flag any credentials with missing descriptions or stale modification dates for review.

### 4. Safely Remove a Credential

1. GET the credential to confirm it exists and review its details.
2. Check automation runbooks to ensure no active jobs depend on this credential.
3. Send DELETE to `.../credentials/{credentialName}`.
4. Confirm a 200 response.
5. List all credentials to verify it no longer appears.

### 5. Rename a Credential

1. GET the existing credential to capture its `userName` and `description`.
2. Send PUT to `.../credentials/{newCredentialName}` with the same `userName`, `password`, and `description`.
3. Confirm a 201 response for the new credential.
4. Update any runbooks referencing the old credential name to use the new name.
5. Send DELETE to `.../credentials/{oldCredentialName}` to remove the old entry.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
