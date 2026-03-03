---
name: configuration-api
description: "Configuration API skill. Use when working with Configuration for accountHolders, balanceAccounts, balancePlatforms. Covers 79 endpoints."
version: 1.0.0
generator: lapsh
---

# Configuration API
API version: 2

## Auth
ApiKey X-API-Key in header | Bearer basic | ApiKey clientKey in query

## Base URL
https://balanceplatform-api-test.adyen.com/bcl/v2

## Setup
1. Set Authorization header with your Bearer token
2. GET /cardorders -- verify access
3. POST /accountHolders -- create first accountHolders

## Endpoints

79 endpoints across 17 groups. See references/api-spec.lap for full details.

### accountHolders
| Method | Path | Description |
|--------|------|-------------|
| POST | /accountHolders | Create an account holder |
| GET | /accountHolders/{id} | Get an account holder |
| PATCH | /accountHolders/{id} | Update an account holder |
| GET | /accountHolders/{id}/balanceAccounts | Get all balance accounts of an account holder |
| GET | /accountHolders/{id}/taxForms | Get a tax form |
| GET | /accountHolders/{id}/transactionRules | Get all transaction rules for an account holder |
| GET | /accountHolders/{id}/taxFormSummary | Get summary of tax forms for an account holder |

### balanceAccounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /balanceAccounts | Create a balance account |
| GET | /balanceAccounts/{balanceAccountId}/sweeps | Get all sweeps for a balance account |
| POST | /balanceAccounts/{balanceAccountId}/sweeps | Create a sweep |
| GET | /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} | Get a sweep |
| DELETE | /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} | Delete a sweep |
| PATCH | /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} | Update a sweep |
| GET | /balanceAccounts/{id} | Get a balance account |
| PATCH | /balanceAccounts/{id} | Update a balance account |
| GET | /balanceAccounts/{id}/paymentInstruments | Get payment instruments linked to a balance account |
| GET | /balanceAccounts/{id}/transactionRules | Get all transaction rules for a balance account |
| POST | /balanceAccounts/{id}/transferLimits/approve | Approve pending transfer limits |
| GET | /balanceAccounts/{id}/transferLimits | Filter and view the transfer limits |
| POST | /balanceAccounts/{id}/transferLimits | Create a transfer limit |
| GET | /balanceAccounts/{id}/transferLimits/current | Get all current transfer limits |
| GET | /balanceAccounts/{id}/transferLimits/{transferLimitId} | Get the details of a transfer limit |
| DELETE | /balanceAccounts/{id}/transferLimits/{transferLimitId} | Delete a scheduled or pending transfer limit |

### balancePlatforms
| Method | Path | Description |
|--------|------|-------------|
| GET | /balancePlatforms/{id} | Get a balance platform |
| GET | /balancePlatforms/{id}/accountHolders | Get all account holders under a balance platform |
| GET | /balancePlatforms/{id}/transactionRules | Get all transaction rules for a balance platform |
| GET | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings | Get all balance webhook settings |
| POST | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings | Create a balance webhook setting |
| GET | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings/{settingId} | Get a balance webhook setting by id |
| DELETE | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings/{settingId} | Delete a balance webhook setting by id |
| PATCH | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings/{settingId} | Update a balance webhook setting by id |
| GET | /balancePlatforms/{id}/transferLimits | Filter and view the transfer limits |
| POST | /balancePlatforms/{id}/transferLimits | Create a transfer limit |
| GET | /balancePlatforms/{id}/transferLimits/{transferLimitId} | Get the details of a transfer limit |
| DELETE | /balancePlatforms/{id}/transferLimits/{transferLimitId} | Delete a scheduled or pending transfer limit |

### cardorders
| Method | Path | Description |
|--------|------|-------------|
| GET | /cardorders | Get a list of card orders |
| GET | /cardorders/{id}/items | Get card order items |

### grantAccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /grantAccounts/{id} | Get a grant account |

### grantOffers
| Method | Path | Description |
|--------|------|-------------|
| GET | /grantOffers | Get all available grant offers |
| GET | /grantOffers/{grantOfferId} | Get a grant offer |

### networkTokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /networkTokens/{networkTokenId} | Get a network token |
| PATCH | /networkTokens/{networkTokenId} | Update a network token |

### paymentInstrumentGroups
| Method | Path | Description |
|--------|------|-------------|
| POST | /paymentInstrumentGroups | Create a payment instrument group |
| GET | /paymentInstrumentGroups/{id} | Get a payment instrument group |
| GET | /paymentInstrumentGroups/{id}/transactionRules | Get all transaction rules for a payment instrument group |

