---
name: novu-api
description: "Novu API skill. Use when working with Novu for environments, events, notifications. Covers 95 endpoints."
version: 1.0.0
generator: lapsh
---

# Novu API
API version: 3.14.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.novu.co

## Setup
1. Set your API key in the appropriate header
2. GET /v1/environments -- verify access
3. POST /v1/environments -- create first environments

## Endpoints

95 endpoints across 14 groups. See references/api-spec.lap for full details.

### environments
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/environments | Create an environment |
| GET | /v1/environments | List all environments |
| PUT | /v1/environments/{environmentId} | Update an environment |
| DELETE | /v1/environments/{environmentId} | Delete an environment |
| GET | /v2/environments/{environmentId}/tags | List environment tags |
| POST | /v2/environments/{targetEnvironmentId}/publish | Publish resources to target environment |
| POST | /v2/environments/{targetEnvironmentId}/diff | Compare resources between environments |

### events
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/events/trigger | Trigger event |
| POST | /v1/events/trigger/bulk | Bulk trigger event |
| POST | /v1/events/trigger/broadcast | Broadcast event to all |
| DELETE | /v1/events/trigger/{transactionId} | Cancel triggered event |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/notifications | List all events |
| GET | /v1/notifications/{notificationId} | Retrieve an event |

### integrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/integrations | List all integrations |
| POST | /v1/integrations | Create an integration |
| GET | /v1/integrations/active | List active integrations |
| PUT | /v1/integrations/{integrationId} | Update an integration |
| DELETE | /v1/integrations/{integrationId} | Delete an integration |
| POST | /v1/integrations/{integrationId}/auto-configure | Auto-configure an integration for inbound webhooks |
| POST | /v1/integrations/{integrationId}/set-primary | Update integration as primary |
| POST | /v1/integrations/chat/oauth | Generate chat OAuth URL |

### contexts
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/contexts | Create a context |
| GET | /v2/contexts | List all contexts |
| PATCH | /v2/contexts/{type}/{id} | Update a context |
| GET | /v2/contexts/{type}/{id} | Retrieve a context |
| DELETE | /v2/contexts/{type}/{id} | Delete a context |

### subscribers
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/subscribers/bulk | Bulk create subscribers |
| PUT | /v1/subscribers/{subscriberId}/credentials | Update provider credentials |
| PATCH | /v1/subscribers/{subscriberId}/credentials | Upsert provider credentials |
| DELETE | /v1/subscribers/{subscriberId}/credentials/{providerId} | Delete provider credentials |
| PATCH | /v1/subscribers/{subscriberId}/online-status | Update subscriber online status |
| GET | /v1/subscribers/{subscriberId}/notifications/feed | Retrieve subscriber notifications |
| GET | /v1/subscribers/{subscriberId}/notifications/unseen | Retrieve unseen notifications count |
| POST | /v1/subscribers/{subscriberId}/messages/mark-as | Update notifications state |
| POST | /v1/subscribers/{subscriberId}/messages/mark-all | Update all notifications state |
| POST | /v1/subscribers/{subscriberId}/messages/{messageId}/actions/{type} | Update notification action status |
| GET | /v2/subscribers | Search subscribers |
| POST | /v2/subscribers | Create a subscriber |
| GET | /v2/subscribers/{subscriberId} | Retrieve a subscriber |
| PATCH | /v2/subscribers/{subscriberId} | Update a subscriber |
| DELETE | /v2/subscribers/{subscriberId} | Delete a subscriber |
| GET | /v2/subscribers/{subscriberId}/preferences | Retrieve subscriber preferences |
| PATCH | /v2/subscribers/{subscriberId}/preferences | Update subscriber preferences |
| PATCH | /v2/subscribers/{subscriberId}/preferences/bulk | Bulk update subscriber preferences |
| GET | /v2/subscribers/{subscriberId}/subscriptions | Retrieve subscriber subscriptions |

### layouts
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/layouts | Create a layout |
| GET | /v2/layouts | List all layouts |
| PUT | /v2/layouts/{layoutId} | Update a layout |
| GET | /v2/layouts/{layoutId} | Retrieve a layout |
| DELETE | /v2/layouts/{layoutId} | Delete a layout |
| POST | /v2/layouts/{layoutId}/duplicate | Duplicate a layout |
| POST | /v2/layouts/{layoutId}/preview | Generate layout preview |
| GET | /v2/layouts/{layoutId}/usage | Get layout usage |

### messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/messages | List all messages |
| DELETE | /v1/messages/{messageId} | Delete a message |
| DELETE | /v1/messages/transaction/{transactionId} | Delete messages by transactionId |

