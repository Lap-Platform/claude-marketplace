---
name: assess-api
description: "Assess API skill. Use when working with Assess for data, companies. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Assess API
API version: 1.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/status -- verify access
3. POST /data/companies/{companyId}/assess/excel -- create first excel

## Endpoints

20 endpoints across 2 groups. See references/api-spec.lap for full details.

### data
| Method | Path | Description |
|--------|------|-------------|
| GET | /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/status | Get data integrity status |
| GET | /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/summaries | Get data integrity summary |
| GET | /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/details | List data type data integrity |
| GET | /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/revenue | Get commerce revenue metrics |
| GET | /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/orders | Get orders report |
| GET | /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/refunds | Get refunds report |
| GET | /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/customerRetention | Get customer retention metrics |
| GET | /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/lifetimeValue | Get lifetime value metric |
| GET | /data/companies/{companyId}/connections/{connectionId}/assess/accountingMetrics/marketing | Get marketing metrics report |
| POST | /data/companies/{companyId}/assess/excel | Generate Excel report |
| GET | /data/companies/{companyId}/assess/excel | Get Excel report status |
| GET | /data/companies/{companyId}/assess/excel/download | Download Excel report |

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies/{companyId}/reports/enhancedProfitAndLoss/accounts | Get enhanced profit and loss accounts |
| GET | /companies/{companyId}/reports/enhancedBalanceSheet/accounts | Get enhanced balance sheet accounts |
| GET | /companies/{companyId}/reports/enhancedCashFlow/transactions | Get enhanced cash flow report |
| GET | /companies/{companyId}/reports/enhancedInvoices | Get enhanced invoices report |
| POST | /companies/{companyId}/reports/liabilities/loans/transactions | Generate loan transactions report |
| GET | /companies/{companyId}/reports/liabilities/loans/transactions | List loan transactions |
| POST | /companies/{companyId}/reports/liabilities/loans | Generate loan summaries report |
| GET | /companies/{companyId}/reports/liabilities/loans | Get loan summaries |

## Enhanced Skill Content
## Question Mapping

- "What is the data integrity status for this company's accounting data?" -> GET /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/status
- "Show me a summary of data integrity issues for invoices" -> GET /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/summaries
- "Which specific records have data integrity mismatches?" -> GET /data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/details
- "What does this company's profit and loss look like?" -> GET /companies/{companyId}/reports/enhancedProfitAndLoss/accounts
- "Show me the balance sheet for this company as of last quarter" -> GET /companies/{companyId}/reports/enhancedBalanceSheet/accounts
- "What are the recent cash flow transactions?" -> GET /companies/{companyId}/reports/enhancedCashFlow/transactions
- "List enhanced invoice details for this company" -> GET /companies/{companyId}/reports/enhancedInvoices
- "What is the monthly revenue trend for this merchant?" -> GET /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/revenue
- "How is customer retention trending over the last 6 months?" -> GET /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/customerRetention
- "What is the customer lifetime value for this commerce connection?" -> GET /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/lifetimeValue
- "Show me order volume and refund rates side by side" -> GET /data/companies/{companyId}/connections/{connectionId}/assess/commerceMetrics/orders + GET .../refunds
- "Generate an Excel audit report for this company" -> POST /data/companies/{companyId}/assess/excel
- "Is my Excel report ready to download?" -> GET /data/companies/{companyId}/assess/excel
- "Download the enhanced financials Excel report" -> GET /data/companies/{companyId}/assess/excel/download
- "What outstanding loans does this company have?" -> GET /companies/{companyId}/reports/liabilities/loans

## Response Tips

