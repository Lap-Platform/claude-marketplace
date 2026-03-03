---
name: amazonnimblestudio
description: "AmazonNimbleStudio API skill. Use when working with AmazonNimbleStudio for 2020-08-01. Covers 49 endpoints."
version: 1.0.0
generator: lapsh
---

# AmazonNimbleStudio
API version: 2020-08-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /2020-08-01/eulas -- verify access
3. POST /2020-08-01/studios/{studioId}/eula-acceptances -- create first eula-acceptances

## Endpoints

49 endpoints across 1 groups. See references/api-spec.lap for full details.

### 2020-08-01
| Method | Path | Description |
|--------|------|-------------|
| POST | /2020-08-01/studios/{studioId}/eula-acceptances | Accept EULAs. |
| POST | /2020-08-01/studios/{studioId}/launch-profiles | Create a launch profile. |
| POST | /2020-08-01/studios/{studioId}/streaming-images | Creates a streaming image resource in a studio. |
| POST | /2020-08-01/studios/{studioId}/streaming-sessions | Creates a streaming session in a studio. After invoking this operation, you must poll GetStreamingSession until the streaming session is in the READY state. |
| POST | /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/streams | Creates a streaming session stream for a streaming session. After invoking this API, invoke GetStreamingSessionStream with the returned streamId to poll the resource until it is in the READY state. |
| POST | /2020-08-01/studios | Create a new studio. When creating a studio, two IAM roles must be provided: the admin role and the user role. These roles are assumed by your users when they log in to the Nimble Studio portal. The user role must have the AmazonNimbleStudio-StudioUser managed policy attached for the portal to function properly. The admin role must have the AmazonNimbleStudio-StudioAdmin managed policy attached for the portal to function properly. You may optionally specify a KMS key in the StudioEncryptionConfiguration. In Nimble Studio, resource names, descriptions, initialization scripts, and other data you provide are always encrypted at rest using an KMS key. By default, this key is owned by Amazon Web Services and managed on your behalf. You may provide your own KMS key when calling CreateStudio to encrypt this data using a key you own and manage. When providing an KMS key during studio creation, Nimble Studio creates KMS grants in your account to provide your studio user and admin roles access to these KMS keys. If you delete this grant, the studio will no longer be accessible to your portal users. If you delete the studio KMS key, your studio will no longer be accessible. |
| POST | /2020-08-01/studios/{studioId}/studio-components | Creates a studio component resource. |
| DELETE | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId} | Permanently delete a launch profile. |
| DELETE | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership/{principalId} | Delete a user from launch profile membership. |
| DELETE | /2020-08-01/studios/{studioId}/streaming-images/{streamingImageId} | Delete streaming image. |
| DELETE | /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId} | Deletes streaming session resource. After invoking this operation, use GetStreamingSession to poll the resource until it transitions to a DELETED state. A streaming session will count against your streaming session quota until it is marked DELETED. |
| DELETE | /2020-08-01/studios/{studioId} | Delete a studio resource. |
| DELETE | /2020-08-01/studios/{studioId}/studio-components/{studioComponentId} | Deletes a studio component resource. |
| DELETE | /2020-08-01/studios/{studioId}/membership/{principalId} | Delete a user from studio membership. |
| GET | /2020-08-01/eulas/{eulaId} | Get EULA. |
| GET | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId} | Get a launch profile. |
| GET | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/details | Launch profile details include the launch profile resource and summary information of resources that are used by, or available to, the launch profile. This includes the name and description of all studio components used by the launch profiles, and the name and description of streaming images that can be used with this launch profile. |
| GET | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/init | Get a launch profile initialization. |
| GET | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership/{principalId} | Get a user persona in launch profile membership. |
| GET | /2020-08-01/studios/{studioId}/streaming-images/{streamingImageId} | Get streaming image. |
| GET | /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId} | Gets StreamingSession resource. Invoke this operation to poll for a streaming session state while creating or deleting a session. |
| GET | /2020-08-01/studios/{studioId}/streaming-session-backups/{backupId} | Gets StreamingSessionBackup resource. Invoke this operation to poll for a streaming session backup while stopping a streaming session. |
| GET | /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/streams/{streamId} | Gets a StreamingSessionStream for a streaming session. Invoke this operation to poll the resource after invoking CreateStreamingSessionStream. After the StreamingSessionStream changes to the READY state, the url property will contain a stream to be used with the DCV streaming client. |
| GET | /2020-08-01/studios/{studioId} | Get a studio resource. |
| GET | /2020-08-01/studios/{studioId}/studio-components/{studioComponentId} | Gets a studio component resource. |
| GET | /2020-08-01/studios/{studioId}/membership/{principalId} | Get a user's membership in a studio. |
| GET | /2020-08-01/studios/{studioId}/eula-acceptances | List EULA acceptances. |
| GET | /2020-08-01/eulas | List EULAs. |
| GET | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership | Get all users in a given launch profile membership. |
| GET | /2020-08-01/studios/{studioId}/launch-profiles | List all the launch profiles a studio. |
| GET | /2020-08-01/studios/{studioId}/streaming-images | List the streaming image resources available to this studio. This list will contain both images provided by Amazon Web Services, as well as streaming images that you have created in your studio. |
| GET | /2020-08-01/studios/{studioId}/streaming-session-backups | Lists the backups of a streaming session in a studio. |
| GET | /2020-08-01/studios/{studioId}/streaming-sessions | Lists the streaming sessions in a studio. |
| GET | /2020-08-01/studios/{studioId}/studio-components | Lists the StudioComponents in a studio. |
| GET | /2020-08-01/studios/{studioId}/membership | Get all users in a given studio membership.   ListStudioMembers only returns admin members. |
| GET | /2020-08-01/studios | List studios in your Amazon Web Services accounts in the requested Amazon Web Services Region. |
| GET | /2020-08-01/tags/{resourceArn} | Gets the tags for a resource, given its Amazon Resource Names (ARN). This operation supports ARNs for all resource types in Nimble Studio that support tags, including studio, studio component, launch profile, streaming image, and streaming session. All resources that can be tagged will contain an ARN property, so you do not have to create this ARN yourself. |
| POST | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership | Add/update users with given persona to launch profile membership. |
| POST | /2020-08-01/studios/{studioId}/membership | Add/update users with given persona to studio membership. |
| POST | /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/start | Transitions sessions from the STOPPED state into the READY state. The START_IN_PROGRESS state is the intermediate state between the STOPPED and READY states. |
| PUT | /2020-08-01/studios/{studioId}/sso-configuration | Repairs the IAM Identity Center configuration for a given studio. If the studio has a valid IAM Identity Center configuration currently associated with it, this operation will fail with a validation error. If the studio does not have a valid IAM Identity Center configuration currently associated with it, then a new IAM Identity Center application is created for the studio and the studio is changed to the READY state. After the IAM Identity Center application is repaired, you must use the Amazon Nimble Studio console to add administrators and users to your studio. |
| POST | /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/stop | Transitions sessions from the READY state into the STOPPED state. The STOP_IN_PROGRESS state is the intermediate state between the READY and STOPPED states. |
| POST | /2020-08-01/tags/{resourceArn} | Creates tags for a resource, given its ARN. |
| DELETE | /2020-08-01/tags/{resourceArn} | Deletes the tags for a resource. |
| PATCH | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId} | Update a launch profile. |
| PATCH | /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership/{principalId} | Update a user persona in launch profile membership. |
| PATCH | /2020-08-01/studios/{studioId}/streaming-images/{streamingImageId} | Update streaming image. |
| PATCH | /2020-08-01/studios/{studioId} | Update a Studio resource. Currently, this operation only supports updating the displayName of your studio. |
| PATCH | /2020-08-01/studios/{studioId}/studio-components/{studioComponentId} | Updates a studio component resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new studio?" -> POST /2020-08-01/studios
- "What studios do I have?" -> GET /2020-08-01/studios
- "How do I set up a launch profile for streaming workstations?" -> POST /2020-08-01/studios/{studioId}/launch-profiles
- "How do I start a streaming session?" -> POST /2020-08-01/studios/{studioId}/streaming-sessions
- "How do I get a stream URL to connect to my session?" -> POST /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/streams
- "How do I stop a running streaming session?" -> POST /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/stop
- "How do I resume a stopped session from a backup?" -> POST /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/start
- "What streaming images are available in my studio?" -> GET /2020-08-01/studios/{studioId}/streaming-images
- "How do I add members to a launch profile?" -> POST /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership
- "How do I accept EULAs for my studio?" -> POST /2020-08-01/studios/{studioId}/eula-acceptances
- "What studio components (render farms, license servers, shared storage) are configured?" -> GET /2020-08-01/studios/{studioId}/studio-components
- "How do I get the initialization config needed to launch a workstation?" -> GET /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/init
- "How do I tag or untag a Nimble Studio resource?" -> POST /2020-08-01/tags/{resourceArn} and DELETE /2020-08-01/tags/{resourceArn}
- "How do I update my studio's SSO configuration?" -> PUT /2020-08-01/studios/{studioId}/sso-configuration
- "How do I check for session backups I can restore from?" -> GET /2020-08-01/studios/{studioId}/streaming-session-backups

