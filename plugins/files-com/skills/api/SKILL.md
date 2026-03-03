---
name: filescom-api
description: "Files.com API skill. Use when working with Files.com for sessions, action_logs, action_notification_exports. Covers 324 endpoints."
version: 1.0.0
generator: lapsh
---

# Files.com API
API version: 0.0.1

## Auth
ApiKey X-FilesAPI-Key in header

## Base URL
https://app.files.com/api/rest/v1

## Setup
1. Set your API key in the appropriate header
2. GET /action_logs -- verify access
3. POST /sessions -- create first sessions

## Endpoints

324 endpoints across 99 groups. See references/api-spec.lap for full details.

### sessions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /sessions | Delete user session (log out) |
| POST | /sessions | Create user session (log in) |

### action_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /action_logs | List Action Logs |

### action_notification_exports
| Method | Path | Description |
|--------|------|-------------|
| POST | /action_notification_exports | Create Action Notification Export |
| GET | /action_notification_exports/{id} | Show Action Notification Export |

### action_notification_export_results
| Method | Path | Description |
|--------|------|-------------|
| GET | /action_notification_export_results | List Action Notification Export Results |

### api_key
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /api_key | Delete current API key.  (Requires current API connection to be using an API key.) |
| PATCH | /api_key | Update current API key.  (Requires current API connection to be using an API key.) |
| GET | /api_key | Show information about current API key.  (Requires current API connection to be using an API key.) |

### api_keys
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /api_keys/{id} | Delete API Key |
| PATCH | /api_keys/{id} | Update API Key |
| GET | /api_keys/{id} | Show API Key |
| POST | /api_keys | Create API Key |
| GET | /api_keys | List API Keys |

### site
| Method | Path | Description |
|--------|------|-------------|
| GET | /site/usage | Get the most recent usage snapshot (usage data for billing purposes) for a Site. |
| PATCH | /site | Update Site Settings |
| GET | /site | Show Site Settings |
| GET | /site/ip_addresses | List IP Addresses associated with the current site |
| GET | /site/dns_records | Show Site DNS Configuration |
| POST | /site/test-webhook | Test Webhook |
| POST | /site/api_keys | Create API Key |
| GET | /site/api_keys | List API Keys |

### user
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /user | Update User |
| POST | /user/public_keys | Create Public Key |
| GET | /user/public_keys | List Public Keys |
| GET | /user/groups | List Group Users |
| POST | /user/api_keys | Create API Key |
| GET | /user/api_keys | List API Keys |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users/{id}/unlock | Unlock user who has been locked out due to failed logins. |
| POST | /users/{id}/resend_welcome_email | Resend user welcome email |
| POST | /users/{id}/2fa/reset | Trigger 2FA Reset process for user who has lost access to their existing 2FA methods. |
| DELETE | /users/{id} | Delete User |
| PATCH | /users/{id} | Update User |
| GET | /users/{id} | Show User |
| POST | /users | Create User |
| GET | /users | List Users |
| GET | /users/{user_id}/sftp_client_uses | List User SFTP Client Uses |
| GET | /users/{user_id}/cipher_uses | List User Cipher Uses |
| POST | /users/{user_id}/public_keys | Create Public Key |
| GET | /users/{user_id}/public_keys | List Public Keys |
| GET | /users/{user_id}/permissions | List Permissions |
| GET | /users/{user_id}/groups | List Group Users |
| POST | /users/{user_id}/api_keys | Create API Key |
| GET | /users/{user_id}/api_keys | List API Keys |

### api_request_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /api_request_logs | List API Request Logs |

### apps
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps | List Apps |

### as2_incoming_messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /as2_incoming_messages | List AS2 Incoming Messages |

### as2_outgoing_messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /as2_outgoing_messages | List AS2 Outgoing Messages |

### as2_partners
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /as2_partners/{id} | Delete AS2 Partner |
| PATCH | /as2_partners/{id} | Update AS2 Partner |
| GET | /as2_partners/{id} | Show AS2 Partner |
| POST | /as2_partners | Create AS2 Partner |
| GET | /as2_partners | List AS2 Partners |

