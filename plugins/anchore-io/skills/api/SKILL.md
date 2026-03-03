---
name: anchore-engine-api-server
description: "Anchore Engine API Server API skill. Use when working with Anchore Engine API Server for root, health, version. Covers 112 endpoints."
version: 1.0.0
generator: lapsh
---

# Anchore Engine API Server
API version: 0.1.20

## Auth
ApiKey username in formData

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET / -- verify access
3. POST /policies -- create first policies

## Endpoints

112 endpoints across 21 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Simple status check |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Health check, returns 200 and no body if service is running |

### version
| Method | Path | Description |
|--------|------|-------------|
| GET | /version | Returns the version object for the service, including db schema version info |

### policies
| Method | Path | Description |
|--------|------|-------------|
| GET | /policies | List policies |
| POST | /policies | Add a new policy |
| GET | /policies/{policyId} | Get specific policy |
| PUT | /policies/{policyId} | Update policy |
| DELETE | /policies/{policyId} | Delete policy |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions | List all subscriptions |
| POST | /subscriptions | Add a subscription of a specific type |
| GET | /subscriptions/{subscriptionId} | Get a specific subscription set |
| PUT | /subscriptions/{subscriptionId} | Update an existing and specific subscription |
| DELETE | /subscriptions/{subscriptionId} | Delete subscriptions of a specific type |

### summaries
| Method | Path | Description |
|--------|------|-------------|
| GET | /summaries/imagetags | List all visible image digests and tags |

### images
| Method | Path | Description |
|--------|------|-------------|
| POST | /images | Submit a new image for analysis by the engine |
| GET | /images | List all visible images |
| DELETE | /images | Bulk mark images for deletion |
| GET | /images/{imageDigest} | Get image metadata |
| DELETE | /images/{imageDigest} | Delete an image analysis |
| GET | /images/by_id/{imageId} | Lookup image by docker imageId |
| DELETE | /images/by_id/{imageId} | Delete image by docker imageId |
| GET | /images/{imageDigest}/check | Check policy evaluation status for image |
| GET | /images/by_id/{imageId}/check | Check policy evaluation status for image |
| GET | /images/{imageDigest}/vuln | Get vulnerability types |
| GET | /images/{imageDigest}/vuln/{vtype} | Get vulnerabilities by type |
| GET | /images/by_id/{imageId}/vuln | Get vulnerability types |
| GET | /images/by_id/{imageId}/vuln/{vtype} | Get vulnerabilities by type |
| GET | /images/{imageDigest}/content | List image content types |
| GET | /images/by_id/{imageId}/content | List image content types |
| GET | /images/{imageDigest}/content/{ctype} | Get the content of an image by type |
| GET | /images/{imageDigest}/content/files | Get the content of an image by type files |
| GET | /images/{imageDigest}/content/java | Get the content of an image by type java |
| GET | /images/{imageDigest}/content/malware | Get the content of an image by type malware |
| GET | /images/by_id/{imageId}/content/{ctype} | Get the content of an image by type |
| GET | /images/by_id/{imageId}/content/files | Get the content of an image by type files |
| GET | /images/by_id/{imageId}/content/java | Get the content of an image by type java |
| GET | /images/{imageDigest}/artifacts/retrieved_files | Return a list of analyzer artifacts of the specified type |
| GET | /images/{imageDigest}/artifacts/file_content_search | Return a list of analyzer artifacts of the specified type |
| GET | /images/{imageDigest}/artifacts/secret_search | Return a list of analyzer artifacts of the specified type |
| GET | /images/{imageDigest}/metadata | List image metadata types |
| GET | /images/{imageDigest}/sboms/native | Get image sbom in the native Anchore format |
| GET | /images/{imageDigest}/metadata/{mtype} | Get the metadata of an image by type |

### import
| Method | Path | Description |
|--------|------|-------------|
| POST | /import/images | Import an anchore image tar.gz archive file. This is a deprecated API replaced by the "/imports/images" route |

