---
name: hookdeck-admin-rest-api
description: "Hookdeck Admin REST API skill. Use when working with Hookdeck Admin REST for issue-triggers, attempts, bookmarks. Covers 101 endpoints."
version: 1.0.0
generator: lapsh
---

# Hookdeck Admin REST API
API version: 1.0.0

## Auth
Bearer bearer | Bearer basic

## Base URL
https://api.hookdeck.com/2024-09-01

## Setup
1. Set Authorization header with your Bearer token
2. GET /issue-triggers -- verify access
3. POST /issue-triggers -- create first issue-triggers

## Endpoints

101 endpoints across 14 groups. See references/api-spec.lap for full details.

### issue-triggers
| Method | Path | Description |
|--------|------|-------------|
| GET | /issue-triggers | Get issue triggers |
| POST | /issue-triggers | Create an issue trigger |
| PUT | /issue-triggers | Create or update an issue trigger |
| GET | /issue-triggers/{id} | Get a single issue trigger |
| PUT | /issue-triggers/{id} | Update an issue trigger |
| DELETE | /issue-triggers/{id} | Delete an issue trigger |
| PUT | /issue-triggers/{id}/disable | Disable an issue trigger |
| PUT | /issue-triggers/{id}/enable | Enable an issue trigger |

### attempts
| Method | Path | Description |
|--------|------|-------------|
| GET | /attempts | Get attempts |
| GET | /attempts/{id} | Get a single attempt |

### bookmarks
| Method | Path | Description |
|--------|------|-------------|
| GET | /bookmarks | Get bookmarks |
| POST | /bookmarks | Create a bookmark |
| GET | /bookmarks/{id} | Get a single bookmark |
| PUT | /bookmarks/{id} | Update a bookmark |
| DELETE | /bookmarks/{id} | Delete a bookmark |
| GET | /bookmarks/{id}/raw_body | Get a bookmark raw body data |
| POST | /bookmarks/{id}/trigger | Trigger a bookmark |

### destinations
| Method | Path | Description |
|--------|------|-------------|
| GET | /destinations | Get destinations |
| POST | /destinations | Create a destination |
| PUT | /destinations | Update or create a destination |
| GET | /destinations/{id} | Get a destination |
| PUT | /destinations/{id} | Update a destination |
| DELETE | /destinations/{id} | Delete a destination |
| PUT | /destinations/{id}/disable | Disable a destination |
| PUT | /destinations/{id}/archive | Disable a destination |
| PUT | /destinations/{id}/enable | Enable a destination |
| PUT | /destinations/{id}/unarchive | Enable a destination |

### bulk
| Method | Path | Description |
|--------|------|-------------|
| GET | /bulk/events/retry | Get events bulk retries |
| POST | /bulk/events/retry | Create an events bulk retry |
| GET | /bulk/events/retry/plan | Generate an events bulk retry plan |
| GET | /bulk/events/retry/{id} | Get an events bulk retry |
| POST | /bulk/events/retry/{id}/cancel | Cancel an events bulk retry |
| GET | /bulk/ignored-events/retry | Get ignored events bulk retries |
| POST | /bulk/ignored-events/retry | Create an ignored events bulk retry |
| GET | /bulk/ignored-events/retry/plan | Generate an ignored events bulk retry plan |
| GET | /bulk/ignored-events/retry/{id} | Get an ignored events bulk retry |
| POST | /bulk/ignored-events/retry/{id}/cancel | Cancel an ignored events bulk retry |
| GET | /bulk/requests/retry | Get request bulk retries |
| POST | /bulk/requests/retry | Create a requests bulk retry |
| GET | /bulk/requests/retry/plan | Generate a requests bulk retry plan |
| GET | /bulk/requests/retry/{id} | Get a requests bulk retry |
| POST | /bulk/requests/retry/{id}/cancel | Cancel a requests bulk retry |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Get events |
| GET | /events/{id} | Get an event |
| GET | /events/{id}/raw_body | Get a event raw body data |
| POST | /events/{id}/retry | Retry an event |
| PUT | /events/{id}/mute | Mute an event |

### integrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /integrations | Get integrations |
| POST | /integrations | Create an integration |
| GET | /integrations/{id} | Get an integration |
| PUT | /integrations/{id} | Update an integration |
| DELETE | /integrations/{id} | Delete an integration |
| PUT | /integrations/{id}/attach/{source_id} | Attach an integration to a source |
| PUT | /integrations/{id}/detach/{source_id} | Detach an integration from a source |

