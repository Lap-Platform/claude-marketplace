---
name: adyen-stored-value-api
description: "Adyen Stored Value API skill. Use when working with Adyen Stored Value for changeStatus, checkBalance, issue. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen Stored Value API
API version: 46

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://pal-test.adyen.com/pal/servlet/StoredValue/v46

## Setup
1. Set Authorization header with your Bearer token
3. POST /changeStatus -- create first changeStatus

## Endpoints

6 endpoints across 6 groups. See references/api-spec.lap for full details.

### changeStatus
| Method | Path | Description |
|--------|------|-------------|
| POST | /changeStatus | Changes the status of the payment method. |

### checkBalance
| Method | Path | Description |
|--------|------|-------------|
| POST | /checkBalance | Checks the balance. |

### issue
| Method | Path | Description |
|--------|------|-------------|
| POST | /issue | Issues a new card. |

### load
| Method | Path | Description |
|--------|------|-------------|
| POST | /load | Loads the payment method. |

### mergeBalance
| Method | Path | Description |
|--------|------|-------------|
| POST | /mergeBalance | Merge the balance of two cards. |

### voidTransaction
| Method | Path | Description |
|--------|------|-------------|
| POST | /voidTransaction | Voids a transaction. |

## Enhanced Skill Content
## Question Mapping

- "How do I check the balance on a gift card?" -> POST /checkBalance
- "How do I activate or deactivate a stored value card?" -> POST /changeStatus
- "How do I issue a new gift card?" -> POST /issue
- "How do I load funds onto a prepaid card?" -> POST /load
- "How do I process a merchandise return to a gift card?" -> POST /load (with loadType: merchandiseReturn)
- "How do I merge two gift card balances into one?" -> POST /mergeBalance
- "How do I cancel a stored value transaction?" -> POST /voidTransaction
- "How do I set up a recurring stored value payment?" -> POST /load (with shopperReference + recurringDetailReference)
- "How do I check balance before processing a payment?" -> POST /checkBalance, then conditional logic
- "How do I transfer balance from one card to another?" -> POST /mergeBalance (sourcePaymentMethod -> paymentMethod)
- "How do I deactivate a lost or stolen gift card?" -> POST /changeStatus (status: inactive)
- "How do I reactivate a previously disabled card?" -> POST /changeStatus (status: active)
- "How do I issue a gift card for a specific amount?" -> POST /issue (with amount)
- "How do I void a load that was done in error?" -> POST /voidTransaction (with originalReference from load response)

## Response Tips

- **All endpoints**: Check `resultCode` first -- values like "Success", "Refused", or "Error" determine outcome. A 200 status does NOT guarantee success; the operation may be refused at the payment method level.
- **Balance responses**: `currentBalance` is a map with `currency` (ISO 4217) and `value` in minor units (e.g., 1000 = 10.00 EUR). Always divide by 100 for display currencies with two decimal places.
- **Refusals**: When `resultCode` indicates refusal, check both `refusalReason` (Adyen's reason) and `thirdPartyRefusalReason` (issuer/processor reason) for diagnostics.
- **Transaction references**: Save `pspReference` from every response -- it is required for void operations and useful for reconciliation.
- **Errors**: 400 = malformed request (check required fields), 401/403 = API key or permission issue, 500 = retry with idempotency via `reference`.

## Anomaly Flags

- **Refused resultCode on 200**: Surface immediately -- the HTTP call succeeded but the operation was denied. Display both `refusalReason` and `thirdPartyRefusalReason`.
- **Zero or negative currentBalance**: Flag after a load or issue operation -- may indicate the operation did not apply as expected.
- **Missing authCode**: Some successful responses omit `authCode`. If present, store it; if absent on a successful result, note it as processor-dependent.
- **Currency mismatch**: If the `currentBalance.currency` in the response differs from the `amount.currency` sent in the request, flag for review.
- **500 errors without pspReference**: Indicates the request may not have reached the payment platform -- advise retry with the same `reference` for idempotency.
- **Repeated refusals on changeStatus**: May indicate the card is permanently blocked at issuer level, not just inactive in Adyen.

## Playbook

### Issue a Gift Card and Load Initial Balance

1. Call POST /issue with `paymentMethod` (card details) and `merchantAccount`
2. Confirm `resultCode` is successful and note the `pspReference`
3. Call POST /load with the same `paymentMethod`, desired `amount`, and `merchantAccount`
4. Verify `currentBalance` in the response matches the loaded amount
5. Store the `pspReference` from both calls for reconciliation

### Process a Merchandise Return to Gift Card

1. Call POST /checkBalance with the gift card `paymentMethod` to confirm the card is active
2. Call POST /load with `loadType: "merchandiseReturn"`, the return `amount`, and the card's `paymentMethod`
3. Verify `resultCode` is successful and `currentBalance` reflects the added return amount
4. Store the `pspReference` for the return transaction audit trail

### Deactivate a Lost Card and Transfer Balance

1. Call POST /checkBalance on the lost card's `paymentMethod` to capture remaining balance
2. Call POST /changeStatus with `status: "inactive"` to disable the lost card
3. Confirm `resultCode` is successful on deactivation
4. Call POST /issue to create a replacement card
5. Call POST /mergeBalance with the lost card as `sourcePaymentMethod` and the new card as `paymentMethod` (if balance transfer is supported while inactive; otherwise load the captured amount onto the new card)

### Void an Erroneous Transaction

1. Locate the `pspReference` from the original transaction response (load, issue, etc.)
2. Call POST /voidTransaction with `originalReference` set to that `pspReference`
3. Check `resultCode` for success confirmation
4. Verify `currentBalance` reflects the reversal

### Check Balance Before a POS Transaction

1. Call POST /checkBalance with the card's `paymentMethod` and `shopperInteraction: "POS"`
2. Read `currentBalance.value` and `currentBalance.currency` from the response
3. If balance is sufficient, proceed with the payment flow
4. If balance is insufficient, calculate the remaining amount for a split-tender scenario


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