### repositories
| Method | Path | Description |
|--------|------|-------------|
| POST | /repositories | Add repository to watch |

### registries
| Method | Path | Description |
|--------|------|-------------|
| GET | /registries | List configured registries |
| POST | /registries | Add a new registry |
| GET | /registries/{registry} | Get a specific registry configuration |
| PUT | /registries/{registry} | Update/replace a registry configuration |
| DELETE | /registries/{registry} | Delete a registry configuration |

### status
| Method | Path | Description |
|--------|------|-------------|
| GET | /status | Service status |

### system
| Method | Path | Description |
|--------|------|-------------|
| GET | /system | System status |
| GET | /system/feeds | list feeds operations and information |
| POST | /system/feeds | trigger feeds operations |
| PUT | /system/feeds/{feed} | Disable the feed so that it does not sync on subsequent sync operations |
| DELETE | /system/feeds/{feed} | Delete the groups and data for the feed and disable the feed itself |
| PUT | /system/feeds/{feed}/{group} | Disable a specific group within a feed to not sync |
| DELETE | /system/feeds/{feed}/{group} | Delete the group data and disable the group itself |
| GET | /system/services | List system services |
| GET | /system/services/{servicename} | Get a service configuration and state |
| GET | /system/services/{servicename}/{hostid} | Get service config for a specific host |
| DELETE | /system/services/{servicename}/{hostid} | Delete the service config |
| GET | /system/policy_spec | Describe the policy language spec implemented by this service. |
| GET | /system/error_codes | Describe anchore engine error codes. |
| POST | /system/webhooks/{webhook_type}/test | Adds the capabilities to test a webhook delivery for the given notification type |

### event_types
| Method | Path | Description |
|--------|------|-------------|
| GET | /event_types | List Event Types |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | List Events |
| DELETE | /events | Delete Events |
| GET | /events/{eventId} | Get Event |
| DELETE | /events/{eventId} | Delete Event |

### query
| Method | Path | Description |
|--------|------|-------------|
| GET | /query/images/by_vulnerability | List images vulnerable to the specific vulnerability ID. |
| GET | /query/images/by_package | List of images containing given package |
| GET | /query/vulnerabilities | Listing information about given vulnerability |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | List user summaries. Only available to the system admin user. |
| POST | /accounts | Create a new user. Only avaialble to admin user. |
| GET | /accounts/{accountname} | Get info about an user. Only available to admin user. Uses the main user Id, not a username. |
| DELETE | /accounts/{accountname} | Delete the specified account, only allowed if the account is in the disabled state. All users will be deleted along with the account and all resources will be garbage collected |
| PUT | /accounts/{accountname}/state | Update the state of an account to either enabled or disabled. For deletion use the DELETE route |
| GET | /accounts/{accountname}/users | List accounts for the user |
| POST | /accounts/{accountname}/users | Create a new user |
| DELETE | /accounts/{accountname}/users/{username} | Delete a specific user credential by username of the credential. Cannot be the credential used to authenticate the request. |
| GET | /accounts/{accountname}/users/{username} | Get a specific user in the specified account |
| GET | /accounts/{accountname}/users/{username}/credentials | Get current credential summary |
| POST | /accounts/{accountname}/users/{username}/credentials | add/replace credential |
| DELETE | /accounts/{accountname}/users/{username}/credentials | Delete a credential by type |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | List the account for the authenticated user |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user | List authenticated user info |
| GET | /user/credentials | Get current credential summary |
| POST | /user/credentials | add/replace credential |

### archives
| Method | Path | Description |
|--------|------|-------------|
| GET | /archives |  |
| GET | /archives/rules |  |
| POST | /archives/rules |  |
| GET | /archives/rules/{ruleId} |  |
| DELETE | /archives/rules/{ruleId} |  |
| GET | /archives/images |  |
| POST | /archives/images |  |
| GET | /archives/images/{imageDigest} | Returns the archive metadata record identifying the image and tags for the analysis in the archive. |
| DELETE | /archives/images/{imageDigest} | Performs a synchronous archive deletion |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/token | Request a jwt token for subsequent operations, this request is authenticated with normal HTTP auth |

