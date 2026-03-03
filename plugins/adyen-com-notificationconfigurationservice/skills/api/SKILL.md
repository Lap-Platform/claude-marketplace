---
name: notification-configuration-api
description: "Notification Configuration API skill. Use when working with Notification Configuration for createNotificationConfiguration, deleteNotificationConfigurations, getNotificationConfiguration. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Notification Configuration API
API version: 6

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://cal-test.adyen.com/cal/services/Notification/v6

## Setup
1. Set Authorization header with your Bearer token
3. POST /createNotificationConfiguration -- create first createNotificationConfiguration

## Endpoints

6 endpoints across 6 groups. See references/api-spec.lap for full details.

### createNotificationConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /createNotificationConfiguration | Subscribe to notifications |

### deleteNotificationConfigurations
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteNotificationConfigurations | Delete a notification subscription configuration |

### getNotificationConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /getNotificationConfiguration | Get a notification subscription configuration |

### getNotificationConfigurationList
| Method | Path | Description |
|--------|------|-------------|
| POST | /getNotificationConfigurationList | Get a list of notification subscription configurations |

### testNotificationConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /testNotificationConfiguration | Test a notification configuration |

### updateNotificationConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateNotificationConfiguration | Update a notification subscription configuration |

## Enhanced Skill Content
## Question Mapping

- "How do I set up webhook notifications for my Adyen account?" -> POST /createNotificationConfiguration
- "How do I list all my notification configurations?" -> POST /getNotificationConfigurationList
- "How do I get details of a specific notification configuration?" -> POST /getNotificationConfiguration
- "How do I update the webhook URL for a notification?" -> POST /updateNotificationConfiguration
- "How do I delete a notification configuration?" -> POST /deleteNotificationConfigurations
- "How do I test if my webhook endpoint is reachable?" -> POST /testNotificationConfiguration
- "How do I enable or disable a notification configuration?" -> POST /updateNotificationConfiguration (set `active: true/false`)
- "How do I change the HMAC signature key for webhook verification?" -> POST /updateNotificationConfiguration
- "How do I subscribe to specific event types?" -> POST /createNotificationConfiguration (set `eventConfigs`)
- "How do I delete multiple notification configurations at once?" -> POST /deleteNotificationConfigurations (pass array of `notificationIds`)
- "How do I verify my webhook endpoint is correctly processing events?" -> POST /testNotificationConfiguration (with specific `eventTypes`)
- "How do I change the authentication credentials for my webhook endpoint?" -> POST /updateNotificationConfiguration (update `notifyUsername`/`notifyPassword`)
- "How do I switch my webhook to use a newer API version?" -> POST /updateNotificationConfiguration (update `apiVersion`)
- "What SSL protocol is my notification using?" -> POST /getNotificationConfiguration (check `sslProtocol` in response)

## Response Tips

- **All endpoints**: Every response includes `pspReference` (unique request ID for support), `resultCode` (operation outcome), and `invalidFields` (array of validation errors -- check this even on 200 responses).
- **Configuration responses** (`create`, `get`, `update`): The full `configurationDetails` object is returned, including the assigned `notificationId` -- always capture this ID for future operations.
- **List response**: Returns `configurations` as a flat array of all configs -- there is no pagination; the full list is always returned.
- **Test response**: Contains parallel arrays: `okMessages` for successful event deliveries, `errorMessages` for failures, and `exchangeMessages` with raw request/response pairs for debugging.
- **Error responses** (400-500): Expect `invalidFields` with per-field error details; 422 indicates valid JSON but semantically invalid configuration (e.g., unreachable URL).

## Anomaly Flags

- **Non-empty `invalidFields` on 200**: The operation may have partially succeeded but some fields were ignored or invalid -- always surface this to the user.
- **`resultCode` is not "OK"**: Even on HTTP 200, the business-level result may indicate failure; check and surface the actual value.
- **Empty `okMessages` after test**: If `/testNotificationConfiguration` returns no `okMessages` but has `errorMessages`, the webhook endpoint is unreachable or rejecting events -- flag immediately.
- **`active: false` on retrieved config**: Surface when a configuration is disabled, as this means no notifications are being delivered.
- **HTTP 422 on create/update**: The notification URL is likely unreachable or the SSL configuration is incompatible -- suggest the user verify the endpoint is publicly accessible.
- **Missing `hmacSignatureKey` in response**: If the key is empty or absent, webhook payloads cannot be verified for authenticity -- recommend setting one.
- **`sslProtocol` set to older versions**: Flag if using anything below TLSv1.2 as a security concern.

## Playbook

### 1. Set Up a New Webhook Endpoint

1. Call `POST /createNotificationConfiguration` with `configurationDetails` containing your `notifyURL`, `notifyUsername`, `notifyPassword`, and desired `eventConfigs`.
2. Capture the `notificationId` from the response's `configurationDetails`.
3. Check `invalidFields` in the response -- if non-empty, fix the flagged fields and retry.
4. Call `POST /testNotificationConfiguration` with the new `notificationId` to verify connectivity.
5. Review `okMessages` and `errorMessages` in the test response to confirm your endpoint handles events correctly.

### 2. Audit and Review All Configurations

1. Call `POST /getNotificationConfigurationList` (no body required) to retrieve all configurations.
2. For each entry in `configurations`, check `active` status and `notifyURL`.
3. For any configuration needing deeper inspection, call `POST /getNotificationConfiguration` with its `notificationId`.
4. Run `POST /testNotificationConfiguration` against each active configuration to verify endpoints are still responsive.
5. Surface any configs with `active: false`, missing HMAC keys, or outdated `apiVersion`.

### 3. Rotate Webhook Credentials

1. Call `POST /getNotificationConfiguration` with the target `notificationId` to retrieve current settings.
2. Call `POST /updateNotificationConfiguration` with the full `configurationDetails`, updating `notifyPassword`, `notifyUsername`, and/or `hmacSignatureKey` with new values.
3. Verify `invalidFields` is empty in the response.
4. Call `POST /testNotificationConfiguration` to confirm the endpoint still accepts connections with the new credentials.

### 4. Decommission a Webhook Endpoint

1. Call `POST /getNotificationConfiguration` to confirm the configuration details before deletion.
2. Optionally call `POST /updateNotificationConfiguration` to set `active: false` first, allowing a grace period.
3. Call `POST /deleteNotificationConfigurations` with the `notificationIds` array containing the target ID(s).
4. Verify `resultCode` is "OK" and `invalidFields` is empty.
5. Call `POST /getNotificationConfigurationList` to confirm the configuration no longer appears.

### 5. Troubleshoot Failed Notifications

1. Call `POST /getNotificationConfiguration` with the `notificationId` to verify the config is `active: true` and the `notifyURL` is correct.
2. Call `POST /testNotificationConfiguration` with the `notificationId` and optionally specific `eventTypes` that are failing.
3. Inspect `exchangeMessages` in the response for the raw HTTP request sent and response received.
4. If `errorMessages` indicate connectivity issues, verify the endpoint is publicly accessible and SSL is configured correctly.
5. If the endpoint responds but rejects events, check `notifyUsername`/`notifyPassword` and HMAC verification logic against the `hmacSignatureKey`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
