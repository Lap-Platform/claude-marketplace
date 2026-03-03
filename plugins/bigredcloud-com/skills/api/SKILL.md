---
name: big-red-cloud-api
description: "Big Red Cloud API skill. Use when working with Big Red Cloud for accounts, analysisCategories, bankAccounts. Covers 120 endpoints."
version: 1.0.0
generator: lapsh
---

# Big Red Cloud API
API version: v1

## Auth
ApiKey (inferred from docs)

## Base URL
https://app.bigredcloud.com/api

## Setup
1. Set your API key in the appropriate header
2. GET /v1/accounts -- verify access
3. POST /v1/bankAccounts -- create first bankAccounts

## Endpoints

120 endpoints across 30 groups. See references/api-spec.lap for full details.

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/accounts | Returns a list of company's Accounts. Supports OData querying protocol. |

### analysisCategories
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/analysisCategories | Returns a list of company's Analysis Categories. Supports OData querying protocol. |

### bankAccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/bankAccounts | Returns a list of company's Bank Account. Supports OData querying protocol. |
| POST | /v1/bankAccounts | Creates a new Bank Account. |
| GET | /v1/bankAccounts/{id} | Returns information about a single Bank Account. |
| PUT | /v1/bankAccounts/{id} | Updates an existing Bank Account. |
| DELETE | /v1/bankAccounts/{id} | Removes an existing Bank Account. |
| PUT | /v1/bankAccounts/batch | Processes a batch of Bank Accounts. |

### bookTranTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/bookTranTypes | Returns a list of global Book Transactions' Types. Supports OData querying protocol. |

### cashPayments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/cashPayments | Returns a list of company's Cash Payments. Supports OData querying protocol. |
| POST | /v1/cashPayments | Creates a new Cash Payment. |
| GET | /v1/cashPayments/{id} | Returns information about a single Cash Payment. |
| PUT | /v1/cashPayments/{id} | Updates an existing Cash Payment. |
| DELETE | /v1/cashPayments/{id} | Removes an existing Cash Payment. |
| PUT | /v1/cashPayments/batch | Processes a batch of Cash Payments. |

### cashReceipts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/cashReceipts | Returns a list of company's Cash Receipts. Supports OData querying protocol. |
| POST | /v1/cashReceipts | Creates a new Cash Receipt. |
| GET | /v1/cashReceipts/{id} | Returns information about a single Cash Receipt. |
| PUT | /v1/cashReceipts/{id} | Updates an existing Cash Receipt. |
| DELETE | /v1/cashReceipts/{id} | Removes an existing Cash Receipt. |
| PUT | /v1/cashReceipts/batch | Processes a batch of Cash Receipts. |

### categoryTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/categoryTypes | Returns a list of company's Category Types. Supports OData querying protocol. |

### companySettings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/companySettings | Returns a list of company settings. Supports OData querying protocol. |

### companySetupConfig
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/companySetupConfig | Returns the company configuration settings. |
| GET | /v1/companySetupConfig/getFinancialYear | Returns the financial year. |
| GET | /v1/companySetupConfig/getCompanyOptions | Returns the company option setting. |
| GET | /v1/companySetupConfig/getCompanyLogo | Returns the company logo. |

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/customers | Returns a list of company's Customers. Supports OData querying protocol. |
| POST | /v1/customers | Creates a new Customer. |
| GET | /v1/customers/{id} | Returns information about a single Customer. You may specify that Customer's ledger balance should be calculated. |
| PUT | /v1/customers/{id} | Updates an existing Customer. |
| DELETE | /v1/customers/{id} | Removes an existing Customer. |
| GET | /v1/customers/GetWithoutDormant | Returns a list of company's Customers without dormant records. Supports OData querying protocol. |
| PUT | /v1/customers/batch | Processes a batch of Customers. |
| GET | /v1/customers/{itemId}/openingBalance | Returns a Customer's opening balances, calculated for the next periods: current month, one month old, two months old, three and more months old. |
| GET | /v1/customers/{itemId}/openingBalanceList | Returns a list of Customer's opening balance transactions. |
| GET | /v1/customers/{itemId}/accountTrans | Returns a list of Customer's account transactions. |
| GET | /v1/customers/{itemId}/quotes | Returns a list of Customer's quotes. |

