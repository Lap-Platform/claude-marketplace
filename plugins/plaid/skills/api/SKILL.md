---
name: the-plaid-api
description: "The Plaid API skill. Use when working with The Plaid for asset_report, cra, credit. Covers 325 endpoints."
version: 1.0.0
generator: lapsh
---

# The Plaid API
API version: 2020-09-14_1.681.5

## Auth
ApiKey PLAID-CLIENT-ID in header | ApiKey PLAID-SECRET in header | ApiKey Plaid-Version in header

## Base URL
https://production.plaid.com

## Setup
1. Set your API key in the appropriate header
2. GET /fdx/recipients -- verify access
3. POST /asset_report/create -- create first create

## Endpoints

325 endpoints across 48 groups. See references/api-spec.lap for full details.

### asset_report
| Method | Path | Description |
|--------|------|-------------|
| POST | /asset_report/create | Create an Asset Report |
| POST | /asset_report/get | Retrieve an Asset Report |
| POST | /asset_report/pdf/get | Retrieve a PDF Asset Report |
| POST | /asset_report/refresh | Refresh an Asset Report |
| POST | /asset_report/filter | Filter Asset Report |
| POST | /asset_report/remove | Delete an Asset Report |
| POST | /asset_report/audit_copy/create | Create Asset Report Audit Copy |
| POST | /asset_report/audit_copy/get | Retrieve an Asset Report Audit Copy |
| POST | /asset_report/audit_copy/pdf/get | Retrieve a PDF Asset Report Audit Copy |
| POST | /asset_report/audit_copy/remove | Remove Asset Report Audit Copy |

### cra
| Method | Path | Description |
|--------|------|-------------|
| POST | /cra/monitoring_insights/subscribe | Subscribe to Monitoring Insights |
| POST | /cra/monitoring_insights/unsubscribe | Unsubscribe from Monitoring Insights |
| POST | /cra/monitoring_insights/get | Retrieve a Monitoring Insights Report |
| POST | /cra/partner_insights/get | Retrieve cash flow insights from the bank accounts used for income verification |
| POST | /cra/check_report/income_insights/get | Retrieve cash flow information from your user's banks |
| POST | /cra/check_report/base_report/get | Retrieve a Base Report |
| POST | /cra/check_report/pdf/get | Retrieve Consumer Reports as a PDF |
| POST | /cra/check_report/create | Refresh or create a Consumer Report |
| POST | /cra/check_report/partner_insights/get | Retrieve cash flow insights from partners |
| POST | /cra/check_report/cashflow_insights/get | Retrieve cash flow insights from your user's banking data |
| POST | /cra/check_report/lend_score/get | Retrieve the LendScore from your user's banking data |
| POST | /cra/check_report/network_insights/get | Retrieve network attributes for the user |
| POST | /cra/check_report/verification/get | Retrieve various home lending reports for a user. |
| POST | /cra/check_report/verification/pdf/get | Retrieve Consumer Reports as a Verification PDF |
| POST | /cra/loans/applications/register | Register loan applications and decisions. |
| POST | /cra/loans/register | Register a list of loans to their applicants. |
| POST | /cra/loans/update | Updates loan data. |
| POST | /cra/loans/unregister | Unregister a list of loans. |

### credit
| Method | Path | Description |
|--------|------|-------------|
| POST | /credit/audit_copy_token/update | Update an Audit Copy Token |
| POST | /credit/sessions/get | Retrieve Link sessions for your user |
| POST | /credit/audit_copy_token/create | Create Asset or Income Report Audit Copy Token |
| POST | /credit/audit_copy_token/remove | Remove an Audit Copy token |
| POST | /credit/asset_report/freddie_mac/get | Retrieve an Asset Report with Freddie Mac format. Only Freddie Mac can use this endpoint. |
| POST | /credit/freddie_mac/reports/get | Retrieve an Asset Report with Freddie Mac format (aka VOA - Verification Of Assets), and a Verification Of Employment (VOE) report if this one is available. Only Freddie Mac can use this endpoint. |
| POST | /credit/bank_income/get | Retrieve information from the bank accounts used for income verification |
| POST | /credit/bank_income/pdf/get | Retrieve information from the bank accounts used for income verification in PDF format |
| POST | /credit/bank_income/refresh | Refresh a user's bank income information |
| POST | /credit/bank_income/webhook/update | Subscribe and unsubscribe to proactive notifications for a user's income profile |
| POST | /credit/payroll_income/parsing_config/update | Update the parsing configuration for a document income verification |
| POST | /credit/bank_statements/uploads/get | Retrieve data for a user's uploaded bank statements |
| POST | /credit/payroll_income/get | Retrieve a user's payroll information |
| POST | /credit/payroll_income/risk_signals/get | Retrieve fraud insights for a user's manually uploaded document(s). |
| POST | /credit/payroll_income/precheck | Check income verification eligibility and optimize conversion |
| POST | /credit/employment/get | Retrieve a summary of an individual's employment information |
| POST | /credit/payroll_income/refresh | Refresh a digital payroll income verification |
| POST | /credit/relay/create | Create a relay token to share an Asset Report with a partner client |
| POST | /credit/relay/get | Retrieve the reports associated with a relay token that was shared with you |
| POST | /credit/relay/pdf/get | Retrieve the pdf reports associated with a relay token that was shared with you (beta) |
| POST | /credit/relay/refresh | Refresh a report of a relay token |
| POST | /credit/relay/remove | Remove relay token |

