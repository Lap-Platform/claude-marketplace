---
name: stytch-api
description: "Stytch API skill. Use when working with Stytch for connected_apps, b2b, users. Covers 184 endpoints."
version: 1.0.0
generator: lapsh
---

# Stytch API
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://api.stytch.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/sessions -- verify access
3. POST /v1/connected_apps/clients/search -- create first search

## Endpoints

184 endpoints across 21 groups. See references/api-spec.lap for full details.

### connected_apps
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/connected_apps/clients/{client_id} | Get |
| PUT | /v1/connected_apps/clients/{client_id} | Update |
| DELETE | /v1/connected_apps/clients/{client_id} | Delete |
| POST | /v1/connected_apps/clients/search | Search |
| POST | /v1/connected_apps/clients | Create |
| POST | /v1/connected_apps/clients/{client_id}/secrets/rotate/start | Rotatestart |
| POST | /v1/connected_apps/clients/{client_id}/secrets/rotate/cancel | Rotatecancel |
| POST | /v1/connected_apps/clients/{client_id}/secrets/rotate | Rotate |

### b2b
| Method | Path | Description |
|--------|------|-------------|
| PUT | /v1/b2b/scim/{organization_id}/connection/{connection_id} | Update |
| DELETE | /v1/b2b/scim/{organization_id}/connection/{connection_id} | Delete |
| GET | /v1/b2b/scim/{organization_id}/connection/{connection_id} | Getgroups |
| POST | /v1/b2b/scim/{organization_id}/connection/{connection_id}/rotate/start | Rotatestart |
| POST | /v1/b2b/scim/{organization_id}/connection/{connection_id}/rotate/complete | Rotatecomplete |
| POST | /v1/b2b/scim/{organization_id}/connection/{connection_id}/rotate/cancel | Rotatecancel |
| POST | /v1/b2b/scim/{organization_id}/connection | Create |
| GET | /v1/b2b/scim/{organization_id}/connection | Get |
| POST | /v1/b2b/organizations | Create |
| GET | /v1/b2b/organizations/{organization_id} | Get |
| PUT | /v1/b2b/organizations/{organization_id} | Update |
| DELETE | /v1/b2b/organizations/{organization_id} | Delete |
| POST | /v1/b2b/organizations/search | Search |
| GET | /v1/b2b/organizations/{organization_id}/metrics | Metrics |
| GET | /v1/b2b/organizations/{organization_id}/connected_apps | Connectedapps |
| GET | /v1/b2b/organizations/{organization_id}/connected_apps/{connected_app_id} | Getconnectedapp |
| DELETE | /v1/b2b/organizations/{organization_id}/external_id | Deleteexternalid |
| PUT | /v1/b2b/organizations/{organization_id}/members/{member_id} | Update |
| DELETE | /v1/b2b/organizations/{organization_id}/members/{member_id} | Delete |
| PUT | /v1/b2b/organizations/{organization_id}/members/{member_id}/reactivate | Reactivate |
| DELETE | /v1/b2b/organizations/{organization_id}/members/mfa_phone_numbers/{member_id} | Deletemfaphonenumber |
| DELETE | /v1/b2b/organizations/{organization_id}/members/{member_id}/totp | Deletetotp |
| POST | /v1/b2b/organizations/members/search | Search |
| DELETE | /v1/b2b/organizations/{organization_id}/members/passwords/{member_password_id} | Deletepassword |
| GET | /v1/b2b/organizations/members/dangerously_get/{member_id} | Dangerouslyget |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/oidc_providers | Oidcproviders |
| POST | /v1/b2b/organizations/{organization_id}/members/{member_id}/unlink_retired_email | Unlinkretiredemail |
| POST | /v1/b2b/organizations/{organization_id}/members/{member_id}/start_email_update | Startemailupdate |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/connected_apps | Getconnectedapps |
| DELETE | /v1/b2b/organizations/{organization_id}/members/{member_id}/external_id | Deleteexternalid |
| POST | /v1/b2b/organizations/{organization_id}/members | Create |
| GET | /v1/b2b/organizations/{organization_id}/member | Get |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/oauth_providers/google | Google |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/oauth_providers/microsoft | Microsoft |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/oauth_providers/slack | Slack |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/oauth_providers/hubspot | Hubspot |
| GET | /v1/b2b/organizations/{organization_id}/members/{member_id}/oauth_providers/github | Github |
| POST | /v1/b2b/organizations/{organization_id}/members/{member_id}/connected_apps/{connected_app_id}/revoke | Revoke |
| POST | /v1/b2b/idp/oauth/authorize/start | Authorizestart |
| POST | /v1/b2b/idp/oauth/authorize | Authorize |
| GET | /v1/b2b/sessions | Get |
| POST | /v1/b2b/sessions/authenticate | Authenticate |
| POST | /v1/b2b/sessions/revoke | Revoke |
| POST | /v1/b2b/sessions/exchange | Exchange |
| POST | /v1/b2b/sessions/exchange_access_token | Exchangeaccesstoken |
| POST | /v1/b2b/sessions/attest | Attest |
| POST | /v1/b2b/sessions/migrate | Migrate |
| GET | /v1/b2b/sessions/jwks/{project_id} | Getjwks |
| POST | /v1/b2b/impersonation/authenticate | Authenticate |
| GET | /v1/b2b/rbac/policy | Policy |
| GET | /v1/b2b/rbac/organizations/{organization_id} | Getorgpolicy |
| PUT | /v1/b2b/rbac/organizations/{organization_id} | Setorgpolicy |
| POST | /v1/b2b/recovery_codes/recover | Recover |
| GET | /v1/b2b/recovery_codes/{organization_id}/{member_id} | Get |
| POST | /v1/b2b/recovery_codes/rotate | Rotate |
| POST | /v1/b2b/totp | Create |
| POST | /v1/b2b/totp/authenticate | Authenticate |
| POST | /v1/b2b/totp/migrate | Migrate |
| POST | /v1/b2b/discovery/intermediate_sessions/exchange | Exchange |
| POST | /v1/b2b/discovery/organizations/create | Create |
| POST | /v1/b2b/discovery/organizations | List |
| POST | /v1/b2b/magic_links/authenticate | Authenticate |
| POST | /v1/b2b/magic_links/email/login_or_signup | Loginorsignup |
| POST | /v1/b2b/magic_links/email/invite | Invite |
| POST | /v1/b2b/magic_links/email/discovery/send | Send |
| POST | /v1/b2b/magic_links/discovery/authenticate | Authenticate |
| POST | /v1/b2b/oauth/authenticate | Authenticate |
| POST | /v1/b2b/oauth/discovery/authenticate | Authenticate |
| POST | /v1/b2b/otps/sms/send | Send |
| POST | /v1/b2b/otps/sms/authenticate | Authenticate |
| POST | /v1/b2b/otps/email/login_or_signup | Loginorsignup |
| POST | /v1/b2b/otps/email/authenticate | Authenticate |
| POST | /v1/b2b/otps/email/discovery/send | Send |
| POST | /v1/b2b/otps/email/discovery/authenticate | Authenticate |
| POST | /v1/b2b/passwords/strength_check | Strengthcheck |
| POST | /v1/b2b/passwords/migrate | Migrate |
| POST | /v1/b2b/passwords/authenticate | Authenticate |
| POST | /v1/b2b/passwords/email/reset/start | Resetstart |
| POST | /v1/b2b/passwords/email/reset | Reset |
| POST | /v1/b2b/passwords/email/require_reset | Requirereset |
| POST | /v1/b2b/passwords/session/reset | Reset |
| POST | /v1/b2b/passwords/existing_password/reset | Reset |
| POST | /v1/b2b/passwords/discovery/authenticate | Authenticate |
| POST | /v1/b2b/passwords/discovery/email/reset/start | Resetstart |
| POST | /v1/b2b/passwords/discovery/email/reset | Reset |
| GET | /v1/b2b/sso/{organization_id} | Getconnections |
| DELETE | /v1/b2b/sso/{organization_id}/connections/{connection_id} | Deleteconnection |
| POST | /v1/b2b/sso/authenticate | Authenticate |
| POST | /v1/b2b/sso/oidc/{organization_id} | Createconnection |
| PUT | /v1/b2b/sso/oidc/{organization_id}/connections/{connection_id} | Updateconnection |
| POST | /v1/b2b/sso/saml/{organization_id} | Createconnection |
| PUT | /v1/b2b/sso/saml/{organization_id}/connections/{connection_id} | Updateconnection |
| PUT | /v1/b2b/sso/saml/{organization_id}/connections/{connection_id}/url | Updatebyurl |
| DELETE | /v1/b2b/sso/saml/{organization_id}/connections/{connection_id}/verification_certificates/{certificate_id} | Deleteverificationcertificate |
| DELETE | /v1/b2b/sso/saml/{organization_id}/connections/{connection_id}/encryption_private_keys/{private_key_id} | Deleteencryptionprivatekey |
| POST | /v1/b2b/sso/external/{organization_id} | Createconnection |
| PUT | /v1/b2b/sso/external/{organization_id}/connections/{connection_id} | Updateconnection |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/users | Create |
| GET | /v1/users/{user_id} | Get |
| PUT | /v1/users/{user_id} | Update |
| DELETE | /v1/users/{user_id} | Delete |
| POST | /v1/users/search | Search |
| PUT | /v1/users/{user_id}/exchange_primary_factor | Exchangeprimaryfactor |
| DELETE | /v1/users/emails/{email_id} | Deleteemail |
| DELETE | /v1/users/phone_numbers/{phone_id} | Deletephonenumber |
| DELETE | /v1/users/webauthn_registrations/{webauthn_registration_id} | Deletewebauthnregistration |
| DELETE | /v1/users/biometric_registrations/{biometric_registration_id} | Deletebiometricregistration |
| DELETE | /v1/users/totps/{totp_id} | Deletetotp |
| DELETE | /v1/users/crypto_wallets/{crypto_wallet_id} | Deletecryptowallet |
| DELETE | /v1/users/passwords/{password_id} | Deletepassword |
| DELETE | /v1/users/oauth/{oauth_user_registration_id} | Deleteoauthregistration |
| DELETE | /v1/users/{user_id}/external_id | Deleteexternalid |
| GET | /v1/users/{user_id}/connected_apps | Connectedapps |
| POST | /v1/users/{user_id}/connected_apps/{connected_app_id}/revoke | Revoke |

