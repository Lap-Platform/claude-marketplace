---
name: topleveldomains-api-client
description: "TopLevelDomains API Client API skill. Use when working with TopLevelDomains API Client for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# TopLevelDomains API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}/listAgreements -- create first listAgreements

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains | Get all top-level domains supported for registration. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name} | Get details of a top-level domain. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}/listAgreements | Gets all legal agreements that user needs to accept before purchasing a domain. |

## Enhanced Skill Content
## Question Mapping

- "What top-level domains are available?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains
- "List all TLDs for my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains
- "Get details about the .com TLD" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}
- "What properties does the .org domain have?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}
- "Is .io available as a top-level domain?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}
- "What are the legal agreements for .com?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}/listAgreements
- "Show me the registration terms for .net" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}/listAgreements
- "What agreements must I accept to register a .dev domain?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}/listAgreements
- "Do I need to agree to privacy terms for .com?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains/{name}/listAgreements
- "Which TLDs support privacy agreements?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains + POST listAgreements per TLD
- "Compare agreement requirements between .com and .org" -> POST listAgreements for each TLD
- "Check if a specific TLD exists before listing its agreements" -> GET /topLevelDomains/{name} then POST listAgreements

## Response Tips

- **TLD listings** (`GET .../topLevelDomains`): Returns a paginated array with `value` and `nextLink`; follow `nextLink` until absent to retrieve all TLDs.
- **TLD details** (`GET .../topLevelDomains/{name}`): Returns a single resource object with `properties` nested inside; domain privacy support and other flags live under `properties`.
- **Agreements** (`POST .../listAgreements`): Returns a paginated list of agreement objects in `value`; each agreement includes `agreementKey`, `title`, `content`, and `url` -- always surface the full list to the user before proceeding with registration.
- **Errors**: 4xx responses return an `error` object with `code` and `message`; a 404 on a TLD name means that TLD is not supported by Azure Domain Registration.

## Anomaly Flags

- **Unknown TLD**: A 404 on `GET .../topLevelDomains/{name}` likely means the TLD is not offered through Azure -- surface this clearly rather than retrying.
- **Empty agreement list**: If `listAgreements` returns zero items, flag this as unusual; most TLDs require at least one agreement for registration.
- **Pagination truncation**: If a `nextLink` is present but subsequent pages return errors, warn that the TLD list may be incomplete.
- **API version mismatch**: If the response contains `error.code: "NoRegisteredProviderFound"` or similar, the `api-version` parameter may be outdated or the `Microsoft.DomainRegistration` resource provider may not be registered on the subscription.
- **Throttling**: Azure ARM returns 429 with a `Retry-After` header -- surface the wait time and retry automatically.
- **Subscription-level blocks**: A 403 may indicate the subscription lacks the App Service domain registration feature; flag this as a permissions or subscription tier issue.

## Playbook

### 1. List All Available Top-Level Domains

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains?api-version=2018-02-01`
2. Collect the `value` array from the response
3. If `nextLink` is present, follow it with a GET request and append results
4. Repeat until no `nextLink` remains
5. Present the full list of TLD names to the user

### 2. Review Agreements Before Domain Registration

1. Call `GET .../topLevelDomains/{name}` to confirm the TLD exists and check its properties
2. Call `POST .../topLevelDomains/{name}/listAgreements` with `agreementOption` specifying whether to include privacy agreements (e.g., `{"includePrivacy": true}`)
3. Parse each agreement object for `title`, `content`, and `url`
4. Present all agreements to the user for review
5. Confirm user acceptance before proceeding with any domain registration workflow

### 3. Compare Agreement Requirements Across TLDs

1. Identify the TLDs to compare (e.g., .com, .org, .net)
2. For each TLD, call `POST .../topLevelDomains/{name}/listAgreements` with identical `agreementOption` settings
3. Collect and deduplicate agreement keys across all responses
4. Present a side-by-side summary showing which agreements apply to which TLDs
5. Highlight any TLD-specific agreements that differ from the others

### 4. Verify Subscription Readiness for Domain Registration

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.DomainRegistration/topLevelDomains?api-version=2018-02-01`
2. If a 403 or provider-not-registered error is returned, advise the user to register the `Microsoft.DomainRegistration` provider on their subscription
3. If successful, confirm the subscription supports domain registration
4. Optionally pick a target TLD and run the agreements playbook to confirm end-to-end access


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
