---
name: twilio-messaging
description: "Twilio - Messaging API skill. Use when working with Twilio - Messaging for Services, a2p, Deactivations. Covers 58 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Messaging
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://messaging.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/a2p/BrandRegistrations -- verify access
3. POST /v1/Services/{ServiceSid}/AlphaSenders -- create first AlphaSenders

## Endpoints

58 endpoints across 5 groups. See references/api-spec.lap for full details.

### Services
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Services/{ServiceSid}/AlphaSenders |  |
| GET | /v1/Services/{ServiceSid}/AlphaSenders |  |
| GET | /v1/Services/{ServiceSid}/AlphaSenders/{Sid} |  |
| DELETE | /v1/Services/{ServiceSid}/AlphaSenders/{Sid} |  |
| GET | /v1/Services/{MessagingServiceSid}/ChannelSenders |  |
| POST | /v1/Services/{MessagingServiceSid}/ChannelSenders |  |
| GET | /v1/Services/{MessagingServiceSid}/ChannelSenders/{Sid} |  |
| DELETE | /v1/Services/{MessagingServiceSid}/ChannelSenders/{Sid} |  |
| POST | /v1/Services/{ServiceSid}/DestinationAlphaSenders |  |
| GET | /v1/Services/{ServiceSid}/DestinationAlphaSenders |  |
| GET | /v1/Services/{ServiceSid}/DestinationAlphaSenders/{Sid} |  |
| DELETE | /v1/Services/{ServiceSid}/DestinationAlphaSenders/{Sid} |  |
| POST | /v1/Services/PreregisteredUsa2p |  |
| POST | /v1/Services/{ServiceSid}/PhoneNumbers |  |
| GET | /v1/Services/{ServiceSid}/PhoneNumbers |  |
| DELETE | /v1/Services/{ServiceSid}/PhoneNumbers/{Sid} |  |
| GET | /v1/Services/{ServiceSid}/PhoneNumbers/{Sid} |  |
| POST | /v1/Services |  |
| GET | /v1/Services |  |
| POST | /v1/Services/{Sid} |  |
| GET | /v1/Services/{Sid} |  |
| DELETE | /v1/Services/{Sid} |  |
| POST | /v1/Services/{ServiceSid}/ShortCodes |  |
| GET | /v1/Services/{ServiceSid}/ShortCodes |  |
| DELETE | /v1/Services/{ServiceSid}/ShortCodes/{Sid} |  |
| GET | /v1/Services/{ServiceSid}/ShortCodes/{Sid} |  |
| POST | /v1/Services/{MessagingServiceSid}/Compliance/Usa2p |  |
| GET | /v1/Services/{MessagingServiceSid}/Compliance/Usa2p |  |
| DELETE | /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/{Sid} |  |
| GET | /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/{Sid} |  |
| POST | /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/{Sid} |  |
| GET | /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/Usecases |  |
| GET | /v1/Services/Usecases |  |

### a2p
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/a2p/BrandRegistrations/{BrandRegistrationSid}/SmsOtp |  |
| GET | /v1/a2p/BrandRegistrations/{Sid} |  |
| POST | /v1/a2p/BrandRegistrations/{Sid} |  |
| GET | /v1/a2p/BrandRegistrations |  |
| POST | /v1/a2p/BrandRegistrations |  |
| POST | /v1/a2p/BrandRegistrations/{BrandSid}/Vettings |  |
| GET | /v1/a2p/BrandRegistrations/{BrandSid}/Vettings |  |
| GET | /v1/a2p/BrandRegistrations/{BrandSid}/Vettings/{BrandVettingSid} |  |

### Deactivations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Deactivations | Fetch a list of all United States numbers that have been deactivated on a specific date. |

### LinkShortening
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/LinkShortening/Domains/{DomainSid}/Certificate |  |
| GET | /v1/LinkShortening/Domains/{DomainSid}/Certificate |  |
| DELETE | /v1/LinkShortening/Domains/{DomainSid}/Certificate |  |
| POST | /v1/LinkShortening/Domains/{DomainSid}/Config |  |
| GET | /v1/LinkShortening/Domains/{DomainSid}/Config |  |
| GET | /v1/LinkShortening/MessagingService/{MessagingServiceSid}/DomainConfig |  |
| GET | /v1/LinkShortening/Domains/{DomainSid}/ValidateDns |  |
| POST | /v1/LinkShortening/Domains/{DomainSid}/MessagingServices/{MessagingServiceSid} |  |
| DELETE | /v1/LinkShortening/Domains/{DomainSid}/MessagingServices/{MessagingServiceSid} |  |
| GET | /v1/LinkShortening/MessagingServices/{MessagingServiceSid}/Domain |  |
| POST | /v1/LinkShortening/Domains/{DomainSid}/RequestManagedCert |  |

