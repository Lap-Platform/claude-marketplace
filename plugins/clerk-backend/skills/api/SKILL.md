---
name: clerk-backend-api
description: "Clerk Backend API skill. Use when working with Clerk Backend for public, jwks, clients. Covers 195 endpoints."
version: 1.0.0
generator: lapsh
---

# Clerk Backend API
API version: 2025-11-10

## Auth
Bearer bearer

## Base URL
https://api.clerk.com/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /public/interstitial -- verify access
3. POST /clients/verify -- create first verify

## Endpoints

195 endpoints across 37 groups. See references/api-spec.lap for full details.

### public
| Method | Path | Description |
|--------|------|-------------|
| GET | /public/interstitial | Returns the markup for the interstitial page |

### jwks
| Method | Path | Description |
|--------|------|-------------|
| GET | /jwks | Retrieve the JSON Web Key Set of the instance |

### clients
| Method | Path | Description |
|--------|------|-------------|
| GET | /clients | List all clients |
| POST | /clients/verify | Verify a client |
| GET | /clients/{client_id} | Get a client |

### email_addresses
| Method | Path | Description |
|--------|------|-------------|
| POST | /email_addresses | Create an email address |
| GET | /email_addresses/{email_address_id} | Retrieve an email address |
| DELETE | /email_addresses/{email_address_id} | Delete an email address |
| PATCH | /email_addresses/{email_address_id} | Update an email address |

### phone_numbers
| Method | Path | Description |
|--------|------|-------------|
| POST | /phone_numbers | Create a phone number |
| GET | /phone_numbers/{phone_number_id} | Retrieve a phone number |
| DELETE | /phone_numbers/{phone_number_id} | Delete a phone number |
| PATCH | /phone_numbers/{phone_number_id} | Update a phone number |

### sessions
| Method | Path | Description |
|--------|------|-------------|
| GET | /sessions | List all sessions |
| POST | /sessions | Create a new active session |
| GET | /sessions/{session_id} | Retrieve a session |
| POST | /sessions/{session_id}/refresh | Refresh a session |
| POST | /sessions/{session_id}/revoke | Revoke a session |
| POST | /sessions/{session_id}/tokens | Create a session token |
| POST | /sessions/{session_id}/tokens/{template_name} | Create a session token from a JWT template |

### templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /templates/{template_type} | List all templates |
| GET | /templates/{template_type}/{slug} | Retrieve a template |
| PUT | /templates/{template_type}/{slug} | Update a template for a given type and slug |
| POST | /templates/{template_type}/{slug}/revert | Revert a template |
| POST | /templates/{template_type}/{slug}/preview | Preview changes to a template |
| POST | /templates/{template_type}/{slug}/toggle_delivery | Toggle the delivery by Clerk for a template of a given type and slug |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | List all users |
| POST | /users | Create a new user |
| GET | /users/count | Count users |
| GET | /users/{user_id} | Retrieve a user |
| PATCH | /users/{user_id} | Update a user |
| DELETE | /users/{user_id} | Delete a user |
| POST | /users/{user_id}/ban | Ban a user |
| POST | /users/{user_id}/unban | Unban a user |
| POST | /users/ban | Ban multiple users |
| POST | /users/unban | Unban multiple users |
| POST | /users/{user_id}/lock | Lock a user |
| POST | /users/{user_id}/unlock | Unlock a user |
| POST | /users/{user_id}/profile_image | Set user profile image |
| DELETE | /users/{user_id}/profile_image | Delete user profile image |
| PATCH | /users/{user_id}/metadata | Merge and update a user's metadata |
| GET | /users/{user_id}/billing/subscription | Retrieve a user's billing subscription |
| GET | /users/{user_id}/oauth_access_tokens/{provider} | Retrieve the OAuth access token of a user |
| GET | /users/{user_id}/organization_memberships | Retrieve all memberships for a user |
| GET | /users/{user_id}/organization_invitations | Retrieve all invitations for a user |
| POST | /users/{user_id}/verify_password | Verify the password of a user |
| POST | /users/{user_id}/verify_totp | Verify a TOTP or backup code for a user |
| DELETE | /users/{user_id}/mfa | Disable a user's MFA methods |
| DELETE | /users/{user_id}/backup_code | Disable all user's Backup codes |
| DELETE | /users/{user_id}/passkeys/{passkey_identification_id} | Delete a user passkey |
| DELETE | /users/{user_id}/web3_wallets/{web3_wallet_identification_id} | Delete a user web3 wallet |
| DELETE | /users/{user_id}/totp | Delete all the user's TOTPs |
| DELETE | /users/{user_id}/external_accounts/{external_account_id} | Delete External Account |
| POST | /users/{user_id}/password/set_compromised | Set a user's password as compromised |
| POST | /users/{user_id}/password/unset_compromised | Unset a user's password as compromised |

