---
name: google-analytics-api
description: "Google Analytics API skill. Use when working with Google Analytics for data, management, metadata. Covers 88 endpoints."
version: 1.0.0
generator: lapsh
---

# Google Analytics API
API version: v3

## Auth
OAuth2 | OAuth2

## Base URL
https://analytics.googleapis.com/analytics/v3

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /data/ga -- verify access
3. POST /management/accounts/{accountId}/entityUserLinks -- create first entityUserLinks

## Endpoints

88 endpoints across 5 groups. See references/api-spec.lap for full details.

### data
| Method | Path | Description |
|--------|------|-------------|
| GET | /data/ga | Returns Analytics data for a view (profile). |
| GET | /data/mcf | Returns Analytics Multi-Channel Funnels data for a view (profile). |
| GET | /data/realtime | Returns real time data for a view (profile). |

### management
| Method | Path | Description |
|--------|------|-------------|
| GET | /management/accountSummaries | Lists account summaries (lightweight tree comprised of accounts/properties/profiles) to which the user has access. |
| GET | /management/accounts | Lists all accounts to which the user has access. |
| GET | /management/accounts/{accountId}/entityUserLinks | Lists account-user links for a given account. |
| POST | /management/accounts/{accountId}/entityUserLinks | Adds a new user to the given account. |
| DELETE | /management/accounts/{accountId}/entityUserLinks/{linkId} | Removes a user from the given account. |
| PUT | /management/accounts/{accountId}/entityUserLinks/{linkId} | Updates permissions for an existing user on the given account. |
| GET | /management/accounts/{accountId}/filters | Lists all filters for an account |
| POST | /management/accounts/{accountId}/filters | Create a new filter. |
| DELETE | /management/accounts/{accountId}/filters/{filterId} | Delete a filter. |
| GET | /management/accounts/{accountId}/filters/{filterId} | Returns filters to which the user has access. |
| PATCH | /management/accounts/{accountId}/filters/{filterId} | Updates an existing filter. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/filters/{filterId} | Updates an existing filter. |
| GET | /management/accounts/{accountId}/webproperties | Lists web properties to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties | Create a new property if the account has fewer than 20 properties. Web properties are visible in the Google Analytics interface only if they have at least one profile. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId} | Gets a web property to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId} | Updates an existing web property. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId} | Updates an existing web property. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDataSources | List custom data sources to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDataSources/{customDataSourceId}/deleteUploadData | Delete data associated with a previous upload. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDataSources/{customDataSourceId}/uploads | List uploads to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDataSources/{customDataSourceId}/uploads | Upload data for a custom data source. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDataSources/{customDataSourceId}/uploads/{uploadId} | List uploads to which the user has access. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions | Lists custom dimensions to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions | Create a new custom dimension. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions/{customDimensionId} | Get a custom dimension to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions/{customDimensionId} | Updates an existing custom dimension. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions/{customDimensionId} | Updates an existing custom dimension. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customMetrics | Lists custom metrics to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/customMetrics | Create a new custom metric. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/customMetrics/{customMetricId} | Get a custom metric to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/customMetrics/{customMetricId} | Updates an existing custom metric. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/customMetrics/{customMetricId} | Updates an existing custom metric. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks | Lists webProperty-Google Ads links for a given web property. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks | Creates a webProperty-Google Ads link. |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks/{webPropertyAdWordsLinkId} | Deletes a web property-Google Ads link. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks/{webPropertyAdWordsLinkId} | Returns a web property-Google Ads link to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks/{webPropertyAdWordsLinkId} | Updates an existing webProperty-Google Ads link. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks/{webPropertyAdWordsLinkId} | Updates an existing webProperty-Google Ads link. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityUserLinks | Lists webProperty-user links for a given web property. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityUserLinks | Adds a new user to the given web property. |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityUserLinks/{linkId} | Removes a user from the given web property. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/entityUserLinks/{linkId} | Updates permissions for an existing user on the given web property. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles | Lists views (profiles) to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles | Create a new view (profile). |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId} | Deletes a view (profile). |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId} | Gets a view (profile) to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId} | Updates an existing view (profile). This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId} | Updates an existing view (profile). |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/entityUserLinks | Lists profile-user links for a given view (profile). |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/entityUserLinks | Adds a new user to the given view (profile). |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/entityUserLinks/{linkId} | Removes a user from the given view (profile). |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/entityUserLinks/{linkId} | Updates permissions for an existing user on the given view (profile). |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/experiments | Lists experiments to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/experiments | Create a new experiment. |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/experiments/{experimentId} | Delete an experiment. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/experiments/{experimentId} | Returns an experiment to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/experiments/{experimentId} | Update an existing experiment. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/experiments/{experimentId} | Update an existing experiment. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals | Lists goals to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals | Create a new goal. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals/{goalId} | Gets a goal to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals/{goalId} | Updates an existing goal. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals/{goalId} | Updates an existing goal. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/profileFilterLinks | Lists all profile filter links for a profile. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/profileFilterLinks | Create a new profile filter link. |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/profileFilterLinks/{linkId} | Delete a profile filter link. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/profileFilterLinks/{linkId} | Returns a single profile filter link. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/profileFilterLinks/{linkId} | Update an existing profile filter link. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/profileFilterLinks/{linkId} | Update an existing profile filter link. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/unsampledReports | Lists unsampled reports to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/unsampledReports | Create a new unsampled report. |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/unsampledReports/{unsampledReportId} | Deletes an unsampled report. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/unsampledReports/{unsampledReportId} | Returns a single unsampled report. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences | Lists remarketing audiences to which the user has access. |
| POST | /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences | Creates a new remarketing audience. |
| DELETE | /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences/{remarketingAudienceId} | Delete a remarketing audience. |
| GET | /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences/{remarketingAudienceId} | Gets a remarketing audience to which the user has access. |
| PATCH | /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences/{remarketingAudienceId} | Updates an existing remarketing audience. This method supports patch semantics. |
| PUT | /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences/{remarketingAudienceId} | Updates an existing remarketing audience. |
| POST | /management/clientId:hashClientId | Hashes the given Client ID. |
| GET | /management/segments | Lists segments to which the user has access. |

