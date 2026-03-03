---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates | Lists a collection of all certificates in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId} | Gets the entity state (Etag) version of the certificate specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId} | Gets the details of the certificate specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId} | Creates or updates the certificate being used for authentication with the backend. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId} | Deletes specific certificate. |

## Enhanced Skill Content
## Question Mapping

- "What certificates are configured on my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates
- "List all certificates filtered by thumbprint?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates (with $filter)
- "Does a specific certificate exist in my APIM instance?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId}
- "Get details for a specific certificate by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId}
- "Upload a new certificate to API Management?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId}
- "Update an existing certificate?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId}
- "Remove a certificate from my APIM service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId}
- "How do I rotate a certificate in API Management?" -> PUT (upload new) then DELETE (remove old)
- "Check if a certificate ID is already taken before uploading?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId}
- "How many certificates do I have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates (count from response)
- "Find certificates expiring soon?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates (with $filter on expiry)
- "Replace a certificate without downtime?" -> HEAD (verify exists) then PUT (overwrite with new cert)
- "Delete a certificate that may or may not exist?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/certificates/{certificateId} (check 200 vs 204)

## Response Tips

- **List (GET collection):** Response is paged; look for `nextLink` to retrieve additional results. The `value` array contains certificate entities with `id`, `name`, and `properties` nested object.
- **HEAD (existence check):** Returns 200 with no body if the certificate exists; expect a 404-family error if not found. Use response headers (`ETag`) for conditional updates.
- **GET (single):** Returns the full certificate entity. The `properties` object holds `subject`, `thumbprint`, `expirationDate`, and `keyVault` details. The `ETag` header is needed for safe updates and deletes.
- **PUT (create/update):** Returns 201 for newly created certificates and 200 for updates to existing ones. Pass `If-Match: *` or a specific ETag in the header to control concurrency.
- **DELETE:** Returns 200 when a certificate was found and removed, 204 when the resource was already absent. Both are success states -- do not treat 204 as an error.

## Anomaly Flags

- **ETag mismatch on PUT/DELETE:** A 412 Precondition Failed means the certificate was modified by another process since you last read it. Surface this as a concurrency conflict and suggest re-fetching before retrying.
- **Approaching certificate expiration:** When listing certificates, proactively flag any with `expirationDate` within 30 days. Warn the user to rotate soon.
- **Unexpected 204 on DELETE:** If the caller expected the certificate to exist but got 204, flag that it was already gone -- possible drift between expected and actual state.
- **Pagination truncation:** If the list response includes `nextLink` but the agent stops after one page, surface that results are incomplete.
- **Throttling (429):** Azure ARM enforces rate limits. If a 429 response appears, surface the `Retry-After` header value and pause before retrying.
- **Deprecated API version:** If response headers include `Sunset` or deprecation warnings, alert the user that `2019-12-01-preview` is a preview version and a stable release may be available.
- **Key Vault reference errors:** If a certificate's `properties.keyVault` block contains provisioning errors, flag that the Key Vault integration is unhealthy.

## Playbook

### 1. Upload a New Certificate

1. Choose a unique `certificateId` (alphanumeric, typically descriptive like `backend-tls-2026`).
2. HEAD the certificate path to confirm the ID is not already in use (expect 404).
3. Build the request body with `properties.data` (base64-encoded PFX) and `properties.password`.
4. PUT to the certificate path with the parameters body.
5. Confirm a 201 response and store the returned `ETag` for future operations.

### 2. Rotate an Expiring Certificate

1. GET the list of certificates and identify any with `expirationDate` within your rotation window.
2. GET the specific certificate to retrieve its current `ETag` and configuration.
3. PUT to the same `certificateId` with the new certificate data, passing `If-Match: {ETag}` to prevent conflicts.
4. Confirm a 200 response (update, not create) and verify the new `thumbprint` and `expirationDate` in the response body.
5. Optionally, if using a new ID instead: PUT the new cert under a new ID, update backend/gateway references, then DELETE the old one.

### 3. Audit All Certificates

1. GET the certificates collection (no filter) to retrieve the first page.
2. If `nextLink` is present, follow it to get subsequent pages. Repeat until no `nextLink` remains.
3. For each certificate, extract `properties.subject`, `properties.thumbprint`, and `properties.expirationDate`.
4. Flag certificates expiring within 30 days and any with Key Vault provisioning errors.
5. Compile results into a summary table for review.

### 4. Safely Delete a Certificate

1. GET the specific certificate to confirm it exists and retrieve its `ETag`.
2. Verify the certificate is not actively referenced by any API backend or gateway configuration (out-of-band check).
3. DELETE the certificate, passing `If-Match: {ETag}` to avoid deleting a concurrently-updated resource.
4. Confirm a 200 response. If 204 is returned, the certificate was already removed.
5. Re-list certificates to verify the deletion is reflected.

### 5. Check Certificate Existence Before Conditional Logic

1. HEAD the certificate path with the target `certificateId`.
2. If 200 is returned, the certificate exists -- read the `ETag` from response headers.
3. If a not-found error is returned, the certificate does not exist -- proceed to create with PUT.
4. Use this pattern to build idempotent scripts that create-if-missing or skip-if-present.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
