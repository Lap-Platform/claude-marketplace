---
name: single-sign-on-overview
description: "Single Sign-On Overview API skill. Use when working with Single Sign-On Overview for resources. Covers 29 endpoints."
version: 1.0.0
generator: lapsh
---

# Single Sign-On Overview

## Auth
Bearer bearer

## Base URL
https://api.frontegg.com/team

## Setup
1. Set Authorization header with your Bearer token
2. GET /resources/sso/v1/saml/configurations/vendor-config -- verify access
3. POST /resources/sso/v1/configurations -- create first configurations

## Endpoints

29 endpoints across 1 groups. See references/api-spec.lap for full details.

### resources
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources/sso/v1/saml/configurations/vendor-config | Get vendor's SAML config |
| GET | /resources/sso/v1/saml/configurations/sp-certificate | Get service provider certificate |
| GET | /resources/sso/v1/saml/configurations/sp-metadata | Get service provider metadata |
| POST | /resources/sso/v1/configurations | Create SSO configuration |
| GET | /resources/sso/v1/configurations | Get SSO configurations |
| DELETE | /resources/sso/v1/configurations/{configurationId} | Delete SSO configuration |
| PATCH | /resources/sso/v1/configurations/{configurationId} | Update SSO configuration |
| POST | /resources/sso/v1/configurations/metadata | Create SSO configuration using metadata |
| PUT | /resources/sso/v1/configurations/{configurationId}/metadata | Update SSO configuration using metadata |
| POST | /resources/sso/v1/configurations/{configurationId}/domains | Create SSO domain |
| DELETE | /resources/sso/v1/configurations/{configurationId}/domains/{domainId} | Delete SSO domain |
| PUT | /resources/sso/v1/configurations/{configurationId}/domains/{domainId}/validate/email | Validate SSO domain by email |
| PUT | /resources/sso/v2/configurations/{configurationId}/domains/{domainId}/validate | Validate SSO domain |
| PUT | /resources/sso/v1/configurations/{configurationId}/roles | Set SSO default roles |
| GET | /resources/sso/v1/configurations/{configurationId}/roles | Get SSO default roles |
| POST | /resources/sso/v1/configurations/{configurationId}/groups | Create an SSO group |
| GET | /resources/sso/v1/configurations/{configurationId}/groups | Get SSO group |
| PATCH | /resources/sso/v1/configurations/{configurationId}/groups/{groupId} | Update SSO group |
| DELETE | /resources/sso/v1/configurations/{configurationId}/groups/{groupId} | Delete SSO group |
| POST | /resources/sso/v1/configurations/excluded-emails | Exclude email from SSO |
| GET | /resources/sso/v1/configurations/excluded-emails | Get SSO excluded emails |
| DELETE | /resources/sso/v1/configurations/excluded-emails/{email} | Delete SSO excluded email |
| PUT | /resources/sso/v1/configurations/domains/{domain}/force-validate | Vendor only - Force SSO domain validation |
| GET | /resources/sso/v1/configurations/multiple-sso-per-domain | Get SSO per account (tenant) configuration |
| PUT | /resources/sso/v1/configurations/multiple-sso-per-domain | Create or update SSO per account (tenant) configuration |
| PUT | /resources/sso/v1/configurations/domains | Create or update SSO domains configuration |
| GET | /resources/sso/v1/configurations/domains | Get SSO domains configuration |
| GET | /resources/sso/v1/oidc/configurations | Get OIDC configuration |
| POST | /resources/sso/v1/oidc/configurations | Configure OIDC |

## Enhanced Skill Content
## Question Mapping

- "How do I set up SSO for a tenant?" -> POST /resources/sso/v1/configurations
- "What SSO configurations exist for my tenant?" -> GET /resources/sso/v1/configurations
- "How do I update an existing SSO configuration?" -> PATCH /resources/sso/v1/configurations/{configurationId}
- "How do I delete an SSO configuration?" -> DELETE /resources/sso/v1/configurations/{configurationId}
- "How do I add a domain to an SSO configuration?" -> POST /resources/sso/v1/configurations/{configurationId}/domains
- "How do I validate a domain for SSO?" -> PUT /resources/sso/v2/configurations/{configurationId}/domains/{domainId}/validate
- "How do I validate a domain via email?" -> PUT /resources/sso/v1/configurations/{configurationId}/domains/{domainId}/validate/email
- "How do I assign roles to an SSO configuration?" -> PUT /resources/sso/v1/configurations/{configurationId}/roles
- "What roles are mapped to my SSO configuration?" -> GET /resources/sso/v1/configurations/{configurationId}/roles
- "How do I create a group mapping for SSO?" -> POST /resources/sso/v1/configurations/{configurationId}/groups
- "How do I exclude an email from SSO enforcement?" -> POST /resources/sso/v1/configurations/excluded-emails
- "How do I configure SSO using a metadata XML file?" -> POST /resources/sso/v1/configurations/metadata
- "What is my service provider certificate?" -> GET /resources/sso/v1/saml/configurations/sp-certificate
- "How do I enable multiple SSO providers per domain?" -> PUT /resources/sso/v1/configurations/multiple-sso-per-domain
- "How do I configure OIDC-based SSO?" -> POST /resources/sso/v1/oidc/configurations

