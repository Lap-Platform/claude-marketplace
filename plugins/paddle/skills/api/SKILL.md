---
name: paddle-api
description: "Paddle API skill. Use when working with Paddle for customers, adjustments, client-tokens. Covers 87 endpoints."
version: 1.0.0
generator: lapsh
---

# Paddle API
API version: 1.0

## Auth
Bearer Bearer

## Base URL
https://sandbox-api.paddle.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /adjustments -- verify access
3. POST /customers/{customer_id}/addresses -- create first addresses

## Endpoints

87 endpoints across 18 groups. See references/api-spec.lap for full details.

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /customers/{customer_id}/addresses | List addresses for a customer |
| POST | /customers/{customer_id}/addresses | Create an address for a customer |
| GET | /customers/{customer_id}/addresses/{address_id} | Get an address for a customer |
| PATCH | /customers/{customer_id}/addresses/{address_id} | Update an address for a customer |
| GET | /customers/{customer_id}/businesses | List businesses for a customer |
| POST | /customers/{customer_id}/businesses | Create a business for a customer |
| GET | /customers/{customer_id}/businesses/{business_id} | Get a business for a customer |
| PATCH | /customers/{customer_id}/businesses/{business_id} | Update a business for a customer |
| GET | /customers | List customers |
| POST | /customers | Create a customer |
| GET | /customers/{customer_id} | Get a customer |
| PATCH | /customers/{customer_id} | Update a customer |
| GET | /customers/{customer_id}/credit-balances | List credit balances for a customer |
| POST | /customers/{customer_id}/auth-token | Generate an authentication token for a customer |
| POST | /customers/{customer_id}/portal-sessions | Create a customer portal session |
| GET | /customers/{customer_id}/payment-methods | List payment methods for a customer |
| GET | /customers/{customer_id}/payment-methods/{payment_method_id} | Get a payment method for a customer |
| DELETE | /customers/{customer_id}/payment-methods/{payment_method_id} | Delete a payment method for a customer |

### adjustments
| Method | Path | Description |
|--------|------|-------------|
| GET | /adjustments | List adjustments |
| POST | /adjustments | Create an adjustment |
| GET | /adjustments/{adjustment_id}/credit-note | Get a PDF credit note for an adjustment |

### client-tokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /client-tokens | List client-side tokens |
| POST | /client-tokens | Create a client-side token |
| GET | /client-tokens/{client_token_id} | Get a client-side token |
| PATCH | /client-tokens/{client_token_id} | Update a client-side token |

### discount-groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /discount-groups | List discount groups |
| POST | /discount-groups | Create a discount group |
| GET | /discount-groups/{discount_group_id} | Get a discount group |
| PATCH | /discount-groups/{discount_group_id} | Update a discount group |

### discounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /discounts | List discounts |
| POST | /discounts | Create a discount |
| GET | /discounts/{discount_id} | Get a discount |
| PATCH | /discounts/{discount_id} | Update a discount |

### event-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /event-types | List events types |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | List events |

### ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /ips | Get Paddle IP addresses |

### notification-settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification-settings | List notification settings |
| POST | /notification-settings | Create a notification setting |
| GET | /notification-settings/{notification_setting_id} | Get a notification setting |
| PATCH | /notification-settings/{notification_setting_id} | Update a notification setting |
| DELETE | /notification-settings/{notification_setting_id} | Delete a notification setting |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /notifications | List notifications |
| GET | /notifications/{notification_id} | Get a notification |
| GET | /notifications/{notification_id}/logs | List logs for a notification |
| POST | /notifications/{notification_id}/replay | Replay a notification |

### prices
| Method | Path | Description |
|--------|------|-------------|
| GET | /prices | List prices |
| POST | /prices | Create a price |
| GET | /prices/{price_id} | Get a price |
| PATCH | /prices/{price_id} | Update a price |

### pricing-preview
| Method | Path | Description |
|--------|------|-------------|
| POST | /pricing-preview | Preview prices |

### products
| Method | Path | Description |
|--------|------|-------------|
| GET | /products | List products |
| POST | /products | Create a product |
| GET | /products/{product_id} | Get a product |
| PATCH | /products/{product_id} | Update a product |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /reports | List reports |
| POST | /reports | Create a report |
| GET | /reports/{report_id} | Get a report |
| GET | /reports/{report_id}/download-url | Get a CSV file for a report |

### simulation-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /simulation-types | List simulation types |

