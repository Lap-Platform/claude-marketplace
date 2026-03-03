---
name: vsonline
description: "VSOnline API skill. Use when working with VSOnline for api, health, internal. Covers 61 endpoints."
version: 1.0.0
generator: lapsh
---

# VSOnline
API version: v1

## Auth
Bearer bearer

## Base URL
https://online.visualstudio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/v1/Billing -- verify access
3. POST /api/v1/AgentTelemetry -- create first AgentTelemetry

## Endpoints

61 endpoints across 5 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/Agents/{family} |  |
| POST | /api/v1/AgentTelemetry |  |
| POST | /api/v1/AgentTelemetry/standalone |  |
| PUT | /api/v1/Billing/ensure_plan |  |
| GET | /api/v1/Billing |  |
| GET | /api/v1/GenevaActions/Billing/{environmentId} |  |
| POST | /api/v1/GenevaActions/Billing/resend |  |
| POST | /api/v1/GenevaActions/Billing/{environmentId}/state-changes |  |
| GET | /api/v1/GenevaActions/Billing/{environmentId}/state-changes |  |
| GET | /api/v1/GenevaActions/Configuration/{key} |  |
| DELETE | /api/v1/GenevaActions/Configuration/{key} |  |
| POST | /api/v1/GenevaActions/Configuration |  |
| GET | /api/v1/Environments/{environmentId} |  |
| DELETE | /api/v1/Environments/{environmentId} |  |
| PATCH | /api/v1/Environments/{environmentId} |  |
| GET | /api/v1/Environments |  |
| POST | /api/v1/Environments |  |
| POST | /api/v1/Environments/{environmentId}/shutdown |  |
| POST | /api/v1/Environments/{environmentId}/start |  |
| POST | /api/v1/Environments/{environmentId}/archive |  |
| GET | /api/v1/Environments/{environmentId}/archive |  |
| POST | /api/v1/Environments/{environmentId}/export |  |
| PATCH | /api/v1/Environments/{environmentId}/restore |  |
| PATCH | /api/v1/Environments/{environmentId}/folder |  |
| PUT | /api/v1/Environments/{environmentId}/secrets |  |
| POST | /api/v1/Environments/{environmentId}/notify |  |
| GET | /api/v1/GenevaActions/Environments/{environmentId} |  |
| DELETE | /api/v1/GenevaActions/Environments/{environmentId} |  |
| PUT | /api/v1/GenevaActions/Environments/{environmentId}/shutdown |  |
| PUT | /api/v1/GenevaActions/Environments/{environmentId}/archive |  |
| GET | /api/v1/GenevaActions/Environments/storage/{environmentIdOrFriendlyName}/{targetBlob} |  |
| POST | /api/v1/GenevaActions/Environments/{environmentId}/upload/running/vm/logs |  |
| GET | /api/v1/Environments/{environmentId}/state |  |
| POST | /api/v1/GenevaActions/Failover/start/{region} |  |
| POST | /api/v1/HeartBeat |  |
| GET | /api/v1/Locations |  |
| GET | /api/v1/Locations/{location} |  |
| GET | /api/v1/pools/default |  |
| POST | /api/v1/GenevaActions/Pools/rotate-pools |  |
| POST | /api/v1/GenevaActions/Pools |  |
| POST | /api/v1/GenevaActions/Pools/change-resource-deletion-setting |  |
| POST | /api/v2/prebuilds/templates |  |
| POST | /api/v2/prebuilds/templates/{templateId}/updatestatus |  |
| GET | /api/v2/prebuilds/templates/skus/repo/{repoId}/branch/{branchName}/hash/{prebuildHash}/location/{location}/devcontainerpath/{devContainerPath} |  |
| POST | /api/v2/prebuilds/delete |  |
| POST | /api/v2/prebuilds/templates/updatemaxversions |  |
| PUT | /api/v2/prebuilds/pools/{poolId}/instances |  |
| POST | /api/v2/prebuilds/pools/{poolId}/instances |  |
| GET | /api/v2/prebuilds/template/{environmentId} |  |
| POST | /api/v1/GenevaActions/Prebuilds/pools/delete |  |
| POST | /api/v1/GenevaActions/Prebuilds/pools/createorupdatesettings |  |
| POST | /api/v1/GenevaActions/Resources/{resourceId}/under-investigation |  |
| POST | /api/v1/GenevaActions/Resources/{resourceId}/storage-credentials |  |
| GET | /api/v1/Tunnel/{environmentId}/portInfo |  |
| POST | /api/v1/GenevaActions/VnetPoolDefinitions |  |
| DELETE | /api/v1/GenevaActions/VnetPoolDefinitions |  |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health |  |

### internal
| Method | Path | Description |
|--------|------|-------------|
| GET | /internal/Netmon/correlation |  |

### .well-known
| Method | Path | Description |
|--------|------|-------------|
| GET | /.well-known/jwks |  |
| GET | /.well-known/openid-configuration |  |

