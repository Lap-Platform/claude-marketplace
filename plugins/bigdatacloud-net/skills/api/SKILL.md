---
name: ip-geolocation-api
description: "IP Geolocation API skill. Use when working with IP Geolocation for data. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# IP Geolocation API

## Auth
ApiKey key in query

## Base URL
https://api-bdc.net

## Setup
1. Set your API key in the appropriate header
2. GET /data/ip-geolocation -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### data
| Method | Path | Description |
|--------|------|-------------|
| GET | /data/ip-geolocation | IP Geolocation API |
| GET | /data/ip-geolocation-with-confidence | IP Geolocation with Confidence Area API |
| GET | /data/ip-geolocation-full | IP Geolocation with Confidence Area and Hazard Report API |

## Enhanced Skill Content
## Question Mapping

- "Where is this IP address located?" -> GET /data/ip-geolocation
- "What country does IP 8.8.8.8 belong to?" -> GET /data/ip-geolocation
- "What timezone is this IP in?" -> GET /data/ip-geolocation
- "Is this IP a VPN or proxy?" -> GET /data/ip-geolocation-full
- "Is this IP on any spam blacklists?" -> GET /data/ip-geolocation-full
- "What is the confidence level for this IP's geolocation?" -> GET /data/ip-geolocation-with-confidence
- "Get the latitude and longitude for an IP address" -> GET /data/ip-geolocation
- "What ISP or carrier owns this IP?" -> GET /data/ip-geolocation
- "Is this IP a known Tor exit node?" -> GET /data/ip-geolocation-full
- "What currency does the country of this IP use?" -> GET /data/ip-geolocation
- "Get the BGP prefix and network details for an IP" -> GET /data/ip-geolocation
- "What is the local time at this IP's location?" -> GET /data/ip-geolocation
- "Is this IP address a bogon (non-routable)?" -> GET /data/ip-geolocation-full
- "Get full security threat assessment and hosting likelihood for an IP" -> GET /data/ip-geolocation-full
- "Look up geolocation with results in French/Spanish/etc.?" -> GET /data/ip-geolocation (set `localityLanguage` to desired locale code)

## Response Tips

- **All endpoints**: Responses are flat objects (no pagination). The top-level `ip` field echoes back the queried address -- verify it matches your request. Nested maps like `country`, `location`, and `network` are always present but inner fields may be empty strings or zero for unknown IPs.
- **Location data**: `location.localityInfo.administrative` and `informative` are arrays of maps ordered by geographic hierarchy (continent down to locality). Check array length before indexing.
- **Security/threat fields** (`ip-geolocation-full` only): `hazardReport` contains boolean flags and an integer `hostingLikelihood` (0-100). The `securityThreat` field is a string summary -- treat empty string as "no known threat."
- **Confidence** (`with-confidence` and `full`): `confidence` is a string label (not numeric). `confidenceArea` is an array of coordinate maps defining a polygon -- may be empty for low-confidence results.
- **Errors**: Invalid or missing `key` returns 401/403. Malformed IPs typically return 200 with empty/default fields rather than 4xx -- always check `isReachableGlobally` to confirm the IP resolved.

## Anomaly Flags

- **Bogon IP detected**: Surface when `network.isBogon` is `true` -- the IP is non-routable and geolocation data will be meaningless.
- **Unreachable IP**: Flag when `isReachableGlobally` is `false` -- results are likely stale or inferred.
- **Security threats**: Proactively warn when any of `isKnownAsTorServer`, `isKnownAsVpn`, `isKnownAsProxy` are `true` in `hazardReport`.
- **Blacklist hits**: Alert when any Spamhaus or blocklist flags (`isSpamhausDrop`, `isSpamhausEdrop`, `isBlacklistedUceprotect`, `isBlacklistedBlocklistDe`) are `true`.
- **High hosting likelihood**: Flag when `hazardReport.hostingLikelihood` exceeds 80 -- strong indicator the IP belongs to a data center, not an end user.
- **iCloud Private Relay**: Surface `iCloudPrivateRelay: true` -- geolocation will reflect Apple's relay region, not the user's actual location.
- **Empty confidence area**: Warn when `confidenceArea` is an empty array -- the provider could not establish a geographic confidence polygon.
- **Stale data**: Check `lastUpdated` and flag if it is more than 30 days old.

## Playbook

### 1. Basic IP Geolocation Lookup

1. Call `GET /data/ip-geolocation?ip={address}&localityLanguage=en&key={apiKey}`.
2. Read `country.name` and `location.city` for the human-readable location.
3. Use `location.latitude` and `location.longitude` for map plotting.
4. Check `location.timeZone.ianaTimeId` to convert timestamps to the IP's local time.

### 2. Security Threat Assessment for an IP

1. Call `GET /data/ip-geolocation-full?ip={address}&localityLanguage=en&key={apiKey}`.
2. Inspect `securityThreat` for a summary threat label.
3. Iterate over `hazardReport` boolean fields to build a threat profile (VPN, Tor, proxy, blacklists).
4. Check `hazardReport.hostingLikelihood` -- values above 50 suggest a hosted/cloud IP.
5. Cross-reference `network.isBogon` and `isReachableGlobally` to rule out non-routable addresses before acting on threat data.

### 3. Geolocation with Confidence Verification

1. Call `GET /data/ip-geolocation-with-confidence?ip={address}&localityLanguage=en&key={apiKey}`.
2. Read the `confidence` string to gauge result reliability.
3. If `confidenceArea` is non-empty, parse the coordinate polygon to determine the geographic bounds of the estimate.
4. For low confidence, consider falling back to country-level data only (`country.name`) rather than city-level.

### 4. Multi-IP Batch Analysis

1. Prepare a list of target IPs.
2. For each IP, call `GET /data/ip-geolocation?ip={ip}&localityLanguage=en&key={apiKey}`.
3. Aggregate results by `country.isoAlpha2` or `location.continentCode` to build geographic distribution.
4. Flag any IPs where `isReachableGlobally` is `false` or `network.isBogon` is `true` as unresolvable.
5. Export the aggregated country/city counts for reporting.

### 5. Localized Geolocation for Multilingual Applications

1. Determine the user's preferred language (e.g., `fr`, `de`, `ja`).
2. Call `GET /data/ip-geolocation?ip={address}&localityLanguage={langCode}&key={apiKey}`.
3. Read `country.name`, `location.city`, and `location.localityName` -- these will be returned in the requested language when available.
4. Fall back to `en` if the response returns empty locality names for the requested language.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
