---
name: accounting-api
description: "Accounting API skill. Use when working with Accounting for accounting. Covers 138 endpoints."
version: 1.0.0
generator: lapsh
---

# Accounting API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /accounting/tax-rates -- verify access
3. POST /accounting/tax-rates -- create first tax-rates

## Endpoints

138 endpoints across 1 groups. See references/api-spec.lap for full details.

### accounting
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounting/tax-rates | List Tax Rates |
| POST | /accounting/tax-rates | Create Tax Rate |
| GET | /accounting/tax-rates/{id} | Get Tax Rate |
| PATCH | /accounting/tax-rates/{id} | Update Tax Rate |
| DELETE | /accounting/tax-rates/{id} | Delete Tax Rate |
| GET | /accounting/bills | List Bills |
| POST | /accounting/bills | Create Bill |
| GET | /accounting/bills/{id} | Get Bill |
| PATCH | /accounting/bills/{id} | Update Bill |
| DELETE | /accounting/bills/{id} | Delete Bill |
| GET | /accounting/invoices | List Invoices |
| POST | /accounting/invoices | Create Invoice |
| GET | /accounting/invoices/{id} | Get Invoice |
| PATCH | /accounting/invoices/{id} | Update Invoice |
| DELETE | /accounting/invoices/{id} | Delete Invoice |
| GET | /accounting/ledger-accounts | List Ledger Accounts |
| POST | /accounting/ledger-accounts | Create Ledger Account |
| GET | /accounting/ledger-accounts/{id} | Get Ledger Account |
| PATCH | /accounting/ledger-accounts/{id} | Update Ledger Account |
| DELETE | /accounting/ledger-accounts/{id} | Delete Ledger Account |
| GET | /accounting/invoice-items | List Invoice Items |
| POST | /accounting/invoice-items | Create Invoice Item |
| GET | /accounting/invoice-items/{id} | Get Invoice Item |
| PATCH | /accounting/invoice-items/{id} | Update Invoice Item |
| DELETE | /accounting/invoice-items/{id} | Delete Invoice Item |
| GET | /accounting/credit-notes | List Credit Notes |
| POST | /accounting/credit-notes | Create Credit Note |
| GET | /accounting/credit-notes/{id} | Get Credit Note |
| PATCH | /accounting/credit-notes/{id} | Update Credit Note |
| DELETE | /accounting/credit-notes/{id} | Delete Credit Note |
| GET | /accounting/customers | List Customers |
| POST | /accounting/customers | Create Customer |
| GET | /accounting/customers/{id} | Get Customer |
| PATCH | /accounting/customers/{id} | Update Customer |
| DELETE | /accounting/customers/{id} | Delete Customer |
| GET | /accounting/suppliers | List Suppliers |
| POST | /accounting/suppliers | Create Supplier |
| GET | /accounting/suppliers/{id} | Get Supplier |
| PATCH | /accounting/suppliers/{id} | Update Supplier |
| DELETE | /accounting/suppliers/{id} | Delete Supplier |
| GET | /accounting/payments | List Payments |
| POST | /accounting/payments | Create Payment |
| GET | /accounting/payments/{id} | Get Payment |
| PATCH | /accounting/payments/{id} | Update Payment |
| DELETE | /accounting/payments/{id} | Delete Payment |
| GET | /accounting/company-info | Get company info |
| GET | /accounting/companies | List companies |
| GET | /accounting/balance-sheet | Get BalanceSheet |
| GET | /accounting/profit-and-loss | Get Profit and Loss |
| GET | /accounting/journal-entries | List Journal Entries |
| POST | /accounting/journal-entries | Create Journal Entry |
| GET | /accounting/journal-entries/{id} | Get Journal Entry |
| PATCH | /accounting/journal-entries/{id} | Update Journal Entry |
| DELETE | /accounting/journal-entries/{id} | Delete Journal Entry |
| GET | /accounting/purchase-orders | List Purchase Orders |
| POST | /accounting/purchase-orders | Create Purchase Order |
| GET | /accounting/purchase-orders/{id} | Get Purchase Order |
| PATCH | /accounting/purchase-orders/{id} | Update Purchase Order |
| DELETE | /accounting/purchase-orders/{id} | Delete Purchase Order |
| GET | /accounting/subsidiaries | List Subsidiaries |
| POST | /accounting/subsidiaries | Create Subsidiary |
| GET | /accounting/subsidiaries/{id} | Get Subsidiary |
| PATCH | /accounting/subsidiaries/{id} | Update Subsidiary |
| DELETE | /accounting/subsidiaries/{id} | Delete Subsidiary |
| GET | /accounting/locations | List Locations |
| POST | /accounting/locations | Create Location |
| GET | /accounting/locations/{id} | Get Location |
| PATCH | /accounting/locations/{id} | Update Location |
| DELETE | /accounting/locations/{id} | Delete Location |
| GET | /accounting/departments | List Departments |
| POST | /accounting/departments | Create Department |
| GET | /accounting/departments/{id} | Get Department |
| PATCH | /accounting/departments/{id} | Update Department |
| DELETE | /accounting/departments/{id} | Delete Department |
| GET | /accounting/attachments/{reference_type}/{reference_id} | List Attachments |
| POST | /accounting/attachments/{reference_type}/{reference_id} | Upload attachment |
| GET | /accounting/attachments/{reference_type}/{reference_id}/{id} | Get Attachment |
| DELETE | /accounting/attachments/{reference_type}/{reference_id}/{id} | Delete Attachment |
| GET | /accounting/attachments/{reference_type}/{reference_id}/{id}/download | Download Attachment |
| GET | /accounting/bank-accounts | List Bank Accounts |
| POST | /accounting/bank-accounts | Create Bank Account |
| GET | /accounting/bank-accounts/{id} | Get Bank Account |
| PATCH | /accounting/bank-accounts/{id} | Update Bank Account |
| DELETE | /accounting/bank-accounts/{id} | Delete Bank Account |
| GET | /accounting/tracking-categories | List Tracking Categories |
| POST | /accounting/tracking-categories | Create Tracking Category |
| GET | /accounting/tracking-categories/{id} | Get Tracking Category |
| PATCH | /accounting/tracking-categories/{id} | Update Tracking Category |
| DELETE | /accounting/tracking-categories/{id} | Delete Tracking Category |
| GET | /accounting/bill-payments | List Bill Payments |
| POST | /accounting/bill-payments | Create Bill Payment |
| GET | /accounting/bill-payments/{id} | Get Bill Payment |
| PATCH | /accounting/bill-payments/{id} | Update Bill Payment |
| DELETE | /accounting/bill-payments/{id} | Delete Bill Payment |
| GET | /accounting/expenses | List Expenses |
| POST | /accounting/expenses | Create Expense |
| GET | /accounting/expenses/{id} | Get Expense |
| PATCH | /accounting/expenses/{id} | Update Expense |
| DELETE | /accounting/expenses/{id} | Delete Expense |
| GET | /accounting/aged-creditors | Get Aged Creditors |
| GET | /accounting/aged-debtors | Get Aged Debtors |
| GET | /accounting/bank-feed-accounts | List Bank Feed Accounts |
| POST | /accounting/bank-feed-accounts | Create Bank Feed Account |
| GET | /accounting/bank-feed-accounts/{id} | Get Bank Feed Account |
| PATCH | /accounting/bank-feed-accounts/{id} | Update Bank Feed Account |
| DELETE | /accounting/bank-feed-accounts/{id} | Delete Bank Feed Account |
| GET | /accounting/bank-feed-statements | List Bank Feed Statements |
| POST | /accounting/bank-feed-statements | Create Bank Feed Statement |
| GET | /accounting/bank-feed-statements/{id} | Get Bank Feed Statement |
| PATCH | /accounting/bank-feed-statements/{id} | Update Bank Feed Statement |
| DELETE | /accounting/bank-feed-statements/{id} | Delete Bank Feed Statement |
| GET | /accounting/categories | List Categories |
| GET | /accounting/categories/{id} | Get Category |
| GET | /accounting/quotes | List Quotes |
| POST | /accounting/quotes | Create Quote |
| GET | /accounting/quotes/{id} | Get Quote |
| PATCH | /accounting/quotes/{id} | Update Quote |
| DELETE | /accounting/quotes/{id} | Delete Quote |
| GET | /accounting/projects | List projects |
| POST | /accounting/projects | Create project |
| GET | /accounting/projects/{id} | Get project |
| PATCH | /accounting/projects/{id} | Update project |
| DELETE | /accounting/projects/{id} | Delete project |
| GET | /accounting/employees | List Employees |
| POST | /accounting/employees | Create Employee |
| GET | /accounting/employees/{id} | Get Employee |
| PATCH | /accounting/employees/{id} | Update Employee |
| DELETE | /accounting/employees/{id} | Delete Employee |
| GET | /accounting/expense-categories | List Expense Categories |
| POST | /accounting/expense-categories | Create Expense Category |
| GET | /accounting/expense-categories/{id} | Get Expense Category |
| PATCH | /accounting/expense-categories/{id} | Update Expense Category |
| DELETE | /accounting/expense-categories/{id} | Delete Expense Category |
| GET | /accounting/expense-reports | List Expense Reports |
| POST | /accounting/expense-reports | Create Expense Report |
| GET | /accounting/expense-reports/{id} | Get Expense Report |
| PATCH | /accounting/expense-reports/{id} | Update Expense Report |
| DELETE | /accounting/expense-reports/{id} | Delete Expense Report |

