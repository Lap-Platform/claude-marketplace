---
name: aws-mediatailor
description: "AWS MediaTailor API skill. Use when working with AWS MediaTailor for configureLogs, channel, sourceLocation. Covers 44 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS MediaTailor
API version: 2018-04-23

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /alerts -- verify access
3. POST /channel/{ChannelName} -- create first channel

## Endpoints

44 endpoints across 10 groups. See references/api-spec.lap for full details.

### configureLogs
| Method | Path | Description |
|--------|------|-------------|
| PUT | /configureLogs/channel | Configures Amazon CloudWatch log settings for a channel. |
| PUT | /configureLogs/playbackConfiguration | Amazon CloudWatch log settings for a playback configuration. |

### channel
| Method | Path | Description |
|--------|------|-------------|
| POST | /channel/{ChannelName} | Creates a channel. For information about MediaTailor channels, see Working with channels in the MediaTailor User Guide. |
| POST | /channel/{ChannelName}/program/{ProgramName} | Creates a program within a channel. For information about programs, see Working with programs in the MediaTailor User Guide. |
| DELETE | /channel/{ChannelName} | Deletes a channel. For information about MediaTailor channels, see Working with channels in the MediaTailor User Guide. |
| DELETE | /channel/{ChannelName}/policy | The channel policy to delete. |
| DELETE | /channel/{ChannelName}/program/{ProgramName} | Deletes a program within a channel. For information about programs, see Working with programs in the MediaTailor User Guide. |
| GET | /channel/{ChannelName} | Describes a channel. For information about MediaTailor channels, see Working with channels in the MediaTailor User Guide. |
| GET | /channel/{ChannelName}/program/{ProgramName} | Describes a program within a channel. For information about programs, see Working with programs in the MediaTailor User Guide. |
| GET | /channel/{ChannelName}/policy | Returns the channel's IAM policy. IAM policies are used to control access to your channel. |
| GET | /channel/{ChannelName}/schedule | Retrieves information about your channel's schedule. |
| PUT | /channel/{ChannelName}/policy | Creates an IAM policy for the channel. IAM policies are used to control access to your channel. |
| PUT | /channel/{ChannelName}/start | Starts a channel. For information about MediaTailor channels, see Working with channels in the MediaTailor User Guide. |
| PUT | /channel/{ChannelName}/stop | Stops a channel. For information about MediaTailor channels, see Working with channels in the MediaTailor User Guide. |
| PUT | /channel/{ChannelName} | Updates a channel. For information about MediaTailor channels, see Working with channels in the MediaTailor User Guide. |
| PUT | /channel/{ChannelName}/program/{ProgramName} | Updates a program within a channel. |

### sourceLocation
| Method | Path | Description |
|--------|------|-------------|
| POST | /sourceLocation/{SourceLocationName}/liveSource/{LiveSourceName} | The live source configuration. |
| POST | /sourceLocation/{SourceLocationName} | Creates a source location. A source location is a container for sources. For more information about source locations, see Working with source locations in the MediaTailor User Guide. |
| POST | /sourceLocation/{SourceLocationName}/vodSource/{VodSourceName} | The VOD source configuration parameters. |
| DELETE | /sourceLocation/{SourceLocationName}/liveSource/{LiveSourceName} | The live source to delete. |
| DELETE | /sourceLocation/{SourceLocationName} | Deletes a source location. A source location is a container for sources. For more information about source locations, see Working with source locations in the MediaTailor User Guide. |
| DELETE | /sourceLocation/{SourceLocationName}/vodSource/{VodSourceName} | The video on demand (VOD) source to delete. |
| GET | /sourceLocation/{SourceLocationName}/liveSource/{LiveSourceName} | The live source to describe. |
| GET | /sourceLocation/{SourceLocationName} | Describes a source location. A source location is a container for sources. For more information about source locations, see Working with source locations in the MediaTailor User Guide. |
| GET | /sourceLocation/{SourceLocationName}/vodSource/{VodSourceName} | Provides details about a specific video on demand (VOD) source in a specific source location. |
| GET | /sourceLocation/{SourceLocationName}/liveSources | Lists the live sources contained in a source location. A source represents a piece of content. |
| GET | /sourceLocation/{SourceLocationName}/vodSources | Lists the VOD sources contained in a source location. A source represents a piece of content. |
| PUT | /sourceLocation/{SourceLocationName}/liveSource/{LiveSourceName} | Updates a live source's configuration. |
| PUT | /sourceLocation/{SourceLocationName} | Updates a source location. A source location is a container for sources. For more information about source locations, see Working with source locations in the MediaTailor User Guide. |
| PUT | /sourceLocation/{SourceLocationName}/vodSource/{VodSourceName} | Updates a VOD source's configuration. |

