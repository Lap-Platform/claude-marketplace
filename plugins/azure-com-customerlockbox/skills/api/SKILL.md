---
name: customer-lockbox
description: "Customer Lockbox API skill. Use when working with Customer Lockbox for providers, subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Customer Lockbox
API version: 2018-02-28-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.CustomerLockbox/operations -- verify access
3. POST /providers/Microsoft.CustomerLockbox/enableLockbox -- create first enableLockbox

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.CustomerLockbox/operations | Lists all the available REST API operations. |
| GET | /providers/Microsoft.CustomerLockbox/tenantOptedIn/{tenantId} | Get Customer Lockbox request |
| POST | /providers/Microsoft.CustomerLockbox/enableLockbox | Enable Tenant for Lockbox |
| POST | /providers/Microsoft.CustomerLockbox/disableLockbox | Disable Tenant for Lockbox |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId} | Get Customer Lockbox request |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}/updateApproval | Update Customer Lockbox request approval status API |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests | Lists all of the Lockbox requests in the given subscription. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Customer Lockbox?" -> GET /providers/Microsoft.CustomerLockbox/operations
- "Is Customer Lockbox enabled for my tenant?" -> GET /providers/Microsoft.CustomerLockbox/tenantOptedIn/{tenantId}
- "Check if tenant abc-123 has opted into Lockbox" -> GET /providers/Microsoft.CustomerLockbox/tenantOptedIn/{tenantId}
- "Enable Customer Lockbox for my organization" -> POST /providers/Microsoft.CustomerLockbox/enableLockbox
- "Turn on Lockbox so Microsoft needs approval before accessing data" -> POST /providers/Microsoft.CustomerLockbox/enableLockbox
- "Disable Customer Lockbox" -> POST /providers/Microsoft.CustomerLockbox/disableLockbox
- "Turn off Lockbox approval requirements" -> POST /providers/Microsoft.CustomerLockbox/disableLockbox
- "Get details on a specific Lockbox request" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}
- "What is the status of Lockbox request req-456?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}
- "List all Lockbox requests for my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests
- "Show pending Lockbox requests that need my approval" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests (with $filter)
- "Approve a Customer Lockbox request" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}/updateApproval
- "Deny a Lockbox access request from Microsoft" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}/updateApproval
- "How do I respond to a Microsoft support access request?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}/updateApproval

## Response Tips

- **Operations** (`/operations`): Returns a list of available API operations with name, display info, and descriptions. Useful for capability discovery only.
- **Tenant opt-in** (`/tenantOptedIn`): Returns a simple boolean-style status indicating whether Lockbox is active. Check the `isOptedIn` field directly.
- **Enable/Disable** (`/enableLockbox`, `/disableLockbox`): Returns 200 on success with the updated tenant status. These are idempotent -- enabling an already-enabled tenant is a no-op.
- **Request details** (`/requests/{requestId}`): Returns the full request object including status (`Pending`, `Approved`, `Denied`, `Expired`), requestor info, creation time, and expiration. Watch for `Expired` status on requests you intended to review.
- **Request listing** (`/requests`): Supports OData `$filter` for narrowing results. Returns a `value` array; check `nextLink` for pagination when many requests exist.
- **Update approval** (`/updateApproval`): The `approval` map must include `status` (`Approve` or `Deny`) and a `reason`. Returns the updated request object.

## Anomaly Flags

- **Lockbox disabled at tenant level**: If `tenantOptedIn` returns false, surface this immediately -- no approval workflows are active and Microsoft support can access data without customer consent.
- **Expired requests**: When listing or fetching requests, flag any with `Expired` status -- these represent missed approval windows where the default action (deny) was applied automatically.
- **Pending requests nearing expiration**: Surface requests in `Pending` status, especially if creation timestamps suggest they are close to the expiration window (typically 4-12 hours).
- **Rapid approval/deny patterns**: If multiple requests are being bulk-approved or denied in quick succession, flag for review -- this may indicate automation without human oversight.
- **API version mismatch**: All endpoints require `api-version`. If calls fail with 400, verify `2018-02-28-preview` is passed -- this is a preview API and version sensitivity is high.
- **Filter returning empty results**: When listing requests with `$filter` returns zero results but unfiltered returns many, surface the filter mismatch to avoid false "all clear" conclusions.

## Playbook

### 1. First-Time Lockbox Setup

1. Check current status: `GET /providers/Microsoft.CustomerLockbox/tenantOptedIn/{tenantId}` with your tenant ID
2. If not opted in, enable it: `POST /providers/Microsoft.CustomerLockbox/enableLockbox`
3. Verify activation: repeat the opt-in check to confirm `isOptedIn` is true
4. List available operations for reference: `GET /providers/Microsoft.CustomerLockbox/operations`

### 2. Review and Respond to an Access Request

1. List pending requests: `GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests` with `$filter` for pending status
2. Inspect the specific request: `GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}`
3. Review the requestor, justification, resource scope, and expiration time
4. Approve or deny: `POST /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests/{requestId}/updateApproval` with `approval: { status: "Approve"|"Deny", reason: "..." }`
5. Confirm the updated status by re-fetching the request

### 3. Audit All Lockbox Activity for a Subscription

1. List all requests (no filter): `GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests`
2. Follow `nextLink` pagination until all results are collected
3. Group by status (`Approved`, `Denied`, `Expired`, `Pending`) for a summary
4. Flag any `Expired` requests -- these indicate missed review windows
5. For each approved request, note the approver and reason for compliance records

### 4. Emergency Lockbox Disable and Re-enable

1. Verify current status: `GET /providers/Microsoft.CustomerLockbox/tenantOptedIn/{tenantId}`
2. Disable Lockbox: `POST /providers/Microsoft.CustomerLockbox/disableLockbox`
3. Confirm disabled state with another opt-in check
4. After the emergency window, re-enable: `POST /providers/Microsoft.CustomerLockbox/enableLockbox`
5. Review any requests that arrived during the disabled period: list requests and check for gaps

### 5. Multi-Subscription Request Monitoring

1. For each subscription ID in your organization, call `GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerLockbox/requests`
2. Aggregate all pending requests across subscriptions
3. Prioritize by expiration time (closest to expiring first)
4. Process approvals/denials per request using `updateApproval`
5. Confirm each response was recorded by re-fetching the request status


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
