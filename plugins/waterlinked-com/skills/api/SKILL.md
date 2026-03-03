---
name: the-water-linked-underwater-gps-api
description: "The Water Linked Underwater GPS API skill. Use when working with The Water Linked Underwater GPS for api. Covers 38 endpoints."
version: 1.0.0
generator: lapsh
---

# The Water Linked Underwater GPS API

## Auth
No authentication required.

## Base URL
http://demo.waterlinked.com

## Setup
1. No auth setup needed
2. GET /api/ -- verify access
3. POST /api/v1/about/factoryreset -- create first factoryreset

## Endpoints

38 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/ | ApiVersion about |
| GET | /api/v1/about | Get about |
| POST | /api/v1/about/factoryreset | FactoryReset about |
| GET | /api/v1/about/led | LED about |
| GET | /api/v1/about/status | Status about |
| GET | /api/v1/about/temperature | Temperature about |
| GET | /api/v1/config/antenna | GetAntennaConfig config |
| PUT | /api/v1/config/antenna | ModifyAntennaConfig config |
| GET | /api/v1/config/generic | Get config |
| PUT | /api/v1/config/generic | Modify config |
| GET | /api/v1/config/ip | GetIP config |
| PUT | /api/v1/config/ip | ModifyIP config |
| GET | /api/v1/config/receivers/ | ListReceiver config |
| GET | /api/v1/config/receivers/{ID} | ShowReceiver config |
| PUT | /api/v1/config/receivers/{ID} | ModifyReceiver config |
| GET | /api/v1/config/wifi | GetWIFI config |
| PUT | /api/v1/config/wifi | ModifyWIFI config |
| PUT | /api/v1/external/depth | SetDepth external |
| GET | /api/v1/external/imu | GetVehicleIMU external |
| PUT | /api/v1/external/imu | SetVehicleIMU external |
| PUT | /api/v1/external/master | SetMaster external |
| GET | /api/v1/external/orientation | GetOrientation external |
| PUT | /api/v1/external/orientation | SetOrientation external |
| GET | /api/v1/imu/calibrate | Get imu |
| POST | /api/v1/imu/calibrate | Calibrate imu |
| POST | /api/v1/imu/resetgyros | ResetGyro imu |
| POST | /api/v1/imu/setnorth | SetNorth imu |
| GET | /api/v1/poi/ | List poi |
| POST | /api/v1/poi/ | Create poi |
| GET | /api/v1/poi/{ID} | Show poi |
| DELETE | /api/v1/poi/{ID} | Delete poi |
| PATCH | /api/v1/poi/{ID} | Update poi |
| GET | /api/v1/position/acoustic/filtered | AcousticFiltered position |
| GET | /api/v1/position/acoustic/raw | AcousticRaw position |
| GET | /api/v1/position/global | Get position |
| GET | /api/v1/position/master | GetMaster position |
| GET | /api/v1/status_report/ | Get status_report |
| GET | /api/v1/warnings/ | Get warnings |

## Enhanced Skill Content
## Question Mapping

- "What version or info does the Water Linked system report?" -> GET /api/v1/about
- "What is the current status of the underwater GPS?" -> GET /api/v1/about/status
- "What is the system temperature?" -> GET /api/v1/about/temperature
- "How do I factory reset the device?" -> POST /api/v1/about/factoryreset
- "Where is the locator right now in global coordinates?" -> GET /api/v1/position/global
- "What is the raw acoustic position of the locator?" -> GET /api/v1/position/acoustic/raw
- "What is the filtered acoustic position?" -> GET /api/v1/position/acoustic/filtered
- "How do I configure the antenna placement?" -> PUT /api/v1/config/antenna
- "How do I set the depth of the locator externally?" -> PUT /api/v1/external/depth
- "How do I add a point of interest?" -> POST /api/v1/poi/
- "How do I delete a saved point of interest?" -> DELETE /api/v1/poi/{ID}
- "What receivers are connected and how are they configured?" -> GET /api/v1/config/receivers/
- "How do I calibrate the IMU?" -> POST /api/v1/imu/calibrate
- "Are there any active warnings on the system?" -> GET /api/v1/warnings/
- "How do I change the Wi-Fi settings?" -> PUT /api/v1/config/wifi

## Response Tips

