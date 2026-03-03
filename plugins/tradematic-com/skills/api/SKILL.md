---
name: tradematic-api
description: "Tradematic API skill. Use when working with Tradematic for ping, time, client. Covers 90 endpoints."
version: 1.0.0
generator: lapsh
---

# Tradematic API
API version: 1.0.6

## Auth
ApiKey X-API-Key in header

## Base URL
https://api.tradematic.com

## Setup
1. Set your API key in the appropriate header
2. GET /ping -- verify access
3. POST /client/users/login -- create first login

## Endpoints

90 endpoints across 9 groups. See references/api-spec.lap for full details.

### ping
| Method | Path | Description |
|--------|------|-------------|
| GET | /ping | Ping |

### time
| Method | Path | Description |
|--------|------|-------------|
| GET | /time | Get current server time |

### client
| Method | Path | Description |
|--------|------|-------------|
| GET | /client/users | Get users list |
| GET | /client/users/{userid} | Get user by ID |
| POST | /client/users/login | Logs user into the system |
| POST | /client/users/register | Register a new user |
| GET | /client/users/roles | Get user roles list |
| PUT | /client/users/{userid}/role | Get user roles list |
| POST | /client/users/check | Checks for a user |
| GET | /client/apikeys | Get API keys |
| POST | /client/apikeys | Create new API key |
| DELETE | /client/apikeys/{keyid} | Delete API key |

### autofollow
| Method | Path | Description |
|--------|------|-------------|
| GET | /autofollow/strategies | Get autofollow strategies list |
| POST | /autofollow/strategies | Create new autofollow strategy |
| GET | /autofollow/strategies/{strategyid} | Get autofollow strategy by ID |
| PUT | /autofollow/strategies/{strategyid} | Update autofollow strategy |
| PUT | /autofollow/strategies/{strategyid}/content | Update rules for strategy that was created with strategy builder, or just content field |
| PUT | /autofollow/strategies/{strategyid}/state | Update autofollow strategy state |
| PUT | /autofollow/strategies/{strategyid}/status | Update autofollow strategy status |
| GET | /autofollow/strategies/{strategyid}/positions | Get positions for strategy |
| POST | /autofollow/strategies/{strategyid}/positions | Send a new position for autofollow strategy |
| PUT | /autofollow/strategies/{strategyid}/positions | Update an existing position for autofollow strategy |
| DELETE | /autofollow/strategies/{strategyid}/positions | Delete an existing position for autofollow strategy |
| GET | /autofollow/strategies/{strategyid}/signals | Get trading signals for strategy |
| POST | /autofollow/strategies/{strategyid}/signals | Send a new signal for autofollow strategy |
| GET | /autofollow/strategies/risklevels | Get risk levels |
| GET | /autofollow/strategies/rates | Get strategies rates |
| GET | /autofollow/strategies/statuses | Get strategies statuses |
| GET | /autofollow/authors | Get authors |

### taskmanager
| Method | Path | Description |
|--------|------|-------------|
| GET | /taskmanager/tasks | Get tasks list |
| POST | /taskmanager/tasks | Create a new task |
| GET | /taskmanager/tasks/{taskid} | Get task by ID |
| GET | /taskmanager/tasks/{taskid}/status | Get task status |
| GET | /taskmanager/tasks/{taskid}/folder | Get task result folder name |
| GET | /taskmanager/tasks/{taskid}/result | Get task result |
| GET | /taskmanager/tasks/{taskid}/result2 | Get task result (version 2) |
| GET | /taskmanager/tasks/{taskid}/equity | Get data for equity chart |
| GET | /taskmanager/tasks/{taskid}/equitypct | Get data for equity chart (%) |
| GET | /taskmanager/tasks/{taskid}/equitypctsm | Get spared data for equity chart (%) |
| GET | /taskmanager/tasks/{taskid}/drawdown | Get data for drawdown chart |
| GET | /taskmanager/tasks/{taskid}/performance | Get backtest statistics |
| GET | /taskmanager/tasks/{taskid}/trades | Get backtest trades list |
| GET | /taskmanager/tasks/{taskid}/contribution | Get backtest symbol contribution data |
| GET | /taskmanager/tasks/{taskid}/bymonths | Get backtest data for equity chart, grouped by months |
| GET | /taskmanager/tasks/{taskid}/byquarters | Get backtest data for equity chart, grouped by quarters |
| GET | /taskmanager/tasks/{taskid}/byyears | Get backtest data for equity chart, grouped by years |