### topics
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/topics/{topicKey}/subscribers/{externalSubscriberId} | Check topic subscriber |
| GET | /v2/topics | List all topics |
| POST | /v2/topics | Create a topic |
| GET | /v2/topics/{topicKey} | Retrieve a topic |
| PATCH | /v2/topics/{topicKey} | Update a topic |
| DELETE | /v2/topics/{topicKey} | Delete a topic |
| GET | /v2/topics/{topicKey}/subscriptions | List topic subscriptions |
| POST | /v2/topics/{topicKey}/subscriptions | Create topic subscriptions |
| DELETE | /v2/topics/{topicKey}/subscriptions | Delete topic subscriptions |
| GET | /v2/topics/{topicKey}/subscriptions/{identifier} | Retrieve a topic subscription |
| PATCH | /v2/topics/{topicKey}/subscriptions/{identifier} | Update a topic subscription |

### workflows
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/workflows | Create a workflow |
| GET | /v2/workflows | List all workflows |
| PUT | /v2/workflows/{workflowId}/sync | Sync a workflow |
| PUT | /v2/workflows/{workflowId} | Update a workflow |
| GET | /v2/workflows/{workflowId} | Retrieve a workflow |
| DELETE | /v2/workflows/{workflowId} | Delete a workflow |
| PATCH | /v2/workflows/{workflowId} | Update a workflow |
| GET | /v2/workflows/{workflowId}/steps/{stepId} | Retrieve workflow step |

### channel-connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/channel-connections | List all channel connections |
| POST | /v1/channel-connections | Create a channel connection |
| GET | /v1/channel-connections/{identifier} | Retrieve a channel connection |
| PATCH | /v1/channel-connections/{identifier} | Update a channel connection |
| DELETE | /v1/channel-connections/{identifier} | Delete a channel connection |

### channel-endpoints
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/channel-endpoints | List all channel endpoints |
| POST | /v1/channel-endpoints | Create a channel endpoint |
| GET | /v1/channel-endpoints/{identifier} | Retrieve a channel endpoint |
| PATCH | /v1/channel-endpoints/{identifier} | Update a channel endpoint |
| DELETE | /v1/channel-endpoints/{identifier} | Delete a channel endpoint |

### translations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/translations/upload | Upload translation files |
| POST | /v2/translations | Create a translation |
| GET | /v2/translations/master-json | Retrieve master translations JSON |
| POST | /v2/translations/master-json | Import master translations JSON |
| POST | /v2/translations/master-json/upload | Upload master translations JSON file |
| GET | /v2/translations/group/{resourceType}/{resourceId} | Retrieve a translation group |
| GET | /v2/translations/{resourceType}/{resourceId}/{locale} | Retrieve a translation |
| DELETE | /v2/translations/{resourceType}/{resourceId}/{locale} | Delete a translation |
| DELETE | /v2/translations/{resourceType}/{resourceId} | Delete a translation group |

### inbound-webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/inbound-webhooks/delivery-providers/{environmentId}/{integrationId} | Track activity and engagement events |

## Enhanced Skill Content
## Question Mapping

- "How do I send a notification to a user?" -> POST /v1/events/trigger
- "How do I send the same notification to all subscribers?" -> POST /v1/events/trigger/broadcast
- "How do I send multiple notifications at once?" -> POST /v1/events/trigger/bulk
- "How do I cancel a pending notification?" -> DELETE /v1/events/trigger/{transactionId}
- "How do I create a new subscriber?" -> POST /v2/subscribers
- "How do I check a subscriber's unread notification count?" -> GET /v1/subscribers/{subscriberId}/notifications/unseen
- "How do I mark notifications as read for a subscriber?" -> POST /v1/subscribers/{subscriberId}/messages/mark-all
- "How do I set up a new email/SMS/push integration?" -> POST /v1/integrations
- "How do I create a notification workflow with steps?" -> POST /v2/workflows
- "How do I add subscribers to a topic for group notifications?" -> POST /v2/topics/{topicKey}/subscriptions
- "How do I manage a subscriber's notification preferences per channel?" -> PATCH /v2/subscribers/{subscriberId}/preferences
- "How do I promote workflows from dev to production?" -> POST /v2/environments/{targetEnvironmentId}/publish
- "How do I see what changed between environments before promoting?" -> POST /v2/environments/{targetEnvironmentId}/diff
- "How do I connect a subscriber's Slack or Discord credentials?" -> PUT /v1/subscribers/{subscriberId}/credentials
- "How do I add translations for a workflow?" -> POST /v2/translations

## Response Tips

- **Events**: Trigger responses return `acknowledged: bool` and `transactionId` -- store the transactionId to cancel or trace the notification later.
- **Notifications/Messages**: Paginated via `page` (0-indexed) and `limit` (default 10); check `hasMore` to continue fetching. Notification detail nests `jobs`, `subscriber`, and `template` as expanded objects.
- **Subscribers (v2)**: Cursor-paginated using `after`/`before` strings and `next`/`previous` pointers; `totalCountCapped: true` means the real count exceeds the cap.
- **Topics (v2)**: Same cursor pagination as subscribers. Topic creation can return either 200 (already existed with `failIfExists: false`) or 201 (newly created).
- **Workflows**: Listed via offset pagination (`offset`/`limit`); detail responses include an `issues` map and `status` field that indicate validation problems.
- **Integrations**: Active integrations (`GET /v1/integrations/active`) returns a filtered subset; the full list from `GET /v1/integrations` includes soft-deleted entries (`deleted: true`).
- **Layouts**: Offset-paginated with `totalCount`; the `controls` and `variables` fields may be null on layouts that have no dynamic content.
- **Translations**: Upload endpoints return `successfulUploads`/`failedUploads` counts and an `errors` array -- always check both even on 200.
- **Environments**: Diff and publish responses include a `summary` object and per-resource `results` array for granular change tracking.
- **Errors**: All endpoints share the same error code set (400-503). 422 typically means payload validation failure; 429 means rate limited; 409 means a conflict (duplicate key, name collision).

