---
name: render-public-api
description: "Render Public API skill. Use when working with Render Public for blueprints, owners, disks. Covers 196 endpoints."
version: 1.0.0
generator: lapsh
---

# Render Public API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.render.com/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /blueprints -- verify access
3. POST /blueprints/validate -- create first validate

## Endpoints

196 endpoints across 25 groups. See references/api-spec.lap for full details.

### blueprints
| Method | Path | Description |
|--------|------|-------------|
| GET | /blueprints | List Blueprints |
| POST | /blueprints/validate | Validate Blueprint |
| GET | /blueprints/{blueprintId} | Retrieve Blueprint |
| PATCH | /blueprints/{blueprintId} | Update Blueprint |
| DELETE | /blueprints/{blueprintId} | Disconnect Blueprint |
| GET | /blueprints/{blueprintId}/syncs | List Blueprint syncs |

### owners
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /owners/{ownerId}/members/{userId} | Update workspace member role |
| DELETE | /owners/{ownerId}/members/{userId} | Remove workspace member |
| GET | /owners | List workspaces |
| GET | /owners/{ownerId} | Retrieve workspace |
| GET | /owners/{ownerId}/members | List workspace members |
| GET | /owners/{ownerId}/audit-logs | List workspace audit logs |

### disks
| Method | Path | Description |
|--------|------|-------------|
| GET | /disks | List disks |
| POST | /disks | Add disk |
| GET | /disks/{diskId} | Retrieve disk |
| PATCH | /disks/{diskId} | Update disk |
| DELETE | /disks/{diskId} | Delete disk |
| GET | /disks/{diskId}/snapshots | List snapshots |
| POST | /disks/{diskId}/snapshots/restore | Restore snapshot |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Get the authenticated user |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations/{orgId}/audit-logs | List organization audit logs |

### notification-settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification-settings/owners/{ownerId} | Retrieve notification settings |
| PATCH | /notification-settings/owners/{ownerId} | Update notification settings |
| GET | /notification-settings/overrides | List notification overrides |
| GET | /notification-settings/overrides/services/{serviceId} | Retrieve notification override |
| PATCH | /notification-settings/overrides/services/{serviceId} | Update notification override |

### registrycredentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /registrycredentials | List registry credentials |
| POST | /registrycredentials | Create registry credential |
| GET | /registrycredentials/{registryCredentialId} | Retrieve registry credential |
| PATCH | /registrycredentials/{registryCredentialId} | Update registry credential |
| DELETE | /registrycredentials/{registryCredentialId} | Delete registry credential |

