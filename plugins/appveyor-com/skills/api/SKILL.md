---
name: appveyor-rest-api
description: "AppVeyor REST API skill. Use when working with AppVeyor REST for users, user, collaborators. Covers 53 endpoints."
version: 1.0.0
generator: lapsh
---

# AppVeyor REST API
API version: 1.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://ci.appveyor.com/api

## Setup
1. Set your API key in the appropriate header
2. GET /users -- verify access
3. POST /users/invitations -- create first invitations

## Endpoints

53 endpoints across 10 groups. See references/api-spec.lap for full details.

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Get users |
| PUT | /users | Update user |
| GET | /users/{userId} | Get user |
| DELETE | /users/{userId} | Delete user |
| GET | /users/invitations | Get user invitations |
| POST | /users/invitations | Invite user |
| DELETE | /users/invitations/{userInvitationId} | Cancel user invitation |

### user
| Method | Path | Description |
|--------|------|-------------|
| PUT | /user/join-account | Join Account |

### collaborators
| Method | Path | Description |
|--------|------|-------------|
| GET | /collaborators | Get collaborators |
| PUT | /collaborators | Update collaborator |
| GET | /collaborators/{userId} | Get collaborator |
| DELETE | /collaborators/{userId} | Delete collaborator |

### roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /roles | Get roles |
| POST | /roles | Add role |
| PUT | /roles | Update role |
| GET | /roles/{roleId} | Get role |
| DELETE | /roles/{roleId} | Delete role |

### account
| Method | Path | Description |
|--------|------|-------------|
| POST | /account/encrypt | Encrypt a value for use in StoredValue. |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects | Get projects |
| POST | /projects | Add project |
| PUT | /projects | Update project |
| GET | /projects/{accountName}/{projectSlug} | Get project last build |
| DELETE | /projects/{accountName}/{projectSlug} | Delete project |
| GET | /projects/{accountName}/{projectSlug}/branch/{buildBranch} | Get project last branch build |
| GET | /projects/{accountName}/{projectSlug}/build/{buildVersion} | Get project build by version |
| GET | /projects/{accountName}/{projectSlug}/history | Get project history |
| GET | /projects/{accountName}/{projectSlug}/artifacts/{artifactFileName} | Get last successful build artifact |
| GET | /projects/{accountName}/{projectSlug}/deployments | Get project deployments |
| GET | /projects/{accountName}/{projectSlug}/settings | Get project settings |
| GET | /projects/{accountName}/{projectSlug}/settings/yaml | Get project settings in YAML |
| PUT | /projects/{accountName}/{projectSlug}/settings/yaml | Update project settings in YAML |
| PUT | /projects/{accountName}/{projectSlug}/settings/build-number | Update project build number |
| GET | /projects/{accountName}/{projectSlug}/settings/environment-variables | Get project environment variables |
| PUT | /projects/{accountName}/{projectSlug}/settings/environment-variables | Update project environment variables |
| DELETE | /projects/{accountName}/{projectSlug}/buildcache | Delete project build cache |
| GET | /projects/status/{statusBadgeId} | Get project status badge image |
| GET | /projects/status/{statusBadgeId}/branch/{buildBranch} | Get project branch status badge image |
| GET | /projects/status/{badgeRepoProvider}/{repoAccountName}/{repoSlug} | Get status badge image for a project with a public repository |

### builds
| Method | Path | Description |
|--------|------|-------------|
| POST | /builds | Start build of branch most recent commit |
| PUT | /builds | Re-run build |
| DELETE | /builds/{accountName}/{projectSlug}/{buildVersion} | Cancel build |

### buildjobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /buildjobs/{jobId}/artifacts | Get build artifacts |
| GET | /buildjobs/{jobId}/artifacts/{artifactFileName} | Download build artifact |
| GET | /buildjobs/{jobId}/log | Download build log |

### environments
| Method | Path | Description |
|--------|------|-------------|
| GET | /environments | Get environments |
| POST | /environments | Add environment |
| PUT | /environments | Update environment |
| GET | /environments/{deploymentEnvironmentId}/settings | Get environment settings |
| GET | /environments/{deploymentEnvironmentId}/deployments | Get environment deployments |
| DELETE | /environments/{deploymentEnvironmentId} | Delete environment |

### deployments
| Method | Path | Description |
|--------|------|-------------|
| GET | /deployments/{deploymentId} | Get deployment |
| POST | /deployments | Start deployment |
| PUT | /deployments/stop | Cancel deployment |

## Enhanced Skill Content
## Question Mapping

