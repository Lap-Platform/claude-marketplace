---
name: computediskadminmanagementclient
description: "ComputeDiskAdminManagementClient API skill. Use when working with ComputeDiskAdminManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# ComputeDiskAdminManagementClient
API version: 2018-07-30-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}/Cancel -- create first Cancel

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs | Returns a list of disk migration jobs. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId} | Returns the requested disk migration job. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId} | Create a disk migration job. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}/Cancel | Cancel a disk migration job. |

## Enhanced Skill Content


## Question Mapping

- "What disk migration jobs exist in my location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs
- "List all active disk migrations for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs
- "What is the status of a specific disk migration job?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}
- "Has my disk migration completed?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}
- "How do I start a new disk migration?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}
- "How do I create or update a disk migration job?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}
- "How do I cancel a running disk migration?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}/Cancel
- "Can I stop a migration that is in progress?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId}/Cancel
- "Are there any failed disk migration jobs?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs (filter response for failed status)
- "How do I retry a failed disk migration?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId} (re-create with same or updated config)
- "What migrations are running in eastus?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/eastus/diskmigrationjobs
- "How do I monitor a disk migration end to end?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/diskmigrationjobs/{migrationId} (poll until terminal state)

## Response Tips

- **List endpoints**: Response may include a `value` array with pagination via `nextLink`; follow `nextLink` until absent to retrieve all jobs.
- **Single resource GET**: Returns the full migration job object including `properties.migrationStatus`; check `provisioningState` for async operation status.
- **PUT (create/update)**: May return synchronously (200) or initiate a long-running operation; check for `Azure-AsyncOperation` or `Location` headers for polling.
- **POST Cancel**: Returns 200 on acceptance; the job may not terminate immediately -- poll the GET endpoint to confirm cancellation completed.
- **Errors**: Azure returns `{ "error": { "code": "...", "message": "..." } }` with standard HTTP codes (400, 404, 409, 500); the `code` field gives machine-readable detail.

## Anomaly Flags

- **Stuck migrations**: A job in `Running` or `InProgress` state for longer than expected -- surface if status has not changed across multiple polls.
- **Cancellation failures**: Cancel POST returns 200 but subsequent GET still shows the job progressing -- flag for manual intervention.
- **Provisioning state mismatch**: `provisioningState` differs from `migrationStatus` (e.g., provisioning succeeded but migration failed).
- **Throttling (429)**: Azure subscription-level rate limits approaching; surface `Retry-After` header values and recommend backoff.
- **Deprecated API version**: This spec uses `2018-07-30-preview` -- a preview version. Flag if a newer stable API version is available.
- **Unexpected 409 Conflict**: Returned on PUT when a migration job with the same ID already exists in a non-terminal state.

## Playbook

### 1. Create and Monitor a Disk Migration

1. PUT `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs/{migrationId}` with the job configuration body.
2. Check the response for `provisioningState`. If `Accepted` or `Creating`, note any async polling headers.
3. Poll GET `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs/{migrationId}` at intervals (e.g., 30s).
4. Continue polling until `properties.migrationStatus` reaches a terminal state (`Succeeded`, `Failed`, or `Canceled`).
5. On failure, inspect the error details in the response body before deciding to retry or escalate.

### 2. Cancel a Running Migration

1. GET `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs/{migrationId}` to confirm the job is still active.
2. POST `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs/{migrationId}/Cancel`.
3. Poll GET on the same job until `migrationStatus` shows `Canceled`.
4. If the status does not change to `Canceled` after several attempts, escalate -- the cancel may not have taken effect.

### 3. Audit All Migration Jobs in a Region

1. GET `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs` to list all jobs.
2. Follow any `nextLink` values to paginate through the full set.
3. Group jobs by status (`Succeeded`, `Failed`, `Running`, `Canceled`) for a summary view.
4. For each failed job, GET the individual resource to retrieve detailed error information.

### 4. Retry a Failed Migration

1. GET `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs/{migrationId}` to inspect the failure reason.
2. Fix the underlying issue (e.g., permissions, disk availability, quota).
3. PUT `/subscriptions/{sub}/providers/Microsoft.Compute.Admin/locations/{loc}/diskmigrationjobs/{migrationId}` with corrected configuration.
4. Monitor as described in Playbook 1 until the job reaches a terminal state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