### services
| Method | Path | Description |
|--------|------|-------------|
| GET | /services | List services |
| POST | /services | Create service |
| GET | /services/{serviceId} | Retrieve service |
| PATCH | /services/{serviceId} | Update service |
| DELETE | /services/{serviceId} | Delete service |
| POST | /services/{serviceId}/cache/purge | Purge Web Service Cache |
| GET | /services/{serviceId}/deploys | List deploys |
| POST | /services/{serviceId}/deploys | Trigger deploy |
| GET | /services/{serviceId}/deploys/{deployId} | Retrieve deploy |
| POST | /services/{serviceId}/deploys/{deployId}/cancel | Cancel deploy |
| POST | /services/{serviceId}/rollback | Roll back deploy |
| GET | /services/{serviceId}/env-vars | List environment variables |
| PUT | /services/{serviceId}/env-vars | Update environment variables |
| GET | /services/{serviceId}/env-vars/{envVarKey} | Retrieve environment variable |
| PUT | /services/{serviceId}/env-vars/{envVarKey} | Add or update environment variable |
| DELETE | /services/{serviceId}/env-vars/{envVarKey} | Delete environment variable |
| GET | /services/{serviceId}/secret-files | List secret files |
| PUT | /services/{serviceId}/secret-files | Update secret files |
| GET | /services/{serviceId}/secret-files/{secretFileName} | Retrieve secret file |
| PUT | /services/{serviceId}/secret-files/{secretFileName} | Add or update secret file |
| DELETE | /services/{serviceId}/secret-files/{secretFileName} | Delete secret file |
| GET | /services/{serviceId}/events | List events |
| GET | /services/{serviceId}/headers | List header rules |
| POST | /services/{serviceId}/headers | Add header rule |
| PUT | /services/{serviceId}/headers | Replace header rules |
| DELETE | /services/{serviceId}/headers/{headerId} | Delete header rule |
| GET | /services/{serviceId}/routes | List redirect/rewrite rules |
| POST | /services/{serviceId}/routes | Add redirect/rewrite rules |
| PATCH | /services/{serviceId}/routes | Update redirect/rewrite rule priority |
| PUT | /services/{serviceId}/routes | Update redirect/rewrite rules |
| DELETE | /services/{serviceId}/routes/{routeId} | Delete redirect/rewrite rule |
| GET | /services/{serviceId}/custom-domains | List custom domains |
| POST | /services/{serviceId}/custom-domains | Add custom domain |
| GET | /services/{serviceId}/custom-domains/{customDomainIdOrName} | Retrieve custom domain |
| DELETE | /services/{serviceId}/custom-domains/{customDomainIdOrName} | Delete custom domain |
| POST | /services/{serviceId}/custom-domains/{customDomainIdOrName}/verify | Verify DNS configuration |
| POST | /services/{serviceId}/suspend | Suspend service |
| POST | /services/{serviceId}/resume | Resume service |
| POST | /services/{serviceId}/restart | Restart service |
| POST | /services/{serviceId}/scale | Scale instance count |
| PUT | /services/{serviceId}/autoscaling | Update autoscaling config |
| DELETE | /services/{serviceId}/autoscaling | Delete autoscaling config |
| POST | /services/{serviceId}/preview | Create service preview (image-backed) |
| GET | /services/{serviceId}/jobs | List jobs |
| POST | /services/{serviceId}/jobs | Create job |
| GET | /services/{serviceId}/jobs/{jobId} | Retrieve job |
| POST | /services/{serviceId}/jobs/{jobId}/cancel | Cancel running job |
| GET | /services/{serviceId}/instances | List instances |

### cron-jobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /cron-jobs/{cronJobId}/runs | Trigger cron job run |
| DELETE | /cron-jobs/{cronJobId}/runs | Cancel running cron job |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events/{eventId} | Retrieve event |

### logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /logs | List logs |
| GET | /logs/subscribe | Subscribe to new logs |
| GET | /logs/values | List log label values |
| GET | /logs/streams/owner/{ownerId} | Retrieve log stream |
| PUT | /logs/streams/owner/{ownerId} | Update log stream |
| DELETE | /logs/streams/owner/{ownerId} | Delete log stream |
| GET | /logs/streams/resource | List log stream overrides |
| GET | /logs/streams/resource/{resourceId} | Retrieve log stream override |
| PUT | /logs/streams/resource/{resourceId} | Update log stream override |
| DELETE | /logs/streams/resource/{resourceId} | Delete log stream override |

### metrics-stream
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics-stream/{ownerId} | Retrieve metrics stream |
| PUT | /metrics-stream/{ownerId} | Create or update metrics stream |
| DELETE | /metrics-stream/{ownerId} | Delete metrics stream |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics/cpu | Get CPU usage |
| GET | /metrics/cpu-limit | Get CPU limit |
| GET | /metrics/cpu-target | Get CPU target |
| GET | /metrics/memory | Get memory usage |
| GET | /metrics/memory-limit | Get memory limit |
| GET | /metrics/memory-target | Get memory target |
| GET | /metrics/http-requests | Get HTTP request count |
| GET | /metrics/http-latency | Get HTTP latency |
| GET | /metrics/bandwidth | Get bandwidth usage |
| GET | /metrics/bandwidth-sources | Get bandwidth usage breakdown by traffic source |
| GET | /metrics/disk-usage | Get disk usage |
| GET | /metrics/disk-capacity | Get disk capacity |
| GET | /metrics/instance-count | Get instance count |
| GET | /metrics/active-connections | Get active connection count |
| GET | /metrics/replication-lag | Get replica lag |
| GET | /metrics/filters/application | List queryable instance values |
| GET | /metrics/filters/http | List queryable status codes and host values |
| GET | /metrics/filters/path | List queryable paths |
| GET | /metrics/task-runs-queued | Get task runs queued count |
| GET | /metrics/task-runs-completed | Get task runs completed count |

