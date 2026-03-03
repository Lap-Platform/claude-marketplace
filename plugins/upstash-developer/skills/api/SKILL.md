---
name: developer-api-upstash
description: "Developer API - Upstash API skill. Use when working with Developer API - Upstash for redis, teams, auditlogs. Covers 52 endpoints."
version: 1.0.0
generator: lapsh
---

# Developer API - Upstash
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://api.upstash.com/v2

## Setup
1. Set Authorization header with your Bearer token
2. GET /redis/databases -- verify access
3. POST /redis/database -- create first database

## Endpoints

52 endpoints across 8 groups. See references/api-spec.lap for full details.

### redis
| Method | Path | Description |
|--------|------|-------------|
| GET | /redis/databases | List Databases |
| GET | /redis/database/{id} | Get Database |
| DELETE | /redis/database/{id} | Delete Database |
| POST | /redis/database | Create Redis Database |
| POST | /redis/rename/{id} | Rename Database |
| POST | /redis/reset-password/{id} | Reset Password |
| POST | /redis/enable-tls/{id} | Enable TLS |
| POST | /redis/enable-eviction/{id} | Enable Eviction |
| POST | /redis/disable-eviction/{id} | Disable Eviction |
| POST | /redis/enable-autoupgrade/{id} | Enable Auto Upgrade |
| POST | /redis/disable-autoupgrade/{id} | Disable Auto Upgrade |
| POST | /redis/change-plan/{id} | Change Database Plan |
| PATCH | /redis/update-budget/{id} | Update Database Budget |
| POST | /redis/update-regions/{id} | Update Regions |
| POST | /redis/move-to-team | Move To Team |
| GET | /redis/stats/{id} | Get Database Stats |
| GET | /redis/list-backup/{id} | List Backup |
| POST | /redis/create-backup/{id} | Create Backup |
| DELETE | /redis/delete-backup/{id}/{backup_id} | Delete Backup |
| POST | /redis/restore-backup/{id} | Restore Backup |
| PATCH | /redis/enable-dailybackup/{id} | Enable Daily Backup |
| PATCH | /redis/disable-dailybackup/{id} | Disable Daily Backup |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /teams | List Teams |
| GET | /teams/{team_id} | Get Team Members |
| POST | /teams/member | Add Team Member |
| DELETE | /teams/member | Delete Team Member |

### auditlogs
| Method | Path | Description |
|--------|------|-------------|
| GET | /auditlogs | List Audit Logs |

### team
| Method | Path | Description |
|--------|------|-------------|
| POST | /team | Create Team |
| DELETE | /team/{id} | Delete Team |

### vector
| Method | Path | Description |
|--------|------|-------------|
| GET | /vector/index | List Indices |
| POST | /vector/index | Create Index |
| GET | /vector/index/{id} | Get Index |
| DELETE | /vector/index/{id} | Delete Index |
| POST | /vector/index/{id}/rename | Rename Index |
| POST | /vector/index/{id}/reset-password | Reset Index Passwords |
| POST | /vector/index/{id}/setplan | Set Index Plan |
| POST | /vector/index/{id}/transfer | Transfer Index |
| GET | /vector/index/stats | Get Vector Stats |
| GET | /vector/index/{id}/stats | Get Index Stats |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | List Search Indexes |
| POST | /search | Create Search Index |
| GET | /search/{id} | Get Search Index |
| DELETE | /search/{id} | Delete Search Index |
| GET | /search/stats | Get Search Stats |
| GET | /search/{id}/stats | Get Index Stats |
| POST | /search/{id}/reset-password | Reset Password |
| POST | /search/{id}/transfer | Transfer Search Index |
| POST | /search/{id}/rename | Rename Search Index |

### qstash
| Method | Path | Description |
|--------|------|-------------|
| GET | /qstash/user | Get QStash |
| POST | /qstash/user/rotatetoken | Reset QStash Token |
| GET | /qstash/stats | Get QStash Stats |

### qstash-upgrade
| Method | Path | Description |
|--------|------|-------------|
| POST | /qstash-upgrade | Set QStash Plan |

## Enhanced Skill Content
## Question Mapping

- "What Redis databases do I have?" -> GET /redis/databases
- "Show me details for a specific Redis database" -> GET /redis/database/{id}
- "Create a new Redis database on AWS in us-east-1" -> POST /redis/database
- "Delete a Redis database" -> DELETE /redis/database/{id}
- "How is my Redis database performing?" -> GET /redis/stats/{id}
- "Change the plan for my Redis database to pay-as-you-go" -> POST /redis/change-plan/{id}
- "Reset the password on my Redis database" -> POST /redis/reset-password/{id}
- "List all my vector indexes" -> GET /vector/index
- "Create a vector index with cosine similarity" -> POST /vector/index
- "What are my QStash usage stats for the last 7 days?" -> GET /qstash/stats
- "Rotate my QStash token" -> POST /qstash/user/rotatetoken
- "Add a team member as a developer" -> POST /teams/member
- "Transfer a vector index to another account" -> POST /vector/index/{id}/transfer
- "Create a new search index" -> POST /search
- "What teams am I part of?" -> GET /teams