### invitations
| Method | Path | Description |
|--------|------|-------------|
| POST | /invitations | Create an invitation |
| GET | /invitations | List all invitations |
| POST | /invitations/bulk | Create multiple invitations |
| POST | /invitations/{invitation_id}/revoke | Revokes an invitation |

### organization_invitations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization_invitations | Get a list of organization invitations for the current instance |

### allowlist_identifiers
| Method | Path | Description |
|--------|------|-------------|
| GET | /allowlist_identifiers | List all identifiers on the allow-list |
| POST | /allowlist_identifiers | Add identifier to the allow-list |
| DELETE | /allowlist_identifiers/{identifier_id} | Delete identifier from allow-list |

### blocklist_identifiers
| Method | Path | Description |
|--------|------|-------------|
| GET | /blocklist_identifiers | List all identifiers on the block-list |
| POST | /blocklist_identifiers | Add identifier to the block-list |
| DELETE | /blocklist_identifiers/{identifier_id} | Delete identifier from block-list |

### beta_features
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /beta_features/instance_settings | Update instance settings |
| PUT | /beta_features/domain | Update production instance domain |

### actor_tokens
| Method | Path | Description |
|--------|------|-------------|
| POST | /actor_tokens | Create actor token |
| POST | /actor_tokens/{actor_token_id}/revoke | Revoke actor token |

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /domains | List all instance domains |
| POST | /domains | Add a domain |
| DELETE | /domains/{domain_id} | Delete a satellite domain |
| PATCH | /domains/{domain_id} | Update a domain |

### instance
| Method | Path | Description |
|--------|------|-------------|
| GET | /instance | Fetch the current instance |
| PATCH | /instance | Update instance settings |
| PATCH | /instance/restrictions | Update instance restrictions |
| GET | /instance/protect | Get instance protect settings |
| PATCH | /instance/protect | Update instance protect settings |
| POST | /instance/change_domain | Update production instance domain |
| PATCH | /instance/organization_settings | Update instance organization settings |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhooks/svix | Create a Svix app |
| DELETE | /webhooks/svix | Delete a Svix app |
| POST | /webhooks/svix_url | Create a Svix Dashboard URL |

### jwt_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /jwt_templates | List all templates |
| POST | /jwt_templates | Create a JWT template |
| GET | /jwt_templates/{template_id} | Retrieve a template |
| PATCH | /jwt_templates/{template_id} | Update a JWT template |
| DELETE | /jwt_templates/{template_id} | Delete a Template |

