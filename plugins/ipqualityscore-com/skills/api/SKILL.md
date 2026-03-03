---
name: ipqualityscore-api
description: "IPQualityScore API skill. Use when working with IPQualityScore for json. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# IPQualityScore API

## Auth
Basic username:password

## Base URL
https://ipqualityscore.com/api

## Setup
1. Configure auth: Basic username:password
2. GET /json/email/{YOUR_API_KEY_HERE}/{USER_EMAIL_HERE} -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### json
| Method | Path | Description |
|--------|------|-------------|
| GET | /json/email/{YOUR_API_KEY_HERE}/{USER_EMAIL_HERE} | Email Validation |
| GET | /json/phone/{YOUR_API_KEY_HERE}/{USER_PHONE_HERE} | Phone Validation |
| GET | /json/url/{YOUR_API_KEY_HERE}/{URL_HERE} | Malicious URL Scanner |

## Enhanced Skill Content
## Question Mapping

- "Is this email address valid?" -> GET /json/email/{KEY}/{EMAIL}
- "Check if an email is disposable or temporary" -> GET /json/email/{KEY}/{EMAIL}
- "What is the fraud score for this email?" -> GET /json/email/{KEY}/{EMAIL}
- "Has this email been involved in data breaches?" -> GET /json/email/{KEY}/{EMAIL}
- "Is this phone number a VOIP or prepaid number?" -> GET /json/phone/{KEY}/{PHONE}
- "Look up the carrier and line type for a phone number" -> GET /json/phone/{KEY}/{PHONE}
- "Is this phone number associated with fraud or spam?" -> GET /json/phone/{KEY}/{PHONE}
- "What region and timezone does this phone number belong to?" -> GET /json/phone/{KEY}/{PHONE}
- "Is this URL safe to visit?" -> GET /json/url/{KEY}/{URL}
- "Check if a URL contains malware or phishing" -> GET /json/url/{KEY}/{URL}
- "What is the domain age and reputation of this URL?" -> GET /json/url/{KEY}/{URL}
- "Verify a user's email and phone together for KYC" -> GET /json/email/{KEY}/{EMAIL} + GET /json/phone/{KEY}/{PHONE}
- "Is this email a spam trap or honeypot?" -> GET /json/email/{KEY}/{EMAIL}
- "Find email addresses associated with a phone number" -> GET /json/phone/{KEY}/{PHONE}
- "Is this phone number on the Do Not Call list?" -> GET /json/phone/{KEY}/{PHONE}

## Response Tips

- **Email endpoints**: Check `success` first; `fraud_score` (0-100) is the primary risk indicator. `associated_names` and `associated_phone_numbers` have a nested `status` field that indicates data availability before accessing the arrays.
- **Phone endpoints**: `country` param is required for non-international format numbers. Nested `associated_email_addresses` follows the same `{status, emails[]}` pattern as email associations. `active_status` and `line_type` are the key classification fields.
- **URL endpoints**: `risk_score` (0-100) is the composite indicator; check individual boolean flags (`malware`, `phishing`, `spamming`, `suspicious`, `adult`) for specific threat categories. `domain_age` is nested with `human`, `timestamp`, and `iso` representations.
- **All endpoints**: Every response includes `message` and `success` -- always gate on `success: true` before reading other fields. `request_id` is present on all responses for support troubleshooting. Errors return 400 (bad input) or 500 (server-side); the spec lists no 401/403, so invalid API keys surface as `success: false` in the 200 body.

## Anomaly Flags

