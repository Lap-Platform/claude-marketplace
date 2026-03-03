---
name: customers-v3
description: "Customers V3 API skill. Use when working with Customers V3 for customers. Covers 34 endpoints."
version: 1.0.0
generator: lapsh
---

# Customers V3

## Auth
ApiKey X-Auth-Token in header

## Base URL
https://api.bigcommerce.com/stores/{store_hash}/v3

## Setup
1. Set your API key in the appropriate header
2. GET /customers -- verify access
3. POST /customers -- create first customers

## Endpoints

34 endpoints across 1 groups. See references/api-spec.lap for full details.

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /customers | Get All Customers |
| POST | /customers | Create Customers |
| PUT | /customers | Update Customers |
| DELETE | /customers | Delete Customers |
| GET | /customers/addresses | Get All Customer Addresses |
| POST | /customers/addresses | Create a Customer Address |
| PUT | /customers/addresses | Update a Customer Address |
| DELETE | /customers/addresses | Delete a Customer Address |
| POST | /customers/validate-credentials | Validate a customer credentials |
| GET | /customers/settings | Get Customer Settings |
| PUT | /customers/settings | Update Customer Settings |
| GET | /customers/settings/channels/{channel_id} | Get Customer Settings per Channel |
| PUT | /customers/settings/channels/{channel_id} | Update Customer Settings per Channel |
| GET | /customers/attributes | Get All Customer Attributes |
| POST | /customers/attributes | Create a Customer Attribute |
| PUT | /customers/attributes | Update a Customer Attribute |
| DELETE | /customers/attributes | Delete Customer Attributes |
| GET | /customers/attribute-values | Get All Customer Attribute Values |
| PUT | /customers/attribute-values | Upsert Customer Attribute Values |
| DELETE | /customers/attribute-values | Delete Customer Attribute Values |
| GET | /customers/form-field-values | Get Customer Form Field Values |
| PUT | /customers/form-field-values | Upsert Customer Form Field Values (Deprecated) |
| GET | /customers/{customerId}/consent | Get Customer Consent |
| PUT | /customers/{customerId}/consent | Update Customer Consent |
| GET | /customers/{customerId}/stored-instruments | Get Stored Instruments |
| GET | /customers/{customerId}/metafields | Get Customer Metafields |
| POST | /customers/{customerId}/metafields | Create Customer Metafields |
| GET | /customers/{customerId}/metafields/{metafieldId} | Get a Customer Metafield |
| PUT | /customers/{customerId}/metafields/{metafieldId} | Update a Metafield |
| DELETE | /customers/{customerId}/metafields/{metafieldId} | Delete a Customer Metafield |
| GET | /customers/metafields | Get All Customer Metafields |
| POST | /customers/metafields | Create Multiple Metafields |
| PUT | /customers/metafields | Update Multiple Metafields |
| DELETE | /customers/metafields | Delete Multiple Metafields |

## Enhanced Skill Content
## Question Mapping

- "How do I list all customers?" -> GET /customers
- "Find a customer by email address?" -> GET /customers?email:in=user@example.com
- "Which customers signed up after a specific date?" -> GET /customers?date_created:min={date}
- "How do I search customers by name?" -> GET /customers?name:like={pattern}
- "How do I create a new customer?" -> POST /customers
- "How do I update a customer's details?" -> PUT /customers
- "How do I delete customers in bulk?" -> DELETE /customers?id:in={ids}
- "How do I validate a customer's login credentials?" -> POST /customers/validate-credentials
- "What addresses does a customer have?" -> GET /customers/addresses?customer_id:in={id}
- "How do I add a shipping address for a customer?" -> POST /customers/addresses
- "How do I get or set privacy and customer group settings?" -> GET /customers/settings + PUT /customers/settings
- "How do I manage custom attributes on customers?" -> GET /customers/attributes + POST /customers/attributes
- "How do I read a customer's consent preferences?" -> GET /customers/{customerId}/consent
- "How do I store metadata on a customer?" -> POST /customers/{customerId}/metafields
- "What stored payment instruments does a customer have?" -> GET /customers/{customerId}/stored-instruments

## Response Tips

