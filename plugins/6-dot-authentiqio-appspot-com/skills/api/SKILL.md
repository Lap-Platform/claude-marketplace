---
name: authentiq-api
description: "Authentiq API skill. Use when working with Authentiq for key, login, scope. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# Authentiq API
API version: 6

## Auth
ApiKey secret in query

## Base URL
https://6-dot-authentiqio.appspot.com/

## Setup
1. Set your API key in the appropriate header
2. GET /key/{PK} -- verify access
3. POST /key -- create first key

## Endpoints

14 endpoints across 3 groups. See references/api-spec.lap for full details.

### key
| Method | Path | Description |
|--------|------|-------------|
| POST | /key | Register a new ID `JWT(sub, devtoken)` |
| DELETE | /key | Revoke an Authentiq ID using email & phone. |
| GET | /key/{PK} | Get public details of an Authentiq ID. |
| POST | /key/{PK} | update properties of an Authentiq ID. |
| HEAD | /key/{PK} | HEAD info on Authentiq ID |
| PUT | /key/{PK} | Update Authentiq ID by replacing the object. |
| DELETE | /key/{PK} | Revoke an Identity (Key) with a revocation secret |

### login
| Method | Path | Description |
|--------|------|-------------|
| POST | /login | push sign-in request |

### scope
| Method | Path | Description |
|--------|------|-------------|
| POST | /scope | scope verification request |
| POST | /scope/{job} | this is a scope confirmation |
| PUT | /scope/{job} | authority updates a JWT with its signature |
| GET | /scope/{job} | get the status / current content of a verification job |
| HEAD | /scope/{job} | HEAD to get the status of a verification job |
| DELETE | /scope/{job} | delete a verification job |

## Enhanced Skill Content
## Question Mapping

- "How do I register a new identity key?" -> POST /key
- "How do I revoke or remove an identity?" -> DELETE /key
- "How do I look up a specific key by its public key?" -> GET /key/{PK}
- "How do I update an existing identity key?" -> POST /key/{PK}
- "Is a specific key still valid and not expired?" -> HEAD /key/{PK}
- "How do I replace or rotate a key?" -> PUT /key/{PK}
- "How do I permanently delete a key I own?" -> DELETE /key/{PK}
- "How do I authenticate a user with a callback?" -> POST /login
- "How do I initiate a new verification scope?" -> POST /scope
- "How do I confirm or push a verification job?" -> POST /scope/{job}
- "How do I update the status of a pending scope job?" -> PUT /scope/{job}
- "How do I check the result of a verification job?" -> GET /scope/{job}
- "Has a verification job completed yet?" -> HEAD /scope/{job}
- "How do I cancel an in-progress verification?" -> DELETE /scope/{job}
- "How do I test a scope request without triggering real verification?" -> POST /scope (with `test` param)

## Response Tips

- **key endpoints**: 201 on creation, 200 on updates/reads. A 410 on GET or HEAD means the key existed but has expired or been revoked -- treat as permanently gone, not a transient error. 409 signals a conflict (duplicate key or concurrent update).
- **login endpoint**: 200 returns authentication context to the provided callback URL. 401 means the credentials or identity could not be verified.
- **scope endpoints**: GET/HEAD return 200 when the job is complete with a result, 204 when the job is still pending (no body). Use HEAD for lightweight polling, GET only when you need the payload. 429 on POST /scope means you are being rate-limited on new verification requests.

## Anomaly Flags

- **Rate limit hit (429 on POST /scope)**: Surface immediately -- the client is creating scopes too fast. Back off before retrying.
- **Gone keys (410 on GET/HEAD /key/{PK})**: Flag that the key has been permanently revoked or expired, not just missing. Do not retry.
- **Conflict responses (409)**: On POST /key, the identity already exists. On PUT /key/{PK}, a concurrent modification occurred. Surface the conflict reason before retrying.
- **Unauthorized deletes (401 on DELETE /key/{PK})**: The provided secret does not match. Flag possible credential misconfiguration rather than silent retry.
- **Method not allowed (405 on POST /scope/{job})**: The job exists but is in a state that does not accept this action. Surface the job's current state to the user.

## Playbook

### Register and Verify a New Identity

1. POST /key with the identity body to register a new key (expect 201)
2. POST /scope with verification parameters to initiate identity verification
3. Poll HEAD /scope/{job} until response is 200 (complete) instead of 204 (pending)
4. GET /scope/{job} to retrieve the full verification result

### Authenticate a User

1. POST /login with credentials and a callback URL
2. On 200, redirect or process the authentication result delivered to the callback
3. On 401, surface the failure and prompt for corrected credentials

### Rotate an Existing Key

1. GET /key/{PK} to confirm the current key exists and retrieve its state
2. PUT /key/{PK} with the new key body to replace it (expect 200)
3. If 409, re-fetch the key to resolve the conflict, then retry the PUT

### Revoke and Clean Up an Identity

1. HEAD /key/{PK} to confirm the key is still active (200, not 410)
2. DELETE /key/{PK} with the secret to permanently remove the key
3. If any pending scopes exist, DELETE /scope/{job} for each to cancel them

### Test a Scope Before Going Live

1. POST /scope with the `test` parameter set to preview the verification flow
2. Review the 201 response for expected behavior
3. If satisfactory, POST /scope again without `test` to initiate real verification
4. Monitor with HEAD /scope/{job} and retrieve results with GET /scope/{job}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