### consumer_report
| Method | Path | Description |
|--------|------|-------------|
| POST | /consumer_report/pdf/get | Retrieve a PDF Reports |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/token | Create or refresh an OAuth access token |
| POST | /oauth/introspect | Get metadata about an OAuth token |
| POST | /oauth/revoke | Revoke an OAuth token |

### statements
| Method | Path | Description |
|--------|------|-------------|
| POST | /statements/list | Retrieve a list of all statements associated with an item. |
| POST | /statements/download | Retrieve a single statement. |
| POST | /statements/refresh | Refresh statements data. |

### consent
| Method | Path | Description |
|--------|------|-------------|
| POST | /consent/events/get | List a historical log of item consent events |

### item
| Method | Path | Description |
|--------|------|-------------|
| POST | /item/activity/list | List a historical log of user consent events |
| POST | /item/application/list | List a user’s connected applications |
| POST | /item/application/unlink | Unlink a user’s connected application |
| POST | /item/application/scopes/update | Update the scopes of access for a particular application |
| POST | /item/get | Retrieve an Item |
| POST | /item/remove | Remove an Item |
| POST | /item/webhook/update | Update Webhook URL |
| POST | /item/access_token/invalidate | Invalidate access_token |
| POST | /item/public_token/exchange | Exchange public token for an access token |
| POST | /item/public_token/create | Create public token |
| POST | /item/import | Import Item |

### application
| Method | Path | Description |
|--------|------|-------------|
| POST | /application/get | Retrieve information about a Plaid application |

### user_account
| Method | Path | Description |
|--------|------|-------------|
| POST | /user_account/session/get | Retrieve User Account |
| POST | /user_account/session/event/send | Send User Account Session Event |

### profile
| Method | Path | Description |
|--------|------|-------------|
| POST | /profile/network_status/get | Check a user's Plaid Network status |

### network
| Method | Path | Description |
|--------|------|-------------|
| POST | /network/status/get | Check a user's Plaid Network status |

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/get | Retrieve auth data |
| POST | /auth/verify | Verify auth data |

### transactions
| Method | Path | Description |
|--------|------|-------------|
| POST | /transactions/get | Get transaction data |
| POST | /transactions/refresh | Refresh transaction data |
| POST | /transactions/recurring/get | Fetch recurring transaction streams |
| POST | /transactions/sync | Get incremental transaction updates on an Item |
| POST | /transactions/enrich | Enrich locally-held transaction data |