### as2_stations
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /as2_stations/{id} | Delete AS2 Station |
| PATCH | /as2_stations/{id} | Update AS2 Station |
| GET | /as2_stations/{id} | Show AS2 Station |
| POST | /as2_stations | Create AS2 Station |
| GET | /as2_stations | List AS2 Stations |

### automations
| Method | Path | Description |
|--------|------|-------------|
| POST | /automations/{id}/manual_run | Manually Run Automation |
| DELETE | /automations/{id} | Delete Automation |
| PATCH | /automations/{id} | Update Automation |
| GET | /automations/{id} | Show Automation |
| POST | /automations | Create Automation |
| GET | /automations | List Automations |

### automation_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /automation_logs | List Automation Logs |

### automation_runs
| Method | Path | Description |
|--------|------|-------------|
| GET | /automation_runs/{id} | Show Automation Run |
| GET | /automation_runs | List Automation Runs |

### bandwidth_snapshots
| Method | Path | Description |
|--------|------|-------------|
| GET | /bandwidth_snapshots | List Bandwidth Snapshots |

### behaviors
| Method | Path | Description |
|--------|------|-------------|
| POST | /behaviors/webhook/test | Test Webhook |
| DELETE | /behaviors/{id} | Delete Behavior |
| PATCH | /behaviors/{id} | Update Behavior |
| GET | /behaviors/{id} | Show Behavior |
| POST | /behaviors | Create Behavior |
| GET | /behaviors | List Behaviors |
| GET | /behaviors/folders/{path} | List Behaviors by Path |

### bundle_actions
| Method | Path | Description |
|--------|------|-------------|
| GET | /bundle_actions | List Bundle Actions |

### bundle_downloads
| Method | Path | Description |
|--------|------|-------------|
| GET | /bundle_downloads | List Share Link Downloads |

### bundle_notifications
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /bundle_notifications/{id} | Delete Share Link Notification |
| PATCH | /bundle_notifications/{id} | Update Share Link Notification |
| GET | /bundle_notifications/{id} | Show Share Link Notification |
| POST | /bundle_notifications | Create Share Link Notification |
| GET | /bundle_notifications | List Share Link Notifications |

### bundle_recipients
| Method | Path | Description |
|--------|------|-------------|
| POST | /bundle_recipients | Create Share Link Recipient |
| GET | /bundle_recipients | List Share Link Recipients |

### bundle_registrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /bundle_registrations | List Share Link Registrations |

### bundles
| Method | Path | Description |
|--------|------|-------------|
| GET | /bundles/{id} | Show Share Link |
| PATCH | /bundles/{id} | Update Share Link |
| DELETE | /bundles/{id} | Delete Share Link |
| GET | /bundles | List Share Links |
| POST | /bundles | Create Share Link |
| POST | /bundles/{id}/share | Send email(s) with a link to bundle |

### child_site_management_policies
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /child_site_management_policies/{id} | Delete Child Site Management Policy |
| PATCH | /child_site_management_policies/{id} | Update Child Site Management Policy |
| GET | /child_site_management_policies/{id} | Show Child Site Management Policy |
| POST | /child_site_management_policies | Create Child Site Management Policy |
| GET | /child_site_management_policies | List Child Site Management Policies |

### clickwraps
| Method | Path | Description |
|--------|------|-------------|
| GET | /clickwraps | List Clickwraps |
| POST | /clickwraps | Create Clickwrap |
| DELETE | /clickwraps/{id} | Delete Clickwrap |
| PATCH | /clickwraps/{id} | Update Clickwrap |
| GET | /clickwraps/{id} | Show Clickwrap |

### dns_records
| Method | Path | Description |
|--------|------|-------------|
| GET | /dns_records | Show Site DNS Configuration |

### email_incoming_messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /email_incoming_messages | List Email Incoming Messages |

### email_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /email_logs | List Email Logs |

### exavault_api_request_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /exavault_api_request_logs | List Exavault API Request Logs |

### external_events
| Method | Path | Description |
|--------|------|-------------|
| POST | /external_events | Create External Event |
| GET | /external_events | List External Events |
| GET | /external_events/{id} | Show External Event |

### files
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /files/{path} | Delete File/Folder |
| PATCH | /files/{path} | Update File/Folder Metadata |
| POST | /files/{path} | Upload File |
| GET | /files/{path} | Download File |

