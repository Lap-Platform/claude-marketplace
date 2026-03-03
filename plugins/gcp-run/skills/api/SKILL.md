---
name: cloud-run-admin-api
description: "Cloud Run Admin API skill. Use when working with Cloud Run Admin for {name}, {name}:run, {name}:wait. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# Cloud Run Admin API
API version: v2

## Auth
OAuth2 | OAuth2

## Base URL
https://run.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /v2/{name}/operations -- verify access
3. POST /v2/{name}:run -- create first resource

## Endpoints

16 endpoints across 7 groups. See references/api-spec.lap for full details.

### {name}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v2/{name} | Deletes a Revision. |
| GET | /v2/{name} | Gets information about a Revision. |
| PATCH | /v2/{name} | Updates a Service. |
| GET | /v2/{name}/operations | Lists operations that match the specified filter in the request. If the server doesn't support this method, it returns `UNIMPLEMENTED`. |

### {name}:run
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{name}:run | Triggers creation of a new Execution of this Job. |

### {name}:wait
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{name}:wait | Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state. If the operation is already done, the latest state is immediately returned. If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC timeout is used. If the server does not support this method, it returns `google.rpc.Code.UNIMPLEMENTED`. Note that this method is on a best-effort basis. It may return the latest state before the specified timeout (including immediately), meaning even an immediate response is no guarantee that the operation is done. |

### {parent}
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/{parent}/executions | Lists Executions from a Job. |
| GET | /v2/{parent}/jobs | Lists Jobs. |
| POST | /v2/{parent}/jobs | Creates a Job. |
| GET | /v2/{parent}/revisions | Lists Revisions from a given Service, or from a given location. |
| GET | /v2/{parent}/services | Lists Services. |
| POST | /v2/{parent}/services | Creates a new Service in a given project and location. |
| GET | /v2/{parent}/tasks | Lists Tasks from an Execution of a Job. |

### {resource}:getIamPolicy
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/{resource}:getIamPolicy | Gets the IAM Access Control policy currently in effect for the given Cloud Run Service. This result does not include any inherited policies. |

### {resource}:setIamPolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{resource}:setIamPolicy | Sets the IAM Access control policy for the specified Service. Overwrites any existing policy. |

### {resource}:testIamPermissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{resource}:testIamPermissions | Returns permissions that a caller has on the specified Project. There are no permissions required for making this API call. |

## Enhanced Skill Content
## Question Mapping

- "What services are running in my project?" -> GET /v2/{parent}/services
- "Show me details for a specific service" -> GET /v2/{name}
- "Deploy a new Cloud Run service" -> POST /v2/{parent}/services
- "Update my service's container image or scaling" -> PATCH /v2/{name}
- "Delete a Cloud Run service" -> DELETE /v2/{name}
- "List all jobs in my project" -> GET /v2/{parent}/jobs
- "Create a new Cloud Run job" -> POST /v2/{parent}/jobs
- "Trigger a job execution" -> POST /v2/{name}:run
- "What executions has this job had?" -> GET /v2/{parent}/executions
- "List tasks within a job execution" -> GET /v2/{parent}/tasks
- "Check the status of a long-running operation" -> POST /v2/{name}:wait
- "List all operations for a resource" -> GET /v2/{name}/operations
- "Who has access to this service?" -> GET /v2/{resource}:getIamPolicy
- "Grant a user permission to invoke a service" -> POST /v2/{resource}:setIamPolicy
- "Check if a principal has specific permissions" -> POST /v2/{resource}:testIamPermissions

## Response Tips