### sandbox
| Method | Path | Description |
|--------|------|-------------|
| POST | /sandbox/transactions/create | Create sandbox transactions |
| POST | /sandbox/processor_token/create | Create a test Item and processor token |
| POST | /sandbox/public_token/create | Create a test Item |
| POST | /sandbox/item/fire_webhook | Fire a test webhook |
| POST | /sandbox/item/reset_login | Force a Sandbox Item into an error state |
| POST | /sandbox/item/set_verification_status | Set verification status for Sandbox account |
| POST | /sandbox/user/reset_login | Force item(s) for a Sandbox User into an error state |
| POST | /sandbox/bank_transfer/simulate | Simulate a bank transfer event in Sandbox |
| POST | /sandbox/transfer/sweep/simulate | Simulate creating a sweep |
| POST | /sandbox/transfer/simulate | Simulate a transfer event in Sandbox |
| POST | /sandbox/transfer/refund/simulate | Simulate a refund event in Sandbox |
| POST | /sandbox/transfer/ledger/simulate_available | Simulate converting pending balance to available balance |
| POST | /sandbox/transfer/ledger/deposit/simulate | Simulate a ledger deposit event in Sandbox |
| POST | /sandbox/transfer/ledger/withdraw/simulate | Simulate a ledger withdraw event in Sandbox |
| POST | /sandbox/transfer/repayment/simulate | Trigger the creation of a repayment |
| POST | /sandbox/transfer/fire_webhook | Manually fire a Transfer webhook |
| POST | /sandbox/transfer/test_clock/create | Create a test clock |
| POST | /sandbox/transfer/test_clock/advance | Advance a test clock |
| POST | /sandbox/transfer/test_clock/get | Get a test clock |
| POST | /sandbox/transfer/test_clock/list | List test clocks |
| POST | /sandbox/payment_profile/reset_login | Reset the login of a Payment Profile |
| POST | /sandbox/payment/simulate | Simulate a payment event in Sandbox |
| POST | /sandbox/bank_transfer/fire_webhook | Manually fire a Bank Transfer webhook |
| POST | /sandbox/income/fire_webhook | Manually fire an Income webhook |
| POST | /sandbox/bank_income/fire_webhook | Manually fire a bank income webhook in sandbox |
| POST | /sandbox/cra/cashflow_updates/update | Trigger an update for Cash Flow Updates |
| POST | /sandbox/oauth/select_accounts | Save the selected accounts when connecting to the Platypus Oauth institution |

### cashflow_report
| Method | Path | Description |
|--------|------|-------------|
| POST | /cashflow_report/refresh | Refresh transaction data in `cashflow_report` |
| POST | /cashflow_report/get | Gets transaction data in `cashflow_report` |
| POST | /cashflow_report/transactions/get | Gets transaction data in cashflow_report |
| POST | /cashflow_report/insights/get | Gets insights data in Cashflow Report |

### user
| Method | Path | Description |
|--------|------|-------------|
| POST | /user/transactions/refresh | Refresh user items for Transactions bundle |
| POST | /user/financial_data/refresh | Refresh user items for Financial-Insights bundle |
| POST | /user/create | Create user |
| POST | /user/get | Retrieve user identity and information |
| POST | /user/identity/remove | Remove user identity data |
| POST | /user/update | Update user information |
| POST | /user/remove | Remove user |
| POST | /user/products/terminate | Terminate user-based products |
| POST | /user/items/get | Get Items associated with a User |
| POST | /user/items/associate | Associate Items to a User |
| POST | /user/items/remove | Remove Items from a User |
| POST | /user/third_party_token/create | Create a third-party user token |
| POST | /user/third_party_token/remove | Remove a third-party user token |

### institutions
| Method | Path | Description |
|--------|------|-------------|
| POST | /institutions/get | Get details of all supported institutions |
| POST | /institutions/search | Search institutions |
| POST | /institutions/get_by_id | Get details of an institution |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /accounts/get | Retrieve accounts |
| POST | /accounts/balance/get | Retrieve real-time balance data |

### categories
| Method | Path | Description |
|--------|------|-------------|
| POST | /categories/get | (Deprecated) Get legacy categories |

### identity
| Method | Path | Description |
|--------|------|-------------|
| POST | /identity/get | Retrieve identity data |
| POST | /identity/documents/uploads/get | Returns uploaded document identity |
| POST | /identity/match | Retrieve identity match score |
| POST | /identity/refresh | Refresh identity data |

### dashboard_user
| Method | Path | Description |
|--------|------|-------------|
| POST | /dashboard_user/get | Retrieve a dashboard user |
| POST | /dashboard_user/list | List dashboard users |

### identity_verification
| Method | Path | Description |
|--------|------|-------------|
| POST | /identity_verification/create | Create a new Identity Verification |
| POST | /identity_verification/get | Retrieve Identity Verification |
| POST | /identity_verification/list | List Identity Verifications |
| POST | /identity_verification/retry | Retry an Identity Verification |
| POST | /identity_verification/autofill/create | Create autofill for an Identity Verification |

