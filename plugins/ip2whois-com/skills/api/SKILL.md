---
name: ip2whois-domain-lookup
description: "IP2WHOIS Domain Lookup API skill. Use when working with IP2WHOIS Domain Lookup for root. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# IP2WHOIS Domain Lookup
API version: 1.0

## Auth
ApiKey key in query

## Base URL
https://api.ip2whois.com/v2

## Setup
1. Set your API key in the appropriate header
2. GET / -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Lookup WHOIS information |

## Enhanced Skill Content
## Question Mapping

- "Who owns this domain?" -> GET /
- "What are the WHOIS details for example.com?" -> GET /
- "When does this domain expire?" -> GET /
- "When was this domain registered?" -> GET /
- "Who is the registrar for this domain?" -> GET /
- "What are the nameservers for example.com?" -> GET /
- "Get WHOIS contact info for a domain" -> GET /
- "Is this domain available or already registered?" -> GET /
- "What is the registrant email for example.com?" -> GET /
- "Look up domain age for example.com" -> GET /
- "Get WHOIS data in JSON format" -> GET /?format=json
- "Get WHOIS data in XML format" -> GET /?format=xml
- "Check who registered a suspicious domain" -> GET /
- "Compare registration dates of two domains" -> GET / (call twice)

## Response Tips

- **Domain lookup (GET /)**: Response contains nested contact objects (registrant, admin, tech) -- each may be redacted due to WHOIS privacy. Check `domain_status` for registration state. The `format` param controls output shape (JSON default, XML optional). Empty string fields mean data is unavailable or privacy-protected, not an error.

## Anomaly Flags

- **WHOIS privacy enabled**: Surface when registrant/admin/tech contact fields are all redacted or empty -- inform user that domain uses privacy protection
- **Domain expiring soon**: Flag if `expiry_date` is within 30 days of current date
- **Unusual domain status**: Surface non-standard `domain_status` values (e.g., `clientHold`, `serverHold`, `pendingDelete`)
- **API key errors**: Watch for 401/403 responses indicating invalid or exhausted API key quota
- **Rate limiting**: Flag repeated 429 responses -- suggest spacing requests or upgrading plan
- **Missing fields**: Surface when expected top-level fields are absent, which may indicate the TLD registry does not support full WHOIS

## Playbook

### 1. Basic Domain WHOIS Lookup

1. Call `GET /?key={api_key}&domain=example.com`
2. Parse the response for registration, expiry, and registrar details
3. Present registrant name, organization, and country to the user
4. Note any privacy-redacted fields

### 2. Domain Expiry Check

1. Call `GET /?key={api_key}&domain=example.com`
2. Extract `create_date` and `expiry_date` fields
3. Calculate domain age and days until expiry
4. Flag if expiry is within 90 days as a renewal reminder

### 3. Bulk Domain Investigation

1. Collect the list of domains to investigate
2. Call `GET /?key={api_key}&domain={each_domain}` sequentially (respect rate limits)
3. Compare registrant info, nameservers, and creation dates across results
4. Surface domains sharing the same registrant or registrar as potentially related
5. Flag any domains with privacy-protected WHOIS as requiring alternative investigation

### 4. Suspicious Domain Analysis

1. Call `GET /?key={api_key}&domain={suspicious_domain}`
2. Check `create_date` -- recently registered domains are higher risk
3. Check registrant country and organization for known patterns
4. Review `domain_status` for holds or pending actions
5. Summarize risk indicators: young domain, privacy-protected, unusual registrar

### 5. Domain Ownership Verification

1. Call `GET /?key={api_key}&domain={domain}` to retrieve current WHOIS
2. Compare registrant name and organization against expected owner
3. Verify nameservers match the expected hosting provider
4. If registrant is privacy-protected, note that verification requires contacting the registrar directly


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