### imports
| Method | Path | Description |
|--------|------|-------------|
| POST | /imports/images | Begin the import of an image analyzed by Syft into the system |
| GET | /imports/images | Lists in-progress imports |
| GET | /imports/images/{operation_id} | Get detail on a single import |
| DELETE | /imports/images/{operation_id} | Invalidate operation ID so it can be garbage collected |
| GET | /imports/images/{operation_id}/packages | List uploaded package manifests |
| POST | /imports/images/{operation_id}/packages | Begin the import of an image analyzed by Syft into the system |
| GET | /imports/images/{operation_id}/dockerfile | List uploaded dockerfiles |
| POST | /imports/images/{operation_id}/dockerfile | Begin the import of an image analyzed by Syft into the system |
| GET | /imports/images/{operation_id}/manifest | List uploaded image manifests |
| POST | /imports/images/{operation_id}/manifest | Import a docker or OCI distribution manifest to associate with the image |
| GET | /imports/images/{operation_id}/parent_manifest | List uploaded parent manifests (manifest lists for a tag) |
| POST | /imports/images/{operation_id}/parent_manifest | Import a docker or OCI distribution manifest list to associate with the image |
| GET | /imports/images/{operation_id}/image_config | List uploaded image configs |
| POST | /imports/images/{operation_id}/image_config | Import a docker or OCI image config to associate with the image |

## Enhanced Skill Content
## Question Mapping

- "Is the Anchore Engine running and healthy?" -> GET /health
- "What version of Anchore Engine is deployed?" -> GET /version
- "How do I add a new container image for scanning?" -> POST /images
- "What vulnerabilities exist in my image?" -> GET /images/{imageDigest}/vuln/{vtype}
- "Does my image pass the security policy?" -> GET /images/{imageDigest}/check
- "What packages are installed in this image?" -> GET /images/{imageDigest}/content/{ctype}
- "Which images are affected by a specific CVE?" -> GET /query/images/by_vulnerability
- "Which images contain a specific package?" -> GET /query/images/by_package
- "How do I set up a new policy bundle?" -> POST /policies
- "What registries are configured for pulling images?" -> GET /registries
- "How do I create a new user account?" -> POST /accounts
- "What events or alerts have fired recently?" -> GET /events
- "How do I get an OAuth token for API access?" -> POST /oauth/token
- "What feeds are synced and are they up to date?" -> GET /system/feeds
- "How do I import an image from an archive file?" -> POST /import/images

## Response Tips

- **Images**: Results are arrays of image records; use `imageDigest` as the stable identifier across all subsequent calls (content, vuln, check). Images can also be referenced by `imageId` via `/images/by_id/` endpoints.
- **Vulnerabilities**: Vuln responses nest under vulnerability type (`vtype` such as `os`, `non-os`, `all`). Always specify `vtype` to avoid empty results. Use `vendor_only=true` to filter to vendor-confirmed CVEs.
- **Policies**: Policy check responses contain nested evaluation results per tag. Pass `detail=true` to get per-rule pass/fail breakdown. The `history=true` flag returns previous evaluation results.
- **Events**: Paginated via `page` and `limit` query params. Filter with `since`/`before` (ISO timestamps), `level`, `event_type`, and `resource_type` to narrow results.
- **Query endpoints**: `/query/images/by_vulnerability` and `/query/images/by_package` are paginated (`page`/`limit`). Response includes matched image records with digest and tag info.
- **Accounts/Users**: Account creation returns 409 on name conflicts. User credential endpoints return credential metadata, not raw secrets.
- **System/Feeds**: Feed and group objects include `enabled` booleans and last sync timestamps. A 400 on PUT means invalid enable/disable state transition.
- **Archives**: Archive image listing returns references, not full image records. Use the digest to retrieve or delete archived images.