### machines
| Method | Path | Description |
|--------|------|-------------|
| GET | /machines | Get a list of machines for an instance |
| POST | /machines | Create a machine |
| GET | /machines/{machine_id} | Retrieve a machine |
| PATCH | /machines/{machine_id} | Update a machine |
| DELETE | /machines/{machine_id} | Delete a machine |
| GET | /machines/{machine_id}/secret_key | Retrieve a machine secret key |
| POST | /machines/{machine_id}/secret_key/rotate | Rotate a machine's secret key |
| POST | /machines/{machine_id}/scopes | Create a machine scope |
| DELETE | /machines/{machine_id}/scopes/{other_machine_id} | Delete a machine scope |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations | Get a list of organizations for an instance |
| POST | /organizations | Create an organization |
| GET | /organizations/{organization_id} | Retrieve an organization by ID or slug |
| PATCH | /organizations/{organization_id} | Update an organization |
| DELETE | /organizations/{organization_id} | Delete an organization |
| PATCH | /organizations/{organization_id}/metadata | Merge and update metadata for an organization |
| PUT | /organizations/{organization_id}/logo | Upload a logo for the organization |
| DELETE | /organizations/{organization_id}/logo | Delete the organization's logo. |
| GET | /organizations/{organization_id}/billing/subscription | Retrieve an organization's billing subscription |
| POST | /organizations/{organization_id}/invitations | Create and send an organization invitation |
| GET | /organizations/{organization_id}/invitations | Get a list of organization invitations |
| POST | /organizations/{organization_id}/invitations/bulk | Bulk create and send organization invitations |
| GET | /organizations/{organization_id}/invitations/pending | Get a list of pending organization invitations |
| GET | /organizations/{organization_id}/invitations/{invitation_id} | Retrieve an organization invitation by ID |
| POST | /organizations/{organization_id}/invitations/{invitation_id}/revoke | Revoke a pending organization invitation |
| POST | /organizations/{organization_id}/memberships | Create a new organization membership |
| GET | /organizations/{organization_id}/memberships | Get a list of all members of an organization |
| PATCH | /organizations/{organization_id}/memberships/{user_id} | Update an organization membership |
| DELETE | /organizations/{organization_id}/memberships/{user_id} | Remove a member from an organization |
| PATCH | /organizations/{organization_id}/memberships/{user_id}/metadata | Merge and update organization membership metadata |
| POST | /organizations/{organization_id}/domains | Create a new organization domain. |
| GET | /organizations/{organization_id}/domains | Get a list of all domains of an organization. |
| PATCH | /organizations/{organization_id}/domains/{domain_id} | Update an organization domain. |
| DELETE | /organizations/{organization_id}/domains/{domain_id} | Remove a domain from an organization. |

### organization_roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization_roles | Get a list of organization roles |
| POST | /organization_roles | Create an organization role |
| GET | /organization_roles/{organization_role_id} | Retrieve an organization role |
| PATCH | /organization_roles/{organization_role_id} | Update an organization role |
| DELETE | /organization_roles/{organization_role_id} | Delete an organization role |
| POST | /organization_roles/{organization_role_id}/permissions/{permission_id} | Assign a permission to an organization role |
| DELETE | /organization_roles/{organization_role_id}/permissions/{permission_id} | Remove a permission from an organization role |

### organization_domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization_domains | List all organization domains |

### proxy_checks
| Method | Path | Description |
|--------|------|-------------|
| POST | /proxy_checks | Verify the proxy configuration for your domain |

### redirect_urls
| Method | Path | Description |
|--------|------|-------------|
| GET | /redirect_urls | List all redirect URLs |
| POST | /redirect_urls | Create a redirect URL |
| GET | /redirect_urls/{id} | Retrieve a redirect URL |
| DELETE | /redirect_urls/{id} | Delete a redirect URL |

### sign_in_tokens
| Method | Path | Description |
|--------|------|-------------|
| POST | /sign_in_tokens | Create sign-in token |
| POST | /sign_in_tokens/{sign_in_token_id}/revoke | Revoke the given sign-in token |

### sign_ups
| Method | Path | Description |
|--------|------|-------------|
| GET | /sign_ups/{id} | Retrieve a sign-up by ID |
| PATCH | /sign_ups/{id} | Update a sign-up |

