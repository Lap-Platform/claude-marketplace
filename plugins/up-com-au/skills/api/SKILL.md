---
name: up-api
description: "Up API skill. Use when working with Up for accounts, attachments, categories. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Up API
API version: v1

## Auth
Bearer bearer

## Base URL
https://api.up.com.au/api/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /accounts -- verify access
3. POST /transactions/{transactionId}/relationships/tags -- create first tags

## Endpoints

20 endpoints across 7 groups. See references/api-spec.lap for full details.

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | List accounts |
| GET | /accounts/{id} | Retrieve account |
| GET | /accounts/{accountId}/transactions | List transactions by account |

### attachments
| Method | Path | Description |
|--------|------|-------------|
| GET | /attachments | List attachments |
| GET | /attachments/{id} | Retrieve attachment |

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories | List categories |
| GET | /categories/{id} | Retrieve category |

### transactions
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /transactions/{transactionId}/relationships/category | Categorize transaction |
| POST | /transactions/{transactionId}/relationships/tags | Add tags to transaction |
| DELETE | /transactions/{transactionId}/relationships/tags | Remove tags from transaction |
| GET | /transactions | List transactions |
| GET | /transactions/{id} | Retrieve transaction |

### util
| Method | Path | Description |
|--------|------|-------------|
| GET | /util/ping | Ping |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags | List tags |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks | List webhooks |
| POST | /webhooks | Create webhook |
| GET | /webhooks/{id} | Retrieve webhook |
| DELETE | /webhooks/{id} | Delete webhook |
| POST | /webhooks/{webhookId}/ping | Ping webhook |
| GET | /webhooks/{webhookId}/logs | List webhook logs |

## Enhanced Skill Content
## Question Mapping

- "What bank accounts do I have?" -> GET /accounts
- "Show me details for a specific account" -> GET /accounts/{id}
- "What are my recent transactions?" -> GET /transactions
- "Show transactions for a specific account" -> GET /accounts/{accountId}/transactions
- "Look up a specific transaction" -> GET /transactions/{id}
- "What categories are available?" -> GET /categories
- "What subcategories exist under a parent category?" -> GET /categories?filter[parent]={parent}
- "Change the category of a transaction" -> PATCH /transactions/{transactionId}/relationships/category
- "Add tags to a transaction" -> POST /transactions/{transactionId}/relationships/tags
- "Remove tags from a transaction" -> DELETE /transactions/{transactionId}/relationships/tags
- "List all my tags" -> GET /tags
- "Is the API working right now?" -> GET /util/ping
- "List my webhooks" -> GET /webhooks
- "Create a new webhook" -> POST /webhooks
- "Check webhook delivery logs" -> GET /webhooks/{webhookId}/logs

## Response Tips

- **Accounts, transactions, tags, webhooks, attachments**: Paginated via `links.next`/`links.prev`. Always check `links.next` for more pages. Control page size with `page[size]`.
- **Single resource endpoints** (GET by id): Return `{data: ...}` with the full resource object -- no pagination wrapper.
- **Category/tag mutations** (PATCH category, POST/DELETE tags): Return 204 No Content with an empty body. A successful response means the operation worked -- do not attempt to parse a body.
- **Webhook creation and ping**: Return 201 Created with the new resource in `{data: ...}`.
- **Ping utility**: Returns `{meta: {id, statusEmoji}}` -- the emoji confirms API health visually.

## Anomaly Flags

- **401 on /util/ping**: Bearer token is invalid or expired. Surface immediately -- all subsequent calls will also fail.
- **Empty `links.next`**: End of paginated results reached. If the user expected more data, flag that filters or date ranges may be too narrow.
- **204 with unexpected body**: If a tag or category mutation returns a body, the API behavior may have changed -- flag for investigation.
- **Repeated pagination loops**: If `links.next` returns the same URL twice, break the loop and alert -- possible API pagination bug.
- **Webhook log failures**: When GET /webhooks/{id}/logs shows repeated delivery failures, proactively surface the failing webhook URL and suggest checking the endpoint.
- **Large page sizes**: If the user requests `page[size]` above typical limits (e.g., 100+), warn that the API may cap or reject the value silently.

## Playbook

### Categorize and Tag a Transaction

1. GET /transactions to find the target transaction, note its `id`
2. GET /categories to find the desired category `id`
3. PATCH /transactions/{transactionId}/relationships/category with `{data: {type: "categories", id: "<categoryId>"}}`
4. GET /tags to find or confirm existing tag IDs
5. POST /transactions/{transactionId}/relationships/tags with `{data: [{type: "tags", id: "<tagId>"}]}`

### Export All Transactions for an Account

1. GET /accounts to list accounts, note the target `accountId`
2. GET /accounts/{accountId}/transactions with desired `page[size]`
3. Follow `links.next` repeatedly until `links.next` is null
4. Aggregate all `data` arrays from each page into a single list

### Set Up and Verify a Webhook

1. POST /webhooks with `{data: {attributes: {url: "https://your-endpoint.com/hook", description: "My webhook"}}}`
2. Note the returned webhook `id`
3. POST /webhooks/{webhookId}/ping to send a test event
4. GET /webhooks/{webhookId}/logs to confirm the ping was delivered successfully
5. If logs show failure, check the target URL and retry

### Health Check and Authentication Validation

1. GET /util/ping with your Bearer token
2. If 200 with `statusEmoji`, the API and your credentials are working
3. If 401, regenerate or refresh your API token before making further calls

### Audit and Clean Up Webhooks

1. GET /webhooks to list all registered webhooks
2. For each webhook, GET /webhooks/{id} to review its configuration
3. GET /webhooks/{webhookId}/logs to check recent delivery history
4. DELETE /webhooks/{id} for any webhooks with dead endpoints or that are no longer needed


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
