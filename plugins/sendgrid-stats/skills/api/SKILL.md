---
name: twilio-sendgrid-statistics-api
description: "Twilio SendGrid Statistics API skill. Use when working with Twilio SendGrid Statistics for browsers, categories, clients. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio SendGrid Statistics API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.sendgrid.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v3/browsers/stats -- verify access

## Endpoints

10 endpoints across 7 groups. See references/api-spec.lap for full details.

### browsers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/browsers/stats | Retrieve email statistics by browser. |

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/categories | Retrieve all categories |
| GET | /v3/categories/stats | Retrieve Email Statistics for Categories |
| GET | /v3/categories/stats/sums | Retrieve sums of email stats for each category. |

### clients
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/clients/stats | Retrieve email statistics by client type. |
| GET | /v3/clients/{client_type}/stats | Retrieve stats by a specific client type. |

### devices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/devices/stats | Retrieve email statistics by device type. |

### geo
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/geo/stats | Retrieve email statistics by country and state/province. |

### mailbox_providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/mailbox_providers/stats | Retrieve email statistics by mailbox provider. |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/stats | Retrieve global email statistics |

## Enhanced Skill Content
## Question Mapping

- "What browsers are my recipients using to open emails?" -> GET /v3/browsers/stats
- "Show me email stats broken down by category for the last month" -> GET /v3/categories/stats
- "What email categories do I have?" -> GET /v3/categories
- "Which category has the most delivered emails?" -> GET /v3/categories/stats/sums
- "What's my overall email performance this week?" -> GET /v3/stats
- "Which email clients are my subscribers using?" -> GET /v3/clients/stats
- "How do my emails perform specifically on Outlook?" -> GET /v3/clients/{client_type}/stats
- "What devices are people reading my emails on?" -> GET /v3/devices/stats
- "Which countries are my email opens coming from?" -> GET /v3/geo/stats
- "How are my emails performing across different mailbox providers like Gmail and Yahoo?" -> GET /v3/mailbox_providers/stats
- "Compare my transactional vs marketing email stats side by side" -> GET /v3/categories/stats (with categories param)
- "Give me a daily breakdown of all email stats for January" -> GET /v3/stats (with aggregated_by=day)
- "What are the top 5 categories by delivery count?" -> GET /v3/categories/stats/sums (with sort_by_metric=delivered, limit=5)
- "How did email engagement in Germany trend over the past quarter?" -> GET /v3/geo/stats (with country param)

## Response Tips

- **Global stats** (`/v3/stats`): Returns array of date-keyed objects, each containing a `stats` array with metric maps (delivered, opens, clicks, bounces, etc.). Always check for empty arrays when no data exists for the date range.
- **Categories** (`/v3/categories`): Returns flat list of category name objects. Supports pagination via `limit`/`offset` -- default limit is 50. Watch for 400 errors on malformed requests.
- **Category sums** (`/v3/categories/stats/sums`): Returns `{date, stats}` with pre-aggregated totals. Use `sort_by_metric` and `sort_by_direction` to rank categories server-side rather than sorting client-side.
- **Browser/Client/Device/Geo/Mailbox stats**: All follow the same response shape as global stats -- date-keyed arrays with nested `stats` maps. Filter params (e.g., `browsers`, `country`, `mailbox_providers`) accept specific values to narrow results.
- **Aggregation**: All stat endpoints accept `aggregated_by` (day, week, month). Omitting it returns daily granularity. Weekly aggregation aligns to Monday starts.

## Anomaly Flags

- **Empty stats arrays**: Surface when a date range returns zero data points -- may indicate misconfigured tracking or inactive sending.
- **High bounce/spam rates**: When bounce or spam_report metrics exceed 5% of delivered volume, proactively warn about sender reputation risk.
- **Category proliferation**: Flag when `/v3/categories` returns an unusually high count (100+), as excessive categories degrade dashboard usability.
- **Missing date coverage**: If response dates have gaps within the requested range, flag potential data pipeline delays.
- **Pagination truncation**: When results hit the `limit` ceiling (especially the default 50 on categories or 5 on sums), warn that additional data exists beyond the current page.
- **on-behalf-of header usage**: This common field impersonates a subuser -- surface a note when it's set, as stats will reflect that subuser's data, not the parent account's.
- **Zero opens with non-zero deliveries**: May indicate open tracking is disabled or recipients are blocking tracking pixels.

## Playbook

### 1. Audit Email Performance for a Date Range

1. Call `GET /v3/stats` with `start_date` and `end_date` to get overall metrics.
2. Review delivered, opens, clicks, bounces, and unsubscribes in the response.
3. If bounce rate is high, call `GET /v3/mailbox_providers/stats` with the same date range to identify which providers are rejecting mail.
4. Call `GET /v3/geo/stats` to check if delivery issues are region-specific.

### 2. Compare Category Performance

1. Call `GET /v3/categories` to list all active categories.
2. Call `GET /v3/categories/stats/sums` with `start_date`, `sort_by_metric=delivered`, `sort_by_direction=desc` to rank categories.
3. For the top categories, call `GET /v3/categories/stats` with `categories` set to those names and `aggregated_by=week` to see trends over time.
4. Compare open rates (opens / delivered) across categories to identify the best-performing content types.

### 3. Analyze Recipient Technology Profile

1. Call `GET /v3/clients/stats` with `start_date` to see the client type breakdown (webmail, phone, tablet, desktop).
2. For the dominant client type, call `GET /v3/clients/{client_type}/stats` to get detailed stats.
3. Call `GET /v3/browsers/stats` to understand which browsers webmail users prefer.
4. Call `GET /v3/devices/stats` to see device-level engagement patterns.
5. Use these insights to prioritize email template testing for the most common environments.

### 4. Geographic Engagement Report

1. Call `GET /v3/geo/stats` with `start_date` and `aggregated_by=month` for a high-level regional view.
2. Narrow down by setting `country` to specific markets of interest and switch to `aggregated_by=day` for granular trends.
3. Cross-reference with `GET /v3/mailbox_providers/stats` filtered to region-dominant providers (e.g., Mail.ru for Russia, GMX for Germany).
4. Surface any countries with disproportionately high bounce rates for deliverability investigation.

### 5. Paginate Through All Categories

1. Call `GET /v3/categories` with `limit=50` and `offset=0`.
2. If 50 results are returned, increment `offset` by 50 and repeat.
3. Continue until fewer than `limit` results are returned, indicating the final page.
4. Compile the full category list, then use it to drive targeted calls to `GET /v3/categories/stats` for any category subset of interest.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
