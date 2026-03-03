---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2019-03-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/cancel -- create first cancel

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/cancel | The operation to cancel a subscription |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/rename | The operation to rename a subscription |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/enable | The operation to enable a subscription |

## Enhanced Skill Content
## Question Mapping

- "How do I cancel an Azure subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/cancel
- "Can I disable a subscription temporarily?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/cancel
- "How do I reactivate a cancelled subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/enable
- "How do I enable a disabled subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/enable
- "How do I rename a subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/rename
- "Can I change the display name of my subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/rename
- "How do I turn off a subscription without deleting it?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/cancel
- "What API version should I use for subscription management?" -> All endpoints require `api-version=2019-03-01-preview`
- "How do I restore a subscription after cancelling it?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/enable
- "Can I batch-rename multiple subscriptions?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/rename (call per subscription)
- "How do I cancel and then re-enable a subscription?" -> POST cancel then POST enable (two-step)
- "What body format does the rename endpoint expect?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/rename with `body` map containing the new name

## Response Tips

- **All endpoints** return 200 on success; any other status indicates a failure -- check the `error` object for `code` and `message` fields.
- **Cancel/Enable** return the updated subscription state; verify the `subscriptionState` field matches the expected value (`Disabled` after cancel, `Enabled` after enable).
- **Rename** returns the updated subscription object; confirm `displayName` reflects the requested change.
- **Error responses** follow Azure's standard format: `{ "error": { "code": "...", "message": "..." } }` -- common codes include `SubscriptionNotFound`, `InvalidAuthenticationToken`, and `AuthorizationFailed`.

## Anomaly Flags

- **Subscription already in target state**: Cancelling an already-disabled subscription or enabling an already-enabled one -- surface this as a no-op warning.
- **401/403 responses**: OAuth2 token may be expired or the service principal lacks `Microsoft.Subscription/subscriptions/action` permissions -- prompt the user to check RBAC assignments.
- **404 on subscriptionId**: The subscription does not exist or the authenticated principal has no visibility into it -- flag and suggest verifying the ID.
- **429 Too Many Requests**: Azure ARM throttling is active -- surface the `Retry-After` header value and pause before retrying.
- **Preview API version**: This API uses `2019-03-01-preview` -- flag that behavior may change and recommend checking for GA versions periodically.
- **Cancel on production subscriptions**: Proactively warn before cancelling any subscription, as it disables all resources under it.

## Playbook

### 1. Cancel a Subscription

1. Confirm the `subscriptionId` by listing subscriptions or checking the Azure portal.
2. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/cancel` with query param `api-version=2019-03-01-preview`.
3. Verify the response returns 200 and `subscriptionState` is `Disabled`.
4. Note: resources under the subscription become inaccessible but are retained for a grace period.

### 2. Rename a Subscription

1. Identify the target `subscriptionId`.
2. Build the request body with the new display name: `{ "subscriptionName": "New Name Here" }`.
3. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/rename` with the body and `api-version=2019-03-01-preview`.
4. Confirm the response shows the updated `displayName`.

### 3. Re-enable a Cancelled Subscription

1. Obtain the `subscriptionId` of the disabled subscription.
2. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Subscription/enable` with `api-version=2019-03-01-preview`.
3. Verify the response returns 200 and `subscriptionState` is `Enabled`.
4. Confirm resources under the subscription are accessible again.

### 4. Cancel and Rename Before Re-enabling (Maintenance Workflow)

1. Cancel the subscription using the cancel endpoint.
2. Rename the subscription to include a maintenance tag (e.g., `[MAINTENANCE] My Sub`).
3. Perform any out-of-band maintenance tasks.
4. Re-enable the subscription using the enable endpoint.
5. Rename again to remove the maintenance tag.

### 5. Bulk Subscription Rename

1. Collect all target `subscriptionId` values.
2. For each subscription, call the rename endpoint with the desired new name.
3. Track successes and failures -- retry any 429 responses after the `Retry-After` interval.
4. Verify all subscriptions reflect the correct display names.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
