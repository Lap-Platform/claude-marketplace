---
name: adyen-payment-api
description: "Adyen Payment API skill. Use when working with Adyen Payment for adjustAuthorisation, authorise, authorise3d. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen Payment API
API version: 68

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://pal-test.adyen.com/pal/servlet/Payment/v68

## Setup
1. Set Authorization header with your Bearer token
3. POST /adjustAuthorisation -- create first adjustAuthorisation

## Endpoints

13 endpoints across 13 groups. See references/api-spec.lap for full details.

### adjustAuthorisation
| Method | Path | Description |
|--------|------|-------------|
| POST | /adjustAuthorisation | Change the authorised amount |

### authorise
| Method | Path | Description |
|--------|------|-------------|
| POST | /authorise | Create an authorisation |

### authorise3d
| Method | Path | Description |
|--------|------|-------------|
| POST | /authorise3d | Complete a 3DS authorisation |

### authorise3ds2
| Method | Path | Description |
|--------|------|-------------|
| POST | /authorise3ds2 | Complete a 3DS2 authorisation |

### cancel
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancel | Cancel an authorisation |

### cancelOrRefund
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancelOrRefund | Cancel or refund a payment |

### capture
| Method | Path | Description |
|--------|------|-------------|
| POST | /capture | Capture an authorisation |

### donate
| Method | Path | Description |
|--------|------|-------------|
| POST | /donate | Create a donation |

### getAuthenticationResult
| Method | Path | Description |
|--------|------|-------------|
| POST | /getAuthenticationResult | Get the 3DS authentication result |

### refund
| Method | Path | Description |
|--------|------|-------------|
| POST | /refund | Refund a captured payment |

### retrieve3ds2Result
| Method | Path | Description |
|--------|------|-------------|
| POST | /retrieve3ds2Result | Get the 3DS2 authentication result |

### technicalCancel
| Method | Path | Description |
|--------|------|-------------|
| POST | /technicalCancel | Cancel an authorisation using your reference |

### voidPendingRefund
| Method | Path | Description |
|--------|------|-------------|
| POST | /voidPendingRefund | Cancel an in-person refund |

## Enhanced Skill Content
## Question Mapping

- "How do I authorize a credit card payment?" -> POST /authorise
- "How do I complete a 3D Secure authentication?" -> POST /authorise3d
- "How do I process a 3DS2 payment?" -> POST /authorise3ds2
- "How do I capture a previously authorized payment?" -> POST /capture
- "How do I refund a transaction?" -> POST /refund
- "How do I cancel a payment that hasn't been captured yet?" -> POST /cancel
- "I'm not sure if the payment was captured -- how do I reverse it?" -> POST /cancelOrRefund
- "How do I adjust the authorized amount on an existing authorization?" -> POST /adjustAuthorisation
- "How do I make a donation from a payment?" -> POST /donate
- "How do I check the 3D Secure authentication result?" -> POST /getAuthenticationResult
- "How do I retrieve the 3DS2 result for a transaction?" -> POST /retrieve3ds2Result
- "How do I cancel a payment using the merchant reference instead of pspReference?" -> POST /technicalCancel
- "How do I void a refund that's still pending?" -> POST /voidPendingRefund
- "How do I split a payment across multiple accounts?" -> POST /authorise (with `splits` array)
- "How do I set up a recurring/subscription payment?" -> POST /authorise (with `recurring` and `shopperReference`)

## Response Tips

