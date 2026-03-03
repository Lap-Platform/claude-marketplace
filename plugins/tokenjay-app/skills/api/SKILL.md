---
name: tokenjay-api-services
description: "TokenJay API services API skill. Use when working with TokenJay API services for payment, mosaik, tokens. Covers 27 endpoints."
version: 1.0.0
generator: lapsh
---

# TokenJay API services

## Auth
No authentication required.

## Base URL
https://api.tokenjay.app/

## Setup
1. No auth setup needed
2. GET /tokens/prices/all -- verify access
3. POST /payment/addrequest -- create first addrequest

## Endpoints

27 endpoints across 9 groups. See references/api-spec.lap for full details.

### payment
| Method | Path | Description |
|--------|------|-------------|
| POST | /payment/addrequest | Creates a new payment request. Will return request id to check for transaction state and ergopay url to show the user as QR code |
| GET | /payment/state/{requestId} | Returns the state of a payment request. Please note that payment requests are purged after some time, so persist the state at your side when needed |

### mosaik
| Method | Path | Description |
|--------|------|-------------|
| POST | /mosaik/tokenburn/prepare |  |
| POST | /mosaik/babelfee/newoffer/new-input |  |
| POST | /mosaik/babelfee/newoffer/doit |  |
| GET | /mosaik/tokenburn |  |
| GET | /mosaik/tokenburn/get/{uuid} |  |
| GET | /mosaik/boxconsolidation/consolidate/{p2pkaddress} |  |
| GET | /mosaik/boxconsolidation/ |  |
| GET | /mosaik/babelfee/notificationcheck |  |
| GET | /mosaik/babelfee/newoffer |  |
| GET | /mosaik/babelfee/ |  |

### tokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /tokens/prices/{tokenId} | Lists price and available volume for a certain token |
| GET | /tokens/prices/all | Lists all token prices and available volume |
| GET | /tokens/listGenuine | Lists all genuine tokens known |
| GET | /tokens/listBlocked | Lists all blocked tokens |
| GET | /tokens/check/{tokenId}/{tokenName} | Check a token verification |

### sigusd
| Method | Path | Description |
|--------|------|-------------|
| GET | /sigusd/price | Lists price and available volume for SigmaUSD |
| GET | /sigusd/exchange/{amount}/info | Calculates SigUSD exchange |
| GET | /sigusd/exchange/ | Builds ErgoPayRequest for SigUSD exchange |

### sigrsv
| Method | Path | Description |
|--------|------|-------------|
| GET | /sigrsv/price | Lists price and available volume for SigmaRSV |
| GET | /sigrsv/exchange/{amount}/info | Calculates SigRSV exchange |
| GET | /sigrsv/exchange/ | Builds ErgoPayRequest for SigRSV exchange |

### peers
| Method | Path | Description |
|--------|------|-------------|
| GET | /peers/list | Lists known peers sorted by block height |

### createbabel
| Method | Path | Description |
|--------|------|-------------|
| GET | /createbabel/{address} |  |

### cancelbabel
| Method | Path | Description |
|--------|------|-------------|
| GET | /cancelbabel/{boxId} |  |

### ageusd
| Method | Path | Description |
|--------|------|-------------|
| GET | /ageusd/info | Returns state of AgeUSD at this moment |

## Enhanced Skill Content
## Question Mapping

- "What is the current price of a specific token?" -> GET /tokens/prices/{tokenId}
- "Show me all token prices at once" -> GET /tokens/prices/all
- "Which tokens are verified as genuine?" -> GET /tokens/listGenuine
- "Which tokens are blocked or flagged?" -> GET /tokens/listBlocked
- "Is this token legitimate?" -> GET /tokens/check/{tokenId}/{tokenName}
- "What is the current SigUSD price?" -> GET /sigusd/price
- "How much SigUSD would I get for X nanoErgs?" -> GET /sigusd/exchange/{amount}/info
- "What is the current SigRSV price?" -> GET /sigrsv/price
- "How do I create a payment request?" -> POST /payment/addrequest
- "What is the status of my payment?" -> GET /payment/state/{requestId}
- "How do I create a babel fee offer?" -> POST /mosaik/babelfee/newoffer/doit
- "How do I cancel a babel fee box?" -> GET /cancelbabel/{boxId}
- "Show me the AgeUSD protocol info" -> GET /ageusd/info
- "List available network peers" -> GET /peers/list
- "How do I consolidate my UTXOs?" -> GET /mosaik/boxconsolidation/consolidate/{p2pkaddress}