### prefetchSchedule
| Method | Path | Description |
|--------|------|-------------|
| POST | /prefetchSchedule/{PlaybackConfigurationName}/{Name} | Creates a prefetch schedule for a playback configuration. A prefetch schedule allows you to tell MediaTailor to fetch and prepare certain ads before an ad break happens. For more information about ad prefetching, see Using ad prefetching in the MediaTailor User Guide. |
| DELETE | /prefetchSchedule/{PlaybackConfigurationName}/{Name} | Deletes a prefetch schedule for a specific playback configuration. If you call DeletePrefetchSchedule on an expired prefetch schedule, MediaTailor returns an HTTP 404 status code. For more information about ad prefetching, see Using ad prefetching in the MediaTailor User Guide. |
| GET | /prefetchSchedule/{PlaybackConfigurationName}/{Name} | Retrieves a prefetch schedule for a playback configuration. A prefetch schedule allows you to tell MediaTailor to fetch and prepare certain ads before an ad break happens. For more information about ad prefetching, see Using ad prefetching in the MediaTailor User Guide. |
| POST | /prefetchSchedule/{PlaybackConfigurationName} | Lists the prefetch schedules for a playback configuration. |

### playbackConfiguration
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /playbackConfiguration/{Name} | Deletes a playback configuration. For information about MediaTailor configurations, see Working with configurations in AWS Elemental MediaTailor. |
| GET | /playbackConfiguration/{Name} | Retrieves a playback configuration. For information about MediaTailor configurations, see Working with configurations in AWS Elemental MediaTailor. |
| PUT | /playbackConfiguration | Creates a playback configuration. For information about MediaTailor configurations, see Working with configurations in AWS Elemental MediaTailor. |

### alerts
| Method | Path | Description |
|--------|------|-------------|
| GET | /alerts | Lists the alerts that are associated with a MediaTailor channel assembly resource. |

### channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /channels | Retrieves information about the channels that are associated with the current AWS account. |

### playbackConfigurations
| Method | Path | Description |
|--------|------|-------------|
| GET | /playbackConfigurations | Retrieves existing playback configurations. For information about MediaTailor configurations, see Working with Configurations in AWS Elemental MediaTailor. |

