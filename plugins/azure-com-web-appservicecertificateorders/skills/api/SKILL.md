---
name: appservicecertificateorders-api-client
description: "AppServiceCertificateOrders API Client API skill. Use when working with AppServiceCertificateOrders API Client for subscriptions. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# AppServiceCertificateOrders API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration/certificateOrders -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration/validateCertificateRegistrationInformation -- create first validateCertificateRegistrationInformation

## Endpoints

20 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration/certificateOrders | List all certificate orders in a subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration/validateCertificateRegistrationInformation | Validate information for a certificate order. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders | Get certificate orders in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName} | Get a certificate order. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName} | Create or update a certificate purchase order. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName} | Delete an existing certificate order. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName} | Create or update a certificate purchase order. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates | List all certificates associated with a certificate order. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates/{name} | Get the certificate associated with a certificate order. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates/{name} | Creates or updates a certificate and associates with key vault secret. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates/{name} | Delete the certificate associated with a certificate order. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates/{name} | Creates or updates a certificate and associates with key vault secret. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/reissue | Reissue an existing certificate order. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/renew | Renew an existing certificate order. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/resendEmail | Resend certificate email. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/resendRequestEmails | Verify domain ownership for this certificate order. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/retrieveSiteSeal | Verify domain ownership for this certificate order. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/verifyDomainOwnership | Verify domain ownership for this certificate order. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{name}/retrieveCertificateActions | Retrieve the list of certificate actions. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{name}/retrieveEmailHistory | Retrieve email history. |

## Enhanced Skill Content
## Question Mapping

- "What certificate orders exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration/certificateOrders
- "List certificate orders in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders
- "Get details of a specific certificate order?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}
- "How do I create or purchase a new App Service certificate?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}
- "How do I update an existing certificate order without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}
- "How do I delete a certificate order?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}
- "What Key Vault certificates are linked to my certificate order?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates
- "How do I bind a certificate order to a Key Vault certificate?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/certificates/{name}
- "How do I reissue a certificate with a new CSR?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/reissue
- "How do I renew a certificate order before it expires?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/renew
- "How do I verify domain ownership for a certificate order?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/verifyDomainOwnership
- "How do I get the site seal image for my certificate?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/retrieveSiteSeal
- "What actions have been taken on my certificate order?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{certificateOrderName}/retrieveCertificateActions
- "Can I see the email history for a certificate order?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CertificateRegistration/certificateOrders/{name}/retrieveEmailHistory
- "How do I validate certificate registration info before purchasing?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration/validateCertificateRegistrationInformation

## Response Tips

- **List endpoints (GET collection):** Responses use Azure's `value` array wrapper with optional `nextLink` for pagination; always follow `nextLink` until null to get all results.
- **Single resource GET:** Returns the full ARM resource envelope (`id`, `name`, `type`, `location`, `properties`); certificate status and expiry live inside `properties`.
- **PUT/PATCH (create/update):** 200 means updated in place, 201 means newly created; the response body contains the final resource state -- re-read it rather than assuming your input was applied unchanged.
- **POST actions (reissue, renew, resend, verify):** Return 204 No Content on success with an empty body; any non-204 response indicates failure -- check the `error.code` and `error.message` fields.
- **DELETE:** 200 means deleted, 204 means the resource was already absent; both are success states -- do not treat 204 as an error.
- **Errors:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; watch for `AuthorizationFailed`, `ResourceNotFound`, and `Conflict` codes.

## Anomaly Flags

- **Certificate nearing expiry:** When a GET returns a certificate order whose `properties.expirationTime` is within 30 days, proactively warn the user and suggest the renew endpoint.
- **Provisioning state not Succeeded:** If `properties.provisioningState` is `Failed` or stuck in `InProgress` for an extended period, flag it -- domain verification may be pending.
- **Domain verification pending:** If `properties.domainVerificationToken` is present but `properties.status` is not `Issued`, alert the user that domain ownership verification is still required.
- **Rate limiting (429 responses):** Azure ARM enforces subscription-level throttling; if a 429 is returned with a `Retry-After` header, surface the wait time and pause before retrying.
- **Deprecated api-version:** If the response contains `x-ms-deprecation` headers or the error code `ApiVersionDeprecated`, advise upgrading the `api-version` query parameter.
- **Empty certificate bindings:** If listing certificates under an order returns an empty `value` array, flag that the order exists but has no Key Vault binding -- the certificate cannot be used until bound.
- **Unexpected 409 Conflict:** On PUT or DELETE, a 409 typically means a concurrent operation is in progress; surface this and recommend retrying after a short delay.

## Playbook

### 1. Purchase and Provision a New Certificate

1. Call POST `.../validateCertificateRegistrationInformation` with the desired certificate details to confirm the order is valid.
2. Call PUT `.../certificateOrders/{certificateOrderName}` with `certificateDistinguishedName` containing the domain, key size, validity period, and product type.
3. Check the response for `properties.provisioningState` -- if not `Succeeded`, proceed to domain verification.
4. Call POST `.../verifyDomainOwnership` to trigger domain verification (ensure DNS TXT or CNAME records are in place beforehand).
5. Call PUT `.../certificates/{name}` with `keyVaultCertificate` to bind the issued certificate to an Azure Key Vault for storage and deployment.

### 2. Renew an Expiring Certificate

1. Call GET `.../certificateOrders/{certificateOrderName}` to confirm current status and check `properties.expirationTime`.
2. Call POST `.../renew` with `renewCertificateOrderRequest` containing the key size and CSR (if regenerating).
3. Poll GET `.../certificateOrders/{certificateOrderName}` until `properties.status` returns `Issued` with an updated expiry.
4. If the Key Vault binding needs updating, call PATCH `.../certificates/{name}` with the new Key Vault reference.

### 3. Reissue a Compromised Certificate

1. Call POST `.../reissue` with `reissueCertificateOrderRequest` containing a new CSR and the reason for reissue.
2. Call POST `.../verifyDomainOwnership` if domain re-verification is required after reissue.
3. Call POST `.../retrieveCertificateActions` to confirm the reissue action was logged and track progress.
4. Call POST `.../resendEmail` if the verification or approval email was not received.

### 4. Audit Certificate Order Activity

1. Call GET `.../certificateOrders` (subscription-wide) or scoped to a resource group to list all orders.
2. For each order of interest, call POST `.../retrieveCertificateActions` to get the full action history (issue, renew, reissue events).
3. Call POST `.../retrieveEmailHistory` to review all email notifications sent for the order.
4. Cross-reference `properties.status` and `properties.provisioningState` to identify any orders requiring attention.

### 5. Clean Up Unused Certificate Orders

1. Call GET `.../certificateOrders` scoped to the target resource group to list all orders.
2. For each order, call GET `.../certificates` to check if any Key Vault bindings exist.
3. If no bindings exist and the certificate is expired or unused, call DELETE `.../certificateOrders/{certificateOrderName}`.
4. Confirm deletion succeeded (200) or was already absent (204).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
