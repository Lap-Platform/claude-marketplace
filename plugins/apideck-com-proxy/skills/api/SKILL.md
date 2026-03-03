---
name: proxy-api
description: "Proxy API skill. Use when working with Proxy for proxy. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Proxy API
API version: 10.24.0

## Auth
ApiKey Authorization in header | ApiKey x-apideck-app-id in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /proxy -- verify access
3. POST /proxy -- create first proxy

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### proxy
| Method | Path | Description |
|--------|------|-------------|
| GET | /proxy | GET |
| OPTIONS | /proxy | OPTIONS |
| POST | /proxy | POST |
| PUT | /proxy | PUT |
| PATCH | /proxy | PATCH |
| DELETE | /proxy | DELETE |

## Enhanced Skill Content
## Question Mapping

- "How do I fetch data from a downstream service through Apideck?" -> GET /proxy
- "How do I create a resource in a connected integration?" -> POST /proxy
- "How do I update a record in a downstream API?" -> PUT /proxy
- "How do I partially update a resource through the proxy?" -> PATCH /proxy
- "How do I delete a record from a connected service?" -> DELETE /proxy
- "How do I check which methods a downstream API supports?" -> OPTIONS /proxy
- "How do I call a specific connector service like Salesforce through Apideck?" -> GET /proxy (set x-apideck-service-id header)
- "How do I forward a request to a custom downstream URL?" -> POST /proxy (set x-apideck-downstream-url header)
- "How do I pass downstream auth credentials separately from Apideck auth?" -> Any /proxy (set x-apideck-downstream-authorization header)
- "How do I proxy a request for a specific consumer?" -> Any /proxy (set x-apideck-consumer-id header)
- "How do I target a specific unified API category like CRM or accounting?" -> Any /proxy (set x-apideck-unified-api header)
- "How do I list items from a downstream API that only supports GET?" -> GET /proxy
- "Can I send a raw request body through the proxy to the downstream service?" -> POST /proxy or PUT /proxy
- "How do I troubleshoot a 401 error from the proxy?" -> Verify Authorization, x-apideck-app-id, and x-apideck-consumer-id headers

## Response Tips

- **All proxy endpoints**: Responses are pass-through from the downstream service -- status codes, headers, and body formats vary by connector. Do not assume a fixed schema; inspect the downstream API docs for the targeted service.
- **401 errors**: Can originate from Apideck (bad API key or app ID) or from the downstream service (bad downstream authorization). Check the error body to distinguish the source.
- **OPTIONS responses**: Return allowed methods and CORS headers from the downstream service. Useful for preflight checks before making mutating calls.

## Anomaly Flags

- **Dual-layer auth failures**: Surface when a 401 occurs whether it originates from Apideck or the downstream service, since the proxy masks the source by default.
- **Missing required headers**: Proactively warn if `x-apideck-consumer-id` or `x-apideck-app-id` is absent -- these are required for routing but easy to forget.
- **Downstream URL override**: Flag when `x-apideck-downstream-url` is set, as it bypasses the standard connector routing and may hit unintended endpoints.
- **No service ID specified**: Warn when `x-apideck-service-id` is omitted and the consumer has multiple connectors enabled for the same unified API -- the proxy may pick an unexpected default.
- **Pass-through error codes**: Surface any 4xx/5xx from downstream verbatim, since the proxy returns them as 200-wrapped or raw depending on configuration.

## Playbook

### Fetching CRM Contacts Through a Connected Integration

1. Set `Authorization` header with your Apideck API key
2. Set `x-apideck-app-id` to your application ID
3. Set `x-apideck-consumer-id` to the target consumer
4. Set `x-apideck-service-id` to the specific CRM connector (e.g., `salesforce`)
5. Set `x-apideck-unified-api` to `crm`
6. Send GET /proxy with the downstream path appended via `x-apideck-downstream-url` if needed
7. Parse the downstream response body directly -- format depends on the connector

### Creating a Record in a Downstream Service

1. Authenticate with `Authorization` and `x-apideck-app-id` headers
2. Set `x-apideck-consumer-id` and `x-apideck-service-id` to target the correct connection
3. Build the request body matching the downstream API's expected schema
4. Send POST /proxy with the body
5. Check the response for the created resource ID or confirmation from the downstream service

### Calling a Custom Downstream URL

1. Set all standard auth headers (`Authorization`, `x-apideck-app-id`, `x-apideck-consumer-id`)
2. Set `x-apideck-downstream-url` to the full URL of the target endpoint
3. Optionally set `x-apideck-downstream-authorization` if the downstream requires separate credentials
4. Choose the appropriate HTTP method (GET, POST, PUT, PATCH, DELETE) and send to /proxy
5. The proxy forwards your request verbatim to the specified URL and returns the response

### Debugging a Failed Proxy Request

1. Send OPTIONS /proxy first to confirm the downstream service is reachable and which methods are allowed
2. Verify all required headers are present: `Authorization`, `x-apideck-app-id`, `x-apideck-consumer-id`
3. If you receive a 401, check whether the error body references Apideck auth or downstream auth
4. For Apideck auth issues, regenerate your API key and verify your app ID
5. For downstream auth issues, update `x-apideck-downstream-authorization` or reconfigure the connection in Apideck


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