- **Data integrity endpoints**: Responses nest results under `metadata` or `summaries` arrays of maps -- always iterate the array even if expecting a single data type.
- **Enhanced financial reports** (P&L, balance sheet): Check `reportInfo.currency` (ISO 4217) before comparing amounts across companies; `reportItems` is a nested tree of account categories.
- **Cash flow and invoices**: Paginated via `reportInfo.pageNumber`/`pageSize`/`totalResults` -- loop until `pageNumber * pageSize >= totalResults`.
- **Commerce metrics**: Responses include `dimensions`, `measures`, and `reportData` as parallel arrays -- join them by index. The `errors` array may contain partial-failure details even on a 200.
- **Excel reports**: POST queues generation (check `inProgress`/`queued`), GET checks status, GET /download returns the binary file. Always poll status before downloading.
- **Loan reports**: POST returns 202 (accepted, not complete) -- you must poll the corresponding GET until the report is generated.
- **Error responses**: 429 means rate-limited (check `Retry-After` header). 402 indicates a billing/subscription issue on the Codat side, not your auth.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry-after timing. Codat enforces rate limits per API key -- back off and queue remaining calls.
- **402 Payment Required**: Flag to user that the Codat subscription may not cover this endpoint or the company's data connection has a billing issue.
- **Excel report stuck in progress**: If `inProgress: true` persists across multiple polls (>5 min), surface a warning -- generation may have silently failed. Check `errorMessage` field.
- **Empty reportItems on 200**: A successful response with zero report items may indicate the company has no data synced for that period -- flag this rather than silently returning nothing.
- **Commerce metrics errors array non-empty**: Even on HTTP 200, the `errors` array inside the response body can contain partial failures from upstream data sources. Always inspect and surface these.
- **Data integrity mismatches**: If `summaries` show a high mismatch percentage, proactively warn that the company's connected data sources may be out of sync.
- **Deprecated or missing connectionId**: Commerce metrics require both `companyId` and `connectionId`. If the connection has been deleted or deauthorized, the API returns 404 -- surface this as a connection health issue, not a missing resource.

## Playbook

### 1. Assess a New Company's Financial Health

1. Call GET `/companies/{companyId}/reports/enhancedProfitAndLoss/accounts` with `reportDate` set to the current month and `numberOfPeriods: 12` for a year of history.
2. Call GET `/companies/{companyId}/reports/enhancedBalanceSheet/accounts` with the same parameters.
3. Review `reportInfo.currency` to confirm both reports use the same currency.
4. Check `reportItems` for negative net income trends or declining asset ratios.
5. If deeper investigation is needed, call GET `/companies/{companyId}/reports/enhancedCashFlow/transactions` to trace specific cash movements.

### 2. Validate Data Integrity Before Underwriting

1. Call GET `/data/companies/{companyId}/assess/dataTypes/{dataType}/dataIntegrity/status` for each relevant data type (e.g., `invoices`, `payments`, `bankTransactions`).
2. If any status shows mismatches, call GET `.../dataIntegrity/summaries` to get the mismatch percentage and affected record counts.
3. For detailed investigation, call GET `.../dataIntegrity/details` with pagination (`page`, `pageSize`) to retrieve specific mismatched records.
4. Use the `query` parameter to filter details by date range or amount threshold.
5. Surface any data type with >5% mismatch rate as a risk flag.

### 3. Generate and Download an Assessment Excel Report

1. Call POST `/data/companies/{companyId}/assess/excel` with `reportType: "assess"` to queue generation.
2. Confirm the response shows `success: true` or `inProgress: true`.
3. Poll GET `/data/companies/{companyId}/assess/excel?reportType=assess` every 15-30 seconds.
4. When `inProgress` is `false` and `success` is `true`, call GET `/data/companies/{companyId}/assess/excel/download?reportType=assess` to retrieve the file.
5. If `success` is `false`, check `errorMessage` for the failure reason before retrying.

### 4. Evaluate a Merchant's Commerce Performance

1. Determine the `connectionId` for the company's commerce platform.
2. Call GET `.../commerceMetrics/revenue` with `reportDate`, `periodLength: 1`, `numberOfPeriods: 12`, `periodUnit: Month`.
3. In parallel, call GET `.../commerceMetrics/orders` and GET `.../commerceMetrics/refunds` with the same parameters.
4. Calculate refund-to-order ratio from the `reportData` arrays.
5. Call GET `.../commerceMetrics/customerRetention` and `.../commerceMetrics/lifetimeValue` to complete the merchant health picture.
6. Check the `errors` array in each response for partial data source failures.

### 5. Review a Company's Loan Exposure

1. Call POST `/companies/{companyId}/reports/liabilities/loans` to trigger loan report generation (returns 202).
2. Poll GET `/companies/{companyId}/reports/liabilities/loans` until `reportItems` is populated.
3. Review `reportItems` for total outstanding loan amounts and lender details.
4. For transaction-level detail, call POST `/companies/{companyId}/reports/liabilities/loans/transactions` to trigger generation.
5. Poll GET `.../loans/transactions` and paginate through results using `reportInfo.pageNumber` and `totalResults`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
