---
name: invoices
description: "Invoices API skill. Use when working with Invoices for invoicing. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# Invoices
API version: 2.6

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v2/invoicing/invoices -- verify access
3. POST /v2/invoicing/invoices -- create first invoices

## Endpoints

22 endpoints across 1 groups. See references/api-spec.lap for full details.

### invoicing
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/invoicing/invoices | Create draft invoice |
| GET | /v2/invoicing/invoices | List invoices |
| POST | /v2/invoicing/invoices/{invoice_id}/send | Send invoice |
| POST | /v2/invoicing/invoices/{invoice_id}/remind | Send invoice reminder |
| POST | /v2/invoicing/invoices/{invoice_id}/cancel | Cancel sent invoice |
| POST | /v2/invoicing/invoices/{invoice_id}/payments | Record payment for invoice |
| DELETE | /v2/invoicing/invoices/{invoice_id}/payments/{transaction_id} | Delete external payment |
| POST | /v2/invoicing/invoices/{invoice_id}/refunds | Record refund for invoice |
| DELETE | /v2/invoicing/invoices/{invoice_id}/refunds/{transaction_id} | Delete external refund |
| POST | /v2/invoicing/invoices/{invoice_id}/generate-qr-code | Generate QR code |
| POST | /v2/invoicing/generate-next-invoice-number | Generate invoice number |
| GET | /v2/invoicing/invoices/{invoice_id} | Show invoice details |
| PUT | /v2/invoicing/invoices/{invoice_id} | Fully update invoice |
| DELETE | /v2/invoicing/invoices/{invoice_id} | Delete invoice |
| POST | /v2/invoicing/search-invoices | Search for invoices |
| GET | /v2/invoicing/templates | List templates |
| POST | /v2/invoicing/templates | Create template |
| GET | /v2/invoicing/templates/{template_id} | Show template details |
| PUT | /v2/invoicing/templates/{template_id} | Fully update template |
| DELETE | /v2/invoicing/templates/{template_id} | Delete template |
| GET | /v2/invoicing/accounting-sync/merchant/connections | List Connections. |
| GET | /v2/invoicing/accounting-sync/invoices/{id}/connections | List Connection Status for an Invoice. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new invoice?" -> POST /v2/invoicing/invoices
- "Show me all my invoices" -> GET /v2/invoicing/invoices
- "Get the details of a specific invoice" -> GET /v2/invoicing/invoices/{invoice_id}
- "How do I send an invoice to a customer?" -> POST /v2/invoicing/invoices/{invoice_id}/send
- "Send a payment reminder for an overdue invoice" -> POST /v2/invoicing/invoices/{invoice_id}/remind
- "How do I cancel an invoice?" -> POST /v2/invoicing/invoices/{invoice_id}/cancel
- "Record a payment against an invoice" -> POST /v2/invoicing/invoices/{invoice_id}/payments
- "Issue a refund on a paid invoice" -> POST /v2/invoicing/invoices/{invoice_id}/refunds
- "Delete a draft invoice I no longer need" -> DELETE /v2/invoicing/invoices/{invoice_id}
- "Find all unpaid invoices for a specific customer" -> POST /v2/invoicing/search-invoices
- "What is the next available invoice number?" -> POST /v2/invoicing/generate-next-invoice-number
- "Generate a QR code so a customer can pay an invoice" -> POST /v2/invoicing/invoices/{invoice_id}/generate-qr-code
- "Update the line items or due date on an existing invoice" -> PUT /v2/invoicing/invoices/{invoice_id}
- "List my invoice templates" -> GET /v2/invoicing/templates
- "Check if my accounting software is connected" -> GET /v2/invoicing/accounting-sync/merchant/connections

## Response Tips

- **Invoice CRUD** (create/get/update): Response nests `amount.breakdown` with sub-maps for `item_total`, `discount`, `tax_total`, `shipping`, and `custom` -- always drill into `breakdown` for line-level totals rather than relying on the top-level `value`.
- **List & Search** (GET /invoices, POST /search-invoices): Paginated via `total_pages`, `total_items`, and `items[]`. Default `page_size` is 20; set `total_required=true` to get accurate counts. Follow `links[]` for next/prev pages.
- **Action endpoints** (send/remind/cancel): Send returns 200 or 202 with a HATEOAS link; remind and cancel return 204 with no body. A 202 means the send is queued, not completed.
- **Payment & Refund recording**: Returns only `{payment_id}` or `{refund_id}` on success. Fetch the full invoice afterward to see updated `due_amount` and transaction history.
- **Delete endpoints** (invoice/payment/refund/template): All return 204 with no body. Absence of an error confirms success.
- **Templates**: GET list response includes `addresses`, `emails`, and `phones` at the top level alongside `templates[]` -- these are the merchant's stored contact details, not template metadata.
- **Accounting sync**: Returns `connections[]` or `connection_status[]` arrays. An empty array means no integrations are linked.

