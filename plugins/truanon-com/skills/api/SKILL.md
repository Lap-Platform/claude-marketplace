---
name: truanon-private-api
description: "TruAnon Private API skill. Use when working with TruAnon Private for api. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# TruAnon Private API

## Auth
Bearer token

## Base URL
https://staging.truanon.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/get_profile -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/get_profile | Get Profile |
| GET | /api/request_token | Get Token |

## Enhanced Skill Content
## Question Mapping

- "Who is this user?" -> GET /api/get_profile
- "Look up a profile by ID on a specific service" -> GET /api/get_profile
- "Get profile information for a user" -> GET /api/get_profile
- "What does TruAnon know about this account?" -> GET /api/get_profile
- "Check the identity behind this service account" -> GET /api/get_profile
- "Fetch verification details for a user on platform X" -> GET /api/get_profile
- "I need an auth token for a user" -> GET /api/request_token
- "Generate a verification token" -> GET /api/request_token
- "Request a token to verify someone's identity on a service" -> GET /api/request_token
- "Start the verification flow for this account" -> GET /api/request_token
- "How do I authenticate a user on a given platform?" -> GET /api/request_token
- "Get a token then check the profile" -> GET /api/request_token, then GET /api/get_profile
- "Verify and retrieve a user's identity" -> GET /api/request_token, then GET /api/get_profile

## Response Tips

- **Profile responses** (`get_profile`): Expect user identity data keyed by the `service` you queried; a missing or empty profile likely means the ID is unregistered on that service.
- **Token responses** (`request_token`): The returned token is short-lived -- use it promptly; check for error fields indicating the ID/service combination is invalid before proceeding.
- **General**: Both endpoints use GET with required query parameters; a 401 means the Bearer token is missing or expired, not that the queried user is invalid.

## Anomaly Flags

- **401 Unauthorized**: Bearer token expired or missing -- surface immediately and prompt for re-authentication.
- **Unknown service value**: If the API returns an error indicating an unrecognized `service`, flag it and suggest valid service names the user may have meant.
- **Empty profile**: If `get_profile` returns successfully but with no meaningful data, proactively note that the ID may not exist on the specified service.
- **Staging environment**: The base URL points to `staging.truanon.com` -- flag this if the user appears to expect production data.
- **Token already issued**: If `request_token` returns a duplicate or already-active token indicator, surface this to avoid redundant verification flows.

## Playbook

### 1. Look Up a User Profile

1. Confirm you have the user's `id` and the `service` name (e.g., "twitter", "github").
2. Call `GET /api/get_profile?id={id}&service={service}` with the Bearer token.
3. Inspect the response for identity and verification fields.
4. Surface any empty or missing data to the user.

### 2. Request a Verification Token

1. Collect the target `id` and `service` from the user.
2. Call `GET /api/request_token?id={id}&service={service}` with the Bearer token.
3. Extract the token from the response.
4. Inform the user of the token and any expiration window.

### 3. Full Identity Verification Flow

1. Call `GET /api/request_token?id={id}&service={service}` to initiate verification.
2. Capture the returned token.
3. Call `GET /api/get_profile?id={id}&service={service}` to retrieve the profile.
4. Cross-reference the token status with the profile data.
5. Report the verification result and any discrepancies to the user.

### 4. Multi-Service Profile Check

1. Identify all services the user wants to check (e.g., "twitter", "github", "linkedin").
2. For each service, call `GET /api/get_profile?id={id}&service={service}`.
3. Aggregate results and highlight which services returned data vs. which returned empty.
4. Flag any services that returned errors for follow-up.

### 5. Troubleshooting a Failed Request

1. Check the HTTP status code: 401 means auth issue, 400 means bad parameters.
2. Verify the Bearer token is set and not expired.
3. Confirm `id` and `service` are both provided and correctly spelled.
4. Note this is the **staging** environment -- confirm the user isn't expecting production data.
5. Retry the request after corrections.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
