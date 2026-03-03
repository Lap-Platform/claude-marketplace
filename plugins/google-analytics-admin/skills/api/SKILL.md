---
name: google-analytics-admin-api
description: "Google Analytics Admin API skill. Use when working with Google Analytics Admin for v1beta. Covers 26 endpoints."
version: 1.0.0
generator: lapsh
---

# Google Analytics Admin API
API version: v1beta

## Auth
OAuth2 | OAuth2

## Base URL
https://analyticsadmin.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /v1beta/accountSummaries -- verify access
3. POST /v1beta/accounts:provisionAccountTicket -- create first accounts:provisionAccountTicket

## Endpoints

26 endpoints across 1 groups. See references/api-spec.lap for full details.

### v1beta
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1beta/accountSummaries | Returns summaries of all accounts accessible by the caller. |
| GET | /v1beta/accounts | Returns all accounts accessible by the caller. Note that these accounts might not currently have GA4 properties. Soft-deleted (ie: "trashed") accounts are excluded by default. Returns an empty list if no relevant accounts are found. |
| POST | /v1beta/accounts:provisionAccountTicket | Requests a ticket for creating an account. |
| GET | /v1beta/properties | Returns child Properties under the specified parent Account. Only "GA4" properties will be returned. Properties will be excluded if the caller does not have access. Soft-deleted (ie: "trashed") properties are excluded by default. Returns an empty list if no relevant properties are found. |
| POST | /v1beta/properties | Creates an "GA4" property with the specified location and attributes. |
| POST | /v1beta/{account}:searchChangeHistoryEvents | Searches through all changes to an account or its children given the specified set of filters. |
| POST | /v1beta/{entity}:runAccessReport | Returns a customized report of data access records. The report provides records of each time a user reads Google Analytics reporting data. Access records are retained for up to 2 years. Data Access Reports can be requested for a property. The property must be in Google Analytics 360. This method is only available to Administrators. These data access records include GA4 UI Reporting, GA4 UI Explorations, GA4 Data API, and other products like Firebase & Admob that can retrieve data from Google Analytics through a linkage. These records don't include property configuration changes like adding a stream or changing a property's time zone. For configuration change history, see [searchChangeHistoryEvents](https://developers.google.com/analytics/devguides/config/admin/v1/rest/v1alpha/accounts/searchChangeHistoryEvents). |
| DELETE | /v1beta/{name} | Deletes a GoogleAdsLink on a property |
| GET | /v1beta/{name} | Lookup for a single "GA4" MeasurementProtocolSecret. |
| PATCH | /v1beta/{name} | Updates a GoogleAdsLink on a property |
| POST | /v1beta/{name}:archive | Archives a CustomMetric on a property. |
| GET | /v1beta/{parent}/conversionEvents | Returns a list of conversion events in the specified parent property. Returns an empty list if no conversion events are found. |
| POST | /v1beta/{parent}/conversionEvents | Creates a conversion event with the specified attributes. |
| GET | /v1beta/{parent}/customDimensions | Lists CustomDimensions on a property. |
| POST | /v1beta/{parent}/customDimensions | Creates a CustomDimension. |
| GET | /v1beta/{parent}/customMetrics | Lists CustomMetrics on a property. |
| POST | /v1beta/{parent}/customMetrics | Creates a CustomMetric. |
| GET | /v1beta/{parent}/dataStreams | Lists DataStreams on a property. |
| POST | /v1beta/{parent}/dataStreams | Creates a DataStream. |
| GET | /v1beta/{parent}/firebaseLinks | Lists FirebaseLinks on a property. Properties can have at most one FirebaseLink. |
| POST | /v1beta/{parent}/firebaseLinks | Creates a FirebaseLink. Properties can have at most one FirebaseLink. |
| GET | /v1beta/{parent}/googleAdsLinks | Lists GoogleAdsLinks on a property. |
| POST | /v1beta/{parent}/googleAdsLinks | Creates a GoogleAdsLink. |
| GET | /v1beta/{parent}/measurementProtocolSecrets | Returns child MeasurementProtocolSecrets under the specified parent Property. |
| POST | /v1beta/{parent}/measurementProtocolSecrets | Creates a measurement protocol secret. |
| POST | /v1beta/{property}:acknowledgeUserDataCollection | Acknowledges the terms of user data collection for the specified property. This acknowledgement must be completed (either in the Google Analytics UI or through this API) before MeasurementProtocolSecret resources may be created. |

## Enhanced Skill Content
## Question Mapping

- "What Analytics accounts do I have access to?" -> GET /v1beta/accountSummaries
- "List all my Google Analytics accounts including deleted ones" -> GET /v1beta/accounts
- "How do I create a new Analytics account?" -> POST /v1beta/accounts:provisionAccountTicket
- "Show me all properties for a specific account" -> GET /v1beta/properties
- "Create a new GA4 property for my e-commerce site" -> POST /v1beta/properties
- "Who made changes to my Analytics property last week?" -> POST /v1beta/{account}:searchChangeHistoryEvents
- "Run a data access audit report for my property" -> POST /v1beta/{entity}:runAccessReport
- "Delete a data stream from my property" -> DELETE /v1beta/{name}
- "Get the measurement protocol secret for my data stream" -> GET /v1beta/{name}
- "Update the Google Ads link settings on my property" -> PATCH /v1beta/{name}
- "Archive a custom dimension I no longer need" -> POST /v1beta/{name}:archive
- "What conversion events are configured on my property?" -> GET /v1beta/{parent}/conversionEvents
- "Add a custom metric to track revenue per user" -> POST /v1beta/{parent}/customMetrics
- "List all data streams (web, iOS, Android) on my property" -> GET /v1beta/{parent}/dataStreams
- "Link my Firebase project to my Analytics property" -> POST /v1beta/{parent}/firebaseLinks

## Response Tips

- **List endpoints** (accounts, properties, streams, links): All return paginated arrays with `nextPageToken` -- keep fetching until `nextPageToken` is absent or empty.
- **Create/Update endpoints**: Return the full resource object on success; compare with your request to confirm all fields were applied.
- **Delete/Archive endpoints**: Return empty `{}` on 200 -- absence of error IS the success signal.
- **Change history**: Results are nested maps containing `changeHistoryEvent` objects with `actorEmail`, `changeTime`, and `changedResources` arrays -- drill into `changedResources` for before/after snapshots.
- **Access reports**: Response contains separate `dimensionHeaders`, `metricHeaders`, and `rows` arrays -- zip headers with row cell values to reconstruct tabular data. The `quota` object is only present when `returnEntityQuota` is true.
- **Resource names**: All resources use hierarchical name strings (e.g., `accounts/123/properties/456/dataStreams/789`) -- parse segments to extract IDs.

## Anomaly Flags

- **Quota exhaustion**: When `runAccessReport` returns `quota` fields, surface a warning if any `remaining` value drops below 10% of its typical allocation.
- **Deleted resources**: Properties and accounts can appear with `deleteTime`/`expireTime` set -- flag these as pending permanent deletion and note the expiry window.
- **showDeleted surprises**: GET accounts/properties return only active resources by default; if results seem incomplete, suggest adding `showDeleted: true`.
- **Empty change history**: If `searchChangeHistoryEvents` returns no results for a broad time range, flag that the actor email or resource type filters may be too restrictive.
- **Missing measurement protocol secrets**: If `secretValue` comes back empty on a GET, the caller may lack sufficient permissions -- surface this as a permission issue rather than a missing secret.
- **Service level mismatch**: When creating properties, flag if `serviceLevel` returns `GOOGLE_ANALYTICS_STANDARD` when the user expected GA360 features.
- **Data stream type confusion**: If a user creates a `WEB_DATA_STREAM` but provides `androidAppStreamData`, the API may silently ignore mismatched fields -- warn when stream type and provided data don't align.

## Playbook

### 1. Set Up a New GA4 Property with Web Tracking

1. List accounts via `GET /v1beta/accountSummaries` to find the target account name.
2. Create the property via `POST /v1beta/properties` with `account`, `displayName`, `timeZone`, and `currencyCode`.
3. Note the returned `name` (e.g., `properties/123456`).
4. Create a web data stream via `POST /v1beta/{parent}/dataStreams` with `type: WEB_DATA_STREAM` and `webStreamData.defaultUri`.
5. Retrieve the measurement protocol secret via `POST /v1beta/{parent}/measurementProtocolSecrets` with a `displayName` for the secret.
6. Acknowledge user data collection via `POST /v1beta/{property}:acknowledgeUserDataCollection`.

### 2. Audit Property Access and Changes

1. Run an access report via `POST /v1beta/{entity}:runAccessReport` with `dimensions: [{dimensionName: "userEmail"}]` and a `dateRanges` covering the audit window.
2. Review the `rows` array to identify which users accessed data.
3. Search change history via `POST /v1beta/{account}:searchChangeHistoryEvents` with `earliestChangeTime` and `latestChangeTime` matching the same window.
4. Cross-reference `actorEmail` from change events with the access report to build a complete audit trail.

### 3. Connect Google Ads and Firebase to a Property

1. Fetch the property via `GET /v1beta/{name}` to confirm it exists and note its resource name.
2. Link Google Ads via `POST /v1beta/{parent}/googleAdsLinks` with the `customerId` from your Ads account.
3. Verify the link by listing via `GET /v1beta/{parent}/googleAdsLinks` and checking `adsPersonalizationEnabled`.
4. Link Firebase via `POST /v1beta/{parent}/firebaseLinks` with the `project` resource name.
5. Confirm via `GET /v1beta/{parent}/firebaseLinks` that the link is active.

### 4. Manage Custom Dimensions and Metrics

1. List existing custom dimensions via `GET /v1beta/{parent}/customDimensions` to avoid duplicates.
2. Create a new custom dimension via `POST /v1beta/{parent}/customDimensions` with `parameterName`, `displayName`, and `scope` (EVENT, USER, or ITEM).
3. List existing custom metrics via `GET /v1beta/{parent}/customMetrics`.
4. Create a new custom metric via `POST /v1beta/{parent}/customMetrics` with `parameterName`, `measurementUnit`, and `scope`.
5. To retire a dimension or metric, archive it via `POST /v1beta/{name}:archive`.

### 5. Configure Conversion Events

1. List current conversion events via `GET /v1beta/{parent}/conversionEvents` to see what's already tracked.
2. Mark a new event as a conversion via `POST /v1beta/{parent}/conversionEvents` with the `eventName` matching your GA4 event.
3. Verify the event appears in the list with `custom: true` and `deletable: true`.
4. To remove a conversion event, delete it via `DELETE /v1beta/{name}` using its resource name from the list response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