### watchlist_screening
| Method | Path | Description |
|--------|------|-------------|
| POST | /watchlist_screening/entity/create | Create a watchlist screening for an entity |
| POST | /watchlist_screening/entity/get | Get an entity screening |
| POST | /watchlist_screening/entity/history/list | List history for entity watchlist screenings |
| POST | /watchlist_screening/entity/hit/list | List hits for entity watchlist screenings |
| POST | /watchlist_screening/entity/list | List entity watchlist screenings |
| POST | /watchlist_screening/entity/program/get | Get entity watchlist screening program |
| POST | /watchlist_screening/entity/program/list | List entity watchlist screening programs |
| POST | /watchlist_screening/entity/review/create | Create a review for an entity watchlist screening |
| POST | /watchlist_screening/entity/review/list | List reviews for entity watchlist screenings |
| POST | /watchlist_screening/entity/update | Update an entity screening |
| POST | /watchlist_screening/individual/create | Create a watchlist screening for a person |
| POST | /watchlist_screening/individual/get | Retrieve an individual watchlist screening |
| POST | /watchlist_screening/individual/history/list | List history for individual watchlist screenings |
| POST | /watchlist_screening/individual/hit/list | List hits for individual watchlist screening |
| POST | /watchlist_screening/individual/list | List Individual Watchlist Screenings |
| POST | /watchlist_screening/individual/program/get | Get individual watchlist screening program |
| POST | /watchlist_screening/individual/program/list | List individual watchlist screening programs |
| POST | /watchlist_screening/individual/review/create | Create a review for an individual watchlist screening |
| POST | /watchlist_screening/individual/review/list | List reviews for individual watchlist screenings |
| POST | /watchlist_screening/individual/update | Update individual watchlist screening |

### beacon
| Method | Path | Description |
|--------|------|-------------|
| POST | /beacon/account_risk/v1/evaluate | Evaluate risk of a bank account |
| POST | /beacon/user/create | Create a Beacon User |
| POST | /beacon/user/get | Get a Beacon User |
| POST | /beacon/user/review | Review a Beacon User |
| POST | /beacon/report/create | Create a Beacon Report |
| POST | /beacon/report/list | List Beacon Reports for a Beacon User |
| POST | /beacon/report_syndication/list | List Beacon Report Syndications for a Beacon User |
| POST | /beacon/report/get | Get a Beacon Report |
| POST | /beacon/report_syndication/get | Get a Beacon Report Syndication |
| POST | /beacon/user/update | Update the identity data of a Beacon User |
| POST | /beacon/duplicate/get | Get a Beacon Duplicate |
| POST | /beacon/user/history/list | List a Beacon User's history |
| POST | /beacon/user/account_insights/get | Get Account Insights for a Beacon User |

### protect
| Method | Path | Description |
|--------|------|-------------|
| POST | /protect/user/insights/get | Get Protect user insights |
| POST | /protect/report/create | Create a Protect report |
| POST | /protect/compute | Compute Protect Trust Index Score |
| POST | /protect/event/send | Send a new event to enrich user data |
| POST | /protect/event/get | Get information about a user event |

### business_verification
| Method | Path | Description |
|--------|------|-------------|
| POST | /business_verification/get | Get a business verification |
| POST | /business_verification/create | Create a business verification |

### processor
| Method | Path | Description |
|--------|------|-------------|
| POST | /processor/auth/get | Retrieve Auth data |
| POST | /processor/account/get | Retrieve the account associated with a processor token |
| POST | /processor/investments/holdings/get | Retrieve Investment Holdings |
| POST | /processor/investments/transactions/get | Get investment transactions data |
| POST | /processor/transactions/get | Get transaction data |
| POST | /processor/transactions/sync | Get incremental transaction updates on a processor token |
| POST | /processor/transactions/refresh | Refresh transaction data |
| POST | /processor/transactions/recurring/get | Fetch recurring transaction streams |
| POST | /processor/signal/evaluate | Evaluate a planned ACH transaction |
| POST | /processor/signal/decision/report | Report whether you initiated an ACH transaction |
| POST | /processor/signal/return/report | Report a return for an ACH transaction |
| POST | /processor/signal/prepare | Opt-in a processor token to Signal |
| POST | /processor/bank_transfer/create | Create a bank transfer as a processor |
| POST | /processor/liabilities/get | Retrieve Liabilities data |
| POST | /processor/identity/get | Retrieve Identity data |
| POST | /processor/identity/match | Retrieve identity match score |
| POST | /processor/balance/get | Retrieve Balance data |
| POST | /processor/token/create | Create processor token |
| POST | /processor/token/permissions/set | Control a processor's access to products |
| POST | /processor/token/permissions/get | Get a processor token's product permissions |
| POST | /processor/token/webhook/update | Update a processor token's webhook URL |
| POST | /processor/stripe/bank_account_token/create | Create Stripe bank account token |
| POST | /processor/apex/processor_token/create | Create Apex bank account token |

