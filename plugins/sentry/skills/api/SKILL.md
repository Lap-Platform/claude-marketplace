---
name: api-reference
description: "API Reference API skill. Use when working with API Reference for api. Covers 214 endpoints."
version: 1.0.0
generator: lapsh
---

# API Reference
API version: v0

## Auth
Bearer bearer | Bearer DSN

## Base URL
https://{region}.sentry.io

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/0/organizations/ -- verify access
3. POST /api/0/organizations/{organization_id_or_slug}/alert-rules/ -- create first alert-rules

## Endpoints

214 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/0/organizations/ | Return a list of organizations available to the authenticated session in a region. |
| GET | /api/0/organizations/{organization_id_or_slug}/ | Return details on an individual organization, including various details |
| PUT | /api/0/organizations/{organization_id_or_slug}/ | Update various attributes and configurable settings for the given organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/alert-rules/ | ## Deprecated |
| POST | /api/0/organizations/{organization_id_or_slug}/alert-rules/ | ## Deprecated |
| GET | /api/0/organizations/{organization_id_or_slug}/alert-rules/{alert_rule_id}/ | ## Deprecated |
| PUT | /api/0/organizations/{organization_id_or_slug}/alert-rules/{alert_rule_id}/ | ## Deprecated |
| DELETE | /api/0/organizations/{organization_id_or_slug}/alert-rules/{alert_rule_id}/ | ## Deprecated |
| GET | /api/0/organizations/{organization_id_or_slug}/config/integrations/ | Get integration provider information about all available integrations for an organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/dashboards/ | Retrieve a list of custom dashboards that are associated with the given organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/dashboards/ | Create a new dashboard for the given Organization |
| GET | /api/0/organizations/{organization_id_or_slug}/dashboards/{dashboard_id}/ | Return details about an organization's custom dashboard. |
| PUT | /api/0/organizations/{organization_id_or_slug}/dashboards/{dashboard_id}/ | Edit an organization's custom dashboard as well as any bulk |
| DELETE | /api/0/organizations/{organization_id_or_slug}/dashboards/{dashboard_id}/ | Delete an organization's custom dashboard, or tombstone |
| GET | /api/0/organizations/{organization_id_or_slug}/detectors/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| POST | /api/0/organizations/{organization_id_or_slug}/detectors/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| PUT | /api/0/organizations/{organization_id_or_slug}/detectors/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/detectors/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| GET | /api/0/organizations/{organization_id_or_slug}/detectors/{detector_id}/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| PUT | /api/0/organizations/{organization_id_or_slug}/detectors/{detector_id}/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/detectors/{detector_id}/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| GET | /api/0/organizations/{organization_id_or_slug}/discover/saved/ | Retrieve a list of saved queries that are associated with the given organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/discover/saved/ | Create a new saved query for the given organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/discover/saved/{query_id}/ | Retrieve a saved query. |
| PUT | /api/0/organizations/{organization_id_or_slug}/discover/saved/{query_id}/ | Modify a saved query. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/discover/saved/{query_id}/ | Delete a saved query. |
| GET | /api/0/organizations/{organization_id_or_slug}/environments/ | Lists an organization's environments. |
| GET | /api/0/organizations/{organization_id_or_slug}/eventids/{event_id}/ | This resolves an event ID to the project slug and internal issue ID and internal event ID. |
| GET | /api/0/organizations/{organization_id_or_slug}/events/ | Retrieves explore data for a given organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/events-timeseries/ | Retrieves explore data for a given organization as a timeseries. |
| POST | /api/0/organizations/{organization_id_or_slug}/external-users/ | Link a user from an external provider to a Sentry user. |
| PUT | /api/0/organizations/{organization_id_or_slug}/external-users/{external_user_id}/ | Update a user in an external provider that is currently linked to a Sentry user. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/external-users/{external_user_id}/ | Delete the link between a user from an external provider and a Sentry user. |
| GET | /api/0/organizations/{organization_id_or_slug}/forwarding/ | Returns a list of data forwarders for an organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/forwarding/ | Creates a new data forwarder for an organization. |
| PUT | /api/0/organizations/{organization_id_or_slug}/forwarding/{data_forwarder_id}/ | Updates a data forwarder for an organization or update a project-specific override. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/forwarding/{data_forwarder_id}/ | Deletes a data forwarder for an organization. All project-specific overrides will be deleted as well. |
| GET | /api/0/organizations/{organization_id_or_slug}/integrations/ | Lists all the available Integrations for an Organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/integrations/{integration_id}/ | OrganizationIntegrationBaseEndpoints expect both Integration and |
| DELETE | /api/0/organizations/{organization_id_or_slug}/integrations/{integration_id}/ | OrganizationIntegrationBaseEndpoints expect both Integration and |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/ | Return a list of issues for an organization. All parameters are supplied as query string parameters. A default query of `is:unresolved` is applied. To return all results, use an empty query value (i.e. ``?query=`). |
| PUT | /api/0/organizations/{organization_id_or_slug}/issues/ | Bulk mutate various attributes on a maxmimum of 1000 issues. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/issues/ | Permanently remove the given issues. If IDs are provided, queries and filtering will be ignored. If any IDs are out of scope, the data won't be mutated but the endpoint will still produce a successful response. For example, if no issues were found matching the criteria, a HTTP 204 is returned. |
| GET | /api/0/organizations/{organization_id_or_slug}/members/ | List all organization members. |
| POST | /api/0/organizations/{organization_id_or_slug}/members/ | Add or invite a member to an organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/members/{member_id}/ | Retrieve an organization member's details. |
| PUT | /api/0/organizations/{organization_id_or_slug}/members/{member_id}/ | Update a member's [organization-level](https://docs.sentry.io/organization/membership/#organization-level-roles) and [team-level](https://docs.sentry.io/organization/membership/#team-level-roles) roles. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/members/{member_id}/ | Remove an organization member. |
| POST | /api/0/organizations/{organization_id_or_slug}/members/{member_id}/teams/{team_id_or_slug}/ | This request can return various success codes depending on the context of the team: |
| PUT | /api/0/organizations/{organization_id_or_slug}/members/{member_id}/teams/{team_id_or_slug}/ | The relevant organization member must already be a part of the team. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/members/{member_id}/teams/{team_id_or_slug}/ | Delete an organization member from a team. |
| GET | /api/0/organizations/{organization_id_or_slug}/monitors/ | Lists monitors, including nested monitor environments. May be filtered to a project or environment. |
| POST | /api/0/organizations/{organization_id_or_slug}/monitors/ | Create a new monitor. |
| GET | /api/0/organizations/{organization_id_or_slug}/monitors/{monitor_id_or_slug}/ | Retrieves details for a monitor. |
| PUT | /api/0/organizations/{organization_id_or_slug}/monitors/{monitor_id_or_slug}/ | Update a monitor. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/monitors/{monitor_id_or_slug}/ | Delete a monitor or monitor environments. |
| GET | /api/0/organizations/{organization_id_or_slug}/monitors/{monitor_id_or_slug}/checkins/ | Retrieve a list of check-ins for a monitor |
| GET | /api/0/organizations/{organization_id_or_slug}/notifications/actions/ | Returns all Spike Protection Notification Actions for an organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/notifications/actions/ | Creates a new Notification Action for Spike Protection. |
| GET | /api/0/organizations/{organization_id_or_slug}/notifications/actions/{action_id}/ | Returns a serialized Spike Protection Notification Action object. |
| PUT | /api/0/organizations/{organization_id_or_slug}/notifications/actions/{action_id}/ | Updates a Spike Protection Notification Action. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/notifications/actions/{action_id}/ | Deletes a Spike Protection Notification Action. |
| GET | /api/0/organizations/{organization_id_or_slug}/preprodartifacts/{artifact_id}/install-details/ | Retrieve install info for a given artifact. |
| GET | /api/0/organizations/{organization_id_or_slug}/preprodartifacts/{artifact_id}/size-analysis/ | Retrieve size analysis results for a given artifact. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repositories/ | Retrieves repository data for a given owner. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repositories/sync/ | Gets syncing status for repositories for an integrated organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repositories/sync/ | Syncs repositories for an integrated organization with GitHub. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repositories/tokens/ | Retrieves a paginated list of repository tokens for a given owner. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repository/{repository}/ | Retrieves repository data for a single repository. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repository/{repository}/branches/ | Retrieves branch data for a given owner and repository. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repository/{repository}/test-results/ | Retrieves the list of test results for a given repository and owner. Also accepts a number of query parameters to filter the results. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repository/{repository}/test-results-aggregates/ | Retrieves aggregated test result metrics for a given repository and owner. |
| GET | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repository/{repository}/test-suites/ | Retrieves test suites belonging to a repository's test results. |
| POST | /api/0/organizations/{organization_id_or_slug}/prevent/owner/{owner}/repository/{repository}/token/regenerate/ | Regenerates a repository upload token and returns the new token. |
| GET | /api/0/organizations/{organization_id_or_slug}/project-keys/ | Return a list of client keys (DSNs) for all projects in an organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/projects/ | Return a list of projects bound to a organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/relay_usage/ | Return a list of trusted relays bound to an organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/release-threshold-statuses/ | **`[WARNING]`**: This API is an experimental Alpha feature and is subject to change! |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/{version}/ | Return details on an individual release. |
| PUT | /api/0/organizations/{organization_id_or_slug}/releases/{version}/ | Update a release. This can change some metadata associated with |
| DELETE | /api/0/organizations/{organization_id_or_slug}/releases/{version}/ | Permanently remove a release and all of its files. |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/{version}/deploys/ | Returns a list of deploys based on the organization, version, and project. |
| POST | /api/0/organizations/{organization_id_or_slug}/releases/{version}/deploys/ | Create a deploy for a given release. |
| GET | /api/0/organizations/{organization_id_or_slug}/replay-count/ | Return a count of replays for a list of issue or transaction IDs. |
| GET | /api/0/organizations/{organization_id_or_slug}/replay-selectors/ | Return a list of selectors for a given organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/replays/ | Return a list of replays belonging to an organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/replays/{replay_id}/ | Return details on an individual replay. |
| GET | /api/0/organizations/{organization_id_or_slug}/repos/{repo_id}/commits/ | List a Repository's Commits |
| GET | /api/0/organizations/{organization_id_or_slug}/scim/v2/Groups | Returns a paginated list of teams bound to a organization with a SCIM Groups GET Request. |
| POST | /api/0/organizations/{organization_id_or_slug}/scim/v2/Groups | Create a new team bound to an organization via a SCIM Groups POST |
| GET | /api/0/organizations/{organization_id_or_slug}/scim/v2/Groups/{team_id_or_slug} | Query an individual team with a SCIM Group GET Request. |
| PATCH | /api/0/organizations/{organization_id_or_slug}/scim/v2/Groups/{team_id_or_slug} | Update a team's attributes with a SCIM Group PATCH Request. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/scim/v2/Groups/{team_id_or_slug} | Delete a team with a SCIM Group DELETE Request. |
| GET | /api/0/organizations/{organization_id_or_slug}/scim/v2/Users | Returns a paginated list of members bound to a organization with a SCIM Users GET Request. |
| POST | /api/0/organizations/{organization_id_or_slug}/scim/v2/Users | Create a new Organization Member via a SCIM Users POST Request. |
| GET | /api/0/organizations/{organization_id_or_slug}/scim/v2/Users/{member_id} | Query an individual organization member with a SCIM User GET Request. |
| PATCH | /api/0/organizations/{organization_id_or_slug}/scim/v2/Users/{member_id} | Update an organization member's attributes with a SCIM PATCH Request. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/scim/v2/Users/{member_id} | Delete an organization member with a SCIM User DELETE Request. |
| GET | /api/0/organizations/{organization_id_or_slug}/sentry-apps/ | Retrieve the custom integrations for an organization |
| GET | /api/0/organizations/{organization_id_or_slug}/sessions/ | Returns a time series of release health session statistics for projects bound to an organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/shortids/{issue_id}/ | Resolve a short ID to the project slug and group details. |
| GET | /api/0/organizations/{organization_id_or_slug}/stats-summary/ | Query summarized event counts by project for your Organization. Also see https://docs.sentry.io/api/organizations/retrieve-event-counts-for-an-organization-v2/ for reference. |
| GET | /api/0/organizations/{organization_id_or_slug}/stats_v2/ | Query event counts for your Organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/teams/ | Returns a list of teams bound to a organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/teams/ | Create a new team bound to an organization. Requires at least one of the `name` |
| GET | /api/0/organizations/{organization_id_or_slug}/user-teams/ | Returns a list of teams the user has access to in the specified organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/workflows/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| POST | /api/0/organizations/{organization_id_or_slug}/workflows/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| PUT | /api/0/organizations/{organization_id_or_slug}/workflows/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/workflows/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| GET | /api/0/organizations/{organization_id_or_slug}/workflows/{workflow_id}/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| PUT | /api/0/organizations/{organization_id_or_slug}/workflows/{workflow_id}/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/workflows/{workflow_id}/ | ⚠️ This endpoint is currently in **beta** and may be subject to change. It is supported by [New Monitors and Alerts](/product/new-monitors-and-alerts/) and may not be viewable in the UI today. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/ | Return details on an individual project. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/ | Update various attributes and configurable settings for the given project. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/ | Schedules a project for deletion. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/environments/ | Lists a project's environments. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/environments/{environment}/ | Return details on a project environment. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/environments/{environment}/ | Update the visibility for a project environment. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/events/ | Return a list of events bound to a project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/events/{event_id}/source-map-debug/ | Return a list of source map errors for a given event. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/filters/ | Retrieve a list of filters for a given project. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/filters/{filter_id}/ | Update various inbound data filters for a project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/keys/ | Return a list of client keys bound to a project. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/keys/ | Create a new client key bound to a project.  The key's secret and public key |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/keys/{key_id}/ | Return a client key bound to a project. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/keys/{key_id}/ | Update various settings for a client key. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/keys/{key_id}/ | Delete a client key for a given project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/members/ | Returns a list of active organization members that belong to any team assigned to the project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/monitors/{monitor_id_or_slug}/ | Retrieves details for a monitor. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/monitors/{monitor_id_or_slug}/ | Update a monitor. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/monitors/{monitor_id_or_slug}/ | Delete a monitor or monitor environments. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/monitors/{monitor_id_or_slug}/checkins/ | Retrieve a list of check-ins for a monitor |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/ownership/ | Returns details on a project's ownership configuration. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/ownership/ | Updates ownership configurations for a project. Note that only the |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/replays/{replay_id}/ | Delete a replay. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/replays/{replay_id}/clicks/ | Retrieve a collection of RRWeb DOM node-ids and the timestamp they were clicked. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/replays/{replay_id}/recording-segments/ | Return a collection of replay recording segments. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/replays/{replay_id}/recording-segments/{segment_id}/ | Return a replay recording segment. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/replays/{replay_id}/viewed-by/ | Return a list of users who have viewed a replay. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/rules/ | ## Deprecated |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/rules/ | ## Deprecated |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/rules/{rule_id}/ | ## Deprecated |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/rules/{rule_id}/ | ## Deprecated |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/rules/{rule_id}/ | ## Deprecated |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/symbol-sources/ | List custom symbol sources configured for a project. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/symbol-sources/ | Add a custom symbol source to a project. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/symbol-sources/ | Update a custom symbol source in a project. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/symbol-sources/ | Delete a custom symbol source from a project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/teams/ | Return a list of teams that have access to this project. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/teams/{team_id_or_slug}/ | Give a team access to a project. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/teams/{team_id_or_slug}/ | Revoke a team's access to a project. |
| GET | /api/0/seer/models/ | Get list of actively used LLM model names from Seer. |
| GET | /api/0/sentry-apps/{sentry_app_id_or_slug}/ | Retrieve a custom integration. |
| PUT | /api/0/sentry-apps/{sentry_app_id_or_slug}/ | Update an existing custom integration. |
| DELETE | /api/0/sentry-apps/{sentry_app_id_or_slug}/ | Delete a custom integration. |
| GET | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/ | Return details on an individual team. |
| PUT | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/ | Update various attributes and configurable settings for the given |
| DELETE | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/ | Schedules a team for deletion. |
| POST | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/external-teams/ | Link a team from an external provider to a Sentry team. |
| PUT | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/external-teams/{external_team_id}/ | Update a team in an external provider that is currently linked to a Sentry team. |
| DELETE | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/external-teams/{external_team_id}/ | Delete the link between a team from an external provider and a Sentry team. |
| GET | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/members/ | List all members on a team. |
| GET | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/projects/ | Return a list of projects bound to a team. |
| POST | /api/0/teams/{organization_id_or_slug}/{team_id_or_slug}/projects/ | Create a new project bound to a team. |
| GET | /api/0/organizations/{organization_id_or_slug}/repos/ | Return a list of version control repositories for a given organization. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/files/dsyms/ | Retrieve a list of debug information files for a given project. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/files/dsyms/ | Upload a new debug information file for the given release. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/files/dsyms/ | Delete a debug information file for a given project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/users/ | Return a list of users seen within this project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/tags/{key}/values/ | Return a list of values associated with this key.  The `query` |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/stats/ | Caution |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/user-feedback/ | Return a list of user feedback items within this project. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/user-feedback/ | *This endpoint is DEPRECATED. We document it here for older SDKs and users who are still migrating to the [User Feedback Widget](https://docs.sentry.io/product/user-feedback/#user-feedback-widget) or [API](https://docs.sentry.io/platforms/javascript/user-feedback/#user-feedback-api)(multi-platform). If you are a new user, do not use this endpoint - unless you don't have a JS frontend, and your platform's SDK does not offer a feedback API.* |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/hooks/ | Return a list of service hooks bound to a project. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/hooks/ | Register a new service hook on a project. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/hooks/{hook_id}/ | Return a service hook bound to a project. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/hooks/{hook_id}/ | Update a service hook. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/hooks/{hook_id}/ | Remove a service hook. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/events/{event_id}/ | Return details on an individual event. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/issues/ | **Deprecated**: This endpoint has been replaced with the [Organization Issues endpoint](/api/events/list-an-organizations-issues/) which |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/issues/ | Bulk mutate various attributes on issues.  The list of issues to modify is given through the `id` query parameter.  It is repeated for each issue that should be modified. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/issues/ | Permanently remove the given issues. The list of issues to modify is given through the `id` query parameter.  It is repeated for each issue that should be removed. |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/tags/{key}/values/ | Returns a list of values associated with this key for an issue. |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/hashes/ | This endpoint lists an issue's hashes, which are the generated checksums used to aggregate individual events. |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/ | Return details on an individual issue. This returns the basic stats for the issue (title, last seen, first seen), some overall numbers (number of comments, user reports) as well as the summarized event data. |
| PUT | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/ | Updates an individual issue's attributes.  Only the attributes submitted are modified. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/ | Removes an individual issue. |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/ | Return a list of releases for a given organization. |
| POST | /api/0/organizations/{organization_id_or_slug}/releases/ | Create a new release for the given organization.  Releases are used by |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/{version}/files/ | Return a list of files for a given release. |
| POST | /api/0/organizations/{organization_id_or_slug}/releases/{version}/files/ | Upload a new file for the given release. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/releases/{version}/files/ | Return a list of files for a given release. |
| POST | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/releases/{version}/files/ | Upload a new file for the given release. |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/{version}/files/{file_id}/ | Retrieve a file for a given release. |
| PUT | /api/0/organizations/{organization_id_or_slug}/releases/{version}/files/{file_id}/ | Update an organization release file. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/releases/{version}/files/{file_id}/ | Delete a file for a given release. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/releases/{version}/files/{file_id}/ | Retrieve a file for a given release. |
| PUT | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/releases/{version}/files/{file_id}/ | Update a project release file. |
| DELETE | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/releases/{version}/files/{file_id}/ | Delete a file for a given release. |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/{version}/commits/ | List an organization release's commits. |
| GET | /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/releases/{version}/commits/ | List a project release's commits. |
| GET | /api/0/organizations/{organization_id_or_slug}/releases/{version}/commitfiles/ | Retrieve files changed in a release's commits |
| GET | /api/0/organizations/{organization_id_or_slug}/sentry-app-installations/ | Return a list of integration platform installations for a given organization. |
| POST | /api/0/sentry-app-installations/{uuid}/external-issues/ | Create or update an external issue from an integration platform integration. |
| DELETE | /api/0/sentry-app-installations/{uuid}/external-issues/{external_issue_id}/ | Delete an external issue. |
| POST | /api/0/organizations/{organization_id_or_slug}/spike-protections/ | Enables Spike Protection feature for some of the projects within the organization. |
| DELETE | /api/0/organizations/{organization_id_or_slug}/spike-protections/ | Disables Spike Protection feature for some of the projects within the organization. |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/autofix/ | Retrieve the current detailed state of an issue fix process for a specific issue including: |
| POST | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/autofix/ | Trigger a Seer Issue Fix run for a specific issue. |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/events/ | Return a list of error events bound to an issue |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/events/{event_id}/ | Retrieves the details of an issue event. |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/external-issues/ | Retrieve custom integration issue links for the given Sentry issue |
| GET | /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/tags/{key}/ | Return a list of values associated with this key for an issue. When paginated can return at most 1000 values. |

## Enhanced Skill Content
## Question Mapping

- "What organizations do I have access to?" -> GET /api/0/organizations/
- "Show me details about my organization's settings" -> GET /api/0/organizations/{organization_id_or_slug}/
- "What are the unresolved issues in my project?" -> GET /api/0/organizations/{organization_id_or_slug}/issues/
- "Can you look up this short issue ID?" -> GET /api/0/organizations/{organization_id_or_slug}/shortids/{issue_id}/
- "Resolve all issues matching a query in bulk" -> PUT /api/0/organizations/{organization_id_or_slug}/issues/
- "What alert rules are configured for my org?" -> GET /api/0/organizations/{organization_id_or_slug}/alert-rules/
- "Create a metric alert for high error rates" -> POST /api/0/organizations/{organization_id_or_slug}/alert-rules/
- "Show me the latest event for this issue" -> GET /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/events/{event_id}/ (use event_id=latest)
- "Who are the members of my organization?" -> GET /api/0/organizations/{organization_id_or_slug}/members/
- "Invite a new user to the organization" -> POST /api/0/organizations/{organization_id_or_slug}/members/
- "What cron monitors are set up and are any failing?" -> GET /api/0/organizations/{organization_id_or_slug}/monitors/
- "Show me my project's DSN keys" -> GET /api/0/projects/{organization_id_or_slug}/{project_id_or_slug}/keys/
- "How many events has my project received this month?" -> GET /api/0/organizations/{organization_id_or_slug}/stats_v2/
- "Deploy a new release to production" -> POST /api/0/organizations/{organization_id_or_slug}/releases/{version}/deploys/
- "Run autofix on this issue" -> POST /api/0/organizations/{organization_id_or_slug}/issues/{issue_id}/autofix/

## Response Tips

- **List endpoints** (organizations, issues, members, teams, monitors, releases): Paginated via `cursor` query param. Check response headers for `Link` with `rel="next"` to detect more pages. Empty arrays mean end of results.
- **Issues**: Default query is `is:unresolved`. The `status` field uses string values (`resolved`, `unresolved`, `ignored`, `muted`). `substatus` provides finer state (`archived_until_escalating`, `ongoing`, `regressed`, `new`). `count` is returned as a string, not int.
- **Events/Discover**: Responses wrap data in `{data: [...], meta: {fields: ...}}`. The `meta.fields` map tells you column types. `dataset` is required and must be one of `logs`, `spans`, `profile_functions`, `uptime_results`.
- **Stats**: `stats_v2` returns `{intervals: [...], groups: [...]}` where groups contain series data keyed by the `groupBy` values. `stats-summary` flattens to per-project totals.
- **Alert rules**: `triggers` is an array of threshold objects. `thresholdType` 0 = above, 1 = below. `timeWindow` accepts only specific minute values (1, 5, 10, 15, 30, 60, 120, 240, 1440).
- **Releases**: `version` is used as a path parameter and must be URL-encoded if it contains slashes or special characters. `shortVersion` is the display-friendly form.
- **Monitors (Crons)**: Environment status is nested inside `environments` with `activeIncident` present only during failures. `nextCheckIn` and `nextCheckInLatest` define the expected window.
- **SCIM endpoints**: Follow SCIM 2.0 spec with `schemas`, `totalResults`, `startIndex`, `itemsPerPage`, and `Resources` (capital R). Use `startIndex` and `count` for pagination instead of `cursor`.
- **Dashboards/Widgets**: Widget `queries` is deeply nested. Each query has `conditions` (Sentry search syntax), `fields`/`aggregates`/`columns`, and `orderby`. `display_type` controls chart rendering.
- **Mutations (PUT/DELETE)**: 204 means success with no body. 202 means accepted/queued (common for deletes of issues and monitors). 409 on POST means a conflict (duplicate slug or name).

## Anomaly Flags

- **403 on any endpoint**: Token lacks required scopes or the user's org role is insufficient. Surface this immediately -- it won't resolve by retrying. Check if the token has the right permissions for the resource type (project vs org level).
- **401 responses**: Auth token is invalid or expired. If using DSN auth, note that DSN tokens only work for a subset of endpoints. Surface and prompt for re-authentication.
- **Issue count anomalies**: If `GET /issues/` returns significantly more results than expected, check the `query` default (`is:unresolved`) -- issues may be accumulating without triage. Flag when unresolved count exceeds typical thresholds.
- **Monitor `activeIncident` present**: A cron monitor is in a broken state. Proactively surface the `brokenNotice` timestamps and whether the environment has been auto-muted.
- **Release with zero `newGroups` but high `deployCount`**: May indicate source maps are missing or events aren't being tagged to releases correctly.
- **`isOnlyOwner: true` on member detail**: Warn before any role change or removal -- this is the sole owner. Removing or demoting them will lock out the organization.
- **`expired: true` on member invites or saved queries**: Stale invitations or discover queries that need refresh. Surface these during member or query listing operations.
- **`storeCrashReports` set to -1**: Unlimited crash report storage is enabled, which can consume quota quickly. Flag when reviewing project or org settings.
- **`isDynamicallySampled: true` with low `targetSampleRate`**: Client-side sampling may be dropping events. Surface when investigating missing event data.
- **`disableReason` on issue alert rules**: A rule has been auto-disabled (usually due to too many triggers). The `disableDate` tells when it was turned off.

## Playbook

### 1. Triage and resolve a spike of new issues

1. `GET /api/0/organizations/{org}/issues/?query=is:unresolved&sort=date&limit=25` to fetch the latest unresolved issues.
2. For each critical issue, `GET /api/0/organizations/{org}/issues/{issue_id}/events/latest/` to inspect the most recent event, stack trace, and context.
3. Check `GET /api/0/organizations/{org}/issues/{issue_id}/tags/environment/values/` to determine affected environments.
4. Assign the issue: `PUT /api/0/organizations/{org}/issues/{issue_id}/` with `{"assignedTo": "user:email@example.com", "priority": "high"}`.
5. Once fixed, resolve in bulk: `PUT /api/0/organizations/{org}/issues/` with `{"status": "resolved", "query": "is:unresolved first-release:1.2.3"}`.

### 2. Ship a release with commit tracking and deploy marker

1. Create the release: `POST /api/0/organizations/{org}/releases/` with `{"version": "1.2.3", "projects": ["my-project"], "refs": [{"repository": "org/repo", "commit": "abc123"}]}`.
2. Upload source maps: `POST /api/0/organizations/{org}/releases/1.2.3/files/` (multipart form with the file).
3. Mark the deploy: `POST /api/0/organizations/{org}/releases/1.2.3/deploys/` with `{"environment": "production", "dateStarted": "...", "dateFinished": "..."}`.
4. Verify: `GET /api/0/organizations/{org}/releases/1.2.3/` and confirm `deployCount` incremented and `lastDeploy.environment` is `production`.

### 3. Set up a cron monitor for a scheduled job

1. Create the monitor: `POST /api/0/organizations/{org}/monitors/` with `{"project": "my-project", "name": "nightly-sync", "config": {"schedule_type": "crontab", "schedule": "0 3 * * *", "checkin_margin": 10, "max_runtime": 30, "timezone": "UTC"}, "status": "active"}`.
2. Integrate check-in calls in your job: send `POST` to the DSN-based check-in URL at job start (`status: in_progress`) and job end (`status: ok` or `status: error`).
3. Verify it's working: `GET /api/0/organizations/{org}/monitors/nightly-sync/checkins/` to see recent check-in history.
4. If it breaks, inspect: `GET /api/0/organizations/{org}/monitors/nightly-sync/` and check `environments[].activeIncident` for incident details.

### 4. Onboard a new team member with scoped access

1. Invite the user: `POST /api/0/organizations/{org}/members/` with `{"email": "new@example.com", "orgRole": "member", "teamRoles": [{"teamSlug": "backend", "role": "contributor"}]}`.
2. Confirm invite sent: check response for `pending: true` and `inviteStatus: "approved"`.
3. Add them to a project team: `POST /api/0/organizations/{org}/members/{member_id}/teams/backend/`.
4. Verify access: `GET /api/0/organizations/{org}/members/{member_id}/` and confirm `teams` includes `"backend"` and `teamRoles` shows the correct role.

### 5. Build a custom dashboard for error monitoring

1. Create the dashboard: `POST /api/0/organizations/{org}/dashboards/` with `{"title": "Error Overview", "widgets": []}`.
2. Add an error count widget: `PUT /api/0/organizations/{org}/dashboards/{id}/` with a widget using `{"display_type": "line", "queries": [{"conditions": "!event.type:transaction", "fields": ["count()"], "orderby": "-count()"}]}`.
3. Add a top issues table widget: include `{"display_type": "table", "queries": [{"conditions": "is:unresolved", "fields": ["issue", "title", "count()", "users"], "orderby": "-count()"}]}`.
4. Set time range and filters: update the dashboard with `{"period": "7d", "environment": ["production"], "projects": [project_id]}`.
5. Verify: `GET /api/0/organizations/{org}/dashboards/{id}/` and confirm all widgets appear with correct `queries` and `display_type`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
