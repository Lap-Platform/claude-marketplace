---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications -- verify access

## Endpoints

11 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications | Lists a collection of properties defined within a service instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName} | Gets the details of the Notification specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName} | Create or Update API Management publisher notification. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers | Gets the list of the Notification Recipient User subscribed to the notification. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers/{userId} | Determine if the Notification Recipient User is subscribed to the notification. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers/{userId} | Adds the API Management User to the list of Recipients for the Notification. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers/{userId} | Removes the API Management user from the list of Notification. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails | Gets the list of the Notification Recipient Emails subscribed to a notification. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails/{email} | Determine if Notification Recipient Email subscribed to the notification. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails/{email} | Adds the Email address to the list of Recipients for the Notification. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails/{email} | Removes the email from the list of Notification. |

## Enhanced Skill Content


## Question Mapping

- "What notifications are configured for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications
- "Show me details for a specific notification type" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}
- "How do I create or update a notification?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}
- "Who are the user recipients for a notification?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers
- "Is a specific user subscribed to a notification?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers/{userId}
- "Add a user as a recipient for a notification" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers/{userId}
- "Remove a user from notification recipients" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientUsers/{userId}
- "What email addresses receive a specific notification?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails
- "Is a specific email subscribed to a notification?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails/{email}
- "Add an email address to notification recipients" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails/{email}
- "Remove an email from notification recipients" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/notifications/{notificationName}/recipientEmails/{email}
- "How do I set up alerts for API quota limits?" -> PUT .../notifications/{notificationName} then PUT .../recipientUsers/{userId} or .../recipientEmails/{email}
- "Which users and emails get notified about new subscriptions?" -> GET .../notifications/{notificationName}/recipientUsers + GET .../notifications/{notificationName}/recipientEmails

## Response Tips

- **Notification listings** (GET .../notifications): Returns a paginated collection with `value` array and `nextLink` for continuation; iterate `nextLink` until absent.
- **Single notification** (GET/PUT .../notifications/{name}): Returns the full notification contract object; check `properties` for current state.
- **Recipient listings** (GET .../recipientUsers, .../recipientEmails): Returns `value` array of recipient contracts; no pagination expected for small sets but check for `nextLink`.
- **Existence checks** (HEAD endpoints): 204 means the recipient exists, 404 means not found; no response body is returned.
- **Create/add operations** (PUT endpoints): 200 means updated existing, 201 means newly created; both return the resource body.
- **Delete operations** (DELETE endpoints): 200 means deleted with body, 204 means deleted with no content; both are success.

## Anomaly Flags

- **404 on HEAD checks**: Expected behavior (recipient not subscribed), not an error -- do not escalate unless it follows a PUT that should have created it.
- **Repeated 200 on PUT instead of 201**: The recipient already existed; surface if the caller expected a new addition.
- **Missing `nextLink` on large notification lists**: Could indicate truncated results if the service has many notification types configured.
- **OAuth token expiry (401)**: Surface immediately and prompt for token refresh before retrying.
- **Throttling (429)**: Azure ARM has per-subscription rate limits; surface `Retry-After` header value and pause operations.
- **Inconsistent recipient state**: If a HEAD returns 404 immediately after a successful PUT 201, flag a potential replication delay.

## Playbook

### 1. Audit all notification recipients

1. GET .../notifications to list all notification types
2. For each notification in the response `value` array, extract `notificationName`
3. GET .../notifications/{notificationName}/recipientUsers to list user recipients
4. GET .../notifications/{notificationName}/recipientEmails to list email recipients
5. Compile results into a summary of who receives what

### 2. Subscribe a new team member to all notifications

1. GET .../notifications to retrieve every notification type
2. For each `notificationName`, PUT .../notifications/{notificationName}/recipientUsers/{userId} to add by user ID
3. Alternatively, PUT .../notifications/{notificationName}/recipientEmails/{email} to add by email
4. Verify each PUT returns 200 or 201
5. Optionally, HEAD each recipient endpoint to confirm subscription is active

### 3. Remove a departing user from all notifications

1. GET .../notifications to list all notification types
2. For each `notificationName`, HEAD .../recipientUsers/{userId} to check if subscribed (204 = yes)
3. For each 204 response, DELETE .../recipientUsers/{userId}
4. Repeat steps 2-3 for .../recipientEmails/{email} if the user had email subscriptions
5. Confirm all DELETE calls return 200 or 204

### 4. Set up a new notification type with recipients

1. PUT .../notifications/{notificationName} to create the notification configuration
2. Confirm 200/201 response with the notification contract
3. PUT .../recipientUsers/{userId} for each user who should receive it
4. PUT .../recipientEmails/{email} for each email address that should receive it
5. GET .../recipientUsers and .../recipientEmails to verify all recipients are registered

### 5. Check if a specific person receives a specific notification

1. HEAD .../notifications/{notificationName}/recipientUsers/{userId} to check user subscription
2. If 204: user is subscribed; if 404: user is not
3. HEAD .../notifications/{notificationName}/recipientEmails/{email} to check email subscription
4. If 204: email is subscribed; if 404: email is not
5. Report combined result to confirm full coverage


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
