---
name: braze-endpoints
description: "Braze Endpoints API skill. Use when working with Braze Endpoints for email, campaigns, sends. Covers 68 endpoints."
version: 1.0.0
generator: lapsh
---

# Braze Endpoints

## Auth
ApiKey Authorization in header

## Base URL
https://{{instance_url}}

## Setup
1. Set your API key in the appropriate header
2. GET /email/hard_bounces -- verify access
3. POST /email/status -- create first status

## Endpoints

68 endpoints across 17 groups. See references/api-spec.lap for full details.

### email
| Method | Path | Description |
|--------|------|-------------|
| GET | /email/hard_bounces | Query Hard Bounced Emails |
| GET | /email/unsubscribes | Query List of Unsubscribed Email Addresses |
| POST | /email/status | Change Email Subscription Status |
| POST | /email/bounce/remove | Remove Hard Bounced Emails |
| POST | /email/spam/remove | Remove Email Addresses from Spam List |
| POST | /email/blacklist | Blacklist Email Addresses |

### campaigns
| Method | Path | Description |
|--------|------|-------------|
| GET | /campaigns/data_series | Campaign Analytics |
| GET | /campaigns/details | Campaign Details |
| GET | /campaigns/list | Campaign List |
| POST | /campaigns/trigger/schedule/delete | Delete Scheduled API Triggered Campaigns |
| POST | /campaigns/trigger/schedule/create | Schedule API Triggered Campaigns |
| POST | /campaigns/trigger/schedule/update | Update Scheduled API Triggered Campaigns |
| POST | /campaigns/trigger/send | Sending Campaign Messages via API Triggered Delivery |

### sends
| Method | Path | Description |
|--------|------|-------------|
| GET | /sends/data_series | Send Analytics |
| POST | /sends/id/create | Create Send IDs For Message Send Tracking |

### canvas
| Method | Path | Description |
|--------|------|-------------|
| GET | /canvas/data_series | Canvas Data Series Analytics |
| GET | /canvas/data_summary | Canvas Data Analytics Summary |
| GET | /canvas/details | Canvas Details |
| GET | /canvas/list | Canvas List |
| POST | /canvas/trigger/schedule/delete | Delete Scheduled API-Triggered Canvases |
| POST | /canvas/trigger/schedule/create | Schedule API Triggered Canvases |
| POST | /canvas/trigger/schedule/update | Update Scheduled API Triggered Canvases |
| POST | /canvas/trigger/send | Sending Canvas Messages via API Triggered Delivery |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events/list | Custom Events List |
| GET | /events/data_series | Custom Events Analytics |

### kpi
| Method | Path | Description |
|--------|------|-------------|
| GET | /kpi/new_users/data_series | Daily New Users by Date |
| GET | /kpi/dau/data_series | Daily Active Users by Date |
| GET | /kpi/mau/data_series | Monthly Active Users for Last 30 Days |
| GET | /kpi/uninstalls/data_series | KPIs for Daily App Uninstalls by Date |

### feed
| Method | Path | Description |
|--------|------|-------------|
| GET | /feed/data_series | News Feed Card Analytics |
| GET | /feed/details | News Feed Cards Details |
| GET | /feed/list | News Feed Cards List |

### purchases
| Method | Path | Description |
|--------|------|-------------|
| GET | /purchases/product_list | Product IDs List |

### segments
| Method | Path | Description |
|--------|------|-------------|
| GET | /segments/list | Segment List |
| GET | /segments/data_series | Segment Analytics |
| GET | /segments/details | Segment Details |

### sessions
| Method | Path | Description |
|--------|------|-------------|
| GET | /sessions/data_series | App Sessions by Time |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users/export/ids | User Profile Export by Identifier |
| POST | /users/export/segment | User Profile Export by Segment |
| POST | /users/export/global_control_group | User Profile Export by Global Control Group |
| POST | /users/external_ids/remove | External ID Remove |
| POST | /users/external_ids/rename | External ID Rename |
| POST | /users/alias/new | Create New User Aliases |
| POST | /users/delete | User Delete |
| POST | /users/identify | Identify Users |
| POST | /users/track | User Track |

### messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /messages/scheduled_broadcasts | Get Upcoming Scheduled Campaigns and Canvases |
| POST | /messages/schedule/delete | Delete Scheduled Messages |
| POST | /messages/schedule/create | Create Scheduled Messages |
| POST | /messages/schedule/update | Update Scheduled Messages |
| POST | /messages/send | Sending Messages Immediately via API Only |

### transactional
| Method | Path | Description |
|--------|------|-------------|
| POST | /transactional/v1/campaigns/YOUR_CAMPAIGN_ID_HERE/send | Sending Transactional Email via API Triggered Delivery |

### sms
| Method | Path | Description |
|--------|------|-------------|
| GET | /sms/invalid_phone_numbers | Query Invalid Phone Numbers |
| POST | /sms/invalid_phone_numbers/remove | Remove Invalid Phone Numbers |

### subscription
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscription/status/get | List User's  Subscription Group Status - Email |
| GET | /subscription/user/status | List User's Subscription Group - Email |
| POST | /subscription/status/set | Update User's Subscription Group Status - Email |
| GET | /subscription/status/get | List User's  Subscription Group Status - SMS |
| GET | /subscription/user/status | List User's Subscription Group - SMS |
| POST | /subscription/status/set | Update User's Subscription Group Status - SMS |

### content_blocks
| Method | Path | Description |
|--------|------|-------------|
| GET | /content_blocks/list | List Available Content Blocks |
| GET | /content_blocks/info | See Content Block Information |
| POST | /content_blocks/create | Create Content Block |
| POST | /content_blocks/update | Update Content Block |

### templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /templates/email/list | List Available Email Templates |
| GET | /templates/email/info | See Email Template Information |
| POST | /templates/email/create | Create Email Template |
| POST | /templates/email/update | Update Email Template |

## Enhanced Skill Content
## Question Mapping

- "Which emails have hard bounced recently?" -> GET /email/hard_bounces
- "Who unsubscribed from our emails this month?" -> GET /email/unsubscribes
- "How do I resubscribe a user or change their email subscription status?" -> POST /email/status
- "Remove an email from the bounce list" -> POST /email/bounce/remove
- "What campaigns are running and how are they performing?" -> GET /campaigns/list then GET /campaigns/data_series
- "Show me the details and analytics for a specific Canvas" -> GET /canvas/details then GET /canvas/data_series
- "How many daily active users do we have?" -> GET /kpi/dau/data_series
- "What is our new user growth trend?" -> GET /kpi/new_users/data_series
- "Export user profiles by external ID or email" -> POST /users/export/ids
- "Export all users in a segment" -> POST /users/export/segment
- "Schedule a campaign to send later" -> POST /campaigns/trigger/schedule/create
- "Cancel a scheduled broadcast" -> POST /messages/schedule/delete
- "Track custom events and purchases for users" -> POST /users/track
- "List all subscription groups a user belongs to" -> GET /subscription/user/status
- "Create or update an email template" -> POST /templates/email/create or POST /templates/email/update

## Response Tips

- **List endpoints** (campaigns/list, canvas/list, segments/list, feed/list, events/list, content_blocks/list, templates/email/list): Paginated via `page` or `offset`/`limit` params; always check if more pages exist before stopping iteration.
- **Data series endpoints** (*/data_series): Return time-bucketed arrays; confirm `length`, `ending_at`, and `unit` align to avoid empty or truncated series.
- **Export endpoints** (users/export/*): Large exports return asynchronously via `callback_endpoint`; poll or listen for the callback rather than expecting inline data.
- **Schedule endpoints** (*/schedule/create, */schedule/update): Return a `schedule_id` on creation; persist it because deletion and updates require it.
- **Subscription endpoints**: Identical paths serve both email and SMS contexts -- differentiate by whether `email` or `phone` is provided in params.
- **Error responses**: Braze returns `errors` arrays with message strings; check HTTP status and the `errors` field together since 4xx can carry multiple validation failures.

