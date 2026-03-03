---
name: consumptionmanagementclient
description: "ConsumptionManagementClient API skill. Use when working with ConsumptionManagementClient for {scope}, providers, subscriptions. Covers 25 endpoints."
version: 1.0.0
generator: lapsh
---

# ConsumptionManagementClient
API version: 2019-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Consumption/operations -- verify access

## Endpoints

25 endpoints across 3 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.Consumption/usageDetails | Lists the usage details for the defined scope. Usage details are available via this API only for May 1, 2014 or later. |
| GET | /{scope}/providers/Microsoft.Consumption/marketplaces | Lists the marketplaces for a scope at the defined scope. Marketplaces are available via this API only for May 1, 2014 or later. |
| GET | /{scope}/providers/Microsoft.Consumption/budgets | Lists all budgets for the defined scope. |
| GET | /{scope}/providers/Microsoft.Consumption/budgets/{budgetName} | Gets the budget for the scope by budget name. |
| PUT | /{scope}/providers/Microsoft.Consumption/budgets/{budgetName} | The operation to create or update a budget. Update operation requires latest eTag to be set in the request mandatorily. You may obtain the latest eTag by performing a get operation. Create operation does not require eTag. |
| DELETE | /{scope}/providers/Microsoft.Consumption/budgets/{budgetName} | The operation to delete a budget. |
| GET | /{scope}/providers/Microsoft.Consumption/tags | Get all available tag keys for the defined scope |
| GET | /{scope}/providers/Microsoft.Consumption/charges | Lists the charges based for the defined scope. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/balances | Gets the balances for a scope by billingAccountId. Balances are available via this API only for May 1, 2014 or later. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Billing/billingPeriods/{billingPeriodName}/providers/Microsoft.Consumption/balances | Gets the balances for a scope by billing period and billingAccountId. Balances are available via this API only for May 1, 2014 or later. |
| GET | /providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/providers/Microsoft.Consumption/reservationSummaries | Lists the reservations summaries for daily or monthly grain. |
| GET | /providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/reservations/{reservationId}/providers/Microsoft.Consumption/reservationSummaries | Lists the reservations summaries for daily or monthly grain. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/reservationSummaries | Lists the reservations summaries for daily or monthly grain. |
| GET | /providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/providers/Microsoft.Consumption/reservationDetails | Lists the reservations details for provided date range. |
| GET | /providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/reservations/{reservationId}/providers/Microsoft.Consumption/reservationDetails | Lists the reservations details for provided date range. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/reservationDetails | Lists the reservations details for provided date range. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/microsoft.consumption/ReservationRecommendations | List of recommendations for purchasing reserved instances on billing account scope |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/reservationTransactions | List of transactions for reserved instances on billing account scope |
| GET | /providers/Microsoft.Consumption/operations | Lists all of the available consumption REST API operations. |
| GET | /providers/Microsoft.Management/managementGroups/{managementGroupId}/providers/Microsoft.Consumption/aggregatedcost | Provides the aggregate cost of a management group and all child management groups by current billing period. |
| GET | /providers/Microsoft.Management/managementGroups/{managementGroupId}/providers/Microsoft.Billing/billingPeriods/{billingPeriodName}/Microsoft.Consumption/aggregatedcost | Provides the aggregate cost of a management group and all child management groups by specified billing period |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Consumption/reservationRecommendations | List of recommendations for purchasing reserved instances. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Consumption/pricesheets/default | Gets the price sheet for a scope by subscriptionId. Price sheet is available via this API only for May 1, 2014 or later. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Billing/billingPeriods/{billingPeriodName}/providers/Microsoft.Consumption/pricesheets/default | Get the price sheet for a scope by subscriptionId and billing period. Price sheet is available via this API only for May 1, 2014 or later. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Consumption/forecasts | Lists the forecast charges by subscriptionId. |

## Enhanced Skill Content
## Question Mapping

- "What are my usage details for this subscription?" -> GET /{scope}/providers/Microsoft.Consumption/usageDetails
- "Show me marketplace purchases for my resource group" -> GET /{scope}/providers/Microsoft.Consumption/marketplaces
- "List all budgets on my subscription" -> GET /{scope}/providers/Microsoft.Consumption/budgets
- "What is the current status of budget 'monthly-limit'?" -> GET /{scope}/providers/Microsoft.Consumption/budgets/{budgetName}
- "Create or update a budget with a $5000 limit" -> PUT /{scope}/providers/Microsoft.Consumption/budgets/{budgetName}
- "Delete the budget named 'old-budget'" -> DELETE /{scope}/providers/Microsoft.Consumption/budgets/{budgetName}
- "What tags are used across my billing scope?" -> GET /{scope}/providers/Microsoft.Consumption/tags
- "Show me charges for a department or enrollment account" -> GET /{scope}/providers/Microsoft.Consumption/charges
- "What is the current balance on my billing account?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/balances
- "How utilized are my reserved instances this month?" -> GET /providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/providers/Microsoft.Consumption/reservationSummaries
- "Show detailed reservation usage for a specific reservation" -> GET /providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/reservations/{reservationId}/providers/Microsoft.Consumption/reservationDetails
- "What reservations does Azure recommend I purchase?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Consumption/reservationRecommendations
- "List reservation purchase and refund transactions" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/reservationTransactions
- "What is the price sheet for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Consumption/pricesheets/default
- "What is my forecasted spend for this subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Consumption/forecasts
- "What is the aggregated cost for my management group?" -> GET /providers/Microsoft.Management/managementGroups/{managementGroupId}/providers/Microsoft.Consumption/aggregatedcost

