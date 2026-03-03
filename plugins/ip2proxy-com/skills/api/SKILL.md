---
name: ip2proxy-proxy-detection
description: "IP2Proxy Proxy Detection API skill. Use when working with IP2Proxy Proxy Detection for root. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# IP2Proxy Proxy Detection
API version: 1.0

## Auth
ApiKey key in query

## Base URL
https://api.ip2proxy.com

## Setup
1. Set your API key in the appropriate header
2. GET / -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Check if an IP address is proxy |

## Enhanced Skill Content
## Question Mapping

- "Is this IP address a proxy?" -> GET /
- "Check if 8.8.8.8 is using a VPN" -> GET /?ip=8.8.8.8&key={key}
- "What type of proxy is this IP?" -> GET /?ip={ip}&key={key}&package=PX11
- "Which country does this proxy IP originate from?" -> GET /?ip={ip}&key={key}&package=PX3
- "Is this IP a Tor exit node?" -> GET /?ip={ip}&key={key}&package=PX8
- "Get proxy detection results in XML format" -> GET /?ip={ip}&key={key}&format=xml
- "What ISP is associated with this IP?" -> GET /?ip={ip}&key={key}&package=PX4
- "What domain is registered to this IP?" -> GET /?ip={ip}&key={key}&package=PX5
- "Detect if a user is hiding behind a data center proxy" -> GET /?ip={ip}&key={key}&package=PX2
- "Get the usage type for a suspicious IP" -> GET /?ip={ip}&key={key}&package=PX9
- "What threat level does this proxy IP have?" -> GET /?ip={ip}&key={key}&package=PX10
- "Look up the AS number for a proxied IP" -> GET /?ip={ip}&key={key}&package=PX7
- "Check proxy status and get the provider name" -> GET /?ip={ip}&key={key}&package=PX11

## Response Tips

- **Proxy detection (GET /)**: Response nesting depends on `package` tier -- higher packages (PX2-PX11) return additional fields like `proxyType`, `countryCode`, `isp`, `domain`, `usageType`, `asn`, `threat`, `provider`, and `lastSeen`. The `isProxy` field returns `0` (not proxy), `1` (proxy), `2` (data center), or `-1` (not supported). A `response` field of `OK` confirms success; `INVALID_IP_ADDRESS`, `MISSING_PARAMETER`, `INVALID_API_KEY`, or `INSUFFICIENT_CREDIT` indicate errors. XML format wraps the same fields in `<result>` tags.

## Anomaly Flags

- **Insufficient credits**: Surface immediately when `response` returns `INSUFFICIENT_CREDIT` -- the account needs a top-up or plan upgrade before further queries work.
- **Invalid API key**: Flag `INVALID_API_KEY` responses and prompt the user to verify their key, as subsequent calls will all fail.
- **Unsupported IP**: When `isProxy` returns `-1`, alert that the queried IP is not supported by the current package tier.
- **Data center IPs**: When `isProxy` returns `2`, proactively note this is a data center/hosting IP (not a traditional proxy) as it may warrant different handling than residential proxies.
- **Package mismatch**: If a user asks for fields (e.g., ISP, threat) that require a higher package tier than specified, warn before making the call.

## Playbook

### 1. Quick Proxy Check for a Single IP

1. Call `GET /?ip={target_ip}&key={api_key}` with default package.
2. Check `response` field equals `OK`.
3. Read `isProxy` -- `0` means clean, `1` means proxy, `2` means data center.
4. Report result to user with country code if available.

### 2. Deep Proxy Intelligence Lookup

1. Call `GET /?ip={target_ip}&key={api_key}&package=PX11` to get all available fields.
2. Verify `response` is `OK` (if `INSUFFICIENT_CREDIT`, fall back to a lower package like PX2).
3. Extract `proxyType`, `isp`, `domain`, `usageType`, `threat`, and `provider`.
4. Summarize findings: proxy type, threat level, provider identity, and usage classification.

### 3. Batch Screening of Multiple IPs

1. Prepare a list of IPs to check.
2. For each IP, call `GET /?ip={ip}&key={api_key}&package=PX2`.
3. Collect results, grouping by `isProxy` value (clean vs proxy vs data center).
4. Flag any `INSUFFICIENT_CREDIT` responses and stop further calls.
5. Present a summary table of flagged IPs with proxy type and country.

### 4. Fraud Prevention Integration

1. Receive a user's IP from your application.
2. Call `GET /?ip={user_ip}&key={api_key}&package=PX10` to get threat assessment.
3. If `isProxy` is `1` or `2`, check the `threat` field for severity.
4. Apply risk rules: block high-threat proxies, flag data center IPs for review, allow clean IPs.
5. Log the `proxyType` and `provider` for audit trail.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