### oauth_applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth_applications | Get a list of OAuth applications for an instance |
| POST | /oauth_applications | Create an OAuth application |
| GET | /oauth_applications/{oauth_application_id} | Retrieve an OAuth application by ID |
| PATCH | /oauth_applications/{oauth_application_id} | Update an OAuth application |
| DELETE | /oauth_applications/{oauth_application_id} | Delete an OAuth application |
| POST | /oauth_applications/{oauth_application_id}/rotate_secret | Rotate the client secret of the given OAuth application |
| POST | /oauth_applications/access_tokens/verify | Verify an OAuth Access Token |

### saml_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /saml_connections | Get a list of SAML Connections for an instance |
| POST | /saml_connections | Create a SAML Connection |
| GET | /saml_connections/{saml_connection_id} | Retrieve a SAML Connection by ID |
| PATCH | /saml_connections/{saml_connection_id} | Update a SAML Connection |
| DELETE | /saml_connections/{saml_connection_id} | Delete a SAML Connection |

### testing_tokens
| Method | Path | Description |
|--------|------|-------------|
| POST | /testing_tokens | Retrieve a new testing token |

### agents
| Method | Path | Description |
|--------|------|-------------|
| POST | /agents/tasks | Create agent task |
| POST | /agents/tasks/{agent_task_id}/revoke | Revoke agent task |

### organization_memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization_memberships | Get a list of all organization memberships within an instance. |

### waitlist_entries
| Method | Path | Description |
|--------|------|-------------|
| GET | /waitlist_entries | List all waitlist entries |
| POST | /waitlist_entries | Create a waitlist entry |
| POST | /waitlist_entries/bulk | Create multiple waitlist entries |
| DELETE | /waitlist_entries/{waitlist_entry_id} | Delete a pending waitlist entry |
| POST | /waitlist_entries/{waitlist_entry_id}/invite | Invite a waitlist entry |
| POST | /waitlist_entries/{waitlist_entry_id}/reject | Reject a waitlist entry |

### billing
| Method | Path | Description |
|--------|------|-------------|
| GET | /billing/plans | List all billing plans |
| GET | /billing/prices | List all billing prices |
| POST | /billing/prices | Create a custom billing price |
| GET | /billing/subscription_items | List all subscription items |
| DELETE | /billing/subscription_items/{subscription_item_id} | Cancel a subscription item |
| POST | /billing/subscription_items/{subscription_item_id}/extend_free_trial | Extend free trial for a subscription item |
| POST | /billing/subscription_items/{subscription_item_id}/price_transition | Create a price transition for a subscription item |
| GET | /billing/statements | List all billing statements |
| GET | /billing/statements/{statementID} | Retrieve a billing statement |
| GET | /billing/statements/{statementID}/payment_attempts | List payment attempts for a billing statement |

### organization_permissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization_permissions | Get a list of all organization permissions |
| POST | /organization_permissions | Create a new organization permission |
| GET | /organization_permissions/{permission_id} | Get an organization permission |
| PATCH | /organization_permissions/{permission_id} | Update an organization permission |
| DELETE | /organization_permissions/{permission_id} | Delete an organization permission |

### role_sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /role_sets | Get a list of role sets |
| POST | /role_sets | Create a role set |
| GET | /role_sets/{role_set_key_or_id} | Retrieve a role set |
| PATCH | /role_sets/{role_set_key_or_id} | Update a role set |
| POST | /role_sets/{role_set_key_or_id}/replace | Replace a role set |
| POST | /role_sets/{role_set_key_or_id}/roles | Add roles to a role set |
| POST | /role_sets/{role_set_key_or_id}/roles/replace | Replace a role in a role set |

### api_keys
| Method | Path | Description |
|--------|------|-------------|
| POST | /api_keys | Create an API Key |
| GET | /api_keys | Get API Keys |
| GET | /api_keys/{apiKeyID} | Get an API Key by ID |
| PATCH | /api_keys/{apiKeyID} | Update an API Key |
| DELETE | /api_keys/{apiKeyID} | Delete an API Key |
| GET | /api_keys/{apiKeyID}/secret | Get an API Key Secret |
| POST | /api_keys/{apiKeyID}/revoke | Revoke an API Key |
| POST | /api_keys/verify | Verify an API Key |