### sessions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/sessions | Get |
| POST | /v1/sessions/authenticate | Authenticate |
| POST | /v1/sessions/revoke | Revoke |
| POST | /v1/sessions/migrate | Migrate |
| POST | /v1/sessions/exchange_access_token | Exchangeaccesstoken |
| GET | /v1/sessions/jwks/{project_id} | Getjwks |
| POST | /v1/sessions/attest | Attest |

### rbac
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/rbac/policy | Policy |

### crypto_wallets
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/crypto_wallets/authenticate/start | Authenticatestart |
| POST | /v1/crypto_wallets/authenticate | Authenticate |

### debug
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/debug/whoami | Whoami |

### fingerprint
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/fingerprint/lookup | Lookup |

### rules
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/rules/set | Set |
| POST | /v1/rules/list | List |

### verdict_reasons
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/verdict_reasons/override | Override |
| POST | /v1/verdict_reasons/list | List |

### email
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/email/risk | Risk |

### idp
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/idp/oauth/authorize/start | Authorizestart |
| POST | /v1/idp/oauth/authorize | Authorize |

### impersonation
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/impersonation/authenticate | Authenticate |

### m2m
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/m2m/clients/{client_id} | Get |
| PUT | /v1/m2m/clients/{client_id} | Update |
| DELETE | /v1/m2m/clients/{client_id} | Delete |
| POST | /v1/m2m/clients/search | Search |
| POST | /v1/m2m/clients | Create |
| POST | /v1/m2m/clients/{client_id}/secrets/rotate/start | Rotatestart |
| POST | /v1/m2m/clients/{client_id}/secrets/rotate/cancel | Rotatecancel |
| POST | /v1/m2m/clients/{client_id}/secrets/rotate | Rotate |

