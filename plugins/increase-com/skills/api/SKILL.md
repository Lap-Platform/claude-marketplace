---
name: increase-api
description: "Increase API skill. Use when working with Increase for account_numbers, account_statements, account_transfers. Covers 232 endpoints."
version: 1.0.0
generator: lapsh
---

# Increase API
API version: 0.0.1

## Auth
Bearer bearer

## Base URL
https://api.increase.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /account_numbers -- verify access
3. POST /account_numbers -- create first account_numbers

## Endpoints

232 endpoints across 56 groups. See references/api-spec.lap for full details.

### account_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /account_numbers | List Account Numbers |
| POST | /account_numbers | Create an Account Number |
| GET | /account_numbers/{account_number_id} | Retrieve an Account Number |
| PATCH | /account_numbers/{account_number_id} | Update an Account Number |

### account_statements
| Method | Path | Description |
|--------|------|-------------|
| GET | /account_statements | List Account Statements |
| GET | /account_statements/{account_statement_id} | Retrieve an Account Statement |

### account_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /account_transfers | List Account Transfers |
| POST | /account_transfers | Create an Account Transfer |
| GET | /account_transfers/{account_transfer_id} | Retrieve an Account Transfer |
| POST | /account_transfers/{account_transfer_id}/approve | Approve an Account Transfer |
| POST | /account_transfers/{account_transfer_id}/cancel | Cancel an Account Transfer |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | List Accounts |
| POST | /accounts | Create an Account |
| GET | /accounts/{account_id} | Retrieve an Account |
| PATCH | /accounts/{account_id} | Update an Account |
| GET | /accounts/{account_id}/balance | Retrieve an Account Balance |
| POST | /accounts/{account_id}/close | Close an Account |
| GET | /accounts/{account_id}/intrafi_balance | Get IntraFi balance |

### ach_prenotifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /ach_prenotifications | List ACH Prenotifications |
| POST | /ach_prenotifications | Create an ACH Prenotification |
| GET | /ach_prenotifications/{ach_prenotification_id} | Retrieve an ACH Prenotification |

### ach_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /ach_transfers | List ACH Transfers |
| POST | /ach_transfers | Create an ACH Transfer |
| GET | /ach_transfers/{ach_transfer_id} | Retrieve an ACH Transfer |
| POST | /ach_transfers/{ach_transfer_id}/approve | Approve an ACH Transfer |
| POST | /ach_transfers/{ach_transfer_id}/cancel | Cancel a pending ACH Transfer |

### bookkeeping_accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /bookkeeping_accounts | List Bookkeeping Accounts |
| POST | /bookkeeping_accounts | Create a Bookkeeping Account |
| PATCH | /bookkeeping_accounts/{bookkeeping_account_id} | Update a Bookkeeping Account |
| GET | /bookkeeping_accounts/{bookkeeping_account_id}/balance | Retrieve a Bookkeeping Account Balance |

### bookkeeping_entries
| Method | Path | Description |
|--------|------|-------------|
| GET | /bookkeeping_entries | List Bookkeeping Entries |
| GET | /bookkeeping_entries/{bookkeeping_entry_id} | Retrieve a Bookkeeping Entry |

### bookkeeping_entry_sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /bookkeeping_entry_sets | List Bookkeeping Entry Sets |
| POST | /bookkeeping_entry_sets | Create a Bookkeeping Entry Set |
| GET | /bookkeeping_entry_sets/{bookkeeping_entry_set_id} | Retrieve a Bookkeeping Entry Set |

### card_disputes
| Method | Path | Description |
|--------|------|-------------|
| GET | /card_disputes | List Card Disputes |
| POST | /card_disputes | Create a Card Dispute |
| GET | /card_disputes/{card_dispute_id} | Retrieve a Card Dispute |
| POST | /card_disputes/{card_dispute_id}/submit_user_submission | Submit a User Submission for a Card Dispute |
| POST | /card_disputes/{card_dispute_id}/withdraw | Withdraw a Card Dispute |

### card_payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /card_payments | List Card Payments |
| GET | /card_payments/{card_payment_id} | Retrieve a Card Payment |

