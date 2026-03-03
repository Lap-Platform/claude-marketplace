---
name: adyen-checkout-api
description: "Adyen Checkout API skill. Use when working with Adyen Checkout for applePay, cancels, cardDetails. Covers 28 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen Checkout API
API version: 71

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://checkout-test.adyen.com/v71

## Setup
1. Set Authorization header with your Bearer token
2. GET /storedPaymentMethods -- verify access
3. POST /applePay/sessions -- create first sessions

## Endpoints

28 endpoints across 15 groups. See references/api-spec.lap for full details.

### applePay
| Method | Path | Description |
|--------|------|-------------|
| POST | /applePay/sessions | Get an Apple Pay session |

### cancels
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancels | Cancel an authorised payment |

### cardDetails
| Method | Path | Description |
|--------|------|-------------|
| POST | /cardDetails | Get the brands and other details of a card |

### donationCampaigns
| Method | Path | Description |
|--------|------|-------------|
| POST | /donationCampaigns | Get a list of donation campaigns. |

### donations
| Method | Path | Description |
|--------|------|-------------|
| POST | /donations | Make a donation |

### forward
| Method | Path | Description |
|--------|------|-------------|
| POST | /forward | Forward stored payment details |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders | Create an order |
| POST | /orders/cancel | Cancel an order |

### originKeys
| Method | Path | Description |
|--------|------|-------------|
| POST | /originKeys | Create originKey values for domains |

### paymentLinks
| Method | Path | Description |
|--------|------|-------------|
| POST | /paymentLinks | Create a payment link |
| GET | /paymentLinks/{linkId} | Get a payment link |
| PATCH | /paymentLinks/{linkId} | Update the status of a payment link |

### paymentMethods
| Method | Path | Description |
|--------|------|-------------|
| POST | /paymentMethods | Get a list of available payment methods |
| POST | /paymentMethods/balance | Get the balance of a gift card |

### payments
| Method | Path | Description |
|--------|------|-------------|
| POST | /payments | Start a transaction |
| POST | /payments/details | Submit details for a payment |
| POST | /payments/{paymentPspReference}/amountUpdates | Update an authorised amount |
| POST | /payments/{paymentPspReference}/cancels | Cancel an authorised payment |
| POST | /payments/{paymentPspReference}/captures | Capture an authorised payment |
| POST | /payments/{paymentPspReference}/refunds | Refund a captured payment |
| POST | /payments/{paymentPspReference}/reversals | Refund or cancel a payment |

### paypal
| Method | Path | Description |
|--------|------|-------------|
| POST | /paypal/updateOrder | Updates the order for PayPal Express Checkout |

### sessions
| Method | Path | Description |
|--------|------|-------------|
| POST | /sessions | Create a payment session |
| GET | /sessions/{sessionId} | Get the result of a payment session |

### storedPaymentMethods
| Method | Path | Description |
|--------|------|-------------|
| GET | /storedPaymentMethods | Get tokens for stored payment details |
| POST | /storedPaymentMethods | Create a token to store payment details |
| DELETE | /storedPaymentMethods/{storedPaymentMethodId} | Delete a token for stored payment details |

### validateShopperId
| Method | Path | Description |
|--------|------|-------------|
| POST | /validateShopperId | Validates shopper Id |

## Enhanced Skill Content
## Question Mapping

- "How do I process a card payment?" -> POST /payments
- "What payment methods are available for my merchant account?" -> POST /paymentMethods
- "How do I refund a payment?" -> POST /payments/{paymentPspReference}/refunds
- "How do I cancel an authorized payment?" -> POST /payments/{paymentPspReference}/cancels
- "How do I create a payment link to send to a customer?" -> POST /paymentLinks
- "How do I check the status of a payment link?" -> GET /paymentLinks/{linkId}
- "How do I expire or deactivate a payment link?" -> PATCH /paymentLinks/{linkId}
- "How do I capture a pre-authorized payment?" -> POST /payments/{paymentPspReference}/captures
- "How do I update the amount on an authorized payment (e.g., hotel extended stay)?" -> POST /payments/{paymentPspReference}/amountUpdates
- "How do I reverse a payment that may or may not be captured yet?" -> POST /payments/{paymentPspReference}/reversals
- "How do I check a gift card or prepaid card balance?" -> POST /paymentMethods/balance
- "How do I save a shopper's card for future payments?" -> POST /storedPaymentMethods
- "How do I list a shopper's saved payment methods?" -> GET /storedPaymentMethods
- "How do I delete a stored payment method?" -> DELETE /storedPaymentMethods/{storedPaymentMethodId}
- "How do I create a checkout session for Drop-in/Components?" -> POST /sessions

## Response Tips

- **Payments & donations:** Check `resultCode` first -- `Authorised`, `Refused`, `Pending`, `RedirectShopper`, `ChallengeShopper`, and `IdentifyShopper` all require different handling. If `action` is present, the shopper must complete an additional step (redirect, 3DS challenge, etc.) before the payment is final.
- **Payment modifications (captures, refunds, cancels, reversals, amountUpdates):** Return `status` field (`received`) confirming the request was accepted -- these are asynchronous. Final outcomes arrive via webhooks, not in the API response.
- **Payment links:** The `status` field tracks lifecycle (`active`, `completed`, `expired`, `paid`). The `url` field is the shareable link. `id` is needed for GET/PATCH operations.
- **Sessions:** Response includes `id` and `sessionData` -- both are required to initialize Drop-in/Components on the frontend. Use GET /sessions/{sessionId} with the `sessionResult` from the frontend to verify final status.
- **Stored payment methods:** POST returns tokenized card details (`id`, `lastFour`, `brand`). The `id` becomes the `storedPaymentMethodId` used in future payment requests.
- **Error responses (400, 401, 403, 422, 500):** All errors follow the same structure. 422 typically means validation failure with details in the response body. 401/403 indicate API key or permission issues.
- **Balance check:** Returns `balance` (available funds), `transactionLimit` (max single-transaction amount), and `resultCode`. A `NotEnough` result means the balance is insufficient.

