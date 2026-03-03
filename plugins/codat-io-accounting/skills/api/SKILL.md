---
name: accounting-api
description: "Accounting API skill. Use when working with Accounting for companies. Covers 135 endpoints."
version: 1.0.0
generator: lapsh
---

# Accounting API
API version: 3.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies/{companyId}/connections/{connectionId}/data/accountTransactions -- verify access
3. POST /companies/{companyId}/connections/{connectionId}/push/accounts -- create first accounts

## Endpoints

135 endpoints across 1 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies/{companyId}/connections/{connectionId}/data/accountTransactions | List account transactions |
| GET | /companies/{companyId}/connections/{connectionId}/data/accountTransactions/{accountTransactionId} | Get account transaction |
| GET | /companies/{companyId}/data/accounts | List accounts |
| GET | /companies/{companyId}/data/accounts/{accountId} | Get account |
| GET | /companies/{companyId}/connections/{connectionId}/options/chartOfAccounts | Get create account model |
| POST | /companies/{companyId}/connections/{connectionId}/push/accounts | Create account |
| GET | /companies/{companyId}/data/billCreditNotes | List bill credit notes |
| GET | /companies/{companyId}/data/billCreditNotes/{billCreditNoteId} | Get bill credit note |
| GET | /companies/{companyId}/connections/{connectionId}/options/billCreditNotes | Get create/update bill credit note model |
| POST | /companies/{companyId}/connections/{connectionId}/push/billCreditNotes | Create bill credit note |
| PUT | /companies/{companyId}/connections/{connectionId}/push/billCreditNotes/{billCreditNoteId} | Update bill credit note |
| POST | /companies/{companyId}/connections/{connectionId}/push/billCreditNotes/{billCreditNoteId}/attachment | Upload bill credit note attachment |
| GET | /companies/{companyId}/data/billPayments | List bill payments |
| GET | /companies/{companyId}/data/billPayments/{billPaymentId} | Get bill payment |
| POST | /companies/{companyId}/connections/{connectionId}/push/billPayments | Create bill payments |
| GET | /companies/{companyId}/connections/{connectionId}/options/billPayments | Get create bill payment model |
| DELETE | /companies/{companyId}/connections/{connectionId}/push/billPayments/{billPaymentId} | Delete bill payment |
| GET | /companies/{companyId}/data/bills | List bills |
| GET | /companies/{companyId}/data/bills/{billId} | Get bill |
| GET | /companies/{companyId}/connections/{connectionId}/options/bills | Get create/update bill model |
| POST | /companies/{companyId}/connections/{connectionId}/push/bills | Create bill |
| PUT | /companies/{companyId}/connections/{connectionId}/push/bills/{billId} | Update bill |
| DELETE | /companies/{companyId}/connections/{connectionId}/push/bills/{billId} | Delete bill |
| GET | /companies/{companyId}/connections/{connectionId}/data/bills/{billId}/attachments | List bill attachments |
| GET | /companies/{companyId}/connections/{connectionId}/data/bills/{billId}/attachments/{attachmentId} | Get bill attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/bills/{billId}/attachments/{attachmentId}/download | Download bill attachment |
| POST | /companies/{companyId}/connections/{connectionId}/push/bills/{billId}/attachments | Upload bill attachment |
| GET | /companies/{companyId}/data/creditNotes | List credit notes |
| GET | /companies/{companyId}/data/creditNotes/{creditNoteId} | Get credit note |
| GET | /companies/{companyId}/connections/{connectionId}/options/creditNotes | Get create/update credit note model |
| POST | /companies/{companyId}/connections/{connectionId}/push/creditNotes | Create credit note |
| PUT | /companies/{companyId}/connections/{connectionId}/push/creditNotes/{creditNoteId} | Update credit note |
| GET | /companies/{companyId}/data/customers | List customers |
| GET | /companies/{companyId}/data/customers/{customerId} | Get customer |
| GET | /companies/{companyId}/connections/{connectionId}/options/customers | Get create/update customer model |
| POST | /companies/{companyId}/connections/{connectionId}/push/customers | Create customer |
| PUT | /companies/{companyId}/connections/{connectionId}/push/customers/{customerId} | Update customer |
| GET | /companies/{companyId}/connections/{connectionId}/data/customers/{customerId}/attachments | List customer attachments |
| GET | /companies/{companyId}/connections/{connectionId}/data/customers/{customerId}/attachments/{attachmentId} | Get customer attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/customers/{customerId}/attachments/{attachmentId}/download | Download customer attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directCosts | List direct costs |
| GET | /companies/{companyId}/connections/{connectionId}/data/directCosts/{directCostId} | Get direct cost |
| GET | /companies/{companyId}/connections/{connectionId}/options/directCosts | Get create direct cost model |
| POST | /companies/{companyId}/connections/{connectionId}/push/directCosts | Create direct cost |
| DELETE | /companies/{companyId}/connections/{connectionId}/push/directCosts/{directCostId} | Delete direct cost |
| POST | /companies/{companyId}/connections/{connectionId}/push/directCosts/{directCostId}/attachment | Upload direct cost attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directCosts/{directCostId}/attachments/{attachmentId} | Get direct cost attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directCosts/{directCostId}/attachments/{attachmentId}/download | Download direct cost attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directCosts/{directCostId}/attachments | List direct cost attachments |
| GET | /companies/{companyId}/connections/{connectionId}/data/directIncomes | List direct incomes |
| GET | /companies/{companyId}/connections/{connectionId}/data/directIncomes/{directIncomeId} | Get direct income |
| GET | /companies/{companyId}/connections/{connectionId}/options/directIncomes | Get create direct income model |
| POST | /companies/{companyId}/connections/{connectionId}/push/directIncomes | Create direct income |
| POST | /companies/{companyId}/connections/{connectionId}/push/directIncomes/{directIncomeId}/attachment | Create direct income attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directIncomes/{directIncomeId}/attachments/{attachmentId} | Get direct income attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directIncomes/{directIncomeId}/attachments/{attachmentId}/download | Download direct income attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/directIncomes/{directIncomeId}/attachments | List direct income attachments |
| GET | /companies/{companyId}/data/financials/balanceSheet | Get balance sheet |
| GET | /companies/{companyId}/data/financials/profitAndLoss | Get profit and loss |
| GET | /companies/{companyId}/data/financials/cashFlowStatement | Get cash flow statement |
| GET | /companies/{companyId}/data/info | Get company info |
| POST | /companies/{companyId}/data/info | Refresh company info |
| GET | /companies/{companyId}/data/invoices | List invoices |
| GET | /companies/{companyId}/data/invoices/{invoiceId} | Get invoice |
| GET | /companies/{companyId}/data/invoices/{invoiceId}/pdf | Get invoice as PDF |
| GET | /companies/{companyId}/connections/{connectionId}/data/invoices/{invoiceId}/attachments | List invoice attachments |
| GET | /companies/{companyId}/connections/{connectionId}/data/invoices/{invoiceId}/attachments/{attachmentId} | Get invoice attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/invoices/{invoiceId}/attachments/{attachmentId}/download | Download invoice attachment |
| GET | /companies/{companyId}/connections/{connectionId}/options/invoices | Get create/update invoice model |
| POST | /companies/{companyId}/connections/{connectionId}/push/invoices | Create invoice |
| PUT | /companies/{companyId}/connections/{connectionId}/push/invoices/{invoiceId} | Update invoice |
| DELETE | /companies/{companyId}/connections/{connectionId}/push/invoices/{invoiceId} | Delete invoice |
| POST | /companies/{companyId}/connections/{connectionId}/push/invoices/{invoiceId}/attachment | Upload invoice attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/itemReceipts | List item receipts |
| GET | /companies/{companyId}/connections/{connectionId}/data/itemReceipts/{itemReceiptId} | Get item receipt |
| GET | /companies/{companyId}/data/items | List items |
| GET | /companies/{companyId}/data/items/{itemId} | Get item |
| GET | /companies/{companyId}/connections/{connectionId}/options/items | Get create item model |
| POST | /companies/{companyId}/connections/{connectionId}/push/items | Create item |
| GET | /companies/{companyId}/data/journalEntries | List journal entries |
| GET | /companies/{companyId}/data/journalEntries/{journalEntryId} | Get journal entry |
| GET | /companies/{companyId}/connections/{connectionId}/options/journalEntries | Get create journal entry model |
| POST | /companies/{companyId}/connections/{connectionId}/push/journalEntries | Create journal entry |
| DELETE | /companies/{companyId}/connections/{connectionId}/push/journalEntries/{journalEntryId} | Delete journal entry |
| GET | /companies/{companyId}/data/journals | List journals |
| GET | /companies/{companyId}/data/journals/{journalId} | Get journal |
| GET | /companies/{companyId}/connections/{connectionId}/options/journals | Get create journal model |
| POST | /companies/{companyId}/connections/{connectionId}/push/journals | Create journal |
| GET | /companies/{companyId}/data/paymentMethods | List payment methods |
| GET | /companies/{companyId}/data/paymentMethods/{paymentMethodId} | Get payment method |
| GET | /companies/{companyId}/data/payments | List payments |
| GET | /companies/{companyId}/data/payments/{paymentId} | Get payment |
| GET | /companies/{companyId}/connections/{connectionId}/data/payments | List payments |
| GET | /companies/{companyId}/connections/{connectionId}/options/payments | Get create payment model |
| POST | /companies/{companyId}/connections/{connectionId}/push/payments | Create payment |
| GET | /companies/{companyId}/data/purchaseOrders | List purchase orders |
| GET | /companies/{companyId}/data/purchaseOrders/{purchaseOrderId} | Get purchase order |
| GET | /companies/{companyId}/connections/{connectionId}/options/purchaseOrders | Get create/update purchase order model |
| POST | /companies/{companyId}/connections/{connectionId}/push/purchaseOrders | Create purchase order |
| PUT | /companies/{companyId}/connections/{connectionId}/push/purchaseOrders/{purchaseOrderId} | Update purchase order |
| GET | /companies/{companyId}/data/purchaseOrders/{purchaseOrderId}/pdf | Download purchase order as PDF |
| GET | /companies/{companyId}/connections/{connectionId}/data/purchaseOrders/{purchaseOrderId}/attachments | List purchase order attachments |
| GET | /companies/{companyId}/connections/{connectionId}/data/purchaseOrders/{purchaseOrderId}/attachments/{attachmentId} | Get purchase order attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/purchaseOrders/{purchaseOrderId}/attachments/{attachmentId}/download | Download purchase order attachment |
| GET | /companies/{companyId}/data/salesOrders | List sales orders |
| GET | /companies/{companyId}/data/salesOrders/{salesOrderId} | Get sales order |
| GET | /companies/{companyId}/data/suppliers | List suppliers |
| GET | /companies/{companyId}/data/suppliers/{supplierId} | Get supplier |
| GET | /companies/{companyId}/connections/{connectionId}/options/suppliers | Get create/update supplier model |
| POST | /companies/{companyId}/connections/{connectionId}/push/suppliers | Create supplier |
| PUT | /companies/{companyId}/connections/{connectionId}/push/suppliers/{supplierId} | Update supplier |
| GET | /companies/{companyId}/connections/{connectionId}/data/suppliers/{supplierId}/attachments | List supplier attachments |
| GET | /companies/{companyId}/connections/{connectionId}/data/suppliers/{supplierId}/attachments/{attachmentId} | Get supplier attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/suppliers/{supplierId}/attachments/{attachmentId}/download | Download supplier attachment |
| GET | /companies/{companyId}/data/taxRates | List all tax rates |
| GET | /companies/{companyId}/data/taxRates/{taxRateId} | Get tax rate |
| GET | /companies/{companyId}/data/trackingCategories | List tracking categories |
| GET | /companies/{companyId}/data/trackingCategories/{trackingCategoryId} | Get tracking categories |
| GET | /companies/{companyId}/connections/{connectionId}/data/transfers | List transfers |
| POST | /companies/{companyId}/connections/{connectionId}/push/transfers/{transferId}/attachment | Upload transfer attachment |
| GET | /companies/{companyId}/connections/{connectionId}/data/transfers/{transferId} | Get transfer |
| GET | /companies/{companyId}/connections/{connectionId}/options/transfers | Get create transfer model |
| POST | /companies/{companyId}/connections/{connectionId}/push/transfers | Create transfer |
| GET | /companies/{companyId}/connections/{connectionId}/data/bankAccounts | List bank accounts |
| GET | /companies/{companyId}/connections/{connectionId}/data/bankAccounts/{accountId} | Get bank account |
| GET | /companies/{companyId}/connections/{connectionId}/options/bankAccounts | Get create/update bank account model |
| POST | /companies/{companyId}/connections/{connectionId}/push/bankAccounts | Create bank account |
| PUT | /companies/{companyId}/connections/{connectionId}/push/bankAccounts/{bankAccountId} | Update bank account |
| GET | /companies/{companyId}/connections/{connectionId}/data/bankAccounts/{accountId}/bankTransactions | List bank account transactions |
| GET | /companies/{companyId}/connections/{connectionId}/options/bankAccounts/{accountId}/bankTransactions | Get create bank account transactions model |
| POST | /companies/{companyId}/connections/{connectionId}/push/bankAccounts/{accountId}/bankTransactions | Create bank account transactions |
| GET | /companies/{companyId}/reports/agedDebtor/available | Aged debtors report available |
| GET | /companies/{companyId}/reports/agedDebtor | Aged debtors report |
| GET | /companies/{companyId}/reports/agedCreditor/available | Aged creditors report available |
| GET | /companies/{companyId}/reports/agedCreditor | Aged creditors report |