### file_actions
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_actions/metadata/{path} | Find File/Folder by Path |
| POST | /file_actions/copy/{path} | Copy File/Folder |
| POST | /file_actions/move/{path} | Move File/Folder |
| POST | /file_actions/unzip | Extract a ZIP file to a destination folder. |
| GET | /file_actions/zip_list/{path} | List the contents of a ZIP file. |
| POST | /file_actions/zip | Create a ZIP from one or more paths and save it to a destination path. |
| POST | /file_actions/begin_upload/{path} | Begin File Upload |

### file_comments
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /file_comments/{id} | Delete File Comment |
| PATCH | /file_comments/{id} | Update File Comment |
| POST | /file_comments | Create File Comment |
| GET | /file_comments/files/{path} | List File Comments by Path |

### file_comment_reactions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /file_comment_reactions/{id} | Delete File Comment Reaction |
| POST | /file_comment_reactions | Create File Comment Reaction |

### file_migrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_migrations/{id} | Show File Migration |

### file_migration_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_migration_logs | List File Migration Logs |

### folders
| Method | Path | Description |
|--------|------|-------------|
| POST | /folders/{path} | Create Folder |
| GET | /folders/{path} | List Folders by Path |

### form_field_sets
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /form_field_sets/{id} | Delete Form Field Set |
| PATCH | /form_field_sets/{id} | Update Form Field Set |
| GET | /form_field_sets/{id} | Show Form Field Set |
| POST | /form_field_sets | Create Form Field Set |
| GET | /form_field_sets | List Form Field Sets |

### ftp_action_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /ftp_action_logs | List FTP Action Logs |

### groups
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups/{group_id}/users | Create User |
| GET | /groups/{group_id}/users | List Group Users |
| GET | /groups/{group_id}/permissions | List Permissions |
| DELETE | /groups/{group_id}/memberships/{user_id} | Delete Group User |
| PATCH | /groups/{group_id}/memberships/{user_id} | Update Group User |
| DELETE | /groups/{id} | Delete Group |
| PATCH | /groups/{id} | Update Group |
| GET | /groups/{id} | Show Group |
| POST | /groups | Create Group |
| GET | /groups | List Groups |

### group_users
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /group_users/{id} | Delete Group User |
| PATCH | /group_users/{id} | Update Group User |
| GET | /group_users | List Group Users |
| POST | /group_users | Create Group User |

### gpg_keys
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /gpg_keys/{id} | Delete GPG Key |
| PATCH | /gpg_keys/{id} | Update GPG Key |
| GET | /gpg_keys/{id} | Show GPG Key |
| POST | /gpg_keys | Create GPG Key |
| GET | /gpg_keys | List GPG Keys |

### history
| Method | Path | Description |
|--------|------|-------------|
| GET | /history/files/{path} | List history for specific file. |
| GET | /history/folders/{path} | List history for specific folder. |
| GET | /history/users/{user_id} | List history for specific user. |
| GET | /history/login | List site login history. |
| GET | /history | List site full action history. |

### history_exports
| Method | Path | Description |
|--------|------|-------------|
| POST | /history_exports | Create History Export |
| GET | /history_exports/{id} | Show History Export |

### history_export_results
| Method | Path | Description |
|--------|------|-------------|
| GET | /history_export_results | List History Export Results |

### holiday_regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /holiday_regions/supported | List all possible holiday regions |

### inbox_recipients
| Method | Path | Description |
|--------|------|-------------|
| POST | /inbox_recipients | Create Inbox Recipient |
| GET | /inbox_recipients | List Inbox Recipients |

### inbox_registrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbox_registrations | List Inbox Registrations |

### inbox_uploads
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbox_uploads | List Inbox Uploads |

### inbound_s3_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_s3_logs | List Inbound S3 Logs |

### invoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /invoices/{id} | Show Invoice |
| GET | /invoices | List Invoices |

### ip_addresses
| Method | Path | Description |
|--------|------|-------------|
| GET | /ip_addresses/smartfile-reserved | List all possible public SmartFile IP addresses |
| GET | /ip_addresses/exavault-reserved | List all possible public ExaVault IP addresses |
| GET | /ip_addresses/reserved | List all possible public IP addresses |
| GET | /ip_addresses | List IP Addresses associated with the current site |