### card_purchase_supplements
| Method | Path | Description |
|--------|------|-------------|
| GET | /card_purchase_supplements | List Card Purchase Supplements |
| GET | /card_purchase_supplements/{card_purchase_supplement_id} | Retrieve a Card Purchase Supplement |

### card_push_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /card_push_transfers | List Card Push Transfers |
| POST | /card_push_transfers | Create a Card Push Transfer |
| GET | /card_push_transfers/{card_push_transfer_id} | Retrieve a Card Push Transfer |
| POST | /card_push_transfers/{card_push_transfer_id}/approve | Approve a Card Push Transfer |
| POST | /card_push_transfers/{card_push_transfer_id}/cancel | Cancel a pending Card Push Transfer |

### card_tokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /card_tokens | List Card Tokens |
| GET | /card_tokens/{card_token_id} | Retrieve a Card Token |
| GET | /card_tokens/{card_token_id}/capabilities | Retrieve the capabilities of a Card Token |

### card_validations
| Method | Path | Description |
|--------|------|-------------|
| GET | /card_validations | List Card Validations |
| POST | /card_validations | Create a Card Validation |
| GET | /card_validations/{card_validation_id} | Retrieve a Card Validation |

### cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /cards | List Cards |
| POST | /cards | Create a Card |
| GET | /cards/{card_id} | Retrieve a Card |
| PATCH | /cards/{card_id} | Update a Card |
| POST | /cards/{card_id}/create_details_iframe | Create a Card details iframe |
| GET | /cards/{card_id}/details | Retrieve sensitive details for a Card |
| POST | /cards/{card_id}/update_pin | Update a Card's PIN |

### check_deposits
| Method | Path | Description |
|--------|------|-------------|
| GET | /check_deposits | List Check Deposits |
| POST | /check_deposits | Create a Check Deposit |
| GET | /check_deposits/{check_deposit_id} | Retrieve a Check Deposit |

### check_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /check_transfers | List Check Transfers |
| POST | /check_transfers | Create a Check Transfer |
| GET | /check_transfers/{check_transfer_id} | Retrieve a Check Transfer |
| POST | /check_transfers/{check_transfer_id}/approve | Approve a Check Transfer |
| POST | /check_transfers/{check_transfer_id}/cancel | Cancel a pending Check Transfer |
| POST | /check_transfers/{check_transfer_id}/stop_payment | Stop payment on a Check Transfer |

### declined_transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /declined_transactions | List Declined Transactions |
| GET | /declined_transactions/{declined_transaction_id} | Retrieve a Declined Transaction |

### digital_card_profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /digital_card_profiles | List Card Profiles |
| POST | /digital_card_profiles | Create a Digital Card Profile |
| GET | /digital_card_profiles/{digital_card_profile_id} | Retrieve a Digital Card Profile |
| POST | /digital_card_profiles/{digital_card_profile_id}/archive | Archive a Digital Card Profile |
| POST | /digital_card_profiles/{digital_card_profile_id}/clone | Clones a Digital Card Profile |

### digital_wallet_tokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /digital_wallet_tokens | List Digital Wallet Tokens |
| GET | /digital_wallet_tokens/{digital_wallet_token_id} | Retrieve a Digital Wallet Token |

### entities
| Method | Path | Description |
|--------|------|-------------|
| GET | /entities | List Entities |
| POST | /entities | Create an Entity |
| GET | /entities/{entity_id} | Retrieve an Entity |
| PATCH | /entities/{entity_id} | Update an Entity |
| POST | /entities/{entity_id}/archive | Archive an Entity |
| POST | /entities/{entity_id}/archive_beneficial_owner | Archive a beneficial owner for a corporate Entity |
| POST | /entities/{entity_id}/confirm | Confirm an Entity's details are correct |
| POST | /entities/{entity_id}/create_beneficial_owner | Create a beneficial owner for a corporate Entity |
| POST | /entities/{entity_id}/update_address | Update a Natural Person or Corporation's address |
| POST | /entities/{entity_id}/update_beneficial_owner_address | Update the address for a beneficial owner belonging to a corporate Entity |
| POST | /entities/{entity_id}/update_industry_code | Update the industry code for a corporate Entity |

