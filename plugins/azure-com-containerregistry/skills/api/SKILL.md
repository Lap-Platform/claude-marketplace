---
name: azure-container-registry
description: "Azure Container Registry API skill. Use when working with Azure Container Registry for v2, {name}, {nextBlobUuidLink}. Covers 26 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Container Registry
API version: 2019-08-15-preview

## Auth
basic | ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /v2/ -- verify access
3. POST /v2/{name}/blobs/uploads/ -- create first uploads

## Endpoints

26 endpoints across 5 groups. See references/api-spec.lap for full details.

### v2
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/ | Tells whether this Docker Registry instance supports Docker Registry HTTP API v2 |

### {name}
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/{name}/manifests/{reference} | Get the manifest identified by `name` and `reference` where `reference` can be a tag or digest. |
| PUT | /v2/{name}/manifests/{reference} | Put the manifest identified by `name` and `reference` where `reference` can be a tag or digest. |
| DELETE | /v2/{name}/manifests/{reference} | Delete the manifest identified by `name` and `reference`. Note that a manifest can _only_ be deleted by `digest`. |
| GET | /v2/{name}/blobs/{digest} | Retrieve the blob from the registry identified by digest. |
| HEAD | /v2/{name}/blobs/{digest} | Same as GET, except only the headers are returned. |
| DELETE | /v2/{name}/blobs/{digest} | Removes an already uploaded blob. |
| POST | /v2/{name}/blobs/uploads/ | Mount a blob identified by the `mount` parameter from another repository. |

### {nextBlobUuidLink}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{nextBlobUuidLink} | Retrieve status of upload identified by uuid. The primary purpose of this endpoint is to resolve the current status of a resumable upload. |
| PATCH | /{nextBlobUuidLink} | Upload a stream of data without completing the upload. |
| PUT | /{nextBlobUuidLink} | Complete the upload, providing all the data in the body, if necessary. A request without a body will just complete the upload with previously uploaded content. |
| DELETE | /{nextBlobUuidLink} | Cancel outstanding upload processes, releasing associated resources. If this is not called, the unfinished uploads will eventually timeout. |

### acr
| Method | Path | Description |
|--------|------|-------------|
| GET | /acr/v1/_catalog | List repositories |
| GET | /acr/v1/{name} | Get repository attributes |
| DELETE | /acr/v1/{name} | Delete the repository identified by `name` |
| PATCH | /acr/v1/{name} | Update the attribute identified by `name` where `reference` is the name of the repository. |
| GET | /acr/v1/{name}/_tags | List tags of a repository |
| GET | /acr/v1/{name}/_tags/{reference} | Get tag attributes by tag |
| PATCH | /acr/v1/{name}/_tags/{reference} | Update tag attributes |
| DELETE | /acr/v1/{name}/_tags/{reference} | Delete tag |
| GET | /acr/v1/{name}/_manifests | List manifests of a repository |
| GET | /acr/v1/{name}/_manifests/{reference} | Get manifest attributes |
| PATCH | /acr/v1/{name}/_manifests/{reference} | Update attributes of a manifest |

### oauth2
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth2/exchange | Exchange AAD tokens for an ACR refresh Token |
| POST | /oauth2/token | Exchange ACR Refresh token for an ACR Access Token |
| GET | /oauth2/token | Exchange Username, Password and Scope an ACR Access Token |

## Enhanced Skill Content
## Question Mapping

- "What repositories exist in my registry?" -> GET /acr/v1/_catalog
- "How do I pull a container image manifest?" -> GET /v2/{name}/manifests/{reference}
- "How do I push a new manifest to my repository?" -> PUT /v2/{name}/manifests/{reference}
- "How do I delete an image by tag or digest?" -> DELETE /v2/{name}/manifests/{reference}
- "Does a specific blob exist in my repository?" -> HEAD /v2/{name}/blobs/{digest}
- "How do I start uploading a blob or mount from another repo?" -> POST /v2/{name}/blobs/uploads/
- "How do I list all tags for a repository?" -> GET /acr/v1/{name}/_tags
- "How do I get details about a specific tag?" -> GET /acr/v1/{name}/_tags/{reference}
- "How do I delete a specific tag without deleting the manifest?" -> DELETE /acr/v1/{name}/_tags/{reference}
- "How do I update repository attributes (e.g., enable/disable write)?" -> PATCH /acr/v1/{name}
- "How do I get an OAuth2 access token for ACR?" -> POST /oauth2/token
- "How do I exchange an AAD token for an ACR refresh token?" -> POST /oauth2/exchange
- "How do I list all manifests for a repository?" -> GET /acr/v1/{name}/_manifests
- "How do I resume a chunked blob upload?" -> PATCH /{nextBlobUuidLink}
- "How do I check if the registry supports the V2 API?" -> GET /v2/

## Response Tips

