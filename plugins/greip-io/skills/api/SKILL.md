---
name: greip-api
description: "Greip API skill. Use when working with Greip for geoip, lookup, scoring. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# Greip API
API version: 1.2.0

## Auth
Bearer bearer | ApiKey key in query

## Base URL
https://greipapi.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /geoip -- verify access
3. POST /scoring/payment -- create first payment

## Endpoints

14 endpoints across 5 groups. See references/api-spec.lap for full details.

### geoip
| Method | Path | Description |
|--------|------|-------------|
| GET | /geoip | Retrieve detailed geolocation information for a visitor’s or user’s IP address |

### lookup
| Method | Path | Description |
|--------|------|-------------|
| GET | /lookup/ip | Get the full information of a given IP address |
| GET | /lookup/ip/threats | Retrieve threat intelligence information for a given IP address |
| GET | /lookup/ip/bulk | Get the full information of multiple IP Addresses |
| GET | /lookup/asn | Lookup any AS Number and receive it's details |
| GET | /lookup/bin | Get the complete data associated with a debit/credit card |
| GET | /lookup/iban | Validate International IBANs and obtain essential information |
| GET | /lookup/country | Get the full information of a country |

### scoring
| Method | Path | Description |
|--------|------|-------------|
| POST | /scoring/payment | Prevent financial losses by deploying AI-Powered modules |
| GET | /scoring/email | Validate email addresses and retrieve additional information |
| GET | /scoring/phone | Validate phone numbers and retrieve additional information |
| GET | /scoring/profanity | Detect profanity in a given text |

### ip
| Method | Path | Description |
|--------|------|-------------|
| GET | /ip | Retrieve the IP address of your visitors or users without the need for an account or API key in Greip |

### account
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /account/users/delete | Request to delete your user data from Greip |

## Enhanced Skill Content
## Question Mapping

- "What is my current IP address?" -> GET /ip
- "Where is this IP address located?" -> GET /geoip
- "Look up geolocation details for a specific IP" -> GET /lookup/ip
- "Is this IP address associated with any threats?" -> GET /lookup/ip/threats
- "Check multiple IP addresses at once for geolocation" -> GET /lookup/ip/bulk
- "What network/ASN does this IP belong to?" -> GET /lookup/asn
- "List all ASNs available" -> GET /lookup/asn (with isList param)
- "Validate a credit card BIN number" -> GET /lookup/bin
- "Validate an IBAN bank account number" -> GET /lookup/iban
- "Get information about a country by its code" -> GET /lookup/country
- "Is this email address legitimate or disposable?" -> GET /scoring/email
- "Validate a phone number and check its risk" -> GET /scoring/phone
- "Score a payment transaction for fraud risk" -> POST /scoring/payment
- "Check text for profanity or bad words" -> GET /scoring/profanity
- "Delete a user's data from my Greip account" -> DELETE /account/users/delete

## Response Tips

- **GeoIP/Lookup endpoints**: Responses nest location data under geographic hierarchy (country > region > city); use `params` to limit returned fields and reduce payload size.
- **Threat lookups**: Threat data includes boolean flags and risk scores; absence of a threat category means not detected, not necessarily safe.
- **Bulk IP lookup**: Returns an object keyed by IP address, not an array; iterate over keys to process each result.
- **Scoring endpoints**: Return numeric scores (typically 0-1 range); higher values indicate higher risk or confidence depending on context.
- **Profanity scoring**: Use `listBadWords=yes` to get matched words alongside the score; `scoreOnly=yes` returns only the numeric score.
- **All endpoints**: Errors return 400 (bad request/invalid params) or 500 (server error); check for an error message field in the response body.
- **Format param**: Set `format=JSON` (default) or `format=XML`; `callback` param wraps response in JSONP.

## Anomaly Flags

- **401/403 responses**: Surface immediately -- API key is missing, invalid, or rate-limited; prompt user to verify their key and plan limits.
- **Unexpected 500 errors**: Flag service degradation if multiple consecutive 500s occur across different endpoints.
- **High threat scores on IP lookup**: Proactively warn when threat indicators (VPN, proxy, Tor, bot) are detected on a looked-up IP.
- **Elevated fraud scores on payment scoring**: Alert when payment risk score exceeds a reasonable threshold (e.g., > 0.7).
- **Disposable/invalid email detection**: Surface when email scoring flags a disposable or recently created domain.
- **BIN/IBAN mismatches**: Flag when the BIN country does not match the expected transaction country, or IBAN validation fails.
- **Bulk lookup partial failures**: Warn if some IPs in a bulk request return errors while others succeed.
- **Deprecated `mode` parameter usage**: Note if `mode=test` is being used in what appears to be a production workflow.

## Playbook

### 1. Fraud-Check a Payment Transaction

1. Get the customer's IP geolocation: `GET /lookup/ip?ip={customerIP}`
2. Check the IP for known threats: `GET /lookup/ip/threats?ip={customerIP}`
3. Validate the email address: `GET /scoring/email?email={customerEmail}`
4. Validate the phone number: `GET /scoring/phone?phone={customerPhone}&countryCode={cc}`
5. Validate the card BIN: `GET /lookup/bin?bin={first6digits}`
6. Score the full payment: `POST /scoring/payment` with all collected data in the `data` body
7. Compare the IP country, BIN country, and provided billing country for mismatches

### 2. Verify a New User at Signup

1. Detect the user's IP: `GET /ip`
2. Geolocate and threat-check the IP: `GET /lookup/ip?ip={ip}` then `GET /lookup/ip/threats?ip={ip}`
3. Validate the provided email: `GET /scoring/email?email={email}`
4. Validate the provided phone: `GET /scoring/phone?phone={phone}&countryCode={cc}`
5. Check the username/bio for profanity: `GET /scoring/profanity?text={username}`
6. If any score exceeds threshold, flag the account for manual review

### 3. Bulk IP Intelligence for Log Analysis

1. Collect unique IPs from your access logs (up to the API's bulk limit)
2. Submit them in one call: `GET /lookup/ip/bulk?ips={comma-separated-ips}`
3. Iterate over the keyed results to enrich each log entry with geolocation
4. For any IPs flagged as suspicious, run individual threat checks: `GET /lookup/ip/threats?ip={ip}`
5. Aggregate results by country or ASN using `GET /lookup/asn?asn={asn}` for network context

### 4. Validate Banking Details

1. Validate the IBAN: `GET /lookup/iban?iban={iban}`
2. Cross-reference the IBAN's country with the customer's claimed country via `GET /lookup/country?CountryCode={cc}`
3. If a card is also provided, validate the BIN: `GET /lookup/bin?bin={bin}`
4. Compare the BIN issuer country against the IBAN country to detect geographic inconsistencies

### 5. Content Moderation Pipeline

1. Check user-submitted text for profanity: `GET /scoring/profanity?text={content}&listBadWords=yes`
2. If the score exceeds your threshold, flag or reject the content
3. Optionally re-check with `scoreOnly=yes` for a lightweight pass on edits
4. Log the `userID` parameter to track repeat offenders across submissions


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