### entity_supplemental_documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /entity_supplemental_documents | List Entity Supplemental Document Submissions |
| POST | /entity_supplemental_documents | Create a supplemental document for an Entity |

### event_subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /event_subscriptions | List Event Subscriptions |
| POST | /event_subscriptions | Create an Event Subscription |
| GET | /event_subscriptions/{event_subscription_id} | Retrieve an Event Subscription |
| PATCH | /event_subscriptions/{event_subscription_id} | Update an Event Subscription |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | List Events |
| GET | /events/{event_id} | Retrieve an Event |

### exports
| Method | Path | Description |
|--------|------|-------------|
| GET | /exports | List Exports |
| POST | /exports | Create an Export |
| GET | /exports/{export_id} | Retrieve an Export |

### external_accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /external_accounts | List External Accounts |
| POST | /external_accounts | Create an External Account |
| GET | /external_accounts/{external_account_id} | Retrieve an External Account |
| PATCH | /external_accounts/{external_account_id} | Update an External Account |

### fednow_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /fednow_transfers | List FedNow Transfers |
| POST | /fednow_transfers | Create a FedNow Transfer |
| GET | /fednow_transfers/{fednow_transfer_id} | Retrieve a FedNow Transfer |
| POST | /fednow_transfers/{fednow_transfer_id}/approve | Approve a FedNow Transfer |
| POST | /fednow_transfers/{fednow_transfer_id}/cancel | Cancel a pending FedNow Transfer |

### file_links
| Method | Path | Description |
|--------|------|-------------|
| POST | /file_links | Create a File Link |

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /files | List Files |
| POST | /files | Create a File |
| GET | /files/{file_id} | Retrieve a File |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups/current | Retrieve Group details |

### inbound_ach_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_ach_transfers | List Inbound ACH Transfers |
| GET | /inbound_ach_transfers/{inbound_ach_transfer_id} | Retrieve an Inbound ACH Transfer |
| POST | /inbound_ach_transfers/{inbound_ach_transfer_id}/create_notification_of_change | Create a notification of change for an Inbound ACH Transfer |
| POST | /inbound_ach_transfers/{inbound_ach_transfer_id}/decline | Decline an Inbound ACH Transfer |
| POST | /inbound_ach_transfers/{inbound_ach_transfer_id}/transfer_return | Return an Inbound ACH Transfer |

### inbound_check_deposits
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_check_deposits | List Inbound Check Deposits |
| GET | /inbound_check_deposits/{inbound_check_deposit_id} | Retrieve an Inbound Check Deposit |
| POST | /inbound_check_deposits/{inbound_check_deposit_id}/decline | Decline an Inbound Check Deposit |
| POST | /inbound_check_deposits/{inbound_check_deposit_id}/return | Return an Inbound Check Deposit |

### inbound_fednow_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_fednow_transfers | List Inbound FedNow Transfers |
| GET | /inbound_fednow_transfers/{inbound_fednow_transfer_id} | Retrieve an Inbound FedNow Transfer |

### inbound_mail_items
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_mail_items | List Inbound Mail Items |
| GET | /inbound_mail_items/{inbound_mail_item_id} | Retrieve an Inbound Mail Item |
| POST | /inbound_mail_items/{inbound_mail_item_id}/action | Action an Inbound Mail Item |

### inbound_real_time_payments_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_real_time_payments_transfers | List Inbound Real-Time Payments Transfers |
| GET | /inbound_real_time_payments_transfers/{inbound_real_time_payments_transfer_id} | Retrieve an Inbound Real-Time Payments Transfer |

### inbound_wire_drawdown_requests
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_wire_drawdown_requests | List Inbound Wire Drawdown Requests |
| GET | /inbound_wire_drawdown_requests/{inbound_wire_drawdown_request_id} | Retrieve an Inbound Wire Drawdown Request |

### inbound_wire_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_wire_transfers | List Inbound Wire Transfers |
| GET | /inbound_wire_transfers/{inbound_wire_transfer_id} | Retrieve an Inbound Wire Transfer |
| POST | /inbound_wire_transfers/{inbound_wire_transfer_id}/reverse | Reverse an Inbound Wire Transfer |