- **Customers & Addresses**: Responses wrap results in `data` (array) and `meta.pagination`. Use `total_pages` and `current_page` to paginate; some endpoints also support cursor pagination via `meta.cursor_pagination` with `before`/`after` params.
- **Validate Credentials**: Returns a flat object with `is_valid` (bool) and `customer_id` (nullable) -- no `data` wrapper. Watch for 429 rate limit errors on repeated attempts.
- **Settings**: Returns a single `data` object (not array). Channel-specific settings add an `allow_global_logins` field.
- **Attributes & Attribute Values**: Standard `data` array + `meta` pagination. Attribute values link to customers via `customer_id` and to definitions via `attribute_id`.
- **Metafields**: Bulk endpoints (`/customers/metafields`) return `data`, `errors`, and `meta` -- always check the `errors` array even on 200 responses. The DELETE bulk endpoint returns `meta.total`, `meta.success`, and `meta.failed` counts.
- **Consent**: Returns flat `allow`/`deny` string arrays (not wrapped in `data`). Expect 401/403 if auth scope is insufficient.
- **Errors**: 422 is the most common error across all endpoints (validation failures). 413 appears on POST/PUT /customers for oversized payloads.

## Anomaly Flags

- **429 on validate-credentials**: Rate limit hit -- surface immediately and advise backing off. This endpoint is specifically throttled to prevent brute-force attacks.
- **413 on customer create/update**: Payload too large -- flag the batch size and suggest splitting into smaller requests.
- **Partial failures in bulk metafield operations**: The `errors` array can be non-empty even with a 200 status. Always surface `meta.failed > 0` to the user.
- **Empty `data` arrays with 200 status**: Could indicate incorrect filter params (e.g., wrong `id:in` values). Flag when a query returns zero results unexpectedly.
- **`customer_id: null` on valid credentials**: The credentials are valid but the customer ID could not be resolved -- unusual state worth flagging.
- **Missing pagination links**: If `meta.pagination.links.next` is absent but `total_pages > current_page`, pagination may be misconfigured.
- **401/403 on consent or stored-instruments**: Auth token lacks required OAuth scopes -- surface the specific scope needed.

## Playbook

### 1. Look Up a Customer and Their Full Profile

1. `GET /customers?email:in={email}` to find the customer by email
2. Note the `id` from the response
3. `GET /customers/addresses?customer_id:in={id}` to get their addresses
4. `GET /customers/attribute-values?customer_id:in={id}` to get custom attribute values
5. `GET /customers/{id}/consent` to check their consent preferences
6. `GET /customers/{id}/metafields` to retrieve any stored metadata

### 2. Create a Customer with Address and Custom Attributes

1. `POST /customers` with the customer details (email, first/last name, etc.)
2. Note the returned customer `id` from `data[0].id`
3. `POST /customers/addresses` with the address linked to the new customer ID
4. If custom attributes are needed, first `GET /customers/attributes` to find attribute IDs
5. `PUT /customers/attribute-values` to set values for the new customer

### 3. Bulk Delete Customers Safely

1. `GET /customers?id:in={ids}` to confirm the customers exist and verify you have the right records
2. `GET /customers/addresses?customer_id:in={ids}` to check for associated addresses
3. `DELETE /customers/addresses?id:in={address_ids}` to remove addresses first
4. `DELETE /customers?id:in={ids}` to delete the customers
5. Verify with `GET /customers?id:in={ids}` -- expect an empty `data` array

### 4. Configure Store Privacy Settings per Channel

1. `GET /customers/settings` to review current global settings
2. `GET /customers/settings/channels/{channel_id}` to check channel-specific overrides
3. `PUT /customers/settings/channels/{channel_id}` with updated `privacy_settings` (e.g., set `ask_shopper_for_tracking_consent: true` and provide `policy_url`)
4. Verify with `GET /customers/settings/channels/{channel_id}`

### 5. Manage Customer Metafields in Bulk

1. `GET /customers/metafields?namespace={ns}` to list existing metafields across customers
2. `POST /customers/metafields` with an array of metafield objects (each specifying `customer_id`, `namespace`, `key`, `value`, `permission_set`)
3. Check response `errors` array for any failures -- handle individually
4. To update existing metafields: `PUT /customers/metafields` with updated values
5. To clean up: `DELETE /customers/metafields` with the metafield IDs, then check `meta.failed` count


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
