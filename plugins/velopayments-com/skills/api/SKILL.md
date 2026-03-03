---
name: velo-payments-apis
description: "Velo Payments APIs API skill. Use when working with Velo Payments APIs for authenticate, logout, password. Covers 109 endpoints."
version: 1.0.0
generator: lapsh
---

# Velo Payments APIs
API version: 2.38.183

## Auth
OAuth2 | Bearer basic | OAuth2

## Base URL
https://api.sandbox.velopayments.com/

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/users -- verify access
3. POST /v1/authenticate -- create first authenticate

## Endpoints

109 endpoints across 20 groups. See references/api-spec.lap for full details.

### authenticate
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/authenticate | Authentication endpoint |

### logout
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/logout | Logout |

### password
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/password/reset | Reset password |

### validate
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/validate | validate |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/users | List Users |
| DELETE | /v2/users/{userId} | Delete a User |
| GET | /v2/users/{userId} | Get User |
| POST | /v2/users/{userId}/disable | Disable a User |
| POST | /v2/users/{userId}/enable | Enable a User |
| POST | /v2/users/invite | Invite a User |
| POST | /v2/users/{userId}/roleUpdate | Update User Role |
| POST | /v2/users/{userId}/mfa/unregister | Unregister MFA for the user |
| POST | /v2/users/{userId}/tokens | Resend a token |
| POST | /v2/users/{userId}/unlock | Unlock a User |
| POST | /v2/users/{userId}/userDetailsUpdate | Update User Details |
| POST | /v2/users/registration/sms | Register SMS Number |
| GET | /v2/users/self | Get Self |
| POST | /v2/users/self/userDetailsUpdate | Update User Details for self |
| POST | /v2/users/self/mfa/unregister | Unregister MFA for Self |
| POST | /v2/users/self/password | Update Password for self |
| POST | /v2/users/self/password/validate | Validate the proposed password |

### payors
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/payors/{payorId} | Get Payor |
| POST | /v1/payors/{payorId}/applications | Create Application |
| POST | /v1/payors/{payorId}/applications/{applicationId}/keys | Create API Key |
| POST | /v1/payors/{payorId}/reminderEmailsUpdate | Reminder Email Opt-Out |
| POST | /v1/payors/{payorId}/branding/logos | Add Logo |
| GET | /v1/payors/{payorId}/branding | Get Branding |

### payorLinks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/payorLinks | List Payor Links |
| POST | /v1/payorLinks | Create a Payor Link |

### payees
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v3/payees/{payeeId} | Delete Payee by Id |
| GET | /v3/payees/{payeeId} | Get Payee by Id |
| GET | /v3/payees | List Payees |
| POST | /v3/payees | Initiate Payee Creation |
| GET | /v3/payees/batch/{batchId} | Query Batch Status |
| POST | /v3/payees/{payeeId}/invite | Resend Payee Invite |
| GET | /v3/payees/payors/{payorId}/invitationStatus | Get Payee Invitation Status |
| GET | /v3/payees/deltas | List Payee Changes |
| POST | /v3/payees/{payeeId}/remoteIdUpdate | Update Payee Remote Id |
| POST | /v3/payees/{payeeId}/payeeDetailsUpdate | Update Payee Details |
| DELETE | /v4/payees/{payeeId} | Delete Payee by Id |
| GET | /v4/payees/{payeeId} | Get Payee by Id |
| POST | /v4/payees/{payeeId}/payeeDetailsUpdate | Update Payee Details |
| POST | /v4/payees/{payeeId}/remoteIdUpdate | Update Payee Remote Id |
| GET | /v4/payees | List Payees |
| POST | /v4/payees | Initiate Payee Creation |
| GET | /v4/payees/batch/{batchId} | Query Batch Status |
| POST | /v4/payees/{payeeId}/invite | Resend Payee Invite |
| GET | /v4/payees/payors/{payorId}/invitationStatus | Get Payee Invitation Status |
| GET | /v4/payees/deltas | List Payee Changes |
| GET | /v4/payees/{payeeId}/paymentChannels/ | Get All Payment Channels Details |
| POST | /v4/payees/{payeeId}/paymentChannels/ | Create Payment Channel |
| DELETE | /v4/payees/{payeeId}/paymentChannels/{paymentChannelId} | Delete Payment Channel |
| GET | /v4/payees/{payeeId}/paymentChannels/{paymentChannelId} | Get Payment Channel Details |
| POST | /v4/payees/{payeeId}/paymentChannels/{paymentChannelId} | Update Payment Channel |
| POST | /v4/payees/{payeeId}/paymentChannels/{paymentChannelId}/enable | Enable Payment Channel |
| PUT | /v4/payees/{payeeId}/paymentChannels/order | Update Payees preferred Payment Channel order |

### sourceAccounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/sourceAccounts/{sourceAccountId}/notifications | Set notifications |
| POST | /v2/sourceAccounts/{sourceAccountId}/fundingRequest | Create Funding Request |
| GET | /v2/sourceAccounts | Get list of source accounts |
| GET | /v2/sourceAccounts/{sourceAccountId} | Get Source Account |
| POST | /v2/sourceAccounts/{sourceAccountId}/transfers | Transfer Funds between source accounts |
| POST | /v3/sourceAccounts/{sourceAccountId}/fundingRequest | Create Funding Request |
| GET | /v3/sourceAccounts | Get list of source accounts |
| DELETE | /v3/sourceAccounts/{sourceAccountId} | Delete a source account by ID |
| GET | /v3/sourceAccounts/{sourceAccountId} | Get details about given source account. |
| POST | /v3/sourceAccounts/{sourceAccountId}/transfers | Transfer Funds between source accounts |
| POST | /v3/sourceAccounts/{sourceAccountId}/notifications | Set notifications |

### fundingAccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/fundingAccounts | Get Funding Accounts |
| POST | /v2/fundingAccounts | Create Funding Account |
| GET | /v2/fundingAccounts/{fundingAccountId} | Get Funding Account |

### deltas
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/deltas/fundings | Get Funding Audit Delta |
| GET | /v1/deltas/payments | V1 List Payment Changes |

### fundings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/fundings/{fundingId} | Get Funding |

### transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/transactions | Get Transactions |
| POST | /v1/transactions | Create a Transaction |
| GET | /v1/transactions/{transactionId} | Get Transaction |

### paymentaudit
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/paymentaudit/fundings | V1 Get Fundings for Payor |
| GET | /v1/paymentaudit/payoutStatistics | V1 Get Payout Statistics |
| GET | /v3/paymentaudit/payouts | V3 Get Payouts for Payor |
| GET | /v3/paymentaudit/payouts/{payoutId} | V3 Get Payments for Payout |
| GET | /v3/paymentaudit/payments | V3 Get List of Payments |
| GET | /v3/paymentaudit/payments/{paymentId} | V3 Get Payment |
| GET | /v3/paymentaudit/transactions | V3 Export Transactions |
| GET | /v4/paymentaudit/payouts | Get Payouts for Payor |
| GET | /v4/paymentaudit/payouts/{payoutId} | Get Payments for Payout |
| GET | /v4/paymentaudit/payments | Get List of Payments |
| GET | /v4/paymentaudit/payments/{paymentId} | Get Payment |
| GET | /v4/paymentaudit/fundings | Get Fundings for Payor |
| GET | /v4/paymentaudit/payoutStatistics | Get Payout Statistics |
| GET | /v4/paymentaudit/transactions | Export Transactions |

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/payments/deltas | List Payment Changes |
| POST | /v1/payments/{paymentId}/withdraw | Withdraw a Payment |