### intrafi_account_enrollments
| Method | Path | Description |
|--------|------|-------------|
| GET | /intrafi_account_enrollments | List IntraFi Account Enrollments |
| POST | /intrafi_account_enrollments | Enroll an account in the IntraFi deposit sweep network |
| GET | /intrafi_account_enrollments/{intrafi_account_enrollment_id} | Get an IntraFi Account Enrollment |
| POST | /intrafi_account_enrollments/{intrafi_account_enrollment_id}/unenroll | Unenroll an account from IntraFi |

### intrafi_exclusions
| Method | Path | Description |
|--------|------|-------------|
| GET | /intrafi_exclusions | List IntraFi Exclusions |
| POST | /intrafi_exclusions | Create an IntraFi Exclusion |
| GET | /intrafi_exclusions/{intrafi_exclusion_id} | Get an IntraFi Exclusion |
| POST | /intrafi_exclusions/{intrafi_exclusion_id}/archive | Archive an IntraFi Exclusion |

### lockboxes
| Method | Path | Description |
|--------|------|-------------|
| GET | /lockboxes | List Lockboxes |
| POST | /lockboxes | Create a Lockbox |
| GET | /lockboxes/{lockbox_id} | Retrieve a Lockbox |
| PATCH | /lockboxes/{lockbox_id} | Update a Lockbox |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/tokens | Create an OAuth Token |

### oauth_applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth_applications | List OAuth Applications |
| GET | /oauth_applications/{oauth_application_id} | Retrieve an OAuth Application |

### oauth_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth_connections | List OAuth Connections |
| GET | /oauth_connections/{oauth_connection_id} | Retrieve an OAuth Connection |

### pending_transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /pending_transactions | List Pending Transactions |
| POST | /pending_transactions | Create a Pending Transaction |
| GET | /pending_transactions/{pending_transaction_id} | Retrieve a Pending Transaction |
| POST | /pending_transactions/{pending_transaction_id}/release | Release a user-initiated Pending Transaction |

### physical_card_profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /physical_card_profiles | List Physical Card Profiles |
| POST | /physical_card_profiles | Create a Physical Card Profile |
| GET | /physical_card_profiles/{physical_card_profile_id} | Retrieve a Card Profile |
| POST | /physical_card_profiles/{physical_card_profile_id}/archive | Archive a Physical Card Profile |
| POST | /physical_card_profiles/{physical_card_profile_id}/clone | Clone a Physical Card Profile |

### physical_cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /physical_cards | List Physical Cards |
| POST | /physical_cards | Create a Physical Card |
| GET | /physical_cards/{physical_card_id} | Retrieve a Physical Card |
| PATCH | /physical_cards/{physical_card_id} | Update a Physical Card |

### programs
| Method | Path | Description |
|--------|------|-------------|
| GET | /programs | List Programs |
| GET | /programs/{program_id} | Retrieve a Program |

### real_time_decisions
| Method | Path | Description |
|--------|------|-------------|
| GET | /real_time_decisions/{real_time_decision_id} | Retrieve a Real-Time Decision |
| POST | /real_time_decisions/{real_time_decision_id}/action | Action a Real-Time Decision |

### real_time_payments_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /real_time_payments_transfers | List Real-Time Payments Transfers |
| POST | /real_time_payments_transfers | Create a Real-Time Payments Transfer |
| GET | /real_time_payments_transfers/{real_time_payments_transfer_id} | Retrieve a Real-Time Payments Transfer |
| POST | /real_time_payments_transfers/{real_time_payments_transfer_id}/approve | Approve a Real-Time Payments Transfer |
| POST | /real_time_payments_transfers/{real_time_payments_transfer_id}/cancel | Cancel a pending Real-Time Payments Transfer |

### routing_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /routing_numbers | List Routing Numbers |