### warmup
| Method | Path | Description |
|--------|------|-------------|
| GET | /warmup |  |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new codespace?" -> POST /api/v1/Environments
- "How do I list all my environments?" -> GET /api/v1/Environments
- "What is the status of my codespace?" -> GET /api/v1/Environments/{environmentId}
- "How do I stop a running codespace?" -> POST /api/v1/Environments/{environmentId}/shutdown
- "How do I start a stopped codespace?" -> POST /api/v1/Environments/{environmentId}/start
- "How do I delete an environment?" -> DELETE /api/v1/Environments/{environmentId}
- "How do I change the SKU or auto-shutdown timeout on my codespace?" -> PATCH /api/v1/Environments/{environmentId}
- "How do I set secrets on an environment?" -> PUT /api/v1/Environments/{environmentId}/secrets
- "What regions and SKUs are available?" -> GET /api/v1/Locations/{location}
- "How do I check my billing plan?" -> GET /api/v1/Billing
- "How do I ensure a billing plan exists for my subscription?" -> PUT /api/v1/Billing/ensure_plan
- "How do I archive a codespace for long-term storage?" -> POST /api/v1/Environments/{environmentId}/archive
- "How do I restore an archived codespace?" -> PATCH /api/v1/Environments/{environmentId}/restore
- "How do I export my environment data?" -> POST /api/v1/Environments/{environmentId}/export
- "How do I check if a prebuild template exists for my repo and branch?" -> GET /api/v2/prebuilds/templates/skus/repo/{repoId}/branch/{branchName}/hash/{prebuildHash}/location/{location}/devcontainerpath/{devContainerPath}

## Response Tips

- **Environments**: Responses are deeply nested -- `seed.repository`, `connection.tunnelProperties`, and `gitStatus` are the most useful sub-objects; most top-level fields are nullable.
- **Billing**: `usage` and `usageDetail` are opaque maps; always check `periodStart`/`periodEnd` for the billing window.
- **Locations**: `available` is an integer array of location enum codes (not names); map them using the enum defined on the billing endpoint.
- **State values**: Environment `state` is a string (Available, Shutdown, Archived, etc.) but GenevaActions state-change endpoints use integer enums (0-16) for `oldValue`/`newValue`.
- **204 responses**: Shutdown secrets, delete, telemetry, and heartbeat return empty bodies on success -- check status code only.
- **Error codes**: 307 on POST Environments or PUT secrets means a region redirect; follow the Location header. 409 on PATCH means a concurrent modification conflict; retry with fresh data. 503 means the service is temporarily overloaded.

## Anomaly Flags

- **State: Failed (13) or Unavailable (6)**: Surface immediately when an environment enters these states -- user action or support escalation likely needed.
- **409 Conflict on PATCH**: Indicates a race condition; warn the user to re-fetch before retrying.
- **307 Redirect on create/secrets**: The environment is in a different region than expected; confirm the redirect target with the user.
- **503 on start/archive/export**: Service is capacity-constrained; recommend retrying after a short wait or choosing a different region.
- **subscriptionData.computeUsage approaching computeQuota**: Proactively warn when usage is above 80% of quota to prevent creation failures.
- **gitStatus.hasUnpushedChanges or hasUncommittedChanges**: Flag before shutdown/delete/archive to prevent data loss.
- **lastStateUpdateReason**: Surface when it contains error-related text -- it explains why the environment entered its current state.
- **Deprecated prebuild fields**: `storageType` V1 (0) is legacy; flag if templates are still using it when V2 is available.

## Playbook

### 1. Create and Connect to a New Codespace

1. `GET /api/v1/Locations` to find available regions.
2. `GET /api/v1/Locations/{location}` with your preferred region to list available SKUs.
3. `GET /api/v1/Billing` to confirm a billing plan exists; if not, call `PUT /api/v1/Billing/ensure_plan`.
4. `POST /api/v1/Environments` with `type`, `friendlyName`, `skuName`, `location`, and `seed.repository` for your repo.
5. Poll `GET /api/v1/Environments/{environmentId}` until `state` is `Available`.
6. Read `connection.tunnelProperties` from the response to establish your tunnel connection.

### 2. Safely Shut Down and Archive an Idle Codespace

1. `GET /api/v1/Environments/{environmentId}` and check `gitStatus.hasUnpushedChanges` and `hasUncommittedChanges`.
2. If there are uncommitted/unpushed changes, warn the user or push first.
3. `POST /api/v1/Environments/{environmentId}/shutdown` and wait for `state` to become `Shutdown`.
4. Optionally, `POST /api/v1/Environments/{environmentId}/archive` for long-term storage (reduces costs).
5. Confirm archive by checking `GET /api/v1/Environments/{environmentId}/archive` returns the archived state.

### 3. Restore and Resize an Archived Environment

1. `PATCH /api/v1/Environments/{environmentId}/restore` to move from Archived back to Shutdown.
2. `PATCH /api/v1/Environments/{environmentId}` with the new `skuName` to resize.
3. `POST /api/v1/Environments/{environmentId}/start` to boot the environment.
4. Poll `GET /api/v1/Environments/{environmentId}` until `state` is `Available`.

### 4. Set Up Prebuild Templates for Faster Creation

1. `POST /api/v2/prebuilds/templates` with `friendlyName`, `seed.repository`, and `planId`.
2. Wait for the template build; call `POST /api/v2/prebuilds/templates/{templateId}/updatestatus` with `isSuccess: true` when done.
3. Verify availability: `GET /api/v2/prebuilds/templates/skus/repo/{repoId}/branch/{branchName}/hash/{prebuildHash}/location/{location}/devcontainerpath/{devContainerPath}`.
4. Create environments from the prebuild by setting `createFromPrebuild` and `seed.repository.prebuildHash` in the `POST /api/v1/Environments` call.

### 5. Investigate and Diagnose a Failed Environment

1. `GET /api/v1/Environments/{environmentId}` -- check `state`, `lastStateUpdateReason`, and `userControlledFailureReason`.
2. `GET /api/v1/Environments/{environmentId}/state` for the raw state value.
3. `GET /api/v1/GenevaActions/Billing/{environmentId}/state-changes` to review the state transition history and find when the failure occurred.
4. `POST /api/v1/GenevaActions/Environments/{environmentId}/upload/running/vm/logs` to capture VM-level logs for deeper investigation.
5. If the environment is recoverable, try `POST /api/v1/Environments/{environmentId}/start`; if it returns 503, consider creating a new environment from the same seed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