## Anomaly Flags

- **429 responses**: Rate limit hit. Surface the retry-after timing and recommend batching or throttling requests.
- **Workflow `issues` map is non-empty**: The workflow has validation problems that may prevent it from triggering correctly. Surface the specific issues to the user.
- **Workflow `status` is not "active"**: Workflow exists but will not fire. Alert the user that notifications will silently fail.
- **`totalCountCapped: true` in cursor-paginated responses**: The actual count exceeds the API cap. Warn that subscriber/topic counts are approximate.
- **Integration `active: false` or `deleted: true`**: Integration exists but is not delivering. Flag if the user is trying to send via a channel with no active integration.
- **Trigger response `acknowledged: false` or non-empty `error` array**: The event was received but not processed. Surface the error strings immediately.
- **Translation `outdatedLocales` is non-empty**: Some translations are stale relative to the source content. Flag for the user to update.
- **`failedUploads > 0` on translation upload**: Partial failure. Surface the `errors` array so the user can fix and retry.
- **Environment diff shows resources with breaking changes**: Before publish, alert the user to review changes that could affect production notifications.

## Playbook

### 1. Send a notification to a single user

1. Ensure the subscriber exists: `GET /v2/subscribers/{subscriberId}`. If 404, create with `POST /v2/subscribers`.
2. Verify the workflow is active: `GET /v2/workflows/{workflowId}`. Check that `active: true` and `issues` is empty.
3. Confirm at least one integration is active for the target channel: `GET /v1/integrations/active`.
4. Trigger the event: `POST /v1/events/trigger` with `name` (workflow identifier), `to` (subscriberId), and `payload` (template variables).
5. Store the returned `transactionId`. Check `acknowledged: true` and `error: []`.
6. Optionally verify delivery: `GET /v1/notifications` filtered by `transactionId`.

### 2. Set up group notifications with topics

1. Create a topic: `POST /v2/topics` with a unique `key` and display `name`.
2. Add subscribers to the topic: `POST /v2/topics/{topicKey}/subscriptions` with `subscriberIds` array.
3. Verify membership: `GET /v2/topics/{topicKey}/subscriptions` and page through results.
4. Send to the entire topic: `POST /v1/events/trigger` with `to` set to `{ type: "Topic", topicKey: "your-key" }`.
5. To remove subscribers later: `DELETE /v2/topics/{topicKey}/subscriptions` with `subscriberIds`.

### 3. Promote workflows from development to production

1. List environments: `GET /v1/environments` to get the dev and production environment IDs.
2. Preview changes: `POST /v2/environments/{prodEnvId}/diff` with `sourceEnvironmentId` set to the dev environment.
3. Review the `resources` array in the diff response for added, modified, or removed items.
4. Dry run the publish: `POST /v2/environments/{prodEnvId}/publish` with `dryRun: true` to validate without applying.
5. Execute the publish: `POST /v2/environments/{prodEnvId}/publish` with `dryRun: false`. Check `results` for per-resource success/failure.

### 4. Configure a new integration and connect a subscriber

1. Create the integration: `POST /v1/integrations` with `providerId` (e.g., "sendgrid"), `channel` (e.g., "email"), `credentials`, and `active: true`.
2. Optionally auto-configure: `POST /v1/integrations/{integrationId}/auto-configure`.
3. If this should be the default for its channel: `POST /v1/integrations/{integrationId}/set-primary`.
4. For chat/push channels, set subscriber credentials: `PUT /v1/subscribers/{subscriberId}/credentials` with the `providerId` and channel-specific `credentials` (tokens, webhook URLs).
5. Test by triggering a notification: `POST /v1/events/trigger` targeting that subscriber and a workflow using that channel.

### 5. Manage subscriber notification preferences

1. Fetch current preferences: `GET /v2/subscribers/{subscriberId}/preferences`. The response splits into `global` (all workflows) and `workflows` (per-workflow overrides).
2. Update a single workflow preference: `PATCH /v2/subscribers/{subscriberId}/preferences` with `workflowId` and `channels` (e.g., `{ email: true, sms: false }`).
3. Bulk update multiple workflows at once: `PATCH /v2/subscribers/{subscriberId}/preferences/bulk` with a `preferences` array containing `workflowId` and `channels` for each.
4. Verify the update: `GET /v2/subscribers/{subscriberId}/preferences` again and confirm the changes are reflected.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