### simulations
| Method | Path | Description |
|--------|------|-------------|
| POST | /simulations/account_statements | Sandbox: Create an Account Statement |
| POST | /simulations/account_transfers/{account_transfer_id}/complete | Sandbox: Approve an Account Transfer |
| POST | /simulations/ach_transfers/{ach_transfer_id}/acknowledge | Sandbox: Acknowledge an ACH Transfer |
| POST | /simulations/ach_transfers/{ach_transfer_id}/create_notification_of_change | Sandbox: Create a Notification of Change for an ACH Transfer |
| POST | /simulations/ach_transfers/{ach_transfer_id}/return | Sandbox: Return an ACH Transfer |
| POST | /simulations/ach_transfers/{ach_transfer_id}/settle | Sandbox: Settle an ACH Transfer |
| POST | /simulations/ach_transfers/{ach_transfer_id}/submit | Sandbox: Submit an ACH Transfer |
| POST | /simulations/card_authorization_expirations | Sandbox: Expire a Card Authorization |
| POST | /simulations/card_authorizations | Sandbox: Create a Card Authorization |
| POST | /simulations/card_balance_inquiries | Sandbox: Create a Card Balance Inquiry |
| POST | /simulations/card_disputes/{card_dispute_id}/action | Sandbox: Advance the state of a Card Dispute |
| POST | /simulations/card_fuel_confirmations | Sandbox: Confirm the fuel pump amount for a Card Authorization |
| POST | /simulations/card_increments | Sandbox: Increment a Card Authorization |
| POST | /simulations/card_refunds | Sandbox: Refund a card transaction |
| POST | /simulations/card_reversals | Sandbox: Reverse a Card Authorization |
| POST | /simulations/card_settlements | Sandbox: Settle a Card Authorization |
| POST | /simulations/card_tokens | Sandbox: Create a Card Token |
| POST | /simulations/check_deposits/{check_deposit_id}/reject | Sandbox: Reject a Check Deposit |
| POST | /simulations/check_deposits/{check_deposit_id}/return | Sandbox: Return a Check Deposit |
| POST | /simulations/check_deposits/{check_deposit_id}/submit | Sandbox: Submit a Check Deposit |
| POST | /simulations/check_transfers/{check_transfer_id}/mail | Sandbox: Mail a Check Transfer |
| POST | /simulations/digital_wallet_token_requests | Sandbox: Create a digital wallet token request |
| POST | /simulations/exports | Sandbox: Generate a Tax Form Export |
| POST | /simulations/inbound_ach_transfers | Sandbox: Create an Inbound ACH Transfer |
| POST | /simulations/inbound_check_deposits | Sandbox: Create an Inbound Check Deposit |
| POST | /simulations/inbound_fednow_transfers | Sandbox: Create an Inbound FedNow Transfer |
| POST | /simulations/inbound_mail_items | Sandbox: Create an Inbound Mail Item |
| POST | /simulations/inbound_real_time_payments_transfers | Sandbox: Create an Inbound Real-Time Payments Transfer |
| POST | /simulations/inbound_wire_drawdown_requests | Sandbox: Create an Inbound Wire Drawdown request |
| POST | /simulations/inbound_wire_transfers | Sandbox: Create an Inbound Wire Transfer |
| POST | /simulations/interest_payments | Sandbox: Create an interest payment |
| POST | /simulations/pending_transactions/{pending_transaction_id}/release_inbound_funds_hold | Sandbox: Release an Inbound Funds Hold |
| POST | /simulations/physical_cards/{physical_card_id}/advance_shipment | Sandbox: Advance the shipment status of a Physical Card |
| POST | /simulations/physical_cards/{physical_card_id}/tracking_updates | Sandbox: Create a Physical Card Shipment Tracking Update |
| POST | /simulations/programs | Sandbox: Create a Program |
| POST | /simulations/real_time_payments_transfers/{real_time_payments_transfer_id}/complete | Sandbox: Complete a Real-Time Payments Transfer |
| POST | /simulations/wire_drawdown_requests/{wire_drawdown_request_id}/refuse | Sandbox: Refuse a Wire Drawdown Request |
| POST | /simulations/wire_drawdown_requests/{wire_drawdown_request_id}/submit | Sandbox: Submit a Wire Drawdown Request |
| POST | /simulations/wire_transfers/{wire_transfer_id}/reverse | Sandbox: Reverse a Wire Transfer |
| POST | /simulations/wire_transfers/{wire_transfer_id}/submit | Sandbox: Submit a Wire Transfer |