### webhook_verification_key
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhook_verification_key/get | Get webhook verification key |

### liabilities
| Method | Path | Description |
|--------|------|-------------|
| POST | /liabilities/get | Retrieve Liabilities data |

### payment_initiation
| Method | Path | Description |
|--------|------|-------------|
| POST | /payment_initiation/recipient/create | Create payment recipient |
| POST | /payment_initiation/payment/reverse | Reverse an existing payment |
| POST | /payment_initiation/recipient/get | Get payment recipient |
| POST | /payment_initiation/recipient/list | List payment recipients |
| POST | /payment_initiation/payment/create | Create a payment |
| POST | /payment_initiation/payment/token/create | Create payment token |
| POST | /payment_initiation/consent/create | Create payment consent |
| POST | /payment_initiation/consent/get | Get payment consent |
| POST | /payment_initiation/consent/revoke | Revoke payment consent |
| POST | /payment_initiation/consent/payment/execute | Execute a single payment using consent |
| POST | /payment_initiation/payment/get | Get payment details |
| POST | /payment_initiation/payment/list | List payments |

### investments
| Method | Path | Description |
|--------|------|-------------|
| POST | /investments/holdings/get | Get Investment holdings |
| POST | /investments/transactions/get | Get investment transactions |
| POST | /investments/refresh | Refresh investment data |
| POST | /investments/auth/get | Get data needed to authorize an investments transfer |

### link
| Method | Path | Description |
|--------|------|-------------|
| POST | /link/token/create | Create Link Token |
| POST | /link/token/get | Get Link Token |
| POST | /link/oauth/correlation_id/exchange | Exchange the Link Correlation Id for a Link Token |

### session
| Method | Path | Description |
|--------|------|-------------|
| POST | /session/token/create | Create a Link token for Layer |

### transfer
| Method | Path | Description |
|--------|------|-------------|
| POST | /transfer/get | Retrieve a transfer |
| POST | /transfer/recurring/get | Retrieve a recurring transfer |
| POST | /transfer/authorization/create | Create a transfer authorization |
| POST | /transfer/authorization/cancel | Cancel a transfer authorization |
| POST | /transfer/balance/get | (Deprecated) Retrieve a balance held with Plaid |
| POST | /transfer/capabilities/get | Get RTP eligibility information of a transfer |
| POST | /transfer/configuration/get | Get transfer product configuration |
| POST | /transfer/ledger/get | Retrieve Plaid Ledger balance |
| POST | /transfer/ledger/distribute | Move available balance between ledgers |
| POST | /transfer/ledger/deposit | Deposit funds into a Plaid Ledger balance |
| POST | /transfer/ledger/withdraw | Withdraw funds from a Plaid Ledger balance |
| POST | /transfer/originator/funding_account/update | Update the funding account associated with the originator |
| POST | /transfer/originator/funding_account/create | Create a new funding account for an originator |
| POST | /transfer/metrics/get | Get transfer product usage metrics |
| POST | /transfer/create | Create a transfer |
| POST | /transfer/recurring/create | Create a recurring transfer |
| POST | /transfer/list | List transfers |
| POST | /transfer/recurring/list | List recurring transfers |
| POST | /transfer/cancel | Cancel a transfer |
| POST | /transfer/recurring/cancel | Cancel a recurring transfer. |
| POST | /transfer/event/list | List transfer events |
| POST | /transfer/ledger/event/list | List transfer ledger events |
| POST | /transfer/event/sync | Sync transfer events |
| POST | /transfer/sweep/get | Retrieve a sweep |
| POST | /transfer/sweep/list | List sweeps |
| POST | /transfer/migrate_account | Migrate account into Transfers |
| POST | /transfer/intent/create | Create a transfer intent object to invoke the Transfer UI |
| POST | /transfer/intent/get | Retrieve more information about a transfer intent |
| POST | /transfer/repayment/list | Lists historical repayments |
| POST | /transfer/repayment/return/list | List the returns included in a repayment |
| POST | /transfer/platform/requirement/submit | Submit additional onboarding information on behalf of an originator |
| POST | /transfer/originator/create | Create a new originator |
| POST | /transfer/questionnaire/create | Generate a Plaid-hosted onboarding UI URL. |
| POST | /transfer/diligence/submit | Submit transfer diligence on behalf of the originator |
| POST | /transfer/diligence/document/upload | Upload transfer diligence document on behalf of the originator |
| POST | /transfer/originator/get | Get status of an originator's onboarding |
| POST | /transfer/originator/list | Get status of all originators' onboarding |
| POST | /transfer/refund/create | Create a refund |
| POST | /transfer/refund/get | Retrieve a refund |
| POST | /transfer/refund/cancel | Cancel a refund |
| POST | /transfer/platform/originator/create | Create an originator for Transfer for Platforms customers |
| POST | /transfer/platform/person/create | Create a person associated with an originator |