### key_lifecycle_rules
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /key_lifecycle_rules/{id} | Update Key Lifecycle Rule |
| DELETE | /key_lifecycle_rules/{id} | Delete Key Lifecycle Rule |
| GET | /key_lifecycle_rules/{id} | Show Key Lifecycle Rule |
| POST | /key_lifecycle_rules | Create Key Lifecycle Rule |
| GET | /key_lifecycle_rules | List Key Lifecycle Rules |

### locks
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /locks/{path} | Delete Lock |
| POST | /locks/{path} | Create Lock |
| GET | /locks/{path} | List Locks by Path |

### messages
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /messages/{id} | Delete Message |
| PATCH | /messages/{id} | Update Message |
| GET | /messages/{id} | Show Message |
| POST | /messages | Create Message |
| GET | /messages | List Messages |

### message_comments
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /message_comments/{id} | Delete Message Comment |
| PATCH | /message_comments/{id} | Update Message Comment |
| GET | /message_comments/{id} | Show Message Comment |
| POST | /message_comments | Create Message Comment |
| GET | /message_comments | List Message Comments |

### message_comment_reactions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /message_comment_reactions/{id} | Delete Message Comment Reaction |
| GET | /message_comment_reactions/{id} | Show Message Comment Reaction |
| POST | /message_comment_reactions | Create Message Comment Reaction |
| GET | /message_comment_reactions | List Message Comment Reactions |

### message_reactions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /message_reactions/{id} | Delete Message Reaction |
| GET | /message_reactions/{id} | Show Message Reaction |
| POST | /message_reactions | Create Message Reaction |
| GET | /message_reactions | List Message Reactions |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /notifications/{id} | Delete Notification |
| PATCH | /notifications/{id} | Update Notification |
| GET | /notifications/{id} | Show Notification |
| POST | /notifications | Create Notification |
| GET | /notifications | List Notifications |

### outbound_connection_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /outbound_connection_logs | List Outbound Connection Logs |

### partners
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /partners/{id} | Delete Partner |
| PATCH | /partners/{id} | Update Partner |
| GET | /partners/{id} | Show Partner |
| GET | /partners | List Partners |
| POST | /partners | Create Partner |

### partner_sites
| Method | Path | Description |
|--------|------|-------------|
| GET | /partner_sites/linked_partner_sites | Get Partner Sites linked to the current Site |
| GET | /partner_sites | List Partner Sites |

### partner_site_requests
| Method | Path | Description |
|--------|------|-------------|
| POST | /partner_site_requests/{id}/reject | Reject partner site request |
| POST | /partner_site_requests/{id}/approve | Approve partner site request |
| GET | /partner_site_requests/find_by_pairing_key | Find partner site request by pairing key |
| DELETE | /partner_site_requests/{id} | Delete Partner Site Request |
| POST | /partner_site_requests | Create Partner Site Request |
| GET | /partner_site_requests | List Partner Site Requests |

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /payments/{id} | Show Payment |
| GET | /payments | List Payments |

### permissions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /permissions/{id} | Delete Permission |
| POST | /permissions | Create Permission |
| GET | /permissions | List Permissions |

### priorities
| Method | Path | Description |
|--------|------|-------------|
| GET | /priorities | List Priorities |

### projects
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /projects/{id} | Delete Project |
| PATCH | /projects/{id} | Update Project |
| GET | /projects/{id} | Show Project |
| POST | /projects | Create Project |
| GET | /projects | List Projects |

### public_hosting_request_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /public_hosting_request_logs | List Public Hosting Request Logs |

### public_keys
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /public_keys/{id} | Delete Public Key |
| PATCH | /public_keys/{id} | Update Public Key |
| GET | /public_keys/{id} | Show Public Key |
| POST | /public_keys | Create Public Key |
| GET | /public_keys | List Public Keys |

### restores
| Method | Path | Description |
|--------|------|-------------|
| POST | /restores | Create Restore |
| GET | /restores | List Restores |

### remote_bandwidth_snapshots
| Method | Path | Description |
|--------|------|-------------|
| GET | /remote_bandwidth_snapshots | List Remote Bandwidth Snapshots |