## Anomaly Flags

- **3DS challenge required:** Surface immediately when `resultCode` is `RedirectShopper`, `ChallengeShopper`, or `IdentifyShopper` -- the payment is not complete and requires frontend action via `/payments/details`.
- **Payment refused:** Flag `resultCode: Refused` with the `refusalReason` and `refusalReasonCode` -- these indicate why the issuer declined (insufficient funds, stolen card, etc.).
- **Idempotency collisions:** All POST endpoints accept `Idempotency-Key`. Warn if retrying a request without the same key, as this can create duplicate transactions.
- **Amount mismatch on partial operations:** When capturing or refunding, flag if the `amount.value` differs from the original authorization -- this indicates a partial capture/refund which not all acquirers support.
- **Expiring payment links:** Flag when creating links without `expiresAt` or with far-future expiry -- abandoned links remain active indefinitely.
- **Missing shopperReference for tokenization:** If `storePaymentMethod: true` is set on `/payments` but `shopperReference` is missing, the token cannot be associated with a shopper.
- **Deprecated fields:** `threeDSAuthenticationOnly`, `enableOneClick`, `enableRecurring`, `enablePayOut`, `recurringExpiry`, `recurringFrequency`, `dccQuote`, and `originKeys` endpoint are legacy -- recommend using `authenticationData`, `storePaymentMethodMode`, and `/sessions` instead.
- **HTTP 422 on modifications:** This usually means the original payment is in an incompatible state (e.g., trying to capture an already-captured payment, or refunding beyond the captured amount).

## Playbook

### 1. Accept a one-time card payment (Drop-in/Components flow)

1. Call `POST /sessions` with `amount`, `merchantAccount`, `reference`, and `returnUrl` to create a checkout session.
2. Pass the `id` and `sessionData` from the response to your frontend Drop-in or Components integration.
3. The shopper completes payment on the frontend. On completion, the frontend returns a `sessionResult`.
4. Call `GET /sessions/{sessionId}?sessionResult=...` to verify the payment outcome server-side.
5. Check the `status` field: `completed` means the payment succeeded.

### 2. Capture, then partially refund a payment

1. Process an authorization via `POST /payments` with your payment details (ensure `captureDelayHours` is set for manual capture, or omit for auto-capture).
2. When ready to capture, call `POST /payments/{paymentPspReference}/captures` with the desired `amount` (can be less than or equal to the authorized amount).
3. Note the `pspReference` in the capture response -- the capture is asynchronous (`status: received`).
4. To issue a partial refund later, call `POST /payments/{paymentPspReference}/refunds` using the original payment's `paymentPspReference`, with an `amount` less than the captured total.
5. Optionally set `merchantRefundReason` to categorize the refund (FRAUD, CUSTOMER REQUEST, RETURN, DUPLICATE, OTHER).

### 3. Save a card and charge it later (tokenization)

1. Call `POST /payments` with `shopperReference` (your unique shopper ID), `storePaymentMethod: true`, and `recurringProcessingModel: CardOnFile`.
2. On success, the card is tokenized. Retrieve saved cards via `GET /storedPaymentMethods?shopperReference=...&merchantAccount=...`.
3. For subsequent charges, call `POST /payments` with `paymentMethod: { storedPaymentMethodId: "<id>" }`, `shopperReference`, and `shopperInteraction: ContAuth`.
4. To remove a saved card, call `DELETE /storedPaymentMethods/{storedPaymentMethodId}?shopperReference=...&merchantAccount=...`.

### 4. Create and manage a payment link

1. Call `POST /paymentLinks` with `amount`, `merchantAccount`, and `reference`. Optionally set `expiresAt`, `allowedPaymentMethods`, and `shopperEmail`.
2. Share the `url` from the response with the customer (email, SMS, chat).
3. Poll the link status via `GET /paymentLinks/{linkId}` -- check the `status` field for `active`, `paid`, `completed`, or `expired`.
4. To cancel an active link, call `PATCH /paymentLinks/{linkId}` with `status: expired`.

### 5. Handle 3DS authentication on a payment

1. Call `POST /payments` with full payment details including `browserInfo`, `origin`, and `returnUrl`.
2. If `resultCode` is `RedirectShopper`: redirect the shopper to the URL in `action`. After redirect-back, collect `redirectResult` from the query string.
3. If `resultCode` is `ChallengeShopper` or `IdentifyShopper`: render the 3DS challenge using the `action` data in your frontend component.
4. Once the shopper completes the challenge, call `POST /payments/details` with the collected `details` (e.g., `threeDSResult`, `redirectResult`, or `threeds2.challengeResult`) and the `paymentData` from the original response.
5. Check `resultCode` in the `/payments/details` response -- `Authorised` means success. If another action is returned, repeat from step 2.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
