---
name: amazon-pinpoint
description: "Amazon Pinpoint API skill. Use when working with Amazon Pinpoint for apps, templates, recommenders. Covers 122 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Pinpoint
API version: 2016-12-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /v1/apps -- verify access
3. POST /v1/apps -- create first apps

## Endpoints

122 endpoints across 5 groups. See references/api-spec.lap for full details.

### apps
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/apps | Creates an application. |
| POST | /v1/apps/{application-id}/campaigns | Creates a new campaign for an application or updates the settings of an existing campaign for an application. |
| POST | /v1/apps/{application-id}/jobs/export | Creates an export job for an application. |
| POST | /v1/apps/{application-id}/jobs/import | Creates an import job for an application. |
| POST | /v1/apps/{application-id}/journeys | Creates a journey for an application. |
| POST | /v1/apps/{application-id}/segments | Creates a new segment for an application or updates the configuration, dimension, and other settings for an existing segment that's associated with an application. |
| DELETE | /v1/apps/{application-id}/channels/adm | Disables the ADM channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/channels/apns | Disables the APNs channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/channels/apns_sandbox | Disables the APNs sandbox channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/channels/apns_voip | Disables the APNs VoIP channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/channels/apns_voip_sandbox | Disables the APNs VoIP sandbox channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id} | Deletes an application. |
| DELETE | /v1/apps/{application-id}/channels/baidu | Disables the Baidu channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/campaigns/{campaign-id} | Deletes a campaign from an application. |
| DELETE | /v1/apps/{application-id}/channels/email | Disables the email channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/endpoints/{endpoint-id} | Deletes an endpoint from an application. |
| DELETE | /v1/apps/{application-id}/eventstream | Deletes the event stream for an application. |
| DELETE | /v1/apps/{application-id}/channels/gcm | Disables the GCM channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/journeys/{journey-id} | Deletes a journey from an application. |
| DELETE | /v1/apps/{application-id}/segments/{segment-id} | Deletes a segment from an application. |
| DELETE | /v1/apps/{application-id}/channels/sms | Disables the SMS channel for an application and deletes any existing settings for the channel. |
| DELETE | /v1/apps/{application-id}/users/{user-id} | Deletes all the endpoints that are associated with a specific user ID. |
| DELETE | /v1/apps/{application-id}/channels/voice | Disables the voice channel for an application and deletes any existing settings for the channel. |
| GET | /v1/apps/{application-id}/channels/adm | Retrieves information about the status and settings of the ADM channel for an application. |
| GET | /v1/apps/{application-id}/channels/apns | Retrieves information about the status and settings of the APNs channel for an application. |
| GET | /v1/apps/{application-id}/channels/apns_sandbox | Retrieves information about the status and settings of the APNs sandbox channel for an application. |
| GET | /v1/apps/{application-id}/channels/apns_voip | Retrieves information about the status and settings of the APNs VoIP channel for an application. |
| GET | /v1/apps/{application-id}/channels/apns_voip_sandbox | Retrieves information about the status and settings of the APNs VoIP sandbox channel for an application. |
| GET | /v1/apps/{application-id} | Retrieves information about an application. |
| GET | /v1/apps/{application-id}/kpis/daterange/{kpi-name} | Retrieves (queries) pre-aggregated data for a standard metric that applies to an application. |
| GET | /v1/apps/{application-id}/settings | Retrieves information about the settings for an application. |
| GET | /v1/apps | Retrieves information about all the applications that are associated with your Amazon Pinpoint account. |
| GET | /v1/apps/{application-id}/channels/baidu | Retrieves information about the status and settings of the Baidu channel for an application. |
| GET | /v1/apps/{application-id}/campaigns/{campaign-id} | Retrieves information about the status, configuration, and other settings for a campaign. |
| GET | /v1/apps/{application-id}/campaigns/{campaign-id}/activities | Retrieves information about all the activities for a campaign. |
| GET | /v1/apps/{application-id}/campaigns/{campaign-id}/kpis/daterange/{kpi-name} | Retrieves (queries) pre-aggregated data for a standard metric that applies to a campaign. |
| GET | /v1/apps/{application-id}/campaigns/{campaign-id}/versions/{version} | Retrieves information about the status, configuration, and other settings for a specific version of a campaign. |
| GET | /v1/apps/{application-id}/campaigns/{campaign-id}/versions | Retrieves information about the status, configuration, and other settings for all versions of a campaign. |
| GET | /v1/apps/{application-id}/campaigns | Retrieves information about the status, configuration, and other settings for all the campaigns that are associated with an application. |
| GET | /v1/apps/{application-id}/channels | Retrieves information about the history and status of each channel for an application. |
| GET | /v1/apps/{application-id}/channels/email | Retrieves information about the status and settings of the email channel for an application. |
| GET | /v1/apps/{application-id}/endpoints/{endpoint-id} | Retrieves information about the settings and attributes of a specific endpoint for an application. |
| GET | /v1/apps/{application-id}/eventstream | Retrieves information about the event stream settings for an application. |
| GET | /v1/apps/{application-id}/jobs/export/{job-id} | Retrieves information about the status and settings of a specific export job for an application. |
| GET | /v1/apps/{application-id}/jobs/export | Retrieves information about the status and settings of all the export jobs for an application. |
| GET | /v1/apps/{application-id}/channels/gcm | Retrieves information about the status and settings of the GCM channel for an application. |
| GET | /v1/apps/{application-id}/jobs/import/{job-id} | Retrieves information about the status and settings of a specific import job for an application. |
| GET | /v1/apps/{application-id}/jobs/import | Retrieves information about the status and settings of all the import jobs for an application. |
| GET | /v1/apps/{application-id}/endpoints/{endpoint-id}/inappmessages | Retrieves the in-app messages targeted for the provided endpoint ID. |
| GET | /v1/apps/{application-id}/journeys/{journey-id} | Retrieves information about the status, configuration, and other settings for a journey. |
| GET | /v1/apps/{application-id}/journeys/{journey-id}/kpis/daterange/{kpi-name} | Retrieves (queries) pre-aggregated data for a standard engagement metric that applies to a journey. |
| GET | /v1/apps/{application-id}/journeys/{journey-id}/activities/{journey-activity-id}/execution-metrics | Retrieves (queries) pre-aggregated data for a standard execution metric that applies to a journey activity. |
| GET | /v1/apps/{application-id}/journeys/{journey-id}/execution-metrics | Retrieves (queries) pre-aggregated data for a standard execution metric that applies to a journey. |
| GET | /v1/apps/{application-id}/journeys/{journey-id}/runs/{run-id}/activities/{journey-activity-id}/execution-metrics | Retrieves (queries) pre-aggregated data for a standard run execution metric that applies to a journey activity. |
| GET | /v1/apps/{application-id}/journeys/{journey-id}/runs/{run-id}/execution-metrics | Retrieves (queries) pre-aggregated data for a standard run execution metric that applies to a journey. |
| GET | /v1/apps/{application-id}/journeys/{journey-id}/runs | Provides information about the runs of a journey. |
| GET | /v1/apps/{application-id}/segments/{segment-id} | Retrieves information about the configuration, dimension, and other settings for a specific segment that's associated with an application. |
| GET | /v1/apps/{application-id}/segments/{segment-id}/jobs/export | Retrieves information about the status and settings of the export jobs for a segment. |
| GET | /v1/apps/{application-id}/segments/{segment-id}/jobs/import | Retrieves information about the status and settings of the import jobs for a segment. |
| GET | /v1/apps/{application-id}/segments/{segment-id}/versions/{version} | Retrieves information about the configuration, dimension, and other settings for a specific version of a segment that's associated with an application. |
| GET | /v1/apps/{application-id}/segments/{segment-id}/versions | Retrieves information about the configuration, dimension, and other settings for all the versions of a specific segment that's associated with an application. |
| GET | /v1/apps/{application-id}/segments | Retrieves information about the configuration, dimension, and other settings for all the segments that are associated with an application. |
| GET | /v1/apps/{application-id}/channels/sms | Retrieves information about the status and settings of the SMS channel for an application. |
| GET | /v1/apps/{application-id}/users/{user-id} | Retrieves information about all the endpoints that are associated with a specific user ID. |
| GET | /v1/apps/{application-id}/channels/voice | Retrieves information about the status and settings of the voice channel for an application. |
| GET | /v1/apps/{application-id}/journeys | Retrieves information about the status, configuration, and other settings for all the journeys that are associated with an application. |
| POST | /v1/apps/{application-id}/eventstream | Creates a new event stream for an application or updates the settings of an existing event stream for an application. |
| POST | /v1/apps/{application-id}/events | Creates a new event to record for endpoints, or creates or updates endpoint data that existing events are associated with. |
| PUT | /v1/apps/{application-id}/attributes/{attribute-type} | Removes one or more custom attributes, of the same attribute type, from the application. Existing endpoints still have the attributes but Amazon Pinpoint will stop capturing new or changed values for these attributes. |
| POST | /v1/apps/{application-id}/messages | Creates and sends a direct message. |
| POST | /v1/apps/{application-id}/otp | Send an OTP message |
| POST | /v1/apps/{application-id}/users-messages | Creates and sends a message to a list of users. |
| PUT | /v1/apps/{application-id}/channels/adm | Enables the ADM channel for an application or updates the status and settings of the ADM channel for an application. |
| PUT | /v1/apps/{application-id}/channels/apns | Enables the APNs channel for an application or updates the status and settings of the APNs channel for an application. |
| PUT | /v1/apps/{application-id}/channels/apns_sandbox | Enables the APNs sandbox channel for an application or updates the status and settings of the APNs sandbox channel for an application. |
| PUT | /v1/apps/{application-id}/channels/apns_voip | Enables the APNs VoIP channel for an application or updates the status and settings of the APNs VoIP channel for an application. |
| PUT | /v1/apps/{application-id}/channels/apns_voip_sandbox | Enables the APNs VoIP sandbox channel for an application or updates the status and settings of the APNs VoIP sandbox channel for an application. |
| PUT | /v1/apps/{application-id}/settings | Updates the settings for an application. |
| PUT | /v1/apps/{application-id}/channels/baidu | Enables the Baidu channel for an application or updates the status and settings of the Baidu channel for an application. |
| PUT | /v1/apps/{application-id}/campaigns/{campaign-id} | Updates the configuration and other settings for a campaign. |
| PUT | /v1/apps/{application-id}/channels/email | Enables the email channel for an application or updates the status and settings of the email channel for an application. |
| PUT | /v1/apps/{application-id}/endpoints/{endpoint-id} | Creates a new endpoint for an application or updates the settings and attributes of an existing endpoint for an application. You can also use this operation to define custom attributes for an endpoint. If an update includes one or more values for a custom attribute, Amazon Pinpoint replaces (overwrites) any existing values with the new values. |
| PUT | /v1/apps/{application-id}/endpoints | Creates a new batch of endpoints for an application or updates the settings and attributes of a batch of existing endpoints for an application. You can also use this operation to define custom attributes for a batch of endpoints. If an update includes one or more values for a custom attribute, Amazon Pinpoint replaces (overwrites) any existing values with the new values. |
| PUT | /v1/apps/{application-id}/channels/gcm | Enables the GCM channel for an application or updates the status and settings of the GCM channel for an application. |
| PUT | /v1/apps/{application-id}/journeys/{journey-id} | Updates the configuration and other settings for a journey. |
| PUT | /v1/apps/{application-id}/journeys/{journey-id}/state | Cancels (stops) an active journey. |
| PUT | /v1/apps/{application-id}/segments/{segment-id} | Creates a new segment for an application or updates the configuration, dimension, and other settings for an existing segment that's associated with an application. |
| PUT | /v1/apps/{application-id}/channels/sms | Enables the SMS channel for an application or updates the status and settings of the SMS channel for an application. |
| PUT | /v1/apps/{application-id}/channels/voice | Enables the voice channel for an application or updates the status and settings of the voice channel for an application. |
| POST | /v1/apps/{application-id}/verify-otp | Verify an OTP |