## Response Tips

- **SAML metadata/certificate endpoints** (GET sp-certificate, sp-metadata, vendor-config): Return raw XML or PEM content; parse as text, not JSON.
- **Configuration CRUD** (POST/GET/PATCH/DELETE configurations): Responses include the full configuration object with `configurationId` needed for all sub-resource operations.
- **Domain operations**: POST returns the created domain with a `domainId`; validation endpoints return status but may require async DNS or email confirmation before the domain is fully verified.
- **Role and group mappings**: Role PUT is idempotent (replaces entire role set); group POST is additive. Both return the updated mapping list.
- **Excluded emails**: Flat list responses; the DELETE path takes the email directly as a URL segment (URL-encode `@` and dots).
- **Multi-SSO and domain settings**: GET returns current policy flags; PUT returns the updated policy. These are environment-wide, not per-tenant.

## Anomaly Flags

- **Missing `frontegg-tenant-id` header**: Most endpoints require it; omitting it returns ambiguous 401/403 errors. Surface this if the user forgets tenant context.
- **SAML vs OIDC type mismatch**: The POST/PATCH configuration `type` field determines which fields matter. Flag if OIDC fields (`oidcClientId`, `oidcSecret`) are set on a SAML-type config or vice versa.
- **Domain validation pending**: After adding a domain, it is unverified. Proactively remind the user to call the validate endpoint before expecting SSO login to work.
- **Overriding active tenant**: The `overrideActiveTenant` flag can silently redirect users between tenants. Warn when this is enabled.
- **`subAccountAccessLimit` set to 0**: This may unintentionally block all sub-account access. Flag if set to zero or a very low value.
- **Excluded emails accumulation**: Large excluded-email lists can create security blind spots. Surface if the list grows beyond a reasonable threshold.
- **Multiple SSO per domain active with no strategy**: If `active: true` but `unspecifiedTenantStrategy` is empty or missing, users hitting that domain will get undefined behavior.

## Playbook

### 1. Set Up SAML SSO for a Tenant

1. GET /resources/sso/v1/saml/configurations/sp-metadata with `frontegg-tenant-id` to retrieve the SP metadata XML.
2. Provide the SP metadata to the identity provider (IdP) and obtain the IdP's SSO endpoint URL, public certificate, and entity ID.
3. POST /resources/sso/v1/configurations with `type: "saml"`, `ssoEndpoint`, `publicCertificate`, `acsUrl`, `spEntityId`, and `enabled: true`.
4. Note the `configurationId` from the response.
5. POST /resources/sso/v1/configurations/{configurationId}/domains to link the tenant's email domain.
6. PUT /resources/sso/v1/configurations/{configurationId}/domains/{domainId}/validate/email or the v2 validate endpoint to verify domain ownership.
7. PUT /resources/sso/v1/configurations/{configurationId}/roles with the default `roleIds` for SSO users.

### 2. Configure OIDC SSO

1. POST /resources/sso/v1/oidc/configurations with `active: true` and optionally a `redirectUri`.
2. POST /resources/sso/v1/configurations with `type: "oidc"`, `oidcClientId`, `oidcSecret`, and `enabled: true`.
3. Note the `configurationId` and add domains via POST /resources/sso/v1/configurations/{configurationId}/domains.
4. Validate the domain using PUT /resources/sso/v2/configurations/{configurationId}/domains/{domainId}/validate.

### 3. Map IdP Groups to Application Roles

1. GET /resources/sso/v1/configurations to find the target `configurationId`.
2. POST /resources/sso/v1/configurations/{configurationId}/groups with the IdP `group` name and desired `roleIds`.
3. Repeat for each group mapping needed.
4. GET /resources/sso/v1/configurations/{configurationId}/groups to verify all mappings are correct.

### 4. Exclude Specific Users from SSO Enforcement

1. GET /resources/sso/v1/configurations/excluded-emails to review currently excluded addresses.
2. POST /resources/sso/v1/configurations/excluded-emails with the `email` to exclude (e.g., a break-glass admin account).
3. To remove an exclusion later, DELETE /resources/sso/v1/configurations/excluded-emails/{email}.

### 5. Enable Multiple SSO Providers on a Single Domain

1. GET /resources/sso/v1/configurations/multiple-sso-per-domain to check current status.
2. PUT /resources/sso/v1/configurations/multiple-sso-per-domain with `active: true`, `unspecifiedTenantStrategy` (e.g., `"prompt"`), and `useActiveTenant` as needed.
3. Ensure each tenant has its own SSO configuration (POST /resources/sso/v1/configurations) with the shared domain added and validated.
4. PUT /resources/sso/v1/configurations/domains with `skipDomainVerification` or `bypassDomainCrossValidation` if the same domain is intentionally shared across tenants.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
