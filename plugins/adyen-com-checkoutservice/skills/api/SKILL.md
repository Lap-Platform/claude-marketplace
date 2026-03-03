---
name: adyen-checkout-api
description: "Adyen Checkout API skill. Use when working with Adyen Checkout for applePay, cancels, cardDetails. Covers 28 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen Checkout API
API version: 70

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://checkout-test.adyen.com/v70

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

- "How do I accept a credit card payment?" -> POST /payments
- "What payment methods are available for my merchant account?" -> POST /paymentMethods
- "How do I refund a payment?" -> POST /payments/{paymentPspReference}/refunds
- "How do I cancel a payment that hasn't been captured yet?" -> POST /payments/{paymentPspReference}/cancels
- "How do I capture an authorized payment?" -> POST /payments/{paymentPspReference}/captures
- "How do I create a shareable payment link for a customer?" -> POST /paymentLinks
- "How do I check the status of a payment link?" -> GET /paymentLinks/{linkId}
- "How do I expire or deactivate a payment link?" -> PATCH /paymentLinks/{linkId}
- "How do I save a shopper's card for future payments?" -> POST /storedPaymentMethods
- "How do I list a shopper's saved payment methods?" -> GET /storedPaymentMethods
- "How do I delete a stored payment method?" -> DELETE /storedPaymentMethods/{storedPaymentMethodId}
- "How do I create a checkout session for Drop-in/Components?" -> POST /sessions
- "How do I check the outcome of a session after the shopper returns?" -> GET /sessions/{sessionId}
- "How do I handle 3D Secure redirects after a payment?" -> POST /payments/details
- "How do I reverse a payment when I don't know if it was captured?" -> POST /payments/{paymentPspReference}/reversals
- "How do I check a gift card or voucher balance?" -> POST /paymentMethods/balance

## Response Tips

- **Payments & donations**: Check `resultCode` first -- values include `Authorised`, `Refused`, `Pending`, `RedirectShopper`, `ChallengeShopper`. If `action` is present, the shopper must complete an additional step (3DS, redirect). Always store `pspReference` for later operations.
- **Payment modifications** (captures, refunds, cancels, reversals, amountUpdates): Return `status` field (e.g., `received`) -- this confirms the request was accepted, not that the modification is final. Use webhooks for the definitive result.
- **Payment links**: Return the full link object including `url` (the shareable link) and `status` (`active`, `completed`, `expired`). `201` on create, `200` on get/update.
- **Sessions**: `POST` returns `id` and `sessionData` (both needed to initialize Drop-in/Components). `GET` returns `status` and a `payments` array with individual payment attempt outcomes.
- **Stored payment methods**: `GET` returns a `storedPaymentMethods` array. `DELETE` returns `204` with no body. `POST` returns card details including `id` to use in future payments.
- **Errors**: All write endpoints share the same error codes -- `400` (validation), `401` (auth), `403` (permissions), `422` (unprocessable), `500` (server). Error bodies contain `errorCode`, `message`, and `errorType`.

## Anomaly Flags

- **`resultCode: Refused`** with a `refusalReasonCode` -- surface the reason code and suggest the merchant check their Adyen dashboard for details. Common codes: `2` (transaction refused), `5` (do not honor), `14` (invalid card number).
- **`action` present in payment response** -- the payment is NOT complete. The agent must guide the user through handling the redirect, 3DS challenge, or additional input. Do not treat this as a successful payment.
- **`422 Unprocessable Entity`** -- usually means a semantic error (e.g., capturing more than authorized, refunding an uncaptured payment). Surface the error message verbatim.
- **`401 Unauthorized`** -- API key is invalid or missing required roles. Prompt the user to verify their `X-API-Key` and its permissions in the Adyen Customer Area.
- **`remainingAmount` in order responses** -- if this differs from the original `amount`, partial payments have been applied. Surface the remaining balance.
- **`expiresAt` on payment links and sessions** -- flag if the expiry is in the past or imminent (within the hour). Suggest creating a new link/session.
- **`fraudResult.accountScore`** -- if present and high (risk scores vary by configuration), flag the transaction as potentially fraudulent so the merchant can review.
- **`threeDSAuthenticationOnly: true`** -- authentication-only mode means no payment is taken. Surface this if the user seems to expect a charge.

## Playbook

### 1. Accept a one-time card payment (Drop-in/Components flow)

1. Call `POST /sessions` with `amount`, `merchantAccount`, `reference`, and `returnUrl` to create a session.
2. Use the returned `id` and `sessionData` to initialize the Adyen Drop-in or Components on the frontend.
3. The shopper completes payment in the browser. On return, call `GET /sessions/{sessionId}` with the `sessionResult` query parameter.
4. Check `status` in the response to confirm payment outcome.

### 2. Authorize, capture, and refund a payment (manual capture flow)

1. Call `POST /payments` with `amount`, `paymentMethod`, `merchantAccount`, `reference`, `returnUrl`, and optionally `captureDelayHours: -1` for manual capture (or set manual capture in the Adyen dashboard).
2. If `resultCode` is `Authorised`, store the `pspReference`.
3. When ready to capture, call `POST /payments/{pspReference}/captures` with the `amount` and `merchantAccount`.
4. To refund later, call `POST /payments/{pspReference}/refunds` with the refund `amount` and `merchantAccount`. Include `merchantRefundReason` if applicable.

### 3. Create and manage a pay-by-link

1. Call `POST /paymentLinks` with `amount`, `merchantAccount`, and `reference`. Optionally set `expiresAt`, `shopperEmail`, and `description`.
2. Share the returned `url` with the customer via email, SMS, or chat.
3. Check the link status anytime with `GET /paymentLinks/{linkId}`.
4. To deactivate the link, call `PATCH /paymentLinks/{linkId}` with `status: "expired"`.

### 4. Save and reuse a shopper's card (tokenization)

1. Call `POST /storedPaymentMethods` with the card details in `paymentMethod`, set `recurringProcessingModel` (e.g., `CardOnFile`), and provide a unique `shopperReference`.
2. Store the returned `id` as the token for future use.
3. For subsequent payments, call `POST /payments` with `paymentMethod: { storedPaymentMethodId: "<id>", type: "scheme" }` and `shopperReference` matching the original. Set `shopperInteraction: "ContAuth"` and `recurringProcessingModel: "CardOnFile"`.
4. To list all saved methods for a shopper, call `GET /storedPaymentMethods?shopperReference=<ref>&merchantAccount=<acct>`.
5. To remove a saved method, call `DELETE /storedPaymentMethods/{id}?shopperReference=<ref>&merchantAccount=<acct>`.

### 5. Handle 3D Secure authentication during payment

1. Call `POST /payments` with the payment details. Include `browserInfo` for web channel, or `threeDS2RequestData` with `deviceChannel` for native mobile.
2. If `resultCode` is `RedirectShopper` or `ChallengeShopper`, an `action` object is returned. Use the Adyen frontend library to handle the action (redirect or challenge).
3. After the shopper completes authentication, collect the result details and call `POST /payments/details` with the `details` object (e.g., `redirectResult` or `threeds2.challengeResult`) and `paymentData` from the original response.
4. Check the final `resultCode` in the response. `Authorised` means success; `Refused` means the payment was declined.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
