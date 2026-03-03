---
name: id4i-api
description: "ID4i API skill. Use when working with ID4i for account, api, go. Covers 107 endpoints."
version: 1.0.0
generator: lapsh
---

# ID4i API
API version: 1.0.2

## Auth
ApiKey Authorization in header

## Base URL
https://backend.id4i.de/

## Setup
1. Set your API key in the appropriate header
2. GET /api/v1/apikeys -- verify access
3. POST /account/password -- create first password

## Endpoints

107 endpoints across 5 groups. See references/api-spec.lap for full details.

### account
| Method | Path | Description |
|--------|------|-------------|
| POST | /account/password | Request password reset |
| PUT | /account/password | Verify password reset |
| POST | /account/registration | Register user |
| PUT | /account/registration | Complete registration |
| POST | /account/verification | Verify registration |

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/apikeys | Find API key by organization |
| POST | /api/v1/apikeys | Create API key |
| GET | /api/v1/apikeys/privileges | List all privileges |
| GET | /api/v1/apikeys/{key} | Show API key |
| PUT | /api/v1/apikeys/{key} | Update API keys |
| DELETE | /api/v1/apikeys/{key} | Delete API key |
| GET | /api/v1/apikeys/{key}/privileges | List privileges |
| POST | /api/v1/apikeys/{key}/privileges | Add privilege |
| DELETE | /api/v1/apikeys/{key}/privileges | Remove privilege |
| GET | /api/v1/apikeys/{key}/privileges/{privilege}/id4ns | ID4ns of a privilege |
| POST | /api/v1/apikeys/{key}/privileges/{privilege}/id4ns | Add ID4ns of a privilege |
| DELETE | /api/v1/apikeys/{key}/privileges/{privilege}/id4ns | Remove id4ns of a privilege |
| GET | /api/v1/billing/{organizationId} | Get billing amount of services for a given organization |
| GET | /api/v1/billing/{organizationId}/positions | Get billing positions for a given organization |
| GET | /api/v1/changelog/organization/{organizationId}/ | List change log entries of an organization |
| POST | /api/v1/collections | Create collection |
| GET | /api/v1/collections/{id4n} | Find collection |
| DELETE | /api/v1/collections/{id4n} | Delete collection |
| PATCH | /api/v1/collections/{id4n} | Update collection |
| GET | /api/v1/collections/{id4n}/elements | List contents of the collection |
| POST | /api/v1/collections/{id4n}/elements | Add elements to collection |
| DELETE | /api/v1/collections/{id4n}/elements | Remove elements from collection |
| GET | /api/v1/countries | List countries |
| GET | /api/v1/documents/{id4n} | List documents |
| GET | /api/v1/documents/{id4n}/{organizationId} | List organization specific documents |
| POST | /api/v1/documents/{id4n}/{organizationId} | Create an document for an id4n |
| PUT | /api/v1/documents/{id4n}/{organizationId} | Put an document for an id4n |
| GET | /api/v1/documents/{id4n}/{organizationId}/{fileName} | Read document contents |
| DELETE | /api/v1/documents/{id4n}/{organizationId}/{fileName} | Delete a document |
| GET | /api/v1/documents/{id4n}/{organizationId}/{fileName}/metadata | Retrieve a document (meta-data only, no content) |
| PATCH | /api/v1/documents/{id4n}/{organizationId}/{fileName}/metadata | Update a document |
| POST | /api/v1/guids | Create GUID(s) |
| GET | /api/v1/guids/withoutCollection | Retrieve GUIDs not in any collection |
| GET | /api/v1/guids/{id4n} | Retrieve GUID information |
| PATCH | /api/v1/guids/{id4n} | Change GUID information. |
| GET | /api/v1/history/{id4n} | List history |
| POST | /api/v1/history/{id4n} | Add history item |
| GET | /api/v1/history/{id4n}/{organizationId} | DEPRECATED - List history |
| GET | /api/v1/history/{id4n}/{organizationId}/{sequenceId} | Get history item |
| PATCH | /api/v1/history/{id4n}/{organizationId}/{sequenceId} | Update history item |
| PUT | /api/v1/history/{id4n}/{organizationId}/{sequenceId}/visibility | Set history item visibility |
| GET | /api/v1/id4ns/{id4n} | Retrieve ID4n information |
| GET | /api/v1/id4ns/{id4n}/alias | Get all aliases for the given GUID or Collection. |
| POST | /api/v1/id4ns/{id4n}/alias/{aliasType} | Add alias for GUID or Collection |
| DELETE | /api/v1/id4ns/{id4n}/alias/{aliasType} | Remove aliases from GUID or Collection |
| GET | /api/v1/id4ns/{id4n}/collections | Retrieve collections of an ID |
| GET | /api/v1/id4ns/{id4n}/properties | Retrieve ID4n properties |
| DELETE | /api/v1/id4ns/{id4n}/properties | Delete ID4n properties |
| PATCH | /api/v1/id4ns/{id4n}/properties | Patch ID4n properties |
| POST | /api/v1/import/gs1 | Import GS1/MAPP codes |
| GET | /api/v1/info | Retrieve version information about ID4i |
| GET | /api/v1/microstorage/{id4n}/{organization} | Read data from microstorage |
| PUT | /api/v1/microstorage/{id4n}/{organization} | Write data to microstorage |
| GET | /api/v1/multiple/id4ns/properties | Get multiple ID4n properties |
| POST | /api/v1/organizations | Create organization |
| GET | /api/v1/organizations/{organizationId} | Find organization by id/namespace |
| PUT | /api/v1/organizations/{organizationId} | Update organization |
| DELETE | /api/v1/organizations/{organizationId} | Delete organization |
| GET | /api/v1/organizations/{organizationId}/addresses/billing | Retrieve billing address |
| PUT | /api/v1/organizations/{organizationId}/addresses/billing | Store billing address |
| DELETE | /api/v1/organizations/{organizationId}/addresses/billing | Remove billing address |
| GET | /api/v1/organizations/{organizationId}/addresses/default | Retrieve address |
| PUT | /api/v1/organizations/{organizationId}/addresses/default | Store address |
| GET | /api/v1/organizations/{organizationId}/collections | Get collections of organization |
| POST | /api/v1/organizations/{organizationId}/logo | Update organization logo |
| DELETE | /api/v1/organizations/{organizationId}/logo | Delete organization logo |
| GET | /api/v1/organizations/{organizationId}/messaging |  |
| PATCH | /api/v1/organizations/{organizationId}/messaging |  |
| POST | /api/v1/organizations/{organizationId}/messaging/enqueueCustomMessage | Enqueue a custom message |
| GET | /api/v1/organizations/{organizationId}/partner | Get partners of an organization |
| PUT | /api/v1/organizations/{organizationId}/partner | Add partner |
| DELETE | /api/v1/organizations/{organizationId}/partner | Remove partner |
| GET | /api/v1/organizations/{organizationId}/privileges | List my privileges |
| GET | /api/v1/organizations/{organizationId}/roles | List users and their roles |
| GET | /api/v1/organizations/{organizationId}/users | Find users in organization |
| POST | /api/v1/organizations/{organizationId}/users/invite | Invite Users |
| GET | /api/v1/organizations/{organizationId}/users/{username}/roles | Get user roles by username |
| POST | /api/v1/organizations/{organizationId}/users/{username}/roles | Add role(s) to user |
| DELETE | /api/v1/organizations/{organizationId}/users/{username}/roles | Remove role(s) from user |
| GET | /api/v1/public/documents/{id4n} | List public documents |
| GET | /api/v1/public/documents/{id4n}/{organizationId}/{fileName} | Read public document contents |
| GET | /api/v1/public/documents/{id4n}/{organizationId}/{fileName}/metadata | Retrieve a public document (meta-data only, no content) |
| GET | /api/v1/public/history/{id4n} | Shows the public history of the given GUID |
| GET | /api/v1/public/image/{imageID} | Resolve image |
| GET | /api/v1/public/organizations/{organizationId} | Read public organization information |
| GET | /api/v1/public/routes/{id4n} | Retrieve all public routes for a GUID |
| GET | /api/v1/roles | List roles |
| GET | /api/v1/routingfiles/{id4n} | Retrieve routing file |
| PUT | /api/v1/routingfiles/{id4n} | Store routing file |
| GET | /api/v1/routingfiles/{id4n}/route/{type} | Retrieve current route of a GUID (or ID4N) |
| GET | /api/v1/routingfiles/{id4n}/routes/{type} | Retrieve all routes of a GUID (or ID4N) |
| GET | /api/v1/search/guids | Search for GUIDs by alias |
| GET | /api/v1/search/guids/aliases/types | List all supported alias types |
| PUT | /api/v1/transfers/{id4n}/receiveInfo | Transfer a GUID or collection, obtaining it (i.e. becoming the holder) and if allowed also taking ownership |
| GET | /api/v1/transfers/{id4n}/sendInfo | Show transfer preparation information |
| PUT | /api/v1/transfers/{id4n}/sendInfo | Prepare an object for transfer |
| GET | /api/v1/user/organizations | Retrieve organizations of user |
| GET | /api/v1/users | Find users |
| GET | /api/v1/users/{username} | Find by username |