## Response Tips

- **Studios**: Top-level object is `studio` (singular on GET/create) or `studios` (array on list). Check `state` (CREATE_IN_PROGRESS, READY, DELETE_IN_PROGRESS, etc.) and `statusCode` for operational health.
- **Launch Profiles**: Response nests `streamConfiguration` deeply -- instance types, session storage, volume config, and backup settings are all inside it. Always check `validationResults` for configuration errors.
- **Streaming Sessions**: The `state` field drives lifecycle (CREATE_IN_PROGRESS, READY, START_IN_PROGRESS, STOPPED, DELETE_IN_PROGRESS). `stopAt` and `terminateAt` are future timestamps indicating auto-shutdown deadlines.
- **Streaming Images**: `state` indicates readiness (READY, CREATE_IN_PROGRESS, UPDATE_IN_PROGRESS, DELETE_IN_PROGRESS). `encryptionConfiguration` is nested under the image object.
- **Studio Components**: `configuration` is a polymorphic union -- only one of `activeDirectoryConfiguration`, `computeFarmConfiguration`, `licenseServiceConfiguration`, or `sharedFileSystemConfiguration` will be populated, matching the `type` field.
- **Paginated Lists**: All list endpoints use `nextToken` for cursor-based pagination. Some also accept `maxResults`. Loop until `nextToken` is null/absent.
- **Membership**: Returns `member` (singular) or `members` (array) with `persona` indicating the access level and `identityStoreId` linking to IAM Identity Center.

