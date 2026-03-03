---
name: altoroj-rest-api
description: "AltoroJ REST API skill. Use when working with AltoroJ REST for login, account, transfer. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# AltoroJ REST API
API version: 1.0.2

## Auth
ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /login -- verify access
3. POST /login -- create first login

## Endpoints

12 endpoints across 6 groups. See references/api-spec.lap for full details.

### login
| Method | Path | Description |
|--------|------|-------------|
| GET | /login | Check if any user is logged in |
| POST | /login | Login method |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | Returns a list of all the accounts owned by the user |
| GET | /account/{accountNo} | Returns details about a specific account |
| GET | /account/{accountNo}/transactions | Returns the last 10 transactions attached to an account |
| POST | /account/{accountNo}/transactions | Return transactions between 2 specific dates |

### transfer
| Method | Path | Description |
|--------|------|-------------|
| POST | /transfer | Transfer money between two accounts |

### feedback
| Method | Path | Description |
|--------|------|-------------|
| POST | /feedback/submit | Submit feedback for the bank |
| GET | /feedback/{feedbackId} | Retrieve feedback |

### admin
| Method | Path | Description |
|--------|------|-------------|
| POST | /admin/addUser | Add new user |
| POST | /admin/changePassword | Change user password |

### logout
| Method | Path | Description |
|--------|------|-------------|
| GET | /logout | Logout from the bank |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the API?" -> POST /login
- "How do I check if my session is valid?" -> GET /login
- "What accounts do I have access to?" -> GET /account
- "Show me details for a specific account" -> GET /account/{accountNo}
- "What are the recent transactions on my account?" -> GET /account/{accountNo}/transactions
- "How do I add a transaction record to an account?" -> POST /account/{accountNo}/transactions
- "How do I transfer money between accounts?" -> POST /transfer
- "How do I submit feedback or a complaint?" -> POST /feedback/submit
- "How do I look up a specific feedback submission?" -> GET /feedback/{feedbackId}
- "How do I create a new user?" -> POST /admin/addUser
- "How do I change a user's password?" -> POST /admin/changePassword
- "How do I end my session?" -> GET /logout
- "How do I view all transactions then transfer funds?" -> GET /account/{accountNo}/transactions + POST /transfer
- "How do I onboard a new user and set their password?" -> POST /admin/addUser + POST /admin/changePassword

## Response Tips

- **Login/Logout**: 200 returns session or token data; 401 means invalid credentials -- re-prompt, do not retry silently.
- **Account**: 200 returns account objects, possibly nested with balances; 401 means expired session -- re-authenticate first.
- **Transactions**: 200 may return an array; check for empty lists vs missing account. 501 on POST means the operation is not implemented server-side.
- **Transfer**: 200 confirms the transfer; 400 typically means insufficient funds or invalid account numbers -- surface the body message verbatim.
- **Feedback**: Submit (POST) needs no auth; retrieval (GET) does -- a 401 on GET means the user must log in first.
- **Admin**: 200 confirms the action; 400 usually contains validation detail (duplicate username, weak password) -- always parse and display the error body.

## Anomaly Flags

- **501 on POST endpoints** (transactions, transfer): The server does not support this operation -- flag immediately rather than retrying.
- **401 on any authenticated endpoint**: Session likely expired. Proactively suggest re-authentication via POST /login before continuing the workflow.
- **500 errors**: Server-side failure -- surface to the user with the response body; do not retry more than once.
- **400 on transfer or admin actions**: Almost always a validation error with actionable detail in the response body -- extract and display the message field.
- **Missing Authorization header**: Several endpoints require it. If a 401 appears early in a workflow, check that the auth header is being passed before assuming bad credentials.
- **Feedback submit returning 401**: Unusual since the endpoint does not list Authorization as required in the spec, yet 401 is a possible error -- flag this inconsistency and inspect the response.

## Playbook

### 1. Authenticate and Browse Accounts

1. POST /login with credentials in the body to obtain a session/token.
2. GET /account with the Authorization header to list all accessible accounts.
3. GET /account/{accountNo} to drill into a specific account's details.

### 2. Review Transactions and Transfer Funds

1. Authenticate via POST /login.
2. GET /account to identify source and destination account numbers.
3. GET /account/{accountNo}/transactions on the source account to verify balance/history.
4. POST /transfer with source account, destination account, and amount in the body.
5. GET /account/{accountNo}/transactions again to confirm the transfer appears.

### 3. Admin: Onboard a New User

1. Authenticate as an admin via POST /login.
2. POST /admin/addUser with the new user's details in the body.
3. POST /admin/changePassword to set the initial password for the new user.
4. Verify by logging in as the new user via POST /login with their credentials.

### 4. Submit and Track Feedback

1. POST /feedback/submit with the feedback payload (no auth required to submit).
2. Note the feedbackId returned in the response.
3. Authenticate via POST /login if not already.
4. GET /feedback/{feedbackId} to check the status of the submission.

### 5. Secure Session Lifecycle

1. POST /login to start a session.
2. Perform all required operations (account queries, transfers, admin tasks).
3. GET /logout to terminate the session.
4. Verify logout by calling GET /login -- expect a 401 confirming the session is invalidated.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
