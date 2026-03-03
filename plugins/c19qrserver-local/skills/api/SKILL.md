---
name: api-for-the-covid-19-tracking-qr-code-signin-server
description: "API for the COVID-19 Tracking QR Code Signin Server. API skill. Use when working with API for the COVID-19 Tracking QR Code Signin Server. for login, logout, signins. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# API for the COVID-19 Tracking QR Code Signin Server.
API version: 1.1

## Auth
ApiKey token in header

## Base URL
https://virtserver.swaggerhub.com/aijaz/QRCodeSigninServer/1.1

## Setup
1. Set your API key in the appropriate header
2. GET /signins -- verify access
3. POST /login -- create first login

## Endpoints

14 endpoints across 9 groups. See references/api-spec.lap for full details.

### login
| Method | Path | Description |
|--------|------|-------------|
| POST | /login | Log in to get an API token |

### logout
| Method | Path | Description |
|--------|------|-------------|
| POST | /logout | Log out |

### signins
| Method | Path | Description |
|--------|------|-------------|
| GET | /signins | Get signin info |

### signin
| Method | Path | Description |
|--------|------|-------------|
| POST | /signin | Create a new signin record |
| GET | /signin/{signinId} | Retrieve the information associated with a signin record |
| PUT | /signin/{signinId} | Update a signin record |
| DELETE | /signin/{signinId} | Delete a signin record |

### verifyPasswordChange
| Method | Path | Description |
|--------|------|-------------|
| POST | /verifyPasswordChange | Used for resetting your password when you forgot it |

### changePassword
| Method | Path | Description |
|--------|------|-------------|
| POST | /changePassword | Used for changing your password |

### requestPasswordReset
| Method | Path | Description |
|--------|------|-------------|
| POST | /requestPasswordReset | Used for requesting a password reset code |

### user
| Method | Path | Description |
|--------|------|-------------|
| POST | /user | Create a user |
| DELETE | /user/{userId} | Delete a team member's user record |
| GET | /user/{userId} | Retrieve the information associated with a team member's user record |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Retrieve the information associated with all team members' user records |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the API?" -> POST /login
- "How do I log out of the system?" -> POST /logout
- "How do I record a new visitor signin?" -> POST /signin
- "How do I look up a specific signin record?" -> GET /signin/{signinId}
- "How do I update a visitor's signin information?" -> PUT /signin/{signinId}
- "How do I delete a signin record?" -> DELETE /signin/{signinId}
- "How do I get a list of all recent signins?" -> GET /signins
- "How do I page through signin history?" -> GET /signins (use less_than + return_count)
- "How do I create a new user account?" -> POST /user
- "How do I look up a user's profile and permissions?" -> GET /user/{userId}
- "How do I list all users in the system?" -> GET /users
- "How do I delete a user account?" -> DELETE /user/{userId}
- "How do I reset a forgotten password?" -> POST /requestPasswordReset
- "How do I complete a password reset after receiving the email?" -> POST /verifyPasswordChange
- "How do I change my current password?" -> POST /changePassword

## Response Tips

- **Auth (login/logout):** Login returns a `token` for all subsequent requests plus role flags (`admin`, `read_only`). Store the token immediately.
- **Signins (list):** Returns an array; pagination is cursor-based using `less_than` (pass the lowest `id` from the previous page) with `return_count` controlling page size (default 100). No total count is provided.
- **Signin (single):** GET returns the full record including `dt` (numeric timestamp). POST returns only `{result: int}` (the new ID). PUT returns the user profile, not the signin record.
- **User management:** POST /user returns `{email, guid}` (guid is for password setup, not the user ID). GET /user/{userId} includes permission flags.
- **Password flows:** requestPasswordReset returns a `guid`; verifyPasswordChange consumes that `guid` with the new password. Neither returns detailed status beyond 200.
- **Errors:** 401 is universal (bad or missing token). 503 appears only on signin-related endpoints (service temporarily unavailable).

## Anomaly Flags

- **503 on signin endpoints:** The server may be temporarily unavailable. Surface this immediately -- it means the physical location's QR check-in is down.
- **401 after successful login:** Token may have expired or been invalidated server-side. Prompt re-authentication rather than retrying.
- **PUT /signin returns user profile instead of signin data:** This is by design, not a bug. Flag if the caller expects the updated signin record back.
- **POST /user returns guid, not user ID:** The guid is for password setup flow. Surface this so the caller doesn't mistake it for a session token.
- **Pagination exhaustion:** When GET /signins returns fewer results than `return_count`, the dataset is fully consumed. Flag when empty arrays come back unexpectedly.
- **Missing optional fields:** Signin records may lack `email` or `dt`. Surface when critical fields are absent in bulk operations.

## Playbook

### 1. Register a New User and Set Their Password

1. POST /login with admin credentials to get a token
2. POST /user with `{email, name, admin, read_only}` to create the account
3. Note the `guid` from the response
4. POST /verifyPasswordChange with `{guid, password}` to set the initial password
5. Confirm the new user can POST /login with their credentials

### 2. Record and Verify a Visitor Signin

1. POST /login to authenticate
2. POST /signin with `{name, phone}` (and optionally `email`)
3. Capture the `result` (signin ID) from the response
4. GET /signin/{signinId} to confirm the record was stored correctly
5. If corrections are needed, PUT /signin/{signinId} with updated fields

### 3. Page Through All Signin History

1. POST /login to authenticate
2. GET /signins with `{return_count: 100}` to fetch the first page
3. Find the lowest `id` in the returned batch
4. GET /signins with `{less_than: <lowest_id>, return_count: 100}`
5. Repeat step 3-4 until fewer than `return_count` results are returned

### 4. Reset a Forgotten Password

1. POST /requestPasswordReset with `{email}` (no auth token needed)
2. Capture the `guid` from the response
3. POST /verifyPasswordChange with `{guid, password}` to set the new password
4. POST /login with the email and new password to confirm it works

### 5. Audit Users and Clean Up Stale Accounts

1. POST /login with admin credentials
2. GET /users to retrieve the full user list
3. For each user of interest, GET /user/{userId} to check `admin` and `read_only` flags
4. DELETE /user/{userId} for any accounts that should be removed
5. GET /users again to confirm the cleanup


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
