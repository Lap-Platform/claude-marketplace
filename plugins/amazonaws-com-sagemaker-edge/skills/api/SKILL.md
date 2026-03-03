---
name: amazon-sagemaker-edge-manager
description: "Amazon Sagemaker Edge Manager API skill. Use when working with Amazon Sagemaker Edge Manager for GetDeployments, GetDeviceRegistration, SendHeartbeat. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Sagemaker Edge Manager
API version: 2020-09-23

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /GetDeployments -- create first GetDeployments

## Endpoints

3 endpoints across 3 groups. See references/api-spec.lap for full details.

### GetDeployments
| Method | Path | Description |
|--------|------|-------------|
| POST | /GetDeployments | Use to get the active deployments from a device. |

### GetDeviceRegistration
| Method | Path | Description |
|--------|------|-------------|
| POST | /GetDeviceRegistration | Use to check if a device is registered with SageMaker Edge Manager. |

### SendHeartbeat
| Method | Path | Description |
|--------|------|-------------|
| POST | /SendHeartbeat | Use to get the current status of devices registered on SageMaker Edge Manager. |

## Enhanced Skill Content
## Question Mapping

- "What models are deployed to my edge device?" -> POST /GetDeployments
- "List all deployments for a specific device fleet" -> POST /GetDeployments
- "Is my edge device registered?" -> POST /GetDeviceRegistration
- "How long is my device registration cached?" -> POST /GetDeviceRegistration
- "Get the registration status for a device by name" -> POST /GetDeviceRegistration
- "Send a heartbeat from my edge device" -> POST /SendHeartbeat
- "Report model metrics from an edge device" -> POST /SendHeartbeat
- "Update the agent version for a device" -> POST /SendHeartbeat
- "Report a deployment result back to SageMaker" -> POST /SendHeartbeat
- "Check if a device still has active deployments" -> POST /GetDeployments
- "Register a device and then start sending heartbeats" -> POST /GetDeviceRegistration + POST /SendHeartbeat
- "Verify deployment landed on a device and report status" -> POST /GetDeployments + POST /SendHeartbeat
- "What agent metrics can I send with a heartbeat?" -> POST /SendHeartbeat
- "Refresh device registration before cache expires" -> POST /GetDeviceRegistration

## Response Tips

- **GetDeployments**: `Deployments` array may be null/empty when no models are deployed; each `EdgeDeployment` contains model and config details -- iterate the list to inspect per-model status.
- **GetDeviceRegistration**: `DeviceRegistration` and `CacheTTL` are both optional strings; a null registration means the device is not registered. Use `CacheTTL` to schedule re-registration calls and avoid unnecessary requests.
- **SendHeartbeat**: Returns no meaningful body on success (200). Treat any non-200 as a failure; the value is in the side effect, not the response payload.

## Anomaly Flags

- **Null DeviceRegistration**: Surface immediately when `GetDeviceRegistration` returns null -- the device is unregistered and heartbeats will likely fail.
- **CacheTTL expiring soon**: If `CacheTTL` is present and near expiration, proactively suggest re-registering the device.
- **Empty Deployments array**: Flag when `GetDeployments` returns null or an empty list -- may indicate a fleet misconfiguration or a device that was removed from a deployment group.
- **SendHeartbeat non-200 responses**: Any error here means the device is going dark from the service's perspective. Surface 403 (SigV4 credential issues) and 404 (unknown device/fleet) distinctly.
- **DeploymentResult in heartbeat**: When a `DeploymentResult` indicates failure, flag it -- this means a model deployment to the edge device did not succeed.
- **AWS SigV4 auth errors (403)**: Often caused by clock skew on edge devices or expired credentials. Surface with a hint to check device time sync and IAM role validity.

## Playbook

### 1. Register and Monitor a New Edge Device

1. Call `POST /GetDeviceRegistration` with `DeviceName` and `DeviceFleetName` to register the device.
2. Store the `CacheTTL` value to know when to re-register.
3. Call `POST /SendHeartbeat` with `AgentVersion`, `DeviceName`, and `DeviceFleetName` to confirm connectivity.
4. Set up a recurring heartbeat on an interval shorter than the `CacheTTL`.

### 2. Check and Report Deployment Status

1. Call `POST /GetDeployments` with `DeviceName` and `DeviceFleetName` to retrieve current deployments.
2. Inspect the `Deployments` array for each `EdgeDeployment` and its status.
3. After loading/applying models locally, call `POST /SendHeartbeat` with a `DeploymentResult` to report success or failure back to SageMaker.

### 3. Continuous Device Health Loop

1. Call `POST /GetDeviceRegistration` to ensure registration is valid; re-register if `CacheTTL` has expired.
2. Collect local agent and model metrics.
3. Call `POST /SendHeartbeat` with `AgentMetrics` and `Models` arrays populated with current telemetry.
4. Repeat on a fixed interval (e.g., every 5 minutes), re-checking registration periodically based on `CacheTTL`.

### 4. Diagnose a Silent Device

1. Call `POST /GetDeviceRegistration` to check if the device is still registered. If null, re-register it.
2. Call `POST /GetDeployments` to verify the device has expected deployments assigned.
3. Attempt `POST /SendHeartbeat` with minimal required fields to test connectivity.
4. If any call returns 403, check AWS SigV4 credentials and device clock synchronization.
5. If calls succeed but the device appears offline in the console, check that heartbeat interval is frequent enough.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
