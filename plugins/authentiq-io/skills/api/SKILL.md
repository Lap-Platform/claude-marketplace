---
name: authentiq-connect-api
description: "Authentiq Connect API skill. Use when working with Authentiq Connect for authorize, token, userinfo. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Authentiq Connect API
API version: 1.0

## Auth
OAuth2 | ApiKey Authorization in header | OAuth2 | OAuth2 | OAuth2

## Base URL
https://connect.authentiq.io/

## Setup
1. Set your API key in the appropriate header
2. GET /authorize -- verify access
3. POST /token -- create first token

## Endpoints

9 endpoints across 5 groups. See references/api-spec.lap for full details.

### authorize
| Method | Path | Description |
|--------|------|-------------|
| GET | /authorize | Authenticate a user |

### token
| Method | Path | Description |
|--------|------|-------------|
| POST | /token | Obtain an ID Token |

### userinfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /userinfo | Retrieve a user profile |

### client
| Method | Path | Description |
|--------|------|-------------|
| GET | /client | List clients |
| POST | /client | Register a client |
| GET | /client/{client_id} | View a client |
| PUT | /client/{client_id} | Update a client |
| DELETE | /client/{client_id} | Delete a client |

### {client_id}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{client_id}/iframe | Include a session iframe |

## Enhanced Skill Content
## Question Mapping

- "How do I start an OAuth2 login flow?" -> GET /authorize
- "How do I exchange an authorization code for tokens?" -> POST /token
- "How do I get the current user's profile?" -> GET /userinfo
- "How do I list all registered OAuth clients?" -> GET /client
- "How do I register a new OAuth client?" -> POST /client
- "How do I look up a specific client by ID?" -> GET /client/{client_id}
- "How do I update an existing client's settings?" -> PUT /client/{client_id}
- "How do I delete an OAuth client?" -> DELETE /client/{client_id}
- "How do I embed the login widget in my page?" -> GET /{client_id}/iframe
- "How do I refresh an access token?" -> POST /token (with grant_type=refresh_token)
- "How do I implement the full authorization code flow?" -> GET /authorize + POST /token
- "How do I verify a user's identity after login?" -> POST /token + GET /userinfo
- "How do I rotate client credentials?" -> GET /client/{client_id} + PUT /client/{client_id}
- "What scopes are available for authorization?" -> GET /authorize (scope parameter)

## Response Tips

- **authorize**: Does not return a body. Expect 302/303 redirects to your redirect_uri with `code` or `error` query params.
- **token**: Returns JSON with `access_token`, `token_type`, `expires_in`, and optionally `id_token` and `refresh_token`. A 401 means invalid client credentials; 400 means malformed grant.
- **userinfo**: Returns JSON with OIDC standard claims (sub, email, name, etc.). Presence of fields depends on granted scopes.
- **client CRUD**: GET collection returns an array of client objects. POST returns the created client with a generated `client_id` (201). PUT returns the updated client. DELETE returns no body (204).
- **iframe**: Returns HTML content, not JSON. Use the response directly in an iframe `srcdoc` or inject into the DOM.

## Anomaly Flags

- **401 on /userinfo**: Access token is expired or revoked. Surface immediately and suggest re-running the token flow.
- **400 on /token**: Usually indicates mismatched `redirect_uri`, expired `code`, or wrong `grant_type`. Flag the specific error field in the response body.
- **302 to redirect_uri with `error` param**: Authorization was denied or failed. Parse `error` and `error_description` from the redirect and surface to the user.
- **Missing `refresh_token` in /token response**: The authorization server may not support refresh tokens for this client type or the `offline_access` scope was not requested. Flag this if the user's workflow depends on token renewal.
- **204 without confirmation**: After DELETE /client/{client_id}, confirm to the user that absence of a body is expected success, not a silent failure.
- **Unexpected `prompt=login` loops**: If repeated /authorize calls keep requiring login, flag possible session or cookie misconfiguration.

## Playbook

### 1. Register a New Client and Get Credentials

1. POST /client with the client metadata (redirect URIs, client name, grant types) in the body
2. Store the returned `client_id` and `client_secret` securely
3. GET /client/{client_id} to confirm registration details

### 2. Complete Authorization Code Flow

1. GET /authorize with `response_type=code`, your `client_id`, `redirect_uri`, desired `scope`, and a random `state` value
2. User authenticates and is redirected back to your `redirect_uri` with a `code` param
3. POST /token with `grant_type=authorization_code`, the received `code`, `client_id`, `client_secret`, and the same `redirect_uri`
4. Store the returned `access_token` (and `refresh_token` if present)
5. GET /userinfo with the access token in the Authorization header to retrieve user profile claims

### 3. Embed Login Widget in a Web Page

1. GET /client to find your target `client_id` (or use a known one)
2. GET /{client_id}/iframe to retrieve the embeddable HTML
3. Inject the HTML response into an iframe element on your page
4. Listen for postMessage events from the iframe to capture auth callbacks

### 4. Update Client Configuration

1. GET /client/{client_id} to retrieve current client settings
2. Modify the desired fields (redirect URIs, client name, allowed scopes)
3. PUT /client/{client_id} with the full updated client body
4. Verify the response matches your intended changes

### 5. Decommission a Client

1. GET /client/{client_id} to confirm you are targeting the correct client
2. DELETE /client/{client_id} and confirm a 204 response
3. GET /client/{client_id} to verify deletion (expect 404)
4. Revoke any outstanding tokens issued to this client via the token endpoint if supported


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