### m2m_tokens
| Method | Path | Description |
|--------|------|-------------|
| POST | /m2m_tokens | Create a M2M Token |
| GET | /m2m_tokens | Get M2M Tokens |
| POST | /m2m_tokens/{m2m_token_id}/revoke | Revoke a M2M Token |
| POST | /m2m_tokens/verify | Verify a M2M Token |

## Enhanced Skill Content
## Question Mapping

- "How do I look up a user by email address?" -> GET /users (with `email_address` filter)
- "How can I ban a user from my application?" -> POST /users/{user_id}/ban
- "How do I create a new organization and invite members?" -> POST /organizations, then POST /organizations/{organization_id}/invitations
- "How do I verify a client session token?" -> POST /clients/verify
- "How can I revoke all sessions for a user?" -> GET /sessions (with `user_id` filter), then POST /sessions/{session_id}/revoke for each
- "How do I set up a SAML SSO connection with Okta?" -> POST /saml_connections (with `provider: saml_okta`)
- "How do I check if a user's password has been compromised?" -> POST /users/{user_id}/password/set_compromised
- "How do I create a JWT template for custom claims?" -> POST /jwt_templates
- "How can I add a user to an allowlist?" -> POST /allowlist_identifiers
- "How do I manage billing subscriptions for an organization?" -> GET /organizations/{organization_id}/billing/subscription
- "How do I rotate an OAuth application's client secret?" -> POST /oauth_applications/{oauth_application_id}/rotate_secret
- "How can I create a sign-in token for passwordless login?" -> POST /sign_in_tokens
- "How do I create a machine-to-machine credential?" -> POST /machines, then GET /machines/{machine_id}/secret_key
- "How do I change a member's role in an organization?" -> PATCH /organizations/{organization_id}/memberships/{user_id}
- "How do I issue an M2M token for service authentication?" -> POST /m2m_tokens

## Response Tips

- **Users/Organizations/Members**: Responses embed nested maps for `email_addresses`, `phone_numbers`, `external_accounts`, `organization_memberships`, and `public_user_data` -- always traverse these arrays rather than expecting flat fields.
- **Paginated lists** (users, sessions, invitations, orgs, billing): Use `limit` (default 10) and `offset` for paging; look for `total_count` in the response to calculate remaining pages. Some endpoints return `{data: [], total_count: N}`, others return a bare array.
- **Delete responses**: All deletions return a uniform `{object, id, slug, deleted, external_id}` shape -- check `deleted: true` to confirm success.
- **Timestamps**: All `created_at`, `updated_at`, `expire_at`, `abandon_at` fields are Unix epoch integers (int64 milliseconds) -- not ISO strings.
- **Billing/Subscriptions**: Money amounts are nested as `{amount, amount_formatted, currency, currency_symbol}` maps -- use `amount_formatted` for display, raw `amount` for calculations (in smallest currency unit).
- **Error responses**: Status 422 indicates validation failures (bad input shape), 402 means a paid feature is required, 403 means insufficient permissions, 409 signals a conflict (duplicate resource).

## Anomaly Flags