### remote_mount_backends
| Method | Path | Description |
|--------|------|-------------|
| POST | /remote_mount_backends/{id}/reset_status | Reset backend status to healthy. |
| DELETE | /remote_mount_backends/{id} | Delete Remote Mount Backend |
| PATCH | /remote_mount_backends/{id} | Update Remote Mount Backend |
| GET | /remote_mount_backends/{id} | Show Remote Mount Backend |
| GET | /remote_mount_backends | List Remote Mount Backends |
| POST | /remote_mount_backends | Create Remote Mount Backend |

### remote_servers
| Method | Path | Description |
|--------|------|-------------|
| POST | /remote_servers/{id}/agent_push_update | Push update to Files Agent |
| POST | /remote_servers/{id}/configuration_file | Post local changes, check in, and download configuration file (used by some Remote Server integrations, such as the Files.com Agent) |
| GET | /remote_servers/{id}/configuration_file | Download configuration file (required for some Remote Server integrations, such as the Files.com Agent) |
| GET | /remote_servers | List Remote Servers |
| POST | /remote_servers | Create Remote Server |
| DELETE | /remote_servers/{id} | Delete Remote Server |
| PATCH | /remote_servers/{id} | Update Remote Server |
| GET | /remote_servers/{id} | Show Remote Server |

### remote_server_credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /remote_server_credentials | List Remote Server Credentials |
| POST | /remote_server_credentials | Create Remote Server Credential |
| DELETE | /remote_server_credentials/{id} | Delete Remote Server Credential |
| PATCH | /remote_server_credentials/{id} | Update Remote Server Credential |
| GET | /remote_server_credentials/{id} | Show Remote Server Credential |

### requests
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /requests/{id} | Delete Request |
| POST | /requests | Create Request |
| GET | /requests | List Requests |
| GET | /requests/folders/{path} | List Requests |

### scim_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /scim_logs/{id} | Show Scim Log |
| GET | /scim_logs | List Scim Logs |

### settings_changes
| Method | Path | Description |
|--------|------|-------------|
| GET | /settings_changes | List Settings Changes |

### sftp_action_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /sftp_action_logs | List SFTP Action Logs |

### sftp_host_keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /sftp_host_keys | List SFTP Host Keys |
| POST | /sftp_host_keys | Create SFTP Host Key |
| DELETE | /sftp_host_keys/{id} | Delete SFTP Host Key |
| PATCH | /sftp_host_keys/{id} | Update SFTP Host Key |
| GET | /sftp_host_keys/{id} | Show SFTP Host Key |

### share_groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /share_groups | List Share Groups |
| POST | /share_groups | Create Share Group |
| DELETE | /share_groups/{id} | Delete Share Group |
| GET | /share_groups/{id} | Show Share Group |
| PATCH | /share_groups/{id} | Update Share Group |

### siem_http_destinations
| Method | Path | Description |
|--------|------|-------------|
| GET | /siem_http_destinations | List SIEM HTTP Destinations |
| POST | /siem_http_destinations | Create SIEM HTTP Destination |
| DELETE | /siem_http_destinations/{id} | Delete SIEM HTTP Destination |
| GET | /siem_http_destinations/{id} | Show SIEM HTTP Destination |
| PATCH | /siem_http_destinations/{id} | Update SIEM HTTP Destination |
| POST | /siem_http_destinations/send_test_entry | send_test_entry SIEM HTTP Destination |

### snapshots
| Method | Path | Description |
|--------|------|-------------|
| POST | /snapshots/{id}/finalize | Finalize Snapshot |
| DELETE | /snapshots/{id} | Delete Snapshot |
| PATCH | /snapshots/{id} | Update Snapshot |
| GET | /snapshots/{id} | Show Snapshot |
| POST | /snapshots | Create Snapshot |
| GET | /snapshots | List Snapshots |

### sso_strategies
| Method | Path | Description |
|--------|------|-------------|
| POST | /sso_strategies/{id}/sync | Synchronize provisioning data with the SSO remote server. |
| GET | /sso_strategies/{id} | Show SSO Strategy |
| GET | /sso_strategies | List SSO Strategies |