## Anomaly Flags

- **Feed sync lag**: Surface when `GET /system/feeds` shows feeds with last sync time older than 24 hours -- vulnerability data may be stale.
- **Analysis stuck**: Flag images returned by `GET /images` with `analysis_status` not progressing to `analyzed` after a reasonable period.
- **Policy evaluation failures**: Alert when `GET /images/{imageDigest}/check` returns 500 -- may indicate a malformed policy bundle or missing image analysis.
- **Account state changes**: Proactively note when `PUT /accounts/{accountname}/state` returns 400 -- invalid state transition (e.g., trying to re-enable a deleted account).
- **Registry auth errors**: Flag 500 responses on `POST /registries` with `validate=true` -- likely credential or connectivity issues with the registry.
- **Malware content hits**: Surface non-empty results from `GET /images/{imageDigest}/content/malware` immediately, as this indicates detected malware in the image.
- **Secret search hits**: Alert on non-empty `GET /images/{imageDigest}/artifacts/secret_search` results -- secrets embedded in container images are a critical finding.
- **Bulk delete caution**: Warn before calling `DELETE /images` with `imageDigests` -- this is a bulk operation and not easily reversed.

## Playbook

### Scan a New Image and Review Results

1. Add the image: `POST /images` with `{"image": {"tag": "docker.io/library/nginx:latest"}}` and optionally `autosubscribe=true`
2. Poll image status: `GET /images/{imageDigest}` until `analysis_status` is `analyzed`
3. Check policy compliance: `GET /images/{imageDigest}/check` with `tag=docker.io/library/nginx:latest&detail=true`
4. List vulnerabilities: `GET /images/{imageDigest}/vuln/all` (use `vendor_only=true` to filter noise)
5. Review installed packages: `GET /images/{imageDigest}/content/os` for OS packages, `content/java` for Java dependencies

### Set Up a Private Registry and Watch for Updates

1. Add registry credentials: `POST /registries` with `registrydata` containing registry URL, username, password, and type; set `validate=true` to test connectivity
2. Add a repository watch: `POST /repositories` with `repository=registry.example.com/myapp` and `autosubscribe=true`
3. Verify subscription created: `GET /subscriptions` filtered by `subscription_key=registry.example.com/myapp`
4. Monitor events for new tag discoveries: `GET /events` with `event_type=tag_update` and `since` set to your start time

### Investigate a CVE Across All Images

1. Query affected images: `GET /query/images/by_vulnerability` with `vulnerability_id=CVE-2024-XXXXX`
2. Optionally narrow by severity: add `severity=Critical` or `severity=High`
3. For each affected image digest, get full vuln details: `GET /images/{imageDigest}/vuln/all`
4. Check if any affected images pass policy despite the CVE: `GET /images/{imageDigest}/check` with the appropriate tag
5. Review the vulnerability definition: `GET /query/vulnerabilities` with `id=CVE-2024-XXXXX` to see affected packages and namespaces

### Manage Accounts and User Access

1. Create a new account: `POST /accounts` with `{"account": {"name": "team-security", "type": "user"}}`
2. Add a user to the account: `POST /accounts/team-security/users` with `{"user": {"username": "analyst1", "password": "..."}}`
3. Set up user credentials: `POST /accounts/team-security/users/analyst1/credentials` with credential object
4. To disable an account later: `PUT /accounts/team-security/state` with `{"state": "disabled"}`
5. Verify account state: `GET /accounts/team-security`

### Archive and Clean Up Old Images

1. Review current archive rules: `GET /archives/rules`
2. Create an archive rule for old images: `POST /archives/rules` with transition criteria (e.g., days since analysis)
3. Manually archive specific images: `POST /archives/images` with a list of image digests
4. Verify archived images: `GET /archives/images`
5. Delete the original image to free resources: `DELETE /images/{imageDigest}` (archived copy remains accessible via `GET /archives/images/{imageDigest}`)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