- **402 Payment Required**: Surface immediately when any endpoint returns 402 -- the instance lacks the required plan tier for the feature (allowlists, blocklists, SAML, actor tokens, JWT templates, domains).
- **409 Conflict**: Flag when creating email addresses, machine scopes, or API keys -- indicates a duplicate resource that the user likely needs to resolve before retrying.
- **User locked/banned state**: After fetching a user, proactively flag if `banned: true`, `locked: true`, or `lockout_expires_in_seconds` is present -- these affect the user's ability to authenticate.
- **Session status anomalies**: When listing sessions, surface any with status `abandoned`, `expired`, or `replaced` alongside `active` ones -- may indicate session hijacking or token reuse.
- **MFA disabled unexpectedly**: If `two_factor_enabled` was true and a subsequent read shows it as false, flag this as a potential security event.
- **Compromised passwords**: When `password_last_updated_at` is null or very old on a password-enabled account, flag as a credential hygiene risk.
- **Template flagged as suspicious**: The `flagged_as_suspicious` field on email/SMS templates should be surfaced immediately -- it means Clerk has flagged content for review.
- **Missing elevated permissions**: When `missing_member_with_elevated_permissions` is true on an organization, flag it -- the org may lack an admin.
- **Token/key expiration**: For API keys, M2M tokens, sign-in tokens, and actor tokens, proactively check `expiration`/`expires_at` and warn if expiring within 24 hours.

## Playbook

### 1. Onboard a New User with Organization

1. `POST /users` with `email_address`, `first_name`, `last_name`, and any `public_metadata`
2. Note the returned `id` (user_id)
3. `POST /organizations` with `name` and `created_by` set to the user_id
4. Confirm the user is automatically an admin via `GET /organizations/{org_id}/memberships`
5. `POST /organizations/{org_id}/invitations` for each additional team member with `email_address` and `role`
6. Optionally `POST /invitations` to send a platform-level invitation email

### 2. Set Up Enterprise SSO (SAML)

1. `POST /saml_connections` with `name`, `provider` (e.g., `saml_okta`), `domain`, and IdP metadata fields (`idp_entity_id`, `idp_sso_url`, `idp_certificate` or `idp_metadata_url`)
2. From the response, copy `acs_url` and `sp_entity_id` into your IdP's configuration
3. `PATCH /saml_connections/{id}` with `active: true` once IdP setup is confirmed
4. `POST /organizations/{org_id}/domains` with the verified domain and `enrollment_mode` to auto-enroll SSO users
5. Test by signing in with a domain email; verify the connection with `GET /saml_connections/{id}` and check `user_count`

### 3. Investigate and Lock a Suspicious Account

1. `GET /users` with `email_address` or `query` filter to find the suspect user
2. `GET /sessions?user_id={id}&status=active` to list all active sessions -- inspect `latest_activity` for suspicious IPs or devices
3. `POST /users/{user_id}/password/set_compromised` with `revoke_all_sessions: true` to force password reset and kill all sessions
4. `POST /users/{user_id}/lock` to prevent new sign-ins
5. Review `GET /users/{user_id}/organization_memberships` to assess blast radius across orgs
6. Once resolved, `POST /users/{user_id}/unlock` and `POST /users/{user_id}/password/unset_compromised`

### 4. Configure Machine-to-Machine Authentication

1. `POST /machines` with a descriptive `name` and optional `default_token_ttl`
2. `GET /machines/{machine_id}/secret_key` to retrieve the client secret for the service
3. `POST /machines/{machine_id}/scopes` with `to_machine_id` to grant cross-service access if needed
4. `POST /m2m_tokens` with desired `token_format` (opaque or JWT) and `claims` to issue a token
5. Verify tokens on the receiving service with `POST /m2m_tokens/verify`
6. Rotate secrets periodically via `POST /machines/{machine_id}/secret_key/rotate` with a `previous_token_ttl` grace period

### 5. Manage Billing Plans and Subscriptions

1. `GET /billing/plans` to list available plans; note each plan's `id` and `payer_type`
2. `POST /billing/prices` to create pricing tiers for a plan (set `amount` in smallest currency unit)
3. `GET /billing/subscription_items` to list all active subscriptions across users and orgs
4. To upgrade/downgrade: `POST /billing/subscription_items/{id}/price_transition` with `from_price_id` and `to_price_id`
5. To cancel: `DELETE /billing/subscription_items/{id}` (use `end_now: true` for immediate cancellation)
6. Review invoices via `GET /billing/statements` and drill into `GET /billing/statements/{id}/payment_attempts` for failed payments


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
