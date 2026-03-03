---
name: snyk-api
description: "Snyk API skill. Use when working with Snyk for user, group, orgs. Covers 100 endpoints."
version: 1.0.0
generator: lapsh
---

# Snyk API
API version: 1.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.snyk.io/v1

## Setup
1. Set your API key in the appropriate header
2. GET /user/me -- verify access
3. POST /group/{groupId}/org/{orgId}/members -- create first members

## Endpoints

100 endpoints across 7 groups. See references/api-spec.lap for full details.

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user/{userId} | Get User Details |
| GET | /user/me | Get My Details |
| GET | /user/me/notification-settings/org/{orgId} | Get organization notification settings |
| PUT | /user/me/notification-settings/org/{orgId} | Modify organization notification settings |
| GET | /user/me/notification-settings/org/{orgId}/project/{projectId} | Get project notification settings |
| PUT | /user/me/notification-settings/org/{orgId}/project/{projectId} | Modify project notification settings |

### group
| Method | Path | Description |
|--------|------|-------------|
| GET | /group/{groupId}/settings | View group settings |
| PUT | /group/{groupId}/settings | Update group settings |
| GET | /group/{groupId}/members | List all members in a group |
| POST | /group/{groupId}/org/{orgId}/members | Add a member to an organization within a group |
| GET | /group/{groupId}/tags | List all tags in a group |
| POST | /group/{groupId}/tags/delete | Delete tag from group |
| GET | /group/{groupId}/orgs | List all organizations in a group |
| GET | /group/{groupId}/roles | List all roles in a group |

### orgs
| Method | Path | Description |
|--------|------|-------------|
| GET | /orgs | List all the organizations a user belongs to |

### org
| Method | Path | Description |
|--------|------|-------------|
| POST | /org | Create a new organization |
| GET | /org/{orgId}/notification-settings | Get organization notification settings |
| PUT | /org/{orgId}/notification-settings | Set notification settings |
| POST | /org/{orgId}/invite | Invite users |
| GET | /org/{orgId}/members | List Members |
| GET | /org/{orgId}/settings | View organization settings |
| PUT | /org/{orgId}/settings | Update organization settings |
| PUT | /org/{orgId}/members/{userId} | Update a member in the organization |
| DELETE | /org/{orgId}/members/{userId} | Remove a member from the organization |
| PUT | /org/{orgId}/members/update/{userId} | Update a member's role in the organization |
| DELETE | /org/{orgId} | Remove organization |
| POST | /org/{orgId}/provision | Provision a user to the organization |
| GET | /org/{orgId}/provision | List pending user provisions |
| DELETE | /org/{orgId}/provision | Delete pending user provision |
| GET | /org/{orgId}/integrations | List |
| POST | /org/{orgId}/integrations | Add new integration |
| PUT | /org/{orgId}/integrations/{integrationId} | Update existing integration |
| DELETE | /org/{orgId}/integrations/{integrationId}/authentication | Delete credentials |
| POST | /org/{orgId}/integrations/{integrationId}/authentication/provision-token | Provision new broker token |
| POST | /org/{orgId}/integrations/{integrationId}/authentication/switch-token | Switch between broker tokens |
| POST | /org/{orgId}/integrations/{integrationId}/clone | Clone an integration (with settings and credentials) |
| GET | /org/{orgId}/integrations/{type} | Get existing integration by type |
| GET | /org/{orgId}/integrations/{integrationId}/settings | Get Integration Settings |
| PUT | /org/{orgId}/integrations/{integrationId}/settings | Update Integration Settings |
| POST | /org/{orgId}/integrations/{integrationId}/import | Import targets |
| GET | /org/{orgId}/integrations/{integrationId}/import/{jobId} | Get import job details |
| GET | /org/{orgId}/project/{projectId} | Retrieve a single project |
| PUT | /org/{orgId}/project/{projectId} | Update a project |
| DELETE | /org/{orgId}/project/{projectId} | Delete a project |
| POST | /org/{orgId}/project/{projectId}/deactivate | Deactivate a project |
| POST | /org/{orgId}/project/{projectId}/activate | Activate a project |
| POST | /org/{orgId}/project/{projectId}/aggregated-issues | List all Aggregated issues |
| GET | /org/{orgId}/project/{projectId}/issue/{issueId}/paths | List all project issue paths |
| POST | /org/{orgId}/project/{projectId}/history | List all project snapshots |
| POST | /org/{orgId}/project/{projectId}/history/{snapshotId}/aggregated-issues | List all project snapshot aggregated issues |
| GET | /org/{orgId}/project/{projectId}/history/{snapshotId}/issue/{issueId}/paths | List all project snapshot issue paths |
| GET | /org/{orgId}/project/{projectId}/dep-graph | Get Project dependency graph |
| GET | /org/{orgId}/project/{projectId}/ignores | List all ignores |
| GET | /org/{orgId}/project/{projectId}/ignore/{issueId} | Retrieve ignore |
| POST | /org/{orgId}/project/{projectId}/ignore/{issueId} | Add ignore |
| PUT | /org/{orgId}/project/{projectId}/ignore/{issueId} | Replace ignores |
| DELETE | /org/{orgId}/project/{projectId}/ignore/{issueId} | Delete ignores |
| GET | /org/{orgId}/project/{projectId}/jira-issues | List all jira issues |
| POST | /org/{orgId}/project/{projectId}/issue/{issueId}/jira-issue | Create jira issue |
| GET | /org/{orgId}/project/{projectId}/settings | List project settings |
| PUT | /org/{orgId}/project/{projectId}/settings | Update project settings |
| DELETE | /org/{orgId}/project/{projectId}/settings | Delete project settings |
| PUT | /org/{orgId}/project/{projectId}/move | Move project to a different organization |
| POST | /org/{orgId}/project/{projectId}/tags | Add a tag to a project |
| POST | /org/{orgId}/project/{projectId}/tags/remove | Remove a tag from a project |
| POST | /org/{orgId}/project/{projectId}/attributes | Applying attributes |
| POST | /org/{orgId}/dependencies | List all dependencies |
| POST | /org/{orgId}/licenses | List all licenses |
| GET | /org/{orgId}/entitlements | List all entitlements |
| GET | /org/{orgId}/entitlement/{entitlementKey} | Get an organization's entitlement value |
| POST | /org/{orgId}/webhooks | Create a webhook |
| GET | /org/{orgId}/webhooks | List webhooks |
| GET | /org/{orgId}/webhooks/{webhookId} | Retrieve a webhook |
| DELETE | /org/{orgId}/webhooks/{webhookId} | Delete a webhook |
| POST | /org/{orgId}/webhooks/{webhookId}/ping | Ping a webhook |

