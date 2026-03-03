---
name: billingo-api-v3
description: "Billingo API v3 API skill. Use when working with Billingo API v3 for bank-accounts, currencies, document-blocks. Covers 31 endpoints."
version: 1.0.0
generator: lapsh
---

# Billingo API v3
API version: 3.0.7

## Auth
ApiKey X-API-KEY in header

## Base URL
https://api.billingo.hu/v3

## Setup
1. Set your API key in the appropriate header
2. GET /bank-accounts -- verify access
3. POST /bank-accounts -- create first bank-accounts

## Endpoints

31 endpoints across 8 groups. See references/api-spec.lap for full details.

### bank-accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /bank-accounts | List all bank account |
| POST | /bank-accounts | Create a bank account |
| GET | /bank-accounts/{id} | Retrieve a bank account |
| PUT | /bank-accounts/{id} | Update a bank account |
| DELETE | /bank-accounts/{id} | Delete a bank account |

### currencies
| Method | Path | Description |
|--------|------|-------------|
| GET | /currencies | Get currencies exchange rate. |

### document-blocks
| Method | Path | Description |
|--------|------|-------------|
| GET | /document-blocks | List all document blocks |

### documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /documents | List all documents |
| POST | /documents | Create a document |
| GET | /documents/{id} | Retrieve a document |
| POST | /documents/{id}/cancel | Cancel a document |
| POST | /documents/{id}/create-from-proforma | Create a document from proforma. |
| GET | /documents/{id}/download | Download a document in PDF format. |
| GET | /documents/{id}/online-szamla | Retrieve a document Online Számla status |
| GET | /documents/{id}/payments | Retrieve a payment histroy |
| PUT | /documents/{id}/payments | Update payment history |
| DELETE | /documents/{id}/payments | Delete all payment history on document |
| GET | /documents/{id}/public-url | Retrieve a document download public url. |
| POST | /documents/{id}/send | Send invoice to given email adresses. |

### organization
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization | Retrieve a organization data. |

### partners
| Method | Path | Description |
|--------|------|-------------|
| GET | /partners | List all partners |
| POST | /partners | Create a partner |
| GET | /partners/{id} | Retrieve a partner |
| PUT | /partners/{id} | Update a partner |
| DELETE | /partners/{id} | Delete a partner |

### products
| Method | Path | Description |
|--------|------|-------------|
| GET | /products | List all product |
| POST | /products | Create a product |
| GET | /products/{id} | Retrieve a product |
| PUT | /products/{id} | Update a product |
| DELETE | /products/{id} | Delete a product |

### utils
| Method | Path | Description |
|--------|------|-------------|
| GET | /utils/convert-legacy-id/{id} | Convert legacy ID to v3 ID. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my invoices?" -> GET /documents
- "Create a new invoice for a partner" -> POST /documents
- "Download a PDF of invoice #1234" -> GET /documents/{id}/download
- "What is the exchange rate from EUR to HUF?" -> GET /currencies
- "Cancel an existing invoice" -> POST /documents/{id}/cancel
- "Send an invoice to a customer by email" -> POST /documents/{id}/send
- "List all my partners/clients" -> GET /partners
- "Add a new product to my catalog" -> POST /products
- "Convert a proforma into a final invoice" -> POST /documents/{id}/create-from-proforma
- "Get a shareable public link for an invoice" -> GET /documents/{id}/public-url
- "Check the NAV Online Szamla status for a document" -> GET /documents/{id}/online-szamla
- "What bank accounts do I have set up?" -> GET /bank-accounts
- "Record a payment against an invoice" -> PUT /documents/{id}/payments
- "What document numbering blocks are available?" -> GET /document-blocks
- "Migrate a legacy Billingo v2 ID to the v3 format" -> GET /utils/convert-legacy-id/{id}

## Response Tips

