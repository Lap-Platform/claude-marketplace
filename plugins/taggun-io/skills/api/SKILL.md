---
name: taggun-receipt-ocr-scanning-api
description: "TAGGUN Receipt OCR Scanning API skill. Use when working with TAGGUN Receipt OCR Scanning for api. Covers 23 endpoints."
version: 1.0.0
generator: lapsh
---

# TAGGUN Receipt OCR Scanning API
API version: 1.16.85

## Auth
ApiKey apikey in header

## Base URL
https://api.taggun.io/

## Setup
1. Set your API key in the appropriate header
2. GET /api/account/v1/known-merchants/export -- verify access
3. POST /api/account/v1/feedback -- create first feedback

## Endpoints

23 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/account/v1/known-merchants/export | Export a list of merchant names and addresses to normalise and match in CSV format |
| GET | /api/account/v1/known-product-codes/export | Export a list of product codes to normalise and match in CSV format |
| GET | /api/account/v1/product-categories/export | Export a list of product categories and descriptions to match in CSV format |
| GET | /api/validation/v1/campaign/settings/list | list all campaign setting IDs for a client |
| GET | /api/validation/v1/campaign/settings/{campaignId} | get campaign settings for a client |
| POST | /api/account/v1/feedback | Add manually verified receipt data to a given receipt for feedback and training purposes |
| POST | /api/account/v1/known-merchants/import | Import a list of merchant names and addresses to normalise and match in CSV to TSV format. |
| POST | /api/account/v1/known-product-codes/import | Import a list of product codes to normalise in and match in CSV to TSV format. |
| POST | /api/account/v1/merchantname/add | Add a keyword to your account's model to predict merchant name. Changes in your account's model are updated daily. |
| POST | /api/account/v1/product-categories/import | Import a list of product categories and descriptions to match in CSV to TSV format. |
| POST | /api/receipt/v1/simple/encoded | transcribe a receipt using base64 encoded image in json payload |
| POST | /api/receipt/v1/simple/file | transcribe a receipt by uploading an image file |
| POST | /api/receipt/v1/simple/url | transcribe a receipt from URL |
| POST | /api/receipt/v1/verbose/encoded | transcribe a receipt using base64 encoded image in json payload and return detailed result |
| POST | /api/receipt/v1/verbose/file | transcribe a receipt by uploading an image file and return detailed result |
| POST | /api/receipt/v1/verbose/url | transcribe a receipt from URL and return detailed result |
| POST | /api/validation/v1/campaign/file | validate and match a receipt against a receipt validation settings by uploading an image file |
| POST | /api/validation/v1/campaign/product-validation/file | validate if user-submitted info like serial number are detected an image file |
| POST | /api/validation/v1/campaign/receipt-validation/file | validate and match a receipt against a receipt validation settings by uploading an image file |
| POST | /api/validation/v1/campaign/receipt-validation/url | validate and match a receipt against a receipt validation settings from URL |
| POST | /api/validation/v1/campaign/settings/create/{campaignId} | create campaign settings for a client |
| PUT | /api/validation/v1/campaign/settings/update/{campaignId} | update campaign settings for a client |
| DELETE | /api/validation/v1/campaign/settings/delete/{campaignId} | delete campaign settings for a client |

## Enhanced Skill Content
## Question Mapping

- "How do I scan a receipt from a file?" -> POST /api/receipt/v1/simple/file
- "How do I scan a receipt from a URL?" -> POST /api/receipt/v1/simple/url
- "How do I get detailed line items from a receipt image?" -> POST /api/receipt/v1/verbose/file
- "How do I scan a base64-encoded receipt?" -> POST /api/receipt/v1/simple/encoded
- "How do I validate a receipt against a campaign?" -> POST /api/validation/v1/campaign/receipt-validation/file
- "How do I verify a product code on a receipt?" -> POST /api/validation/v1/campaign/product-validation/file
- "How do I export my known merchants list?" -> GET /api/account/v1/known-merchants/export
- "How do I import known merchants in bulk?" -> POST /api/account/v1/known-merchants/import
- "How do I add a single merchant name?" -> POST /api/account/v1/merchantname/add
- "How do I create a new validation campaign?" -> POST /api/validation/v1/campaign/settings/create/{campaignId}
- "How do I list all my campaign settings?" -> GET /api/validation/v1/campaign/settings/list
- "How do I update an existing campaign?" -> PUT /api/validation/v1/campaign/settings/update/{campaignId}
- "How do I delete a campaign?" -> DELETE /api/validation/v1/campaign/settings/delete/{campaignId}
- "How do I import product categories?" -> POST /api/account/v1/product-categories/import
- "How do I submit feedback on a scan result?" -> POST /api/account/v1/feedback