### paymentInstruments
| Method | Path | Description |
|--------|------|-------------|
| POST | /paymentInstruments | Create a payment instrument |
| POST | /paymentInstruments/reveal | Reveal the data of a payment instrument |
| GET | /paymentInstruments/{id} | Get a payment instrument |
| PATCH | /paymentInstruments/{id} | Update a payment instrument |
| GET | /paymentInstruments/{id}/networkTokenActivationData | Get network token activation data |
| POST | /paymentInstruments/{id}/networkTokenActivationData | Create network token provisioning data |
| GET | /paymentInstruments/{id}/networkTokens | List network tokens |
| GET | /paymentInstruments/{id}/reveal | Get the PAN of a payment instrument |
| GET | /paymentInstruments/{id}/transactionRules | Get all transaction rules for a payment instrument |
| GET | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Get authorized users for a card. |
| POST | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Create authorized users for a card. |
| DELETE | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Delete the authorized users for a card. |
| PATCH | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Update the authorized users for a card. |

### pins
| Method | Path | Description |
|--------|------|-------------|
| POST | /pins/change | Change a card PIN |
| POST | /pins/reveal | Reveal a card PIN |

### publicKey
| Method | Path | Description |
|--------|------|-------------|
| GET | /publicKey | Get an RSA public key |

### registeredDevices
| Method | Path | Description |
|--------|------|-------------|
| GET | /registeredDevices | Get a list of registered SCA devices |
| POST | /registeredDevices | Initiate the registration of an SCA device |
| POST | /registeredDevices/{deviceId}/associations | Initiate an association between an SCA device and a resource |
| PATCH | /registeredDevices/{deviceId}/associations | Complete an association between an SCA device and a resource |
| DELETE | /registeredDevices/{id} | Delete a registration of an SCA device |
| PATCH | /registeredDevices/{id} | Complete the registration of an SCA device |

### transactionRules
| Method | Path | Description |
|--------|------|-------------|
| POST | /transactionRules | Create a transaction rule |
| GET | /transactionRules/{transactionRuleId} | Get a transaction rule |
| DELETE | /transactionRules/{transactionRuleId} | Delete a transaction rule |
| PATCH | /transactionRules/{transactionRuleId} | Update a transaction rule |

### transferRoutes
| Method | Path | Description |
|--------|------|-------------|
| POST | /transferRoutes/calculate | Calculate transfer routes |

### validateBankAccountIdentification
| Method | Path | Description |
|--------|------|-------------|
| POST | /validateBankAccountIdentification | Validate a bank account |

### scaAssociations
| Method | Path | Description |
|--------|------|-------------|
| GET | /scaAssociations | Get a list of devices associated with an entity |
| DELETE | /scaAssociations | Delete association to devices |
| PATCH | /scaAssociations | Approve a pending approval association |

### scaDevices
| Method | Path | Description |
|--------|------|-------------|
| POST | /scaDevices | Begin SCA device registration |
| PATCH | /scaDevices/{deviceId} | Finish registration process for a SCA device |
| POST | /scaDevices/{deviceId}/scaAssociations | Create a new SCA association for a device |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new account holder?" -> POST /accountHolders
- "What are the balance accounts for account holder X?" -> GET /accountHolders/{id}/balanceAccounts
- "How do I issue a new card or bank account payment instrument?" -> POST /paymentInstruments
- "How do I suspend or close a payment instrument?" -> PATCH /paymentInstruments/{id}
- "How do I set up an automatic sweep on a balance account?" -> POST /balanceAccounts/{balanceAccountId}/sweeps
- "What transaction rules apply to this account holder?" -> GET /accountHolders/{id}/transactionRules
- "How do I block transactions from specific countries?" -> POST /transactionRules
- "How do I reveal the full card number and CVC?" -> GET /paymentInstruments/{id}/reveal
- "How do I change a card's PIN?" -> POST /pins/change
- "What grant offers are available for an account holder?" -> GET /grantOffers
- "How do I validate a bank account number before creating a transfer?" -> POST /validateBankAccountIdentification
- "How do I download a US 1099 tax form for an account holder?" -> GET /accountHolders/{id}/taxForms
- "How do I register an SCA device for strong customer authentication?" -> POST /scaDevices
- "How do I calculate available transfer routes for a payout?" -> POST /transferRoutes/calculate
- "How do I set a daily transfer limit on a balance account?" -> POST /balanceAccounts/{id}/transferLimits

## Response Tips

- **List endpoints** (accountHolders, balanceAccounts, sweeps, cardorders, paymentInstruments): Paginated via `offset`/`limit` params; check `hasNext`/`hasPrevious` booleans to determine if more pages exist -- there is no total count field.
- **Registered devices**: Uses a different pagination model with `pageNumber`/`pageSize` params and returns `itemsTotal`, `pagesTotal`, and `_links` with `first`/`last`/`next`/`previous` hrefs.
- **Error responses** (400, 401, 403, 422, 500): All endpoints share the same error code set; 422 typically means validation failure on input fields -- inspect the response body for field-level details.
- **Async operations**: PATCH /networkTokens/{id} returns 202 (accepted, not completed) -- poll or use webhooks to confirm the status change took effect.
- **Empty success**: DELETE endpoints and some POST endpoints (authorisedCardUsers, transferLimits/approve) return 204 with no body.
- **Monetary values**: Amounts use `{currency: str, value: int64}` where `value` is in minor units (cents) -- divide by 100 for display in most currencies.
- **Card reveal**: The `/paymentInstruments/reveal` POST endpoint returns encrypted data requiring the public key from GET /publicKey, while GET `/paymentInstruments/{id}/reveal` returns plaintext PAN/CVC/expiry.