### templates
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/templates/{template-name}/email | Creates a message template for messages that are sent through the email channel. |
| POST | /v1/templates/{template-name}/inapp | Creates a new message template for messages using the in-app message channel. |
| POST | /v1/templates/{template-name}/push | Creates a message template for messages that are sent through a push notification channel. |
| POST | /v1/templates/{template-name}/sms | Creates a message template for messages that are sent through the SMS channel. |
| POST | /v1/templates/{template-name}/voice | Creates a message template for messages that are sent through the voice channel. |
| DELETE | /v1/templates/{template-name}/email | Deletes a message template for messages that were sent through the email channel. |
| DELETE | /v1/templates/{template-name}/inapp | Deletes a message template for messages sent using the in-app message channel. |
| DELETE | /v1/templates/{template-name}/push | Deletes a message template for messages that were sent through a push notification channel. |
| DELETE | /v1/templates/{template-name}/sms | Deletes a message template for messages that were sent through the SMS channel. |
| DELETE | /v1/templates/{template-name}/voice | Deletes a message template for messages that were sent through the voice channel. |
| GET | /v1/templates/{template-name}/email | Retrieves the content and settings of a message template for messages that are sent through the email channel. |
| GET | /v1/templates/{template-name}/inapp | Retrieves the content and settings of a message template for messages sent through the in-app channel. |
| GET | /v1/templates/{template-name}/push | Retrieves the content and settings of a message template for messages that are sent through a push notification channel. |
| GET | /v1/templates/{template-name}/sms | Retrieves the content and settings of a message template for messages that are sent through the SMS channel. |
| GET | /v1/templates/{template-name}/voice | Retrieves the content and settings of a message template for messages that are sent through the voice channel. |
| GET | /v1/templates/{template-name}/{template-type}/versions | Retrieves information about all the versions of a specific message template. |
| GET | /v1/templates | Retrieves information about all the message templates that are associated with your Amazon Pinpoint account. |
| PUT | /v1/templates/{template-name}/email | Updates an existing message template for messages that are sent through the email channel. |
| PUT | /v1/templates/{template-name}/inapp | Updates an existing message template for messages sent through the in-app message channel. |
| PUT | /v1/templates/{template-name}/push | Updates an existing message template for messages that are sent through a push notification channel. |
| PUT | /v1/templates/{template-name}/sms | Updates an existing message template for messages that are sent through the SMS channel. |
| PUT | /v1/templates/{template-name}/{template-type}/active-version | Changes the status of a specific version of a message template to active. |
| PUT | /v1/templates/{template-name}/voice | Updates an existing message template for messages that are sent through the voice channel. |