### magic_links
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/magic_links/authenticate | Authenticate |
| POST | /v1/magic_links | Create |
| POST | /v1/magic_links/email/send | Send |
| POST | /v1/magic_links/email/login_or_create | Loginorcreate |
| POST | /v1/magic_links/email/invite | Invite |
| POST | /v1/magic_links/email/revoke_invite | Revokeinvite |

### passwords
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/passwords | Create |
| POST | /v1/passwords/authenticate | Authenticate |
| POST | /v1/passwords/strength_check | Strengthcheck |
| POST | /v1/passwords/migrate | Migrate |
| POST | /v1/passwords/email/reset/start | Resetstart |
| POST | /v1/passwords/email/reset | Reset |
| POST | /v1/passwords/existing_password/reset | Reset |
| POST | /v1/passwords/session/reset | Reset |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/oauth/attach | Attach |
| POST | /v1/oauth/authenticate | Authenticate |

### otps
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/otps/authenticate | Authenticate |
| POST | /v1/otps/sms/send | Send |
| POST | /v1/otps/sms/login_or_create | Loginorcreate |
| POST | /v1/otps/whatsapp/send | Send |
| POST | /v1/otps/whatsapp/login_or_create | Loginorcreate |
| POST | /v1/otps/email/send | Send |
| POST | /v1/otps/email/login_or_create | Loginorcreate |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/projects/metrics | Metrics |