- **About/Status endpoints**: Return flat objects with system metadata; 200 means healthy, watch for 503 (service unavailable during boot or reset).
- **Position endpoints**: Return coordinate objects (x/y/z or lat/lon); a 500 means the positioning engine has no valid fix -- retry after ensuring receivers are online.
- **Config endpoints**: GET returns current config as a map; PUT expects the full config object back (not a partial patch), returns 200 on success or 400 for validation errors.
- **Receiver endpoints**: GET /{ID} returns a single receiver object; PUT returns 204 (no body) on success -- check status code, not response body.
- **POI endpoints**: POST returns 201 with the created resource; PATCH and DELETE return 204 (no body); 403 on POST means the POI limit has been reached.
- **IMU endpoints**: 408 means calibration timed out; 409 means a conflicting operation is already in progress -- wait and retry.
- **External sensor endpoints**: Used to feed external data (depth, orientation, IMU, master position) into the system; 500 usually means the system rejected the input format.

## Anomaly Flags

- **503 on config writes or factory reset**: System is busy or rebooting -- surface this as "device unavailable, retry shortly."
- **500 on position endpoints**: No acoustic fix available -- alert the user that receivers may be misaligned or the locator is out of range.
- **408 on IMU calibration**: Calibration timed out -- flag that the device may not be in the correct orientation or environment for calibration.
- **409 on IMU operations**: Another calibration or gyro reset is already running -- warn before retrying.
- **403 on POI creation**: POI storage limit reached -- proactively suggest deleting unused POIs before retrying.
- **404 on receiver or POI by ID**: The requested resource does not exist -- surface as a possible ID mismatch and list available IDs.
- **Repeated 500s on /api/v1/warnings/**: The warning subsystem itself is failing -- escalate as a potential hardware issue.
- **Temperature reading outside normal range**: If /about/temperature returns extreme values, flag possible overheating or sensor fault.

## Playbook

### 1. Initial System Setup

1. GET /api/v1/about -- confirm device firmware version and identity.
2. GET /api/v1/about/status -- verify the system is operational.
3. GET /api/v1/config/generic -- review current generic configuration.
4. PUT /api/v1/config/ip -- set the desired network configuration.
5. PUT /api/v1/config/wifi -- configure Wi-Fi access if needed.
6. PUT /api/v1/config/antenna -- set receiver antenna positions for your setup.
7. GET /api/v1/config/receivers/ -- confirm all receivers are detected.

### 2. Real-Time Locator Tracking

1. PUT /api/v1/external/depth -- send current depth from an external depth sensor.
2. GET /api/v1/position/acoustic/raw -- poll raw acoustic position to verify signal.
3. GET /api/v1/position/acoustic/filtered -- read the filtered (smoothed) position.
4. GET /api/v1/position/global -- retrieve lat/lon/depth in global coordinates.
5. GET /api/v1/warnings/ -- check for any positioning warnings after each cycle.

### 3. IMU Calibration Workflow

1. GET /api/v1/imu/calibrate -- check current calibration status.
2. POST /api/v1/imu/calibrate -- start calibration (handle 408 timeout or 409 conflict).
3. POST /api/v1/imu/setnorth -- set the north reference heading after calibration.
4. POST /api/v1/imu/resetgyros -- reset gyro drift if orientation seems off.
5. GET /api/v1/external/orientation -- verify orientation readings are sensible.

### 4. Managing Points of Interest

1. GET /api/v1/poi/ -- list all saved points of interest.
2. POST /api/v1/poi/ -- create a new POI with name and coordinates (watch for 403 if at limit).
3. GET /api/v1/poi/{ID} -- retrieve a specific POI to verify it was saved correctly.
4. PATCH /api/v1/poi/{ID} -- update a POI's name or coordinates.
5. DELETE /api/v1/poi/{ID} -- remove a POI that is no longer needed.

### 5. Diagnostics and Troubleshooting

1. GET /api/v1/about/status -- check overall system health.
2. GET /api/v1/about/temperature -- verify operating temperature is within range.
3. GET /api/v1/about/led -- check LED status for visual diagnostics.
4. GET /api/v1/warnings/ -- review active warnings for specific issues.
5. GET /api/v1/status_report/ -- pull the full status report for detailed diagnostics.
6. POST /api/v1/about/factoryreset -- last resort: factory reset the device (causes reboot, expect 503 temporarily).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
