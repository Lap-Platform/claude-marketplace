---
name: domainregistrationprovider-api-client
description: "DomainRegistrationProvider API Client API skill. Use when working with DomainRegistrationProvider API Client for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# DomainRegistrationProvider API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DomainRegistration/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.DomainRegistration/operations | Implements Csm operations Api to exposes the list of available Csm Apis under the resource provider |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for domain registration?" -> GET /providers/Microsoft.DomainRegistration/operations
- "List all supported actions in the DomainRegistration resource provider" -> GET /providers/Microsoft.DomainRegistration/operations
- "What can I do with Microsoft domain registration on Azure?" -> GET /providers/Microsoft.DomainRegistration/operations
- "Show me the permissions and operations for domain management" -> GET /providers/Microsoft.DomainRegistration/operations
- "Which RBAC operations exist for DomainRegistration?" -> GET /providers/Microsoft.DomainRegistration/operations
- "What API version should I use for domain registration operations?" -> GET /providers/Microsoft.DomainRegistration/operations (check api-version param)
- "Are there any new operations added in the 2018-02-01 API version?" -> GET /providers/Microsoft.DomainRegistration/operations
- "List all provider operations I can assign in role definitions" -> GET /providers/Microsoft.DomainRegistration/operations
- "What read and write actions does the domain registration provider expose?" -> GET /providers/Microsoft.DomainRegistration/operations
- "How do I discover available domain registration capabilities before building automation?" -> GET /providers/Microsoft.DomainRegistration/operations
- "What operations can I audit in Azure Activity Log for domain registration?" -> GET /providers/Microsoft.DomainRegistration/operations
- "Show the operation display names and descriptions for domain registration" -> GET /providers/Microsoft.DomainRegistration/operations

## Response Tips

- **Operations listing**: Response contains an array of operation objects, each with `name` (e.g., `Microsoft.DomainRegistration/domains/read`), `display` (with `provider`, `resource`, `operation`, `description` fields), and `origin`. Check for a `nextLink` property for pagination -- if present, follow it to retrieve additional pages. Always pass `api-version=2018-02-01` as a query parameter or requests will be rejected.

## Anomaly Flags

- **Missing api-version parameter**: The `api-version` query parameter is required on every request. Omitting it returns a 400 error -- surface this immediately if a user forgets it.
- **Authentication failures (401/403)**: OAuth2 bearer token may be expired or lack sufficient scope. Flag when token refresh is needed or when the service principal lacks `Microsoft.DomainRegistration/*/read` permissions.
- **Throttling (429)**: Azure ARM enforces rate limits per subscription. Surface `Retry-After` header value and recommend backing off before retrying.
- **Deprecated API version**: If Azure returns warnings or `x-ms-deprecation` headers, flag that the 2018-02-01 version may be superseded and recommend checking for newer versions.
- **Empty operations list**: If the response returns zero operations, flag that the resource provider may not be registered in the current subscription -- suggest running `az provider register --namespace Microsoft.DomainRegistration`.

## Playbook

### 1. Discover Available Domain Registration Operations

1. Authenticate with Azure AD to obtain an OAuth2 bearer token with ARM scope (`https://management.azure.com/.default`)
2. Call `GET /providers/Microsoft.DomainRegistration/operations?api-version=2018-02-01`
3. Parse the response array -- each entry represents one RBAC-assignable operation
4. If `nextLink` is present in the response, follow it to retrieve remaining pages
5. Filter results by `origin` field (`user`, `system`, or `user,system`) to find operations relevant to your use case

### 2. Build a Custom RBAC Role for Domain Management

1. Call `GET /providers/Microsoft.DomainRegistration/operations?api-version=2018-02-01` to list all available operations
2. Identify the operation `name` values you need (e.g., `Microsoft.DomainRegistration/domains/write`)
3. Use those operation names as `actions` or `dataActions` in an Azure role definition
4. Create the custom role via the Azure RBAC API or CLI

### 3. Audit Domain Registration Activity

1. Call `GET /providers/Microsoft.DomainRegistration/operations?api-version=2018-02-01` to get the full operation catalog
2. Cross-reference operation `name` values against Azure Activity Log entries for your subscription
3. Flag any operations appearing in logs that are not in the expected set for your workflow
4. Use the `display.description` field to generate human-readable audit reports

### 4. Validate Resource Provider Registration

1. Attempt `GET /providers/Microsoft.DomainRegistration/operations?api-version=2018-02-01`
2. If the response is empty or returns a registration error, the provider is not registered
3. Register it with `POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/register?api-version=2018-02-01`
4. Wait for registration to complete, then retry the operations call to confirm availability


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