### Tollfree
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Tollfree/Verifications/{Sid} | Retrieve a tollfree verification |
| POST | /v1/Tollfree/Verifications/{Sid} | Edit a tollfree verification |
| DELETE | /v1/Tollfree/Verifications/{Sid} | Delete a tollfree verification |
| GET | /v1/Tollfree/Verifications | List tollfree verifications |
| POST | /v1/Tollfree/Verifications | Create a tollfree verification |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new messaging service?" -> POST /v1/Services
- "List all my messaging services" -> GET /v1/Services
- "How do I add a phone number to a messaging service?" -> POST /v1/Services/{ServiceSid}/PhoneNumbers
- "What alpha senders are configured for my service?" -> GET /v1/Services/{ServiceSid}/AlphaSenders
- "How do I register a brand for A2P 10DLC?" -> POST /v1/a2p/BrandRegistrations
- "What is the status of my brand registration?" -> GET /v1/a2p/BrandRegistrations/{Sid}
- "How do I submit a toll-free verification?" -> POST /v1/Tollfree/Verifications
- "Why was my toll-free verification rejected?" -> GET /v1/Tollfree/Verifications/{Sid}
- "How do I set up link shortening for a domain?" -> POST /v1/LinkShortening/Domains/{DomainSid}/Config
- "Is my link shortening domain DNS valid?" -> GET /v1/LinkShortening/Domains/{DomainSid}/ValidateDns
- "How do I register a US A2P campaign for my service?" -> POST /v1/Services/{MessagingServiceSid}/Compliance/Usa2p
- "What A2P use cases are available for my service?" -> GET /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/Usecases
- "How do I request a managed SSL certificate for link shortening?" -> POST /v1/LinkShortening/Domains/{DomainSid}/RequestManagedCert
- "How do I remove a short code from a messaging service?" -> DELETE /v1/Services/{ServiceSid}/ShortCodes/{Sid}
- "Which phone numbers have been deactivated?" -> GET /v1/Deactivations

## Response Tips

- **Services (CRUD):** Responses include `links` map with sub-resource URLs (PhoneNumbers, ShortCodes, AlphaSenders) -- use these for navigation instead of constructing URLs manually.
- **List endpoints:** All paginated responses use a `meta` object with `next_page_url` and `previous_page_url` (nullable). Page through by following `next_page_url` until it is `null`. The `key` field in `meta` tells you which top-level array holds the data (e.g., `"phone_numbers"`, `"services"`, `"alpha_senders"`).
- **Brand Registrations:** `status` is a required string (never null) -- check it directly. `failure_reason` and `errors` are nullable and only populated on failure. `brand_score` is nullable and may not appear until vetting completes.
- **Toll-free Verifications:** The response is large (50+ fields). Focus on `status`, `rejection_reason`, `error_code`, and `edit_allowed` for actionable state. `rejection_reasons` (array) gives granular detail beyond the single `rejection_reason` string.
- **Link Shortening:** `cert_in_validation` is typed as `any` -- it may be a nested object or null depending on certificate state. `is_valid` on DNS validation is boolean; check `reason` string when `false`.
- **Deactivations:** Returns a 307 redirect, not a direct data response -- follow the redirect to get the actual deactivation list.
- **DELETE endpoints:** All return 204 with no body. A non-204 response indicates failure.
- **A2P Campaigns (Usa2p):** `rate_limits` is typed as `any` -- expect a nested object with per-carrier throughput limits when the campaign is approved.

## Anomaly Flags

- **Brand registration `status` stuck in non-terminal state:** If `status` is not `APPROVED` or `FAILED` and `date_updated` is older than 7 days, surface a warning that the registration may need manual follow-up with Twilio support.
- **Toll-free verification `edit_expiration` approaching:** When `edit_allowed` is `true` and `edit_expiration` is within 48 hours, alert the user to make edits before the window closes.
- **Toll-free `error_code` non-null:** Surface immediately with the numeric code -- these map to Twilio-specific rejection reasons that require remediation.
- **Brand `brand_score` below 50:** Low brand scores restrict A2P throughput. Flag when score is returned and is below the threshold.
- **Deactivations 307 redirect:** If the redirect target fails or returns unexpected content, flag it -- this endpoint behaves differently from all others.
- **`cert_in_validation` non-null on link shortening certificates:** Indicates a pending certificate that has not yet been issued. Surface if it persists across multiple checks.
- **Campaign `errors` array non-empty:** A2P campaign registrations with errors need immediate attention even if `campaign_status` appears normal.
- **Vetting `vetting_status` in unexpected state:** If a brand vetting shows a status other than `PENDING`, `IN_PROGRESS`, `APPROVED`, or `FAILED`, flag as potentially stale or corrupted data.