- **Authorisation responses**: Check `resultCode` first -- `Authorised`, `Refused`, `RedirectShopper` (3DS redirect needed), `IdentifyShopper`/`ChallengeShopper` (3DS2 flows). `refusalReason` explains rejections. Save `pspReference` for all subsequent operations.
- **3DS redirect responses**: When `resultCode` is `RedirectShopper`, use `issuerUrl`, `md`, and `paRequest` to redirect the shopper, then complete with `/authorise3d`.
- **Modification responses** (capture, cancel, refund, adjust): The `response` field contains `[capture-received]`, `[cancel-received]`, `[refund-received]`, etc. These are async -- the bracket notation means the request was accepted, not that it's finalized. Listen for webhooks for the final result.
- **Fraud results**: `fraudResult.accountScore` is a 0-100 risk score; `fraudResult.results` contains individual rule outcomes. Only present when fraud checks are configured.
- **Error responses**: All endpoints share the same error codes -- 400 (validation), 401 (auth), 403 (permissions), 422 (unprocessable entity, often business rule violations), 500 (server error). Error body contains `errorCode`, `message`, and `errorType`.

## Anomaly Flags

- **`resultCode: Refused`** with no `refusalReason` -- indicates a silent decline; escalate to Adyen support with the `pspReference`.
- **`resultCode: Error`** -- server-side processing failure; the payment state is unknown. Do NOT retry blindly; use the original `reference` to check status first.
- **HTTP 422** -- typically means the `originalReference` points to a payment in an incompatible state (e.g., capturing an already-captured payment). Surface the specific `errorCode` to the user.
- **3DS `challengeCancel` present** -- the shopper abandoned the 3DS challenge. Flag this pattern if it recurs for the same shopper.
- **`additionalData` containing `fraudManualReview: true`** -- payment is held for manual review; alert the user that it won't settle automatically.
- **Modification returning HTTP 200 but `response` not in bracket notation** -- unexpected format; surface the raw response for inspection.
- **`dccAmount` present in authorisation response** -- dynamic currency conversion was applied; surface the converted amount and exchange rate to avoid billing surprises.

## Playbook

### 1. Standard Card Payment with Capture

1. Call `POST /authorise` with `amount`, `reference`, `card` (or encrypted payment data), and `merchantAccount`.
2. Check `resultCode` -- if `Authorised`, save the `pspReference`.
3. When ready to settle (e.g., after shipping), call `POST /capture` with `originalReference` set to the `pspReference` and `modificationAmount` matching or less than the authorized amount.
4. Confirm the response contains `[capture-received]`.

### 2. 3D Secure Payment (3DS1)

1. Call `POST /authorise` with `amount`, `reference`, `card`, and `browserInfo`.
2. If `resultCode` is `RedirectShopper`, redirect the shopper to `issuerUrl` with `paRequest` and `md` as POST parameters.
3. After the shopper completes authentication, their browser posts back `MD` and `PaRes`.
4. Call `POST /authorise3d` with `md` and `paResponse` to finalize.
5. Check `resultCode` for `Authorised` or `Refused`.

### 3. Full Refund of a Captured Payment

1. Retrieve the `pspReference` from the original authorisation.
2. Call `POST /refund` with `originalReference` set to that `pspReference` and `modificationAmount` matching the original captured amount.
3. Confirm the response contains `[refund-received]`.
4. If you need to cancel the refund before it settles, call `POST /voidPendingRefund` with the refund's `pspReference` as `originalReference`.

### 4. Cancel-or-Refund (Unknown Capture State)

1. When you don't know whether a payment has been captured, call `POST /cancelOrRefund` with `originalReference` set to the payment's `pspReference`.
2. Adyen determines the correct action: cancel if not yet captured, refund if already captured.
3. Confirm the response contains `[cancelOrRefund-received]`.
4. Monitor webhooks for the final `CANCELLATION` or `REFUND` notification.

### 5. Recurring/Subscription Setup and Charge

1. For the initial payment, call `POST /authorise` with `shopperReference` (your unique shopper ID), `shopperInteraction: "Ecommerce"`, and `recurring: { contract: "RECURRING" }`.
2. Save the `pspReference` and note the `recurringDetailReference` from `additionalData` if present.
3. For subsequent charges, call `POST /authorise` with `shopperReference`, `shopperInteraction: "ContAuth"`, `selectedRecurringDetailReference: "LATEST"` (or a specific reference), and `recurringProcessingModel: "Subscription"`.
4. No card details needed for subsequent charges -- Adyen uses the stored token.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