### simulations
| Method | Path | Description |
|--------|------|-------------|
| GET | /simulations | List simulations |
| POST | /simulations | Create a simulation |
| GET | /simulations/{simulation_id} | Get a simulation |
| PATCH | /simulations/{simulation_id} | Update a simulation |
| GET | /simulations/{simulation_id}/runs | List runs for a simulation |
| POST | /simulations/{simulation_id}/runs | Create a run for a simulation |
| GET | /simulations/{simulation_id}/runs/{simulation_run_id} | Get a run for a simulation |
| GET | /simulations/{simulation_id}/runs/{simulation_run_id}/events | List events for a simulation run |
| GET | /simulations/{simulation_id}/runs/{simulation_run_id}/events/{simulation_event_id} | Get an event for a simulation run |
| POST | /simulations/{simulation_id}/runs/{simulation_run_id}/events/{simulation_event_id}/replay | Replay an event for a simulation run |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions | List subscriptions |
| GET | /subscriptions/{subscription_id} | Get a subscription |
| PATCH | /subscriptions/{subscription_id} | Update a subscription |
| POST | /subscriptions/{subscription_id}/cancel | Cancel a subscription |
| POST | /subscriptions/{subscription_id}/pause | Pause a subscription |
| POST | /subscriptions/{subscription_id}/resume | Resume a paused subscription |
| POST | /subscriptions/{subscription_id}/activate | Activate a trialing subscription |
| GET | /subscriptions/{subscription_id}/update-payment-method-transaction | Get a transaction to update payment method |
| PATCH | /subscriptions/{subscription_id}/preview | Preview an update to a subscription |
| POST | /subscriptions/{subscription_id}/charge | Create a one-time charge for a subscription |
| POST | /subscriptions/{subscription_id}/charge/preview | Preview a one-time charge for a subscription |

### transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /transactions | List transactions |
| POST | /transactions | Create a transaction |
| GET | /transactions/{transaction_id} | Get a transaction |
| PATCH | /transactions/{transaction_id} | Update a transaction |
| POST | /transactions/preview | Preview a transaction |
| POST | /transactions/{transaction_id}/revise | Revise customer information on a billed or completed transaction |
| GET | /transactions/{transaction_id}/invoice | Get a PDF invoice for a transaction |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my customers?" -> GET /customers
- "How do I find a customer by email?" -> GET /customers (use `email` filter or `search` param)
- "How do I create a refund for a transaction?" -> POST /adjustments (action: "refund", transaction_id required)
- "What subscriptions does a customer have?" -> GET /subscriptions (filter by `customer_id`)
- "How do I cancel a subscription?" -> POST /subscriptions/{subscription_id}/cancel
- "How do I pause and later resume a subscription?" -> POST /subscriptions/{subscription_id}/pause, then POST /subscriptions/{subscription_id}/resume
- "How do I preview pricing before checkout?" -> POST /pricing-preview
- "How do I get an invoice PDF for a transaction?" -> GET /transactions/{transaction_id}/invoice
- "What payment methods does a customer have saved?" -> GET /customers/{customer_id}/payment-methods
- "How do I create a product with a recurring price?" -> POST /products, then POST /prices (with `billing_cycle`)
- "How do I set up a webhook to receive events?" -> POST /notification-settings
- "How do I check what IP addresses Paddle sends webhooks from?" -> GET /ips
- "How do I preview what happens if I change subscription items?" -> PATCH /subscriptions/{subscription_id}/preview
- "How do I download a credit note for an adjustment?" -> GET /adjustments/{adjustment_id}/credit-note
- "How do I apply a discount to a subscription?" -> PATCH /subscriptions/{subscription_id} (set `discount` field)

## Response Tips

- **All list endpoints**: Paginated via `meta.pagination` -- use `after` cursor (from `meta.pagination.next`) and `per_page` to page through; check `has_more` to know when to stop. Never rely on `estimated_total` for exact counts.
- **Single resource endpoints**: Entity is always in `data` (object), metadata in `meta.request_id` -- log `request_id` for Paddle support debugging.
- **Mutation endpoints (POST/PATCH)**: Return the full updated entity in `data` on success (201 or 200); 204 means success with no body (DELETE operations).
- **Subscriptions**: Deeply nested -- `items`, `scheduled_change`, `billing_details`, `management_urls`, and `current_billing_period` are all nested objects; always check `scheduled_change` for pending future changes.
- **Transactions**: Use `include` param to sideload related entities (`customer`, `address`, `business`, `discount`, `adjustments`) to avoid extra calls.
- **Preview endpoints**: Return the same shape as the real mutation but with additional `immediate_transaction`, `next_transaction`, `update_summary` fields showing financial impact.
- **Errors**: Non-2xx responses include error details -- watch for 409 (conflict/state violation), 404 (invalid ID), and 422 (validation failure).