### go
| Method | Path | Description |
|--------|------|-------------|
| GET | /go/{guid} | Forward |

### login
| Method | Path | Description |
|--------|------|-------------|
| POST | /login | ID4i API Login |

### whois
| Method | Path | Description |
|--------|------|-------------|
| GET | /whois/{id4n} | Resolve owner of id4n |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the ID4i API?" -> POST /login
- "How do I register a new user account?" -> POST /account/registration
- "How do I reset my password?" -> POST /account/password
- "How do I create a new GUID?" -> POST /api/v1/guids
- "How do I look up what an ID4N belongs to?" -> GET /whois/{id4n}
- "How do I find GUIDs that aren't in any collection?" -> GET /api/v1/guids/withoutCollection
- "How do I search for a GUID by alias?" -> GET /api/v1/search/guids
- "How do I create a collection and add items to it?" -> POST /api/v1/collections then POST /api/v1/collections/{id4n}/elements
- "How do I upload a document to an ID4N?" -> POST /api/v1/documents/{id4n}/{organizationId}
- "How do I view the history of an item?" -> GET /api/v1/history/{id4n}
- "How do I transfer an item to another organization?" -> PUT /api/v1/transfers/{id4n}/sendInfo
- "How do I manage API key permissions?" -> POST /api/v1/apikeys/{key}/privileges
- "How do I invite users to my organization?" -> POST /api/v1/organizations/{organizationId}/users/invite
- "How do I set up routing for an ID4N?" -> PUT /api/v1/routingfiles/{id4n}
- "How do I check my organization's billing?" -> GET /api/v1/billing/{organizationId}

