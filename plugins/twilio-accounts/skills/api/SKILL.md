---
name: twilio-accounts
description: "Twilio - Accounts API skill. Use when working with Twilio - Accounts for AuthTokens, Consents, Contacts. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Accounts
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://accounts.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/Credentials/AWS -- verify access
3. POST /v1/AuthTokens/Promote -- create first Promote

## Endpoints

20 endpoints across 6 groups. See references/api-spec.lap for full details.

### AuthTokens
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/AuthTokens/Promote | Promote the secondary Auth Token to primary. After promoting the new token, all requests to Twilio using your old primary Auth Token will result in an error. |
| POST | /v1/AuthTokens/Secondary | Create a new secondary Auth Token |
| DELETE | /v1/AuthTokens/Secondary | Delete the secondary Auth Token from your account |

### Consents
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Consents/Bulk |  |

### Contacts
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Contacts/Bulk |  |

### Credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Credentials/AWS | Retrieves a collection of AWS Credentials belonging to the account used to make the request |
| POST | /v1/Credentials/AWS | Create a new AWS Credential |
| GET | /v1/Credentials/AWS/{Sid} | Fetch the AWS credentials specified by the provided Credential Sid |
| POST | /v1/Credentials/AWS/{Sid} | Modify the properties of a given Account |
| DELETE | /v1/Credentials/AWS/{Sid} | Delete a Credential from your account |
| GET | /v1/Credentials/PublicKeys | Retrieves a collection of Public Key Credentials belonging to the account used to make the request |
| POST | /v1/Credentials/PublicKeys | Create a new Public Key Credential |
| GET | /v1/Credentials/PublicKeys/{Sid} | Fetch the public key specified by the provided Credential Sid |
| POST | /v1/Credentials/PublicKeys/{Sid} | Modify the properties of a given Account |
| DELETE | /v1/Credentials/PublicKeys/{Sid} | Delete a Credential from your account |

### Messaging
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /v1/Messaging/GeoPermissions |  |
| GET | /v1/Messaging/GeoPermissions |  |

### SafeList
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/SafeList/Numbers | Add a new phone number or phone number 1k prefix to SafeList. |
| GET | /v1/SafeList/Numbers | Check if a phone number or phone number 1k prefix exists in SafeList. |
| DELETE | /v1/SafeList/Numbers | Remove a phone number or phone number 1k prefix from SafeList. |

## Enhanced Skill Content
## Question Mapping

- "How do I rotate my Twilio auth token?" -> POST /v1/AuthTokens/Promote
- "How do I create a secondary auth token?" -> POST /v1/AuthTokens/Secondary
- "How do I delete my secondary auth token?" -> DELETE /v1/AuthTokens/Secondary
- "How do I list all my AWS credentials?" -> GET /v1/Credentials/AWS
- "How do I register new AWS credentials with Twilio?" -> POST /v1/Credentials/AWS
- "How do I look up a specific AWS credential by SID?" -> GET /v1/Credentials/AWS/{Sid}
- "How do I update an existing AWS credential?" -> POST /v1/Credentials/AWS/{Sid}
- "How do I remove an AWS credential?" -> DELETE /v1/Credentials/AWS/{Sid}
- "How do I list all public keys?" -> GET /v1/Credentials/PublicKeys
- "How do I upload a new public key?" -> POST /v1/Credentials/PublicKeys
- "How do I check which countries are allowed for messaging?" -> GET /v1/Messaging/GeoPermissions
- "How do I update geo permissions for messaging?" -> PATCH /v1/Messaging/GeoPermissions
- "How do I add a phone number to the safe list?" -> POST /v1/SafeList/Numbers
- "How do I check if a number is on the safe list?" -> GET /v1/SafeList/Numbers
- "How do I remove a number from the safe list?" -> DELETE /v1/SafeList/Numbers

## Response Tips

