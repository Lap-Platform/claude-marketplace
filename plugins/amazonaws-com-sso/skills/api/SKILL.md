---
name: aws-single-sign-on
description: "AWS Single Sign-On API skill. Use when working with AWS Single Sign-On for federation, assignment, logout. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Single Sign-On
API version: 2019-06-10

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /federation/credentials -- verify access
3. POST /logout -- create first logout

## Endpoints

4 endpoints across 3 groups. See references/api-spec.lap for full details.

### federation
| Method | Path | Description |
|--------|------|-------------|
| GET | /federation/credentials | Returns the STS short-term credentials for a given role name that is assigned to the user. |

### assignment
| Method | Path | Description |
|--------|------|-------------|
| GET | /assignment/roles | Lists all roles that are assigned to the user for a given AWS account. |
| GET | /assignment/accounts | Lists all AWS accounts assigned to the user. These AWS accounts are assigned by the administrator of the account. For more information, see Assign User Access in the IAM Identity Center User Guide. This operation returns a paginated response. |

### logout
| Method | Path | Description |
|--------|------|-------------|
| POST | /logout | Removes the locally stored SSO tokens from the client-side cache and sends an API call to the IAM Identity Center service to invalidate the corresponding server-side IAM Identity Center sign in session.  If a user uses IAM Identity Center to access the AWS CLI, the user’s IAM Identity Center sign in session is used to obtain an IAM session, as specified in the corresponding IAM Identity Center permission set. More specifically, IAM Identity Center assumes an IAM role in the target account on behalf of the user, and the corresponding temporary AWS credentials are returned to the client. After user logout, any existing IAM role sessions that were created by using IAM Identity Center permission sets continue based on the duration configured in the permission set. For more information, see User authentications in the IAM Identity Center User Guide. |

## Enhanced Skill Content
## Question Mapping

- "How do I get temporary AWS credentials for a role?" -> GET /federation/credentials
- "What roles do I have access to in account 123456789012?" -> GET /assignment/roles
- "List all AWS accounts I can access with SSO" -> GET /assignment/accounts
- "Which accounts are available through my SSO session?" -> GET /assignment/accounts
- "Get me access keys for the AdminRole in my dev account" -> GET /federation/credentials
- "How do I sign out of SSO?" -> POST /logout
- "Invalidate my SSO bearer token" -> POST /logout
- "Show me the next page of accounts" -> GET /assignment/accounts (with next_token)
- "What roles are available before I assume one?" -> GET /assignment/roles
- "I need session credentials to call AWS services" -> GET /federation/credentials
- "How do I paginate through all my SSO roles?" -> GET /assignment/roles (with next_token + max_result)
- "Get a session token with expiration for a specific role and account" -> GET /federation/credentials
- "End my current SSO session across all accounts" -> POST /logout

## Response Tips

- **Federation (credentials):** `roleCredentials` may be null; check all nested fields (`accessKeyId`, `secretAccessKey`, `sessionToken`) before use. `expiration` is epoch milliseconds (int64), not seconds.
- **Assignment (roles/accounts):** Paginated via `nextToken` -- keep calling with `next_token` until `nextToken` is null. Lists (`roleList`, `accountList`) may be null or empty; treat both as "no results."
- **Logout:** Returns no body on success. A 200 confirms the token is invalidated; subsequent calls with that token will fail.

## Anomaly Flags

- **Expired credentials:** Surface when `roleCredentials.expiration` is in the past or within 5 minutes of now -- the caller needs to re-fetch.
- **Null credential fields:** If `roleCredentials` is returned but any of `accessKeyId`, `secretAccessKey`, or `sessionToken` is null, flag as incomplete -- credentials are unusable.
- **Empty account or role lists:** If `accountList` or `roleList` comes back null/empty with no `nextToken`, the user may lack SSO permission assignments -- surface this explicitly.
- **Bearer token rejection (401/403):** The SSO access token has likely expired. The user needs to re-authenticate through the SSO portal or OIDC device flow before retrying.
- **Pagination loop detection:** If the same `nextToken` is returned twice consecutively, flag to avoid infinite loops.

## Playbook

### 1. Discover Accounts and Assume a Role

1. Call `GET /assignment/accounts` with the SSO bearer token to list available accounts.
2. Pick the target account ID from `accountList`.
3. Call `GET /assignment/roles` with the bearer token and chosen `account_id`.
4. Select the desired role from `roleList`.
5. Call `GET /federation/credentials` with the `role_name`, `account_id`, and bearer token.
6. Use the returned `accessKeyId`, `secretAccessKey`, and `sessionToken` as temporary AWS credentials.

### 2. Paginate Through All Accounts

1. Call `GET /assignment/accounts` with `max_result` set (e.g., 20).
2. If `nextToken` is present in the response, call again with `next_token` set to that value.
3. Repeat until `nextToken` is null.
4. Merge all `accountList` arrays into a single list.

### 3. Rotate Expiring Credentials

1. Check the `expiration` field from a previous `GET /federation/credentials` response.
2. If expiration is within 5 minutes, call `GET /federation/credentials` again with the same `role_name` and `account_id`.
3. Replace the old credentials with the fresh ones in your environment or config.

### 4. Clean Session Teardown

1. Complete any in-flight AWS API calls using current session credentials.
2. Call `POST /logout` with the SSO bearer token to invalidate the session.
3. Discard all cached credentials and tokens locally -- they are no longer valid.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
