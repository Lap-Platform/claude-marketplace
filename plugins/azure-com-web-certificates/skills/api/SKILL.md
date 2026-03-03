---
name: certificates-api-client
description: "Certificates API Client API skill. Use when working with Certificates API Client for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Certificates API Client
API version: 2018-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/certificates -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/certificates | Get all certificates for a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates | Get all certificates in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name} | Get a certificate. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name} | Create or update a certificate. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name} | Delete a certificate. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name} | Create or update a certificate. |

## Enhanced Skill Content
## Question Mapping

- "What certificates exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/certificates
- "List all certificates in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates
- "Get details for a specific certificate?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "How do I upload or create a new certificate?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "How do I replace an existing certificate?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "How do I delete a certificate?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "How do I update certificate properties without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "Is a specific certificate still valid or expiring soon?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "Which resource group contains certificate X?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/certificates
- "How do I rename or move a certificate?" -> DELETE old + PUT new (multi-step)
- "Does a certificate already exist before I create it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}
- "How do I update just the tags on a certificate?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}

## Response Tips

- **List endpoints (GET collection):** Response contains a `value` array of certificate objects. Check for `nextLink` property for pagination -- follow it until absent.
- **Detail endpoint (GET single):** Returns a single certificate resource with `properties` nested object containing expiration date, thumbprint, and host names.
- **Create/Update (PUT, PATCH):** Returns the full certificate resource as created or modified. 200 means success; no 201 distinction, so both create and update return 200.
- **Delete:** 200 means deleted successfully. 204 means the certificate was already gone (idempotent). A 404 should not occur -- treat it as an anomaly if it does.
- **All endpoints:** Errors follow Azure standard format with `error.code` and `error.message`. Always pass `api-version=2018-11-01` as a query parameter.

## Anomaly Flags

- **Certificate expiration approaching:** When GET returns a certificate whose `properties.expirationDate` is within 30 days, surface a warning proactively.
- **API version staleness:** This spec uses `2018-11-01`. If Azure returns deprecation headers or newer `api-version` values in error messages, flag that the version may be outdated.
- **204 on DELETE:** A 204 response means the resource was already absent. Surface this so the user knows the certificate was not found rather than assuming it was just deleted.
- **Empty list results:** If a subscription-wide list returns zero certificates, confirm the subscription ID is correct -- this may indicate a wrong subscription or permissions issue.
- **Auth failures (401/403):** OAuth2 token may have expired or lack the `Microsoft.Web/certificates/*` permission scope. Prompt the user to check their Azure role assignment.
- **Throttling (429):** Azure ARM has rate limits per subscription. If a 429 appears, surface the `Retry-After` header value and pause before retrying.

## Playbook

### 1. Inventory all certificates across a subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Web/certificates` with `api-version=2018-11-01`.
2. Collect the `value` array from the response.
3. If `nextLink` is present, follow it with another GET until no `nextLink` remains.
4. For each certificate, note `properties.expirationDate` and flag any expiring within 30 days.

### 2. Upload a new certificate to a resource group

1. Call GET on the target certificate name to confirm it does not already exist (expect 404 or an error).
2. Construct the `certificateEnvelope` body with required properties (PFX blob, password, host names).
3. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}` with the envelope as the request body.
4. Verify the 200 response contains the certificate with the correct thumbprint and expiration date.

### 3. Rotate an expiring certificate

1. Call GET on the existing certificate to retrieve its current properties and resource group.
2. Prepare a new `certificateEnvelope` with the updated PFX blob and password.
3. Call PUT with the same name to replace the certificate in-place (returns 200 with updated resource).
4. Verify `properties.thumbprint` has changed and `properties.expirationDate` reflects the new certificate.

### 4. Clean up unused certificates

1. Call GET at the subscription level to list all certificates.
2. Identify candidates for removal (expired, unbound, or tagged for cleanup).
3. For each candidate, call DELETE `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}`.
4. Expect 200 (deleted) or 204 (already gone). Log any unexpected errors.

### 5. Update tags on an existing certificate

1. Call GET on the certificate to confirm it exists and retrieve its current tags.
2. Construct a partial `certificateEnvelope` containing only the updated `tags` map.
3. Call PATCH `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/certificates/{name}` with the envelope.
4. Verify the 200 response reflects the updated tags without changes to other properties.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
