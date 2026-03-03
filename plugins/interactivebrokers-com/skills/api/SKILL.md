---
name: ibkr-3rd-party-web-api
description: "IBKR 3rd Party Web API skill. Use when working with IBKR 3rd Party Web for oauth, accounts, secdef. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# IBKR 3rd Party Web API
API version: 1.0.0

## Auth
ApiKey portal in header

## Base URL
https://www.interactivebrokers.com/tradingapi/v1

## Setup
1. Set your API key in the appropriate header
2. GET /accounts -- verify access
3. POST /oauth/request_token -- create first request_token

## Endpoints

16 endpoints across 4 groups. See references/api-spec.lap for full details.

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/request_token | Obtain a request token |
| POST | /oauth/access_token | Obtain a access token |
| POST | /oauth/live_session_token | Obtain a live session token |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | Brokerage Accounts |
| GET | /accounts/{account}/positions | Account Positions |
| GET | /accounts/{account}/summary | Account Values Summary |
| GET | /accounts/{account}/orders | Open Orders |
| POST | /accounts/{account}/orders | Place Order |
| GET | /accounts/{account}/orders/{CustomerOrderId} | Return specific order info |
| DELETE | /accounts/{account}/orders/{CustomerOrderId} | Cancel Order |
| PUT | /accounts/{account}/orders/{CustomerOrderId} | Modify Order |
| POST | /accounts/{account}/order_impact | Return margin impact info |
| GET | /accounts/{account}/trades | Returns trades in account |

### secdef
| Method | Path | Description |
|--------|------|-------------|
| GET | /secdef | Get security definition |

### marketdata
| Method | Path | Description |
|--------|------|-------------|
| GET | /marketdata/snapshot | Market Data Snapshot |
| GET | /marketdata/exchange_components | Exchange Components |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the IBKR API?" -> POST /oauth/request_token
- "How do I get an access token?" -> POST /oauth/access_token
- "How do I create a live session token?" -> POST /oauth/live_session_token
- "What accounts do I have?" -> GET /accounts
- "What are my current positions?" -> GET /accounts/{account}/positions
- "What is my account balance or summary?" -> GET /accounts/{account}/summary
- "Show me my open orders" -> GET /accounts/{account}/orders
- "Place a new order" -> POST /accounts/{account}/orders
- "What is the status of my order?" -> GET /accounts/{account}/orders/{CustomerOrderId}
- "Cancel an order" -> DELETE /accounts/{account}/orders/{CustomerOrderId}
- "Modify an existing order" -> PUT /accounts/{account}/orders/{CustomerOrderId}
- "What would happen if I placed this order?" -> POST /accounts/{account}/order_impact
- "Show my recent trades" -> GET /accounts/{account}/trades
- "Look up a security definition or contract details" -> GET /secdef
- "Get a real-time market quote" -> GET /marketdata/snapshot
- "What exchanges are available?" -> GET /marketdata/exchange_components

## Response Tips

- **OAuth endpoints**: 200 returns tokens/session data. 401 means invalid credentials; 403 means permissions issue. Always check for expiry fields in the response.
- **Account endpoints**: 200 = data ready; 202 = request accepted but data still processing (poll again); 204 = no data available for this account. Always handle all three.
- **Order endpoints**: POST returns order confirmation with a CustomerOrderId for tracking. DELETE returns cancellation status -- verify the order state before assuming success.
- **Security definitions**: Response contains contract details keyed by instrument identifiers. The body parameter is required even on GET -- pass search criteria as query params or structured body.
- **Market data**: Snapshot returns point-in-time quotes, not streaming. Exchange components returns a flat list -- no pagination.

## Anomaly Flags

- **202 Accepted loops**: If account endpoints repeatedly return 202 without eventually resolving to 200, surface this -- the backend may be stalled or the account may be in a restricted state.
- **408 Request Timeout**: Present on every endpoint. If seen more than once in succession, flag potential connectivity or session issues and suggest regenerating the live session token.
- **401 after successful auth**: Likely indicates an expired live session token. Proactively suggest calling POST /oauth/live_session_token before retrying.
- **Order impact vs. order mismatch**: If POST /accounts/{account}/order_impact returns successfully but the subsequent POST /accounts/{account}/orders fails, surface the discrepancy -- order parameters may have drifted.
- **204 on positions or trades**: Could mean the account genuinely has no positions/trades, or the data feed is lagging. Flag if unexpected given recent order activity.
- **Missing account parameter**: GET /accounts requires an account identifier despite listing all accounts -- flag if the caller omits it to avoid silent failures.

## Playbook

### 1. Full Authentication Flow

1. Call POST /oauth/request_token with your consumer key and signature to get a temporary request token.
2. Direct the user through IBKR's authorization flow using the request token.
3. Call POST /oauth/access_token with the authorized request token to receive a long-lived access token.
4. Call POST /oauth/live_session_token to establish an active trading session. This must be done before any account or trading calls.

### 2. Place an Order with Pre-flight Check

1. Call GET /accounts to retrieve available account IDs.
2. Call GET /secdef with the instrument details to confirm the contract ID and trading rules.
3. Call POST /accounts/{account}/order_impact with the proposed order body to preview margin impact, commissions, and buying power changes.
4. Review the impact response. If acceptable, call POST /accounts/{account}/orders with the same order body to submit.
5. Call GET /accounts/{account}/orders/{CustomerOrderId} to confirm the order was accepted and monitor fill status.

### 3. Monitor and Manage Open Orders

1. Call GET /accounts/{account}/orders to list all open orders.
2. For a specific order, call GET /accounts/{account}/orders/{CustomerOrderId} to check its current status.
3. To modify, call PUT /accounts/{account}/orders/{CustomerOrderId} with updated parameters (e.g., new limit price).
4. To cancel, call DELETE /accounts/{account}/orders/{CustomerOrderId} and verify the response confirms cancellation.

### 4. Daily Portfolio Review

1. Call GET /accounts/{account}/summary to check net liquidation value, cash balance, and margin utilization.
2. Call GET /accounts/{account}/positions to review all current holdings with quantity, cost basis, and unrealized P&L.
3. Call GET /accounts/{account}/trades with the `since` parameter set to today's date to see fills from the current session.
4. Call GET /marketdata/snapshot for any positions you want to compare against live market prices.

### 5. Security Lookup and Market Data

1. Call GET /secdef with search criteria (symbol, exchange, instrument type) to find the matching contract.
2. Note the contract identifier from the response.
3. Call GET /marketdata/snapshot with the contract identifier(s) to retrieve current bid, ask, last price, and volume.
4. Call GET /marketdata/exchange_components to verify which exchanges list the instrument and their trading hours.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