### email
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/email/sendSalesInvoice | Sends a Sales Invoice email. |
| POST | /v1/email/sendEmailStatement | Sends a Statement email. |
| POST | /v1/email/sendQuote | Sends a Quote email. |

### nominalAccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/nominalAccounts | Returns a list of company's Nominal Accounts. Supports OData querying protocol. |
| GET | /v1/nominalAccounts/{id} | Returns information about a single Nominal Account. |
| GET | /v1/nominalAccounts/ledger | Returns information about Nominal Ledger from all Nominal accounts. |
| GET | /v1/nominalAccounts/ledger/{ids} | Returns information about Nominal Ledger from specific Nominal Accounts. |

### ownerTypeGroups
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/ownerTypeGroups | Returns a list of global Owner Type Groups. Supports OData querying protocol. |

### ownerTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/ownerTypes | Returns a list of global Owner Types. Supports OData querying protocol. |

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/payments | Returns a list of company's Payments. Supports OData querying protocol. |
| POST | /v1/payments | Creates a new Payment. |
| GET | /v1/payments/{id} | Returns information about a single Payments. |
| PUT | /v1/payments/{id} | Updates an existing Payment. |
| DELETE | /v1/payments/{id} | Removes an existing Payment. |
| PUT | /v1/payments/batch | Processes a batch of Payments. |

### products
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/products | Returns a list of company's Products. Supports OData querying protocol. |
| POST | /v1/products | Creates a new Product. |
| GET | /v1/products/{id} | Returns information about a single Product. |
| PUT | /v1/products/{id} | Updates an existing Product. |
| DELETE | /v1/products/{id} | Removes an existing Product. |
| GET | /v1/products/GetWithoutDormant | Returns a list of company's Products without dormant records. Supports OData querying protocol. |
| PUT | /v1/products/batch | Processes a batch of Products. |

### productTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/productTypes | Returns a list of global Product Types. Supports OData querying protocol. |

### purchases
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/purchases | Returns a list of company's Purchases. Supports OData querying protocol. |
| POST | /v1/purchases | Creates a new Purchase. |
| GET | /v1/purchases/{id} | Returns information about a single Purchases. |
| PUT | /v1/purchases/{id} | Updates an existing Purchase. |
| DELETE | /v1/purchases/{id} | Removes an existing Purchase. |
| PUT | /v1/purchases/batch | Processes a batch of Purchases. |
| POST | /v1/purchases/createPurchaseWithGeneratingReference | Creates a new Purchase with auto generating reference. |

### quotes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/quotes | Returns a list of company's Quotes. |
| POST | /v1/quotes | Creates a new Quote. |
| GET | /v1/quotes/{id} | Returns information about a single Quote. |
| PUT | /v1/quotes/{id} | Updates an existing Quote. |
| DELETE | /v1/quotes/{id} | Removes an existing Quote. |
| PUT | /v1/quotes/batch | Processes a batch of Quote. |
| PUT | /v1/quotes/close/{id} | Close a Quote. |
| PUT | /v1/quotes/reopen/{id} | Reopen a Quote. |
| POST | /v1/quotes/generateSaleInvoice | Generate a sale invoice from a Quote. |
| POST | /v1/quotes/createQuoteWithGeneratingReference | Creates a new Quote with auto generating reference. |

### sales
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/sales | Returns a list of company's Sales Entries, Sales Invoices and Sales Credit Notes. Supports OData querying protocol. |

### salesCreditNotes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/salesCreditNotes | Returns a list of company's Sales Credit Notes. Supports OData querying protocol. |
| POST | /v1/salesCreditNotes | Creates a new Sales Credit Note. |
| GET | /v1/salesCreditNotes/{id} | Returns information about a single Sales Credit Note. |
| PUT | /v1/salesCreditNotes/{id} | Updates an existing Sales Credit Note. |
| DELETE | /v1/salesCreditNotes/{id} | Removes an existing Sales Credit Note. |
| PUT | /v1/salesCreditNotes/batch | Processes a batch of Sales Credit Notes. |
| POST | /v1/salesCreditNotes/createCreditNoteWithGeneratingReference | Creates a new Sale Credit Note with auto generating reference. |

