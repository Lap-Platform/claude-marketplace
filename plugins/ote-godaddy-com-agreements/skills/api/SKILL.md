---
name: spec
description: "spec API skill. Use when working with spec for agreements. Covers 1 endpoint."
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
2. GET /v1/agreements -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### agreements
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/agreements | Retrieve Legal Agreements for provided agreements keys |

## Enhanced Skill Content
## Question Mapping

- "What legal agreements do I need to accept?" -> GET /v1/agreements
- "Show me the terms of service for domain registration" -> GET /v1/agreements
- "What are the current agreements for this product key?" -> GET /v1/agreements
- "Get agreements for a specific private label reseller" -> GET /v1/agreements
- "What agreements apply in the French market?" -> GET /v1/agreements
- "List all required legal agreements before purchasing a domain" -> GET /v1/agreements
- "What terms must a customer accept for this reseller account?" -> GET /v1/agreements
- "Show agreements for multiple product keys at once" -> GET /v1/agreements
- "Are there different agreements for different markets or locales?" -> GET /v1/agreements
- "What does a customer need to agree to before checkout?" -> GET /v1/agreements
- "Retrieve the agreement content so I can display it to end users" -> GET /v1/agreements
- "Which agreements apply to my white-label storefront?" -> GET /v1/agreements

## Response Tips

- **Agreements**: Response is an array of agreement objects; each contains title, content (may be HTML), and a URL. Always check the `content` field length before rendering -- agreement text can be very large. Pass `keys` as a comma-separated list to retrieve multiple agreements in one call.

## Anomaly Flags

- **429 Too Many Requests**: Rate limit hit. Surface immediately and advise backing off before retrying. Check response headers for retry-after timing.
- **401/403 Auth errors**: API credentials may be expired or the private label ID may lack permissions for the requested agreements. Flag the distinction between authentication failure (401) and authorization denial (403).
- **400 Bad Request on keys**: The `keys` parameter is required. A 400 likely means it was omitted or malformed. Surface the exact error message to help the user correct the request.
- **Empty agreements array**: If the response returns 200 but with no agreements, flag this -- the product key may be invalid or no agreements exist for that market/label combination.
- **X-Market-Id mismatch**: If agreements return in an unexpected language, the market ID may be wrong or defaulting. Surface the effective market used.

## Playbook

### 1. Retrieve Agreements Before a Domain Purchase

1. Identify the product keys for the domain TLD (e.g., `domains`, `dnsPurchase`).
2. Call `GET /v1/agreements?keys=domains,dnsPurchase`.
3. Parse the response array -- each object represents one agreement.
4. Display agreement titles and content to the end user.
5. Record user acceptance before proceeding to purchase.

### 2. Fetch Agreements for a Reseller Storefront

1. Obtain the private label ID for the reseller account.
2. Call `GET /v1/agreements?keys={productKeys}` with header `X-Private-Label-Id: {labelId}`.
3. Verify the returned agreements match the reseller's product catalog.
4. Cache agreement content with a reasonable TTL -- agreements change infrequently.

### 3. Display Localized Agreements for International Markets

1. Determine the target market code (e.g., `en-US`, `fr-FR`, `de-DE`).
2. Call `GET /v1/agreements?keys={productKeys}` with header `X-Market-Id: {marketCode}`.
3. Check that returned content language matches the requested market.
4. Fall back to `en-US` if the desired locale returns empty or errors.

### 4. Validate Agreement Availability Across Products

1. Compile the full list of product keys your application supports.
2. Call `GET /v1/agreements?keys={allKeys}` to retrieve all applicable agreements.
3. Map each returned agreement to its originating product key.
4. Flag any products that return no agreements -- these may not require acceptance or may indicate a misconfigured key.
5. Log results for compliance auditing.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