## Response Tips

- **Redis databases**: Responses include nested `securityAddons` map with boolean flags for IP whitelisting, VPC peering, private link, mutual TLS, and encryption at rest -- always check these for security audits.
- **Redis stats**: Time-series data comes as arrays of maps (e.g., `throughput`, `latencymean`, `hits`); the `days` array provides labels for daily aggregates like `dailyrequests` and `dailybilling`.
- **Vector indexes**: Creation returns `token` and `read_only_token` directly -- capture these immediately as they may not be retrievable later without a reset.
- **Search indexes**: Same token pattern as vector; the `throughput_vector` array of maps tracks throughput over time.
- **QStash user**: Returns all rate limits (`max_requests_per_day`, `max_retries`, `max_schedules`, etc.) in a flat object -- useful for capacity planning.
- **Teams**: Member creation returns the full team context including `copy_cc` billing flag; deletion endpoints return minimal confirmation.
- **All endpoints**: 200 is the only documented success code; treat any non-200 as an error. Many toggle endpoints (enable/disable eviction, autoupgrade, daily backup) return empty 200 responses.

## Anomaly Flags

- **Database state not "active"**: Surface `state` and `modifying_state` values when they indicate provisioning, migration, or error conditions.
- **Budget thresholds**: Flag when `budget` is set low relative to usage patterns visible in `redis/stats` monthly totals (`total_monthly_billing`).
- **QStash daily request limits**: Compare `max_requests_per_day` from `/qstash/user` against `daily_used` from `/qstash/stats` and warn when approaching the cap.
- **TLS disabled**: Flag any database where `tls: false` -- this is a security concern for production workloads.
- **Eviction enabled unexpectedly**: Surface `db_eviction: true` or `eviction: true` when it may cause data loss in non-cache use cases.
- **Plan mismatch**: Warn if a database is on the `free` plan but has high request counts or storage usage suggesting it should be upgraded.
- **Vector index pending count**: Flag when `pending_index_count` is non-zero in vector stats, indicating indexing backlog.
- **Bandwidth spikes**: Compare `total_monthly_bandwidth` against `max_monthly_bandwidth` for vector and search indexes to warn before hitting limits.
- **ACL disabled**: Surface `db_acl_enabled` when it is not set to a truthy value on databases that have multiple clients.

## Playbook

### 1. Provision a Production Redis Database

1. `POST /redis/database` with `platform: "aws"`, desired `primary_region`, `plan: "payg"`, `tls: true`, and `eviction: false`.
2. Capture `database_id` and `endpoint` from the response.
3. `POST /redis/enable-tls/{id}` if TLS was not set during creation.
4. `POST /redis/disable-eviction/{id}` to confirm eviction is off for data safety.
5. `PATCH /redis/enable-dailybackup/{id}` to enable automated backups.
6. `PATCH /redis/update-budget/{id}` to set a spending cap.
7. Verify with `GET /redis/database/{id}` and confirm `state: "active"`, `tls: true`, `daily_backup_enabled: true`.

### 2. Set Up a Vector Search Index with Embeddings

1. `POST /vector/index` with `name`, `region`, `similarity_function: "COSINE"`, `dimension_count` matching your embedding model, and optionally `embedding_model: "BGE_SMALL_EN_V1_5"` for built-in embeddings.
2. Save the returned `token`, `read_only_token`, and `endpoint`.
3. Verify creation with `GET /vector/index/{id}`.
4. Monitor usage with `GET /vector/index/{id}/stats` using `period: "1d"` for daily trends.
5. If needed later, change plan with `POST /vector/index/{id}/setplan`.

### 3. Manage Team Access and Billing

1. `POST /team` with `team_name` and `copy_cc: true` to share billing.
2. `POST /teams/member` with `team_id`, `member_email`, and `member_role: "dev"` for each developer.
3. `POST /redis/move-to-team` to transfer existing databases under team ownership.
4. Verify team structure with `GET /teams/{team_id}`.
5. Review activity with `GET /auditlogs` to confirm member actions.

### 4. Rotate Credentials Across All Services

1. For each Redis database: `POST /redis/reset-password/{id}` and update connection strings with new credentials from the response.
2. For QStash: `POST /qstash/user/rotatetoken` and update all webhook publishers with the new `token`.
3. For each vector index: `POST /vector/index/{id}/reset-password` and update application configs.
4. For each search index: `POST /search/{id}/reset-password` and update clients.
5. Verify connectivity to each service after rotation.

### 5. Monitor Costs and Usage Across Services

1. `GET /redis/stats/{id}` for each database -- check `total_monthly_requests`, `total_monthly_billing`, and `current_storage`.
2. `GET /vector/index/stats` for aggregate vector usage across all indexes.
3. `GET /search/stats` for aggregate search usage.
4. `GET /qstash/stats?period=30d` for monthly QStash message volume and billing.
5. Compare each service's usage against plan limits from their respective detail endpoints to identify upgrade or downgrade opportunities.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