## Response Tips

- **Usage & Marketplace**: Paginated via `nextLink`; use `$skiptoken` to continue. Each item nests cost, quantity, and meter details under `properties`. Always pass `api-version=2019-06-01`.
- **Budgets**: Single-object responses for GET by name; list responses wrap items in `value[]`. PUT returns 200 (update) or 201 (create) -- check status to confirm which occurred.
- **Balances**: Nested `properties` contains `beginningBalance`, `endingBalance`, `newPurchases`, `adjustments`. Values are in the billing account's currency.
- **Reservation Summaries & Details**: `grain` param controls daily vs monthly rollup. Filter by date range using `$filter=properties/usageDate ge 2024-01-01`. Results in `value[]` array.
- **Recommendations**: Response mixes single-resource and shared-scope recommendations in the same `value[]` list -- filter on `properties/scope` client-side.
- **Price Sheets**: Large paginated responses; use `$top` to limit and `$skiptoken` to page. Each meter row nests rate info under `properties.pricesheets[]`.
- **Forecasts**: Returns multiple grain entries in `value[]`; each has `properties.charge`, `properties.confidenceLevels` with low/medium/high bounds.
- **Errors**: All endpoints return `ErrorResponse` with `error.code` and `error.message`. Common codes: `BudgetNotFound`, `BillingAccountNotFound`, `429` for throttling.

## Anomaly Flags

- **Rate limiting (429)**: Surface immediately with `Retry-After` header value. Azure Consumption APIs have strict per-tenant throttling.
- **Empty usage data**: If usageDetails returns zero records for a scope that previously had data, flag possible scope permission change or billing period lag (data can be delayed 24-72h).
- **Budget overspend**: When a GET budget response shows `properties.currentSpend.amount` exceeding `properties.amount`, proactively warn the user.
- **Reservation underutilization**: If reservation summaries show `avgUtilizationPercentage` below 60%, flag as potential cost waste with a recommendation to review sizing.
- **Deprecated API version**: If a response includes `x-ms-deprecation` headers or the error message mentions version sunset, alert the user to migrate.
- **Scope mismatch**: If a user passes a subscription-level scope to an endpoint that requires billing account scope (or vice versa), surface the 404/400 with a corrected scope suggestion.
- **Large pagination sets**: If `nextLink` appears and estimated total exceeds 10,000 rows, warn the user about potential timeout and suggest narrower `$filter` date ranges.

## Playbook

### 1. Set Up a Monthly Budget with Alerts

1. Choose the scope (e.g., `/subscriptions/{subscriptionId}`)
2. GET `/{scope}/providers/Microsoft.Consumption/budgets` to see existing budgets
3. PUT `/{scope}/providers/Microsoft.Consumption/budgets/{budgetName}` with `parameters` containing `amount`, `timeGrain: Monthly`, `timePeriod.startDate`, and `notifications` thresholds (e.g., 80%, 100%)
4. Confirm the response is 201 (created) or 200 (updated)
5. GET the budget back by name to verify notification contacts and thresholds are set correctly

### 2. Analyze Monthly Spend and Forecast

1. GET `/{scope}/providers/Microsoft.Consumption/usageDetails` with `$filter=properties/usageStart ge '2024-01-01' and properties/usageEnd le '2024-01-31'` and `$top=1000`
2. Page through results using `$skiptoken` from `nextLink` until all records are collected
3. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Consumption/forecasts` to see projected spend
4. Compare actual spend from step 2 against forecast confidence levels (low/medium/high)
5. If forecast exceeds budget, GET the budget to check notification thresholds and adjust via PUT if needed

### 3. Audit Reservation Utilization

1. GET `/providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/providers/Microsoft.Consumption/reservationSummaries` with `grain=daily` and a date range `$filter`
2. Identify days with low `avgUtilizationPercentage` (below 70%)
3. GET `/providers/Microsoft.Capacity/reservationorders/{reservationOrderId}/providers/Microsoft.Consumption/reservationDetails` with `$filter` for the same period to see which resources consumed the reservation
4. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Consumption/reservationRecommendations` to check if Azure suggests different sizing
5. Compare current reservation cost (from transactions endpoint) against on-demand pricing (from price sheet) to quantify savings or waste

### 4. Compare Costs Across Billing Periods

1. GET `/providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/balances` for current period balance
2. GET `/providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Billing/billingPeriods/{billingPeriodName}/providers/Microsoft.Consumption/balances` for a prior period
3. GET `/{scope}/providers/Microsoft.Consumption/charges` with `$filter` for each period to break down by department or enrollment account
4. Diff the `endingBalance`, `newPurchases`, and `totalUsage` values across periods to identify spend trends

### 5. Export Price Sheet for Cost Allocation

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Consumption/pricesheets/default` with `$expand=properties/meterDetails` for full meter info
2. Page through using `$skiptoken` -- price sheets are often thousands of rows
3. For historical comparison, GET the same endpoint scoped to a billing period: `/subscriptions/{subscriptionId}/providers/Microsoft.Billing/billingPeriods/{billingPeriodName}/providers/Microsoft.Consumption/pricesheets/default`
4. Cross-reference meter IDs from usage details with price sheet rows to calculate per-resource cost allocation


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