## Enhanced Skill Content
## Question Mapping

- "What tax rates are configured in the system?" -> GET /accounting/tax-rates
- "Create a new invoice for a customer" -> POST /accounting/invoices
- "What is the outstanding balance on bill {id}?" -> GET /accounting/bills/{id}
- "Show me the profit and loss report" -> GET /accounting/profit-and-loss
- "Record a payment of $500 against an invoice" -> POST /accounting/payments
- "What is the company's balance sheet?" -> GET /accounting/balance-sheet
- "List all unpaid bills from a specific supplier" -> GET /accounting/bills (with filter)
- "Add a credit note for a returned product" -> POST /accounting/credit-notes
- "Who are my aged creditors past 90 days?" -> GET /accounting/aged-creditors
- "Create a journal entry to adjust accounts" -> POST /accounting/journal-entries
- "Attach a receipt to an expense" -> POST /accounting/attachments/{reference_type}/{reference_id}
- "What purchase orders are currently open?" -> GET /accounting/purchase-orders (with filter on status)
- "Submit an employee expense report" -> POST /accounting/expense-reports
- "Which ledger accounts are classified as expenses?" -> GET /accounting/ledger-accounts (with filter on classification)
- "Update the status of a quote to accepted" -> PATCH /accounting/quotes/{id}

