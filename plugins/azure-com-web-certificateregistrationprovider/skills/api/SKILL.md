---
name: certificateregistrationprovider-api-client
description: "CertificateRegistrationProvider API Client API skill. Use when working with CertificateRegistrationProvider API Client for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# CertificateRegistrationProvider API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.CertificateRegistration/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.CertificateRegistration/operations | Implements Csm operations Api to exposes the list of available Csm Apis under the resource provider |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Certificate Registration?" -> GET /providers/Microsoft.CertificateRegistration/operations
- "List all supported actions in the CertificateRegistration resource provider" -> GET /providers/Microsoft.CertificateRegistration/operations
- "What can I do with Azure App Service Certificates?" -> GET /providers/Microsoft.CertificateRegistration/operations
- "Which RBAC permissions exist for certificate registration?" -> GET /providers/Microsoft.CertificateRegistration/operations
- "Show me the available certificate management operations" -> GET /providers/Microsoft.CertificateRegistration/operations
- "What API version should I use for certificate registration?" -> GET /providers/Microsoft.CertificateRegistration/operations (check api-version param)
- "Are there any write operations for certificate registration?" -> GET /providers/Microsoft.CertificateRegistration/operations (filter results for PUT/POST/DELETE)
- "What display names do certificate operations use?" -> GET /providers/Microsoft.CertificateRegistration/operations (inspect display property)
- "Is certificate order management supported?" -> GET /providers/Microsoft.CertificateRegistration/operations (search results for certificateOrders)
- "What read-only operations exist for certificates?" -> GET /providers/Microsoft.CertificateRegistration/operations (filter for read actions)
- "How do I discover certificate provider capabilities before calling other Azure APIs?" -> GET /providers/Microsoft.CertificateRegistration/operations

## Response Tips

- **Operations listing**: Response is a JSON object with a `value` array of operation objects. Each entry contains `name` (resource provider action string like `Microsoft.CertificateRegistration/certificateOrders/read`), `display` (nested object with `provider`, `resource`, `operation`, `description`), and optionally `origin` and `properties`. No pagination -- single-page response for this provider.

## Anomaly Flags

- **api-version mismatch**: If you receive a 400 or `NoRegisteredProviderFound` error, the api-version value may be unsupported. Surface this immediately and suggest `2018-02-01`.
- **Empty operations list**: If `value` is an empty array, the resource provider may not be registered in the subscription. Prompt the user to run `az provider register --namespace Microsoft.CertificateRegistration`.
- **401/403 responses**: OAuth2 token may be expired or the service principal lacks `Microsoft.CertificateRegistration/*/read` permission. Flag and recommend re-authentication.
- **Deprecation headers**: Watch for `Sunset` or `x-ms-deprecation` headers in the response. Surface these proactively since Azure resource providers do sunset API versions.
- **Throttling (429)**: Azure ARM enforces per-subscription rate limits. If `Retry-After` header appears, surface the wait time and back off automatically.

## Playbook

### 1. Discover Available Certificate Operations

1. Authenticate with Azure AD to obtain a Bearer token (OAuth2 scope: `https://management.azure.com/.default`)
2. Call `GET /providers/Microsoft.CertificateRegistration/operations?api-version=2018-02-01`
3. Inspect the `value` array for the full list of supported actions
4. Use `display.operation` and `display.description` to understand what each action does
5. Reference the `name` field when assigning RBAC roles or building further API calls

### 2. Verify Provider Registration Before Use

1. Call `GET /providers/Microsoft.CertificateRegistration/operations?api-version=2018-02-01`
2. If the response returns an empty `value` array or a provider-not-found error, register the provider:
   - `PUT /subscriptions/{subscriptionId}/providers/Microsoft.CertificateRegistration?api-version=2018-02-01`
3. Wait for registration state to become `Registered`
4. Retry the operations call to confirm availability

### 3. Audit RBAC Permissions for Certificate Management

1. Call `GET /providers/Microsoft.CertificateRegistration/operations?api-version=2018-02-01`
2. Extract all `name` values from the operations list (these are the action strings)
3. Group by pattern: `*/read`, `*/write`, `*/delete`, `*/action`
4. Cross-reference with your role assignments to confirm users have only the permissions they need
5. Flag any `*/write` or `*/delete` operations that are accessible but not expected

### 4. Handle API Version Migration

1. Call the operations endpoint with your current `api-version` parameter
2. Check response headers for `x-ms-deprecation` or `Sunset` indicators
3. If deprecation is flagged, test with the latest known version (`2018-02-01` or newer)
4. Compare the operations lists between versions to identify added or removed capabilities
5. Update all client configurations to the supported version


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