## Enhanced Skill Content
## Question Mapping

- "What invoices does this company have?" -> GET /companies/{companyId}/data/invoices
- "Show me the details of a specific bill" -> GET /companies/{companyId}/data/bills/{billId}
- "How do I create a new supplier in the accounting system?" -> POST /companies/{companyId}/connections/{connectionId}/push/suppliers
- "What fields are required to push a new invoice?" -> GET /companies/{companyId}/connections/{connectionId}/options/invoices
- "Download the PDF for this invoice" -> GET /companies/{companyId}/data/invoices/{invoiceId}/pdf
- "What is the company's profit and loss for the last 3 months?" -> GET /companies/{companyId}/data/financials/profitAndLoss
- "Show me the aged debtor report" -> GET /companies/{companyId}/reports/agedDebtor
- "List all bank transactions for a specific account" -> GET /companies/{companyId}/connections/{connectionId}/data/bankAccounts/{accountId}/bankTransactions
- "Record a direct cost against this connection" -> POST /companies/{companyId}/connections/{connectionId}/push/directCosts
- "Update an existing bill credit note" -> PUT /companies/{companyId}/connections/{connectionId}/push/billCreditNotes/{billCreditNoteId}
- "Delete a journal entry that was pushed in error" -> DELETE /companies/{companyId}/connections/{connectionId}/push/journalEntries/{journalEntryId}
- "What attachments are on this purchase order?" -> GET /companies/{companyId}/connections/{connectionId}/data/purchaseOrders/{purchaseOrderId}/attachments
- "Get the company's balance sheet for year-over-year comparison" -> GET /companies/{companyId}/data/financials/balanceSheet
- "What tax rates are configured for this company?" -> GET /companies/{companyId}/data/taxRates
- "Attach a file to this bill" -> POST /companies/{companyId}/connections/{connectionId}/push/bills/{billId}/attachments