## Response Tips

- **Tokens**: Prices return numeric values in nanoErg scale; divide by 1e9 for ERG. The genuine/blocked lists return arrays -- cross-reference tokenId before transacting.
- **SigUSD/SigRSV**: The `/exchange/{amount}/info` endpoint returns rate previews without executing; the `/exchange/` endpoint initiates the actual swap. Watch for int64 overflow on large amounts.
- **Payment**: `addrequest` returns a requestId used to poll `/payment/state/{requestId}`. States progress through pending to completed or expired.
- **Mosaik**: Babel fee and token burn flows are multi-step -- POST endpoints return intermediate transaction data that must be signed client-side.
- **Errors**: All endpoints share the same error code set (400 bad input, 401 unauthorized, 404 not found, 409 conflict/duplicate). Error bodies typically contain a message string.

## Anomaly Flags

- **409 Conflict on payment**: A duplicate payment request was submitted -- surface the existing requestId rather than retrying.
- **Token blocked status**: If a tokenId appears on `/tokens/listBlocked`, warn the user before any transaction involving that token.
- **Exchange rate drift**: When using `checkRate` on SigUSD/SigRSV exchange, a 400 may indicate the rate moved beyond tolerance -- flag this as market volatility rather than an error.
- **Empty peer list**: If `/peers/list` returns zero results even with `unreachable=true`, the network may be experiencing connectivity issues -- surface this proactively.
- **Token check mismatch**: If `/tokens/check/{tokenId}/{tokenName}` returns a negative result, flag a potential scam or impersonation token before proceeding.

## Playbook

### 1. Accept a Token Payment

1. Call `POST /payment/addrequest` with `nanoErg`, `receiverAddress`, `tokenId`, and `tokenRawAmount`.
2. Store the returned `requestId`.
3. Poll `GET /payment/state/{requestId}` until the state indicates completion or expiration.
4. On success, confirm the transaction to the user.

### 2. Exchange ERG for SigUSD

1. Call `GET /sigusd/price` to show the user the current rate.
2. Call `GET /sigusd/exchange/{amount}/info` with the desired nanoErg amount to preview the exchange.
3. If the rate is acceptable, call `GET /sigusd/exchange/` with `amount`, `address`, and optionally `checkRate` to set a slippage tolerance.
4. Sign and submit the returned transaction.

### 3. Verify a Token Before Transacting

1. Call `GET /tokens/listBlocked` and check if the tokenId appears in the blocked list.
2. Call `GET /tokens/check/{tokenId}/{tokenName}` to validate the token's identity.
3. Call `GET /tokens/prices/{tokenId}` to confirm it has market activity.
4. Proceed with the transaction only if all checks pass.

### 4. Create and Manage a Babel Fee Offer

1. Call `GET /mosaik/babelfee/newoffer` to load the offer creation form data.
2. Call `POST /mosaik/babelfee/newoffer/new-input` to prepare the input for the offer.
3. Call `POST /mosaik/babelfee/newoffer/doit` to finalize and submit the babel fee offer.
4. To cancel later, call `GET /cancelbabel/{boxId}` with the offer's box ID.

### 5. Consolidate Wallet UTXOs

1. Call `GET /mosaik/boxconsolidation/` to check consolidation service availability.
2. Call `GET /mosaik/boxconsolidation/consolidate/{p2pkaddress}` with the wallet address.
3. Sign and submit the returned consolidation transaction.
4. Verify the wallet now has fewer, larger UTXOs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
