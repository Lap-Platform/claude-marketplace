---
name: twilio-verify
description: "Twilio - Verify API skill. Use when working with Twilio - Verify for Services, Forms, SafeList. Covers 57 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Verify
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://verify.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/Services -- verify access
3. POST /v2/Services/{ServiceSid}/AccessTokens -- create first AccessTokens

## Endpoints

57 endpoints across 5 groups. See references/api-spec.lap for full details.

### Services
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/Services/{ServiceSid}/AccessTokens | Create a new enrollment Access Token for the Entity |
| GET | /v2/Services/{ServiceSid}/AccessTokens/{Sid} | Fetch an Access Token for the Entity |
| POST | /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets | Create a new Bucket for a Rate Limit |
| GET | /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets | Retrieve a list of all Buckets for a Rate Limit. |
| POST | /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets/{Sid} | Update a specific Bucket. |
| GET | /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets/{Sid} | Fetch a specific Bucket. |
| DELETE | /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets/{Sid} | Delete a specific Bucket. |
| POST | /v2/Services/{ServiceSid}/Entities/{Identity}/Challenges | Create a new Challenge for the Factor |
| GET | /v2/Services/{ServiceSid}/Entities/{Identity}/Challenges | Retrieve a list of all Challenges for a Factor. |
| GET | /v2/Services/{ServiceSid}/Entities/{Identity}/Challenges/{Sid} | Fetch a specific Challenge. |
| POST | /v2/Services/{ServiceSid}/Entities/{Identity}/Challenges/{Sid} | Verify a specific Challenge. |
| POST | /v2/Services/{ServiceSid}/Entities | Create a new Entity for the Service |
| GET | /v2/Services/{ServiceSid}/Entities | Retrieve a list of all Entities for a Service. |
| DELETE | /v2/Services/{ServiceSid}/Entities/{Identity} | Delete a specific Entity. |
| GET | /v2/Services/{ServiceSid}/Entities/{Identity} | Fetch a specific Entity. |
| DELETE | /v2/Services/{ServiceSid}/Entities/{Identity}/Factors/{Sid} | Delete a specific Factor. |
| GET | /v2/Services/{ServiceSid}/Entities/{Identity}/Factors/{Sid} | Fetch a specific Factor. |
| POST | /v2/Services/{ServiceSid}/Entities/{Identity}/Factors/{Sid} | Update a specific Factor. This endpoint can be used to Verify a Factor if passed an `AuthPayload` param. |
| GET | /v2/Services/{ServiceSid}/Entities/{Identity}/Factors | Retrieve a list of all Factors for an Entity. |
| POST | /v2/Services/{ServiceSid}/Entities/{Identity}/Factors | Create a new Factor for the Entity |
| POST | /v2/Services/{ServiceSid}/MessagingConfigurations | Create a new MessagingConfiguration for a service. |
| GET | /v2/Services/{ServiceSid}/MessagingConfigurations | Retrieve a list of all Messaging Configurations for a Service. |
| POST | /v2/Services/{ServiceSid}/MessagingConfigurations/{Country} | Update a specific MessagingConfiguration |
| GET | /v2/Services/{ServiceSid}/MessagingConfigurations/{Country} | Fetch a specific MessagingConfiguration. |
| DELETE | /v2/Services/{ServiceSid}/MessagingConfigurations/{Country} | Delete a specific MessagingConfiguration. |
| POST | /v2/Services/{ServiceSid}/Entities/{Identity}/Challenges/{ChallengeSid}/Notifications | Create a new Notification for the corresponding Challenge |
| POST | /v2/Services/{ServiceSid}/RateLimits | Create a new Rate Limit for a Service |
| GET | /v2/Services/{ServiceSid}/RateLimits | Retrieve a list of all Rate Limits for a service. |
| POST | /v2/Services/{ServiceSid}/RateLimits/{Sid} | Update a specific Rate Limit. |
| GET | /v2/Services/{ServiceSid}/RateLimits/{Sid} | Fetch a specific Rate Limit. |
| DELETE | /v2/Services/{ServiceSid}/RateLimits/{Sid} | Delete a specific Rate Limit. |
| POST | /v2/Services | Create a new Verification Service. |
| GET | /v2/Services | Retrieve a list of all Verification Services for an account. |
| GET | /v2/Services/{Sid} | Fetch specific Verification Service Instance. |
| DELETE | /v2/Services/{Sid} | Delete a specific Verification Service Instance. |
| POST | /v2/Services/{Sid} | Update a specific Verification Service. |
| POST | /v2/Services/{ServiceSid}/Verifications | Create a new Verification using a Service |
| POST | /v2/Services/{ServiceSid}/Verifications/{Sid} | Update a Verification status |
| GET | /v2/Services/{ServiceSid}/Verifications/{Sid} | Fetch a specific Verification |
| POST | /v2/Services/{ServiceSid}/VerificationCheck | challenge a specific Verification Check. |
| POST | /v2/Services/{ServiceSid}/Webhooks | Create a new Webhook for the Service |
| GET | /v2/Services/{ServiceSid}/Webhooks | Retrieve a list of all Webhooks for a Service. |
| POST | /v2/Services/{ServiceSid}/Webhooks/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Webhooks/{Sid} | Delete a specific Webhook. |
| GET | /v2/Services/{ServiceSid}/Webhooks/{Sid} | Fetch a specific Webhook. |
| POST | /v2/Services/{ServiceSid}/Passkeys/VerifyFactor | Verify a Passkeys Factor |
| POST | /v2/Services/{ServiceSid}/Passkeys/Factors | Create a new Passkeys Factor for the Entity |
| POST | /v2/Services/{ServiceSid}/Passkeys/Challenges | Create a Passkeys Challenge |
| POST | /v2/Services/{ServiceSid}/Passkeys/ApproveChallenge | Approve a Passkeys Challenge |