### totps
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/totps | Create |
| POST | /v1/totps/authenticate | Authenticate |
| POST | /v1/totps/recovery_codes | Recoverycodes |
| POST | /v1/totps/recover | Recover |

### webauthn
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/webauthn/register/start | Registerstart |
| POST | /v1/webauthn/register | Register |
| POST | /v1/webauthn/authenticate/start | Authenticatestart |
| POST | /v1/webauthn/authenticate | Authenticate |
| PUT | /v1/webauthn/{webauthn_registration_id} | Update |
| GET | /v1/webauthn/credentials/{user_id}/{domain} | Listcredentials |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new user with email and password?" -> POST /v1/passwords
- "How do I authenticate a user session?" -> POST /v1/sessions/authenticate
- "How do I search for B2B organization members?" -> POST /v1/b2b/organizations/members/search
- "How do I send a magic link to a user's email?" -> POST /v1/magic_links/email/send
- "How do I rotate an M2M client secret?" -> POST /v1/m2m/clients/{client_id}/secrets/rotate/start
- "How do I check if an email is risky or disposable?" -> POST /v1/email/risk
- "How do I set up SAML SSO for a B2B organization?" -> POST /v1/b2b/sso/saml/{organization_id}
- "How do I revoke all sessions for a user?" -> POST /v1/sessions/revoke
- "How do I look up a device fingerprint verdict?" -> POST /v1/fingerprint/lookup
- "How do I create a new B2B organization and invite a member?" -> POST /v1/b2b/organizations then POST /v1/b2b/magic_links/email/invite
- "How do I migrate passwords from another auth provider?" -> POST /v1/passwords/migrate
- "How do I verify my API credentials are working?" -> GET /v1/debug/whoami
- "How do I create and configure a connected app (OAuth client)?" -> POST /v1/connected_apps/clients
- "How do I set fraud rules to block a suspicious visitor?" -> POST /v1/rules/set
- "How do I check what RBAC policy is configured?" -> GET /v1/rbac/policy

## Response Tips

- **Search endpoints** (`/search`): Paginated via `cursor`/`limit` in request body; check `results_metadata.next_cursor` -- null or empty means last page. `results_metadata.total` gives the full count.
- **Authentication endpoints**: Always return `session_token` + `session_jwt` pair; B2B variants may return `member_authenticated: false` with `intermediate_session_token` and `mfa_required` when MFA is needed -- do not treat this as a failure.
- **User/Member responses**: Deeply nested -- user object contains arrays of `emails`, `phone_numbers`, `webauthn_registrations`, `providers`, `totps`, `crypto_wallets`; B2B member object nests `scim_registration.scim_attributes` several levels deep.
- **Secret rotation endpoints**: Three-phase pattern (`rotate/start` -> deploy new secret -> `rotate` to complete, or `rotate/cancel` to abort); `start` returns the `next_client_secret` in plaintext, subsequent calls only show `last_four`.
- **Organization responses**: B2B endpoints return full `organization` and `member` objects alongside the primary data -- use these to avoid extra GET calls.
- **Error responses**: All endpoints share the same error codes (400/401/429/500); `request_id` is always present for support debugging.
- **Discovery endpoints**: Return `discovered_organizations` array and `intermediate_session_token` -- these are transient and must be exchanged before expiry.

## Anomaly Flags

