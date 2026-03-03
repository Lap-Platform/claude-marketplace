---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/generateSsoUrl -- create first generateSsoUrl

## Endpoints

12 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users | Lists a collection of registered users in the specified service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId} | Gets the entity state (Etag) version of the user specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId} | Gets the details of the user specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId} | Creates or Updates a user. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId} | Updates the details of the user specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId} | Deletes specific user. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/generateSsoUrl | Retrieves a redirection URL containing an authentication token for signing a given user into the developer portal. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/groups | Lists all user groups. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/subscriptions | Lists the collection of subscriptions of the specified user. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/identities | List of all user identities. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/token | Gets the Shared Access Authorization Token for the User. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users/{userId}/confirmations/password/send | Sends confirmation |

## Enhanced Skill Content
## Question Mapping

- "List all users in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/users
- "Filter users by name or email?" -> GET /.../{serviceName}/users with $filter parameter
- "Does a specific user exist?" -> HEAD /.../{serviceName}/users/{userId}
- "Get details for a specific user?" -> GET /.../{serviceName}/users/{userId}
- "Create a new user in API Management?" -> PUT /.../{serviceName}/users/{userId}
- "Update an existing user's properties?" -> PATCH /.../{serviceName}/users/{userId}
- "Delete a user and optionally remove their subscriptions?" -> DELETE /.../{serviceName}/users/{userId} with deleteSubscriptions and notify options
- "Generate a single sign-on URL for a user?" -> POST /.../{serviceName}/users/{userId}/generateSsoUrl
- "What groups does a user belong to?" -> GET /.../{serviceName}/users/{userId}/groups
- "List a user's API subscriptions?" -> GET /.../{serviceName}/users/{userId}/subscriptions
- "What identity providers are linked to a user?" -> GET /.../{serviceName}/users/{userId}/identities
- "Generate a shared access token for a user?" -> POST /.../{serviceName}/users/{userId}/token
- "Send a password reset email to a user?" -> POST /.../{serviceName}/users/{userId}/confirmations/password/send
- "How do I onboard a new developer and give them portal access?" -> PUT (create user) then POST generateSsoUrl
- "How do I audit a user's access before deleting them?" -> GET groups + GET subscriptions then DELETE user

## Response Tips

- **User listings** (GET .../users, .../groups, .../subscriptions): Responses are paged; follow `nextLink` to retrieve all results. Use `$filter` (OData syntax) to narrow results server-side rather than filtering client-side.
- **User detail** (GET .../users/{userId}): Returns a single entity with an `ETag` header -- capture this value, it is required for PATCH and DELETE via `If-Match`.
- **HEAD check**: Returns 200 with no body if the user exists; 404 if not. Use this for existence checks before create-or-update logic.
- **Create/Update** (PUT/PATCH): PUT returns 201 (created) or 200 (updated). PATCH returns 204 (no content) on success. Both require `If-Match: *` or a specific ETag.
- **Delete**: Returns 200 or 204 on success. A 404 means the user was already removed.
- **Token generation** (POST .../token): Returns a `SharedAccessSignature` string with an expiry. Treat this as a secret.
- **SSO URL** (POST .../generateSsoUrl): Returns a one-time URL. It expires quickly -- use it immediately.
- **Password confirmation** (POST .../confirmations/password/send): Returns 204 with no body. Success means the email was queued, not delivered.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed)**: The user entity was modified between your GET and your PATCH/DELETE. Re-fetch and retry.
- **404 on user operations**: The userId may be wrong, or the user was deleted externally. Surface this clearly rather than failing silently.
- **deleteSubscriptions=true on DELETE**: Flag when this flag is set -- it cascades and removes all the user's API subscriptions permanently.
- **notify=true on DELETE**: An email notification will be sent to the deleted user. Flag this in case the deletion should be silent.
- **Token expiry**: If the `parameters` body for token generation specifies an unusually long expiry, warn about security implications.
- **$filter injection**: If user-supplied input flows into the `$filter` parameter, flag potential OData injection risk.
- **Throttling (429 Too Many Requests)**: Azure ARM has per-subscription rate limits. Surface `Retry-After` header values and suggest backing off.
- **Deprecated API version**: This spec uses `2019-12-01-preview`. If Azure returns a warning header about version deprecation, surface it immediately.

## Playbook

### 1. Onboard a New Developer

1. PUT .../users/{userId} with `parameters` containing email, first/last name, and password or identity provider info
2. Confirm 201 response (user created) and capture the ETag
3. POST .../users/{userId}/generateSsoUrl to get a portal sign-in link
4. Send the SSO URL to the developer (it is single-use and short-lived)

### 2. Audit and Remove a User

1. GET .../users/{userId} to confirm the user exists and capture the ETag
2. GET .../users/{userId}/groups to review group memberships
3. GET .../users/{userId}/subscriptions to review active API subscriptions
4. DELETE .../users/{userId} with `If-Match` set to the ETag; set `deleteSubscriptions=true` if subscriptions should be removed, `notify=true` to email the user
5. HEAD .../users/{userId} to confirm deletion (expect 404)

### 3. Generate a Temporary Access Token

1. GET .../users/{userId} to confirm the user exists
2. POST .../users/{userId}/token with `parameters` specifying the desired `keyType` and `expiry`
3. Store the returned shared access signature securely -- do not log it
4. Use the token in subsequent API calls as a `Authorization: SharedAccessSignature` header

### 4. Reset a User's Password

1. HEAD .../users/{userId} to verify the user exists (expect 200)
2. POST .../users/{userId}/confirmations/password/send
3. Confirm 204 response -- the password reset email is queued
4. No further action needed; the user completes the reset via the email link

### 5. Bulk List Users and Their Group Memberships

1. GET .../users to retrieve the first page of users
2. Follow `nextLink` until all pages are consumed
3. For each user, GET .../users/{userId}/groups (parallelize where possible)
4. Use `$filter` on either call to narrow scope if only a subset of users or groups is needed


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