## Response Tips

- **Receipt scanning (simple):** Returns extracted merchant name, total amount, date, and tax. The `simple` variants omit line items -- use `verbose` if you need itemized data.
- **Receipt scanning (verbose):** Includes everything from `simple` plus `lineItems` array with per-item descriptions, quantities, and prices. Pass `extractLineItems: true` on the file endpoint for best results.
- **Validation endpoints:** Return match/no-match verdicts against campaign rules. Check the top-level status field before reading nested validation details.
- **Account exports:** Return file downloads (CSV/JSON). Handle the response as a binary stream, not parsed JSON.
- **Account imports:** Accept multipart file uploads. A 200 response includes a summary with counts of created, updated, and skipped records.
- **Campaign settings:** CRUD responses mirror the campaign object. On create/update, the full saved object is returned for confirmation.
- **All endpoints:** A 400 error means malformed input -- the response body contains a message field describing what went wrong. There are no other documented error codes.

## Anomaly Flags

- **400 on every endpoint:** This is the only documented error code. If you receive a 401 or 403, the API key is missing or invalid -- surface this immediately as an auth configuration problem.
- **Missing or empty OCR results:** If a scan returns 200 but with null/empty merchant, total, or date fields, flag that the image quality may be too low or the file format unsupported.
- **Verbose vs simple mismatch:** If a user requests line items but is calling a `simple` endpoint, proactively suggest switching to the `verbose` variant.
- **Large file uploads:** Receipt image files over 20MB may time out or be rejected. Flag oversized files before upload.
- **Incognito mode usage:** When `incognito: true` is passed, results are not stored -- warn the user that feedback and merchant learning will not apply to that scan.
- **Campaign ID not found:** If campaign endpoints return 400, verify the campaignId exists by checking GET /api/validation/v1/campaign/settings/{campaignId} first.
- **Deprecated or undocumented status codes:** Any 5xx response should be surfaced as a TAGGUN service issue, not a client error.

## Playbook

### 1. Scan a Receipt and Extract Totals

1. Prepare the receipt image file (JPEG, PNG, or PDF).
2. Call `POST /api/receipt/v1/simple/file` with the file in multipart form data and `apikey` header set.
3. Optionally pass `language` to improve OCR accuracy for non-English receipts.
4. Read the response for `merchantName`, `totalAmount`, `taxAmount`, and `date`.
5. If results look wrong, call `POST /api/account/v1/feedback` with corrections to improve future scans.

### 2. Get Itemized Line Items from a Receipt

1. Call `POST /api/receipt/v1/verbose/file` with the receipt file and set `extractLineItems: true`.
2. Parse the `lineItems` array from the response -- each entry contains description, quantity, unit price, and total.
3. Cross-reference totals: sum line item totals and compare against `totalAmount` to catch OCR misreads.
4. For receipts hosted online, use `POST /api/receipt/v1/verbose/url` with the image URL in the body instead.

### 3. Set Up and Run a Receipt Validation Campaign

1. Create a campaign: `POST /api/validation/v1/campaign/settings/create/{campaignId}` with your rules in the body.
2. Verify the campaign exists: `GET /api/validation/v1/campaign/settings/{campaignId}`.
3. Submit receipts for validation: `POST /api/validation/v1/campaign/receipt-validation/file` with the `campaignId` and receipt file.
4. Review the validation verdict in the response to determine if the receipt meets campaign criteria.
5. To adjust rules, call `PUT /api/validation/v1/campaign/settings/update/{campaignId}`.

### 4. Manage Known Merchants for Better Accuracy

1. Export your current merchant list: `GET /api/account/v1/known-merchants/export` and save the file.
2. Edit the export file to add or correct merchant names.
3. Re-import the updated list: `POST /api/account/v1/known-merchants/import` with the file.
4. To add a single merchant without a full import, call `POST /api/account/v1/merchantname/add` with the merchant details in the body.
5. Scan a test receipt to confirm the merchant is now recognized correctly.

### 5. Bulk Import Product Categories and Codes

1. Export existing product categories: `GET /api/account/v1/product-categories/export`.
2. Export existing product codes: `GET /api/account/v1/known-product-codes/export`.
3. Prepare import files with new categories and codes in the expected format (matching export structure).
4. Import categories: `POST /api/account/v1/product-categories/import`.
5. Import product codes: `POST /api/account/v1/known-product-codes/import`.
6. Validate by running `POST /api/validation/v1/campaign/product-validation/file` with a receipt containing a known product code.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
