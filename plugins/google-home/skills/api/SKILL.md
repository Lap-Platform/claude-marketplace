---
name: google-home
description: "Google Home API skill. Use when working with Google Home for supported_timezones, get_app_device_id, supported_locales. Covers 30 endpoints."
version: 1.0.0
generator: lapsh
---

# Google Home
API version: 2.0

## Auth
ApiKey cast-local-authorization-token in header

## Base URL
http://example.com/setup

## Setup
1. Set your API key in the appropriate header
2. GET /supported_timezones -- verify access
3. POST /get_app_device_id -- create first get_app_device_id

## Endpoints

30 endpoints across 18 groups. See references/api-spec.lap for full details.

### supported_timezones
| Method | Path | Description |
|--------|------|-------------|
| GET | /supported_timezones | Timezones |

### get_app_device_id
| Method | Path | Description |
|--------|------|-------------|
| POST | /get_app_device_id | App Device ID |

### supported_locales
| Method | Path | Description |
|--------|------|-------------|
| GET | /supported_locales | Locales |

### assistant
| Method | Path | Description |
|--------|------|-------------|
| POST | /assistant/check_ready_status | Check Ready Status |
| POST | /assistant/set_night_mode_params | Night Mode settings |
| GET | /assistant/alarms | Get Alarms and Timers |
| POST | /assistant/alarms/delete | Delete Alarms and Timers |
| POST | /assistant/notifications | Do Not Disturb |
| POST | /assistant/alarms/volume | Alarm Volume |
| POST | /assistant/a11y_mode | Accessibility |

### offer
| Method | Path | Description |
|--------|------|-------------|
| GET | /offer | Offer |

### eureka_info
| Method | Path | Description |
|--------|------|-------------|
| GET | /eureka_info | Eureka Info |

### test_internet_download_speed
| Method | Path | Description |
|--------|------|-------------|
| POST | /test_internet_download_speed | Test Internet Download Speed |

### reboot
| Method | Path | Description |
|--------|------|-------------|
| POST | /reboot | Reboot and Factory Reset |

### set_eureka_info
| Method | Path | Description |
|--------|------|-------------|
| POST | /set_eureka_info | Set Eureka Info |

### user_eq
| Method | Path | Description |
|--------|------|-------------|
| POST | /user_eq/set_equalizer | Set Equalizer Values |

### bluetooth
| Method | Path | Description |
|--------|------|-------------|
| GET | /bluetooth/scan_results | Get Scan Results |
| POST | /bluetooth/bond | Forget paired device |
| POST | /bluetooth/discovery | Change Discoverability |
| POST | /bluetooth/connect | Pair with Speaker |
| GET | /bluetooth/status | Status |
| POST | /bluetooth/scan | Scan for devices |
| GET | /bluetooth/get_bonded | Get Paired Devices |

### connect_wifi
| Method | Path | Description |
|--------|------|-------------|
| POST | /connect_wifi | Connect to Wi-Fi Network |

### scan_wifi
| Method | Path | Description |
|--------|------|-------------|
| POST | /scan_wifi | Scan for Networks |

### configured_networks
| Method | Path | Description |
|--------|------|-------------|
| GET | /configured_networks | Get Saved Networks |

### forget_wifi
| Method | Path | Description |
|--------|------|-------------|
| POST | /forget_wifi | Forget Wi-Fi Network |

### scan_results
| Method | Path | Description |
|--------|------|-------------|
| GET | /scan_results | Get Wi-Fi Scan Results |

### NOTICE.html.gz
| Method | Path | Description |
|--------|------|-------------|
| GET | /NOTICE.html.gz | Legal Notice |

### icon.png
| Method | Path | Description |
|--------|------|-------------|
| GET | /icon.png | Chromecast Icon |

## Enhanced Skill Content
## Question Mapping

- "What timezones does my Google Home support?" -> GET /supported_timezones
- "What languages/locales are available on my device?" -> GET /supported_locales
- "How do I get detailed info about my Chromecast/Google Home device?" -> GET /eureka_info
- "What's the current Bluetooth status and connected devices?" -> GET /bluetooth/status
- "Which Wi-Fi networks has my device saved?" -> GET /configured_networks
- "What Wi-Fi networks are available nearby?" -> GET /scan_results
- "How do I reboot my Google Home?" -> POST /reboot
- "How do I connect my device to a new Wi-Fi network?" -> POST /connect_wifi
- "How do I pair a Bluetooth device?" -> POST /bluetooth/bond
- "How do I set up night mode with a schedule?" -> POST /assistant/set_night_mode_params
- "What alarms and timers are currently set?" -> GET /assistant/alarms
- "How do I delete an alarm or timer?" -> POST /assistant/alarms/delete
- "How do I adjust the equalizer (bass/treble)?" -> POST /user_eq/set_equalizer
- "How do I rename my device or change its settings?" -> POST /set_eureka_info
- "How do I test my device's internet speed?" -> POST /test_internet_download_speed

## Response Tips