### sourceLocations
| Method | Path | Description |
|--------|------|-------------|
| GET | /sourceLocations | Lists the source locations for a channel. A source location defines the host server URL, and contains a list of sources. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{ResourceArn} | A list of tags that are associated with this resource. Tags are key-value pairs that you can associate with Amazon resources to help with organization, access control, and cost tracking. For more information, see Tagging AWS Elemental MediaTailor Resources. |
| POST | /tags/{ResourceArn} | The resource to tag. Tags are key-value pairs that you can associate with Amazon resources to help with organization, access control, and cost tracking. For more information, see Tagging AWS Elemental MediaTailor Resources. |
| DELETE | /tags/{ResourceArn} | The resource to untag. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new channel?" -> POST /channel/{ChannelName}
- "How do I list all my channels?" -> GET /channels
- "What is the current state of my channel?" -> GET /channel/{ChannelName}
- "How do I start or stop a channel?" -> PUT /channel/{ChannelName}/start, PUT /channel/{ChannelName}/stop
- "How do I set up a playback configuration for ad insertion?" -> PUT /playbackConfiguration
- "How do I add a program to a channel schedule?" -> POST /channel/{ChannelName}/program/{ProgramName}
- "How do I create a source location for my content origin?" -> POST /sourceLocation/{SourceLocationName}
- "How do I register a VOD source under a source location?" -> POST /sourceLocation/{SourceLocationName}/vodSource/{VodSourceName}
- "How do I register a live source under a source location?" -> POST /sourceLocation/{SourceLocationName}/liveSource/{LiveSourceName}
- "How do I schedule ad prefetching for a playback configuration?" -> POST /prefetchSchedule/{PlaybackConfigurationName}/{Name}
- "How do I check alerts for a specific resource?" -> GET /alerts
- "How do I view or update the channel policy?" -> GET /channel/{ChannelName}/policy, PUT /channel/{ChannelName}/policy
- "How do I configure logging for a channel?" -> PUT /configureLogs/channel
- "How do I tag or untag a MediaTailor resource?" -> POST /tags/{ResourceArn}, DELETE /tags/{ResourceArn}
- "How do I view the schedule for a channel?" -> GET /channel/{ChannelName}/schedule

## Response Tips

- **Channels & Programs:** Responses include `ChannelState` (RUNNING/STOPPED) and timestamps as ISO 8601 strings. `Outputs` is an array of output configurations -- iterate to find specific manifest URLs. `DurationMillis` and `ClipRange` offsets are in milliseconds (i64).
- **Source Locations:** `AccessConfiguration` nests `SecretsManagerAccessTokenConfiguration` three levels deep -- drill into it for secret ARN and header details. `HttpConfiguration.BaseUrl` is the only non-optional field.
- **Playback Configurations:** Deeply nested response with `AvailSuppression`, `Bumper`, `CdnConfiguration`, `DashConfiguration`, `HlsConfiguration`, and `ManifestProcessingRules` sub-objects. Check `PlaybackEndpointPrefix` and `SessionInitializationEndpointPrefix` for the actual streaming URLs.
- **Prefetch Schedules:** `Consumption` and `Retrieval` each contain `StartTime`/`EndTime` timestamps defining the prefetch window. `DynamicVariables` in `Retrieval` is a loosely-typed map.
- **Paginated Lists:** All list endpoints (`GET /channels`, `/alerts`, `/playbackConfigurations`, `/sourceLocations`, channel schedule, live/VOD sources, prefetch schedules) return `Items` + `NextToken`. Pass `NextToken` back as `nextToken` (note: casing varies -- `MaxResults`/`NextToken` for playback configs and prefetch schedules, `maxResults`/`nextToken` for the rest).
- **Tags:** Returned as flat `map<str,str>` on both resource responses and `GET /tags/{ResourceArn}`. `DELETE /tags` requires `tagKeys` as a query string array, not a body.

## Anomaly Flags

- **Channel in unexpected state:** Surface when `ChannelState` is STOPPED but the user expects it running, or vice versa. Start/stop are async -- a GET right after PUT may still show the old state.
- **Missing outputs:** Flag if a created or updated channel returns an empty `Outputs` array, as this means no manifest endpoints are configured.
- **Pagination truncation:** Warn when `NextToken` is present in a list response but the user has not paginated further -- results are incomplete.
- **Prefetch window already expired:** Flag when a prefetch schedule's `Consumption.EndTime` or `Retrieval.EndTime` is in the past.
- **Empty HttpPackageConfigurations:** Warn if a live or VOD source is created/updated with an empty `HttpPackageConfigurations` array -- the source will have no usable package types.
- **Log percentage at 0:** If `PUT /configureLogs/playbackConfiguration` sets `PercentEnabled` to 0, surface that no logs will actually be emitted.
- **AccessType mismatch:** If a source location's `AccessConfiguration.AccessType` references Secrets Manager but `SecretsManagerAccessTokenConfiguration` fields are null, flag the incomplete setup.
- **Parameter casing inconsistency:** `maxResults` vs `MaxResults` and `nextToken` vs `NextToken` vary across endpoints -- flag if the wrong casing is used (request will silently ignore the parameter).

