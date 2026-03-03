---
name: domains-api-client
description: "Domains API Client API skill. Use when working with Domains API Client for subscriptions. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Domains API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/domains -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/checkDomainAvailability -- create first checkDomainAvailability

## Endpoints

15 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/checkDomainAvailability | Check if a domain is available for registration. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/domains | Get all domains in a subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/generateSsoRequest | Generate a single sign-on request for the domain management portal. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/listDomainRecommendations | Get domain name recommendations based on keywords. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains | Get all domains in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName} | Get a domain. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName} | Creates or updates a domain. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName} | Delete a domain. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName} | Creates or updates a domain. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers | Lists domain ownership identifiers. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name} | Get ownership identifier for domain |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name} | Creates an ownership identifier for a domain or updates identifier details for an existing identifier |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name} | Delete ownership identifier for domain |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name} | Creates an ownership identifier for a domain or updates identifier details for an existing identifier |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/renew | Renew a domain. |

## Enhanced Skill Content
## Question Mapping

- "Is the domain example.com available for registration?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/checkDomainAvailability
- "List all domains in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/domains
- "What domains are in resource group prod-rg?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains
- "Get details for domain contoso.com" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}
- "Register a new domain" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}
- "Delete domain contoso.com" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}
- "Update contact info for my domain" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}
- "Renew my domain before it expires" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/renew
- "Suggest domain names based on keywords" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/listDomainRecommendations
- "Generate an SSO link for the domain management portal" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/generateSsoRequest
- "List ownership identifiers for my domain" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers
- "Get a specific ownership identifier by name" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name}
- "Set an ownership identifier on my domain" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name}
- "Remove an ownership identifier" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName}/domainOwnershipIdentifiers/{name}
- "Force-delete a domain even if locked" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DomainRegistration/domains/{domainName} (with `forceHardDeleteDomain=true`)

## Response Tips

- **Domain listings** (GET .../domains): Returns a paginated array with `nextLink` for continuation; iterate until `nextLink` is absent.
- **Domain details** (GET .../domains/{name}): Response includes nested `properties` object with registration status, expiration date, contact info, and nameservers.
- **Create/Update** (PUT/PATCH .../domains/{name}): 200 means completed synchronously; 202 means provisioning is in progress -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Delete** (DELETE): 200 means deleted; 204 means the resource was already gone -- both are success states.
- **Renew** (POST .../renew): 200/202 indicate accepted; 204 means no action needed; 400 means the domain is not eligible for renewal (check `error.code`); 500 indicates a registrar-side failure.
- **Availability check** (POST .../checkDomainAvailability): Look at the `available` boolean and `domainType` in the response body.
- **Recommendations** (POST .../listDomainRecommendations): Returns an array; the `parameters` body controls keyword and max count.
- **Ownership identifiers** (GET/PUT/PATCH/DELETE .../domainOwnershipIdentifiers): Lightweight objects; 204 on delete means already removed.

## Anomaly Flags

- **202 on create or update**: The operation is long-running. Surface the async operation URL and remind the user to poll for status before assuming success.
- **Domain expiration approaching**: When a GET domain response shows an `expirationTime` within 30 days, proactively warn and suggest the renew endpoint.
- **400 on renew**: Indicates the domain cannot be renewed in its current state (e.g., redemption period, auto-renew conflict). Surface the full `error.message` for diagnosis.
- **500 on renew**: Registrar-side failure. Flag this as a transient issue worth retrying after a delay, or escalating to Azure support.
- **forceHardDeleteDomain usage**: If the user is deleting with this flag, warn that this bypasses safety locks and the domain may become immediately available for others to register.
- **Missing api-version parameter**: All calls require `api-version=2018-02-01` as a query parameter. If omitted, Azure returns opaque errors. Flag if the user forgets it.
- **Stale domain data after PATCH**: A 202 on update means the response body may not reflect the change yet. Flag this and suggest re-fetching after the async operation completes.

## Playbook

### 1. Check Availability and Register a New Domain

1. Call POST `.../checkDomainAvailability` with `{ "identifier": "example.com" }`.
2. Confirm the response shows `"available": true`.
3. If unsure about the name, call POST `.../listDomainRecommendations` with keywords to explore alternatives.
4. Call PUT `.../resourceGroups/{rg}/providers/Microsoft.DomainRegistration/domains/{domainName}` with the full `domain` object (contact info, consent, DNS settings).
5. If the response is 202, extract the `Azure-AsyncOperation` header and poll until provisioning completes.
6. Verify with GET `.../domains/{domainName}` to confirm registration status.

### 2. Renew an Expiring Domain

1. Call GET `.../domains/{domainName}` and check the `expirationTime` property.
2. If expiration is approaching, call POST `.../domains/{domainName}/renew`.
3. On 200 or 202, the renewal is accepted. On 202, poll the async operation.
4. On 400, read the error message -- the domain may not be eligible (check auto-renew settings or domain state).
5. Confirm by re-fetching the domain details to verify the new expiration date.

### 3. Transfer Domain Management via SSO

1. Call POST `.../generateSsoRequest` to get a single sign-on URL for the domain registrar portal.
2. Provide the returned URL to the domain admin for direct registrar access.
3. This is useful for advanced DNS management, WHOIS updates, or registrar-specific settings not exposed through the Azure API.

### 4. Set Up Domain Ownership Verification

1. Call GET `.../domains/{domainName}/domainOwnershipIdentifiers` to see existing identifiers.
2. Call PUT `.../domains/{domainName}/domainOwnershipIdentifiers/{name}` with the `domainOwnershipIdentifier` object to create or replace an identifier.
3. Use the identifier value in your DNS TXT record or verification mechanism.
4. To clean up, call DELETE `.../domainOwnershipIdentifiers/{name}` -- both 200 and 204 indicate success.

### 5. Audit and Clean Up Domains Across Resource Groups

1. Call GET `.../providers/Microsoft.DomainRegistration/domains` (subscription-level) to list all domains.
2. Page through results using `nextLink` until all domains are collected.
3. For each domain, call GET `.../domains/{domainName}` to inspect status, expiration, and usage.
4. For unused domains, call DELETE `.../domains/{domainName}`. Use `forceHardDeleteDomain=true` only if the domain is locked and you are certain it should be released.
5. Verify cleanup by re-listing domains at the subscription level.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
