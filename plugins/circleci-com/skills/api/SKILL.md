---
name: circleci-rest-api
description: "CircleCI REST API skill. Use when working with CircleCI REST for me, projects, project. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# CircleCI REST API
API version: v1

## Auth
ApiKey circle-token in query

## Base URL
https://circleci.com/api/v1

## Setup
1. Set your API key in the appropriate header
2. GET /me -- verify access
3. POST /project/{username}/{project} -- create first project

## Endpoints

22 endpoints across 5 groups. See references/api-spec.lap for full details.

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me | Provides information about the signed in user. |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects | List of all the projects you're following on CircleCI, with build information organized by branch. |

### project
| Method | Path | Description |
|--------|------|-------------|
| GET | /project/{username}/{project} | Build summary for each of the last 30 builds for a single git repo. |
| POST | /project/{username}/{project} | Triggers a new build, returns a summary of the build. |
| GET | /project/{username}/{project}/{build_num} | Full details for a single build. The response includes all of the fields from the build summary. |
| GET | /project/{username}/{project}/{build_num}/artifacts | List the artifacts produced by a given build. |
| POST | /project/{username}/{project}/{build_num}/retry | Retries the build, returns a summary of the new build. |
| POST | /project/{username}/{project}/{build_num}/cancel | Cancels the build, returns a summary of the build. |
| GET | /project/{username}/{project}/{build_num}/tests | Provides test metadata for a build |
| POST | /project/{username}/{project}/tree/{branch} | Triggers a new build, returns a summary of the build. |
| POST | /project/{username}/{project}/ssh-key | Create an ssh key used to access external systems that require SSH key-based authentication |
| GET | /project/{username}/{project}/checkout-key | Lists checkout keys. |
| POST | /project/{username}/{project}/checkout-key | Creates a new checkout key. |
| GET | /project/{username}/{project}/checkout-key/{fingerprint} | Get a checkout key. |
| DELETE | /project/{username}/{project}/checkout-key/{fingerprint} | Delete a checkout key. |
| DELETE | /project/{username}/{project}/build-cache | Clears the cache for a project. |
| GET | /project/{username}/{project}/envvar | Lists the environment variables for :project |
| POST | /project/{username}/{project}/envvar | Creates a new environment variable |
| GET | /project/{username}/{project}/envvar/{name} | Gets the hidden value of environment variable :name |
| DELETE | /project/{username}/{project}/envvar/{name} | Deletes the environment variable named ':name' |

### recent-builds
| Method | Path | Description |
|--------|------|-------------|
| GET | /recent-builds | Build summary for each of the last 30 recent builds, ordered by build_num. |

### user
| Method | Path | Description |
|--------|------|-------------|
| POST | /user/heroku-key | Adds your Heroku API key to CircleCI, takes apikey as form param name. |

## Enhanced Skill Content
## Question Mapping

- "Who am I logged in as?" -> GET /me
- "What projects do I have access to?" -> GET /projects
- "Show me recent builds for a project" -> GET /project/{username}/{project}
- "What are my recent builds across all projects?" -> GET /recent-builds
- "Get details for a specific build" -> GET /project/{username}/{project}/{build_num}
- "What artifacts were produced by this build?" -> GET /project/{username}/{project}/{build_num}/artifacts
- "Retry a failed build" -> POST /project/{username}/{project}/{build_num}/retry
- "Cancel a running build" -> POST /project/{username}/{project}/{build_num}/cancel
- "Did any tests fail in this build?" -> GET /project/{username}/{project}/{build_num}/tests
- "Trigger a new build on a specific branch" -> POST /project/{username}/{project}/tree/{branch}
- "What environment variables are set for this project?" -> GET /project/{username}/{project}/envvar
- "Add an environment variable to a project" -> POST /project/{username}/{project}/envvar
- "Delete an environment variable from a project" -> DELETE /project/{username}/{project}/envvar/{name}
- "List checkout keys for a project" -> GET /project/{username}/{project}/checkout-key
- "Clear the build cache for a project" -> DELETE /project/{username}/{project}/build-cache