### metadata
| Method | Path | Description |
|--------|------|-------------|
| GET | /metadata/{reportType}/columns | Lists all columns for a report type |

### provisioning
| Method | Path | Description |
|--------|------|-------------|
| POST | /provisioning/createAccountTicket | Creates an account ticket. |
| POST | /provisioning/createAccountTree | Provision account. |

### userDeletion
| Method | Path | Description |
|--------|------|-------------|
| POST | /userDeletion/userDeletionRequests:upsert | Insert or update a user deletion requests. |

## Enhanced Skill Content
## Question Mapping

- "How many page views did my site get last month?" -> GET /data/ga
- "What is happening on my site right now?" -> GET /data/realtime
- "Which channels drove the most conversions?" -> GET /data/mcf
- "What accounts do I have access to?" -> GET /management/accountSummaries
- "Who has access to my Analytics property?" -> GET /management/accounts/{accountId}/webproperties/{webPropertyId}/entityUserLinks
- "How do I create a new view (profile) for my property?" -> POST /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles
- "What filters are applied to my account?" -> GET /management/accounts/{accountId}/filters
- "How do I link Google Ads to my Analytics property?" -> POST /management/accounts/{accountId}/webproperties/{webPropertyId}/entityAdWordsLinks
- "What custom dimensions are configured?" -> GET /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions
- "How do I set up a goal for tracking form submissions?" -> POST /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals
- "Can I get an unsampled version of my report?" -> POST /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/unsampledReports
- "How do I create a remarketing audience?" -> POST /management/accounts/{accountId}/webproperties/{webPropertyId}/remarketingAudiences
- "What metrics and dimensions are available for reporting?" -> GET /metadata/{reportType}/columns
- "How do I remove a user from my Analytics account?" -> DELETE /management/accounts/{accountId}/entityUserLinks/{linkId}
- "How do I provision a brand new Analytics account with property and view?" -> POST /provisioning/createAccountTree

## Response Tips