### recommenders
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/recommenders | Creates an Amazon Pinpoint configuration for a recommender model. |
| DELETE | /v1/recommenders/{recommender-id} | Deletes an Amazon Pinpoint configuration for a recommender model. |
| GET | /v1/recommenders/{recommender-id} | Retrieves information about an Amazon Pinpoint configuration for a recommender model. |
| GET | /v1/recommenders | Retrieves information about all the recommender model configurations that are associated with your Amazon Pinpoint account. |
| PUT | /v1/recommenders/{recommender-id} | Updates an Amazon Pinpoint configuration for a recommender model. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/tags/{resource-arn} | Retrieves all the tags (keys and values) that are associated with an application, campaign, message template, or segment. |
| POST | /v1/tags/{resource-arn} | Adds one or more tags (keys and values) to an application, campaign, message template, or segment. |
| DELETE | /v1/tags/{resource-arn} | Removes one or more tags (keys and values) from an application, campaign, message template, or segment. |

### phone
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/phone/number/validate | Retrieves information about a phone number. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Pinpoint application?" -> POST /v1/apps
- "How do I list all my Pinpoint apps?" -> GET /v1/apps
- "How do I send a push notification to specific users?" -> POST /v1/apps/{application-id}/users-messages
- "How do I send a direct message to an endpoint?" -> POST /v1/apps/{application-id}/messages
- "How do I create an email template?" -> POST /v1/templates/{template-name}/email
- "How do I validate a phone number?" -> POST /v1/phone/number/validate
- "How do I check campaign performance metrics?" -> GET /v1/apps/{application-id}/campaigns/{campaign-id}/kpis/daterange/{kpi-name}
- "How do I create a segment of users?" -> POST /v1/apps/{application-id}/segments
- "How do I set up a customer journey?" -> POST /v1/apps/{application-id}/journeys
- "How do I export endpoint data to S3?" -> POST /v1/apps/{application-id}/jobs/export
- "How do I send and verify an OTP code?" -> POST /v1/apps/{application-id}/otp + POST /v1/apps/{application-id}/verify-otp
- "How do I enable the APNs channel for iOS push?" -> PUT /v1/apps/{application-id}/channels/apns
- "How do I pause or stop a running journey?" -> PUT /v1/apps/{application-id}/journeys/{journey-id}/state
- "How do I look up all endpoints for a user?" -> GET /v1/apps/{application-id}/users/{user-id}
- "How do I configure a recommender model?" -> POST /v1/recommenders