## Response Tips

- **List endpoints** (invoices, bills, accounts, etc.): Paginated with `page` (default 1) and `pageSize` (default 100); always check if more pages exist before assuming the full dataset is returned.
- **Single-resource GETs** (by ID): Return the object directly; a 404 means the ID is wrong or the data hasn't synced yet -- do not retry blindly.
- **Push/write endpoints** (POST, PUT, DELETE): Return a push operation object with `status`, `pushOperationKey`, `validation`, and `errorMessage` -- check `status` for completion and inspect `validation.errors` on failure.
- **Options endpoints**: Return a schema descriptor with `properties`, `options`, and `validation` -- use these to discover required fields and allowed values before pushing data.
- **Financial reports** (P&L, balance sheet, cash flow): Return `reports` array with nested line items, plus `mostRecentAvailableMonth` and `earliestAvailableMonth` to know the data range.
- **Aged reports** (debtor/creditor): Return `data` array grouped by customer/supplier with aging buckets; call the `/available` endpoint first to confirm the report can be generated.
- **Attachment endpoints**: List returns `{attachments: [map]?}` -- the array may be null if none exist; download endpoints return raw file bytes.
- **Delete operations**: Return full push operation metadata including `changes` array -- inspect this to confirm what was actually modified.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface rate limit hits immediately and back off before retrying. If multiple 429s occur in sequence, pause all requests and alert the user.
- **402 Payment Required**: Present on all endpoints. Indicates the Codat subscription may be expired or the data type isn't covered by the current plan -- flag this as a billing/plan issue, not a code bug.
- **409 Conflict**: Returned by read endpoints when data is being synced or is in a conflicted state. Surface this as "data sync in progress" rather than an error.
- **503 Service Unavailable**: The underlying accounting platform may be down. Distinguish from 500 (Codat-side error) and advise checking platform status.
- **Push operation `status` not `Success`**: After any POST/PUT/DELETE, if the returned push operation shows a non-success status or has `validation.errors`, surface the specific validation messages proactively.
- **`errorMessage` non-null on push results**: Always surface push error messages -- they contain platform-specific details that are easy to miss.
- **Empty `reports` array on financial statements**: If `mostRecentAvailableMonth` is far in the past or the reports array is empty, flag that the financial data may not be synced or the platform doesn't support this report type.
- **`forceUpdate` parameter usage**: When PUT endpoints are called with `forceUpdate=True`, warn that this overrides version checks and may clobber concurrent changes.