## Anomaly Flags

- **Subscription `scheduled_change` is non-null**: A cancellation, pause, or plan change is pending -- surface this before making further modifications, as it may conflict.
- **Discount `usage_limit` approaching `times_used`**: The discount is nearly exhausted and may stop applying to new checkouts.
- **Discount `expires_at` is in the past or imminent**: Surface when a discount is referenced but expired or expiring within 24 hours.
- **Notification delivery failures**: When `GET /notifications` returns entries with `status` other than "delivered" or `times_attempted` is high, the webhook endpoint may be failing.
- **Subscription status is "past_due"**: Payment collection failed -- surface immediately as revenue is at risk; check `next_billed_at` and payment methods.
- **Transaction `status` is "ready" but not "completed"**: The checkout was created but never finished -- may indicate abandoned carts.
- **Credit balance exists**: When `GET /customers/{id}/credit-balances` returns non-zero balances, mention this when creating transactions as credits apply automatically.
- **Archived entities referenced**: If a product, price, or discount has `status: "archived"`, flag it when it appears in active subscriptions or new transaction creation attempts.
- **`collection_mode` mismatch**: If a subscription uses `manual` collection mode, agent should flag that invoices must be collected outside Paddle's automatic billing.

## Playbook

### 1. Create a New Product with Pricing and a Checkout

1. Create the product: `POST /products` with `name`, `tax_category` (e.g., "saas" or "digital-goods")
2. Create a price for the product: `POST /prices` with `product_id` from step 1, `description`, `unit_price` (object with `amount` and `currency_code`), and optionally `billing_cycle` for recurring
3. Preview the pricing: `POST /pricing-preview` with `items: [{price_id, quantity}]` and optional `address` to verify tax calculations
4. Create a transaction to start checkout: `POST /transactions` with `items: [{price_id, quantity}]` and `customer_id` (or let Paddle create a new customer)
5. Use the `checkout.url` from the transaction response to direct the customer to pay

### 2. Process a Refund

1. Look up the transaction: `GET /transactions/{transaction_id}` (include `adjustments` to check for prior refunds)
2. Verify the transaction status is "completed" or "billed" -- refunds only work on completed payments
3. Create the adjustment: `POST /adjustments` with `action: "refund"`, `transaction_id`, and `reason`; set `type: "partial"` and specify `items` for partial refunds, or `type: "full"` for a complete refund
4. Confirm the adjustment status in the response -- it may be "pending" before funds are returned
5. Optionally retrieve the credit note: `GET /adjustments/{adjustment_id}/credit-note` for the PDF URL

### 3. Set Up Webhook Notifications

1. Check available event types: `GET /event-types` to see all subscribable events
2. Verify your endpoint IP allowlist if needed: `GET /ips` returns Paddle's outbound CIDRs
3. Create the notification setting: `POST /notification-settings` with `description`, `type: "url"`, `destination` (your HTTPS endpoint), and `subscribed_events` (array of event type names)
4. Note the `endpoint_secret_key` from the response -- use this to verify webhook signatures
5. Test delivery: create a simulation with `POST /simulations`, add a run with `POST /simulations/{id}/runs`, then check `GET /notifications` to verify delivery

### 4. Modify a Subscription (Upgrade/Downgrade)

1. Get the current subscription: `GET /subscriptions/{subscription_id}` to review current `items` and `billing_cycle`
2. Preview the change: `PATCH /subscriptions/{subscription_id}/preview` with updated `items` array and `proration_billing_mode` (e.g., "prorated_immediately") -- review `update_summary` and `immediate_transaction` for financial impact
3. If the preview looks correct, apply the change: `PATCH /subscriptions/{subscription_id}` with the same body (minus `/preview`)
4. Check the response for `scheduled_change` -- some changes take effect at next billing period rather than immediately
5. If an immediate charge was created, verify the transaction status in the response `items` and `billing_details`

### 5. Customer Self-Service Portal Setup

1. Look up the customer: `GET /customers` filtered by `email` or `GET /customers/{customer_id}`
2. Generate an auth token: `POST /customers/{customer_id}/auth-token` -- returns a short-lived `customer_auth_token`
3. Create a portal session: `POST /customers/{customer_id}/portal-sessions` with optional `subscription_ids` to scope which subscriptions are visible
4. Use the `urls` from the portal session response to redirect the customer -- these are pre-authenticated deep links to manage subscriptions, update payment methods, and view invoices


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
