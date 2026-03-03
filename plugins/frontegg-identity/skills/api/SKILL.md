---
name: authentication-and-identity-management
description: "Authentication and Identity Management API skill. Use when working with Authentication and Identity Management for resources. Covers 305 endpoints."
version: 1.0.0
generator: lapsh
---

# Authentication and Identity Management

## Auth
Bearer bearer

## Base URL
https://api.frontegg.com/identity

## Setup
1. Set Authorization header with your Bearer token
2. GET /resources/tenants/access-tokens/v1 -- verify access
3. POST /resources/auth/v2/api-token -- create first api-token

## Endpoints

305 endpoints across 1 groups. See references/api-spec.lap for full details.

### resources
| Method | Path | Description |
|--------|------|-------------|
| POST | /resources/auth/v2/api-token | Authenticate using API token |
| POST | /resources/auth/v2/api-token/token/refresh | Refresh API token |
| POST | /resources/tenants/access-tokens/v1 | Create account (tenant) access token |
| GET | /resources/tenants/access-tokens/v1 | Get account (tenant) access tokens |
| DELETE | /resources/tenants/access-tokens/v1/{id} | Delete account (tenant) access token |
| POST | /resources/tenants/api-tokens/v1 | Create client credentials token |
| GET | /resources/tenants/api-tokens/v1 | Get client credentials tokens |
| DELETE | /resources/tenants/api-tokens/v1/{id} | Delete client credentials token |
| PATCH | /resources/tenants/api-tokens/v1/{id} | Update client credentials token |
| POST | /resources/tenants/api-tokens/v2 | Create client credentials token |
| GET | /resources/tenants/invites/v1/user | Get account (tenant) invite of user |
| POST | /resources/tenants/invites/v1/user | Create account (tenant) invite for user |
| DELETE | /resources/tenants/invites/v1/user | Delete account (tenant) invite of user |
| PATCH | /resources/tenants/invites/v1/user | Update account (tenant) invite of user |
| POST | /resources/tenants/invites/v1/verify | Verify account (tenant) invite |
| GET | /resources/tenants/invites/v1/configuration | Get account (tenant) invite configuration |
| POST | /resources/tenants/invites/v2/user | Create tenant invite with roles for user |
| POST | /resources/tenants/invites/v1 | Create account (tenant) invite |
| GET | /resources/tenants/invites/v1/all | Get all account (tenant) invites |
| DELETE | /resources/tenants/invites/v1/token/{id} | Delete an account (tenant) invite |
| GET | /resources/configurations/v1/activation/strategies | Get activation strategies |
| POST | /resources/configurations/v1/activation/strategies | Create or update activation strategy |
| GET | /resources/configurations/v1/invitation/strategies | Get invitation strategies |
| POST | /resources/configurations/v1/invitation/strategies | Create or update invitation strategy |
| GET | /resources/roles/v2 | Get roles v2 |
| POST | /resources/roles/v2 | Create a new role |
| GET | /resources/roles/v2/distinct-levels | Get distinct levels of roles |
| GET | /resources/roles/v2/distinct-tenants | Get distinct assigned accounts (tenants) of roles |
| POST | /resources/approval-flows/v1 | Create approval flow |
| GET | /resources/approval-flows/v1 | Get approval flows |
| GET | /resources/approval-flows/v1/{id} | Get approval flow by ID |
| PATCH | /resources/approval-flows/v1/{id} | Update approval flow |
| DELETE | /resources/approval-flows/v1/{id} | Delete approval flow |
| POST | /resources/approval-flows/v1/approver-action | Approver action |
| GET | /resources/approval-flows/v1/execution-data | Get approval flow execution data |
| POST | /resources/approval-flows/v1/{id}/execute | Execute approval flow |
| POST | /resources/approval-flows/v1/step-up/execute | Execute step up approval flow |
| POST | /resources/configurations/v1 | Update identity management configuration |
| GET | /resources/configurations/v1 | Get identity management configuration |
| POST | /resources/configurations/v1/captcha-policy | Create captcha policy |
| PUT | /resources/configurations/v1/captcha-policy | Update captcha policy |
| GET | /resources/configurations/v1/captcha-policy | Get captcha policy |
| GET | /resources/configurations/v1/jwt-template-targeting | Get JWT template targeting configuration |
| POST | /resources/configurations/v1/jwt-template-targeting | Create JWT template targeting configuration |
| PUT | /resources/configurations/v1/jwt-template-targeting | Update or create JWT template targeting configuration |
| PATCH | /resources/configurations/v1/jwt-template-targeting/{id} | Update JWT template targeting configuration by ID |
| DELETE | /resources/configurations/v1/jwt-template-targeting/{id} | Delete JWT template targeting configuration by ID |
| POST | /resources/jwt-templates/v1 | Create JWT template |
| GET | /resources/jwt-templates/v1 | Get all JWT templates |
| GET | /resources/jwt-templates/v1/{id} | Get JWT template by ID |
| PUT | /resources/jwt-templates/v1/{id} | Update JWT template |
| DELETE | /resources/jwt-templates/v1/{id} | Delete JWT template |
| GET | /resources/configurations/v1/basic | Get identity management configuration |
| POST | /resources/sso/custom/v1 | Create custom oauth provider |
| GET | /resources/sso/custom/v1 | Get custom oauth provider |
| PATCH | /resources/sso/custom/v1/{id} | Update custom oauth provider |
| DELETE | /resources/sso/custom/v1/{id} | Delete custom oauth provider |
| POST | /resources/migrations/v1/auth0 | Migrate from Auth0 |
| POST | /resources/migrations/v1/local | Migrate a single user |
| POST | /resources/migrations/v1/local/bulk | Migrate users in bulk |
| GET | /resources/migrations/v1/local/bulk/status/{migrationId} | Check status of bulk migration |
| POST | /resources/migrations/v2/local/bulk | Migrate vendor users in bulk |
| GET | /resources/configurations/v1/delegation | Get delegation configuration |
| POST | /resources/configurations/v1/delegation | Create or update delegation configuration |
| POST | /resources/configurations/restrictions/v1/email-domain | Create domain restriction |
| GET | /resources/configurations/restrictions/v1/email-domain | Get domain restrictions |
| GET | /resources/configurations/restrictions/v1/email-domain/config | Get domain restrictions |
| POST | /resources/configurations/restrictions/v1/email-domain/config | Change domain restrictions config list type and toggle it off/on |
| DELETE | /resources/configurations/restrictions/v1/email-domain/{id} | Delete domain restriction |
| POST | /resources/configurations/restrictions/v1/email-domain/replace-bulk | Replace bulk domain restriction |
| POST | /resources/mail/v1/configurations | Create or update configuration |
| GET | /resources/mail/v1/configurations | Get configuration |
| DELETE | /resources/mail/v1/configurations | Delete configuration |
| POST | /resources/mail/v2/configurations | Create or update configuration v2 |
| POST | /resources/mail/v1/configs/templates | Add or update template |
| GET | /resources/mail/v1/configs/templates | Get template |
| DELETE | /resources/mail/v1/configs/templates/{templateId} | Delete template |
| GET | /resources/mail/v1/configs/{type}/default | Get default template by type |
| POST | /resources/auth/v1/user | Authenticate user with password |
| POST | /resources/auth/v1/user/token/refresh | Refresh user JWT token |
| POST | /resources/auth/v1/logout | Logout user |
| POST | /resources/users/v1/signUp | Signup user |
| POST | /resources/users/v1/signUp/username | Signup user with username |
| POST | /resources/configurations/v1/restrictions/ip/config | Create or update IP restriction configuration (ALLOW/BLOCK) |
| GET | /resources/configurations/v1/restrictions/ip/config | Get IP restriction configuration (ALLOW/BLOCK) |
| GET | /resources/configurations/v1/restrictions/ip | Get all IP restrictions |
| POST | /resources/configurations/v1/restrictions/ip | Create IP restriction |
| POST | /resources/configurations/v1/restrictions/ip/verify | Test Current IP |
| POST | /resources/configurations/v1/restrictions/ip/verify/allow | Test current IP is in allow list |
| DELETE | /resources/configurations/v1/restrictions/ip/{id} | Delete IP restriction by IP |
| POST | /resources/configurations/v1/lockout-policy | Create lockout policy |
| PATCH | /resources/configurations/v1/lockout-policy | Update lockout policy |
| GET | /resources/configurations/v1/lockout-policy | Get lockout policy |
| GET | /resources/vendor-only/users/access-tokens/v1/active | Get active access tokens list |
| GET | /resources/vendor-only/users/access-tokens/v1/{id} | Get user access token data |
| GET | /resources/vendor-only/tenants/access-tokens/v1/{id} | Get account (tenant) access token data |
| POST | /resources/auth/v1/user/mfa/recover | Recover MFA |
| POST | /resources/users/v1/mfa/disable | Disable authenticator app MFA |
| POST | /resources/users/v1/mfa/authenticator/{deviceId}/disable/verify | Disable authenticator app MFA |
| POST | /resources/users/v1/mfa/sms/{deviceId}/disable | Pre-disable SMS MFA |
| POST | /resources/users/v1/mfa/sms/{deviceId}/disable/verify | Disable SMS MFA |
| POST | /resources/auth/v1/user/mfa/verify | Verify MFA using code from authenticator app |
| POST | /resources/auth/v1/user/mfa/emailcode | Request verify MFA using email code |
| POST | /resources/auth/v1/user/mfa/emailcode/verify | Verify MFA using email code |
| POST | /resources/auth/v1/user/mfa/authenticator/enroll | Pre enroll MFA using Authenticator App |
| POST | /resources/auth/v1/user/mfa/authenticator/enroll/verify | Enroll MFA using Authenticator App |
| POST | /resources/auth/v1/user/mfa/authenticator/{deviceId}/verify | Verify MFA using authenticator app |
| POST | /resources/auth/v1/user/mfa/sms/enroll | Pre-enroll MFA using sms |
| POST | /resources/auth/v1/user/mfa/sms/enroll/verify | Enroll MFA using sms |
| POST | /resources/auth/v1/user/mfa/sms/{deviceId} | Request to verify MFA using sms |
| POST | /resources/auth/v1/user/mfa/sms/{deviceId}/verify | Verify MFA using sms |
| POST | /resources/auth/v1/user/mfa/webauthn/enroll | Pre enroll MFA using WebAuthN |
| POST | /resources/auth/v1/user/mfa/webauthn/enroll/verify | Enroll MFA using WebAuthN |
| POST | /resources/auth/v1/user/mfa/webauthn/{deviceId} | Request verify MFA using WebAuthN |
| POST | /resources/auth/v1/user/mfa/webauthn/{deviceId}/verify | Verify MFA using webauthn |
| GET | /resources/configurations/v1/mfa-policy/allow-remember-device | Check if remember device allowed |
| POST | /resources/users/v1/mfa/enroll | Enroll authenticator app MFA |
| POST | /resources/users/v1/mfa/authenticator/enroll | Enroll authenticator app MFA |
| POST | /resources/users/v1/mfa/enroll/verify | Verify authenticator app MFA enrollment |
| POST | /resources/users/v1/mfa/authenticator/enroll/verify | Verify authenticator app MFA enrollment |
| POST | /resources/users/v1/mfa/sms/enroll | Enroll SMS MFA |
| POST | /resources/users/v1/mfa/sms/enroll/verify | Verify MFA enrollment |
| POST | /resources/configurations/v1/mfa | Update MFA configuration |
| GET | /resources/configurations/v1/mfa | Get MFA configuration |
| POST | /resources/configurations/v1/mfa-policy | Create MFA policy |
| PATCH | /resources/configurations/v1/mfa-policy | Update security policy |
| PUT | /resources/configurations/v1/mfa-policy | Upsert security policy |
| GET | /resources/configurations/v1/mfa-policy | Get security policy |
| GET | /resources/configurations/v1/mfa/strategies | Get MFA strategies |
| POST | /resources/configurations/v1/mfa/strategies | Create or update MFA strategy |
| POST | /resources/configurations/v1/password | Create or update password configuration |
| GET | /resources/configurations/v1/password | Get password policy configuration |
| POST | /resources/configurations/v1/password-history-policy | Create password history policy |
| PATCH | /resources/configurations/v1/password-history-policy | Update password history policy |
| GET | /resources/configurations/v1/password-history-policy | Get password history policy |
| POST | /resources/users/v1/passwords/reset | Reset password |
| POST | /resources/users/v1/passwords/reset/verify | Verify password |
| POST | /resources/users/v1/passwords/change | Change password |
| GET | /resources/users/v1/passwords/config | Get strictest password configuration |
| POST | /resources/users/v2/passwords/reset/email | Reset password via email |
| POST | /resources/users/v2/passwords/reset/sms | Reset password via SMS |
| POST | /resources/users/v2/passwords/reset/sms/verify | Verify password reset code sent via SMS |
| GET | /resources/configurations/v1/password-rotation | Get password expiration period configuration |
| POST | /resources/configurations/v1/password-rotation | Manage password expiration |
| GET | /resources/configurations/v1/password-rotation/vendor | Get environment configuration for password expiration period. |
| POST | /resources/auth/v1/passwordless/smscode/prelogin | SMS code prelogin |
| POST | /resources/auth/v1/passwordless/smscode/postlogin | SMS code postlogin |
| POST | /resources/auth/v1/passwordless/magiclink/prelogin | Magic link prelogin |
| POST | /resources/auth/v1/passwordless/magiclink/postlogin | Magic link postlogin |
| POST | /resources/auth/v1/passwordless/code/prelogin | OTC (One-Time Code) prelogin |
| POST | /resources/auth/v1/passwordless/code/postlogin | OTC (One-Time Code) postlogin |
| GET | /resources/permissions/v1 | Get permissions |
| POST | /resources/permissions/v1 | Create permissions |
| DELETE | /resources/permissions/v1/{permissionId} | Delete permission |
| PATCH | /resources/permissions/v1/{permissionId} | Update permission |
| PUT | /resources/permissions/v1/{permissionId}/roles | Set a permission to multiple roles |
| PUT | /resources/permissions/v1/classification | Set permissions classification |
| GET | /resources/permissions/v1/categories | Get permissions categories |
| POST | /resources/permissions/v1/categories | Create category |
| PATCH | /resources/permissions/v1/categories/{categoryId} | Update category |
| DELETE | /resources/permissions/v1/categories/{categoryId} | Delete category |
| POST | /resources/users/access-tokens/v1 | Create user access token |
| GET | /resources/users/access-tokens/v1 | Get user access tokens |
| DELETE | /resources/users/access-tokens/v1/{id} | Delete user access token by token ID |
| POST | /resources/users/api-tokens/v1 | Create user client credentials token |
| GET | /resources/users/api-tokens/v1 | Get user client credentials tokens |
| DELETE | /resources/users/api-tokens/v1/{id} | Delete user client credentials token by token ID |
| GET | /resources/roles/v1 | Get roles |
| POST | /resources/roles/v1 | Create roles |
| DELETE | /resources/roles/v1/{roleId} | Delete role |
| PATCH | /resources/roles/v1/{roleId} | Update role |
| PUT | /resources/roles/v1/{roleId}/permissions | Assign permissions to a role |
| PUT | /resources/roles/v1/{roleId}/tenant | Update role tenant |
| GET | /resources/users/phone-numbers/v1 | Get all phone numbers |
| POST | /resources/users/phone-numbers/v1 | Set phone number for a user |
| POST | /resources/users/phone-numbers/v1/preverify | Pre-verify user's phone number |
| POST | /resources/users/phone-numbers/v1/verify | Verify creation of phone number for user |
| DELETE | /resources/users/phone-numbers/v1/{id} | Delete user's phone number |
| POST | /resources/users/phone-numbers/v1/{id}/delete/verify | Verify delete user's phone number |
| GET | /resources/users/phone-numbers/v1/me | Get current user's phone numbers |
| GET | /resources/users/phone-numbers/v2 | Get all phone numbers v2 |
| POST | /resources/configurations/v1/sms | Creates or updates a vendor SMS config |
| DELETE | /resources/configurations/v1/sms | Deletes a vendor SMS config |
| GET | /resources/configurations/v1/sms | Gets a vendor SMS config |
| GET | /resources/configurations/v1/sms/templates | Gets vendor SMS templates |
| GET | /resources/configurations/v1/sms/templates/{type} | Gets vendor SMS template by type |
| DELETE | /resources/configurations/v1/sms/templates/{type} | Deletes vendor SMS template by type |
| POST | /resources/configurations/v1/sms/templates/{type} | Create or update a vendor SMS template |
| GET | /resources/configurations/v1/sms/templates/{type}/default | Gets vendor default SMS template by type |
| GET | /resources/configurations/v1/sms/templates/default/all | Gets all vendor default SMS templates |
| GET | /resources/configurations/sessions/v1/vendor | Get environment session configuration |
| GET | /resources/configurations/sessions/v1 | Get account (tenant) or vendor default session configuration |
| POST | /resources/configurations/sessions/v1 | Create or update account (tenant) or vendor default session configuration |
| GET | /resources/configurations/v1/user-emails-policy | Get user emails policy |
| POST | /resources/configurations/v1/user-emails-policy | Create or update user emails policy |
| GET | /resources/groups/v1 | Get all groups |
| POST | /resources/groups/v1 | Create group |
| POST | /resources/groups/v1/bulkGet | Get groups by Ids |
| PATCH | /resources/groups/v1/{id} | Update group |
| DELETE | /resources/groups/v1/{id} | Delete group |
| GET | /resources/groups/v1/{id} | Get group by ID |
| GET | /resources/groups/v1/config | Get groups configuration |
| POST | /resources/groups/v1/config | Create or update groups configuration |
| POST | /resources/groups/v1/{groupId}/roles | Add roles to group |
| DELETE | /resources/groups/v1/{groupId}/roles | Remove roles from group |
| POST | /resources/groups/v1/{groupId}/users | Add users to group |
| DELETE | /resources/groups/v1/{groupId}/users | Remove users from group |
| GET | /resources/groups/v2 | Get all groups paginated |
| POST | /resources/tenants/users/v1/{userId}/disable | Disable user account (tenant) |
| POST | /resources/tenants/users/v1/{userId}/enable | Enable user account (tenant) |
| PUT | /resources/users/temporary/v1/{userId} | Sets a permanent user to temporary |
| DELETE | /resources/users/temporary/v1/{userId} | Sets a temporary user to permanent |
| GET | /resources/users/temporary/v1/configuration | Gets temporary users configuration |
| PUT | /resources/users/temporary/v1/configuration | Set temporary users configuration |
| GET | /resources/users/emails/v1 | Get all user emails |
| POST | /resources/users/emails/v1 | Create a user email |
| POST | /resources/users/emails/v1/verify | Verify user email |
| DELETE | /resources/users/emails/v1/{emailId} | Delete a user email |
| POST | /resources/users/emails/v1/vendor/{userId} | Create a user email for vendor |
| DELETE | /resources/users/emails/v1/vendor/{userId}/{emailId} | Delete a user email for vendor |
| POST | /resources/users/emails/v1/vendor/{userId}/primary | Mark email as primary for vendor |
| POST | /resources/users/emails/v1/me/primary | Mark email as primary |
| GET | /resources/users/emails/v1/me | Get current user`s emails |
| PUT | /resources/sub-tenants/users/v1/{userId}/access | Set sub-account access for a user |
| POST | /resources/users/v1/activate/reset | Reset user activation token |
| POST | /resources/users/v1/invitation/reset | Reset invitation |
| POST | /resources/users/v1/invitation/reset/all | Reset all invitation tokens |
| GET | /resources/users/v3 | Get users |
| GET | /resources/users/v3/roles | Get users roles |
| GET | /resources/users/v3/groups | Get users groups |
| POST | /resources/users/v3/me/unlock | Unlock user |
| POST | /resources/users/v2 | Invite user |
| PUT | /resources/users/v2/me | Update user profile |
| GET | /resources/users/v2/me | Get user profile |
| POST | /resources/users/v1 | Create user |
| PUT | /resources/users/v1 | Update user |
| DELETE | /resources/users/v1/{userId} | Remove user |
| PUT | /resources/users/v1/{userId} | Update user (global) |
| POST | /resources/users/v1/{userId}/roles | Assign roles to user |
| DELETE | /resources/users/v1/{userId}/roles | Unassign roles from user |
| PUT | /resources/users/v1/tenant | Update user's active account (tenant) |
| GET | /resources/users/v1/query/phrase | Get users with fuzzy search |
| GET | /resources/usernames/v1 | Get usernames for users |
| POST | /resources/usernames/v1 | Create a username for user |
| DELETE | /resources/usernames/v1/{username} | Delete a username for user |
| GET | /resources/usernames/v1/me | Get authenticated user's username |
| POST | /resources/users/v1/email/me | Update user email |
| POST | /resources/users/v1/email/me/verify | Verify user email |
| POST | /resources/users/v1/activate | Activate user |
| POST | /resources/users/v1/activate/code | Activate user with code |
| GET | /resources/users/v1/activate/strategy | Get user activation strategy |
| POST | /resources/users/v1/invitation/accept | Accept invitation |
| POST | /resources/users/v1/invitation/accept/code | Accept invitation with code |
| GET | /resources/users/v3/me | Get user profile |
| GET | /resources/users/v2/me/tenants | Get user accounts (tenants) |
| GET | /resources/users/v2/me/hierarchy | Get user accounts (tenants) hierarchy |
| GET | /resources/users/v1/me/authorization | Get user permissions and roles |
| GET | /resources/users/v1/me/tenants | Get user accounts (tenants) |
| GET | /resources/user-sources/v1 | Get vendor user sources |
| GET | /resources/user-sources/v1/{id} | Get vendor user source |
| DELETE | /resources/user-sources/v1/{id} | Delete user source |
| POST | /resources/user-sources/v1/external/auth0 | Create Auth0 external user source |
| POST | /resources/user-sources/v1/external/cognito | Create Cognito external user source |
| POST | /resources/user-sources/v1/external/firebase | Create Firebase external user source |
| POST | /resources/user-sources/v1/external/custom-code | Create Custom-Code external user source |
| POST | /resources/user-sources/v1/federation | Create Federation user source |
| PUT | /resources/user-sources/v1/external/auth0/{id} | Update Auth0 external user source |
| PUT | /resources/user-sources/v1/external/cognito/{id} | Update Cognito external user source |
| PUT | /resources/user-sources/v1/external/firebase/{id} | Update Firebase external user source |
| PUT | /resources/user-sources/v1/external/custom-code/{id} | Update Custom-Code external user source |
| PUT | /resources/user-sources/v1/federation/{id} | Update Federation user source |
| POST | /resources/user-sources/v1/assign | Assign applications to a user source |
| POST | /resources/user-sources/v1/unassign | Unassign applications from a user source |
| GET | /resources/user-sources/v1/{id}/users | Get user source users |
| GET | /resources/users/sessions/v1/me | Get user's active sessions |
| DELETE | /resources/users/sessions/v1/me/all | Delete all user sessions |
| DELETE | /resources/users/sessions/v1/me/{id} | Delete single user's session |
| GET | /resources/vendor-only/users/v1/{userId} | Get user |
| POST | /resources/vendor-only/users/v1/{userId}/mfa/unenroll | Unenroll user from MFA globally |
| POST | /resources/vendor-only/users/v1/passwords/verify | Verify user's password |
| POST | /resources/vendor-only/users/v1 | Create user |
| GET | /resources/tenants/users/v1/statuses | Get users account (tenant) statuses |
| POST | /resources/users/phone-numbers/v1/vendor/{userId} | Create user phone number verified by default |
| DELETE | /resources/users/phone-numbers/v1/vendor/{userId}/{phoneId} | Delete user phone number on an environment |
| POST | /resources/users/bulk/v1/invite | Invite users to an account (tenant) in bulk |
| GET | /resources/users/bulk/v1/status/{id} | Get status of bulk invite task |
| GET | /resources/users/v1/email | Get user by email |
| GET | /resources/users/v1/{id} | Get user by ID |
| POST | /resources/users/v1/{userId}/verify | Verify user |
| PUT | /resources/users/v1/{userId}/invisible | Make user invisible |
| PUT | /resources/users/v1/{userId}/superuser | Make user super-user |
| PUT | /resources/users/v1/{userId}/tenant | Set user's account (tenant) |
| POST | /resources/users/v1/{userId}/tenant | Add user to account (tenant) |
| PUT | /resources/users/v1/{userId}/email | Update user email |
| POST | /resources/users/v1/{userId}/links/generate-activation-token | Generate activation token |
| POST | /resources/users/v1/{userId}/links/generate-password-reset-token | Generate password reset token |
| POST | /resources/users/v1/{userId}/unlock | Unlock user |
| POST | /resources/users/v1/{userId}/lock | Lock user |
| PUT | /resources/users/v1/tenants/migrate | Move all users from one account (tenant) to another |
| GET | /resources/applications/v1/{appId}/users | Get users for application |
| GET | /resources/applications/v1/{userId}/apps | Get applications for user |
| POST | /resources/applications/v1 | Assign users to application |
| DELETE | /resources/applications/v1 | Unassign users from application |
| GET | /resources/applications/user-tenants/active/v1 | Get user active accounts (tenants) in applications |
| PUT | /resources/applications/user-tenants/active/v1 | Switch users active account (tenant) in applications |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the API?" -> POST /resources/auth/v2/api-token
- "How do I refresh an expired token?" -> POST /resources/auth/v2/api-token/token/refresh
- "How do I sign up a new user?" -> POST /resources/users/v1/signUp
- "How do I log in a user with email and password?" -> POST /resources/auth/v1/user
- "How do I reset a user's password?" -> POST /resources/users/v1/passwords/reset
- "How do I list all users in a tenant?" -> GET /resources/users/v3
- "How do I create a role and assign permissions?" -> POST /resources/roles/v1 + PUT /resources/roles/v1/{roleId}/permissions
- "How do I invite a user to a tenant?" -> POST /resources/tenants/invites/v1/user
- "How do I enable MFA for a user?" -> POST /resources/users/v1/mfa/enroll + POST /resources/users/v1/mfa/enroll/verify
- "How do I set up an approval workflow?" -> POST /resources/approval-flows/v1
- "How do I configure password complexity rules?" -> POST /resources/configurations/v1/password
- "How do I migrate users from Auth0?" -> POST /resources/migrations/v1/auth0
- "How do I create a tenant API token for M2M auth?" -> POST /resources/tenants/api-tokens/v1
- "How do I restrict login by IP address?" -> POST /resources/configurations/v1/restrictions/ip + POST /resources/configurations/v1/restrictions/ip/config
- "How do I bulk invite users to a tenant?" -> POST /resources/users/bulk/v1/invite

## Response Tips

- **Auth endpoints** (`/auth/`): Always check `mfaRequired` -- if `true`, the flow is incomplete and you must proceed to an MFA verification endpoint using the returned `mfaToken`. The `accessToken` is only present when auth is fully complete.
- **Token endpoints** (`/api-tokens/`, `/access-tokens/`): The `secret` field is only returned on creation (POST). Subsequent GET calls omit it. Store it immediately.
- **User endpoints** (`/users/v3`, `/users/v1`): List responses use `_limit`/`_offset` pagination. Default limit is typically 50. Iterate until results returned < limit.
- **Role and permission endpoints** (`/roles/`, `/permissions/`): Responses nest `permissions` as arrays of IDs or maps depending on endpoint version (v1 vs v2). The v2 roles endpoint supports `_sortBy` and `_filter` for server-side filtering.
- **Bulk operations** (`/bulk/`): Return `202 Accepted` with a `migrationId` or `id`. Poll the corresponding status endpoint to track completion.
- **Configuration endpoints** (`/configurations/`): POST creates (returns 201), PATCH updates (returns 200). A 409 on POST means the config already exists -- use PATCH instead.
- **Approval flows**: Execution is async. After `POST /{id}/execute`, the response is 200 with no body. Watch for webhook callbacks or poll execution data.

## Anomaly Flags

- **409 Conflict on policy creation**: The policy already exists. Surface this and suggest using PATCH instead of POST for lockout-policy, mfa-policy, or password-history-policy.
- **`isBreachedPassword: true`** in auth responses: The user's password appeared in a known breach database. Prompt immediate password change via `/passwords/change`.
- **`mfaRequired: true` without `mfaDevices`**: User must enroll in MFA before they can complete login. Route to the appropriate enroll endpoint.
- **`passwordExpiresIn` present and low**: Password rotation is active and the user's password is expiring soon. Surface the remaining time and suggest password change.
- **`isLocked: true` on user objects**: The user account is locked (likely from failed login attempts). Suggest calling `POST /users/v1/{userId}/unlock`.
- **`verified: false` on user objects**: The user has not completed email verification. May need to resend activation via `POST /users/v1/activate/reset`.
- **`activatedForTenant: false`**: User exists but is not active for the current tenant context. May indicate a pending invitation.
- **404 on GET policy endpoints**: The policy has never been created. Use POST to initialize it before attempting PATCH.
- **Bulk operation still pending**: If polling `/bulk/v1/status/{id}` shows incomplete status, surface progress and warn about partial failures.

## Playbook

### 1. Authenticate and maintain a session

1. Obtain tokens: `POST /resources/auth/v2/api-token` with `clientId` and `secret`
2. Check if `mfaRequired` is `true` in the response
3. If MFA required, complete the appropriate MFA flow (authenticator, SMS, or email code)
4. Store `access_token` and `refresh_token`; note `expires_in` for scheduling refresh
5. Before expiry, call `POST /resources/auth/v2/api-token/token/refresh` with the `refreshToken`
6. On logout, call `POST /resources/auth/v1/logout`

### 2. Onboard a new user with roles

1. Create the user: `POST /resources/users/v1` with `frontegg-tenant-id`, `email`, and optional `roleIds`
2. If `skipInviteEmail` was false, the user receives an activation email
3. User activates via `POST /resources/users/v1/activate` with `userId` and `token` from email
4. Assign additional roles if needed: `POST /resources/users/v1/{userId}/roles` with `roleIds`
5. Verify the user profile: `GET /resources/users/v1/{id}` to confirm roles and activation status

### 3. Set up MFA enforcement for a tenant

1. Configure MFA methods: `POST /resources/configurations/v1/mfa` to enable authenticator app, SMS, or email
2. Set MFA strategies: `POST /resources/configurations/v1/mfa/strategies` for each desired method
3. Create the enforcement policy: `POST /resources/configurations/v1/mfa-policy` with `enforceMFAType: "Force"`
4. Optionally allow "remember device": set `allowRememberMyDevice: true` and `mfaDeviceExpiration` in seconds
5. Verify config: `GET /resources/configurations/v1/mfa-policy` to confirm the policy is active

### 4. Migrate users from an external identity provider

1. Configure the source connection (e.g., Auth0): `POST /resources/migrations/v1/auth0` with domain, clientId, and secret
2. For manual/local migration, use `POST /resources/migrations/v1/local` for individual users or `POST /resources/migrations/v1/local/bulk` for batch
3. Supply `passwordHash` and `passwordHashType` (bcrypt, scrypt, argon2, etc.) to preserve existing passwords
4. Poll `GET /resources/migrations/v1/local/bulk/status/{migrationId}` until all users are processed
5. Verify migrated users: `GET /resources/users/v3` filtered by tenant to confirm they appear correctly

### 5. Configure security policies (IP restrictions + lockout + password)

1. Set password complexity: `POST /resources/configurations/v1/password` with min length, required tests, and breach checking
2. Enable password history: `POST /resources/configurations/v1/password-history-policy` with `enabled: true` and `historySize`
3. Configure lockout: `POST /resources/configurations/v1/lockout-policy` with `enabled: true` and `maxAttempts`
4. Set up IP restrictions: `POST /resources/configurations/v1/restrictions/ip/config` with strategy (ALLOW or BLOCK) and `isActive: true`
5. Add specific IPs: `POST /resources/configurations/v1/restrictions/ip` for each IP rule
6. Validate with: `POST /resources/configurations/v1/restrictions/ip/verify` to test the current config against the caller's IP


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