### key-value
| Method | Path | Description |
|--------|------|-------------|
| GET | /key-value | List Key Value instances |
| POST | /key-value | Create Key Value instance |
| GET | /key-value/{keyValueId} | Retrieve Key Value instance |
| PATCH | /key-value/{keyValueId} | Update Key Value instance |
| DELETE | /key-value/{keyValueId} | Delete Key Value instance |
| GET | /key-value/{keyValueId}/connection-info | Retrieve Key Value connection info |
| POST | /key-value/{keyValueId}/suspend | Suspend Key Value instance |
| POST | /key-value/{keyValueId}/resume | Resume Key Value instance |

### redis
| Method | Path | Description |
|--------|------|-------------|
| GET | /redis | List Redis instances |
| POST | /redis | Create Redis instance |
| GET | /redis/{redisId} | Retrieve Redis instance |
| PATCH | /redis/{redisId} | Update Redis instance |
| DELETE | /redis/{redisId} | Delete Redis instance |
| GET | /redis/{redisId}/connection-info | Retrieve Redis connection info |

### postgres
| Method | Path | Description |
|--------|------|-------------|
| GET | /postgres | List Postgres instances |
| POST | /postgres | Create Postgres instance |
| GET | /postgres/{postgresId} | Retrieve Postgres instance |
| PATCH | /postgres/{postgresId} | Update Postgres instance |
| DELETE | /postgres/{postgresId} | Delete Postgres instance |
| GET | /postgres/{postgresId}/connection-info | Retrieve Postgres connection info |
| GET | /postgres/{postgresId}/recovery | Retrieve point-in-time recovery status |
| POST | /postgres/{postgresId}/recovery | Trigger point-in-time recovery |
| POST | /postgres/{postgresId}/suspend | Suspend Postgres instance |
| POST | /postgres/{postgresId}/resume | Resume Postgres instance |
| POST | /postgres/{postgresId}/restart | Restart Postgres instance |
| POST | /postgres/{postgresId}/failover | Failover Postgres instance |
| GET | /postgres/{postgresId}/export | List Postgres exports |
| POST | /postgres/{postgresId}/export | Create Postgres export |
| GET | /postgres/{postgresId}/credentials | List PostgreSQL Users |
| POST | /postgres/{postgresId}/credentials | Create PostgreSQL User |
| DELETE | /postgres/{postgresId}/credentials/{username} | Delete PostgreSQL User |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects | List projects |
| POST | /projects | Create project |
| GET | /projects/{projectId} | Retrieve Project |
| PATCH | /projects/{projectId} | Update project |
| DELETE | /projects/{projectId} | Delete project |

### environments
| Method | Path | Description |
|--------|------|-------------|
| POST | /environments | Create environment |
| GET | /environments | List environments |
| GET | /environments/{environmentId} | Retrieve environment |
| PATCH | /environments/{environmentId} | Update environment |
| DELETE | /environments/{environmentId} | Delete environment |
| POST | /environments/{environmentId}/resources | Add resources to environment |
| DELETE | /environments/{environmentId}/resources | Remove resources from environment |

### env-groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /env-groups | List environment groups |
| POST | /env-groups | Create environment group |
| GET | /env-groups/{envGroupId} | Retrieve environment group |
| PATCH | /env-groups/{envGroupId} | Update environment group |
| DELETE | /env-groups/{envGroupId} | Delete environment group |
| POST | /env-groups/{envGroupId}/services/{serviceId} | Link service |
| DELETE | /env-groups/{envGroupId}/services/{serviceId} | Unlink service |
| GET | /env-groups/{envGroupId}/env-vars/{envVarKey} | Retrieve environment variable |
| PUT | /env-groups/{envGroupId}/env-vars/{envVarKey} | Add or update environment variable |
| DELETE | /env-groups/{envGroupId}/env-vars/{envVarKey} | Remove environment variable |
| GET | /env-groups/{envGroupId}/secret-files/{secretFileName} | Retrieve secret file |
| PUT | /env-groups/{envGroupId}/secret-files/{secretFileName} | Add or update secret file |
| DELETE | /env-groups/{envGroupId}/secret-files/{secretFileName} | Remove secret file |