- **AuthTokens**: Promote returns the new primary token in `auth_token`; Secondary returns `secondary_auth_token`. Store these immediately as they may not be retrievable later.
- **Credentials (AWS & PublicKeys)**: List endpoints return `credentials` array with a `meta` object for pagination. Use `meta.next_page_url` to fetch the next page; `null` means you are on the last page. Control page size with `PageSize` (max varies by account).
- **Messaging GeoPermissions**: Both GET and PATCH return a `permissions` field typed as `any` -- expect a nested structure keyed by country code or region.
- **SafeList**: GET and POST return a flat `{sid, phone_number}` object. DELETE returns 204 with no body.
- **Consents & Contacts**: Bulk endpoints return `{items}` typed as `any` -- expect an array of per-record results with individual success/failure statuses.

## Anomaly Flags

- **Token rotation without secondary**: If a user calls POST /v1/AuthTokens/Promote without first creating a secondary token (POST /v1/AuthTokens/Secondary), warn that existing integrations using the old primary token will break immediately.
- **204 on DELETE with no confirmation**: DELETE endpoints return empty bodies. Surface a confirmation before calling, since there is no undo.
- **Pagination exhaustion**: If `meta.next_page_url` keeps returning results beyond an unexpectedly high count, flag that the credential list may be larger than expected and suggest auditing stale entries.
- **Bulk endpoint partial failures**: Consents and Contacts bulk endpoints may return mixed success/failure in the `items` array. Always inspect individual item statuses rather than relying on the HTTP 201 alone.
- **Stale credentials**: If a GET /v1/Credentials/AWS/{Sid} or PublicKeys/{Sid} returns a `date_updated` significantly older than `date_created`, flag the credential as potentially stale and recommend rotation.
- **Geo permissions changes**: PATCH to GeoPermissions can silently restrict messaging to entire countries. Surface a warning before applying changes.

## Playbook

### 1. Rotate Auth Token Safely

1. Create a secondary auth token: POST /v1/AuthTokens/Secondary
2. Store the `secondary_auth_token` from the response
3. Update all integrations and services to use the secondary token
4. Verify integrations work with the new token
5. Promote the secondary to primary: POST /v1/AuthTokens/Promote
6. Store the new `auth_token` from the response

### 2. Register and Manage AWS Credentials

1. Create the credential: POST /v1/Credentials/AWS (provide AWS key details in the request body)
2. Note the returned `sid` for future reference
3. Verify it appears in the list: GET /v1/Credentials/AWS
4. To update the friendly name or rotate keys: POST /v1/Credentials/AWS/{Sid}
5. To decommission: DELETE /v1/Credentials/AWS/{Sid}

### 3. Manage the Safe List for Phone Numbers

1. Check if a number is already listed: GET /v1/SafeList/Numbers?PhoneNumber=+15551234567
2. If not present, add it: POST /v1/SafeList/Numbers (include phone number in body)
3. Confirm addition by checking the returned `sid`
4. To remove later: DELETE /v1/SafeList/Numbers?PhoneNumber=+15551234567

### 4. Audit and Clean Up Credentials

1. List all AWS credentials: GET /v1/Credentials/AWS?PageSize=50
2. Page through results using `meta.next_page_url` until null
3. List all public keys: GET /v1/Credentials/PublicKeys?PageSize=50
4. For each credential, check `date_updated` -- flag any not updated in over 90 days
5. Review flagged credentials with your team
6. Delete unused credentials: DELETE /v1/Credentials/AWS/{Sid} or DELETE /v1/Credentials/PublicKeys/{Sid}

### 5. Configure Messaging Geo Permissions

1. Review current permissions: GET /v1/Messaging/GeoPermissions
2. Identify countries to enable or restrict
3. Apply changes: PATCH /v1/Messaging/GeoPermissions (include updated permission structure)
4. Verify the update: GET /v1/Messaging/GeoPermissions
5. Optionally filter by country: GET /v1/Messaging/GeoPermissions?CountryCode=US


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