## Playbook

### 1. Set Up a Linear Channel with VOD Content

1. Create a source location: `POST /sourceLocation/{SourceLocationName}` with `HttpConfiguration.BaseUrl` pointing to your content origin.
2. Register a VOD source: `POST /sourceLocation/{SourceLocationName}/vodSource/{VodSourceName}` with `HttpPackageConfigurations` for HLS/DASH.
3. Create the channel: `POST /channel/{ChannelName}` with `PlaybackMode: "LINEAR"`, desired `Outputs`, and optionally a `FillerSlate`.
4. Add programs to the schedule: `POST /channel/{ChannelName}/program/{ProgramName}` with `SourceLocationName`, `VodSourceName`, and `ScheduleConfiguration` for each program.
5. Start the channel: `PUT /channel/{ChannelName}/start`.
6. Verify: `GET /channel/{ChannelName}` and confirm `ChannelState` is RUNNING, then check `GET /channel/{ChannelName}/schedule` to see scheduled entries.

### 2. Configure Server-Side Ad Insertion (SSAI)

1. Create or update a playback configuration: `PUT /playbackConfiguration` with `Name`, `AdDecisionServerUrl` (your ADS endpoint), and `VideoContentSourceUrl`.
2. Optionally set `CdnConfiguration` with `AdSegmentUrlPrefix` and `ContentSegmentUrlPrefix` for CDN integration.
3. Optionally enable ad marker passthrough: set `ManifestProcessingRules.AdMarkerPassthrough.Enabled` to true.
4. Enable logging: `PUT /configureLogs/playbackConfiguration` with a non-zero `PercentEnabled`.
5. Retrieve the configuration: `GET /playbackConfiguration/{Name}` and use `SessionInitializationEndpointPrefix` to initialize player sessions.

### 3. Set Up Ad Prefetching

1. Identify the playback configuration name from `GET /playbackConfigurations`.
2. Create a prefetch schedule: `POST /prefetchSchedule/{PlaybackConfigurationName}/{Name}` with `Consumption` (time window and optional `AvailMatchingCriteria`) and `Retrieval` (time window and optional `DynamicVariables`).
3. Verify: `GET /prefetchSchedule/{PlaybackConfigurationName}/{Name}` to confirm the schedule is active.
4. List all prefetch schedules: `POST /prefetchSchedule/{PlaybackConfigurationName}` to review existing schedules.
5. Clean up expired schedules: `DELETE /prefetchSchedule/{PlaybackConfigurationName}/{Name}` for any with past `EndTime`.

### 4. Manage Live Sources and Go Live

1. Create the source location: `POST /sourceLocation/{SourceLocationName}` with `HttpConfiguration` pointing to your live origin.
2. If origin requires auth, include `AccessConfiguration` with `AccessType` and `SecretsManagerAccessTokenConfiguration`.
3. Register the live source: `POST /sourceLocation/{SourceLocationName}/liveSource/{LiveSourceName}` with `HttpPackageConfigurations`.
4. Create a channel with `PlaybackMode: "LOOP"` or `"LINEAR"`: `POST /channel/{ChannelName}`.
5. Add a program referencing the live source: `POST /channel/{ChannelName}/program/{ProgramName}` with `LiveSourceName` set.
6. Start the channel: `PUT /channel/{ChannelName}/start`.

### 5. Monitor and Troubleshoot a Channel

1. Check channel status: `GET /channel/{ChannelName}` -- look at `ChannelState` and `LastModifiedTime`.
2. Review the schedule: `GET /channel/{ChannelName}/schedule` -- paginate with `nextToken` to see all entries. Use `durationMinutes` to scope the window.
3. Pull alerts: `GET /alerts?resourceArn={channelArn}` -- paginate with `nextToken` and `maxResults`.
4. Check log configuration: `GET /channel/{ChannelName}` and inspect `LogConfiguration.LogTypes` to ensure logging is enabled.
5. Review tags for cost tracking or ownership: `GET /tags/{channelArn}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
