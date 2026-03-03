---
name: hardware-sentry-truesight-presentation-server-rest-api
description: "Hardware Sentry TrueSight Presentation Server REST API skill. Use when working with Hardware Sentry TrueSight Presentation Server REST for hardware. Covers 23 endpoints."
version: 1.0.0
generator: lapsh
---

# Hardware Sentry TrueSight Presentation Server REST API
API version: 11.1.00

## Auth
ApiKey Cookie in header

## Base URL
/tsws/10.0/api/

## Setup
1. Set your API key in the appropriate header
2. GET /hardware/applications -- verify access
3. POST /hardware/actions/{deviceId}/collect-now -- create first collect-now

## Endpoints

23 endpoints across 1 groups. See references/api-spec.lap for full details.

### hardware
| Method | Path | Description |
|--------|------|-------------|
| POST | /hardware/actions/{deviceId}/collect-now | Triggers a new collect on a specific device. |
| POST | /hardware/actions/{deviceId}/rediscover | Triggers a new discovery on a specific device. |
| POST | /hardware/actions/{deviceId}/reinitialize | Sends a 'Reinitialize KM' command. |
| POST | /hardware/actions/{deviceId}/remove | Removes a specific instance from the monitoring environment. |
| POST | /hardware/actions/{deviceId}/reset-error-count | Resets the Error Count parameter. |
| GET | /hardware/applications | Gets summarized information about all monitored applications. |
| GET | /hardware/applications/{applicationId} | Gets detailed information for a specific application. |
| GET | /hardware/device-monitors/{deviceId} | Gets the Monitors for a specific device. |
| GET | /hardware/devices | Gets summarized information about all monitored devices. |
| GET | /hardware/devices-summary | Gets overall information for all devices. |
| GET | /hardware/devices/{deviceId} | Gets detailed information about a specific device. |
| GET | /hardware/devices/{deviceId}/agent | Gets detailed information about an Agent. |
| GET | /hardware/devices/{deviceId}/agent-devices | Gets a list of all the devices monitored by an Agent. |
| GET | /hardware/devices/{deviceId}/parameter-history | Gets data history for a parameter of a specific device over a given period. |
| GET | /hardware/energy-usage/{deviceId} | Gets the energy usage for a specific device and a given period. |
| GET | /hardware/groups | Gets all group summaries. |
| GET | /hardware/groups/{groupId} | Gets detailed information about a specific group. |
| PUT | /hardware/groups/{groupId} | Updates the values of the energy footprint parameter for a specific group. |
| GET | /hardware/heating-margin-devices | Gets the heating margin values for each monitored device, when available. |
| GET | /hardware/history | Gets historical data for a specific group, application or service. |
| GET | /hardware/search-devices | Searches devices by name, model, manufacturer or serial number. |
| GET | /hardware/services | Gets summarized information about all monitored services. |
| GET | /hardware/services/{serviceId} | Gets detailed information about a specific service. |

## Enhanced Skill Content
## Question Mapping

- "What hardware devices are being monitored?" -> GET /hardware/devices
- "Show me details for device 42" -> GET /hardware/devices/{deviceId}
- "How many devices are healthy vs unhealthy?" -> GET /hardware/devices-summary
- "Search for a device by hostname or IP" -> GET /hardware/search-devices
- "What monitors are running on device 15?" -> GET /hardware/device-monitors/{deviceId}
- "Which agent manages device 7?" -> GET /hardware/devices/{deviceId}/agent
- "What other devices share the same agent as device 7?" -> GET /hardware/devices/{deviceId}/agent-devices
- "Show CPU temperature history for device 3 over the last week" -> GET /hardware/devices/{deviceId}/parameter-history
- "How much energy has device 10 consumed this month?" -> GET /hardware/energy-usage/{deviceId}
- "List all device groups" -> GET /hardware/groups
- "Update energy cost for group 'DataCenter-East'" -> PUT /hardware/groups/{groupId}
- "Which devices are at risk of overheating?" -> GET /hardware/heating-margin-devices
- "Force an immediate data collection on device 5" -> POST /hardware/actions/{deviceId}/collect-now
- "Rediscover hardware on device 12 after a component swap" -> POST /hardware/actions/{deviceId}/rediscover
- "Factory-reset monitoring config on device 9" -> POST /hardware/actions/{deviceId}/reinitialize

## Response Tips