### issues
| Method | Path | Description |
|--------|------|-------------|
| GET | /issues | Get issues |
| GET | /issues/count | Get the number of issues |
| GET | /issues/{id} | Get a single issue |
| PUT | /issues/{id} | Update issue |
| DELETE | /issues/{id} | Dismiss an issue |

### requests
| Method | Path | Description |
|--------|------|-------------|
| GET | /requests | Get requests |
| GET | /requests/{id} | Get a request |
| GET | /requests/{id}/raw_body | Get a request raw body data |
| POST | /requests/{id}/retry | Retry a request |
| GET | /requests/{id}/events | Get request events |
| GET | /requests/{id}/ignored_events | Get request ignored events |

### sources
| Method | Path | Description |
|--------|------|-------------|
| GET | /sources | Get sources |
| POST | /sources | Create a source |
| PUT | /sources | Update or create a source |
| GET | /sources/{id} | Get a source |
| PUT | /sources/{id} | Update a source |
| DELETE | /sources/{id} | Delete a source |
| PUT | /sources/{id}/disable | Disable a source |
| PUT | /sources/{id}/archive | Disable a source |
| PUT | /sources/{id}/enable | Enable a source |
| PUT | /sources/{id}/unarchive | Enable a source |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| PUT | /notifications/webhooks | Toggle webhook notifications for the project |

### teams
| Method | Path | Description |
|--------|------|-------------|
| POST | /teams/current/custom_domains | Add a custom domain to the project |
| GET | /teams/current/custom_domains | List all custom domains and their verification statuses for the project |
| DELETE | /teams/current/custom_domains/{domain_id} | Removes a custom domain from the project |

### transformations
| Method | Path | Description |
|--------|------|-------------|
| GET | /transformations | Get transformations |
| POST | /transformations | Create a transformation |
| PUT | /transformations | Update or create a transformation |
| GET | /transformations/{id} | Get a transformation |
| DELETE | /transformations/{id} | Delete a transformation |
| PUT | /transformations/{id} | Update a transformation |
| PUT | /transformations/run | Test a transformation code |
| GET | /transformations/{id}/executions | Get transformation executions |
| GET | /transformations/{id}/executions/{execution_id} | Get a transformation execution |

### connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /connections | Get connections |
| POST | /connections | Create a connection |
| PUT | /connections | Update or create a connection |
| GET | /connections/count | Count connections |
| GET | /connections/{id} | Get a single connection |
| PUT | /connections/{id} | Update a connection |
| DELETE | /connections/{id} | Delete a connection |
| PUT | /connections/{id}/disable | Disable a connection |
| PUT | /connections/{id}/archive | Disable a connection |
| PUT | /connections/{id}/enable | Enable a connection |
| PUT | /connections/{id}/unarchive | Enable a connection |
| PUT | /connections/{id}/pause | Pause a connection |
| PUT | /connections/{id}/unpause | Unpause a connection |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my webhook connections?" -> GET /connections
- "How do I retry a failed event?" -> POST /events/{id}/retry
- "How do I set up a Stripe integration?" -> POST /integrations (with provider: "STRIPE")
- "How do I create a new webhook connection from a source to a destination?" -> POST /connections
- "How do I check what issues are currently open?" -> GET /issues (with status filter)
- "How do I bulk retry all failed events matching a filter?" -> POST /bulk/events/retry
- "How do I pause a connection without deleting it?" -> PUT /connections/{id}/pause
- "How do I write and test a transformation before deploying it?" -> PUT /transformations/run
- "How do I see the raw payload body of a request?" -> GET /requests/{id}/raw_body
- "How do I set up Slack notifications for delivery failures?" -> POST /issue-triggers (type: "delivery", channels.slack)
- "How do I disable a source temporarily?" -> PUT /sources/{id}/disable
- "How do I see all delivery attempts for a specific event?" -> GET /attempts (with event_id filter)
- "How do I check how many connections I have?" -> GET /connections/count
- "How do I replay a bookmark to test my endpoint?" -> POST /bookmarks/{id}/trigger
- "How do I add a custom domain to my team?" -> POST /teams/current/custom_domains

## Response Tips