### bank_transfer
| Method | Path | Description |
|--------|------|-------------|
| POST | /bank_transfer/get | Retrieve a bank transfer |
| POST | /bank_transfer/create | Create a bank transfer |
| POST | /bank_transfer/list | List bank transfers |
| POST | /bank_transfer/cancel | Cancel a bank transfer |
| POST | /bank_transfer/event/list | List bank transfer events |
| POST | /bank_transfer/event/sync | Sync bank transfer events |
| POST | /bank_transfer/sweep/get | Retrieve a sweep |
| POST | /bank_transfer/sweep/list | List sweeps |
| POST | /bank_transfer/balance/get | Get balance of your Bank Transfer account |
| POST | /bank_transfer/migrate_account | Migrate account into Bank Transfers |

### employers
| Method | Path | Description |
|--------|------|-------------|
| POST | /employers/search | Search employer database |

### income
| Method | Path | Description |
|--------|------|-------------|
| POST | /income/verification/create | (Deprecated) Create an income verification instance |
| POST | /income/verification/paystubs/get | (Deprecated) Retrieve information from the paystubs used for income verification |
| POST | /income/verification/documents/download | (Deprecated) Download the original documents used for income verification |
| POST | /income/verification/taxforms/get | (Deprecated) Retrieve information from the tax documents used for income verification |
| POST | /income/verification/precheck | (Deprecated) Check digital income verification eligibility and optimize conversion |

### employment
| Method | Path | Description |
|--------|------|-------------|
| POST | /employment/verification/get | (Deprecated) Retrieve a summary of an individual's employment information |

### beta
| Method | Path | Description |
|--------|------|-------------|
| POST | /beta/credit/v1/bank_employment/get | Retrieve information from the bank accounts used for employment verification |
| POST | /beta/transactions/v1/enhance | enhance locally-held transaction data |
| POST | /beta/transactions/rules/v1/create | Create transaction category rule |
| POST | /beta/transactions/rules/v1/list | Return a list of rules created for the Item associated with the access token. |
| POST | /beta/transactions/rules/v1/remove | Remove transaction rule |
| POST | /beta/transactions/user_insights/v1/get | Obtain user insights based on transactions sent through /transactions/enrich |
| POST | /beta/ewa_report/v1/get | Get EWA Score Report |
| POST | /beta/partner/customer/v1/create | Creates a new end customer for a Plaid reseller. |
| POST | /beta/partner/customer/v1/get | Retrieves the details of a Plaid reseller's end customer. |
| POST | /beta/partner/customer/v1/update | Updates an existing end customer. |
| POST | /beta/partner/customer/v1/enable | Enables a Plaid reseller's end customer in the Production environment. |

### signal
| Method | Path | Description |
|--------|------|-------------|
| POST | /signal/evaluate | Evaluate a planned ACH transaction |
| POST | /signal/schedule | Schedule a planned ACH transaction |
| POST | /signal/decision/report | Report whether you initiated an ACH transaction |
| POST | /signal/return/report | Report a return for an ACH transaction |
| POST | /signal/prepare | Opt-in an Item to Signal Transaction Scores |

### wallet
| Method | Path | Description |
|--------|------|-------------|
| POST | /wallet/create | Create an e-wallet |
| POST | /wallet/get | Fetch an e-wallet |
| POST | /wallet/list | Fetch a list of e-wallets |
| POST | /wallet/transaction/execute | Execute a transaction using an e-wallet |
| POST | /wallet/transaction/get | Fetch an e-wallet transaction |
| POST | /wallet/transaction/list | List e-wallet transactions |