- **Catalog & tag lists** (`/acr/v1/_catalog`, `/_tags`, `/_manifests`): Paginated via `last` and `n` params -- if `n` results return, fetch next page passing the last item name as `last`.
- **Manifest operations** (`/v2/{name}/manifests/`): 200 returns the manifest body with `Content-Type` and `Docker-Content-Digest` headers; set `accept` header to request a specific media type (e.g., OCI vs Docker v2).
- **Blob operations** (`/v2/{name}/blobs/`): GET/HEAD may return 307 redirects to the actual storage URL -- follow the `Location` header automatically.
- **Blob uploads** (`/v2/{name}/blobs/uploads/`, `/{nextBlobUuidLink}`): Chunked upload returns 202 with `Location` header containing `{nextBlobUuidLink}` for the next chunk; final PUT with `digest` completes the upload and returns 201.
- **ACR metadata** (`/acr/v1/{name}`, tags, manifests): PATCH endpoints accept attribute objects in `value` for toggling properties like deleteEnabled and writeEnabled.
- **OAuth2** (`/oauth2/`): Token responses include `access_token` and expiry; exchange endpoint converts AAD tokens to ACR refresh tokens.

## Anomaly Flags

- **307 redirects on blob downloads**: Agent should transparently follow redirects but surface if redirect targets fail or timeout, as this indicates storage-layer issues.
- **202 on deletes**: Deletion is asynchronous -- if the agent needs to confirm removal, it should poll the resource and surface if the item persists after a reasonable interval.
- **Pagination truncation**: If the response count equals `n`, warn the user that results may be truncated and offer to fetch additional pages.
- **Auth failures (401/403)**: Surface immediately with guidance to check token expiry; suggest re-running `/oauth2/token` or `/oauth2/exchange` to refresh credentials.
- **Manifest media type mismatch**: If a GET manifest returns an unexpected `Content-Type`, flag it -- the caller may need to set the `accept` header explicitly.
- **Empty `value` on PATCH responses**: If a metadata update returns 200 but the response body shows unchanged attributes, alert the user that the patch may not have applied.
- **Deprecated API version**: The spec is versioned `2019-08-15-preview` -- flag that this is a preview API and behavior may change.

## Playbook

### 1. Authenticate and List All Repositories

1. POST `/oauth2/exchange` with `grant_type=access_token`, your AAD `access_token`, and `service` set to your registry login server (e.g., `myregistry.azurecr.io`).
2. Use the returned `refresh_token` to POST `/oauth2/token` with `grant_type=refresh_token`, `service`, and `scope=registry:catalog:*`.
3. GET `/acr/v1/_catalog` with the access token as a Bearer header.
4. If results are paginated, repeat with `last` set to the final repository name and `n` for page size.

### 2. Inspect and Delete an Image by Tag

1. GET `/acr/v1/{name}/_tags/{reference}` to retrieve tag metadata including the manifest digest.
2. GET `/v2/{name}/manifests/{reference}` with `accept: application/vnd.docker.distribution.manifest.v2+json` to fetch the full manifest and confirm the digest.
3. DELETE `/v2/{name}/manifests/{digest}` using the digest (not the tag) to remove the image.
4. Optionally DELETE `/acr/v1/{name}/_tags/{reference}` to clean up the tag pointer if it was not auto-removed.

### 3. Push a New Image (Blob + Manifest)

1. POST `/v2/{name}/blobs/uploads/` to initiate a blob upload session; capture the `Location` header as `{nextBlobUuidLink}`.
2. PATCH `/{nextBlobUuidLink}` with each chunk of the layer data; capture the updated `Location` after each 202 response.
3. PUT `/{nextBlobUuidLink}?digest={digest}` with the final chunk to complete the blob upload.
4. Repeat steps 1-3 for each layer and the config blob.
5. PUT `/v2/{name}/manifests/{tag}` with the manifest JSON referencing all uploaded blob digests.

### 4. Manage Repository and Tag Attributes

1. GET `/acr/v1/{name}` to view current repository attributes (deleteEnabled, writeEnabled, listEnabled, readEnabled).
2. PATCH `/acr/v1/{name}` with `value` containing the attributes to change (e.g., `{"deleteEnabled": false}` to lock the repo).
3. To lock a specific tag, PATCH `/acr/v1/{name}/_tags/{reference}` with the desired attribute overrides.
4. Verify by GET on the same resource to confirm the update took effect.

### 5. Cross-Repository Blob Mount

1. POST `/v2/{targetName}/blobs/uploads/?mount={digest}&from={sourceName}` to request a blob mount from another repository.
2. If the blob exists in the source, the registry returns 201 with `Location` pointing to the blob in the target -- no upload needed.
3. If the mount fails (blob not found in source), the response initiates a regular upload session; proceed with the chunked upload flow from Playbook 3.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