- **List endpoints** (events, connections, sources, etc.): All return `{pagination, count, models}`. Use `next`/`prev` cursor strings for pagination -- not page numbers. `count` is total matching, `models` is the current page array.
- **Single-resource GETs**: Return the object directly (not wrapped). Check for `410 Gone` on sources/destinations/connections, which indicates archived resources.
- **Bulk operations**: Return a progress object with `in_progress`, `progress` (0-1 float), `estimated_count`, `completed_count`, and `failed_count`. Poll the GET endpoint to track completion.
- **Delete endpoints**: Return only `{id}` on success, not the full object.
- **Issue triggers/issues**: `disabled_at` and `dismissed_at` are null when active -- presence of a timestamp means disabled/dismissed.
- **Transformations run**: Returns `console` array (log output) and transformed `request` -- use `log_level` to filter noise.
- **Connections**: Embed full `source` and `destination` objects inline -- no need for separate lookups.

## Anomaly Flags

- **Bulk retry `failed_count` > 0**: Some events in the batch could not be retried. Surface this immediately and suggest inspecting individual failures.
- **`disabled_at` populated on sources/destinations/connections**: The resource is disabled and not processing webhooks. Alert the user if they query or create events targeting disabled resources.
- **`410 Gone` on resource lookup**: The source, destination, or connection has been archived. Suggest unarchiving via the `/unarchive` endpoint rather than recreating.
- **Issue count growing**: If `GET /issues/count` returns a count higher than a previous check, proactively flag new issues and suggest reviewing `GET /issues` with `status=OPENED`.
- **`rejection_cause` on requests**: Non-empty rejection cause means inbound webhooks are being dropped. Surface the cause (verification failure, disabled source, etc.).
- **Bulk operation stalled**: If `in_progress` is true but `progress` has not changed across polls, flag a potential stall and suggest cancellation via `/cancel`.
- **`is_large_payload` flag**: When true on event/request data, the body was truncated. Advise using the `/raw_body` endpoint for the complete payload.
- **`422 Unprocessable Entity` errors**: Indicate schema validation failures. Surface the response body, which typically contains field-level error details.

## Playbook

### Set Up a Complete Webhook Pipeline

1. Create a source: `POST /sources` with a name and optional verification config
2. Create a destination: `POST /destinations` with the target URL and HTTP method
3. Create a connection linking them: `POST /connections` with `source_id` and `destination_id`, plus any filter/transform rules
4. Copy the source `url` from the response and configure it in your upstream provider
5. Verify events are flowing: `GET /events?source_id={source_id}&limit=5`

### Investigate and Retry Failed Deliveries

1. List failed events: `GET /events?status=FAILED&order_by=last_attempt_at&dir=desc`
2. Pick an event and inspect attempts: `GET /attempts?event_id={event_id}`
3. Check the response status and error code on each attempt to diagnose the failure
4. If the destination issue is fixed, retry: `POST /events/{id}/retry`
5. For many failures, use bulk retry: first plan with `GET /bulk/events/retry/plan?query[status]=FAILED`, then execute with `POST /bulk/events/retry`

### Add a Transformation to Modify Payloads

1. Write transformation code and test it: `PUT /transformations/run` with inline `code` and a sample `request` object
2. Review the response `request` (transformed output) and `console` logs
3. Once satisfied, save it: `POST /transformations` with `name` and `code`
4. Attach it to a connection by updating the connection rules: `PUT /connections/{id}` with `rules` array including the transformation reference

### Set Up Alerting for Delivery Issues

1. Create an issue trigger for delivery failures: `POST /issue-triggers` with `type: "delivery"` and your preferred channel (Slack, email, or OpsGenie)
2. Verify it was created: `GET /issue-triggers`
3. Optionally create triggers for other types: `"transformation"` (code errors) and `"backpressure"` (queue buildup)
4. Monitor issues: `GET /issues?status=OPENED` to see active alerts
5. Acknowledge or resolve: `PUT /issues/{id}` with `status: "ACKNOWLEDGED"` or `"RESOLVED"`

### Manage Source Lifecycle (Disable, Archive, Restore)

1. To temporarily stop ingestion: `PUT /sources/{id}/disable` -- requests will be rejected
2. To re-enable: `PUT /sources/{id}/enable`
3. To archive (soft delete): `PUT /sources/{id}/archive` -- returns 410 on direct access
4. To restore an archived source: `PUT /sources/{id}/unarchive`
5. To permanently delete: `DELETE /sources/{id}` -- this cannot be undone


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