## Response Tips

- **me/user**: Flat user object; check `login` and `admin` fields for identity and permissions.
- **projects**: Returns an array of project objects; each contains `reponame`, `username`, and `vcs_url` -- use `username/reponame` as the path pair for all project endpoints.
- **builds** (project builds, recent-builds, build detail): Paginated via `limit` and `offset` query params (not link headers). Default limit is typically 30. The `status` field indicates outcome (`success`, `failed`, `running`, `canceled`, etc.).
- **artifacts**: Returns an array with `url` and `path` per artifact; `url` requires appending `?circle-token=...` to download.
- **tests**: Nested under a `tests` key; each entry has `classname`, `name`, `result` (`success`/`failure`), and `run_time`.
- **envvar**: Values are masked in GET responses (only last 4 chars shown) -- you cannot retrieve full secrets after creation.
- **checkout-key**: Includes `fingerprint`, `type`, and `preferred`; use the fingerprint for GET/DELETE of individual keys.
- **errors**: Non-200 responses return `{ "message": "..." }` -- always surface the message field to the user.

## Anomaly Flags

- **Rate limiting**: CircleCI v1 does not return explicit rate-limit headers; if you receive HTTP 429 or sudden 503 responses, surface immediately and back off.
- **Masked secrets**: When listing envvars, warn the user that values are truncated (last 4 chars only) -- they cannot recover full values from the API.
- **Deprecated API version**: This is the v1 API; CircleCI has moved to v2. Flag to the user that some endpoints may behave unexpectedly or be missing newer features.
- **Heroku key 403**: POST /user/heroku-key returns 403 when the user lacks permission -- surface this as a permissions issue, not an auth failure.
- **Build status anomalies**: If a build has status `infrastructure_fail` or `timedout`, proactively flag these as platform-side issues distinct from code failures.
- **Missing artifacts**: If a build succeeded but the artifacts endpoint returns an empty array, note that artifacts may have expired or the build config may not persist them.

## Playbook

### 1. Investigate a Failed Build

1. GET /projects to find the target project's `username` and `reponame`
2. GET /project/{username}/{project}?filter=failed&limit=5 to list recent failures
3. GET /project/{username}/{project}/{build_num} for full detail on the failure
4. GET /project/{username}/{project}/{build_num}/tests to identify which tests broke
5. GET /project/{username}/{project}/{build_num}/artifacts to retrieve any logs or output

### 2. Trigger and Monitor a Branch Build

1. POST /project/{username}/{project}/tree/{branch} with optional build parameters in the body
2. Note the `build_num` from the 201 response
3. GET /project/{username}/{project}/{build_num} to poll status until `lifecycle` is `finished`
4. If failed, POST /project/{username}/{project}/{build_num}/retry to re-run

### 3. Manage Project Environment Variables

1. GET /project/{username}/{project}/envvar to list current variables (values are masked)
2. POST /project/{username}/{project}/envvar with `{ "name": "KEY", "value": "secret" }` to add
3. GET /project/{username}/{project}/envvar/{name} to confirm creation
4. DELETE /project/{username}/{project}/envvar/{name} to remove when no longer needed

### 4. Rotate Checkout Keys

1. GET /project/{username}/{project}/checkout-key to list all current keys
2. POST /project/{username}/{project}/checkout-key with `{ "type": "deploy-key" }` to create a new key
3. DELETE /project/{username}/{project}/checkout-key/{fingerprint} to remove the old key
4. Trigger a test build to verify the new key works: POST /project/{username}/{project}/tree/main

### 5. Audit Across All Projects

1. GET /me to confirm your identity and permissions
2. GET /projects to enumerate all accessible projects
3. For each project, GET /project/{username}/{project}/envvar to audit secrets
4. For each project, GET /project/{username}/{project}/checkout-key to review key hygiene
5. GET /recent-builds?limit=100 for a cross-project health snapshot


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