- **Device info** (`/eureka_info`): Response is deeply nested with maps inside maps -- access capabilities via `device_info.capabilities`, network via `net`, and audio via `audio`. The `sign` block contains certificate data for device verification.
- **Bluetooth** (`/bluetooth/*`): `scan_results` and `get_bonded` return bare lists. `status` nests connected devices as `[map]` -- iterate to find specific devices by `mac_address`.
- **Wi-Fi** (`/connect_wifi`, `/scan_wifi`, `/scan_results`): Connect requires encrypted password (`enc_passwd`) plus WPA auth/cipher integers -- obtain these from scan results first. Forget requires the `wpa_id` from `/configured_networks`.
- **Alarms** (`/assistant/alarms`): Returns separate `alarm` and `timer` arrays of maps. Deletion requires collecting `ids` from these arrays.
- **Night mode** (`/assistant/set_night_mode_params`): The `windows` array uses `days` as integer arrays (0=Sunday through 6=Saturday), `start_hour` as 24h int, and `length_hours` for duration.
- **General**: Most POST endpoints return 200 with empty or minimal bodies on success. A non-200 status or missing expected fields indicates failure. `/get_app_device_id` is the only endpoint explicitly declaring 404 errors.

## Anomaly Flags

- **Auth token missing or rejected**: All requests require `cast-local-authorization-token` in the header. Surface immediately if any call returns 401/403 -- the token may have rotated after a device reboot.
- **Device offline**: If `/eureka_info` returns `net.online: false` or `net.ethernet_connected: false` with no `ip_address`, flag that the device has lost network connectivity.
- **Wi-Fi signal degradation**: If `wifi.signal_level` in eureka_info drops significantly or `wifi.noise_level` is high, surface a warning about potential connectivity issues.
- **Bluetooth connection failures**: If `/bluetooth/status` shows devices in `connecting_devices` but none in `connected_devices` after a bond/connect attempt, flag the pairing as potentially stuck.
- **Night mode misconfiguration**: If `set_night_mode_params` is called with `enabled: true` but an empty `windows` array, warn that night mode will have no active schedule.
- **Speed test anomalies**: If `test_internet_download_speed` returns a very low `bytes_received` relative to `time_for_data_fetch`, surface a potential bandwidth issue.
- **Setup state incomplete**: If `eureka_info` returns `setup.setup_state` other than the expected complete value or `setup.tos_accepted: false`, flag that device setup may be incomplete.

## Playbook

### 1. Connect Device to a New Wi-Fi Network

1. Call `POST /scan_wifi` to trigger a fresh Wi-Fi scan.
2. Call `GET /scan_results` to retrieve available networks.
3. Identify the target network and note its `bssid`, `signal_level`, `ssid`, `wpa_auth`, and `wpa_cipher`.
4. Call `POST /connect_wifi` with the network details and the encrypted password.
5. Verify by calling `GET /eureka_info` and checking `net.online` and `wifi.ssid`.

### 2. Pair and Connect a Bluetooth Speaker

1. Call `POST /bluetooth/scan` with `{"enable": true, "clear_results": true, "timeout": 30}` to scan for nearby devices.
2. Call `GET /bluetooth/scan_results` to list discovered devices and find the target `mac_address`.
3. Call `POST /bluetooth/bond` with `{"mac_address": "<addr>", "bond": true}` to pair.
4. Call `POST /bluetooth/connect` with `{"mac_address": "<addr>", "connect": true, "profile": 2}` to establish the audio connection.
5. Confirm via `GET /bluetooth/status` -- the device should appear in `connected_devices`.

### 3. Configure Night Mode Schedule

1. Call `GET /eureka_info` to check current `night_mode_params` and device capabilities.
2. Call `POST /assistant/set_night_mode_params` with the desired schedule:
   - Set `enabled: true`, `do_not_disturb: true`
   - Define `windows` with days (e.g., `[0,1,2,3,4,5,6]` for every day), `start_hour` (e.g., `22` for 10 PM), and `length_hours` (e.g., `8`).
   - Set `led_brightness` and `volume` to reduced levels (e.g., `0.2` and `0.3`).
3. Verify the response mirrors your settings.

### 4. Manage Alarms and Timers

1. Call `GET /assistant/alarms` to retrieve all current alarms and timers.
2. Identify the alarm/timer IDs you want to manage from the `alarm` and `timer` arrays.
3. To delete, call `POST /assistant/alarms/delete` with `{"ids": ["<id1>", "<id2>"]}`.
4. To adjust alarm volume, call `POST /assistant/alarms/volume` with `{"volume": 5}` (integer scale).
5. Confirm deletion by calling `GET /assistant/alarms` again.

### 5. Full Device Diagnostics

1. Call `GET /eureka_info` with appropriate params to get complete device state.
2. Check `net.online` and `wifi.signal_level` for connectivity health.
3. Call `POST /test_internet_download_speed` with a known test URL to benchmark bandwidth.
4. Call `GET /bluetooth/status` to verify Bluetooth subsystem state.
5. Review `device_info.capabilities` to confirm which features are available.
6. If issues are found, call `POST /reboot` with `{"params": "now"}` as a last resort.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