### Forms
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/Forms/{FormType} | Fetch the forms for a specific Form Type. |

### SafeList
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/SafeList/Numbers | Add a new phone number to SafeList. |
| GET | /v2/SafeList/Numbers/{PhoneNumber} | Check if a phone number exists in SafeList. |
| DELETE | /v2/SafeList/Numbers/{PhoneNumber} | Remove a phone number from SafeList. |

### Attempts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/Attempts | List all the verification attempts for a given Account. |
| GET | /v2/Attempts/{Sid} | Fetch a specific verification attempt. |
| GET | /v2/Attempts/Summary | Get a summary of how many attempts were made and how many were converted. |

### Templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/Templates | List all the available templates for a given Account. |

## Enhanced Skill Content
## Question Mapping

- "How do I send a verification code to a phone number?" -> POST /v2/Services/{ServiceSid}/Verifications
- "How do I check if a verification code is correct?" -> POST /v2/Services/{ServiceSid}/VerificationCheck
- "How do I create a new Verify service?" -> POST /v2/Services
- "How do I list all my Verify services?" -> GET /v2/Services
- "How do I set up rate limiting for a service?" -> POST /v2/Services/{ServiceSid}/RateLimits
- "How do I configure messaging for a specific country?" -> POST /v2/Services/{ServiceSid}/MessagingConfigurations
- "How do I register a passkey factor for a user?" -> POST /v2/Services/{ServiceSid}/Passkeys/Factors
- "How do I check my verification attempt conversion rate?" -> GET /v2/Attempts/Summary
- "How do I add a phone number to the SafeList?" -> POST /v2/SafeList/Numbers
- "How do I set up a webhook for verification events?" -> POST /v2/Services/{ServiceSid}/Webhooks
- "How do I list all factors for a user entity?" -> GET /v2/Services/{ServiceSid}/Entities/{Identity}/Factors
- "How do I create a push notification challenge for MFA?" -> POST /v2/Services/{ServiceSid}/Entities/{Identity}/Challenges
- "How do I look up a specific verification attempt?" -> GET /v2/Attempts/{Sid}
- "How do I delete a Verify service I no longer need?" -> DELETE /v2/Services/{Sid}
- "How do I authenticate a user with a passkey?" -> POST /v2/Services/{ServiceSid}/Passkeys/Challenges then POST /v2/Services/{ServiceSid}/Passkeys/ApproveChallenge

## Response Tips

- **Services/Verifications**: Check `valid` (bool) and `status` ("pending"/"approved"/"canceled") on VerificationCheck responses; `send_code_attempts` is an array tracking each delivery attempt.
- **List endpoints**: All paginated responses use a `meta` object with `next_page_url`/`previous_page_url` (null when at boundary); iterate by following `next_page_url` until null.
- **DELETE endpoints**: Return 204 with no body; treat any non-204 as an error.
- **Attempts/Summary**: `conversion_rate_percentage` is a string (not a number); parse it for calculations.
- **Challenges**: `status` tracks lifecycle ("pending"/"approved"/"denied"/"expired"); `details` and `hidden_details` are opaque `any` types whose shape varies by factor type.
- **Passkeys**: The factor creation response includes `binding` and `options` (WebAuthn ceremony data); pass `options` directly to the browser's `navigator.credentials.create()`.

