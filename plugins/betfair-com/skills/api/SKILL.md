---
name: betfair-exchange-streaming-api
description: "Betfair: Exchange Streaming API skill. Use when working with Betfair: Exchange Streaming for request. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Betfair: Exchange Streaming API
API version: 1.0.1423

## Auth
No authentication required.

## Base URL
http://stream-api.betfair.com:443/api

## Setup
1. No auth setup needed
3. POST /request -- create first request

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### request
| Method | Path | Description |
|--------|------|-------------|
| POST | /request | This is a socket protocol delimited by CRLF (not http) |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate to the Betfair streaming API?" -> POST /request (send AuthenticationMessage with appKey and session token)
- "How do I subscribe to live market prices?" -> POST /request (send MarketSubscriptionMessage with marketFilter and marketDataFilter)
- "How do I get real-time order updates?" -> POST /request (send OrderSubscriptionMessage with optional orderProjection)
- "How do I keep the connection alive?" -> POST /request (send HeartbeatMessage periodically to prevent timeout)
- "How do I unsubscribe from a market?" -> POST /request (send a new MarketSubscriptionMessage with updated marketFilter excluding that market)
- "How do I get full image snapshots instead of deltas?" -> POST /request (MarketSubscriptionMessage with conflateMs set to 0 and initial image requested)
- "How do I filter streaming data to specific event types or competitions?" -> POST /request (use marketFilter fields: eventTypeIds, eventIds, marketTypes inside MarketSubscriptionMessage)
- "How do I reduce bandwidth by requesting only best prices?" -> POST /request (set marketDataFilter with ladderLevels=1 or fields=[EX_BEST_OFFERS_DISP])
- "How do I handle a disconnection and resubscribe?" -> POST /request (reconnect, re-authenticate, resend subscriptions with initialClk/clk from last received message)
- "How do I throttle update frequency?" -> POST /request (set conflateMs in MarketSubscriptionMessage, e.g. 500 for half-second updates)
- "How do I stream in-play market data only?" -> POST /request (use marketFilter with turnInPlayEnabled or inPlayOnly flags)
- "Can I subscribe to multiple markets at once?" -> POST /request (include multiple marketIds in the marketFilter of MarketSubscriptionMessage)
- "How do I detect that a market has closed?" -> POST /request (monitor MarketChangeMessage for marketDefinition.status = CLOSED)

## Response Tips

- **Connection/Auth**: ConnectionMessage arrives immediately on connect with connectionId; StatusMessage confirms auth success or reports errors via errorCode/errorMessage -- always check statusCode field before proceeding.
- **Market Data**: MarketChangeMessage contains img (full image) or a delta; apply changes incrementally using the ct field (SUB_IMAGE, RESUB_DELTA, HEARTBEAT) to determine merge strategy.
- **Order Data**: OrderChangeMessage nests under oc[] with matched/unmatched arrays per market; reconcile using id field as the unique bet identifier.
- **Heartbeats**: Expect heartbeat responses with no data payload; absence beyond ~5s signals a stale connection requiring reconnect.
- **Errors**: StatusMessage with statusCode != null indicates failure; common errorCodes: INVALID_INPUT, NOT_AUTHORIZED, SUBSCRIPTION_LIMIT_EXCEEDED, MAX_CONNECTION_LIMIT_EXCEEDED.

## Anomaly Flags

- **Connection limit approaching**: Betfair enforces a per-appKey connection cap (typically 2-4); surface a warning if multiple connections are active or a MAX_CONNECTION_LIMIT_EXCEEDED error is received.
- **Stale stream detection**: If no message (including heartbeats) is received for more than 5 seconds, flag the connection as potentially dead and recommend reconnect.
- **Subscription limit exceeded**: Flag SUBSCRIPTION_LIMIT_EXCEEDED immediately -- the client is requesting more markets than the account tier allows.
- **Clock drift / resubscription needed**: If a MarketChangeMessage arrives with ct=RESUB_DELTA or the clk token changes unexpectedly, surface that the stream may have missed updates and a full resubscription is advisable.
- **Market closure cascade**: When multiple markets return status=CLOSED in rapid succession, alert that an event has likely concluded -- subscriptions can be cleaned up.
- **Authentication expiry**: Betfair session tokens expire (typically 4-8 hours); if a StatusMessage returns NOT_AUTHORIZED mid-session, flag that re-authentication with a fresh token is required.
- **Deprecated fields**: Watch for unrecognized fields in MarketDefinition or OrderRunnerChange that may indicate API version drift.

## Playbook

### 1. Connect and Subscribe to Market Prices

1. Open a TCP/SSL connection to `stream-api.betfair.com:443/api`
2. Receive the initial `ConnectionMessage` with `connectionId`
3. POST /request with `AuthenticationMessage` containing your `appKey` and `session` (SSO token from Betfair identity API)
4. Confirm `StatusMessage` returns no error
5. POST /request with `MarketSubscriptionMessage` including `marketFilter` (e.g., `marketIds: ["1.234567"]`) and `marketDataFilter` (e.g., `fields: ["EX_BEST_OFFERS"]`)
6. Begin processing `MarketChangeMessage` responses -- first message is a full image, subsequent are deltas

### 2. Monitor Live Orders

1. Authenticate as above (steps 1-4 from Playbook 1)
2. POST /request with `OrderSubscriptionMessage` (optionally set `orderProjection` to filter by status)
3. Process incoming `OrderChangeMessage` events, reconciling by bet `id`
4. On disconnection, reconnect, re-authenticate, and resubscribe using saved `initialClk`/`clk` values to resume from last known state

### 3. Graceful Reconnection After Disconnect

1. Detect disconnect (socket error or heartbeat timeout > 5s)
2. Re-open TCP/SSL connection and receive new `ConnectionMessage`
3. POST /request with `AuthenticationMessage` (refresh session token if expired)
4. POST /request with previous `MarketSubscriptionMessage`, adding `initialClk` and `clk` from the last received `MarketChangeMessage`
5. The server responds with a delta from your last position rather than a full image, minimizing data transfer
6. If server returns an error on clk resume, fall back to a fresh subscription without clk

### 4. Bandwidth-Optimized Streaming for Multiple Markets

1. Authenticate to the stream
2. POST /request with `MarketSubscriptionMessage` using `conflateMs: 1000` (1-second throttle) to reduce update frequency
3. Set `marketDataFilter` with `ladderLevels: 3` and `fields: ["EX_BEST_OFFERS_DISP"]` to limit price depth
4. Group markets by event using `eventIds` in `marketFilter` rather than listing individual `marketIds` to simplify management
5. Monitor total subscription count against your account tier limit

### 5. End-of-Event Cleanup

1. Monitor `MarketChangeMessage` for `marketDefinition.status` transitioning to `CLOSED` or `COMPLETE`
2. Log final market state and any settled order data from `OrderChangeMessage`
3. POST /request with an updated `MarketSubscriptionMessage` removing closed `marketIds` from the filter
4. If all markets for an event are closed, evaluate whether to maintain the connection or disconnect to free up connection slots


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