### swift_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /swift_transfers | List Swift Transfers |
| POST | /swift_transfers | Create a Swift Transfer |
| GET | /swift_transfers/{swift_transfer_id} | Retrieve a Swift Transfer |
| POST | /swift_transfers/{swift_transfer_id}/approve | Approve a Swift Transfer |
| POST | /swift_transfers/{swift_transfer_id}/cancel | Cancel a pending Swift Transfer |

### transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /transactions | List Transactions |
| GET | /transactions/{transaction_id} | Retrieve a Transaction |

### wire_drawdown_requests
| Method | Path | Description |
|--------|------|-------------|
| GET | /wire_drawdown_requests | List Wire Drawdown Requests |
| POST | /wire_drawdown_requests | Create a Wire Drawdown Request |
| GET | /wire_drawdown_requests/{wire_drawdown_request_id} | Retrieve a Wire Drawdown Request |

### wire_transfers
| Method | Path | Description |
|--------|------|-------------|
| GET | /wire_transfers | List Wire Transfers |
| POST | /wire_transfers | Create a Wire Transfer |
| GET | /wire_transfers/{wire_transfer_id} | Retrieve a Wire Transfer |
| POST | /wire_transfers/{wire_transfer_id}/approve | Approve a Wire Transfer |
| POST | /wire_transfers/{wire_transfer_id}/cancel | Cancel a pending Wire Transfer |

## Enhanced Skill Content
## Question Mapping

- "How do I list all accounts?" -> GET /accounts
- "What is the current balance of a specific account?" -> GET /accounts/{account_id}/balance
- "How do I send money to another Increase account?" -> POST /account_transfers
- "How do I initiate an ACH payment to an external bank?" -> POST /ach_transfers
- "How do I send a wire transfer?" -> POST /wire_transfers
- "What transactions happened on my account this month?" -> GET /transactions
- "Are there any pending transactions I should know about?" -> GET /pending_transactions
- "How do I create a new card for an account?" -> POST /cards
- "How do I dispute a card charge?" -> POST /card_disputes
- "How do I onboard a new business entity?" -> POST /entities
- "How do I set up a webhook to receive events?" -> POST /event_subscriptions
- "How do I send a real-time payment?" -> POST /real_time_payments_transfers
- "How do I export my transaction history as CSV?" -> POST /exports
- "How do I cancel a transfer that requires approval?" -> POST /ach_transfers/{ach_transfer_id}/cancel
- "How do I look up a routing number?" -> GET /routing_numbers

## Response Tips

- **List endpoints** (GET /accounts, GET /transactions, etc.): All return `{data: [...], next_cursor}`. Pass `next_cursor` as `cursor` on the next request to paginate. A null `next_cursor` means no more pages. Use `limit` to control page size.
- **Transfer objects** (ACH, wire, FedNow, RTP, account, check, SWIFT): Check `status` field for lifecycle state. The `approval`, `cancellation`, `submission`, and `return` sub-objects are null until the corresponding event occurs.
- **Entity objects**: The response shape is polymorphic -- only the sub-object matching `structure` (corporation, natural_person, joint, trust, government_authority) is populated; others are null.
- **Transaction/pending_transaction source**: Contains a `category` discriminator field; only the matching sub-object within `source` is non-null.
- **Error responses** (4XX): All endpoints return 4XX errors. Inspect the response body for structured error details including the specific validation failure.
- **Amount fields**: All monetary amounts are integers in the smallest currency unit (cents for USD). Divide by 100 for display.

## Anomaly Flags