- **429 status code**: Rate limit hit. Surface immediately and suggest backing off. All endpoints can return this.
- **`mfa_required` in auth response**: Authentication succeeded but MFA step is pending. Alert the user that `intermediate_session_token` must be used with a TOTP/SMS/recovery code endpoint to complete login.
- **`member_authenticated: false`**: B2B auth did not fully complete -- could indicate MFA required, primary auth required, or org-level policy blocking. Check `mfa_required` and `primary_required` fields.
- **`is_locked: true` on user/member**: Account is locked. Surface `lock_created_at` and `lock_expires_at` to help diagnose.
- **`breached_password: true`** from strength check: Password appears in known breach databases. Flag this as a security concern even if `valid_password` is true.
- **`requires_reset: true`** on password object: User's password has been flagged for mandatory reset -- warn before attempting password auth.
- **`bearer_token_expires_at`** on SCIM connections: If close to expiry, proactively suggest token rotation.
- **`next_client_secret_last_four` is non-empty**: A secret rotation is in progress. Surface this to prevent accidental double-rotation or forgetting to complete.
- **`recovery_codes_remaining`** is low (< 3): After recovery code auth, warn the user to rotate recovery codes.
- **Fingerprint verdict `action: BLOCK`**: Device was flagged as fraudulent. Surface the `reasons` array for investigation.

## Playbook

### 1. B2B Member Onboarding (Create Org, Invite Member, Set Up SSO)

1. Create the organization: `POST /v1/b2b/organizations` with `organization_name` and desired auth policies (`email_allowed_domains`, `auth_methods`, `mfa_policy`).
2. Save the `organization_id` from the response.
3. Create an SSO connection if needed: `POST /v1/b2b/sso/oidc/{organization_id}` or `POST /v1/b2b/sso/saml/{organization_id}` with the identity provider details.
4. Configure the SSO connection: `PUT /v1/b2b/sso/oidc/{organization_id}/connections/{connection_id}` with `client_id`, `client_secret`, and URLs from the IdP.
5. Invite the first member: `POST /v1/b2b/magic_links/email/invite` with `organization_id`, `email_address`, and optional `roles`.
6. After the member accepts, verify their session: `POST /v1/b2b/sessions/authenticate`.

### 2. Password Reset Flow (Consumer)

1. Initiate the reset: `POST /v1/passwords/email/reset/start` with the user's `email` and `reset_password_redirect_url`.
2. User clicks the link in their email and lands on your page with a `token` parameter.
3. Optionally check password strength first: `POST /v1/passwords/strength_check` with the new password.
4. Complete the reset: `POST /v1/passwords/email/reset` with the `token` and new `password`.
5. A `session_token` + `session_jwt` are returned -- the user is now logged in.

### 3. M2M Client Secret Rotation (Zero-Downtime)

1. Start rotation: `POST /v1/m2m/clients/{client_id}/secrets/rotate/start`. Save the `next_client_secret` from the response.
2. Deploy the new secret to all services that use this M2M client. Both old and new secrets are valid during this window.
3. Complete rotation: `POST /v1/m2m/clients/{client_id}/secrets/rotate`. The old secret is now invalidated.
4. If something goes wrong before completing, cancel: `POST /v1/m2m/clients/{client_id}/secrets/rotate/cancel`.

### 4. Fraud Detection and Rule Management

1. Look up a device fingerprint: `POST /v1/fingerprint/lookup` with the `telemetry_id` from your frontend SDK.
2. Inspect the `verdict.action` field (`ALLOW`, `CHALLENGE`, `BLOCK`) and `verdict.reasons`.
3. If you want to override a verdict reason globally: `POST /v1/verdict_reasons/override` with `verdict_reason` and `override_action`.
4. To block a specific visitor or IP range: `POST /v1/rules/set` with `action: BLOCK` and the identifier (`visitor_id`, `cidr_block`, `country_code`, etc.).
5. Review active rules: `POST /v1/rules/list`.

### 5. B2B Multi-Org Session Exchange

1. Authenticate the member in their primary org via any method (password, magic link, SSO, OAuth).
2. Discover available organizations: `POST /v1/b2b/discovery/organizations` with the current `session_token`.
3. Present the `discovered_organizations` list to the user.
4. Exchange into the target org: `POST /v1/b2b/sessions/exchange` with the target `organization_id` and current `session_token`.
5. If `mfa_required` is returned, complete MFA: `POST /v1/b2b/otps/sms/authenticate` or `POST /v1/b2b/totp/authenticate`.
6. Use the new `session_token` + `session_jwt` for subsequent requests scoped to the target organization.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