- **High fraud score**: Surface a warning when `fraud_score` or `risk_score` exceeds 75 on any endpoint -- this indicates high-confidence malicious activity.
- **Disposable or honeypot email**: Flag immediately when `disposable: true` or `honeypot: true` -- these are strong signals of throwaway or trap addresses.
- **Leaked credentials**: Alert when `leaked: true` on email or phone lookups -- the user's data appeared in known breaches.
- **Spam trap detection**: When `spam_trap_score` is "high" or "medium", warn that sending to this address risks blocklisting the sender domain.
- **VOIP/prepaid phone**: Flag `VOIP: true` or `prepaid: true` during identity verification workflows -- these are commonly used for fraud.
- **DNS invalid**: Surface `dns_valid: false` on email or URL checks -- the domain may not exist or is misconfigured.
- **Malware or phishing URL**: Immediately warn on `malware: true` or `phishing: true` -- do not proceed with the URL.
- **Suggested domain correction**: When `suggested_domain` is non-empty on email checks, proactively suggest the correction (likely a typo like `gmial.com`).
- **Timed out lookups**: Flag `timed_out: true` on email checks -- results may be incomplete and a retry is warranted.
- **Do Not Call status**: Alert when `do_not_call: true` on phone lookups -- contacting this number may violate regulations.

## Playbook

### 1. Validate a New User Signup (Email + Phone)

1. Call GET /json/email/{KEY}/{EMAIL} with the user's email address
2. Check `success: true`, then verify `valid: true` and `dns_valid: true`
3. Reject if `disposable: true`, `honeypot: true`, or `fraud_score > 75`
4. If `suggested_domain` is non-empty, prompt the user to correct their email
5. Call GET /json/phone/{KEY}/{PHONE} with `country` parameter set
6. Confirm `valid: true` and `active: true`
7. Flag if `VOIP: true` or `fraud_score > 75` for manual review
8. Cross-reference: check `associated_email_addresses` on the phone result to see if the email matches

### 2. Screen a URL Before Processing

1. Call GET /json/url/{KEY}/{URL} with the target URL (URL-encode it)
2. Check `success: true` before reading threat flags
3. Block immediately if `malware: true` or `phishing: true`
4. Warn the user if `suspicious: true`, `spamming: true`, or `adult: true`
5. Review `risk_score` -- scores above 85 should be treated as unsafe regardless of individual flags
6. Check `domain_age` -- newly registered domains (timestamp within last 30 days) combined with any risk flag warrant extra caution

### 3. Enrich Contact Data for CRM

1. Call GET /json/email/{KEY}/{EMAIL} to get `first_name`, `associated_names`, and `associated_phone_numbers`
2. Check `associated_names.status` -- if "enabled", extract the `names` array for the contact record
3. Check `associated_phone_numbers.status` -- if "enabled", extract phone numbers
4. Call GET /json/phone/{KEY}/{PHONE} for each associated phone to get `carrier`, `line_type`, `city`, `region`, and `timezone`
5. Use `user_activity` from both endpoints to gauge engagement recency
6. Store `domain_velocity` from the email check to understand how heavily the domain is used

### 4. Bulk Email List Cleaning

1. For each email in the list, call GET /json/email/{KEY}/{EMAIL}
2. Remove entries where `valid: false` or `dns_valid: false`
3. Remove entries where `disposable: true` or `honeypot: true`
4. Flag entries where `spam_trap_score` is "medium" or "high" -- sending to these risks blocklisting
5. Flag entries where `frequent_complainer: true` -- these degrade sender reputation
6. Sort remaining entries by `deliverability` field: prioritize "high" over "medium" or "low"
7. Check `catch_all: true` entries separately -- delivery is possible but unverifiable

### 5. Investigate a Suspicious Phone Number

1. Call GET /json/phone/{KEY}/{PHONE} with the appropriate `country` code
2. Check `fraud_score` -- above 75 indicates known fraudulent activity
3. Review `recent_abuse` and `spammer` flags for reported malicious behavior
4. Note `line_type` (Wireless, Landline, VOIP, Toll Free) and `VOIP`/`prepaid` flags
5. Check `active_status` to confirm the number is currently in service
6. Review `associated_email_addresses` to discover connected accounts
7. If emails are found, run each through GET /json/email/{KEY}/{EMAIL} to build a fuller risk profile


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