- **Transfer returned or rejected**: Surface immediately when an ACH transfer's `return` field becomes non-null, a FedNow transfer's `rejection` appears, or an RTP transfer shows a `rejection` -- these indicate failed payments requiring action.
- **Declined transactions appearing**: Any new entries from GET /declined_transactions signal blocked payments. Check `source.category` (ach_decline, card_decline, wire_decline, check_decline) and surface the decline reason.
- **Transfers pending approval**: When `status` is `pending_approval` on any transfer type (ACH, wire, check, FedNow, RTP, SWIFT, card push, account transfer), flag it as requiring human action before the `require_approval` deadline.
- **Inbound ACH auto-resolve deadline**: Inbound ACH transfers have `automatically_resolves_at` -- if this timestamp is approaching and the transfer hasn't been accepted or declined, alert immediately.
- **Card dispute submission deadline**: `user_submission_required_by` on card disputes is a hard deadline. Surface when within 48 hours.
- **Real-time decision timeout**: `timeout_at` on real-time decisions is extremely short-lived. Any unactioned decision nearing timeout should be the highest-priority alert.
- **Entity status changes**: If an entity moves to a non-active status, all associated accounts and cards may be affected. Surface entity `status` changes proactively.
- **ACH notifications of change**: When `notifications_of_change` array is non-empty on an ACH transfer, the receiving bank is signaling incorrect account details. Update your records.
- **Check transfer stop payment**: If `stop_payment_request` becomes non-null, the check may have been intercepted or reported. Investigate immediately.

## Playbook

### 1. Open a New Account and Issue a Card

1. Create the entity: POST /entities with `structure: "corporation"` or `"natural_person"` and required identity details
2. Confirm entity details: POST /entities/{entity_id}/confirm
3. Create the account: POST /accounts with `name` and `entity_id` from step 1
4. Create an account number: POST /account_numbers with `account_id` and `name`
5. Issue a virtual card: POST /cards with `account_id` and optional `billing_address`
6. (Optional) Order a physical card: POST /physical_cards with `card_id`, `cardholder`, and `shipment` details

### 2. Send an ACH Payment with Approval Flow

1. Register the external account: POST /external_accounts with `account_number`, `routing_number`, `description`
2. (Optional) Send a prenotification: POST /ach_prenotifications with account details to validate before sending real money
3. Create the transfer with approval required: POST /ach_transfers with `account_id`, `amount`, `statement_descriptor`, `external_account_id`, and `require_approval: true`
4. Review and approve: POST /ach_transfers/{ach_transfer_id}/approve
5. Monitor status: GET /ach_transfers/{ach_transfer_id} -- watch for `status` progressing through submitted, acknowledged, settled
6. Handle returns: If `return` field becomes non-null, inspect the return reason and take corrective action

### 3. Process an Inbound ACH Transfer

1. Set up an event subscription: POST /event_subscriptions with `url` and `selected_event_category: "inbound_ach_transfer.created"`
2. When notified, retrieve the transfer: GET /inbound_ach_transfers/{inbound_ach_transfer_id}
3. Decide: either let it auto-resolve by `automatically_resolves_at`, or explicitly:
   - Accept by taking no action (auto-accepts), or
   - Decline: POST /inbound_ach_transfers/{id}/decline with a `reason`, or
   - Return after acceptance: POST /inbound_ach_transfers/{id}/transfer_return with a `reason`
4. (Optional) Issue a notification of change if account details need updating: POST /inbound_ach_transfers/{id}/create_notification_of_change

### 4. File and Track a Card Dispute

1. Identify the disputed transaction from GET /transactions or GET /card_payments
2. Create the dispute: POST /card_disputes with `disputed_transaction_id`, `network`, and category-specific evidence under `visa`
3. Monitor status: GET /card_disputes/{card_dispute_id} -- watch for `status` changes and check `user_submission_required_by`
4. If further evidence is requested: POST /card_disputes/{id}/submit_user_submission with additional documentation
5. Resolution: Check `win`, `loss`, or `withdrawal` fields for the final outcome

### 5. Export Account Data for Reconciliation

1. Create a transaction CSV export: POST /exports with `category: "transaction_csv"` and date filters in `transaction_csv.created_at`
2. Poll for completion: GET /exports/{export_id} until `status` changes from `pending` to `complete`
3. Download the file: Retrieve `result.file_id` from the export, then POST /file_links with `file_id` to get a temporary `unauthenticated_url`
4. (Optional) Create a balance CSV for the same period: POST /exports with `category: "balance_csv"`
5. (Optional) Generate an account statement: POST /exports with `category: "account_statement_ofx"` or `"account_statement_bai2"` for standard formats


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