### test
| Method | Path | Description |
|--------|------|-------------|
| GET | /test/maven/{groupId}/{artifactId}/{version} | Test for issues in a public package by group id, artifact id and version |
| POST | /test/maven | Test maven file |
| GET | /test/npm/{packageName}/{version} | Test for issues in a public package by name and version |
| POST | /test/npm | Test package.json & package-lock.json File |
| POST | /test/golangdep | Test Gopkg.toml & Gopkg.lock File |
| POST | /test/govendor | Test vendor.json File |
| POST | /test/yarn | Test package.json & yarn.lock File |
| GET | /test/rubygems/{gemName}/{version} | Test for issues in a public gem by name and version |
| POST | /test/rubygems | Test gemfile.lock file |
| GET | /test/gradle/{group}/{name}/{version} | Test for issues in a public package by group, name and version |
| POST | /test/gradle | Test gradle file |
| GET | /test/sbt/{groupId}/{artifactId}/{version} | sbt_Test for issues in a public package by group id, artifact id and version |
| POST | /test/sbt | Test sbt file |
| GET | /test/pip/{packageName}/{version} | pip_Test for issues in a public package by name and version |
| POST | /test/pip | Test requirements.txt file |
| POST | /test/composer | Test composer.json & composer.lock file |
| POST | /test/dep-graph | Test Dep Graph |

### monitor
| Method | Path | Description |
|--------|------|-------------|
| POST | /monitor/dep-graph | Monitor Dep Graph |

### reporting
| Method | Path | Description |
|--------|------|-------------|
| POST | /reporting/issues/latest | Get list of latest issues |
| POST | /reporting/issues | Get list of issues |
| POST | /reporting/counts/issues/latest | Get latest issue counts |
| POST | /reporting/counts/issues | Get issue counts |
| POST | /reporting/counts/projects/latest | Get latest project counts |
| POST | /reporting/counts/projects | Get project counts |
| POST | /reporting/counts/tests | Get test counts |

## Enhanced Skill Content
## Question Mapping

- "Who am I authenticated as?" -> GET /user/me
- "Get details about a specific user?" -> GET /user/{userId}
- "What organizations do I belong to?" -> GET /orgs
- "List all members in my organization?" -> GET /org/{orgId}/members
- "What integrations are configured for my org?" -> GET /org/{orgId}/integrations
- "Show me the vulnerability issues for a project?" -> POST /org/{orgId}/project/{projectId}/aggregated-issues
- "What does the dependency graph look like for a project?" -> GET /org/{orgId}/project/{projectId}/dep-graph
- "Test an npm package for vulnerabilities?" -> POST /test/npm
- "How many issues do we have right now?" -> POST /reporting/counts/issues/latest
- "Ignore a specific vulnerability in a project?" -> POST /org/{orgId}/project/{projectId}/ignore/{issueId}
- "Invite someone to my organization?" -> POST /org/{orgId}/invite
- "Move a project to a different organization?" -> PUT /org/{orgId}/project/{projectId}/move
- "What are the notification settings for my org?" -> GET /user/me/notification-settings/org/{orgId}
- "List all projects' issues over a date range?" -> POST /reporting/issues
- "Create a Jira ticket for a vulnerability?" -> POST /org/{orgId}/project/{projectId}/issue/{issueId}/jira-issue

