---
name: aws-sso-oidc
description: "AWS SSO OIDC API skill. Use when working with AWS SSO OIDC for token, token?aws_iam=t, client. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS SSO OIDC
API version: 2019-06-10

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /token -- create first token

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### token
| Method | Path | Description |
|--------|------|-------------|
| POST | /token | Creates and returns access and refresh tokens for clients that are authenticated using client secrets. The access token can be used to fetch short-term credentials for the assigned AWS accounts or to access application APIs using bearer authentication. |

### token?aws_iam=t
| Method | Path | Description |
|--------|------|-------------|
| POST | /token?aws_iam=t | Creates and returns access and refresh tokens for clients and applications that are authenticated using IAM entities. The access token can be used to fetch short-term credentials for the assigned Amazon Web Services accounts or to access application APIs using bearer authentication. |

### client
| Method | Path | Description |
|--------|------|-------------|
| POST | /client/register | Registers a client with IAM Identity Center. This allows clients to initiate device authorization. The output should be persisted for reuse through many authentication requests. |

### device_authorization
| Method | Path | Description |
|--------|------|-------------|
| POST | /device_authorization | Initiates device authorization by requesting a pair of verification codes from the authorization service. |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate a device with AWS SSO?" -> POST /device_authorization
- "How do I register a new OAuth client?" -> POST /client/register
- "How do I exchange a device code for an access token?" -> POST /token
- "How do I refresh an expired access token?" -> POST /token
- "How do I get a token using IAM credentials?" -> POST /token?aws_iam=t
- "How do I start the SSO login flow for a CLI tool?" -> POST /device_authorization then POST /token
- "How do I exchange an authorization code for tokens?" -> POST /token
- "What scopes can I register my client with?" -> POST /client/register
- "How do I do token exchange (e.g., swap a SAML assertion for an access token)?" -> POST /token?aws_iam=t
- "How do I set up PKCE-based auth with SSO OIDC?" -> POST /token (with codeVerifier)
- "When does my client secret expire?" -> POST /client/register (check clientSecretExpiresAt)
- "How do I get an ID token along with an access token?" -> POST /token
- "How do I register a public client vs a confidential client?" -> POST /client/register (set clientType)
- "How do I use a subject token for cross-account access?" -> POST /token?aws_iam=t (with subjectToken, subjectTokenType)

## Response Tips

- **Token endpoints**: `expiresIn` is seconds until expiry, not a timestamp. Always check for `refreshToken` in the response -- it may be absent depending on grant type. `idToken` is a JWT you can decode for user claims.
- **Client registration**: `clientSecretExpiresAt` is a Unix epoch (int64); value of `0` means the secret never expires. Store `clientId` and `clientSecret` securely -- the secret is only returned once.
- **Device authorization**: `interval` is the minimum polling interval in seconds between token requests. `verificationUriComplete` includes the user code pre-filled and is preferred for UX.
- **Errors**: All endpoints return standard OAuth error bodies (`error`, `error_description`). Watch for `authorization_pending` (keep polling), `slow_down` (increase interval), and `expired_token` (restart flow).

## Anomaly Flags

- **Token expiry imminent**: Surface when `expiresIn` is under 300 seconds and no `refreshToken` is available -- the session will die without re-auth.
- **Client secret expiring soon**: Alert when `clientSecretExpiresAt` is within 7 days of current time -- re-registration will be needed.
- **Slow-down signal**: If a token request returns `slow_down` error, the agent must increase polling interval. Flag this to avoid request storms.
- **Missing refresh token**: When a token response omits `refreshToken`, flag that the session is non-renewable and will require full re-authentication.
- **Expired device code**: If `authorization_pending` persists beyond the `expiresIn` window from device authorization, the flow is dead -- surface this rather than continuing to poll.
- **IAM token exchange with unexpected `issuedTokenType`**: Flag when `issuedTokenType` differs from `requestedTokenType`, as the STS may have downgraded the token.

## Playbook

### 1. Device Authorization Flow (CLI/Headless Login)

1. Register a client: `POST /client/register` with `clientName` and `clientType: "public"`.
2. Store the returned `clientId` and `clientSecret`.
3. Start device auth: `POST /device_authorization` with `clientId`, `clientSecret`, and `startUrl` (your SSO portal URL).
4. Display `verificationUriComplete` (or `verificationUri` + `userCode`) to the user.
5. Poll `POST /token` with `grantType: "urn:ietf:params:oauth:grant-type:device_code"`, `clientId`, `clientSecret`, and `deviceCode` at the returned `interval`.
6. On success, store `accessToken`, `refreshToken`, and note `expiresIn`.

### 2. Token Refresh

1. Detect that `accessToken` is expired or `expiresIn` has elapsed.
2. Call `POST /token` with `grantType: "refresh_token"`, `clientId`, `clientSecret`, and `refreshToken`.
3. Replace stored tokens with the new `accessToken` and `refreshToken` from the response.
4. If refresh fails with `invalid_grant`, restart the full device authorization flow.

### 3. IAM-Based Token Exchange

1. Ensure AWS credentials (SigV4) are configured for the calling identity.
2. Call `POST /token?aws_iam=t` with `clientId`, `grantType: "urn:ietf:params:oauth:grant-type:token-exchange"`, `subjectToken`, and `subjectTokenType`.
3. Optionally set `requestedTokenType` to specify the desired output token type.
4. Verify `issuedTokenType` in the response matches expectations.
5. Use the returned `accessToken` and respect `expiresIn` for caching.

### 4. Authorization Code Exchange (Web App)

1. Register a confidential client: `POST /client/register` with `clientType: "confidential"`, `redirectUris`, and `grantTypes: ["authorization_code"]`.
2. Redirect user to the `authorizationEndpoint` returned in registration.
3. After user approval, receive the `code` at your redirect URI.
4. Exchange it: `POST /token` with `grantType: "authorization_code"`, `clientId`, `clientSecret`, `code`, `redirectUri`, and optionally `codeVerifier` (for PKCE).
5. Store `accessToken`, `refreshToken`, and decode `idToken` for user identity.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