- **Data endpoints** (`/data/ga`, `/data/mcf`, `/data/realtime`): Check `containsSampledData` -- if true, `sampleSize` and `sampleSpace` indicate coverage. Actual data lives in `rows` (array of string arrays), matched positionally to `columnHeaders`. Use `totalResults` vs `itemsPerPage` to detect truncation. Pagination uses `start-index` + `max-results`, not cursor tokens.
- **Management list endpoints**: All return `{items, totalResults, itemsPerPage, startIndex}`. Paginate by incrementing `start-index` by `max-results`. Follow `nextLink`/`previousLink` when present. The `items` array contains the actual resources.
- **Management CRUD endpoints**: Single-resource responses echo back the full object after mutation. Check the `kind` field to confirm resource type. `selfLink` provides the canonical URL for subsequent operations.
- **Metadata endpoint**: Returns `items` with `attributeNames` describing available column attributes. Use `etag` for conditional requests.
- **Provisioning endpoints**: Return composite objects with nested `account`, `webproperty`, and `profile` -- extract IDs from each for subsequent API calls.

## Anomaly Flags

- **Sampled data warning**: Surface when `containsSampledData: true` in GA/MCF responses -- the report is an estimate, not exact. Show `sampleSize / sampleSpace` as coverage percentage.
- **Truncated results**: Alert when `totalResults > itemsPerPage` and no pagination was requested -- the user is missing data rows.
- **Empty rows in GA**: When `include-empty-rows` is not set, zero-value dimension combinations are silently omitted -- flag if the user expects complete matrices.
- **Deprecated API version**: Google Analytics v3 (Universal Analytics) is sunset. Proactively note that GA4 and the Data API v1 are the current standard.
- **Upload errors**: When checking custom data uploads, surface any non-empty `errors` array or `status` other than `COMPLETED`.
- **Experiment winner found**: If `winnerFound: true` in experiment responses, notify that the test has concluded and action may be needed.
- **Unsampled report status**: Poll and surface when `status` changes from `PENDING` to `COMPLETED` or shows an error state.
- **Permission scope mismatch**: When `permissions.effective` differs from `permissions.local`, flag that inherited permissions are in play.

## Playbook

### 1. Pull a weekly traffic report with dimensions

1. GET /management/accountSummaries to find your `accountId`, `webPropertyId`, and `profileId`
2. GET /metadata/ga/columns to discover available metrics and dimensions
3. GET /data/ga with `ids=ga:{profileId}`, `start-date=7daysAgo`, `end-date=yesterday`, `metrics=ga:sessions,ga:pageviews`, `dimensions=ga:date`
4. Check `containsSampledData` in the response -- if true, consider re-requesting with `samplingLevel=HIGHER_PRECISION`
5. If `totalResults > max-results`, paginate by incrementing `start-index`

### 2. Grant a user read access to a property

1. GET /management/accounts to find the target `accountId`
2. GET /management/accounts/{accountId}/webproperties to find the target `webPropertyId`
3. POST /management/accounts/{accountId}/webproperties/{webPropertyId}/entityUserLinks with body: `userRef.email` set to the user's email, `permissions.local` set to `["READ_AND_ANALYZE"]`
4. Confirm the response contains the new `linkId` and correct `permissions.effective`

### 3. Create a destination goal with funnel steps

1. GET /management/accountSummaries to resolve `accountId`, `webPropertyId`, and `profileId`
2. POST /management/accounts/{accountId}/webproperties/{webPropertyId}/profiles/{profileId}/goals with `type: "URL_DESTINATION"`, `urlDestinationDetails.url: "/thank-you"`, `urlDestinationDetails.matchType: "EXACT"`, and `urlDestinationDetails.steps` array defining funnel pages
3. Set `active: true` and provide a descriptive `name`
4. Verify the returned goal `id` and confirm `active` is true

### 4. Set up a custom dimension and use it in a report

1. POST /management/accounts/{accountId}/webproperties/{webPropertyId}/customDimensions with `name`, `scope` (HIT, SESSION, USER, or PRODUCT), and `active: true`
2. Note the returned `index` (e.g., `1` means `ga:dimension1`)
3. Implement the tracking code on your site to send values for this dimension
4. After data collection begins, GET /data/ga with `dimensions=ga:dimension{index}` and your chosen metrics

### 5. Provision a new account with property and view in one call

1. POST /provisioning/createAccountTree with `accountName`, `webpropertyName`, `profileName`, `timezone` (e.g., `America/New_York`), and `websiteUrl`
2. Extract `account.id`, `webproperty.id`, and `profile.id` from the response
3. Use these IDs immediately for subsequent management calls (filters, goals, user links)
4. Optionally POST /management/accounts/{accountId}/filters to apply default filters (e.g., exclude internal IP traffic)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