### payouts
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/payouts | Submit Payout |
| DELETE | /v3/payouts/{payoutId} | Withdraw Payout |
| GET | /v3/payouts/{payoutId} | Get Payout Summary |
| POST | /v3/payouts/{payoutId} | Instruct Payout |
| POST | /v3/payouts/{payoutId}/quote | Create a quote for the payout |
| GET | /v3/payouts/{payoutId}/payments | Retrieve payments for a payout |
| DELETE | /v3/payouts/{payoutId}/schedule | Deschedule a payout |
| POST | /v3/payouts/{payoutId}/schedule | Schedule a payout |

### paymentChannelRules
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/paymentChannelRules | List Payment Channel Country Rules |

### supportedCountries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/supportedCountries | List Supported Countries |
| GET | /v2/supportedCountries | List Supported Countries |

### currencies
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/currencies | List Supported Currencies |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/webhooks | List the details about the webhooks for the given payor. |
| POST | /v1/webhooks | Create Webhook |
| GET | /v1/webhooks/{webhookId} | Get details about the given webhook. |
| POST | /v1/webhooks/{webhookId} | Update Webhook |
| POST | /v1/webhooks/{webhookId}/ping |  |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the Velo API?" -> POST /v1/authenticate
- "How do I log out of my session?" -> POST /v1/logout
- "How do I reset a user's password?" -> POST /v1/password/reset
- "How do I list all payees for a payor?" -> GET /v4/payees
- "How do I onboard a new payee?" -> POST /v4/payees
- "What is the status of a payee batch import?" -> GET /v4/payees/batch/{batchId}
- "How do I create and submit a payout?" -> POST /v3/payouts, then POST /v3/payouts/{payoutId}/quote, then POST /v3/payouts/{payoutId}
- "How do I check the status of a payment?" -> GET /v4/paymentaudit/payments/{paymentId}
- "How do I see my source account balances?" -> GET /v3/sourceAccounts
- "How do I transfer funds between source accounts?" -> POST /v3/sourceAccounts/{sourceAccountId}/transfers
- "How do I invite a user to the platform?" -> POST /v2/users/invite
- "How do I set up a webhook for payment notifications?" -> POST /v1/webhooks
- "What payee records changed since yesterday?" -> GET /v4/payees/deltas
- "How do I withdraw a payment before it settles?" -> POST /v1/payments/{paymentId}/withdraw
- "How do I get payout statistics for this month?" -> GET /v4/paymentaudit/payoutStatistics

## Response Tips

- **Paginated lists** (users, payees, payments, payouts, source accounts, fundings, webhooks): Response contains `page` (numberOfElements, totalElements, totalPages, page, pageSize), `links` for HATEOAS navigation, and `content` array with the actual records. Always check `totalPages` to determine if more pages exist.
- **Batch operations** (POST payees): Returns a `batchId` and `rejectedCsvRows` array immediately; poll GET /v4/payees/batch/{batchId} for `status`, `failureCount`, `pendingCount`, and `failures` array until processing completes.
- **Authentication**: POST /v1/authenticate returns `access_token`, `expires_in` (seconds), and `entityIds` (array of payor/payee UUIDs the token grants access to). Use the access token as `Bearer` in subsequent requests.
- **Payouts**: GET /v3/payouts/{payoutId} nests `fxSummaries`, `accounts`, `acceptedPayments`, `rejectedPayments`, and `schedule` -- inspect `rejectedPayments` for failures before submitting.
- **204 responses**: Most mutation endpoints (update, delete, disable, enable) return empty 204 bodies -- success is indicated by status code alone.
- **Sensitive data**: Payee and payment channel endpoints accept `sensitive=true` to include masked account numbers and routing numbers; defaults to redacted.
- **Delta endpoints**: Return records changed since `updatedSince` (ISO 8601 datetime) -- use these for incremental sync rather than full list pulls.

## Anomaly Flags

