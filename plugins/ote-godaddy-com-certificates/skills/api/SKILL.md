---
name: spec
description: "spec API skill. Use when working with spec for certificates, customers. Covers 28 endpoints."
version: 1.0.0
generator: lapsh
---

# spec

## Auth
No authentication required.

## Base URL
https://api.ote-godaddy.com

## Setup
1. No auth setup needed
2. GET /v2/certificates -- verify access
3. POST /v1/certificates -- create first certificates

## Endpoints

28 endpoints across 2 groups. See references/api-spec.lap for full details.

### certificates
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/certificates | Create a pending order for certificate |
| POST | /v1/certificates/validate | Validate a pending order for certificate |
| GET | /v1/certificates/{certificateId} | Retrieve certificate details |
| GET | /v1/certificates/{certificateId}/actions | Retrieve all certificate actions |
| POST | /v1/certificates/{certificateId}/email/{emailId}/resend | Resend an email |
| POST | /v1/certificates/{certificateId}/email/resend/{emailAddress} | Add alternate email address |
| POST | /v1/certificates/{certificateId}/email/{emailId}/resend/{emailAddress} | Resend email to email address |
| GET | /v1/certificates/{certificateId}/email/history | Retrieve email history |
| DELETE | /v1/certificates/{certificateId}/callback | Unregister system callback |
| GET | /v1/certificates/{certificateId}/callback | Retrieve system stateful action callback url |
| PUT | /v1/certificates/{certificateId}/callback | Register of certificate action callback |
| POST | /v1/certificates/{certificateId}/cancel | Cancel a pending certificate |
| GET | /v1/certificates/{certificateId}/download | Download certificate |
| POST | /v1/certificates/{certificateId}/reissue | Reissue active certificate |
| POST | /v1/certificates/{certificateId}/renew | Renew active certificate |
| POST | /v1/certificates/{certificateId}/revoke | Revoke active certificate |
| GET | /v1/certificates/{certificateId}/siteSeal | Get Site seal |
| POST | /v1/certificates/{certificateId}/verifyDomainControl | Check Domain Control |
| GET | /v2/certificates | Search for certificate details by entitlement |
| POST | /v2/certificates | Create a pending order for certificate |
| GET | /v2/certificates/download | Download certificate by entitlement |
| GET | /v2/certificates/subscriptions/search | Get a page of subscriptions by domain |
| GET | /v2/certificates/subscription/{guid} | GET a page of certificates for a specific domain product |

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/customers/{customerId}/certificates | Retrieve customer's certificates |
| GET | /v2/customers/{customerId}/certificates/{certificateId} | Retrieve individual certificate details |
| GET | /v2/customers/{customerId}/certificates/{certificateId}/domainVerifications | Retrieve domain verification status |
| GET | /v2/customers/{customerId}/certificates/{certificateId}/domainVerifications/{domain} | Retrieve detailed information for supplied domain |
| GET | /v2/customers/{customerId}/certificates/acme/externalAccountBinding | Retrieves the external account binding for the specified customer |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a certificate?" -> POST /v1/certificates
- "Create a validate?" -> POST /v1/certificates/validate
- "Get certificate details?" -> GET /v1/certificates/{certificateId}
- "List all actions?" -> GET /v1/certificates/{certificateId}/actions
- "Create a resend?" -> POST /v1/certificates/{certificateId}/email/{emailId}/resend
- "List all history?" -> GET /v1/certificates/{certificateId}/email/history
- "List all callback?" -> GET /v1/certificates/{certificateId}/callback
- "Create a cancel?" -> POST /v1/certificates/{certificateId}/cancel
- "List all download?" -> GET /v1/certificates/{certificateId}/download
- "Create a reissue?" -> POST /v1/certificates/{certificateId}/reissue
- "Create a renew?" -> POST /v1/certificates/{certificateId}/renew
- "Create a revoke?" -> POST /v1/certificates/{certificateId}/revoke
- "List all siteSeal?" -> GET /v1/certificates/{certificateId}/siteSeal
- "Create a verifyDomainControl?" -> POST /v1/certificates/{certificateId}/verifyDomainControl
- "List all certificates?" -> GET /v2/certificates
- "Create a certificate?" -> POST /v2/certificates
- "List all download?" -> GET /v2/certificates/download
- "List all certificates?" -> GET /v2/customers/{customerId}/certificates
- "Get certificate details?" -> GET /v2/customers/{customerId}/certificates/{certificateId}
- "List all domainVerifications?" -> GET /v2/customers/{customerId}/certificates/{certificateId}/domainVerifications
- "Get domainVerification details?" -> GET /v2/customers/{customerId}/certificates/{certificateId}/domainVerifications/{domain}
- "List all externalAccountBinding?" -> GET /v2/customers/{customerId}/certificates/acme/externalAccountBinding
- "List all search?" -> GET /v2/certificates/subscriptions/search
- "Get subscription details?" -> GET /v2/certificates/subscription/{guid}

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