## Response Tips

- **User endpoints**: Flat object responses; `/user/me` returns the authenticated user profile directly.
- **Group endpoints**: `members`, `tags`, and `orgs` listings support `perPage`/`page` query params for manual pagination -- always check if more pages exist.
- **Org endpoints**: Nested maps are common (`issueCountsBySeverity`, `owner`, `importingUser`); project responses include image metadata fields that may be null for non-container projects.
- **Test endpoints**: Responses contain `ok` boolean, `issues.vulnerabilities` array, and `dependencyCount`; a `200` with `ok: false` means vulnerabilities were found (not an error).
- **Reporting endpoints**: Return `results` array with `total` count; support `page`/`perPage` for pagination and `sortBy`/`order`/`groupBy` for shaping output. 400 errors indicate malformed filter or date params.
- **Integration endpoints**: Settings responses have many boolean flags for PR behavior; unchanged fields are still returned in full on PUT.
- **Ignore endpoints**: Returns a nested `ignorePath` map with `reason`, `reasonType`, `ignoredBy` (user object), and `expires` -- check `disregardIfFixable` to understand auto-unignore behavior.

## Anomaly Flags

- **401 on any endpoint**: API key is invalid, expired, or missing -- surface immediately and halt further calls.
- **403 on org operations**: The authenticated user lacks permissions for that org; flag the role mismatch (common on `/provision`, `/settings` PUT, integration auth endpoints).
- **Test result with `ok: true` but non-empty vulnerabilities array**: Inconsistent state -- flag for manual review.
- **`disregardIfFixable: true` on ignores**: Alert the user that this ignore will auto-expire when a fix becomes available.
- **`expires` field on ignores approaching current date**: Proactively warn that an ignore is about to lapse.
- **`isMonitored: false` on a project**: Flag that this project is not being actively scanned -- may be a gap in coverage.
- **`readOnly: true` on a project**: Surface before any write attempts to avoid confusing 403s.
- **Large `totalDependencies` count (>500)**: May indicate a bloated dependency tree worth investigating.
- **Import job `status` not `complete`**: Poll `/import/{jobId}` and alert if stuck in pending state.
- **422 on org creation**: Signals validation failure (duplicate name, invalid plan) -- surface the response body for details.

## Playbook

### Audit an Organization's Vulnerability Posture

1. Call `GET /orgs` to list all accessible organizations
2. For each org, call `POST /reporting/counts/issues/latest` to get current issue counts
3. Drill into high-count orgs with `POST /reporting/issues/latest` using `sortBy: "severity"` and `order: "desc"`
4. For critical issues, call `GET /org/{orgId}/project/{projectId}/issue/{issueId}/paths` to understand the dependency path
5. Summarize findings by org, severity, and exploitability

### Onboard a New Team Member

1. Call `GET /user/me` to confirm your admin identity
2. Call `POST /org/{orgId}/invite` with the new member's email
3. Optionally call `POST /org/{orgId}/provision` with `email` and `role` to pre-assign permissions
4. Call `GET /org/{orgId}/members` to verify the member appears in the list
5. Call `PUT /user/me/notification-settings/org/{orgId}` to configure their notification preferences

### Set Up a New Integration and Import Projects

1. Call `GET /org/{orgId}/integrations` to see existing integrations
2. Call `POST /org/{orgId}/integrations` with credentials to create a new integration
3. Call `PUT /org/{orgId}/integrations/{integrationId}/settings` to configure PR test behavior (`pullRequestTestEnabled`, `autoRemediationPrs`, etc.)
4. Call `POST /org/{orgId}/integrations/{integrationId}/import` to kick off project import
5. Poll `GET /org/{orgId}/integrations/{integrationId}/import/{jobId}` until `status` is `complete`, checking `logs` for errors

### Triage and Ignore a Known False Positive

1. Call `POST /org/{orgId}/project/{projectId}/aggregated-issues` to list current issues
2. Identify the false positive issue and note its `issueId`
3. Call `POST /org/{orgId}/project/{projectId}/ignore/{issueId}` with `reasonType: "not-vulnerable"`, `reason: "confirmed false positive"`, and `disregardIfFixable: false`
4. Call `GET /org/{orgId}/project/{projectId}/ignore/{issueId}` to verify the ignore was applied
5. Optionally call `POST /org/{orgId}/project/{projectId}/issue/{issueId}/jira-issue` to create a tracking ticket

### Generate a Time-Bound Security Report

1. Call `POST /reporting/issues` with `from` and `to` date range, `perPage: 100`, `page: 1`
2. Paginate through all results by incrementing `page` until results count < `perPage`
3. Call `POST /reporting/counts/issues` with the same date range and `groupBy: "severity"` for summary stats
4. Call `POST /reporting/counts/projects` with the same range to get project-level counts
5. Call `POST /reporting/counts/tests` with `groupBy: "isPrivate"` to show test activity breakdown


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