## Playbook

### 1. Set Up a New Messaging Service with Phone Numbers

1. Create the messaging service: `POST /v1/Services` with `friendly_name` and desired settings (sticky_sender, fallback_url, etc.)
2. Note the returned `sid` -- this is your `ServiceSid` for all subsequent calls
3. Add phone numbers: `POST /v1/Services/{ServiceSid}/PhoneNumbers` for each number (pass the phone number SID in the body)
4. Optionally add alpha senders: `POST /v1/Services/{ServiceSid}/AlphaSenders`
5. Optionally add short codes: `POST /v1/Services/{ServiceSid}/ShortCodes`
6. Verify the setup: `GET /v1/Services/{ServiceSid}` and check the `links` map to browse sub-resources

### 2. Complete A2P 10DLC Registration (Brand + Campaign)

1. Register your brand: `POST /v1/a2p/BrandRegistrations` with customer profile and A2P profile bundle SIDs
2. Poll brand status: `GET /v1/a2p/BrandRegistrations/{Sid}` until `status` reaches `APPROVED` (or `FAILED`)
3. If brand score is low, request external vetting: `POST /v1/a2p/BrandRegistrations/{BrandSid}/Vettings`
4. Check available use cases: `GET /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/Usecases?BrandRegistrationSid={BrandSid}`
5. Register the campaign: `POST /v1/Services/{MessagingServiceSid}/Compliance/Usa2p` with brand SID, use case, message samples, and opt-in/out keywords
6. Monitor campaign status: `GET /v1/Services/{MessagingServiceSid}/Compliance/Usa2p/{Sid}` until `campaign_status` is approved

### 3. Set Up Link Shortening with a Custom Domain

1. Associate domain with messaging service: `POST /v1/LinkShortening/Domains/{DomainSid}/MessagingServices/{MessagingServiceSid}`
2. Configure the domain: `POST /v1/LinkShortening/Domains/{DomainSid}/Config` with fallback_url and callback_url
3. Validate DNS records: `GET /v1/LinkShortening/Domains/{DomainSid}/ValidateDns` -- check `is_valid` is `true`
4. If DNS is valid, request a managed certificate: `POST /v1/LinkShortening/Domains/{DomainSid}/RequestManagedCert`
5. Verify certificate issuance: `GET /v1/LinkShortening/Domains/{DomainSid}/Certificate` -- confirm `certificate_sid` is populated and `date_expires` is in the future

### 4. Submit and Monitor Toll-Free Verification

1. Create the verification: `POST /v1/Tollfree/Verifications` with full business details, use case info, message samples, and opt-in evidence (image URLs)
2. Note the returned `sid` for tracking
3. Poll status: `GET /v1/Tollfree/Verifications/{Sid}` -- watch for `status` changes
4. If `status` indicates rejection, check `rejection_reason`, `rejection_reasons` array, and `error_code` for specifics
5. If `edit_allowed` is `true`, update the verification: `POST /v1/Tollfree/Verifications/{Sid}` with corrected fields before `edit_expiration`
6. To withdraw: `DELETE /v1/Tollfree/Verifications/{Sid}`

### 5. Manage Alpha Senders Across Regions (Destination Alpha Senders)

1. List current alpha senders for a service: `GET /v1/Services/{ServiceSid}/AlphaSenders`
2. Add a destination-specific alpha sender: `POST /v1/Services/{ServiceSid}/DestinationAlphaSenders` with the alpha sender name and ISO country code
3. Filter by country: `GET /v1/Services/{ServiceSid}/DestinationAlphaSenders?IsoCountryCode=GB`
4. Verify capabilities: `GET /v1/Services/{ServiceSid}/DestinationAlphaSenders/{Sid}` -- check the `capabilities` array
5. Remove when no longer needed: `DELETE /v1/Services/{ServiceSid}/DestinationAlphaSenders/{Sid}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