## Playbook

### Reconcile outstanding bills for a company

1. List all bills: GET /companies/{companyId}/data/bills with `query` filter for unpaid status
2. For each bill, check bill payments: GET /companies/{companyId}/data/billPayments with `query` filtering by bill reference
3. Identify bills with no matching payment or partial payment
4. Cross-reference with the aged creditor report: GET /companies/{companyId}/reports/agedCreditor to see aging buckets
5. Surface any bills past their aging threshold as action items

### Push a new invoice with attachment

1. Check what fields are needed: GET /companies/{companyId}/connections/{connectionId}/options/invoices
2. Review the `properties`, `required` flags, and `options` arrays to build a valid payload
3. Look up the customer: GET /companies/{companyId}/data/customers with `query` to find the customer ID
4. Push the invoice: POST /companies/{companyId}/connections/{connectionId}/push/invoices with the constructed body
5. Inspect the push operation response -- confirm `status` is `Success` and `validation.errors` is empty
6. Attach a file: POST /companies/{companyId}/connections/{connectionId}/push/invoices/{invoiceId}/attachment

### Generate a financial health snapshot

1. Pull the balance sheet: GET /companies/{companyId}/data/financials/balanceSheet with `periodLength=1&periodsToCompare=12` for monthly data
2. Pull profit and loss: GET /companies/{companyId}/data/financials/profitAndLoss with the same period parameters
3. Pull cash flow: GET /companies/{companyId}/data/financials/cashFlowStatement with matching parameters
4. Check `mostRecentAvailableMonth` on each response to confirm data freshness
5. Combine the three reports to present assets, liabilities, revenue, expenses, and cash position

### Set up a new supplier and record a direct cost

1. Check supplier push options: GET /companies/{companyId}/connections/{connectionId}/options/suppliers
2. Create the supplier: POST /companies/{companyId}/connections/{connectionId}/push/suppliers with required fields
3. Verify push succeeded by checking `status` in the response
4. Check direct cost options: GET /companies/{companyId}/connections/{connectionId}/options/directCosts
5. Push the direct cost: POST /companies/{companyId}/connections/{connectionId}/push/directCosts with `contactRef` pointing to the new supplier, line items, payment allocations, and currency

### Audit account transactions and journal entries

1. List chart of accounts: GET /companies/{companyId}/data/accounts to identify account IDs of interest
2. Pull account transactions for a specific connection: GET /companies/{companyId}/connections/{connectionId}/data/accountTransactions with `query` filter on date range
3. Cross-reference with journal entries: GET /companies/{companyId}/data/journalEntries filtered to the same period
4. Compare totals and flag any journal entries without matching account transactions
5. Check tracking categories: GET /companies/{companyId}/data/trackingCategories to validate categorization consistency


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
