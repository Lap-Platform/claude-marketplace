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

- "How do I charge a customer's credit card?" -> POST /authorise
- "How do I capture a previously authorized payment?" -> POST /capture
- "How do I refund a transaction?" -> POST /refund
- "How do I cancel a payment that hasn't been captured yet?" -> POST /cancel
- "I'm not sure if the payment was captured -- how do I reverse it safely?" -> POST /cancelOrRefund
- "How do I complete 3D Secure authentication for a payment?" -> POST /authorise3d
- "How do I handle 3DS2 authentication challenges?" -> POST /authorise3ds2
- "How do I adjust the amount on an existing authorization?" -> POST /adjustAuthorisation
- "How do I process a donation from a transaction?" -> POST /donate
- "How do I check the 3DS authentication result for a payment?" -> POST /getAuthenticationResult
- "How do I retrieve the 3DS2 result after the challenge flow?" -> POST /retrieve3ds2Result
- "How do I cancel a payment when I only have the merchant reference, not the PSP reference?" -> POST /technicalCancel
- "How do I void a refund that's still pending?" -> POST /voidPendingRefund
- "How do I set up a recurring/subscription payment?" -> POST /authorise (with `recurring` and `recurringProcessingModel` fields)
- "How do I split a payment across multiple accounts (marketplace)?" -> POST /authorise (with `splits` field)

## Response Tips

- **Authorization responses** (`/authorise`, `/authorise3d`, `/authorise3ds2`): Check `resultCode` first -- `Authorised` means success, `Refused` means declined, `RedirectShopper` means 3DS redirect is required (`issuerUrl`, `md`, `paRequest` will be populated). Always store the `pspReference` for subsequent operations.
- **Modification responses** (`/cancel`, `/capture`, `/refund`, `/adjustAuthorisation`, `/cancelOrRefund`, `/technicalCancel`, `/voidPendingRefund`): The `response` field contains the outcome string (e.g., `[capture-received]`, `[cancel-received]`). These are async -- a `received` response means accepted for processing, not final. Listen for webhooks for the definitive result.
- **3DS result responses** (`/getAuthenticationResult`, `/retrieve3ds2Result`): Return nested `threeDS1Result` or `threeDS2Result` maps. Check `transStatus` for authentication outcome (`Y` = success, `N` = failed, `C` = challenge required).
- **Error responses** (400/401/403/422/500): All endpoints share the same error code set. 422 typically indicates validation failure on business rules (e.g., invalid amount, already-captured payment). 401/403 indicate API key issues.
- **additionalData**: Present on nearly every response as a generic key-value map. Contains risk scores, scheme-specific data, and acquirer details -- always inspect it for debugging.

## Anomaly Flags

- **`resultCode: "Error"` or unexpected values**: Surface immediately -- indicates a system-level failure distinct from a normal refusal.
- **`fraudResult.accountScore` above threshold**: Flag high fraud scores (typically > 50) so the user can decide whether to proceed with capture.
- **`refusalReason` present on authorization**: Always surface the reason text -- common values include `REFUSED`, `BLOCK_CARD`, `CVC_DECLINED`, `EXPIRED_CARD`.
- **422 on modifications**: Likely means the original transaction is in a state that doesn't allow the operation (e.g., capturing an already-captured payment, refunding beyond the original amount). Surface the error detail.
- **3DS `transStatus: "N"` or `challengeCancel` populated**: Authentication was denied or abandoned by the cardholder -- flag before retrying.
- **`dccAmount` present in authorization response**: Dynamic currency conversion was applied -- surface the converted amount and signature so the user is aware of rate markup.
- **Missing `pspReference` in a 200 response**: Should never happen; flag as a potential API anomaly requiring investigation.
- **`splits` validation errors**: When using marketplace splits, amounts not summing to the total will cause silent failures downstream -- flag any 422 related to splits.

## Playbook

### 1. Standard Card Payment (Authorize + Capture)

1. Call `POST /authorise` with `amount` (currency + value in minor units), `reference`, `merchantAccount`, and `card` details.
2. Check the response `resultCode`. If `Authorised`, store the `pspReference`.
3. If `RedirectShopper`, redirect the customer to `issuerUrl` for 3DS (continue to Playbook 2).
4. When ready to settle, call `POST /capture` with the stored `pspReference` as `originalReference` and the `modificationAmount`.
5. Confirm the `response` field contains `[capture-received]`.

### 2. 3D Secure Payment Flow

1. Start with `POST /authorise` including `browserInfo` and optionally `threeDS2RequestData`.
2. If `resultCode` is `RedirectShopper`, extract `issuerUrl`, `md`, and `paRequest` from the response.
3. Redirect the shopper to `issuerUrl` with the `md` and `paRequest` values.
4. After the shopper completes authentication, call `POST /authorise3d` with the returned `md` and `paResponse`.
5. Check `resultCode` for `Authorised`. If using 3DS2, use `POST /authorise3ds2` with `threeDS2Result` or `threeDS2Token` instead.
6. Optionally call `POST /getAuthenticationResult` or `POST /retrieve3ds2Result` to inspect detailed authentication data.

### 3. Full Refund of a Payment

1. Locate the `pspReference` of the original authorized and captured payment.
2. Call `POST /refund` with `originalReference` set to the PSP reference and `modificationAmount` matching the original amount.
3. Confirm the `response` field contains `[refund-received]`.
4. If unsure whether the payment was captured, use `POST /cancelOrRefund` instead -- it automatically picks cancel or refund based on the payment state.

### 4. Cancel an Uncaptured Authorization

1. Retrieve the `pspReference` of the authorization to cancel.
2. Call `POST /cancel` with `originalReference` set to that PSP reference.
3. Confirm `response` contains `[cancel-received]`.
4. If you only have the merchant reference (not the PSP reference), use `POST /technicalCancel` with `originalMerchantReference` instead.

### 5. Marketplace Split Payment

1. Call `POST /authorise` with the full `amount`, `reference`, and a `splits` array defining how funds distribute across sub-merchant accounts.
2. Each split entry needs `type` (e.g., `MarketPlace`, `Commission`), `amount` with `value` and `currency`, and the target `account`.
3. Ensure split amounts sum to the total authorization amount.
4. On capture via `POST /capture`, include the same `splits` array to confirm the distribution.
5. For refunds, include `splits` in the `POST /refund` call to reverse the correct portions per account.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
