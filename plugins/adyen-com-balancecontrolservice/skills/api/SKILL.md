---
name: adyen-balance-control-api
description: "Adyen Balance Control API skill. Use when working with Adyen Balance Control for balanceTransfer. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Adyen Balance Control API
API version: 1

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://pal-test.adyen.com/pal/servlet/BalanceControl/v1

## Setup
1. Set Authorization header with your Bearer token
3. POST /balanceTransfer -- create first balanceTransfer

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### balanceTransfer
| Method | Path | Description |
|--------|------|-------------|
| POST | /balanceTransfer | Start a balance transfer |

## Enhanced Skill Content
## Question Mapping

- "How do I transfer balance between merchant accounts?" -> POST /balanceTransfer
- "How do I move funds from one merchant to another?" -> POST /balanceTransfer
- "How do I process a tax transfer between merchants?" -> POST /balanceTransfer (type: tax)
- "How do I issue a credit adjustment to a merchant?" -> POST /balanceTransfer (type: credit)
- "How do I record a fee transfer between accounts?" -> POST /balanceTransfer (type: fee)
- "How do I process a terminal sale balance transfer?" -> POST /balanceTransfer (type: terminalSale)
- "How do I make a debit adjustment between merchants?" -> POST /balanceTransfer (type: debit)
- "How do I transfer balance with a reference for tracking?" -> POST /balanceTransfer (with reference field)
- "How do I transfer funds in a specific currency?" -> POST /balanceTransfer (set amount.currency)
- "How do I check if a balance transfer succeeded?" -> POST /balanceTransfer (inspect status in response)
- "How do I transfer balance and add a description?" -> POST /balanceTransfer (with description field)
- "How do I reconcile balance transfers using PSP references?" -> POST /balanceTransfer (use pspReference from response)

## Response Tips

- **balanceTransfer**: Response mirrors request fields plus `pspReference` (unique ID for reconciliation), `createdAt` (ISO 8601 timestamp), and `status`. Always store `pspReference` -- it is the canonical identifier for the transfer. The `amount` in the response confirms the actual transferred amount, which should match the request.

## Anomaly Flags

- **Non-success status**: Surface immediately if `status` in the response is anything other than the expected success value -- this indicates the transfer may not have completed.
- **Amount mismatch**: Flag if the response `amount.value` or `amount.currency` differs from the request, as this suggests partial transfer or currency conversion.
- **Missing pspReference**: If the response lacks a `pspReference`, the transfer may not have been recorded -- alert the user to retry or investigate.
- **Authentication errors (401/403)**: Indicate expired or invalid API key -- prompt user to verify `X-API-Key` or basic auth credentials.
- **Duplicate reference**: If using the same `reference` value across calls, surface a warning that this may cause idempotency conflicts or reconciliation issues.
- **High-value transfers**: Consider alerting when `amount.value` exceeds a user-defined threshold, as these may require additional approval.

## Playbook

### 1. Transfer Balance Between Two Merchants

1. Identify the source (`fromMerchant`) and destination (`toMerchant`) merchant account codes.
2. Determine the amount: set `amount.currency` (e.g., "EUR") and `amount.value` in minor units (e.g., 1000 = 10.00 EUR).
3. Choose the transfer `type` (tax, fee, terminalSale, credit, debit, or adjustment).
4. Call `POST /balanceTransfer` with the required fields.
5. Store the `pspReference` from the response for reconciliation.
6. Verify `status` confirms success.

### 2. Tracked Transfer with Reference and Description

1. Generate a unique `reference` string for internal tracking (e.g., order ID or invoice number).
2. Write a human-readable `description` for audit purposes.
3. Call `POST /balanceTransfer` with `reference` and `description` alongside required fields.
4. Log both your `reference` and the returned `pspReference` for cross-referencing.
5. Use `createdAt` from the response to timestamp your records.

### 3. Fee or Tax Settlement Between Merchants

1. Determine the fee or tax amount owed between merchant accounts.
2. Set `type` to `fee` or `tax` as appropriate.
3. Set `description` to document the fee/tax context (e.g., "Q1 2026 platform fee").
4. Call `POST /balanceTransfer`.
5. Confirm the response `status` and archive `pspReference` for financial reporting.

### 4. Reconciling Balance Transfers

1. For each transfer, ensure you captured the `pspReference` from the response.
2. Match `pspReference` values against your internal records using the `reference` field you provided.
3. Verify `createdAt` timestamps align with expected transfer dates.
4. Confirm `amount` values match expected totals per merchant pair.
5. Flag any transfers where `status` indicates an unexpected state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