### issues
| Method | Path | Description |
|--------|------|-------------|
| POST | /issues/search | Search for an Issue |
| POST | /issues/get | Get an Issue |
| POST | /issues/subscribe | Subscribe to an Issue |

### payment_profile
| Method | Path | Description |
|--------|------|-------------|
| POST | /payment_profile/create | Create payment profile |
| POST | /payment_profile/get | Get payment profile |
| POST | /payment_profile/remove | Remove payment profile |

### partner
| Method | Path | Description |
|--------|------|-------------|
| POST | /partner/customer/create | Creates a new end customer for a Plaid reseller. |
| POST | /partner/customer/get | Returns a Plaid reseller's end customer. |
| POST | /partner/customer/enable | Enables a Plaid reseller's end customer in the Production environment. |
| POST | /partner/customer/remove | Removes a Plaid reseller's end customer. |
| POST | /partner/customer/oauth_institutions/get | Returns OAuth-institution registration information for a given end customer. |

### link_delivery
| Method | Path | Description |
|--------|------|-------------|
| POST | /link_delivery/create | Create Hosted Link session |
| POST | /link_delivery/get | Get Hosted Link session |

### fdx
| Method | Path | Description |
|--------|------|-------------|
| POST | /fdx/notifications | Webhook receiver for fdx notifications |
| GET | /fdx/recipients | Get Recipients |
| GET | /fdx/recipient/{recipientId} | Get Recipient |

### network_insights
| Method | Path | Description |
|--------|------|-------------|
| POST | /network_insights/report/get | Retrieve network insights for the provided `access_tokens` |

## Enhanced Skill Content
## Question Mapping

- "How do I get a user's bank account balances?" -> POST /accounts/balance/get
- "How do I pull transaction history for a date range?" -> POST /transactions/get
- "How do I verify a user's identity against their bank records?" -> POST /identity/match
- "How do I create a Link token to start the Plaid flow?" -> POST /link/token/create
- "How do I exchange a public token for an access token?" -> POST /item/public_token/exchange
- "How do I initiate an ACH transfer to a user?" -> POST /transfer/authorization/create then POST /transfer/create
- "How do I check if an ACH payment is likely to return?" -> POST /signal/evaluate
- "How do I screen a user against sanctions watchlists?" -> POST /watchlist_screening/individual/create
- "How do I generate an asset report for a mortgage application?" -> POST /asset_report/create then POST /asset_report/get
- "How do I verify someone's employment through payroll?" -> POST /employment/verification/get
- "How do I look up which institutions support a product?" -> POST /institutions/search
- "How do I detect recurring subscriptions in a user's transactions?" -> POST /transactions/recurring/get
- "How do I simulate a webhook in sandbox?" -> POST /sandbox/item/fire_webhook
- "How do I report fraud on a Beacon user?" -> POST /beacon/report/create
- "How do I refresh stale transaction data?" -> POST /transactions/refresh (triggers async update, listen for webhook)

## Response Tips

- **Accounts/Balances/Identity**: Responses nest an `item` object with error state and product availability; always check `item.error` before trusting account data.
- **Transactions**: Uses offset/count pagination (`total_transactions` tells you when to stop) for `/get`; use cursor-based `/sync` for incremental updates (`has_more` + `next_cursor`).
- **Transfer/Bank Transfer**: Lists use offset-based pagination (default `count=25`, `offset=0`); event endpoints add `has_more` boolean.
- **Watchlist/Beacon/Dashboard**: All list endpoints use cursor-based pagination; `next_cursor` is `null` when no more pages exist.
- **Asset Reports**: Creation is async; poll `/asset_report/get` or listen for the webhook before reading the report.
- **Errors**: Every error response includes `error_type`, `error_code`, `display_message`, and `documentation_url`; use `error_code` for programmatic handling, `display_message` for user-facing text.
- **Signal/Protect**: Score fields are nullable; a `null` score means insufficient data rather than low risk.

## Anomaly Flags