## Response Tips

- **Apps & settings**: Responses wrap the resource in a top-level key (e.g., `ApplicationResponse`, `ApplicationSettingsResource`). Always unwrap one level before reading fields.
- **List endpoints** (campaigns, segments, journeys, templates, jobs, recommenders): Paginated via `NextToken` in the response and `token`/`next-token` query param. Loop until `NextToken` is absent or empty. Use `page-size` to control batch size.
- **KPI/metrics endpoints**: Results are in `KpiResult.Rows` -- an array of `ResultRow` objects, not flat numbers. Time-bounded by `StartTime`/`EndTime` (ISO 8601 timestamps).
- **Channel responses**: All channel GETs/PUTs/DELETEs return the full channel object. Check `Enabled` and `IsArchived` booleans to confirm actual state -- a 200 does not mean the channel is active.
- **Template operations**: PUT returns a minimal `MessageBody` (just `Message` and `RequestID`), not the full template. GET the template afterward if you need the updated content.
- **Job responses** (import/export): Poll `JobStatus` field (`CREATED`, `INITIALIZING`, `PROCESSING`, `PENDING_JOB`, `COMPLETING`, `COMPLETED`, `FAILING`, `FAILED`). Check `Failures` array and `FailedPieces`/`TotalFailures` for error details.
- **Send endpoints** (messages, users-messages, OTP): Response contains per-endpoint `Result`/`EndpointResult` maps -- iterate each entry and check `DeliveryStatus` and `StatusCode` per recipient.
- **Tags**: Returned as `map<str, str>` under a `tags` key. Present on most resource responses but always optional.