## Anomaly Flags

- **State stuck in progress**: If any resource's `state` ends with `_IN_PROGRESS` for an extended period, surface this -- the operation may be hung or failing silently. Cross-reference `statusCode` and `statusMessage` for error details.
- **Session approaching auto-termination**: When `terminateAt` or `stopAt` is within 15 minutes of current time, warn the user their session will be interrupted.
- **Validation failures on launch profiles**: If `validationResults` contains entries with non-success status codes after create or update, the profile may not be usable -- surface these immediately.
- **EULA not accepted**: If session creation fails, check whether required EULAs have been accepted via GET /eula-acceptances. Missing acceptances block streaming.
- **Deleted resources returning data**: DELETE endpoints return the deleted resource's final state. If `state` is not `DELETE_IN_PROGRESS` or `DELETED`, flag as unexpected.
- **Empty streaming image list**: If GET /streaming-images returns an empty array, the studio cannot launch sessions -- proactively suggest registering an image.
- **Idempotency token reuse**: `X-Amz-Client-Token` is used for idempotency. If a retry returns a different resource than expected, surface a possible token collision.
- **Volume retention mode on stop**: When stopping a session, if `volumeRetentionMode` is not explicitly set, the default behavior may destroy persistent storage -- flag if the session has `sessionPersistenceMode` enabled but no retention mode specified.

## Playbook

### 1. Set Up a New Studio End-to-End

1. Create the studio: POST /2020-08-01/studios with `adminRoleArn`, `displayName`, `studioName`, and `userRoleArn`
2. Poll GET /2020-08-01/studios/{studioId} until `state` is `READY`
3. Configure SSO: PUT /2020-08-01/studios/{studioId}/sso-configuration
4. Accept required EULAs: GET /2020-08-01/eulas to list them, then POST /2020-08-01/studios/{studioId}/eula-acceptances with the EULA IDs
5. Register a streaming image: POST /2020-08-01/studios/{studioId}/streaming-images with an `ec2ImageId`
6. Create studio components (render farm, license server, shared storage) as needed: POST /2020-08-01/studios/{studioId}/studio-components
7. Create a launch profile: POST /2020-08-01/studios/{studioId}/launch-profiles referencing your streaming image, subnets, and studio components
8. Add studio members: POST /2020-08-01/studios/{studioId}/membership

### 2. Launch and Connect to a Streaming Session

1. List available launch profiles: GET /2020-08-01/studios/{studioId}/launch-profiles (filter by `states=READY`)
2. Get initialization details: GET /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/init with platform and protocol version
3. Create a streaming session: POST /2020-08-01/studios/{studioId}/streaming-sessions with the `launchProfileId`
4. Poll GET /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId} until `state` is `READY`
5. Create a stream connection: POST /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/streams
6. Use the returned `url` to connect via the Nimble Studio client before `expiresAt`

### 3. Stop, Resume, and Clean Up a Session

1. Stop the session (preserving volume): POST /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/stop with `volumeRetentionMode: "RETAIN"`
2. Poll until `state` is `STOPPED`
3. To resume: POST /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}/start (optionally specify `backupId` to restore from a backup)
4. To check available backups: GET /2020-08-01/studios/{studioId}/streaming-session-backups
5. To permanently delete: DELETE /2020-08-01/studios/{studioId}/streaming-sessions/{sessionId}

### 4. Manage Launch Profile Access

1. List current members: GET /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership
2. Add members in bulk: POST /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership with `identityStoreId` and `members` array (each with `principalId` and `persona`)
3. Update a member's persona: PATCH /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership/{principalId} with new `persona`
4. Remove a member: DELETE /2020-08-01/studios/{studioId}/launch-profiles/{launchProfileId}/membership/{principalId}

### 5. Update Studio Infrastructure Components

1. List existing components: GET /2020-08-01/studios/{studioId}/studio-components (optionally filter by `types` or `states`)
2. Inspect a specific component: GET /2020-08-01/studios/{studioId}/studio-components/{studioComponentId} -- check `configuration` for current settings
3. Update the component: PATCH /2020-08-01/studios/{studioId}/studio-components/{studioComponentId} with changed fields (e.g., new `endpoint` in compute farm config, updated `scriptParameters`)
4. Poll until `state` returns to `READY` -- component updates may cycle through `UPDATE_IN_PROGRESS`
5. Verify dependent launch profiles still validate: GET /2020-08-01/studios/{studioId}/launch-profiles and check `validationResults` on each profile that references the updated component


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