### maintenance
| Method | Path | Description |
|--------|------|-------------|
| GET | /maintenance | List maintenance runs |
| GET | /maintenance/{maintenanceRunParam} | Retrieve maintenance run |
| PATCH | /maintenance/{maintenanceRunParam} | Update maintenance run |
| POST | /maintenance/{maintenanceRunParam}/trigger | Trigger maintenance run |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhooks | Create a webhook |
| GET | /webhooks | List webhooks |
| GET | /webhooks/{webhookId} | Retrieve a webhook |
| PATCH | /webhooks/{webhookId} | Update a webhook |
| DELETE | /webhooks/{webhookId} | Delete a webhook |
| GET | /webhooks/{webhookId}/events | List webhook events |

### workflows
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflows | List workflows |
| POST | /workflows | Create a workflow |
| GET | /workflows/{workflowId} | Retrieve workflow |
| PATCH | /workflows/{workflowId} | Update workflow |
| DELETE | /workflows/{workflowId} | Delete workflow |

### workflowversions
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflowversions | List workflow versions |
| POST | /workflowversions | Deploy a workflow version |
| GET | /workflowversions/{workflowVersionId} | Retrieve workflow version |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| GET | /tasks | List tasks |
| GET | /tasks/{taskId} | Retrieve task |

### task-runs
| Method | Path | Description |
|--------|------|-------------|
| GET | /task-runs | List task runs |
| POST | /task-runs | Run task |
| GET | /task-runs/events | Stream realtime events (SSE) |
| GET | /task-runs/{taskRunId} | Retrieve task run |
| DELETE | /task-runs/{taskRunId} | Cancel task run |

## Enhanced Skill Content
## Question Mapping

- "What services do I have running?" -> GET /services
- "How do I deploy my service?" -> POST /services/{serviceId}/deploys
- "What's the status of my latest deploy?" -> GET /services/{serviceId}/deploys
- "How do I roll back to a previous deployment?" -> POST /services/{serviceId}/rollback
- "Can I see the logs for my service?" -> GET /logs
- "How do I add an environment variable to my service?" -> PUT /services/{serviceId}/env-vars/{envVarKey}
- "What databases do I have and what are their connection strings?" -> GET /postgres then GET /postgres/{postgresId}/connection-info
- "How do I scale my service to more instances?" -> POST /services/{serviceId}/scale
- "How do I set up autoscaling for my service?" -> PUT /services/{serviceId}/autoscaling
- "How do I add a custom domain to my service?" -> POST /services/{serviceId}/custom-domains
- "What's my current CPU and memory usage?" -> GET /metrics/cpu and GET /metrics/memory
- "How do I suspend a service to stop billing?" -> POST /services/{serviceId}/suspend
- "How do I restore a Postgres database to a point in time?" -> POST /postgres/{postgresId}/recovery
- "Who are the members of my team and what roles do they have?" -> GET /owners/{ownerId}/members
- "How do I create a new Redis instance?" -> POST /redis

## Response Tips

- **List endpoints** (services, postgres, redis, disks, blueprints, projects, env-groups, webhooks, workflows, tasks, task-runs): All use cursor-based pagination with `cursor` and `limit` (default 20). Check for a `cursor` field in the response to fetch the next page; stop when absent.
- **Service details**: The `serviceDetails` field is polymorphic (`any`) -- its shape depends on `type` (static_site, web_service, private_service, background_worker, cron_job). Inspect the service `type` before parsing.
- **Deploy responses**: POST to create a deploy may return either 201 (immediate) or 202 (accepted/queued). Poll GET /services/{serviceId}/deploys/{deployId} for final status.
- **Connection info** (postgres, redis, key-value): Strings marked `(password)` contain secrets. Never log or display these without masking.
- **Suspend/resume/restart/scale/failover**: Return 202 (accepted), meaning the operation is asynchronous. Poll the resource's GET endpoint to confirm completion.
- **Delete endpoints**: Always return 204 with no body. A successful delete has no content to parse.
- **Logs**: Response includes `hasMore`, `nextStartTime`, and `nextEndTime` for time-based pagination, not cursor-based.
- **Metrics endpoints**: Return time-series data with minimal error codes (400, 500 only). Pass resource filters via query parameters.

