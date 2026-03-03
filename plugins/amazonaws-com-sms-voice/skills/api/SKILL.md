---
name: amazon-pinpoint-sms-and-voice-service
description: "Amazon Pinpoint SMS and Voice Service API skill. Use when working with Amazon Pinpoint SMS and Voice Service for sms-voice. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Pinpoint SMS and Voice Service
API version: 2018-09-05

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /v1/sms-voice/configuration-sets -- verify access
3. POST /v1/sms-voice/configuration-sets -- create first configuration-sets

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### sms-voice
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/sms-voice/configuration-sets | Create a new configuration set. After you create the configuration set, you can add one or more event destinations to it. |
| POST | /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations | Create a new event destination in a configuration set. |
| DELETE | /v1/sms-voice/configuration-sets/{ConfigurationSetName} | Deletes an existing configuration set. |
| DELETE | /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName} | Deletes an event destination in a configuration set. |
| GET | /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations | Obtain information about an event destination, including the types of events it reports, the Amazon Resource Name (ARN) of the destination, and the name of the event destination. |
| GET | /v1/sms-voice/configuration-sets | List all of the configuration sets associated with your Amazon Pinpoint account in the current region. |
| POST | /v1/sms-voice/voice/message | Create a new voice message and send it to a recipient's phone number. |
| PUT | /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName} | Update an event destination in a configuration set. An event destination is a location that you publish information about your voice calls to. For example, you can log an event to an Amazon CloudWatch destination when a call fails. |

## Enhanced Skill Content
## Question Mapping

- "How do I send a voice message?" -> POST /v1/sms-voice/voice/message
- "How do I create a configuration set?" -> POST /v1/sms-voice/configuration-sets
- "List all my configuration sets" -> GET /v1/sms-voice/configuration-sets
- "What event destinations are set up for my configuration set?" -> GET /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations
- "How do I add an event destination to a configuration set?" -> POST /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations
- "Delete a configuration set I no longer need" -> DELETE /v1/sms-voice/configuration-sets/{ConfigurationSetName}
- "Remove an event destination from a configuration set" -> DELETE /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName}
- "Update where events get routed for a configuration set" -> PUT /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName}
- "How do I set a caller ID for voice messages?" -> POST /v1/sms-voice/voice/message (use CallerId field)
- "How do I page through all configuration sets?" -> GET /v1/sms-voice/configuration-sets (use NextToken and PageSize)
- "Can I track delivery events for voice messages?" -> POST /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations
- "How do I change the SNS topic for an event destination?" -> PUT /v1/sms-voice/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName}
- "What message ID did my voice call get?" -> POST /v1/sms-voice/voice/message (check MessageId in response)

## Response Tips

- **Configuration set listings:** `ConfigurationSets` is an optional string array and may be null when no sets exist; always check for `NextToken` to handle pagination by passing it back with `PageSize`.
- **Event destinations:** `EventDestinations` returns an array of full `EventDestination` objects (not just names); may be null rather than empty when none are configured.
- **Voice message sends:** A 200 response contains `MessageId` which may be null; absence does not necessarily mean failure -- check HTTP status first.
- **Mutating operations (create/delete/update):** Return empty bodies on success; rely on HTTP status codes (200 for success, 4xx/5xx for errors) rather than response content.

## Anomaly Flags

- **Null MessageId on 200:** If POST /voice/message returns 200 but `MessageId` is null, flag this -- the message may not have been queued despite a success status.
- **Pagination loops:** If `NextToken` keeps returning the same value across consecutive calls to GET /configuration-sets, surface a potential infinite-loop risk.
- **Missing ConfigurationSetName on create:** The name field is optional on POST /configuration-sets; warn the user if they omit it since the API may auto-generate an opaque name.
- **Orphaned event destinations:** If a user deletes a configuration set without first removing its event destinations, flag that dependent resources may be silently cleaned up or orphaned depending on API behavior.
- **AWS SigV4 auth failures:** Surface 403 responses prominently -- they typically indicate expired credentials, incorrect region, or missing IAM permissions (`sms-voice:*` actions).

## Playbook

### Send a Voice Message with Delivery Tracking

1. Create a configuration set: POST /v1/sms-voice/configuration-sets with a descriptive `ConfigurationSetName`.
2. Add an event destination to it: POST /v1/sms-voice/configuration-sets/{name}/event-destinations with an SNS or CloudWatch destination in `EventDestination`.
3. Send the voice message: POST /v1/sms-voice/voice/message with `DestinationPhoneNumber`, `Content`, `OriginationPhoneNumber`, and `ConfigurationSetName` set to the name from step 1.
4. Capture the `MessageId` from the response for correlation with delivery events.

### Audit All Event Destinations Across Configuration Sets

1. List all configuration sets: GET /v1/sms-voice/configuration-sets (page through using `NextToken` until it is absent).
2. For each configuration set, retrieve its event destinations: GET /v1/sms-voice/configuration-sets/{name}/event-destinations.
3. Compile results and flag any sets with no destinations (no delivery tracking) or destinations pointing to inactive resources.

### Replace an Event Destination

1. Get current destinations: GET /v1/sms-voice/configuration-sets/{name}/event-destinations to confirm the existing `EventDestinationName`.
2. Update the destination: PUT /v1/sms-voice/configuration-sets/{name}/event-destinations/{destName} with the new `EventDestination` definition.
3. Verify by re-fetching destinations: GET the same endpoint and confirm the updated configuration.

### Clean Up a Configuration Set

1. List event destinations: GET /v1/sms-voice/configuration-sets/{name}/event-destinations.
2. Delete each event destination: DELETE /v1/sms-voice/configuration-sets/{name}/event-destinations/{destName} for every destination returned.
3. Delete the configuration set itself: DELETE /v1/sms-voice/configuration-sets/{name}.

### Page Through All Configuration Sets

1. Make an initial request: GET /v1/sms-voice/configuration-sets with a desired `PageSize` (e.g., "25").
2. Read `ConfigurationSets` from the response and store the results.
3. If `NextToken` is present, repeat the request with `NextToken` set to the returned value.
4. Continue until `NextToken` is absent from the response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