- **Token expiry approaching**: Surface a warning when `expires_in` from authentication is below 300 seconds; prompt for re-authentication.
- **Batch import failures**: Flag immediately when GET /v4/payees/batch/{batchId} shows `failureCount > 0` and list the failure reasons.
- **Rejected payments in payout**: After creating a payout, if GET /v3/payouts/{payoutId} shows `paymentsRejected > 0`, surface the rejected payment details before the user attempts to submit.
- **Low source account balance**: When GET /v3/sourceAccounts/{id} returns a `balance` near or below the `notifications.minimumBalance` threshold, warn the user and suggest a funding request.
- **Payout status INCOMPLETE or WITHDRAWN**: Flag payouts with unexpected terminal states and surface the reason.
- **Failed payments count rising**: If GET /v4/paymentaudit/payoutStatistics shows `thisMonthFailedPaymentsCount` increasing across calls, alert the user to investigate.
- **409 Conflict errors**: These indicate concurrent modification or duplicate operations (duplicate payee invite, payment channel already exists) -- surface the conflict detail and suggest corrective action.
- **User locked out**: When GET /v2/users/{userId} returns `lockedOut: true`, proactively note the `lockedOutTimestamp` and suggest using POST /v2/users/{userId}/unlock.
- **Deprecated v3 endpoints**: When v4 equivalents exist (payees, payment audit), flag usage of v3 endpoints and recommend migration.

## Playbook

### 1. Authenticate and Set Up a Session

1. POST /v1/authenticate with `grant_type=client_credentials` (uses HTTP Basic Auth with API key and secret)
2. Store the returned `access_token` and note `expires_in` for refresh timing
3. If MFA is required, POST /v1/validate with the OTP code to get a fully scoped token
4. Use the `entityIds` array to determine which payor/payee contexts are available
5. Set `Authorization: Bearer {access_token}` on all subsequent requests

### 2. Onboard Payees and Verify Batch Status

1. POST /v4/payees with the `payorId` and array of payee objects (email, remoteId, type, address, payment channel, individual/company details)
2. Capture the returned `batchId` from the 201 response
3. Poll GET /v4/payees/batch/{batchId} until `status` is no longer processing
4. Review `failures` array for any rejected records and correct the data
5. For successfully created payees, POST /v4/payees/{payeeId}/invite to send onboarding invitations
6. Monitor invitation status via GET /v4/payees/payors/{payorId}/invitationStatus

### 3. Create, Quote, and Submit a Payout

1. Ensure the source account has sufficient funds: GET /v3/sourceAccounts to check balances
2. If funds are low, POST /v3/sourceAccounts/{sourceAccountId}/fundingRequest to request a top-up
3. POST /v3/payouts with the payments array (each payment needs `remoteId`, `currency`, `amount`)
4. POST /v3/payouts/{payoutId}/quote to get FX rates and summaries
5. Review the quote: GET /v3/payouts/{payoutId} to inspect accepted vs rejected payments
6. POST /v3/payouts/{payoutId} to submit (optionally set `fxRateDegradationThresholdPercentage`)
7. Optionally schedule instead: POST /v3/payouts/{payoutId}/schedule with `scheduledFor` datetime

### 4. Monitor Payments and Handle Issues

1. GET /v4/paymentaudit/payments with date range and status filters to find payments of interest
2. For a specific payment, GET /v4/paymentaudit/payments/{paymentId} with `sensitive=true` for full details
3. Check the `events` array for the payment lifecycle timeline
4. If a payment is in ACCEPTED or AWAITING_FUNDS status and needs to be cancelled, POST /v1/payments/{paymentId}/withdraw with a reason
5. For ongoing monitoring, use GET /v4/payments/deltas with `updatedSince` to catch status changes incrementally

### 5. Configure Webhooks for Real-Time Notifications

1. POST /v1/webhooks with `payorId`, `webhookUrl`, `enabled: true`, and desired `categories`
2. Optionally set `authorizationHeader` for your endpoint to verify incoming calls
3. POST /v1/webhooks/{webhookId}/ping to test delivery and confirm your endpoint responds correctly
4. GET /v1/webhooks/{webhookId} to verify the configuration is saved
5. To pause notifications, POST /v1/webhooks/{webhookId} with `enabled: false`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