## Anomaly Flags

- **Account holder status is "suspended" or "closed"**: Surface immediately -- downstream operations (creating balance accounts, issuing cards) will fail.
- **verificationDeadlines approaching**: If `expiresAt` on any verification deadline is within 7 days, warn the user -- capabilities may be disabled after expiry.
- **Sweep status is "inactive" with a reason**: Check the `reason` field for values like `notEnoughBalance`, `counterpartyAccountBlocked`, or `error` -- these indicate a sweep that stopped working silently.
- **Payment instrument statusReason contains fraud indicators**: Values like `stolen`, `suspectedFraud`, or `lost` should be flagged for immediate review.
- **Payment instrument has `replacedById` set**: The instrument has been replaced -- any references to the old ID should be updated.
- **Network token status is "suspended" or "closed"**: Digital wallet transactions will fail -- surface to the user if they are debugging payment failures.
- **Transfer limit with `limitStatus` not "active"**: A pending or rejected limit means the intended spending controls are not in effect.
- **Grant offer `expiresAt` approaching**: If a grant offer expires soon, alert the user so they can act before losing the financing option.
- **422 errors on transaction rule creation**: Usually means conflicting rule restrictions -- surface the specific restriction that failed validation.
- **SCA association status "pendingApproval"**: The device is registered but not yet authorized -- transactions requiring SCA will fail until approved.

## Playbook

### 1. Onboard a new seller/merchant

1. Create the account holder: POST /accountHolders with `legalEntityId` (must exist in Legal Entity API first)
2. Note the returned `id` and check `verificationDeadlines` for any upcoming KYC requirements
3. Create a balance account: POST /balanceAccounts with the `accountHolderId` from step 1
4. Issue a payment instrument (card or bank account): POST /paymentInstruments with the `balanceAccountId` and `type`
5. Set up a sweep for automatic payouts: POST /balanceAccounts/{balanceAccountId}/sweeps with counterparty and schedule
6. Optionally create transaction rules: POST /transactionRules to set spending limits or country restrictions

### 2. Issue and configure a card

1. Create a payment instrument group (optional, for batch card orders): POST /paymentInstrumentGroups with `balancePlatform` and `txVariant`
2. Create the card: POST /paymentInstruments with `type: "card"`, the `balanceAccountId`, `issuingCountryCode`, and `card` details (brand, brandVariant, cardholderName, formFactor)
3. Set transaction rules for the card: POST /transactionRules with `entityKey: {entityType: "paymentInstrument", entityReference: cardId}`
4. Register an SCA device if needed: POST /scaDevices, then POST /scaDevices/{deviceId}/scaAssociations to link it
5. Monitor card orders: GET /cardorders to check manufacturing and delivery status
6. Reveal card details when needed: GET /paymentInstruments/{id}/reveal for plaintext PAN/CVC, or use POST /paymentInstruments/reveal with an encrypted key for secure client-side reveal

### 3. Set up automated balance sweeps

1. Get the balance account details: GET /balanceAccounts/{id} to confirm it exists and check current balances
2. Create the sweep: POST /balanceAccounts/{balanceAccountId}/sweeps with `currency`, `counterparty` (target account or transfer instrument), and `schedule` (cron expression or type like "daily")
3. Set the trigger: Use `triggerAmount` to sweep when balance exceeds a threshold, or `targetAmount` to sweep down to a target, or `sweepAmount` for a fixed amount
4. Verify the sweep is active: GET /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} and confirm `status: "active"`
5. To pause: PATCH /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} with `status: "inactive"`

### 4. Create and manage transaction rules

1. Identify the entity to protect: Decide whether the rule applies to an account holder, balance account, payment instrument, or payment instrument group
2. Create the rule: POST /transactionRules with `entityKey`, `type` (allowList, blockList, maxUsage, or velocity), `interval`, and `ruleRestrictions`
3. For spending limits: Use `type: "velocity"` with `totalAmount` restriction and an interval (e.g., daily, weekly)
4. For country blocking: Use `type: "blockList"` with `countries` restriction listing blocked country codes
5. Verify rules in effect: GET /accountHolders/{id}/transactionRules or GET /balanceAccounts/{id}/transactionRules to see all active rules
6. To disable without deleting: PATCH /transactionRules/{id} with `status: "inactive"`

### 5. Manage transfer limits with SCA

1. Check existing limits: GET /balanceAccounts/{id}/transferLimits to see all configured limits
2. Check currently active limits: GET /balanceAccounts/{id}/transferLimits/current for only the in-effect limits
3. Create a new limit: POST /balanceAccounts/{id}/transferLimits with `amount`, `scope` (perDay or perTransaction), and `transferType` (instant or all)
4. If SCA is required: Include `scaInformation` and handle the SCA challenge flow; check `scaInformation.status` in the response
5. Approve pending limits: POST /balanceAccounts/{id}/transferLimits/approve with the `transferLimitIds` array
6. Remove a limit: DELETE /balanceAccounts/{id}/transferLimits/{transferLimitId}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
