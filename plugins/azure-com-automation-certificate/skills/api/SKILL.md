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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName} | Delete the certificate. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName} | Retrieve the certificate identified by certificate name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName} | Create a certificate. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName} | Update a certificate. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates | Retrieve a list of certificates. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all certificates in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates
- "How do I get details for a specific certificate?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I create a new certificate in Azure Automation?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I replace an existing automation certificate?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I update a certificate's description without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I delete a certificate from my automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I check if a specific certificate exists?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I rotate a certificate in Azure Automation?" -> DELETE then PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I rename a certificate?" -> PUT (new name) then DELETE (old name) on /certificates/{certificateName}
- "How do I find out when a certificate expires?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "How do I bulk audit all certificates across an automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates
- "How do I update only the description of a certificate?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates/{certificateName}
- "What certificates does my automation account have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/certificates

## Response Tips

- **List (GET /certificates):** Response includes a `value` array and possibly a `nextLink` field for pagination -- follow `nextLink` until absent to retrieve all certificates.
- **Single certificate (GET /certificates/{name}):** Returns the full certificate resource including `properties.expiryTime`, `properties.isExportable`, and `properties.thumbprint` nested under `properties`.
- **Create (PUT):** Returns 201 on new creation or 200 if a certificate with that name already existed and was replaced -- check the status code to distinguish.
- **Update (PATCH):** Returns 200; only fields included in the `parameters` body are modified, all others are left unchanged.
- **Delete (DELETE):** Returns 200 on success with no body; a 404 indicates the certificate was already removed or never existed.
- **Errors:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure -- always read `error.code` for programmatic handling.

## Anomaly Flags

- **Expiring certificates:** When listing or reading certificates, surface any where `properties.expiryTime` is within 30 days of the current date.
- **Non-exportable certificates:** Flag certificates where `properties.isExportable` is false, as these cannot be backed up or migrated.
- **201 vs 200 on PUT:** Alert the user if PUT returns 200 instead of 201, as this means an existing certificate was overwritten rather than a new one created.
- **Pagination truncation:** If a list response contains `nextLink`, warn that results are incomplete and additional pages must be fetched.
- **Throttling (429):** Azure ARM applies per-subscription rate limits -- surface `Retry-After` header values and recommend exponential backoff.
- **API version drift:** This spec targets `2015-10-31`; flag if Azure docs reference a newer `api-version` with additional certificate properties.

## Playbook

### 1. Create and Verify a New Certificate

1. Prepare the `parameters` body with `properties.base64Value` (base64-encoded .pfx/.cer), `properties.description`, and `properties.isExportable`.
2. PUT to `/certificates/{certificateName}` with the parameters body.
3. Confirm the response is 201 (new) -- if 200, an existing certificate was replaced.
4. GET `/certificates/{certificateName}` to verify `thumbprint` and `expiryTime` match expectations.

### 2. Rotate an Expiring Certificate

1. GET `/certificates/{certificateName}` to confirm current `expiryTime` and note existing properties.
2. Generate or obtain the new certificate file externally.
3. PUT `/certificates/{certificateName}` with updated `base64Value` in the parameters body (this replaces the certificate in place).
4. GET `/certificates/{certificateName}` to verify the new `thumbprint` and extended `expiryTime`.
5. Test any runbooks or DSC configurations that reference this certificate.

### 3. Audit All Certificates for Expiry

1. GET `/certificates` to retrieve the full list (follow `nextLink` for pagination).
2. For each certificate in the `value` array, parse `properties.expiryTime`.
3. Flag any certificates expiring within 30 days as critical, 90 days as warning.
4. For critical certificates, GET each one individually for full details to plan rotation.

### 4. Safely Remove an Unused Certificate

1. GET `/certificates/{certificateName}` to confirm it exists and note its properties.
2. Search your runbooks and DSC configurations to verify no active references to this certificate name or thumbprint.
3. DELETE `/certificates/{certificateName}` and confirm 200 response.
4. GET `/certificates/{certificateName}` to verify it returns 404 (fully removed).

### 5. Bulk Update Certificate Descriptions

1. GET `/certificates` to retrieve all certificates (follow `nextLink` for pagination).
2. For each certificate that needs a description update, PATCH `/certificates/{certificateName}` with `{ "properties": { "description": "updated text" } }`.
3. Confirm each PATCH returns 200.
4. GET `/certificates` again to verify descriptions are updated across the account.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