## Anomaly Flags

- **Job failures**: Surface immediately when `ExportJobResponse` or `ImportJobResponse` has `JobStatus: FAILED` or `FailedPieces > 0`. Include the `Failures` array in the alert.
- **Channel disabled or archived**: Flag when any channel GET returns `Enabled: false` or `IsArchived: true` -- campaigns targeting that channel will silently fail.
- **Campaign paused**: Alert when `CampaignResponse.IsPaused` is `true` or `State.CampaignStatus` is not `COMPLETED`/`SCHEDULED` as expected.
- **Journey state mismatch**: Surface when `JourneyResponse.State` is `PAUSED`, `CANCELLED`, or `CLOSED` unexpectedly after a create/update.
- **Holdout percentage too high**: Warn if `CampaignResponse.HoldoutPercent` exceeds 50 -- this silently excludes a majority of the segment.
- **Missing message configuration**: Flag campaigns where `MessageConfiguration` is null/empty for the channels the segment targets.
- **Throttle limits**: Surface `CampaignLimits.MessagesPerSecond`, `Daily`, `Total`, and `Session` caps. Warn when `Daily` or `Total` limits are set very low relative to segment size.
- **OTP verification failure**: Alert when `VerificationResponse.Valid` is `false` -- the caller should handle retry/lockout logic.
- **Pagination truncation**: Warn when a list response contains `NextToken` but the caller did not paginate -- results are incomplete.
- **Empty segment**: Flag when a created or fetched `SegmentResponse` has `ImportDefinition.Size: 0` or no `Dimensions`/`SegmentGroups` defined.