### styles
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /styles/{path} | Delete Style |
| PATCH | /styles/{path} | Update Style |
| GET | /styles/{path} | Show Style |

### syncs
| Method | Path | Description |
|--------|------|-------------|
| POST | /syncs/{id}/dry_run | Dry Run Sync |
| POST | /syncs/{id}/manual_run | Manually Run Sync |
| DELETE | /syncs/{id} | Delete Sync |
| PATCH | /syncs/{id} | Update Sync |
| GET | /syncs/{id} | Show Sync |
| GET | /syncs | List Syncs |
| POST | /syncs | Create Sync |

### sync_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /sync_logs | List Sync Logs |

### sync_runs
| Method | Path | Description |
|--------|------|-------------|
| GET | /sync_runs/{id} | Show Sync Run |
| GET | /sync_runs | List Sync Runs |

### usage_snapshots
| Method | Path | Description |
|--------|------|-------------|
| GET | /usage_snapshots | List Usage Snapshots |

### usage_daily_snapshots
| Method | Path | Description |
|--------|------|-------------|
| GET | /usage_daily_snapshots | List Usage Daily Snapshots |

### user_cipher_uses
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_cipher_uses | List User Cipher Uses |

### user_lifecycle_rules
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /user_lifecycle_rules/{id} | Update User Lifecycle Rule |
| DELETE | /user_lifecycle_rules/{id} | Delete User Lifecycle Rule |
| GET | /user_lifecycle_rules/{id} | Show User Lifecycle Rule |
| POST | /user_lifecycle_rules | Create User Lifecycle Rule |
| GET | /user_lifecycle_rules | List User Lifecycle Rules |

### user_requests
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_requests | List User Requests |
| POST | /user_requests | Create User Request |
| DELETE | /user_requests/{id} | Delete User Request |
| GET | /user_requests/{id} | Show User Request |

### user_sftp_client_uses
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_sftp_client_uses | List User SFTP Client Uses |

### web_dav_action_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /web_dav_action_logs | List WebDAV Action Logs |

### webhook_tests
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhook_tests | Create Webhook Test |

### workspaces
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /workspaces/{id} | Delete Workspace |
| PATCH | /workspaces/{id} | Update Workspace |
| GET | /workspaces/{id} | Show Workspace |
| POST | /workspaces | Create Workspace |
| GET | /workspaces | List Workspaces |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the API?" -> POST /sessions
- "How do I upload a file?" -> POST /file_actions/begin_upload/{path} then POST /files/{path}
- "How do I list files in a folder?" -> GET /folders/{path}
- "How do I download a file?" -> GET /files/{path} (with action=download)
- "How do I create a new user?" -> POST /users
- "How do I see who accessed a file?" -> GET /history/files/{path}
- "How do I share files externally via a bundle?" -> POST /bundles then POST /bundles/{id}/share
- "How do I set up an automation to copy files on a schedule?" -> POST /automations
- "How do I manage API keys for a specific user?" -> GET /users/{user_id}/api_keys or POST /users/{user_id}/api_keys
- "How do I check site storage usage?" -> GET /site/usage
- "How do I lock a file to prevent edits?" -> POST /locks/{path}
- "How do I set folder-level permissions for a group?" -> POST /permissions (with group_id and path)
- "How do I configure SIEM log forwarding to Splunk?" -> POST /siem_http_destinations (with destination_type and splunk_token)
- "How do I restore deleted files?" -> POST /restores (with earliest_date)
- "How do I sync files between a remote server and Files.com?" -> POST /syncs (with src/dest paths and remote_server_id)

## Response Tips

- **List endpoints** (users, files, groups, bundles, etc.): All paginated via `cursor` and `per_page` params. Follow the `cursor` value in the response to get the next page; stop when cursor is null.
- **Action logs and history**: Filter results using `filter`, `filter_gt`, `filter_lt`, `filter_gteq`, `filter_lteq`, and `filter_prefix` params for date ranges and field matching. Results are sorted by `sort_by`.
- **Create/POST endpoints**: Return 201 with the created resource object. The `id` in the response is needed for subsequent PATCH/DELETE calls.
- **Delete endpoints**: Return 204 with no body. A successful delete has no content to parse.
- **File operations** (copy, move, zip, unzip): Return 201 with a file migration or action object. Long operations may require polling GET /file_migrations/{id} for status.
- **Export endpoints** (history_exports, action_notification_exports): POST creates an async job; poll the GET /{id} endpoint until status is ready, then fetch results from the corresponding _results endpoint.
- **Error responses**: All endpoints share the same error code set (400-429). Expect a JSON body with `error` and `http-code` fields. 422 means validation failure with field-level detail. 423 means the resource is locked.