## Anomaly Flags

- **Rate limit headers**: Surface `X-RateLimit-Remaining` and `X-RateLimit-Reset` when remaining calls drop below 10% of the limit; warn before the agent queues more requests.
- **Deprecation notices**: Flag any `Deprecation` or `Sunset` response headers; Braze periodically retires endpoints and these headers appear before removal.
- **Empty data series**: Alert when a data_series call returns zero data points despite a valid date range -- likely indicates a wrong `app_id`, `segment_id`, or `campaign_id`.
- **Export callback missing**: Warn if `POST /users/export/segment` is called without a `callback_endpoint` -- the response will not contain user data inline and results may be unrecoverable.
- **Bounce/spam removal on non-bounced addresses**: Flag when `POST /email/bounce/remove` or `POST /email/spam/remove` returns a no-op response, indicating the address was not on the list.
- **Bulk user delete**: Proactively confirm before executing `POST /users/delete` since it is irreversible and accepts arrays of IDs.
- **Schedule in the past**: Warn if a schedule/create or schedule/update call sets a time that has already passed -- Braze may reject or send immediately.

## Playbook

### 1. Investigate and Fix Email Deliverability Issues

1. `GET /email/hard_bounces` with the relevant date range to identify bounced addresses.
2. `GET /email/unsubscribes` for the same period to separate voluntary unsubscribes from technical bounces.
3. For addresses that bounced due to transient issues, call `POST /email/bounce/remove` to re-enable delivery.
4. For addresses flagged as spam, call `POST /email/spam/remove` after confirming re-consent.
5. Optionally call `POST /email/status` to set `subscription_state` back to `subscribed` for cleaned addresses.

### 2. Launch and Monitor a Scheduled Campaign

1. `GET /campaigns/list` to find the target campaign and note its `campaign_id`.
2. `POST /sends/id/create` to generate a unique `send_id` for tracking this particular send.
3. `POST /campaigns/trigger/schedule/create` with the `campaign_id`, audience, and desired schedule.
4. Persist the returned `schedule_id` for later modification or cancellation.
5. After the send window, call `GET /campaigns/data_series` and `GET /sends/data_series` to review performance metrics.

### 3. Export and Analyze a User Segment

1. `GET /segments/list` to browse available segments and pick the target `segment_id`.
2. `GET /segments/details` to confirm segment size and filters before exporting.
3. `POST /users/export/segment` with the `segment_id`, desired `fields_to_export`, and a `callback_endpoint`.
4. Wait for the callback or poll the callback URL to retrieve the export file.
5. `GET /segments/data_series` to overlay segment growth trends alongside the exported snapshot.

### 4. Manage Subscription Group Opt-ins Across Email and SMS

1. `GET /subscription/user/status` with the user's `external_id` to see all current subscription group memberships.
2. To check a specific group, call `GET /subscription/status/get` with the `subscription_group_id` and `email` (or `phone` for SMS).
3. To opt a user in or out, call `POST /subscription/status/set` with the group ID, target `subscription_state`, and the user's email array or phone array.
4. Re-query `GET /subscription/user/status` to confirm the change took effect.

### 5. Create and Deploy an Email Template with Content Blocks

1. `GET /content_blocks/list` to check for existing reusable blocks (headers, footers, legal copy).
2. If needed, `POST /content_blocks/create` to build new shared content blocks.
3. `POST /templates/email/create` referencing the content blocks via Liquid tags in the `body` field.
4. `GET /templates/email/info` with the returned `email_template_id` to verify the template rendered correctly.
5. Use the template ID in a subsequent `POST /messages/send` or campaign trigger to deploy.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
