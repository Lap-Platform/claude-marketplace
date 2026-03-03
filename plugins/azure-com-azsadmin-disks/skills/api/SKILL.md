---
name: computediskadminmanagementclient
description: "ComputeDiskAdminManagementClient API skill. Use when working with ComputeDiskAdminManagementClient for subscriptions. Covers 2 endpoints."
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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks | Returns a list of disks. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId} | Returns the disk. |

## Enhanced Skill Content
## Question Mapping

- "What managed disks exist in this location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks
- "List all disks in the eastus region" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks
- "Get details for a specific disk" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}
- "What is the status of disk {id}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}
- "How many disks are provisioned in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks
- "Show me disk metadata for a given disk ID" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}
- "Which disks are in a failed state?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks (filter client-side by status)
- "Are there any unattached disks in this location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks (filter client-side by attach state)
- "What size is disk {id}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}
- "List disks across multiple locations" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks (call per location)
- "Does disk {id} exist?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId} (check for 200 vs 404)
- "What tenant is a disk associated with?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}

## Response Tips

- **Disk list (GET .../disks):** Response is typically `{ "value": [...] }` with an optional `nextLink` for pagination -- follow `nextLink` until absent to retrieve all pages. Each item contains nested `properties` with disk state, size, and share path.
- **Disk detail (GET .../disks/{DiskId}):** Returns a single resource object; key fields live under `properties` (e.g., `provisioningState`, `diskSizeGB`, `status`, `sharePath`). A 404 means the disk ID does not exist in that location.
- **Errors:** Azure ARM errors return `{ "error": { "code": "...", "message": "..." } }`. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `SubscriptionNotFound` (404).

## Anomaly Flags

- **HTTP 429 (Too Many Requests):** Surface the `Retry-After` header value and pause before retrying. Azure ARM enforces per-subscription throttling.
- **Unexpected disk states:** Flag disks where `provisioningState` is `Failed`, `Deleting`, or any non-terminal state that persists across polls.
- **Preview API version:** This spec uses `2018-07-30-preview` -- warn that preview APIs may change or be deprecated without notice. Recommend checking for GA versions.
- **Missing nextLink mid-page:** If a list response returns fewer items than expected but no `nextLink`, flag potential truncation or backend issues.
- **OAuth token expiry:** If a 401 is returned, proactively suggest token refresh rather than retrying with the same credentials.
- **Empty disk lists:** If a location returns zero disks when disks are expected, flag that the location string or subscription ID may be incorrect.

## Playbook

### 1. Inventory All Disks in a Location

1. Authenticate and obtain an OAuth2 bearer token for the Azure management scope.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it with another GET request and append results.
5. Repeat until no `nextLink` remains.
6. Summarize: total count, breakdown by `provisioningState`, and total disk size.

### 2. Inspect a Specific Disk

1. Obtain the disk ID (from a prior list call or known identifier).
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}`.
3. Extract key properties: `diskSizeGB`, `provisioningState`, `status`, `sharePath`, and `userResourceId`.
4. If 404 is returned, confirm the location and disk ID are correct; the disk may have been deleted or is in another location.

### 3. Find Unhealthy Disks Across Locations

1. Compile a list of target locations (e.g., `eastus`, `westus`, `centralus`).
2. For each location, call the list disks endpoint and paginate fully.
3. Filter results where `properties.provisioningState` is not `Succeeded`.
4. Aggregate flagged disks into a report grouped by location and state.
5. Surface any disks stuck in `Creating` or `Failed` for operator review.

### 4. Verify Disk Existence Before Downstream Operations

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/disks/{DiskId}`.
2. If 200: disk exists -- extract `provisioningState` to confirm it is ready.
3. If 404: disk does not exist -- abort the downstream operation and notify the user.
4. If 403: insufficient permissions -- surface the `error.message` and recommend checking RBAC role assignments.

### 5. Compare Disk State Over Time

1. Call the list disks endpoint and store the full response with a timestamp.
2. Wait for the desired interval (e.g., 1 hour).
3. Call the same endpoint again and store the new response.
4. Diff the two snapshots: identify new disks, deleted disks, and disks whose `provisioningState` changed.
5. Flag any disks that transitioned to `Failed` or disappeared unexpectedly.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