## Anomaly Flags

- **429 Too Many Requests**: Rate limit hit. Back off and retry with exponential delay. Surface the `Retry-After` header if present.
- **423 Locked**: File or resource is locked by another user or process. Check GET /locks/{path} to identify who holds the lock before retrying.
- **412 Precondition Failed**: Indicates a concurrency conflict (e.g., file changed since last read). Re-fetch the resource and retry the operation.
- **409 Conflict**: Resource state conflict, often from duplicate creation attempts or username collisions. Surface the conflict detail from the error body.
- **API key expiration approaching**: When listing keys via GET /api_keys, flag any keys where `expires_at` is within 7 days. Proactively suggest rotation via POST /api_keys + DELETE /api_keys/{id}.
- **User lockout events**: If GET /users/{id} shows a locked/disabled user, surface this when the user attempts operations that require that account.
- **Automation/sync failures**: After triggering POST /automations/{id}/manual_run or POST /syncs/{id}/manual_run, monitor GET /automation_runs or GET /sync_runs for error statuses and surface failures immediately.
- **Insecure SFTP ciphers**: If GET /site returns `sftp_insecure_ciphers: true` or `sftp_insecure_diffie_hellman: true`, flag this as a security concern.
- **2FA not required**: If GET /site shows `require_2fa` is disabled while sensitive operations are in use, surface as a security recommendation.

## Playbook

### 1. Onboard a New User with Group Access

1. POST /users with `username`, `email`, `password`, and `authentication_method`
2. POST /groups/{group_id}/users with the new user's `username` to add them to a group
3. POST /permissions with `path`, `group_id`, and `permission` to grant folder access
4. POST /users/{user_id}/public_keys with `title` and `public_key` if SFTP access is needed
5. Verify with GET /users/{id} and GET /users/{user_id}/groups

### 2. Share Files Externally via Bundle

1. POST /bundles with `paths` (array of file/folder paths), optional `password`, `expires_at`, and `max_uses`
2. Note the bundle `id` and `url` from the response
3. POST /bundles/{id}/share with `to` (email addresses) and optional `note`
4. POST /bundle_notifications with `bundle_id` to receive upload/download alerts
5. Monitor activity via GET /bundle_downloads and GET /bundle_actions

### 3. Set Up Scheduled File Sync with a Remote Server

1. POST /remote_servers to configure the external server (S3, SFTP, Azure, etc.) with credentials
2. POST /syncs with `src_path`, `dest_path`, `src_remote_server_id` or `dest_remote_server_id`, and schedule params (`schedule_days_of_week`, `schedule_times_of_day`, `schedule_time_zone`)
3. POST /syncs/{id}/dry_run to validate the configuration without moving files
4. Monitor runs via GET /sync_runs with the sync's `automation_id`
5. Review errors in GET /sync_logs filtered by date range

### 4. Audit File Activity for Compliance

1. POST /history_exports with `start_at`, `end_at`, and query filters (`query_action`, `query_path`, `query_username`)
2. Poll GET /history_exports/{id} until the export status is `ready`
3. GET /history_export_results with `history_export_id` to retrieve paginated results
4. For real-time monitoring, GET /history/files/{path} or GET /history/folders/{path} with date range filters
5. For login auditing specifically, use GET /history/login with `start_at` and `end_at`

### 5. Rotate and Manage API Keys

1. GET /api_keys to list all current keys; identify any with upcoming `expires_at` dates
2. POST /api_keys with `name`, `permission_set`, and `expires_at` to create a replacement key
3. Update consuming applications with the new key value (returned only at creation time)
4. DELETE /api_keys/{id} to revoke the old key
5. Verify with GET /api_keys and check GET /api_request_logs to confirm the old key is no longer in use


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