### salesEntries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/salesEntries | Returns a list of company's Sales Entries. Supports OData querying protocol. |
| POST | /v1/salesEntries | Creates a new Sales Entry. |
| GET | /v1/salesEntries/{id} | Returns information about a single Sales Entry. |
| PUT | /v1/salesEntries/{id} | Updates an existing Sales Entry. |
| DELETE | /v1/salesEntries/{id} | Removes an existing Sales Entry. |
| PUT | /v1/salesEntries/batch | Processes a batch of Sales Entries. |

### salesInvoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/salesInvoices | Returns a list of company's Sales Invoices. Supports OData querying protocol. |
| POST | /v1/salesInvoices | Creates a new Sales Invoice. |
| GET | /v1/salesInvoices/{id} | Returns information about a single Sales Invoice. |
| PUT | /v1/salesInvoices/{id} | Updates an existing Sales Invoice. |
| DELETE | /v1/salesInvoices/{id} | Removes an existing Sales Invoice. |
| PUT | /v1/salesInvoices/batch | Processes a batch of Sales Invoices. |
| POST | /v1/salesInvoices/createSaleInvoiceWithGeneratingReference | Creates a new Sale Invoice with auto generating reference. |

### salesReps
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/salesReps | Returns a list of company's SaleRep. |
| POST | /v1/salesReps | Creates a new SaleRep. |
| GET | /v1/salesReps/{id} | Returns information about a single SaleRep. |
| PUT | /v1/salesReps/{id} | Updates an existing Sale Rep. |
| DELETE | /v1/salesReps/{id} | Removes an existing Sale Rep. |
| PUT | /v1/salesReps/batch | Processes a batch of Sale Rep. |

### suppliers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/suppliers | Returns a list of company's Suppliers. Supports OData querying protocol. |
| POST | /v1/suppliers | Creates a new Supplier. |
| GET | /v1/suppliers/{id} | Returns information about a single Supplier. You may specify that Supplier's ledger balance should be calculated. |
| PUT | /v1/suppliers/{id} | Updates an existing Supplier. |
| DELETE | /v1/suppliers/{id} | Removes an existing Supplier. |
| PUT | /v1/suppliers/batch | Processes a batch of Suppliers. |
| GET | /v1/suppliers/{itemId}/openingBalance | Returns a Supplier's opening balances, calculated for the next periods: current month, one month old, two months old, three and more months old. |
| GET | /v1/suppliers/{itemId}/openingBalanceList | Returns a list of Supplier's opening balance transactions. |
| GET | /v1/suppliers/{itemId}/accountTrans | Returns a list of Supplier's account transactions. |

### userDefinedFields
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/userDefinedFields | Returns a list of company's User Defined Fields. Supports OData querying protocol. |

### vatAnalysisTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/vatAnalysisTypes | Returns a list of global Vat Analysis Types. Supports OData querying protocol. |

### vatCategories
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/vatCategories | Returns a list of global Vat Categories. Supports OData querying protocol. |
| POST | /v1/vatCategories/vatRates | Process Vat Rates |

### vatRates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/vatRates | Returns a list of company's Vat Rates. Supports OData querying protocol. |

### vatTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/vatTypes | Returns a list of global Vat Types. Supports OData querying protocol. |

## Enhanced Skill Content


## Question Mapping

- "How do I list all customers?" -> GET /v1/customers
- "How do I create a new sales invoice?" -> POST /v1/salesInvoices
- "What are my bank accounts?" -> GET /v1/bankAccounts
- "How do I look up a specific supplier's balance?" -> GET /v1/suppliers/{id} (with needBalance param)
- "How do I record a cash payment?" -> POST /v1/cashPayments
- "What is the company's financial year?" -> GET /v1/companySetupConfig/getFinancialYear
- "How do I email an invoice to a customer?" -> POST /v1/email/sendSalesInvoice
- "How do I convert a quote into a sales invoice?" -> POST /v1/quotes/generateSaleInvoice
- "What transactions does a customer have?" -> GET /v1/customers/{itemId}/accountTrans
- "How do I update multiple products at once?" -> PUT /v1/products/batch
- "How do I issue a credit note with an auto-generated reference?" -> POST /v1/salesCreditNotes/createCreditNoteWithGeneratingReference
- "What are the current VAT rates?" -> GET /v1/vatRates
- "How do I get the nominal ledger for a date range?" -> GET /v1/nominalAccounts/ledger (with startDate, endDate)
- "How do I close a quote?" -> PUT /v1/quotes/close/{id}
- "How do I get active customers excluding dormant ones?" -> GET /v1/customers/GetWithoutDormant

