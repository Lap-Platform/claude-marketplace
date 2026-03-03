---
name: customer-support
description: "Customer Support API skill. Use when working with Customer Support for customer-support. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Customer Support
API version: 9.5.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /customer-support/customers -- verify access
3. POST /customer-support/customers -- create first customers

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### customer-support
| Method | Path | Description |
|--------|------|-------------|
| GET | /customer-support/customers | List Customer Support Customers |
| POST | /customer-support/customers | Create Customer Support Customer |
| GET | /customer-support/customers/{id} | Get Customer Support Customer |
| PATCH | /customer-support/customers/{id} | Update Customer Support Customer |
| DELETE | /customer-support/customers/{id} | Delete Customer Support Customer |

## Enhanced Skill Content
## Question Mapping

- "Show me all customers" -> GET /customer-support/customers
- "How do I page through the customer list?" -> GET /customer-support/customers (use `cursor` and `limit` params)
- "Find a specific customer by ID" -> GET /customer-support/customers/{id}
- "Create a new customer with an email and phone number" -> POST /customer-support/customers
- "Add a business customer with a company name" -> POST /customer-support/customers (set `individual: false`, provide `company_name`)
- "Update a customer's address" -> PATCH /customer-support/customers/{id} (send `addresses` array)
- "Change a customer's status to archived" -> PATCH /customer-support/customers/{id} (set `status: "archived"`)
- "Delete a customer record" -> DELETE /customer-support/customers/{id}
- "What fields can I select when listing customers?" -> GET /customer-support/customers (use `fields` param)
- "Add bank account details to an existing customer" -> PATCH /customer-support/customers/{id} (send `bank_accounts` object)
- "Create a customer and then retrieve the full record" -> POST /customer-support/customers, then GET /customer-support/customers/{id}
- "List customers from a specific downstream service" -> GET /customer-support/customers (set `x-apideck-service-id` header)
- "Submit a GDPR erasure request for a customer" -> PATCH /customer-support/customers/{id} (set `status: "gdpr-erasure-request"`)
- "Get the raw downstream response for a customer" -> GET /customer-support/customers/{id} (set `raw: true`)

## Response Tips

- **List endpoint (GET /customers):** Response wraps records in `data` (array). Pagination lives in `meta.cursors` -- pass `meta.cursors.next` as the `cursor` param to fetch the next page. Stop when `cursors.next` is null. `links.next` provides a ready-made URL.
- **Single record (GET /customers/{id}):** `data` is a single map, not an array. Many fields are nullable -- always check for null before accessing nested properties like `bank_accounts.iban` or `addresses[].line2`.
- **Create/Update/Delete (POST, PATCH, DELETE):** Responses return only `data.id` -- refetch via GET if you need the full record after mutation.
- **Errors (400/401/402/404/422):** 401 means bad API key or missing required headers (`x-apideck-consumer-id`, `x-apideck-app-id`). 402 signals a plan/billing issue on the connected service. 422 indicates validation failure -- check field formats (email, currency code, date-time).

## Anomaly Flags

- **402 Payment Required:** Surface immediately -- indicates the downstream service requires a plan upgrade or billing action, not a code fix.
- **GDPR erasure status:** If a customer's `status` is `gdpr-erasure-request`, warn the user before performing further reads or exports of that record.
- **Deprecated currency codes:** Flag if `currency` is set to `UNKNOWN_CURRENCY`, `LTL`, `LVL`, `ZMK`, or other withdrawn ISO 4217 codes.
- **Empty cursors on large datasets:** If `meta.items_on_page` equals `limit` but `meta.cursors.next` is null, the pagination may be incomplete -- flag for investigation.
- **Missing required headers:** If a 401 is returned, proactively check whether `x-apideck-consumer-id` and `x-apideck-app-id` headers were included before retrying with different credentials.
- **Null bank account fields:** If `bank_accounts` exists but all sub-fields are null, flag as potentially incomplete financial data rather than silently passing it through.

## Playbook

### 1. Onboard a New Customer

1. Call POST /customer-support/customers with `first_name`, `last_name`, `emails`, and `phone_numbers`.
2. Capture `data.id` from the 201 response.
3. Call GET /customer-support/customers/{id} to verify the full record was created correctly.
4. If the customer is a business, call PATCH /customer-support/customers/{id} to add `company_name`, set `individual: false`, and attach `addresses`.

### 2. Page Through All Customers

1. Call GET /customer-support/customers with `limit: 50` (or desired page size).
2. Read `meta.cursors.next` from the response.
3. If `next` is not null, call GET /customer-support/customers with `cursor` set to that value.
4. Repeat until `meta.cursors.next` is null.
5. Aggregate `data` arrays from each page for the complete customer list.

### 3. Handle a GDPR Erasure Request

1. Call GET /customer-support/customers/{id} to confirm the customer exists and review their current data.
2. Export or log any data required for compliance records.
3. Call PATCH /customer-support/customers/{id} with `status: "gdpr-erasure-request"`.
4. Verify the update by calling GET /customer-support/customers/{id} and confirming `status` is `gdpr-erasure-request`.
5. If full deletion is required, call DELETE /customer-support/customers/{id} and confirm with the returned `data.id`.

### 4. Update Customer Contact Information

1. Call GET /customer-support/customers/{id} to retrieve the current record.
2. Review existing `emails`, `phone_numbers`, and `addresses` arrays.
3. Call PATCH /customer-support/customers/{id} with the updated arrays -- include existing entries you want to keep alongside new or modified ones.
4. Call GET /customer-support/customers/{id} to confirm the changes persisted correctly.

### 5. Multi-Service Customer Lookup

1. Call GET /customer-support/customers with `x-apideck-service-id` set to the first service (e.g., Zendesk).
2. Call GET /customer-support/customers with `x-apideck-service-id` set to the second service (e.g., Freshdesk).
3. Compare `data` arrays to identify customers that exist in one service but not the other.
4. For missing customers, call POST /customer-support/customers with the appropriate `x-apideck-service-id` to sync records across services.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