## Response Tips

- **Account endpoints**: 200/201/202 all indicate success at different stages; 202 means the action is accepted but pending (e.g., email verification required).
- **Paginated lists** (API keys, collections, users, history, documents): Use `offset` and `limit` params; responses include a result array -- always check total count to determine if more pages exist.
- **GUID/ID4N lookups**: Responses nest organization ownership and type information; check the `type` field to distinguish GUIDs from collections or labelled collections.
- **Document endpoints**: GET returns binary content directly; use the `/metadata` sub-path to get file info without downloading the file body.
- **Error responses**: The API uses a wide error code range (400-500); 409 specifically signals conflicts (duplicate GUID, name collision); 415 means wrong Content-Type header.
- **Public endpoints** (`/api/v1/public/*`): Return the same structure as authenticated counterparts but with restricted fields -- missing fields are permission-gated, not errors.

## Anomaly Flags

- **401 on any endpoint**: API key may be expired or revoked -- surface immediately and suggest re-authenticating via POST /login.
- **409 Conflict on GUID/collection creation**: The identifier already exists -- agent should check existing state with GET before retrying.
- **202 Accepted instead of 200**: The operation is asynchronous (registration verification, transfers) -- agent should notify the user that a follow-up step is required.
- **415 Unsupported Media Type**: Common when uploading documents or microstorage without correct Content-Type -- flag the header requirement.
- **Billing endpoint returning unexpected positions**: Surface billing changes proactively when `fromDate`/`toDate` range shows new line items.
- **Empty collection elements list**: If a collection returns zero elements after a bulk add, the GUIDs may belong to a different organization -- flag the organizationId mismatch.
- **History items with visibility changes**: When PATCH or PUT visibility is used, alert that downstream public history consumers will be affected.

## Playbook

### 1. Register and Set Up a New Organization

1. Register a user account: POST /account/registration with user details
2. Complete registration via the verification link: PUT /account/registration
3. Verify the account token: POST /account/verification
4. Log in to get a session: POST /login with credentials
5. Create an organization: POST /api/v1/organizations
6. Set the default address: PUT /api/v1/organizations/{organizationId}/addresses/default
7. Upload a logo: POST /api/v1/organizations/{organizationId}/logo

### 2. Create GUIDs, Organize into Collections, and Attach Documents

1. Create one or more GUIDs: POST /api/v1/guids with the organization and count
2. Create a collection: POST /api/v1/collections
3. Add GUIDs to the collection: POST /api/v1/collections/{id4n}/elements with the GUID list
4. Upload a document to a GUID: POST /api/v1/documents/{id4n}/{organizationId} with file content
5. Verify the document: GET /api/v1/documents/{id4n}/{organizationId}/{fileName}/metadata

### 3. Set Up API Key with Scoped Privileges

1. Create a new API key: POST /api/v1/apikeys with a name and organizationId
2. List available privileges: GET /api/v1/apikeys/privileges
3. Grant specific privileges to the key: POST /api/v1/apikeys/{key}/privileges
4. Scope a privilege to specific ID4Ns: POST /api/v1/apikeys/{key}/privileges/{privilege}/id4ns
5. Verify the key's effective permissions: GET /api/v1/apikeys/{key}/privileges

### 4. Transfer an Item Between Organizations

1. Look up the item: GET /api/v1/id4ns/{id4n} to confirm ownership
2. Set send info on the source side: PUT /api/v1/transfers/{id4n}/sendInfo with recipient details
3. Recipient sets receive info: PUT /api/v1/transfers/{id4n}/receiveInfo to accept
4. Verify the new ownership: GET /whois/{id4n}
5. Add a history entry documenting the transfer: POST /api/v1/history/{id4n}

### 5. Audit Item History and Public Access

1. Retrieve full private history: GET /api/v1/history/{id4n} with `includePrivate=true`
2. Check what the public sees: GET /api/v1/public/history/{id4n}
3. Adjust visibility on sensitive entries: PUT /api/v1/history/{id4n}/{organizationId}/{sequenceId}/visibility
4. Verify public documents are accessible: GET /api/v1/public/documents/{id4n}
5. Test the public routing resolution: GET /api/v1/public/routes/{id4n} with the target type


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
