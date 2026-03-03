---
name: xero-accounting-api
description: "Xero Accounting API skill. Use when working with Xero Accounting for Accounts, BatchPayments, BankTransactions. Covers 237 endpoints."
version: 1.0.0
generator: lapsh
---

# Xero Accounting API
API version: 11.1.0

## Auth
OAuth2

## Base URL
https://api.xero.com/api.xro/2.0

## Setup
1. Configure auth: OAuth2
2. GET /Accounts -- verify access
3. POST /Accounts/{AccountID} -- create first Accounts

## Endpoints

237 endpoints across 32 groups. See references/api-spec.lap for full details.

### Accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /Accounts | Retrieves the full chart of accounts |
| PUT | /Accounts | Creates a new chart of accounts |
| GET | /Accounts/{AccountID} | Retrieves a single chart of accounts by using a unique account Id |
| POST | /Accounts/{AccountID} | Updates a chart of accounts |
| DELETE | /Accounts/{AccountID} | Deletes a chart of accounts |
| GET | /Accounts/{AccountID}/Attachments | Retrieves attachments for a specific accounts by using a unique account Id |
| GET | /Accounts/{AccountID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific account using a unique attachment Id |
| GET | /Accounts/{AccountID}/Attachments/{FileName} | Retrieves an attachment for a specific account by filename |
| POST | /Accounts/{AccountID}/Attachments/{FileName} | Updates attachment on a specific account by filename |
| PUT | /Accounts/{AccountID}/Attachments/{FileName} | Creates an attachment on a specific account |

### BatchPayments
| Method | Path | Description |
|--------|------|-------------|
| GET | /BatchPayments | Retrieves either one or many batch payments for invoices |
| PUT | /BatchPayments | Creates one or many batch payments for invoices |
| POST | /BatchPayments | Updates a specific batch payment for invoices and credit notes |
| GET | /BatchPayments/{BatchPaymentID} | Retrieves a specific batch payment using a unique batch payment Id |
| POST | /BatchPayments/{BatchPaymentID} | Updates a specific batch payment for invoices and credit notes |
| GET | /BatchPayments/{BatchPaymentID}/History | Retrieves history from a specific batch payment |
| PUT | /BatchPayments/{BatchPaymentID}/History | Creates a history record for a specific batch payment |

### BankTransactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /BankTransactions | Retrieves any spent or received money transactions |
| PUT | /BankTransactions | Creates one or more spent or received money transaction |
| POST | /BankTransactions | Updates or creates one or more spent or received money transaction |
| GET | /BankTransactions/{BankTransactionID} | Retrieves a single spent or received money transaction by using a unique bank transaction Id |
| POST | /BankTransactions/{BankTransactionID} | Updates a single spent or received money transaction |
| GET | /BankTransactions/{BankTransactionID}/Attachments | Retrieves any attachments from a specific bank transactions |
| GET | /BankTransactions/{BankTransactionID}/Attachments/{AttachmentID} | Retrieves specific attachments from a specific BankTransaction using a unique attachment Id |
| GET | /BankTransactions/{BankTransactionID}/Attachments/{FileName} | Retrieves a specific attachment from a specific bank transaction by filename |
| POST | /BankTransactions/{BankTransactionID}/Attachments/{FileName} | Updates a specific attachment from a specific bank transaction by filename |
| PUT | /BankTransactions/{BankTransactionID}/Attachments/{FileName} | Creates an attachment for a specific bank transaction by filename |
| GET | /BankTransactions/{BankTransactionID}/History | Retrieves history from a specific bank transaction using a unique bank transaction Id |
| PUT | /BankTransactions/{BankTransactionID}/History | Creates a history record for a specific bank transactions |

### BankTransfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /BankTransfers | Retrieves all bank transfers |
| PUT | /BankTransfers | Creates a bank transfer |
| GET | /BankTransfers/{BankTransferID} | Retrieves specific bank transfers by using a unique bank transfer Id |
| GET | /BankTransfers/{BankTransferID}/Attachments | Retrieves attachments from a specific bank transfer |
| GET | /BankTransfers/{BankTransferID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific bank transfer using a unique attachment ID |
| GET | /BankTransfers/{BankTransferID}/Attachments/{FileName} | Retrieves a specific attachment on a specific bank transfer by file name |
| POST | /BankTransfers/{BankTransferID}/Attachments/{FileName} |  |
| PUT | /BankTransfers/{BankTransferID}/Attachments/{FileName} |  |
| GET | /BankTransfers/{BankTransferID}/History | Retrieves history from a specific bank transfer using a unique bank transfer Id |
| PUT | /BankTransfers/{BankTransferID}/History | Creates a history record for a specific bank transfer |

### BrandingThemes
| Method | Path | Description |
|--------|------|-------------|
| GET | /BrandingThemes | Retrieves all the branding themes |
| GET | /BrandingThemes/{BrandingThemeID} | Retrieves a specific branding theme using a unique branding theme Id |
| GET | /BrandingThemes/{BrandingThemeID}/PaymentServices | Retrieves the payment services for a specific branding theme |
| POST | /BrandingThemes/{BrandingThemeID}/PaymentServices | Creates a new custom payment service for a specific branding theme |

### Budgets
| Method | Path | Description |
|--------|------|-------------|
| GET | /Budgets | Retrieve a list of budgets |
| GET | /Budgets/{BudgetID} | Retrieves a specific budget, which includes budget lines |

### Contacts
| Method | Path | Description |
|--------|------|-------------|
| GET | /Contacts | Retrieves all contacts in a Xero organisation |
| PUT | /Contacts | Creates multiple contacts (bulk) in a Xero organisation |
| POST | /Contacts | Updates or creates one or more contacts in a Xero organisation |
| GET | /Contacts/{ContactNumber} | Retrieves a specific contact by contact number in a Xero organisation |
| GET | /Contacts/{ContactID} | Retrieves a specific contacts in a Xero organisation using a unique contact Id |
| POST | /Contacts/{ContactID} | Updates a specific contact in a Xero organisation |
| GET | /Contacts/{ContactID}/Attachments | Retrieves attachments for a specific contact in a Xero organisation |
| GET | /Contacts/{ContactID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific contact using a unique attachment Id |
| GET | /Contacts/{ContactID}/Attachments/{FileName} | Retrieves a specific attachment from a specific contact by file name |
| POST | /Contacts/{ContactID}/Attachments/{FileName} |  |
| PUT | /Contacts/{ContactID}/Attachments/{FileName} |  |
| GET | /Contacts/{ContactID}/CISSettings | Retrieves CIS settings for a specific contact in a Xero organisation |
| GET | /Contacts/{ContactID}/History | Retrieves history records for a specific contact |
| PUT | /Contacts/{ContactID}/History | Creates a new history record for a specific contact |

### ContactGroups
| Method | Path | Description |
|--------|------|-------------|
| GET | /ContactGroups | Retrieves the contact Id and name of each contact group |
| PUT | /ContactGroups | Creates a contact group |
| GET | /ContactGroups/{ContactGroupID} | Retrieves a specific contact group by using a unique contact group Id |
| POST | /ContactGroups/{ContactGroupID} | Updates a specific contact group |
| PUT | /ContactGroups/{ContactGroupID}/Contacts | Creates contacts to a specific contact group |
| DELETE | /ContactGroups/{ContactGroupID}/Contacts | Deletes all contacts from a specific contact group |
| DELETE | /ContactGroups/{ContactGroupID}/Contacts/{ContactID} | Deletes a specific contact from a contact group using a unique contact Id |

### CreditNotes
| Method | Path | Description |
|--------|------|-------------|
| GET | /CreditNotes | Retrieves any credit notes |
| PUT | /CreditNotes | Creates a new credit note |
| POST | /CreditNotes | Updates or creates one or more credit notes |
| GET | /CreditNotes/{CreditNoteID} | Retrieves a specific credit note using a unique credit note Id |
| POST | /CreditNotes/{CreditNoteID} | Updates a specific credit note |
| GET | /CreditNotes/{CreditNoteID}/Attachments | Retrieves attachments for a specific credit notes |
| GET | /CreditNotes/{CreditNoteID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific credit note using a unique attachment Id |
| GET | /CreditNotes/{CreditNoteID}/Attachments/{FileName} | Retrieves a specific attachment on a specific credit note by file name |
| POST | /CreditNotes/{CreditNoteID}/Attachments/{FileName} | Updates attachments on a specific credit note by file name |
| PUT | /CreditNotes/{CreditNoteID}/Attachments/{FileName} | Creates an attachment for a specific credit note |
| GET | /CreditNotes/{CreditNoteID}/pdf | Retrieves credit notes as PDF files |
| PUT | /CreditNotes/{CreditNoteID}/Allocations | Creates allocation for a specific credit note |
| DELETE | /CreditNotes/{CreditNoteID}/Allocations/{AllocationID} | Deletes an Allocation from a Credit Note |
| GET | /CreditNotes/{CreditNoteID}/History | Retrieves history records of a specific credit note |
| PUT | /CreditNotes/{CreditNoteID}/History | Retrieves history records of a specific credit note |

### Currencies
| Method | Path | Description |
|--------|------|-------------|
| GET | /Currencies | Retrieves currencies for your Xero organisation |
| PUT | /Currencies | Create a new currency for a Xero organisation |

### Employees
| Method | Path | Description |
|--------|------|-------------|
| GET | /Employees | Retrieves employees used in Xero payrun |
| PUT | /Employees | Creates new employees used in Xero payrun |
| POST | /Employees | Creates a single new employees used in Xero payrun |
| GET | /Employees/{EmployeeID} | Retrieves a specific employee used in Xero payrun using a unique employee Id |

### ExpenseClaims
| Method | Path | Description |
|--------|------|-------------|
| GET | /ExpenseClaims | Retrieves expense claims |
| PUT | /ExpenseClaims | Creates expense claims |
| GET | /ExpenseClaims/{ExpenseClaimID} | Retrieves a specific expense claim using a unique expense claim Id |
| POST | /ExpenseClaims/{ExpenseClaimID} | Updates a specific expense claims |
| GET | /ExpenseClaims/{ExpenseClaimID}/History | Retrieves history records of a specific expense claim |
| PUT | /ExpenseClaims/{ExpenseClaimID}/History | Creates a history record for a specific expense claim |

### Invoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /Invoices | Retrieves sales invoices or purchase bills |
| PUT | /Invoices | Creates one or more sales invoices or purchase bills |
| POST | /Invoices | Updates or creates one or more sales invoices or purchase bills |
| GET | /Invoices/{InvoiceID} | Retrieves a specific sales invoice or purchase bill using a unique invoice Id |
| POST | /Invoices/{InvoiceID} | Updates a specific sales invoices or purchase bills |
| GET | /Invoices/{InvoiceID}/pdf | Retrieves invoices or purchase bills as PDF files |
| GET | /Invoices/{InvoiceID}/Attachments | Retrieves attachments for a specific invoice or purchase bill |
| GET | /Invoices/{InvoiceID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific invoices or purchase bills by using a unique attachment Id |
| GET | /Invoices/{InvoiceID}/Attachments/{FileName} | Retrieves an attachment from a specific invoice or purchase bill by filename |
| POST | /Invoices/{InvoiceID}/Attachments/{FileName} | Updates an attachment from a specific invoices or purchase bill by filename |
| PUT | /Invoices/{InvoiceID}/Attachments/{FileName} | Creates an attachment for a specific invoice or purchase bill by filename |
| GET | /Invoices/{InvoiceID}/OnlineInvoice | Retrieves a URL to an online invoice |
| POST | /Invoices/{InvoiceID}/Email | Sends a copy of a specific invoice to related contact via email |
| GET | /Invoices/{InvoiceID}/History | Retrieves history records for a specific invoice |
| PUT | /Invoices/{InvoiceID}/History | Creates a history record for a specific invoice |

### InvoiceReminders
| Method | Path | Description |
|--------|------|-------------|
| GET | /InvoiceReminders/Settings | Retrieves invoice reminder settings |

### Items
| Method | Path | Description |
|--------|------|-------------|
| GET | /Items | Retrieves items |
| PUT | /Items | Creates one or more items |
| POST | /Items | Updates or creates one or more items |
| GET | /Items/{ItemID} | Retrieves a specific item using a unique item Id |
| POST | /Items/{ItemID} | Updates a specific item |
| DELETE | /Items/{ItemID} | Deletes a specific item |
| GET | /Items/{ItemID}/History | Retrieves history for a specific item |
| PUT | /Items/{ItemID}/History | Creates a history record for a specific item |

### Journals
| Method | Path | Description |
|--------|------|-------------|
| GET | /Journals | Retrieves journals |
| GET | /Journals/{JournalID} | Retrieves a specific journal using a unique journal Id. |
| GET | /Journals/{JournalNumber} | Retrieves a specific journal using a unique journal number. |

### LinkedTransactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /LinkedTransactions | Retrieves linked transactions (billable expenses) |
| PUT | /LinkedTransactions | Creates linked transactions (billable expenses) |
| GET | /LinkedTransactions/{LinkedTransactionID} | Retrieves a specific linked transaction (billable expenses) using a unique linked transaction Id |
| POST | /LinkedTransactions/{LinkedTransactionID} | Updates a specific linked transactions (billable expenses) |
| DELETE | /LinkedTransactions/{LinkedTransactionID} | Deletes a specific linked transactions (billable expenses) |

### ManualJournals
| Method | Path | Description |
|--------|------|-------------|
| GET | /ManualJournals | Retrieves manual journals |
| PUT | /ManualJournals | Creates one or more manual journals |
| POST | /ManualJournals | Updates or creates a single manual journal |
| GET | /ManualJournals/{ManualJournalID} | Retrieves a specific manual journal |
| POST | /ManualJournals/{ManualJournalID} | Updates a specific manual journal |
| GET | /ManualJournals/{ManualJournalID}/Attachments | Retrieves attachment for a specific manual journal |
| GET | /ManualJournals/{ManualJournalID}/Attachments/{AttachmentID} | Allows you to retrieve a specific attachment from a specific manual journal using a unique attachment Id |
| GET | /ManualJournals/{ManualJournalID}/Attachments/{FileName} | Retrieves a specific attachment from a specific manual journal by file name |
| POST | /ManualJournals/{ManualJournalID}/Attachments/{FileName} | Updates a specific attachment from a specific manual journal by file name |
| PUT | /ManualJournals/{ManualJournalID}/Attachments/{FileName} | Creates a specific attachment for a specific manual journal by file name |
| GET | /ManualJournals/{ManualJournalID}/History | Retrieves history for a specific manual journal |
| PUT | /ManualJournals/{ManualJournalID}/History | Creates a history record for a specific manual journal |

### Organisation
| Method | Path | Description |
|--------|------|-------------|
| GET | /Organisation | Retrieves Xero organisation details |
| GET | /Organisation/Actions | Retrieves a list of the key actions your app has permission to perform in the connected Xero organisation. |
| GET | /Organisation/{OrganisationID}/CISSettings | Retrieves the CIS settings for the Xero organistaion. |

### Overpayments
| Method | Path | Description |
|--------|------|-------------|
| GET | /Overpayments | Retrieves overpayments |
| GET | /Overpayments/{OverpaymentID} | Retrieves a specific overpayment using a unique overpayment Id |
| PUT | /Overpayments/{OverpaymentID}/Allocations | Creates a single allocation for a specific overpayment |
| DELETE | /Overpayments/{OverpaymentID}/Allocations/{AllocationID} | Deletes an Allocation from an overpayment |
| GET | /Overpayments/{OverpaymentID}/History | Retrieves history records of a specific overpayment |
| PUT | /Overpayments/{OverpaymentID}/History | Creates a history record for a specific overpayment |

### Payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /Payments | Retrieves payments for invoices and credit notes |
| PUT | /Payments | Creates multiple payments for invoices or credit notes |
| POST | /Payments | Creates a single payment for invoice or credit notes |
| GET | /Payments/{PaymentID} | Retrieves a specific payment for invoices and credit notes using a unique payment Id |
| POST | /Payments/{PaymentID} | Updates a specific payment for invoices and credit notes |
| GET | /Payments/{PaymentID}/History | Retrieves history records of a specific payment |
| PUT | /Payments/{PaymentID}/History | Creates a history record for a specific payment |

### PaymentServices
| Method | Path | Description |
|--------|------|-------------|
| GET | /PaymentServices | Retrieves payment services |
| PUT | /PaymentServices | Creates a payment service |

### Prepayments
| Method | Path | Description |
|--------|------|-------------|
| GET | /Prepayments | Retrieves prepayments |
| GET | /Prepayments/{PrepaymentID} | Allows you to retrieve a specified prepayments |
| PUT | /Prepayments/{PrepaymentID}/Allocations | Allows you to create an Allocation for prepayments |
| DELETE | /Prepayments/{PrepaymentID}/Allocations/{AllocationID} | Deletes an Allocation from a Prepayment |
| GET | /Prepayments/{PrepaymentID}/History | Retrieves history record for a specific prepayment |
| PUT | /Prepayments/{PrepaymentID}/History | Creates a history record for a specific prepayment |

### PurchaseOrders
| Method | Path | Description |
|--------|------|-------------|
| GET | /PurchaseOrders | Retrieves purchase orders |
| PUT | /PurchaseOrders | Creates one or more purchase orders |
| POST | /PurchaseOrders | Updates or creates one or more purchase orders |
| GET | /PurchaseOrders/{PurchaseOrderID}/pdf | Retrieves specific purchase order as PDF files using a unique purchase order Id |
| GET | /PurchaseOrders/{PurchaseOrderID} | Retrieves a specific purchase order using a unique purchase order Id |
| POST | /PurchaseOrders/{PurchaseOrderID} | Updates a specific purchase order |
| GET | /PurchaseOrders/{PurchaseOrderNumber} | Retrieves a specific purchase order using purchase order number |
| GET | /PurchaseOrders/{PurchaseOrderID}/History | Retrieves history for a specific purchase order |
| PUT | /PurchaseOrders/{PurchaseOrderID}/History | Creates a history record for a specific purchase orders |
| GET | /PurchaseOrders/{PurchaseOrderID}/Attachments | Retrieves attachments for a specific purchase order |
| GET | /PurchaseOrders/{PurchaseOrderID}/Attachments/{AttachmentID} | Retrieves specific attachment for a specific purchase order using a unique attachment Id |
| GET | /PurchaseOrders/{PurchaseOrderID}/Attachments/{FileName} | Retrieves a specific attachment for a specific purchase order by filename |
| POST | /PurchaseOrders/{PurchaseOrderID}/Attachments/{FileName} | Updates a specific attachment for a specific purchase order by filename |
| PUT | /PurchaseOrders/{PurchaseOrderID}/Attachments/{FileName} | Creates attachment for a specific purchase order |

### Quotes
| Method | Path | Description |
|--------|------|-------------|
| GET | /Quotes | Retrieves sales quotes |
| PUT | /Quotes | Create one or more quotes |
| POST | /Quotes | Updates or creates one or more quotes |
| GET | /Quotes/{QuoteID} | Retrieves a specific quote using a unique quote Id |
| POST | /Quotes/{QuoteID} | Updates a specific quote |
| GET | /Quotes/{QuoteID}/History | Retrieves history records of a specific quote |
| PUT | /Quotes/{QuoteID}/History | Creates a history record for a specific quote |
| GET | /Quotes/{QuoteID}/pdf | Retrieves a specific quote as a PDF file using a unique quote Id |
| GET | /Quotes/{QuoteID}/Attachments | Retrieves attachments for a specific quote |
| GET | /Quotes/{QuoteID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific quote using a unique attachment Id |
| GET | /Quotes/{QuoteID}/Attachments/{FileName} | Retrieves a specific attachment from a specific quote by filename |
| POST | /Quotes/{QuoteID}/Attachments/{FileName} | Updates a specific attachment from a specific quote by filename |
| PUT | /Quotes/{QuoteID}/Attachments/{FileName} | Creates attachment for a specific quote |

### Receipts
| Method | Path | Description |
|--------|------|-------------|
| GET | /Receipts | Retrieves draft expense claim receipts for any user |
| PUT | /Receipts | Creates draft expense claim receipts for any user |
| GET | /Receipts/{ReceiptID} | Retrieves a specific draft expense claim receipt by using a unique receipt Id |
| POST | /Receipts/{ReceiptID} | Updates a specific draft expense claim receipts |
| GET | /Receipts/{ReceiptID}/Attachments | Retrieves attachments for a specific expense claim receipt |
| GET | /Receipts/{ReceiptID}/Attachments/{AttachmentID} | Retrieves a specific attachments from a specific expense claim receipts by using a unique attachment Id |
| GET | /Receipts/{ReceiptID}/Attachments/{FileName} | Retrieves a specific attachment from a specific expense claim receipts by file name |
| POST | /Receipts/{ReceiptID}/Attachments/{FileName} | Updates a specific attachment on a specific expense claim receipts by file name |
| PUT | /Receipts/{ReceiptID}/Attachments/{FileName} | Creates an attachment on a specific expense claim receipts by file name |
| GET | /Receipts/{ReceiptID}/History | Retrieves a history record for a specific receipt |
| PUT | /Receipts/{ReceiptID}/History | Creates a history record for a specific receipt |

### RepeatingInvoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /RepeatingInvoices | Retrieves repeating invoices |
| PUT | /RepeatingInvoices | Creates one or more repeating invoice templates |
| POST | /RepeatingInvoices | Creates or deletes one or more repeating invoice templates |
| GET | /RepeatingInvoices/{RepeatingInvoiceID} | Retrieves a specific repeating invoice by using a unique repeating invoice Id |
| POST | /RepeatingInvoices/{RepeatingInvoiceID} | Deletes a specific repeating invoice template |
| GET | /RepeatingInvoices/{RepeatingInvoiceID}/Attachments | Retrieves attachments from a specific repeating invoice |
| GET | /RepeatingInvoices/{RepeatingInvoiceID}/Attachments/{AttachmentID} | Retrieves a specific attachment from a specific repeating invoice |
| GET | /RepeatingInvoices/{RepeatingInvoiceID}/Attachments/{FileName} | Retrieves a specific attachment from a specific repeating invoices by file name |
| POST | /RepeatingInvoices/{RepeatingInvoiceID}/Attachments/{FileName} | Updates a specific attachment from a specific repeating invoices by file name |
| PUT | /RepeatingInvoices/{RepeatingInvoiceID}/Attachments/{FileName} | Creates an attachment from a specific repeating invoices by file name |
| GET | /RepeatingInvoices/{RepeatingInvoiceID}/History | Retrieves history record for a specific repeating invoice |
| PUT | /RepeatingInvoices/{RepeatingInvoiceID}/History | Creates a  history record for a specific repeating invoice |

### Reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /Reports/TenNinetyNine | Retrieve reports for 1099 |
| GET | /Reports/AgedPayablesByContact | Retrieves report for aged payables by contact |
| GET | /Reports/AgedReceivablesByContact | Retrieves report for aged receivables by contact |
| GET | /Reports/BalanceSheet | Retrieves report for balancesheet |
| GET | /Reports/BankSummary | Retrieves report for bank summary |
| GET | /Reports/{ReportID} | Retrieves a specific report using a unique ReportID |
| GET | /Reports/BudgetSummary | Retrieves report for budget summary |
| GET | /Reports/ExecutiveSummary | Retrieves report for executive summary |
| GET | /Reports | Retrieves a list of the organistaions unique reports that require a uuid to fetch |
| GET | /Reports/ProfitAndLoss | Retrieves report for profit and loss |
| GET | /Reports/TrialBalance | Retrieves report for trial balance |

### Setup
| Method | Path | Description |
|--------|------|-------------|
| POST | /Setup | Sets the chart of accounts, the conversion date and conversion balances |

### TaxRates
| Method | Path | Description |
|--------|------|-------------|
| GET | /TaxRates | Retrieves tax rates |
| PUT | /TaxRates | Creates one or more tax rates |
| POST | /TaxRates | Updates tax rates |
| GET | /TaxRates/{TaxType} | Retrieves a specific tax rate according to given TaxType code |

### TrackingCategories
| Method | Path | Description |
|--------|------|-------------|
| GET | /TrackingCategories | Retrieves tracking categories and options |
| PUT | /TrackingCategories | Create tracking categories |
| GET | /TrackingCategories/{TrackingCategoryID} | Retrieves specific tracking categories and options using a unique tracking category Id |
| POST | /TrackingCategories/{TrackingCategoryID} | Updates a specific tracking category |
| DELETE | /TrackingCategories/{TrackingCategoryID} | Deletes a specific tracking category |
| PUT | /TrackingCategories/{TrackingCategoryID}/Options | Creates options for a specific tracking category |
| POST | /TrackingCategories/{TrackingCategoryID}/Options/{TrackingOptionID} | Updates a specific option for a specific tracking category |
| DELETE | /TrackingCategories/{TrackingCategoryID}/Options/{TrackingOptionID} | Deletes a specific option for a specific tracking category |

### Users
| Method | Path | Description |
|--------|------|-------------|
| GET | /Users | Retrieves users |
| GET | /Users/{UserID} | Retrieves a specific user |

## Enhanced Skill Content
## Question Mapping

- "How do I list all invoices for a specific contact?" -> GET /Invoices (filter with `ContactIDs` param)
- "How do I create a new sales invoice?" -> PUT /Invoices (with Type, Contact, LineItems)
- "How do I record a payment against an invoice?" -> POST /Payments (with Invoice reference and Amount)
- "What is the balance sheet for my organization?" -> GET /Reports/BalanceSheet
- "How do I find a contact by name or email?" -> GET /Contacts (use `searchTerm` or `where` param)
- "How do I apply a credit note to an outstanding invoice?" -> PUT /CreditNotes/{CreditNoteID}/Allocations
- "How do I download a PDF copy of an invoice?" -> GET /Invoices/{InvoiceID}/pdf
- "How do I transfer money between two bank accounts?" -> PUT /BankTransfers (with FromBankAccount, ToBankAccount, Amount)
- "How do I email an invoice directly to the customer?" -> POST /Invoices/{InvoiceID}/Email
- "What are my overdue receivables by contact?" -> GET /Reports/AgedReceivablesByContact (with contactId)
- "How do I void or delete a payment?" -> POST /Payments/{PaymentID} (set Status=DELETED)
- "How do I attach a receipt image to an expense claim?" -> PUT /Receipts/{ReceiptID}/Attachments/{FileName}
- "How do I set up a recurring monthly invoice?" -> PUT /RepeatingInvoices (with Schedule and LineItems)
- "How do I get profit and loss for a date range?" -> GET /Reports/ProfitAndLoss (with fromDate, toDate)
- "How do I create a purchase order for a supplier?" -> PUT /PurchaseOrders (with Contact and LineItems)

## Response Tips

- **Paginated endpoints** (Invoices, Contacts, BankTransactions, CreditNotes, Payments, PurchaseOrders, ManualJournals, Overpayments, Prepayments): Check `pagination.pageCount` and loop with `page` param; default `pageSize` varies so set it explicitly.
- **List endpoints**: Data is always nested under a plural key matching the resource (e.g., `Invoices`, `Contacts`) -- never at the top level.
- **400 errors**: Return `ValidationErrors` array with `Message` strings on the affected objects; when using `summarizeErrors=false`, each item in the batch carries its own errors instead of failing the whole request.
- **Attachment downloads**: GET by AttachmentID or FileName returns raw binary (no JSON wrapper); you must set the `contentType` header param.
- **Reports**: All report endpoints return `Reports: [any]` -- the structure is dynamic with Rows/Cells; parse by iterating `Rows[].Cells[]` to extract values.
- **History endpoints**: Return `HistoryRecords` array with `Details`, `Changes`, `User`, `DateUTC` -- consistent across all resource types.
- **Warnings array**: Present alongside data on many responses; always check `Warnings` for non-fatal issues even on 200 status.

## Anomaly Flags

- **ValidationErrors present on 200**: Xero returns HTTP 200 with embedded `ValidationErrors` on individual records during batch operations -- surface these immediately even though the status code looks successful.
- **HasValidationErrors / HasErrors flags**: Boolean flags on contacts, invoices, and credit notes that signal problems; check proactively after any write operation.
- **Warnings array non-empty**: Many endpoints include a `Warnings` field that can contain deprecation notices or data quality issues; flag any non-empty Warnings to the user.
- **StatusAttributeString**: An undocumented field on many resources that signals backend status changes or issues; flag when non-empty.
- **RemainingCredit approaching zero**: On CreditNotes, Overpayments, and Prepayments, `RemainingCredit` near 0 means the credit is almost fully allocated -- flag before attempting new allocations.
- **Idempotency-Key reuse**: All write endpoints accept `Idempotency-Key`; if a retry returns the same response, flag that the original request already succeeded.
- **CIS fields present**: `CISDeduction` and `CISRate` on invoices/credit notes indicate UK Construction Industry Scheme applies -- flag for tax compliance awareness.
- **OAuth2 token expiry**: Auth is OAuth2; proactively warn when approaching token refresh boundaries during long batch operations.

## Playbook

### 1. Create and Send an Invoice

1. Look up or create the contact: GET /Contacts?searchTerm={name} or PUT /Contacts
2. Get the chart of accounts for valid account codes: GET /Accounts
3. Create the invoice as draft: PUT /Invoices with `Type: "ACCREC"`, Contact (by ContactID), LineItems (Description, Quantity, UnitAmount, AccountCode), and `Status: "DRAFT"`
4. Review the returned invoice for ValidationErrors
5. Approve the invoice: POST /Invoices/{InvoiceID} with `Status: "AUTHORISED"`
6. Email to customer: POST /Invoices/{InvoiceID}/Email
7. Optionally download PDF: GET /Invoices/{InvoiceID}/pdf

### 2. Record a Payment and Reconcile

1. Identify the invoice: GET /Invoices/{InvoiceID} -- confirm AmountDue > 0
2. Identify the bank account: GET /Accounts?where=Type=="BANK"
3. Create the payment: POST /Payments with `Invoice.InvoiceID`, `Account.AccountID`, `Amount`, `Date`, and `Status: "AUTHORISED"`
4. Verify the payment: GET /Payments/{PaymentID} -- check IsReconciled
5. Confirm invoice is settled: GET /Invoices/{InvoiceID} -- verify AmountDue is now 0

### 3. Issue a Credit Note and Apply to Invoice

1. Create the credit note: PUT /CreditNotes with `Type: "ACCRECCREDIT"`, Contact, LineItems, and `Status: "AUTHORISED"`
2. Verify creation: GET /CreditNotes/{CreditNoteID} -- check RemainingCredit
3. Identify the target invoice: GET /Invoices?where=Status=="AUTHORISED"&&AmountDue>0
4. Allocate to invoice: PUT /CreditNotes/{CreditNoteID}/Allocations with `Invoice.InvoiceID`, `Amount`, and `Date`
5. Confirm allocation: GET /CreditNotes/{CreditNoteID} -- verify RemainingCredit decreased; GET /Invoices/{InvoiceID} -- verify AmountDue reduced

### 4. Bulk Supplier Payment via Batch

1. List outstanding bills: GET /Invoices?Statuses=AUTHORISED&where=Type=="ACCPAY"
2. Identify the payment bank account: GET /Accounts?where=Type=="BANK"
3. Create batch payment: PUT /BatchPayments with `Account` (bank), `Date`, and `Payments` array -- each entry referencing an Invoice by InvoiceID with Amount
4. Check response: iterate each Payment in the result for HasValidationErrors
5. Confirm batch status: GET /BatchPayments/{BatchPaymentID} -- verify Status and TotalAmount

### 5. Month-End Reporting Snapshot

1. Pull the balance sheet: GET /Reports/BalanceSheet?date={end-of-month}
2. Pull profit and loss: GET /Reports/ProfitAndLoss?fromDate={start}&toDate={end}
3. Pull trial balance: GET /Reports/TrialBalance?date={end-of-month}
4. Pull bank summary: GET /Reports/BankSummary?fromDate={start}&toDate={end}
5. Check aged receivables for top contacts: GET /Reports/AgedReceivablesByContact?contactId={id} (repeat per key contact)
6. Check aged payables: GET /Reports/AgedPayablesByContact?contactId={id} (repeat per key supplier)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