## Playbook

### 1. Send a targeted push campaign

1. Create the application: `POST /v1/apps` with `CreateApplicationRequest`.
2. Enable the push channel (e.g., FCM): `PUT /v1/apps/{app-id}/channels/gcm` with credentials.
3. Import endpoints or register them individually: `PUT /v1/apps/{app-id}/endpoints/{endpoint-id}` with `EndpointRequest`.
4. Create a segment: `POST /v1/apps/{app-id}/segments` with `WriteSegmentRequest` defining audience criteria.
5. Create the campaign: `POST /v1/apps/{app-id}/campaigns` with `WriteCampaignRequest` referencing the segment ID, message body, and schedule.
6. Monitor performance: `GET /v1/apps/{app-id}/campaigns/{campaign-id}/kpis/daterange/{kpi-name}` with desired time range.

### 2. Set up and run a multi-step journey

1. Create the application (if not existing): `POST /v1/apps`.
2. Create segments for entry conditions: `POST /v1/apps/{app-id}/segments`.
3. Create message templates: `POST /v1/templates/{name}/email`, `/sms`, `/push` as needed.
4. Create the journey: `POST /v1/apps/{app-id}/journeys` with `WriteJourneyRequest` defining activities, start conditions, schedule, and limits.
5. Activate the journey: `PUT /v1/apps/{app-id}/journeys/{journey-id}/state` with `State: ACTIVE`.
6. Monitor execution: `GET /v1/apps/{app-id}/journeys/{journey-id}/execution-metrics` and per-activity via `GET .../activities/{activity-id}/execution-metrics`.
7. Review individual runs: `GET /v1/apps/{app-id}/journeys/{journey-id}/runs` then drill into run-level metrics.

### 3. Bulk import endpoints and export results

1. Upload your endpoint data file to S3 in CSV or JSON format.
2. Create an import job: `POST /v1/apps/{app-id}/jobs/import` with S3 URL, IAM role ARN, and format.
3. Poll job status: `GET /v1/apps/{app-id}/jobs/import/{job-id}` until `JobStatus` is `COMPLETED` or `FAILED`.
4. Check for failures: Inspect `FailedPieces`, `TotalFailures`, and `Failures` array.
5. Export the imported data: `POST /v1/apps/{app-id}/jobs/export` with S3 prefix and role ARN.
6. Poll export status: `GET /v1/apps/{app-id}/jobs/export/{job-id}` until complete.

### 4. OTP verification flow

1. Send the OTP: `POST /v1/apps/{app-id}/otp` with `SendOTPMessageRequestParameters` (destination number, channel, brand name).
2. Check the send result: Inspect `MessageResponse.Result` for delivery status per address.
3. Collect the code from the user.
4. Verify: `POST /v1/apps/{app-id}/verify-otp` with `VerifyOTPMessageRequestParameters` (reference ID, OTP code).
5. Check `VerificationResponse.Valid` -- `true` means success, `false` means invalid or expired.

### 5. Template lifecycle management

1. Create a template: `POST /v1/templates/{name}/email` (or `/sms`, `/push`, `/voice`, `/inapp`).
2. Update with versioning: `PUT /v1/templates/{name}/email` with `create-new-version: true` to preserve history.
3. Set active version: `PUT /v1/templates/{name}/{type}/active-version` with `TemplateActiveVersionRequest`.
4. List all versions: `GET /v1/templates/{name}/{type}/versions` (paginate with `next-token`).
5. Browse all templates: `GET /v1/templates` with optional `prefix` and `template-type` filters.
6. Delete when retired: `DELETE /v1/templates/{name}/email` with optional `version` to remove a specific version.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