- **Paginated lists** (documents, partners, products, bank-accounts, document-blocks): Response wraps items in `data` array with `total`, `current_page`, `last_page`, `per_page`, `prev_page_url`, and `next_page_url`. Iterate using `page` param until `current_page == last_page`.
- **Document responses**: Deeply nested -- `organization` contains `bank_account` and `address` sub-objects; `summary` contains `vat_rate_summary` array. Always drill into `summary.gross_amount_local` for the local-currency total.
- **Download endpoint**: Returns binary PDF on 200, but returns `{"message": ...}` on 202 -- meaning the PDF is still being generated. Poll again after a short delay.
- **Delete endpoints** (bank-accounts, partners, products): Return 204 with no body on success. Do not attempt to parse a response.
- **Currency conversion**: The response field is `conversation_rate` (not `conversion_rate`) -- this appears to be a known typo in the API schema.
- **Error responses**: 422 indicates validation failure (check field-level errors), 403 means the resource is restricted, 404 means the ID does not exist.

## Anomaly Flags

- **202 on document download**: The PDF is not ready yet. Surface this to the user and suggest retrying after a few seconds rather than treating it as a completed download.
- **`cancelled: true` on documents**: After calling cancel, verify the returned document has `cancelled: true`. Alert if the cancellation did not take effect.
- **`conversation_rate` field name**: Flag this known API typo when users reference conversion rates to avoid confusion.
- **`payment_status` mismatches**: If a document shows `paid: false` after a PUT to payments, surface that the payment may not have been fully applied.
- **NAV Online Szamla `status` field**: Surface non-success statuses (e.g., PROCESSING, ERROR) from `/online-szamla` proactively -- Hungarian tax reporting failures require prompt attention.
- **Deprecated currency codes**: `LTL` (Lithuanian Litas) and `LVL` (Latvian Lats) are listed but have been replaced by EUR. Flag if a user attempts to use them.
- **Missing `items` on document creation**: The `items` field is optional in the schema, but an invoice with zero line items is likely an error. Warn before sending.
- **422 errors on create/update**: Surface the specific validation fields from the error body -- these are the most common failures and usually indicate missing required nested fields (e.g., partner address sub-fields).

## Playbook

### 1. Create and Send an Invoice

1. Look up the partner: `GET /partners` (filter or paginate to find the right one, note their `id`)
2. Confirm the document block: `GET /document-blocks` (pick the appropriate `block_id`)
3. Check exchange rate if invoicing in foreign currency: `GET /currencies?from=EUR&to=HUF`
4. Create the document: `POST /documents` with `type: "invoice"`, `partner_id`, `block_id`, `items`, dates, currency, and payment method
5. Send via email: `POST /documents/{id}/send` with the customer's email address
6. Optionally generate a public link: `GET /documents/{id}/public-url`

### 2. Proforma-to-Invoice Conversion

1. Create a proforma: `POST /documents` with `type: "proforma"` and all required fields
2. Send the proforma to the client: `POST /documents/{id}/send`
3. Once payment is confirmed, convert it: `POST /documents/{id}/create-from-proforma`
4. The response is the new final invoice. Record its `id` and `invoice_number`
5. Send the final invoice: `POST /documents/{new_id}/send`

### 3. Cancel an Invoice and Verify NAV Status

1. Retrieve the document to confirm details: `GET /documents/{id}`
2. Cancel the document: `POST /documents/{id}/cancel`
3. Verify the returned document has `cancelled: true`
4. Check NAV reporting status: `GET /documents/{id}/online-szamla`
5. If `status` is not successful, monitor and retry the check until NAV confirms receipt

### 4. Manage Products and Use Them in Invoices

1. Create a product: `POST /products` with `name`, `currency`, `vat` rate, `unit`, and `net_unit_price`
2. List existing products: `GET /products` (paginate if catalog is large)
3. When creating an invoice, reference products in the `items` array of `POST /documents`
4. Update pricing: `PUT /products/{id}` with revised `net_unit_price`
5. Remove discontinued items: `DELETE /products/{id}`

### 5. Onboard a New Partner and Issue First Invoice

1. Create the partner: `POST /partners` with `name` and full `address` object (`country_code`, `post_code`, `city`, `address`)
2. Optionally add `taxcode`, `emails`, `iban` for automated workflows
3. Set up a bank account if needed: `POST /bank-accounts` with account details and currency
4. Fetch document blocks: `GET /document-blocks` to select the right numbering series
5. Create the first invoice: `POST /documents` referencing the new `partner_id` and `bank_account_id`
6. Send it: `POST /documents/{id}/send`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
