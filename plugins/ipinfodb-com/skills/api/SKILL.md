---
name: ipinfodb-ip-address-lookup
description: "IPInfoDB IP Address Lookup API skill. Use when working with IPInfoDB IP Address Lookup for ip-city, ip-country. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# IPInfoDB IP Address Lookup
API version: 1.0

## Auth
ApiKey key in query

## Base URL
https://api.ipinfodb.com

## Setup
1. Set your API key in the appropriate header
2. GET /v3/ip-city/ -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### ip-city
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/ip-city/ | Get location of an IP address |

### ip-country
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/ip-country/ | Get country of an IP address |

## Enhanced Skill Content


## Question Mapping

- "Where is this IP address located?" -> GET /v3/ip-city/
- "What country does this IP belong to?" -> GET /v3/ip-country/
- "Get the city-level geolocation for an IP" -> GET /v3/ip-city/
- "Which country is 8.8.8.8 from?" -> GET /v3/ip-country/
- "What are the latitude and longitude for this IP?" -> GET /v3/ip-city/
- "Look up the region and zip code for an IP" -> GET /v3/ip-city/
- "Do a quick country-only lookup for an IP" -> GET /v3/ip-country/
- "Get geolocation data in XML format" -> GET /v3/ip-city/ (with format=xml)
- "Is this IP from the US?" -> GET /v3/ip-country/
- "What timezone is this IP address in?" -> GET /v3/ip-city/
- "Get full geolocation details including city, region, and coordinates" -> GET /v3/ip-city/
- "Verify what country an IP resolves to before applying geo-restrictions" -> GET /v3/ip-country/
- "Compare geolocation of two IPs" -> GET /v3/ip-city/ (call twice, compare results)

## Response Tips

- **ip-city**: Returns flat object with city, region, country, zip, lat/lon, and timezone. No pagination. Empty strings indicate unknown fields, not nulls.
- **ip-country**: Returns a simpler flat object with country-level data only. Faster than ip-city when you don't need granular location.
- **Both endpoints**: Default response format is JSON. Pass `format=xml` for XML. Status code is always 200; check the `statusCode` field inside the response body for actual success/error state (e.g., "OK" vs "ERROR").

## Anomaly Flags

- **statusCode field says "ERROR"**: The HTTP status is still 200 -- always check the body's `statusCode` field. Surface this immediately; common cause is an invalid or expired API key.
- **Empty location fields**: If city/region come back as empty strings, the IP may be a proxy, VPN, or unresolvable. Flag when multiple consecutive lookups return empty data.
- **Invalid API key**: The API does not return 401/403 -- it returns 200 with an error message in the body. Always validate the `statusMessage` field.
- **Private/reserved IPs**: Passing RFC 1918 addresses (10.x, 172.16-31.x, 192.168.x) returns empty geolocation. Flag when user submits a non-routable IP.
- **Rate limiting**: IPInfoDB enforces request limits per key (typically 2 req/sec on free tier). If responses slow down or return errors, surface the throttling concern.

## Playbook

### 1. Look Up Full Geolocation for a Single IP

1. Call `GET /v3/ip-city/?key={key}&ip={target_ip}&format=json`
2. Check the `statusCode` field in the response body -- confirm it says "OK"
3. Extract `cityName`, `regionName`, `countryCode`, `latitude`, `longitude`, `zipCode`, `timeZone`
4. If any location fields are empty, note that the IP may be behind a VPN or proxy

### 2. Quick Country Check for Access Control

1. Call `GET /v3/ip-country/?key={key}&ip={target_ip}&format=json`
2. Verify `statusCode` is "OK"
3. Read `countryCode` and `countryName`
4. Compare against your allow/block list and apply the appropriate rule

### 3. Batch Geolocation of Multiple IPs

1. Collect the list of IPs to look up
2. For each IP, call `GET /v3/ip-city/?key={key}&ip={ip}&format=json`
3. Respect rate limits -- space requests at least 500ms apart on free-tier keys
4. Aggregate results; flag any responses where `statusCode` is not "OK" or location fields are empty
5. If only country-level data is needed, use `/v3/ip-country/` instead for faster throughput

### 4. Validate an API Key

1. Call `GET /v3/ip-country/?key={key}&ip=8.8.8.8&format=json` using a known public IP
2. Check `statusCode` in the response body
3. If it returns "ERROR" with a message about the key, the key is invalid or expired
4. If it returns "OK" with `countryCode: "US"`, the key is working correctly

### 5. Compare Geolocation Across Endpoints

1. Call `GET /v3/ip-country/?key={key}&ip={ip}&format=json` and record the country
2. Call `GET /v3/ip-city/?key={key}&ip={ip}&format=json` and record city-level details
3. Confirm the `countryCode` matches between both responses
4. Use the city-level data for detailed reporting and the country-level data for quick filtering


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