- **Device listings** (`/devices`, `/groups`, `/applications`, `/services`, `/search-devices`, `/heating-margin-devices`): Paginated with `page` (0-indexed) and `limit` (default 100). Always check if result count equals `limit` to know if more pages exist. Sortable via `sort` and `direction`.
- **Single resource** (`/devices/{id}`, `/groups/{id}`, `/applications/{id}`, `/services/{id}`): Returns 404 when the ID does not exist; treat this as "not found", not a server error.
- **Action endpoints** (`/actions/{deviceId}/*`): Return 200 on success with minimal body. A 403 means the API key lacks write permissions. A 500 typically means the agent managing that device is unreachable.
- **Parameter history** (`/parameter-history`): `from`/`to` are epoch milliseconds (int64). Omitting them returns the default server-side range. Results are time-series arrays -- watch for gaps indicating agent downtime.
- **Energy usage** (`/energy-usage`): The `rollPeriod` controls the time window and `basis` controls granularity. Mismatched combinations (e.g., HOURLY basis with ONE_YEAR period) may return very large payloads.
- **Summary** (`/devices-summary`): Single aggregate object, not paginated. Use this for dashboards instead of fetching all devices.

## Anomaly Flags

- **500 errors on action endpoints**: Surface immediately -- likely indicates the monitoring agent is offline or the device is unreachable. Recommend checking `/devices/{deviceId}/agent` status.
- **Heating margin devices with `covered=false`**: Proactively warn when uncovered devices exist -- these lack thermal protection monitoring.
- **Device count drift**: If `/devices-summary` totals diverge significantly from `/devices` paginated counts, flag a potential sync issue between the presentation server and agents.
- **Empty parameter history**: When `/parameter-history` returns no data for a known-good monitor, flag that the monitor may be paused or the agent disconnected.
- **Energy cost or CO2 values at zero**: After a `PUT /groups/{groupId}` update, verify the values persisted. Zero values on groups with active devices suggest misconfiguration.
- **403 on write operations**: Surface as a permissions issue rather than retrying. The API key may need elevated privileges or the session cookie may have expired.
- **Reinitialize with all reset flags**: Warn before executing -- resetting thresholds, alert actions, and debug mode simultaneously is a destructive operation that can silence active alerts.

## Playbook

### 1. Investigate a device showing errors

1. GET `/hardware/devices/{deviceId}` to confirm device status and identify its group/application.
2. GET `/hardware/device-monitors/{deviceId}` to list all monitors and spot which ones report errors.
3. GET `/hardware/devices/{deviceId}/parameter-history` with `monitorType` and `parameterName` from the failing monitor to review recent trends.
4. If the error is transient, POST `/hardware/actions/{deviceId}/reset-error-count` with the specific `monitorClass` and `monitorSid` to clear the counter.
5. If the error persists, POST `/hardware/actions/{deviceId}/collect-now` to force a fresh collection and re-check.

### 2. Onboard a replaced hardware component

1. POST `/hardware/actions/{deviceId}/rediscover` to trigger a full hardware rediscovery on the device.
2. Wait 30-60 seconds for the agent to complete the scan.
3. GET `/hardware/device-monitors/{deviceId}` to verify new monitors appeared for the replaced component.
4. If stale monitors remain, POST `/hardware/actions/{deviceId}/remove` with the old `monitorClass` and `monitorSid` to clean them up.

### 3. Generate an energy consumption report for a group

1. GET `/hardware/groups` to list all groups and find the target `groupId`.
2. GET `/hardware/groups/{groupId}` to confirm current `energyCost` and `co2Emission` rates. Update with PUT if rates have changed.
3. GET `/hardware/devices?groupId={groupId}` to enumerate all devices in the group.
4. For each device, GET `/hardware/energy-usage/{deviceId}?rollPeriod=ONE_MONTH&basis=DAILY` to collect daily consumption data.
5. Aggregate the results to produce total kWh and CO2 figures for the group.

### 4. Search and triage devices across organizational boundaries

1. GET `/hardware/search-devices?searchTerms={keyword}` to find devices matching a hostname, IP, or label.
2. For each result, GET `/hardware/devices/{deviceId}` to determine which group, application, and service the device belongs to.
3. GET `/hardware/heating-margin-devices?covered=false&groupId={groupId}` to check if any matched devices lack thermal coverage.
4. GET `/hardware/history?groupId={groupId}` to review historical health trends for the affected group.

### 5. Reset a misbehaving device to clean monitoring state

1. GET `/hardware/device-monitors/{deviceId}` to document current monitor state before the reset.
2. GET `/hardware/devices/{deviceId}/agent` to confirm the agent is online and responsive.
3. POST `/hardware/actions/{deviceId}/reinitialize` with selective reset flags (start with `resetThresholds=1` and `resetDebugMode=1` to minimize disruption).
4. POST `/hardware/actions/{deviceId}/collect-now` with the primary `monitorClass` to force an immediate data refresh.
5. GET `/hardware/device-monitors/{deviceId}` again to verify monitors re-initialized correctly.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