## Anomaly Flags

- **429 Too Many Requests**: Nearly every endpoint can return 429. Surface this immediately with retry-after guidance; back off exponentially.
- **402 Payment Required**: Returned by POST /services, POST /registrycredentials, POST /services/{serviceId}/custom-domains, and PATCH /registrycredentials. Indicates plan limits reached -- alert the user about billing.
- **410 Gone**: Many endpoints return this. The resource was permanently deleted; stop retrying and inform the user the resource no longer exists.
- **Service suspended unexpectedly**: If GET /services/{serviceId} returns `suspended: "suspended"`, proactively surface this with the `suspenders` array to explain why.
- **Postgres expiration approaching**: The `expiresAt` field on free-tier Postgres instances. Alert when expiration is within 7 days.
- **Pending maintenance**: Redis, key-value, and Postgres responses include `maintenance.pendingMaintenanceBy`. Surface when a maintenance window is imminent.
- **Deploy failures**: When polling deploys, surface `status` changes to failed states immediately rather than waiting for the user to ask.
- **Disk usage near capacity**: Compare GET /metrics/disk-usage against GET /metrics/disk-capacity and warn when usage exceeds 85%.
- **High availability disabled on production Postgres**: Flag when `highAvailabilityEnabled: false` on a non-free plan database.
- **Autoscaling hitting max**: If instance count from GET /metrics/instance-count equals the `max` from autoscaling config, warn about potential capacity ceiling.

## Playbook

### 1. Deploy a New Web Service from a Git Repo

1. GET /owners to find your `ownerId`
2. POST /services with `type: "web_service"`, `name`, `ownerId`, `repo`, and `branch`
3. Note the `deployId` from the response
4. Poll GET /services/{serviceId}/deploys/{deployId} until `status` is `live` or `failed`
5. GET /services/{serviceId}/custom-domains to verify the default URL is active
6. Optionally POST /services/{serviceId}/custom-domains to attach a custom domain

### 2. Set Up a Postgres Database with Environment Variables

1. GET /owners to find your `ownerId`
2. POST /postgres with `name`, `ownerId`, `plan`, and `version`
3. GET /postgres/{postgresId}/connection-info to retrieve the connection string
4. PUT /services/{serviceId}/env-vars/DATABASE_URL with the `internalConnectionString` value
5. POST /services/{serviceId}/deploys to redeploy the service with the new variable
6. Verify by polling GET /services/{serviceId}/deploys/{deployId} until status is `live`

### 3. Roll Back a Failed Deployment

1. GET /services/{serviceId}/deploys to list recent deploys and identify the last successful `deployId`
2. POST /services/{serviceId}/rollback with the target `deployId`
3. Poll GET /services/{serviceId}/deploys/{deployId} (the new rollback deploy) until `status` is `live`
4. GET /services/{serviceId} to confirm the service is running the rolled-back version
5. Check GET /logs with the service's `resource` ID to verify healthy application output

### 4. Configure Autoscaling with Monitoring

1. GET /services/{serviceId} to confirm the service type supports scaling
2. PUT /services/{serviceId}/autoscaling with `enabled: true`, `min`, `max`, and CPU/memory thresholds
3. GET /metrics/cpu and GET /metrics/memory to establish baseline usage
4. GET /metrics/instance-count periodically to verify scaling behavior
5. Set up a webhook via POST /webhooks with relevant event filters to get notified of scaling events

### 5. Manage Shared Environment Variables Across Services

1. POST /env-groups with `name`, `ownerId`, and `envVars` array containing shared variables
2. POST /env-groups/{envGroupId}/services/{serviceId} for each service that needs these variables
3. To update a single variable: PUT /env-groups/{envGroupId}/env-vars/{envVarKey}
4. Linked services redeploy automatically if `autoDeploy` is enabled; otherwise trigger POST /services/{serviceId}/deploys for each
5. To remove a service from the group: DELETE /env-groups/{envGroupId}/services/{serviceId}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