## Anomaly Flags

- **429 on Verifications**: The `POST /v2/Services/{ServiceSid}/Verifications` endpoint declares `@errors {429}` -- surface rate limit hits immediately and suggest implementing backoff or adjusting RateLimit Buckets.
- **Verification status "canceled"**: If a VerificationCheck returns `valid: false` with status "canceled", the verification was explicitly invalidated -- flag this as it may indicate a user or system-initiated abort.
- **Challenge expiration**: Surface `expiration_date` on challenges proactively; if a challenge is fetched and `expiration_date` is in the past, warn that it cannot be approved.
- **Factor status not "verified"**: After creating a factor, `status` starts as "unverified" -- flag if a factor remains unverified after the expected verification window.
- **Empty `send_code_attempts` array**: If a verification shows no delivery attempts, the message was never dispatched -- surface as a delivery failure signal.
- **Conversion rate drops**: When calling Attempts/Summary, flag if `conversion_rate_percentage` drops below a reasonable threshold (e.g., < 50%) compared to previous checks.

## Playbook

### 1. Send and Verify an OTP Code

1. Create a service if you don't have one: `POST /v2/Services` with a `friendly_name`.
2. Start a verification: `POST /v2/Services/{ServiceSid}/Verifications` with `To` (phone/email) and `Channel` (sms/call/email).
3. Note the returned `sid` and `status` ("pending").
4. Collect the code from the user, then check it: `POST /v2/Services/{ServiceSid}/VerificationCheck` with `To` and `Code`.
5. Confirm `valid: true` and `status: "approved"` in the response.

### 2. Set Up Passkey Authentication (WebAuthn)

1. Register a factor: `POST /v2/Services/{ServiceSid}/Passkeys/Factors` with `friendly_name`, `identity`, and optional `config` for relying party settings.
2. Pass the response's `binding`/`options` to the browser's `navigator.credentials.create()` to complete device registration.
3. Verify the factor: `POST /v2/Services/{ServiceSid}/Passkeys/VerifyFactor` with the attestation response from the browser.
4. To authenticate later, create a challenge: `POST /v2/Services/{ServiceSid}/Passkeys/Challenges` with the user's `identity`.
5. Pass the challenge `options` to `navigator.credentials.get()`, then approve: `POST /v2/Services/{ServiceSid}/Passkeys/ApproveChallenge` with the assertion response.

### 3. Configure Rate Limiting for a Service

1. Create a rate limit: `POST /v2/Services/{ServiceSid}/RateLimits` with a `unique_name` and optional `description`.
2. Add a bucket to define the limit: `POST /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets` with `max` (request count) and `interval` (seconds).
3. Verify the configuration: `GET /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets` to list all buckets.
4. Adjust if needed: `POST /v2/Services/{ServiceSid}/RateLimits/{RateLimitSid}/Buckets/{Sid}` to update max/interval.

### 4. Monitor Verification Delivery Health

1. Pull recent attempts: `GET /v2/Attempts` with `DateCreatedAfter`/`DateCreatedBefore` and optional `Channel` or `Country` filters.
2. Get aggregate stats: `GET /v2/Attempts/Summary` with the same date range.
3. Check `conversion_rate_percentage` -- below 50% warrants investigation.
4. For failed attempts, inspect individual records: `GET /v2/Attempts/{Sid}` and review `conversion_status`, `channel_data`, and `price`.
5. If a specific country is underperforming, check messaging config: `GET /v2/Services/{ServiceSid}/MessagingConfigurations/{Country}` and verify the linked Messaging Service SID.

### 5. Manage the SafeList for Testing

1. Add a test number to the SafeList: `POST /v2/SafeList/Numbers` with the `phone_number`.
2. Verify it was added: `GET /v2/SafeList/Numbers/{PhoneNumber}`.
3. Send verifications to the SafeList number -- these will bypass fraud checks.
4. When testing is complete, remove the number: `DELETE /v2/SafeList/Numbers/{PhoneNumber}` (returns 204).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