## Response Tips

- **List endpoints** (GET /v1/customers, /v1/products, etc.): Responses return arrays of objects. Check for pagination parameters in query string (page, pageSize) -- the spec does not define them explicitly, so test with large datasets.
- **Single-resource endpoints** (GET /v1/.../\{id\}): Return a single object. A missing or invalid ID typically returns a 404 or empty body, not an error array.
- **Create/Update endpoints** (POST, PUT): Return the created or updated object. The `timestamp` field on the returned object is required for subsequent DELETE calls (optimistic concurrency).
- **Batch endpoints** (PUT .../batch): Accept an array of maps and return results for each item. Check individual item statuses within the response array.
- **Email endpoints** (POST /v1/email/...): Return success/failure status. No email content is returned -- only delivery confirmation.
- **Ledger endpoints** (GET /v1/nominalAccounts/ledger): Require date range parameters. Responses may be large; filter by specific account IDs using the /ledger/\{ids\} variant.
- **Delete endpoints**: Require both `id` and `timestamp` (concurrency token from the last GET/PUT). Omitting timestamp will fail.

## Anomaly Flags

- **Stale timestamp on DELETE**: If a delete fails, the entity was modified since last fetch. Re-fetch to get the current timestamp before retrying.
- **Missing auth**: All endpoints require ApiKey authentication. A 401 or 403 response means the API key is missing, expired, or lacks permissions.
- **Empty results on GetWithoutDormant**: If active customer/product counts are unexpectedly low, dormant flags may have been set in bulk -- verify against the full list endpoint.
- **Financial year boundaries**: When querying ledger endpoints, results outside the active financial year (from /getFinancialYear) may be incomplete or absent.
- **Batch partial failures**: Batch PUT responses may succeed for some items and fail for others. Always inspect each item in the response array individually.
- **Quote lifecycle state**: Attempting to generate a sales invoice from a closed quote will fail. Check quote status or reopen it first via PUT /v1/quotes/reopen/\{id\}.
- **Large ledger responses**: Unbounded date ranges on /nominalAccounts/ledger can return very large payloads. Narrow the date range or filter by account IDs.

## Playbook

### 1. Create and Send a Sales Invoice

1. GET /v1/customers to find the target customer ID
2. GET /v1/products to get product IDs and pricing
3. GET /v1/vatRates to determine applicable VAT rate
4. POST /v1/salesInvoices with customer, line items, and VAT details (or use POST /v1/salesInvoices/createSaleInvoiceWithGeneratingReference for auto-numbering)
5. POST /v1/email/sendSalesInvoice with the returned invoice ID to email it to the customer

### 2. Quote-to-Invoice Workflow

1. POST /v1/quotes (or POST /v1/quotes/createQuoteWithGeneratingReference for auto-numbering)
2. POST /v1/email/sendQuote to send the quote to the customer
3. Once accepted, POST /v1/quotes/generateSaleInvoice with the quote ID to convert it into a sales invoice
4. POST /v1/email/sendSalesInvoice to send the generated invoice

### 3. Record a Supplier Purchase and Payment

1. GET /v1/suppliers to find the supplier ID
2. POST /v1/purchases (or POST /v1/purchases/createPurchaseWithGeneratingReference for auto-numbering)
3. POST /v1/payments to record the payment against the purchase
4. GET /v1/suppliers/{itemId}/accountTrans to verify the transaction appears on the supplier ledger

### 4. Reconcile Customer Account

1. GET /v1/customers/{id} with needBalance=true to check the outstanding balance
2. GET /v1/customers/{itemId}/accountTrans to review all transactions
3. GET /v1/customers/{itemId}/openingBalanceList to verify opening balance entries
4. POST /v1/cashReceipts to record any incoming payments
5. If overcredited, POST /v1/salesCreditNotes to issue a credit note

### 5. Bulk Update Products and Pricing

1. GET /v1/products to retrieve current product catalog
2. Modify pricing, descriptions, or VAT categories in the returned objects
3. PUT /v1/products/batch with the array of updated product maps
4. Verify updates by calling GET /v1/products and spot-checking individual items via GET /v1/products/{id}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
