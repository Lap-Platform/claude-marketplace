---
name: gdpr-api
description: "GDPR API skill. Use when working with GDPR for data-retrievals, data-deletions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# GDPR API
API version: 3.0.0

## Auth
Requires API key (token parameter)

## Base URL
Not specified.

## Setup
1. Include your API key via the token parameter
2. GET /data-retrievals/v3.0/{tracking_id} -- verify access
3. POST /data-retrievals/v3.0 -- create first v3.0

## Endpoints

5 endpoints across 2 groups. See references/api-spec.lap for full details.

### data-retrievals
| Method | Path | Description |
|--------|------|-------------|
| POST | /data-retrievals/v3.0 | Create a Retrieval |
| GET | /data-retrievals/v3.0/{tracking_id} | Check Status of Retrieval |

### data-deletions
| Method | Path | Description |
|--------|------|-------------|
| POST | /data-deletions/v3.0 | Create a Deletion |
| GET | /data-deletions/v3.0/{tracking_id} | Check Status of Deletion |
| DELETE | /data-deletions/v3.0/{tracking_id} | Cancel a Deletion |

## Enhanced Skill Content
## Question Mapping

- "How do I request a data retrieval for a user?" -> POST /data-retrievals/v3.0
- "How do I check the status of a data retrieval?" -> GET /data-retrievals/v3.0/{tracking_id}
- "How do I submit a GDPR deletion request?" -> POST /data-deletions/v3.0
- "What is the status of my deletion request?" -> GET /data-deletions/v3.0/{tracking_id}
- "How do I cancel a pending data deletion?" -> DELETE /data-deletions/v3.0/{tracking_id}
- "How do I retrieve data for multiple users at once?" -> POST /data-retrievals/v3.0 (pass multiple distinct_ids)
- "How do I make a CCPA-compliant data request?" -> POST /data-retrievals/v3.0 (set compliance_type to CCPA)
- "How do I delete data for a specific distinct_id?" -> POST /data-deletions/v3.0 (pass distinct_ids array)
- "How do I get the results of a completed retrieval?" -> GET /data-retrievals/v3.0/{tracking_id} (check results field)
- "Who requested a specific deletion?" -> GET /data-deletions/v3.0/{tracking_id} (check requesting_user)
- "When was a deletion request submitted?" -> GET /data-deletions/v3.0/{tracking_id} (check date_requested)
- "How do I perform a right-to-erasure request?" -> POST /data-deletions/v3.0 (set compliance_type to GDPR)

## Response Tips

- **Data Retrievals (POST):** 201 returns a `results` map containing a `task_id` -- store this to poll status later via the tracking_id.
- **Data Retrievals (GET):** `results` is a nested map with its own `status`, `results` string, and `distinct_ids` array -- check the inner `status` for completion state, not just the outer one.
- **Data Deletions (POST):** Identical 201 shape to retrievals; extract `task_id` from the `results` map for tracking.
- **Data Deletions (GET):** Returns richer metadata than retrievals including `requesting_user`, `compliance_type`, `project_id`, and `date_requested` -- useful for audit trails.
- **Data Deletions (DELETE):** Returns 204 with no body -- success is indicated solely by status code.
- **All endpoints:** Only 401 and 403 errors are documented; 401 means missing/invalid token, 403 means the token lacks permission for the requested resource.

## Anomaly Flags

- **401/403 on any call:** Surface immediately -- likely an expired or misconfigured token. Prompt the user to verify their `token` value.
- **Deletion still pending after extended polling:** If GET /data-deletions/v3.0/{tracking_id} returns a non-terminal status after multiple checks, warn the user that the deletion may be stuck or queued behind a large batch.
- **Retrieval results field is empty or null:** The inner `results` string in GET /data-retrievals may be empty if the task is still processing -- flag this and suggest polling again later rather than treating it as "no data found."
- **Mismatched compliance_type:** If the user requests CCPA compliance but the deletion status returns a different compliance_type, surface the discrepancy as a potential misconfiguration.
- **DELETE called on a completed deletion:** Attempting to cancel an already-completed deletion may behave unexpectedly -- warn before sending.
- **Missing distinct_ids on POST:** Both retrieval and deletion endpoints accept distinct_ids as optional; if omitted, the scope of the operation may be broader than intended. Flag this before submitting.

## Playbook

### 1. Submit and Track a Data Retrieval

1. Call POST /data-retrievals/v3.0 with your `token` and the target `distinct_ids`.
2. Extract `task_id` from the `results` map in the 201 response.
3. Poll GET /data-retrievals/v3.0/{task_id} periodically.
4. When the inner `status` indicates completion, read the `results` string for the retrieved data.

### 2. Execute a GDPR Right-to-Erasure Deletion

1. Call POST /data-deletions/v3.0 with `token`, `distinct_ids`, and `compliance_type` set to the appropriate regulation (e.g., "GDPR").
2. Store the returned `task_id` from the 201 response.
3. Poll GET /data-deletions/v3.0/{task_id} to monitor progress.
4. Confirm deletion is complete by checking that `status` reaches a terminal state.
5. Record `date_requested` and `requesting_user` for your compliance audit log.

### 3. Cancel a Pending Deletion Request

1. Retrieve the `tracking_id` of the deletion (from your original POST response or records).
2. Optionally call GET /data-deletions/v3.0/{tracking_id} to confirm it is still in a cancellable state.
3. Call DELETE /data-deletions/v3.0/{tracking_id}.
4. Verify a 204 response to confirm cancellation succeeded.

### 4. Bulk Data Retrieval for Multiple Users

1. Collect all target user identifiers into a `distinct_ids` array.
2. Call POST /data-retrievals/v3.0 with the full array and your `token`.
3. Extract the `task_id` from the response.
4. Poll GET /data-retrievals/v3.0/{task_id} -- the response `distinct_ids` array confirms which users were included.
5. Parse the `results` string for per-user data once the status is complete.

### 5. Audit a Past Deletion Request

1. Call GET /data-deletions/v3.0/{tracking_id} with the known tracking ID.
2. Record `requesting_user`, `date_requested`, `compliance_type`, and `project_id`.
3. Verify the `status` field shows the expected terminal state.
4. Cross-reference `distinct_ids` against your internal records to confirm scope was correct.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