## Anomaly Flags

- **422 Unprocessable Entity**: Surface immediately -- indicates business rule violations (e.g., sending an already-cancelled invoice, recording payment on a draft). Include the error detail in your response.
- **Invoice status mismatches**: If a user tries to send/remind/cancel but the invoice status doesn't permit it (DRAFT can't be reminded, PAID can't be cancelled), flag the current status and suggest the correct action.
- **due_amount vs amount discrepancy**: After recording a payment, if `due_amount.value` is still greater than zero, proactively note the remaining balance.
- **202 Accepted on send**: Alert the user that the invoice email is queued, not delivered. Suggest checking back or watching for webhook confirmation.
- **Empty items array**: If an invoice is created or updated with no `items[]`, warn that the invoice will appear blank to the recipient.
- **Sandbox base URL**: The spec targets `api-m.sandbox.paypal.com`. Flag if the user appears to intend production use -- they need `api-m.paypal.com` instead.
- **Missing total_required on list calls**: If paginating large result sets without `total_required=true`, warn that `total_items` and `total_pages` may be absent or zero.
- **Deprecated or unusual payment methods**: If the user records a payment with method OTHER, suggest using a more specific method for better reporting.

## Playbook

### 1. Create and Send an Invoice

1. Call `POST /v2/invoicing/generate-next-invoice-number` to get the next available invoice number.
2. Call `POST /v2/invoicing/invoices` with `detail` (including the invoice number, currency, payment term, and due date), `items[]` with line items, and `primary_recipients` with the customer's billing info.
3. Verify the response status is `DRAFT` and review the computed `amount.breakdown` for correctness.
4. Call `POST /v2/invoicing/invoices/{invoice_id}/send` with optional `subject` and `note` to email it to the recipient.
5. If you receive 202, the email is queued. Fetch the invoice with `GET /v2/invoicing/invoices/{invoice_id}` to confirm status changed to `SENT`.

### 2. Record a Payment and Handle Partial Payments

1. Call `GET /v2/invoicing/invoices/{invoice_id}` to check the current `status` and `due_amount`.
2. Call `POST /v2/invoicing/invoices/{invoice_id}/payments` with `method` (e.g., `BANK_TRANSFER`), `amount` for the payment value, and optionally `payment_date` and `note`.
3. Capture the returned `payment_id` for your records.
4. Call `GET /v2/invoicing/invoices/{invoice_id}` again. If `due_amount.value` is `"0.00"`, status will be `PAID`. If a balance remains, status will be `PARTIALLY_PAID` -- decide whether to follow up.
5. To reverse a mistaken payment, call `DELETE /v2/invoicing/invoices/{invoice_id}/payments/{transaction_id}`.

### 3. Search and Follow Up on Overdue Invoices

1. Call `POST /v2/invoicing/search-invoices` with `status: ["SENT", "PARTIALLY_PAID"]` and `due_date_range` ending before today's date, plus `total_required: true`.
2. Iterate through `items[]` in the response. For each overdue invoice, note the `id`, `due_amount`, and recipient info.
3. For each overdue invoice, call `POST /v2/invoicing/invoices/{invoice_id}/remind` with a `note` explaining the overdue status.
4. If pagination is needed (`total_pages > 1`), repeat the search with incremented `page` values.

### 4. Create and Use an Invoice Template

1. Call `POST /v2/invoicing/templates` with `name`, `template_info` (containing default `detail`, `items[]`, `configuration`), and `settings` for display preferences.
2. Capture the returned template `id`.
3. To create an invoice from the template, call `GET /v2/invoicing/templates/{template_id}` to retrieve the template data.
4. Pass the `template_info` fields into `POST /v2/invoicing/invoices`, overriding recipient and date fields as needed.
5. Send the invoice via `POST /v2/invoicing/invoices/{invoice_id}/send`.

### 5. Cancel an Invoice and Issue a Refund

1. If the invoice status is `SENT` or `SCHEDULED`, call `POST /v2/invoicing/invoices/{invoice_id}/cancel` with an optional `note` explaining the reason. Confirm 204 response.
2. If the invoice is already `PAID` or `PARTIALLY_PAID`, cancellation is not allowed. Instead, call `POST /v2/invoicing/invoices/{invoice_id}/refunds` with `method` and the refund `amount`.
3. Capture the returned `refund_id`.
4. Call `GET /v2/invoicing/invoices/{invoice_id}` to verify the status updated to `REFUNDED` or `PARTIALLY_REFUNDED`.
5. To undo a refund recorded in error, call `DELETE /v2/invoicing/invoices/{invoice_id}/refunds/{transaction_id}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