## Response Tips

- **List endpoints** (invoices, bills, payments, etc.): Data lives in `data[]` array; paginate via `meta.cursors.next` passed as `cursor` param; default page size is 20 (adjustable via `limit`).
- **Single-resource GETs**: Primary object is in `data` (not an array); many fields are nullable (marked `?`) so always handle missing values.
- **Create/Update (POST/PATCH)**: Returns only `data.id` (and sometimes `downstream_id`) -- not the full object; follow up with a GET if you need the complete record.
- **Financial reports** (balance-sheet, profit-and-loss, aged-creditors/debtors): Return nested hierarchical structures in `data.reports[]` or `data.outstanding_balances[]` rather than flat lists.
- **Errors**: All endpoints share the same error codes (400, 401, 402, 404, 422); 402 indicates a billing/plan issue with the Apideck connector, not an accounting payment failure.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the Apideck integration tier does not cover this endpoint; user action required.
- **422 Unprocessable Entity**: Flag the validation details; often means required fields like `total_amount` or `transaction_date` are missing or malformed.
- **Stale `row_version`**: If a PATCH returns 422, check whether the `row_version` sent is outdated (optimistic concurrency conflict).
- **Null financial totals**: Alert when `total`, `balance`, or `total_amount` come back null on invoices/bills -- may indicate incomplete upstream sync.
- **Status transitions**: Flag invoices or bills in unexpected states (e.g., `void`, `deleted`, `credit`) when the user expects active records.
- **Currency mismatch**: When `currency` on a transaction differs from the company default (via GET /accounting/company-info), surface the `currency_rate` for review.
- **Missing `x-apideck-consumer-id` or `x-apideck-app-id`**: These common headers are required on every request; omission causes silent auth failures.

## Playbook

### 1. Create and send an invoice

1. GET /accounting/customers to find or confirm the customer ID
2. GET /accounting/invoice-items to look up product/service item IDs and unit prices
3. GET /accounting/tax-rates to get the applicable tax rate ID
4. POST /accounting/invoices with `customer.id`, `line_items` (each with `item`, `tax_rate`, `quantity`, `unit_price`), `invoice_date`, `due_date`, and `currency`
5. PATCH /accounting/invoices/{id} with `status: "submitted"` and `invoice_sent: true`

### 2. Record a bill and pay it

1. GET /accounting/suppliers to find the supplier ID
2. POST /accounting/bills with `supplier.id`, `line_items`, `bill_date`, `due_date`, `status: "authorised"`
3. Capture the returned bill `id`
4. POST /accounting/bill-payments with `supplier.id`, `total_amount`, `transaction_date`, and `allocations` referencing the bill ID
5. Verify via GET /accounting/bills/{id} that `status` changed to `paid` and `balance` is 0

### 3. Issue a credit note and apply it

1. GET /accounting/invoices/{id} to confirm the original invoice details and customer
2. POST /accounting/credit-notes with `customer.id`, `total_amount`, `type: "accounts_receivable_credit"`, `line_items` matching the items to credit, and `status: "authorised"`
3. PATCH /accounting/credit-notes/{id} to add `allocations` linking back to the original invoice ID
4. GET /accounting/invoices/{id} to confirm the `balance` has been reduced accordingly

### 4. Generate a month-end financial snapshot

1. GET /accounting/company-info to confirm fiscal year, currency, and tax settings
2. GET /accounting/profit-and-loss with `filter` for the target date range (`start_date`, `end_date`)
3. GET /accounting/balance-sheet with `filter` for the period end date
4. GET /accounting/aged-debtors and GET /accounting/aged-creditors to assess receivables and payables aging
5. Summarize net income from P&L, total assets/liabilities from balance sheet, and overdue amounts from aging reports

### 5. Submit and track an employee expense report

1. GET /accounting/employees to find the employee ID
2. GET /accounting/expense-categories to identify the correct category IDs for each line item
3. POST /accounting/expense-reports with `employee.id`, `transaction_date`, and `line_items` (each with `expense_category`, `amount`, `description`)
4. POST /accounting/attachments/expense-reports/{report_id} to upload receipt images for each line item
5. Monitor status via GET /accounting/expense-reports/{id} -- watch for transitions from `submitted` to `approved` to `reimbursed`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