### builder
| Method | Path | Description |
|--------|------|-------------|
| GET | /builder/rules | Get strategy builder rules list |
| GET | /builder/rules/{ruleid} | Get strategy builder rules by ID |

### marketdata
| Method | Path | Description |
|--------|------|-------------|
| GET | /marketdata/markets | Get markets list |
| GET | /marketdata/markets/{name} | Get market by name |
| GET | /marketdata/indicators | Get technical indicators list |
| GET | /marketdata/indicators/{name} | Get technical indicator by name |
| GET | /marketdata/indicators/{name}/histdata | Get technical indicator historical data by name |
| GET | /marketdata/symbols | Get symbols list |
| GET | /marketdata/symbols/{name} | Get symbol by name |
| GET | /marketdata/symbols/{name}/histdata | Get historical data for instrument |
| GET | /marketdata/symbols/{name}/snapshot | Get snapshot for a symbol by name |
| GET | /marketdata/symbols/snapshots | Get snapshots for symbols |

### cloud
| Method | Path | Description |
|--------|------|-------------|
| GET | /cloud/accounts | Get trading accounts list |
| GET | /cloud/accounts/{accountid} | Get trading account by ID |
| GET | /cloud/accounts/{accountid}/orders | Get orders list by account |
| POST | /cloud/accounts/{accountid}/orders | Place a new order |
| DELETE | /cloud/accounts/{accountid}/orders/{orderid} | Cancel an order by ID |
| GET | /cloud/accounts/{accountid}/trades | Get trades list by account |
| GET | /cloud/accounts/{accountid}/snapshots | Get account equity and cash snapshots |
| POST | /cloud/accounts/{accountid}/closeall | Close all positions by account |
| POST | /cloud/accounts/{accountid}/close | Close symbol position by account |
| POST | /cloud/accounts/{accountid}/sync | Syhchronize an account with account active strategies |
| GET | /cloud/accounts/{accountid}/sync | Get synchronization status of account with account active strategies |
| GET | /cloud/accounts/{accountid}/commands | Get commands list by account |
| GET | /cloud/commands | Get commands list |
| GET | /cloud/commands/{commandid} | Get command by ID |
| GET | /cloud/sessions | Get sessions list |
| GET | /cloud/sessions/{sessionid} | Get session by ID |
| GET | /cloud/strategies | Get list of active (executing) strategies |
| GET | /cloud/strategies/{strategyid} | Get active (executing) strategy by ID |
| POST | /cloud/strategies/start | Start a strategy execution for account |
| POST | /cloud/strategies/{strategyid}/stop | Stop a strategy execution by ID |
| GET | /cloud/connectors | Get available connectors list |
| GET | /cloud/connectors/{connectorid} | Get connector by ID |
| GET | /cloud/connections | Get connections list |
| POST | /cloud/connections | Create a new connection |
| GET | /cloud/connections/{connectionid} | Get connection by ID |
| PUT | /cloud/connections/{connectionid} | Update existing connection |
| DELETE | /cloud/connections/{connectionid} | Delete connection by ID |

### marketplace
| Method | Path | Description |
|--------|------|-------------|
| GET | /marketplace/balance | Get user balance |
| GET | /marketplace/products | Get products list |
| GET | /marketplace/products/{productid} | Get product by ID |
| GET | /marketplace/products/{productid}/rates | Get product rates by product ID |
| GET | /marketplace/groups | Get product groups list |

## Enhanced Skill Content
## Question Mapping

- "Is the API up?" -> GET /ping
- "What time does the server report?" -> GET /time
- "List all users" -> GET /client/users
- "Find a user by username?" -> GET /client/users?username={username}
- "How do I authenticate a user?" -> POST /client/users/login
- "What trading strategies are available?" -> GET /autofollow/strategies
- "Show me the positions for a strategy" -> GET /autofollow/strategies/{strategyid}/positions
- "What signals has a strategy generated?" -> GET /autofollow/strategies/{strategyid}/signals
- "How is my backtest task performing?" -> GET /taskmanager/tasks/{taskid}/performance
- "Show equity curve for a task" -> GET /taskmanager/tasks/{taskid}/equity
- "Get historical price data for a symbol" -> GET /marketdata/symbols/{name}/histdata
- "What broker accounts do I have?" -> GET /cloud/accounts
- "Place an order on my account" -> POST /cloud/accounts/{accountid}/orders
- "Close all positions on an account" -> POST /cloud/accounts/{accountid}/closeall
- "What's my marketplace balance?" -> GET /marketplace/balance