- **Item errors**: Surface `item.error` immediately when non-null -- it means the connection is broken and requires user re-authentication (LOGIN_REQUIRED, ITEM_LOCKED).
- **Transfer failures**: Flag `failure_reason.ach_return_code` on any transfer; codes R01 (insufficient funds), R02 (closed account), and R10 (unauthorized) require immediate action.
- **Signal risk tiers**: Proactively warn when `risk_tier` >= 3 on either `customer_initiated_return_risk` or `bank_initiated_return_risk`.
- **Stale balances**: Alert when `balance_last_updated` in signal core attributes is more than 24 hours old -- decisions are based on outdated data.
- **Account frozen**: Flag `is_account_closed` or `is_account_frozen_or_restricted` from signal core attributes before initiating payments.
- **Identity verification risk**: Surface `risk_check.behavior.bot_detected` or `fraud_ring_detected` values other than "no_data"/"not_detected".
- **Beacon duplicates**: Alert when a beacon user creation returns matches -- check `/beacon/duplicate/get` for overlap analysis.
- **Consent expiration**: Flag `consent_expiration_time` on item metadata when it is approaching or past.
- **Webhook verification**: Remind callers to validate webhook signatures via `/webhook_verification_key/get` before trusting payloads.

## Playbook

### 1. Connect a Bank Account and Fetch Transactions

1. Create a user with `POST /user/create` using a stable `client_user_id`.
2. Create a Link token with `POST /link/token/create`, including `products: ["transactions"]` and the user's `client_user_id`.
3. Launch Plaid Link in your frontend with the `link_token`.
4. Exchange the resulting `public_token` via `POST /item/public_token/exchange` to get an `access_token`.
5. Call `POST /transactions/sync` with the `access_token` (no cursor on first call) to pull initial transactions.
6. Store `next_cursor`; on subsequent calls pass it back to get only new/modified/removed transactions.
7. Continue calling `/transactions/sync` while `has_more` is `true`.

### 2. Authorize and Execute an ACH Transfer

1. Call `POST /transfer/authorization/create` with the `access_token`, `account_id`, transfer `type` (debit/credit), `network`, `amount`, and `user` details.
2. Check `authorization.decision` -- proceed only if `"approved"`. If `"declined"`, read `decision_rationale` for the reason.
3. Call `POST /transfer/create` with the `authorization_id` from step 2 and a `description`.
4. Monitor transfer status via `POST /transfer/event/sync` (pass `after_id: 0` on first call, then last seen event ID).
5. Report the outcome to Plaid via `POST /signal/decision/report` with `initiated: true` and the decision details.
6. If the transfer is returned, report it via `POST /signal/return/report` with the `return_code`.

### 3. Run KYC Identity Verification

1. Call `POST /identity_verification/create` with `template_id`, `is_shareable`, and `gave_consent`.
2. Direct the user to the `shareable_url` returned in the response.
3. Poll `POST /identity_verification/get` with the `identity_verification_id` until `status` is no longer `"active"`.
4. Inspect `steps` to see which checks passed/failed (kyc_check, documentary_verification, selfie_check).
5. If failed, call `POST /identity_verification/retry` with `strategy: "reset"` to allow the user another attempt.
6. Review `risk_check` scores for synthetic identity, stolen identity, and behavioral signals.

### 4. Generate and Share an Asset Report

1. Call `POST /asset_report/create` with `access_tokens` and `days_requested` (e.g., 60 for mortgage).
2. Wait for the `PRODUCT_READY` webhook or poll `POST /asset_report/get` until successful.
3. Retrieve the full report via `POST /asset_report/get` with the `asset_report_token`.
4. To share with a third party (e.g., lender), call `POST /asset_report/audit_copy/create` to get an `audit_copy_token`.
5. Provide the `audit_copy_token` to the recipient; they retrieve it via `POST /asset_report/audit_copy/get`.
6. When no longer needed, remove the audit copy with `POST /asset_report/audit_copy/remove`.

### 5. Screen Individuals Against Watchlists

1. Call `POST /watchlist_screening/individual/create` with `search_terms` containing `watchlist_program_id` and the person's `legal_name`.
2. Retrieve hits via `POST /watchlist_screening/individual/hit/list` using the screening `id`.
3. Review each hit; call `POST /watchlist_screening/individual/review/create` with arrays of `confirmed_hits` and `dismissed_hits`.
4. Update the screening status via `POST /watchlist_screening/individual/update` (set to `cleared` or `rejected`).
5. For ongoing monitoring, ensure `is_rescanning_enabled` is true on the program (`POST /watchlist_screening/individual/program/get`).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