- "What projects do I have on AppVeyor?" -> GET /projects
- "Show me the latest build for my project" -> GET /projects/{accountName}/{projectSlug}
- "What's the build history for a specific branch?" -> GET /projects/{accountName}/{projectSlug}/history
- "How do I trigger a new build?" -> POST /builds
- "Cancel a running build" -> PUT /builds
- "What artifacts did a build job produce?" -> GET /buildjobs/{jobId}/artifacts
- "Download a specific artifact from a build job" -> GET /buildjobs/{jobId}/artifacts/{artifactFileName}
- "Show me the build log for a job" -> GET /buildjobs/{jobId}/log
- "What deployment environments are configured?" -> GET /environments
- "Start a new deployment" -> POST /deployments
- "Stop a running deployment" -> PUT /deployments/stop
- "What environment variables are set on my project?" -> GET /projects/{accountName}/{projectSlug}/settings/environment-variables
- "Get the status badge for my project" -> GET /projects/status/{statusBadgeId}
- "Who are the collaborators on my account?" -> GET /collaborators
- "How do I encrypt a secret value for appveyor.yml?" -> POST /account/encrypt

## Response Tips

- **Projects/Builds**: Responses nest build details inside the project object; the latest build is typically at `project.builds[0]`. History uses `recordsNumber` for page size and `startBuildId` for cursor-based pagination.
- **Build Jobs**: Artifacts return a flat array of `{fileName, size, type}`; log endpoint returns raw text, not JSON.
- **Environments/Deployments**: Environment settings include nested `deploymentEnvironment` with security-sensitive fields masked. Deployments list is nested under the environment object.
- **Users/Collaborators/Roles**: All return 204 (no body) on mutating operations (PUT/DELETE). Only GET and POST /roles return response bodies.
- **Status Badges**: Returns an image (SVG or PNG) by default, not JSON. Use `svg=true` for vector format.

## Anomaly Flags

- **204 with no body**: Many write operations return 204. If an agent expects a response body, surface that this is normal -- the operation succeeded silently.
- **Rate limiting**: AppVeyor enforces undocumented rate limits. Surface HTTP 429 responses immediately with retry-after guidance.
- **Binary responses**: Artifact downloads and badge endpoints return binary/image content, not JSON. Flag if an agent attempts to parse these as structured data.
- **Missing builds**: If `GET /projects/{accountName}/{projectSlug}` returns a project with no `builds` array or an empty one, flag that no builds have run yet.
- **Stale build cache**: After clearing build cache (DELETE .../buildcache), surface that the next build will be slower due to cold cache.
- **Encrypted values**: POST /account/encrypt returns a one-way encrypted string. Flag if an agent attempts to decrypt or reuse the plaintext.
- **Invitation expiry**: Pending user invitations may expire. Surface if listing invitations shows stale entries.

## Playbook

### 1. Trigger a Build and Monitor It

1. `GET /projects` to find the target project's `accountName` and `projectSlug`
2. `POST /builds` with body specifying `accountName`, `projectSlug`, and optionally `branch`
3. `GET /projects/{accountName}/{projectSlug}` to poll for updated build status
4. Once build completes, `GET /buildjobs/{jobId}/log` to review the log
5. `GET /buildjobs/{jobId}/artifacts` to list and download any produced artifacts

### 2. Set Up a Deployment Environment and Deploy

1. `POST /environments` with environment name, provider, and settings
2. `GET /environments` to confirm the environment was created and note the `deploymentEnvironmentId`
3. `POST /deployments` with body specifying `environmentName`, `accountName`, `projectSlug`, and `buildVersion`
4. `GET /deployments/{deploymentId}` to monitor deployment progress
5. If needed, `PUT /deployments/stop` with the deployment ID to cancel

### 3. Manage Project Environment Variables

1. `GET /projects/{accountName}/{projectSlug}/settings/environment-variables` to list current variables
2. For secrets, `POST /account/encrypt` with the plaintext value to get an encrypted string
3. `PUT /projects/{accountName}/{projectSlug}/settings/environment-variables` with the full array of variables (including encrypted values)
4. Verify by re-fetching with the GET endpoint

### 4. Add a Collaborator with a Custom Role

1. `POST /roles` with the role name and permissions to create a custom role
2. `GET /roles` to confirm and note the `roleId`
3. `POST /users/invitations` with the collaborator's email and the assigned `roleId`
4. `GET /users/invitations` to verify the invitation is pending
5. Once accepted, `GET /collaborators` to confirm the user appears

### 5. Review Build History and Diagnose Failures

1. `GET /projects/{accountName}/{projectSlug}/history` with `recordsNumber=10` to fetch recent builds
2. Identify failed builds from the response and note their `buildId` and `jobs` array
3. `GET /buildjobs/{jobId}/log` for each failed job to read error output
4. `GET /buildjobs/{jobId}/artifacts` to check if partial artifacts were produced
5. Optionally `DELETE /builds/{accountName}/{projectSlug}/{buildVersion}` to clean up broken build records


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