## Response Tips

- **ping/time**: Flat responses; 200 means healthy, 500 means service degradation -- use for connectivity checks before workflows.
- **client**: User objects may nest role info; 404 on user lookup means invalid userid, not empty result.
- **autofollow**: Strategy lists support `filter` for narrowing; positions/signals are sub-resources that require a valid strategyid or return 404.
- **taskmanager**: Task creation returns 202 (accepted, not complete) -- poll `/tasks/{taskid}/status` for progress. Equity/drawdown endpoints accept `from`, `to`, `count` for windowed results.
- **marketdata**: histdata requires `symbol`, `tf` (timeframe) as query params; snapshots endpoint takes a body array of symbol names for batch lookups.
- **cloud**: Order and strategy start/stop return 202 (async); check `/commands/{commandid}` for execution status. Connections are broker link configs.
- **marketplace**: Products may include nested rate structures; use `/products/{id}/rates` for pricing details separate from product metadata.

## Anomaly Flags

- **202 on write operations**: Cloud orders, strategy start/stop, closeall, and task creation are async. Agent should remind the user to poll for completion status rather than assuming success.
- **Dual result endpoints**: `/tasks/{taskid}/result` and `/result2` exist -- surface both when the user asks for task results, as they may contain different result formats.
- **Missing 404 on list endpoints**: Most list endpoints (strategies, tasks, accounts) only return 500, not 404. An empty list is a valid 200, not an error -- flag if user expects a "not found" response from a collection.
- **Sync has dual methods**: `POST /cloud/accounts/{accountid}/sync` triggers a sync (202), while `GET` on the same path checks sync state (200). Agent should clarify which the user intends.
- **No pagination parameters on most lists**: Endpoints like `/cloud/accounts`, `/autofollow/strategies`, `/marketplace/products` lack `count`/`from`/`to` -- large result sets may arrive in full. Flag if responses seem unusually large.
- **API key scope ambiguity**: `/client/apikeys` allows creating and deleting keys. Agent should warn before DELETE operations on API keys, as this may revoke active access.

## Playbook

### 1. Set Up a New User and Generate an API Key

1. POST /client/users/register with user details in body
2. POST /client/users/login to authenticate and receive a session/token
3. POST /client/apikeys to generate a new API key
4. Store the returned key securely for `X-API-Key` header use

### 2. Browse and Follow a Trading Strategy

1. GET /autofollow/strategies to list available strategies (use `filter` to narrow)
2. GET /autofollow/strategies/{strategyid} to inspect a specific strategy
3. GET /autofollow/strategies/risklevels to understand risk options
4. GET /autofollow/strategies/{strategyid}/signals?count=10 to review recent signals
5. POST /autofollow/strategies/{strategyid}/positions to open a position based on signals

### 3. Run a Backtest and Analyze Results

1. POST /taskmanager/tasks with strategy config in body (returns 202)
2. GET /taskmanager/tasks/{taskid}/status -- poll until complete
3. GET /taskmanager/tasks/{taskid}/result for primary results
4. GET /taskmanager/tasks/{taskid}/performance for summary metrics
5. GET /taskmanager/tasks/{taskid}/equity?from={date}&to={date} for equity curve
6. GET /taskmanager/tasks/{taskid}/drawdown for risk analysis
7. GET /taskmanager/tasks/{taskid}/bymonths for monthly breakdown

### 4. Connect a Broker and Place a Trade

1. GET /cloud/connectors to list supported broker connectors
2. POST /cloud/connections with connector ID and credentials in body
3. GET /cloud/accounts to confirm the account appeared
4. POST /cloud/accounts/{accountid}/sync to pull current state (returns 202)
5. GET /cloud/accounts/{accountid}/sync to verify sync completed
6. POST /cloud/accounts/{accountid}/orders with order details (returns 202)
7. GET /cloud/commands/{commandid} to confirm order execution status

### 5. Monitor Live Strategy and Manage Positions

1. GET /cloud/strategies to list running strategies
2. GET /cloud/strategies/{strategyid} for current state and config
3. GET /cloud/accounts/{accountid}/trades?count=20 to review recent trades
4. GET /cloud/accounts/{accountid}/snapshots for account equity snapshots
5. POST /cloud/accounts/{accountid}/close with position details to exit a specific position
6. POST /cloud/strategies/{strategyid}/stop to halt the strategy (returns 202)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