- **Services/Jobs/Revisions (list endpoints):** Paginated via `nextPageToken` -- keep calling with `pageToken` until token is absent. Use `showDeleted: true` to include soft-deleted resources.
- **Mutating operations (create/update/delete):** Return a long-running operation object (`{done, error, metadata, name, response}`). Poll with `GET /v2/{name}/operations` or block with `POST /v2/{name}:wait` until `done: true`. Check `error` before reading `response`.
- **Service/Job detail (GET by name):** `conditions` array holds readiness state -- look for `type: "Ready"` with `state: "CONDITION_SUCCEEDED"`. `reconciling: true` means changes are still propagating.
- **IAM responses:** `bindings` array maps roles to members. Always include the returned `etag` in subsequent `setIamPolicy` calls to avoid concurrent modification conflicts.

## Anomaly Flags

- **`reconciling: true`** on a service or job: Changes are still being applied -- warn the user before making additional updates.
- **`launchStage: "DEPRECATED"`** on any resource: Surface immediately; the resource uses a deprecated feature that may stop working.
- **`error` present in operation response**: Extract `error.code` and `error.message` and surface prominently -- the operation failed silently.
- **`done: false` persisting** on operations after a wait call: The operation is taking unusually long; suggest increasing the `timeout` duration or investigating.
- **`conditions` with `severity: "ERROR"`**: A resource has entered a broken state -- surface the `message` and `reason` fields.
- **`deleteTime` / `expireTime` populated**: Resource is scheduled for deletion -- alert user if they're trying to modify it.
- **Missing `latestReadyRevision`** when `latestCreatedRevision` exists: The newest revision failed to become ready -- check conditions for details.
- **`etag` mismatch on delete/update**: Concurrent modification detected; re-fetch the resource before retrying.

## Playbook

### Deploy a New Service

1. Call `POST /v2/{parent}/services` with `parent` as `projects/{project}/locations/{region}`, providing at minimum `template.containers[0].image`.
2. Capture the operation `name` from the response.
3. Call `POST /v2/{name}:wait` with the operation name and a reasonable `timeout` (e.g., `"300s"`).
4. When `done: true`, read `response` for the created service details. If `error` is present, inspect `error.message`.
5. Verify by calling `GET /v2/{name}` on the service and confirming `conditions` show `Ready` with `CONDITION_SUCCEEDED`.

### Run a Job and Monitor Execution

1. Call `POST /v2/{name}:run` with the job's full resource name to trigger an execution.
2. Capture the operation `name` from the response.
3. Call `POST /v2/{name}:wait` on the operation to block until completion.
4. Once done, call `GET /v2/{parent}/executions` with the job name as parent to list executions.
5. For granular progress, call `GET /v2/{parent}/tasks` with the execution name as parent to see individual task statuses.

### Update Service Traffic Splitting

1. Call `GET /v2/{name}` on the service to retrieve the current config and `etag`.
2. Call `GET /v2/{parent}/revisions` to identify available revision names.
3. Call `PATCH /v2/{name}` with `traffic` array specifying `revision` and `percent` for each split (must total 100). Include the `etag` from step 1.
4. Wait on the returned operation until `done: true`.
5. Verify by reading the service again and checking `trafficStatuses` for the applied split and per-tag URIs.

### Grant Invoke Access to a Service

1. Call `GET /v2/{resource}:getIamPolicy` with the service resource name to retrieve current bindings and `etag`.
2. Add a new entry to `bindings` with `role: "roles/run.invoker"` and `members: ["user:email@example.com"]`.
3. Call `POST /v2/{resource}:setIamPolicy` with the full `policy` object including the original `etag`.
4. Optionally call `POST /v2/{resource}:testIamPermissions` with `permissions: ["run.routes.invoke"]` to confirm the grant took effect.

### Scale Down a Service for Cost Savings

1. Call `GET /v2/{name}` on the service to retrieve the current template and `etag`.
2. Call `PATCH /v2/{name}` setting `template.scaling.minInstanceCount` to `0` and `template.scaling.maxInstanceCount` to a lower bound (e.g., `1`). Include the `etag`.
3. Wait on the returned operation until `done: true`.
4. Confirm by calling `GET /v2/{name}` and checking `scaling` values on the latest ready revision.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
