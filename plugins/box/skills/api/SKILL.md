---
name: box-platform-api
description: "Box Platform API skill. Use when working with Box Platform for authorize, oauth2, files. Covers 296 endpoints."
version: 1.0.0
generator: lapsh
---

# Box Platform API
API version: 2024.0

## Auth
OAuth2

## Base URL
https://api.box.com/2.0

## Setup
1. Configure auth: OAuth2
2. GET /authorize -- verify access
3. POST /oauth2/token -- create first token

## Endpoints

296 endpoints across 56 groups. See references/api-spec.lap for full details.

### authorize
| Method | Path | Description |
|--------|------|-------------|
| GET | /authorize | Authorize user |

### oauth2
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth2/token | Request access token |
| POST | /oauth2/token#refresh | Refresh access token |
| POST | /oauth2/revoke | Revoke access token |

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /files/{file_id} | Get file information |
| POST | /files/{file_id} | Restore file |
| PUT | /files/{file_id} | Update file |
| DELETE | /files/{file_id} | Delete file |
| GET | /files/{file_id}/app_item_associations | List file app item associations |
| GET | /files/{file_id}/content | Download file |
| POST | /files/{file_id}/content | Upload file version |
| OPTIONS | /files/content | Preflight check before upload |
| POST | /files/content | Upload file |
| POST | /files/upload_sessions | Create upload session |
| POST | /files/{file_id}/upload_sessions | Create upload session for existing file |
| GET | /files/upload_sessions/{upload_session_id} | Get upload session |
| PUT | /files/upload_sessions/{upload_session_id} | Upload part of file |
| DELETE | /files/upload_sessions/{upload_session_id} | Remove upload session |
| GET | /files/upload_sessions/{upload_session_id}/parts | List parts |
| POST | /files/upload_sessions/{upload_session_id}/commit | Commit upload session |
| POST | /files/{file_id}/copy | Copy file |
| GET | /files/{file_id}/thumbnail.{extension} | Get file thumbnail |
| GET | /files/{file_id}/collaborations | List file collaborations |
| GET | /files/{file_id}/comments | List file comments |
| GET | /files/{file_id}/tasks | List tasks on file |
| GET | /files/{file_id}/trash | Get trashed file |
| DELETE | /files/{file_id}/trash | Permanently remove file |
| GET | /files/{file_id}/versions | List all file versions |
| GET | /files/{file_id}/versions/{file_version_id} | Get file version |
| DELETE | /files/{file_id}/versions/{file_version_id} | Remove file version |
| PUT | /files/{file_id}/versions/{file_version_id} | Restore file version |
| POST | /files/{file_id}/versions/current | Promote file version |
| GET | /files/{file_id}/metadata | List metadata instances on file |
| GET | /files/{file_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Get classification on file |
| POST | /files/{file_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Add classification to file |
| PUT | /files/{file_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Update classification on file |
| DELETE | /files/{file_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Remove classification from file |
| GET | /files/{file_id}/metadata/{scope}/{template_key} | Get metadata instance on file |
| POST | /files/{file_id}/metadata/{scope}/{template_key} | Create metadata instance on file |
| PUT | /files/{file_id}/metadata/{scope}/{template_key} | Update metadata instance on file |
| DELETE | /files/{file_id}/metadata/{scope}/{template_key} | Remove metadata instance from file |
| GET | /files/{file_id}/metadata/global/boxSkillsCards | List Box Skill cards on file |
| POST | /files/{file_id}/metadata/global/boxSkillsCards | Create Box Skill cards on file |
| PUT | /files/{file_id}/metadata/global/boxSkillsCards | Update Box Skill cards on file |
| DELETE | /files/{file_id}/metadata/global/boxSkillsCards | Remove Box Skill cards from file |
| GET | /files/{file_id}/watermark | Get watermark on file |
| PUT | /files/{file_id}/watermark | Apply watermark to file |
| DELETE | /files/{file_id}/watermark | Remove watermark from file |
| GET | /files/{file_id}#get_shared_link | Get shared link for file |
| PUT | /files/{file_id}#add_shared_link | Add shared link to file |
| PUT | /files/{file_id}#update_shared_link | Update shared link on file |
| PUT | /files/{file_id}#remove_shared_link | Remove shared link from file |

### file_requests
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_requests/{file_request_id} | Get file request |
| PUT | /file_requests/{file_request_id} | Update file request |
| DELETE | /file_requests/{file_request_id} | Delete file request |
| POST | /file_requests/{file_request_id}/copy | Copy file request |

### folders
| Method | Path | Description |
|--------|------|-------------|
| GET | /folders/{folder_id} | Get folder information |
| POST | /folders/{folder_id} | Restore folder |
| PUT | /folders/{folder_id} | Update folder |
| DELETE | /folders/{folder_id} | Delete folder |
| GET | /folders/{folder_id}/app_item_associations | List folder app item associations |
| GET | /folders/{folder_id}/items | List items in folder |
| POST | /folders | Create folder |
| POST | /folders/{folder_id}/copy | Copy folder |
| GET | /folders/{folder_id}/collaborations | List folder collaborations |
| GET | /folders/{folder_id}/trash | Get trashed folder |
| DELETE | /folders/{folder_id}/trash | Permanently remove folder |
| GET | /folders/{folder_id}/metadata | List metadata instances on folder |
| GET | /folders/{folder_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Get classification on folder |
| POST | /folders/{folder_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Add classification to folder |
| PUT | /folders/{folder_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Update classification on folder |
| DELETE | /folders/{folder_id}/metadata/enterprise/securityClassification-6VMVochwUWo | Remove classification from folder |
| GET | /folders/{folder_id}/metadata/{scope}/{template_key} | Get metadata instance on folder |
| POST | /folders/{folder_id}/metadata/{scope}/{template_key} | Create metadata instance on folder |
| PUT | /folders/{folder_id}/metadata/{scope}/{template_key} | Update metadata instance on folder |
| DELETE | /folders/{folder_id}/metadata/{scope}/{template_key} | Remove metadata instance from folder |
| GET | /folders/trash/items | List trashed items |
| GET | /folders/{folder_id}/watermark | Get watermark for folder |
| PUT | /folders/{folder_id}/watermark | Apply watermark to folder |
| DELETE | /folders/{folder_id}/watermark | Remove watermark from folder |
| GET | /folders/{folder_id}#get_shared_link | Get shared link for folder |
| PUT | /folders/{folder_id}#add_shared_link | Add shared link to folder |
| PUT | /folders/{folder_id}#update_shared_link | Update shared link on folder |
| PUT | /folders/{folder_id}#remove_shared_link | Remove shared link from folder |

### folder_locks
| Method | Path | Description |
|--------|------|-------------|
| GET | /folder_locks | List folder locks |
| POST | /folder_locks | Create folder lock |
| DELETE | /folder_locks/{folder_lock_id} | Delete folder lock |

### metadata_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /metadata_templates | Find metadata template by instance ID |
| GET | /metadata_templates/enterprise/securityClassification-6VMVochwUWo/schema | List all classifications |
| PUT | /metadata_templates/enterprise/securityClassification-6VMVochwUWo/schema#add | Add classification |
| PUT | /metadata_templates/enterprise/securityClassification-6VMVochwUWo/schema#update | Update classification |
| GET | /metadata_templates/{scope}/{template_key}/schema | Get metadata template by name |
| PUT | /metadata_templates/{scope}/{template_key}/schema | Update metadata template |
| DELETE | /metadata_templates/{scope}/{template_key}/schema | Remove metadata template |
| GET | /metadata_templates/{template_id} | Get metadata template by ID |
| GET | /metadata_templates/global | List all global metadata templates |
| GET | /metadata_templates/enterprise | List all metadata templates for enterprise |
| POST | /metadata_templates/schema | Create metadata template |
| POST | /metadata_templates/schema#classifications | Add initial classifications |
| GET | /metadata_templates/{namespace}/{template_key}/fields/{field_key}/options | List metadata template's options for taxonomy field |

### metadata_cascade_policies
| Method | Path | Description |
|--------|------|-------------|
| GET | /metadata_cascade_policies | List metadata cascade policies |
| POST | /metadata_cascade_policies | Create metadata cascade policy |
| GET | /metadata_cascade_policies/{metadata_cascade_policy_id} | Get metadata cascade policy |
| DELETE | /metadata_cascade_policies/{metadata_cascade_policy_id} | Remove metadata cascade policy |
| POST | /metadata_cascade_policies/{metadata_cascade_policy_id}/apply | Force-apply metadata cascade policy to folder |

### metadata_queries
| Method | Path | Description |
|--------|------|-------------|
| POST | /metadata_queries/execute_read | Query files/folders by metadata |

### comments
| Method | Path | Description |
|--------|------|-------------|
| GET | /comments/{comment_id} | Get comment |
| PUT | /comments/{comment_id} | Update comment |
| DELETE | /comments/{comment_id} | Remove comment |
| POST | /comments | Create comment |

### collaborations
| Method | Path | Description |
|--------|------|-------------|
| GET | /collaborations/{collaboration_id} | Get collaboration |
| PUT | /collaborations/{collaboration_id} | Update collaboration |
| DELETE | /collaborations/{collaboration_id} | Remove collaboration |
| GET | /collaborations | List pending collaborations |
| POST | /collaborations | Create collaboration |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Search for content |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| POST | /tasks | Create task |
| GET | /tasks/{task_id} | Get task |
| PUT | /tasks/{task_id} | Update task |
| DELETE | /tasks/{task_id} | Remove task |
| GET | /tasks/{task_id}/assignments | List task assignments |

### task_assignments
| Method | Path | Description |
|--------|------|-------------|
| POST | /task_assignments | Assign task |
| GET | /task_assignments/{task_assignment_id} | Get task assignment |
| PUT | /task_assignments/{task_assignment_id} | Update task assignment |
| DELETE | /task_assignments/{task_assignment_id} | Unassign task |

### shared_items
| Method | Path | Description |
|--------|------|-------------|
| GET | /shared_items | Find file for shared link |

### shared_items#folders
| Method | Path | Description |
|--------|------|-------------|
| GET | /shared_items#folders | Find folder for shared link |

### web_links
| Method | Path | Description |
|--------|------|-------------|
| POST | /web_links | Create web link |
| GET | /web_links/{web_link_id} | Get web link |
| POST | /web_links/{web_link_id} | Restore web link |
| PUT | /web_links/{web_link_id} | Update web link |
| DELETE | /web_links/{web_link_id} | Remove web link |
| GET | /web_links/{web_link_id}/trash | Get trashed web link |
| DELETE | /web_links/{web_link_id}/trash | Permanently remove web link |
| GET | /web_links/{web_link_id}#get_shared_link | Get shared link for web link |
| PUT | /web_links/{web_link_id}#add_shared_link | Add shared link to web link |
| PUT | /web_links/{web_link_id}#update_shared_link | Update shared link on web link |
| PUT | /web_links/{web_link_id}#remove_shared_link | Remove shared link from web link |

### shared_items#web_links
| Method | Path | Description |
|--------|------|-------------|
| GET | /shared_items#web_links | Find web link for shared link |

### shared_items#app_items
| Method | Path | Description |
|--------|------|-------------|
| GET | /shared_items#app_items | Find app item for shared link |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | List enterprise users |
| POST | /users | Create user |
| GET | /users/me | Get current user |
| POST | /users/terminate_sessions | Create jobs to terminate users session |
| GET | /users/{user_id} | Get user |
| PUT | /users/{user_id} | Update user |
| DELETE | /users/{user_id} | Delete user |
| GET | /users/{user_id}/avatar | Get user avatar |
| POST | /users/{user_id}/avatar | Add or update user avatar |
| DELETE | /users/{user_id}/avatar | Delete user avatar |
| PUT | /users/{user_id}/folders/0 | Transfer owned folders |
| GET | /users/{user_id}/email_aliases | List user's email aliases |
| POST | /users/{user_id}/email_aliases | Create email alias |
| DELETE | /users/{user_id}/email_aliases/{email_alias_id} | Remove email alias |
| GET | /users/{user_id}/memberships | List user's groups |

### invites
| Method | Path | Description |
|--------|------|-------------|
| POST | /invites | Create user invite |
| GET | /invites/{invite_id} | Get user invite status |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | List groups for enterprise |
| POST | /groups | Create group |
| POST | /groups/terminate_sessions | Create jobs to terminate user group session |
| GET | /groups/{group_id} | Get group |
| PUT | /groups/{group_id} | Update group |
| DELETE | /groups/{group_id} | Remove group |
| GET | /groups/{group_id}/memberships | List members of group |
| GET | /groups/{group_id}/collaborations | List group collaborations |

### group_memberships
| Method | Path | Description |
|--------|------|-------------|
| POST | /group_memberships | Add user to group |
| GET | /group_memberships/{group_membership_id} | Get group membership |
| PUT | /group_memberships/{group_membership_id} | Update group membership |
| DELETE | /group_memberships/{group_membership_id} | Remove user from group |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks | List all webhooks |
| POST | /webhooks | Create webhook |
| GET | /webhooks/{webhook_id} | Get webhook |
| PUT | /webhooks/{webhook_id} | Update webhook |
| DELETE | /webhooks/{webhook_id} | Remove webhook |

### skill_invocations
| Method | Path | Description |
|--------|------|-------------|
| PUT | /skill_invocations/{skill_id} | Update all Box Skill cards on file |

### events
| Method | Path | Description |
|--------|------|-------------|
| OPTIONS | /events | Get events long poll endpoint |
| GET | /events | List user and enterprise events |

### collections
| Method | Path | Description |
|--------|------|-------------|
| GET | /collections | List all collections |
| GET | /collections/{collection_id}/items | List collection items |
| GET | /collections/{collection_id} | Get collection by ID |

### recent_items
| Method | Path | Description |
|--------|------|-------------|
| GET | /recent_items | List recently accessed items |

### retention_policies
| Method | Path | Description |
|--------|------|-------------|
| GET | /retention_policies | List retention policies |
| POST | /retention_policies | Create retention policy |
| GET | /retention_policies/{retention_policy_id} | Get retention policy |
| PUT | /retention_policies/{retention_policy_id} | Update retention policy |
| DELETE | /retention_policies/{retention_policy_id} | Delete retention policy |
| GET | /retention_policies/{retention_policy_id}/assignments | List retention policy assignments |

### retention_policy_assignments
| Method | Path | Description |
|--------|------|-------------|
| POST | /retention_policy_assignments | Assign retention policy |
| GET | /retention_policy_assignments/{retention_policy_assignment_id} | Get retention policy assignment |
| DELETE | /retention_policy_assignments/{retention_policy_assignment_id} | Remove retention policy assignment |
| GET | /retention_policy_assignments/{retention_policy_assignment_id}/files_under_retention | Get files under retention |
| GET | /retention_policy_assignments/{retention_policy_assignment_id}/file_versions_under_retention | Get file versions under retention |

### legal_hold_policies
| Method | Path | Description |
|--------|------|-------------|
| GET | /legal_hold_policies | List all legal hold policies |
| POST | /legal_hold_policies | Create legal hold policy |
| GET | /legal_hold_policies/{legal_hold_policy_id} | Get legal hold policy |
| PUT | /legal_hold_policies/{legal_hold_policy_id} | Update legal hold policy |
| DELETE | /legal_hold_policies/{legal_hold_policy_id} | Remove legal hold policy |

### legal_hold_policy_assignments
| Method | Path | Description |
|--------|------|-------------|
| GET | /legal_hold_policy_assignments | List legal hold policy assignments |
| POST | /legal_hold_policy_assignments | Assign legal hold policy |
| GET | /legal_hold_policy_assignments/{legal_hold_policy_assignment_id} | Get legal hold policy assignment |
| DELETE | /legal_hold_policy_assignments/{legal_hold_policy_assignment_id} | Unassign legal hold policy |
| GET | /legal_hold_policy_assignments/{legal_hold_policy_assignment_id}/files_on_hold | List files with current file versions for legal hold policy assignment |
| GET | /legal_hold_policy_assignments/{legal_hold_policy_assignment_id}/file_versions_on_hold | List previous file versions for legal hold policy assignment |

### file_version_retentions
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_version_retentions | List file version retentions |
| GET | /file_version_retentions/{file_version_retention_id} | Get retention on file |

### file_version_legal_holds
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_version_legal_holds/{file_version_legal_hold_id} | Get file version legal hold |
| GET | /file_version_legal_holds | List file version legal holds |

### shield_information_barriers
| Method | Path | Description |
|--------|------|-------------|
| GET | /shield_information_barriers/{shield_information_barrier_id} | Get shield information barrier with specified ID |
| POST | /shield_information_barriers/change_status | Add changed status of shield information barrier with specified ID |
| GET | /shield_information_barriers | List shield information barriers |
| POST | /shield_information_barriers | Create shield information barrier |

### shield_information_barrier_reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /shield_information_barrier_reports | List shield information barrier reports |
| POST | /shield_information_barrier_reports | Create shield information barrier report |
| GET | /shield_information_barrier_reports/{shield_information_barrier_report_id} | Get shield information barrier report by ID |

### shield_information_barrier_segments
| Method | Path | Description |
|--------|------|-------------|
| GET | /shield_information_barrier_segments/{shield_information_barrier_segment_id} | Get shield information barrier segment with specified ID |
| DELETE | /shield_information_barrier_segments/{shield_information_barrier_segment_id} | Delete shield information barrier segment |
| PUT | /shield_information_barrier_segments/{shield_information_barrier_segment_id} | Update shield information barrier segment with specified ID |
| GET | /shield_information_barrier_segments | List shield information barrier segments |
| POST | /shield_information_barrier_segments | Create shield information barrier segment |

### shield_information_barrier_segment_members
| Method | Path | Description |
|--------|------|-------------|
| GET | /shield_information_barrier_segment_members/{shield_information_barrier_segment_member_id} | Get shield information barrier segment member by ID |
| DELETE | /shield_information_barrier_segment_members/{shield_information_barrier_segment_member_id} | Delete shield information barrier segment member by ID |
| GET | /shield_information_barrier_segment_members | List shield information barrier segment members |
| POST | /shield_information_barrier_segment_members | Create shield information barrier segment member |

### shield_information_barrier_segment_restrictions
| Method | Path | Description |
|--------|------|-------------|
| GET | /shield_information_barrier_segment_restrictions/{shield_information_barrier_segment_restriction_id} | Get shield information barrier segment restriction by ID |
| DELETE | /shield_information_barrier_segment_restrictions/{shield_information_barrier_segment_restriction_id} | Delete shield information barrier segment restriction by ID |
| GET | /shield_information_barrier_segment_restrictions | List shield information barrier segment restrictions |
| POST | /shield_information_barrier_segment_restrictions | Create shield information barrier segment restriction |

### device_pinners
| Method | Path | Description |
|--------|------|-------------|
| GET | /device_pinners/{device_pinner_id} | Get device pin |
| DELETE | /device_pinners/{device_pinner_id} | Remove device pin |

### enterprises
| Method | Path | Description |
|--------|------|-------------|
| GET | /enterprises/{enterprise_id}/device_pinners | List enterprise device pins |

### terms_of_services
| Method | Path | Description |
|--------|------|-------------|
| GET | /terms_of_services | List terms of services |
| POST | /terms_of_services | Create terms of service |
| GET | /terms_of_services/{terms_of_service_id} | Get terms of service |
| PUT | /terms_of_services/{terms_of_service_id} | Update terms of service |

### terms_of_service_user_statuses
| Method | Path | Description |
|--------|------|-------------|
| GET | /terms_of_service_user_statuses | List terms of service user statuses |
| POST | /terms_of_service_user_statuses | Create terms of service status for new user |
| PUT | /terms_of_service_user_statuses/{terms_of_service_user_status_id} | Update terms of service status for existing user |

### collaboration_whitelist_entries
| Method | Path | Description |
|--------|------|-------------|
| GET | /collaboration_whitelist_entries | List allowed collaboration domains |
| POST | /collaboration_whitelist_entries | Add domain to list of allowed collaboration domains |
| GET | /collaboration_whitelist_entries/{collaboration_whitelist_entry_id} | Get allowed collaboration domain |
| DELETE | /collaboration_whitelist_entries/{collaboration_whitelist_entry_id} | Remove domain from list of allowed collaboration domains |

### collaboration_whitelist_exempt_targets
| Method | Path | Description |
|--------|------|-------------|
| GET | /collaboration_whitelist_exempt_targets | List users exempt from collaboration domain restrictions |
| POST | /collaboration_whitelist_exempt_targets | Create user exemption from collaboration domain restrictions |
| GET | /collaboration_whitelist_exempt_targets/{collaboration_whitelist_exempt_target_id} | Get user exempt from collaboration domain restrictions |
| DELETE | /collaboration_whitelist_exempt_targets/{collaboration_whitelist_exempt_target_id} | Remove user from list of users exempt from domain restrictions |

### storage_policies
| Method | Path | Description |
|--------|------|-------------|
| GET | /storage_policies | List storage policies |
| GET | /storage_policies/{storage_policy_id} | Get storage policy |

### storage_policy_assignments
| Method | Path | Description |
|--------|------|-------------|
| GET | /storage_policy_assignments | List storage policy assignments |
| POST | /storage_policy_assignments | Assign storage policy |
| GET | /storage_policy_assignments/{storage_policy_assignment_id} | Get storage policy assignment |
| PUT | /storage_policy_assignments/{storage_policy_assignment_id} | Update storage policy assignment |
| DELETE | /storage_policy_assignments/{storage_policy_assignment_id} | Unassign storage policy |

### zip_downloads
| Method | Path | Description |
|--------|------|-------------|
| POST | /zip_downloads | Create zip download |
| GET | /zip_downloads/{zip_download_id}/content | Download zip archive |
| GET | /zip_downloads/{zip_download_id}/status | Get zip download status |

### sign_requests
| Method | Path | Description |
|--------|------|-------------|
| POST | /sign_requests/{sign_request_id}/cancel | Cancel Box Sign request |
| POST | /sign_requests/{sign_request_id}/resend | Resend Box Sign request |
| GET | /sign_requests/{sign_request_id} | Get Box Sign request by ID |
| GET | /sign_requests | List Box Sign requests |
| POST | /sign_requests | Create Box Sign request |

### workflows
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflows | List workflows |
| POST | /workflows/{workflow_id}/start | Starts workflow based on request body |

### sign_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /sign_templates | List Box Sign templates |
| GET | /sign_templates/{template_id} | Get Box Sign template by ID |

### integration_mappings
| Method | Path | Description |
|--------|------|-------------|
| GET | /integration_mappings/slack | List Slack integration mappings |
| POST | /integration_mappings/slack | Create Slack integration mapping |
| PUT | /integration_mappings/slack/{integration_mapping_id} | Update Slack integration mapping |
| DELETE | /integration_mappings/slack/{integration_mapping_id} | Delete Slack integration mapping |
| GET | /integration_mappings/teams | List Teams integration mappings |
| POST | /integration_mappings/teams | Create Teams integration mapping |
| PUT | /integration_mappings/teams/{integration_mapping_id} | Update Teams integration mapping |
| DELETE | /integration_mappings/teams/{integration_mapping_id} | Delete Teams integration mapping |

### ai
| Method | Path | Description |
|--------|------|-------------|
| POST | /ai/ask | Ask question |
| POST | /ai/text_gen | Generate text |
| POST | /ai/extract | Extract metadata (freeform) |
| POST | /ai/extract_structured | Extract metadata (structured) |

### ai_agent_default
| Method | Path | Description |
|--------|------|-------------|
| GET | /ai_agent_default | Get AI agent default configuration |

### ai_agents
| Method | Path | Description |
|--------|------|-------------|
| GET | /ai_agents | List AI agents |
| POST | /ai_agents | Create AI agent |
| PUT | /ai_agents/{agent_id} | Update AI agent |
| GET | /ai_agents/{agent_id} | Get AI agent by agent ID |
| DELETE | /ai_agents/{agent_id} | Delete AI agent |

### metadata_taxonomies
| Method | Path | Description |
|--------|------|-------------|
| POST | /metadata_taxonomies | Create metadata taxonomy |
| GET | /metadata_taxonomies/{namespace} | Get metadata taxonomies for namespace |
| GET | /metadata_taxonomies/{namespace}/{taxonomy_key} | Get metadata taxonomy by taxonomy key |
| PATCH | /metadata_taxonomies/{namespace}/{taxonomy_key} | Update metadata taxonomy |
| DELETE | /metadata_taxonomies/{namespace}/{taxonomy_key} | Remove metadata taxonomy |
| POST | /metadata_taxonomies/{namespace}/{taxonomy_key}/levels | Create metadata taxonomy levels |
| PATCH | /metadata_taxonomies/{namespace}/{taxonomy_key}/levels/{level_index} | Update metadata taxonomy level |
| POST | /metadata_taxonomies/{namespace}/{taxonomy_key}/levels:append | Add metadata taxonomy level |
| POST | /metadata_taxonomies/{namespace}/{taxonomy_key}/levels:trim | Delete metadata taxonomy level |
| GET | /metadata_taxonomies/{namespace}/{taxonomy_key}/nodes | List metadata taxonomy nodes |
| POST | /metadata_taxonomies/{namespace}/{taxonomy_key}/nodes | Create metadata taxonomy node |
| GET | /metadata_taxonomies/{namespace}/{taxonomy_key}/nodes/{node_id} | Get metadata taxonomy node by ID |
| PATCH | /metadata_taxonomies/{namespace}/{taxonomy_key}/nodes/{node_id} | Update metadata taxonomy node |
| DELETE | /metadata_taxonomies/{namespace}/{taxonomy_key}/nodes/{node_id} | Remove metadata taxonomy node |

## Enhanced Skill Content
## Question Mapping

- "How do I upload a file to Box?" -> POST /files/content
- "How do I download a file?" -> GET /files/{file_id}/content
- "How do I search for files or folders?" -> GET /search
- "How do I create a new folder?" -> POST /folders
- "How do I share a file with someone?" -> POST /collaborations
- "How do I get info about the current user?" -> GET /users/me
- "How do I move a file to a different folder?" -> PUT /files/{file_id} (update parent)
- "How do I create a shared link for a file?" -> PUT /files/{file_id}#add_shared_link
- "How do I set up a webhook for file changes?" -> POST /webhooks
- "How do I ask Box AI a question about a document?" -> POST /ai/ask
- "How do I list all items in a folder?" -> GET /folders/{folder_id}/items
- "How do I restore a file from trash?" -> POST /files/{file_id}/versions/current
- "How do I create a sign request?" -> POST /sign_requests
- "How do I add metadata to a file?" -> POST /files/{file_id}/metadata/{scope}/{template_key}
- "How do I upload a large file in chunks?" -> POST /files/upload_sessions then PUT parts then POST commit

## Response Tips

- **Files/Folders listings**: Paginated via `offset`/`limit` or `marker`-based. Check `total_count` and `entries[]` array. Use `fields` param to limit response size.
- **Search**: Returns relevance-sorted results by default. Use `offset`/`limit` for paging (max 30 default). Empty `entries` means no matches, not an error.
- **Collaborations**: Nested `accessible_by`, `item`, and `acceptance_requirements_status` objects. Role field is one of editor/viewer/previewer/uploader/co-owner/owner.
- **Upload sessions (chunked)**: 201 on session create, 200 on each part upload. Commit may return 202 (still processing) -- poll until 201.
- **Events**: Uses `next_stream_position` for long-polling. `chunk_size` indicates entries returned, not total available.
- **Sign requests**: 201 on creation, but actual signing is async. Poll the sign request ID for status updates.
- **AI endpoints**: May return 204 (no content) if the model has no answer. 500 errors indicate AI processing failures, not auth issues.
- **Metadata**: Uses JSON Patch operations for PUT updates. 409 means metadata instance already exists -- use PUT to update instead of POST.
- **Shared items**: Requires `boxapi` header in format `shared_link=URL&shared_link_password=PASSWORD`, not a query parameter.

## Anomaly Flags

- **412 Precondition Failed**: ETags are stale. Surface when `if-match` fails -- the item was modified by another client since last fetch.
- **409 Conflict with `operation_blocked_temporary`**: Box is temporarily blocking the operation (e.g., during a move/copy). Retry after a short delay. Surface this distinctly from permanent 409s.
- **202 Accepted on downloads**: File content isn't ready yet (e.g., newly uploaded). Agent should advise polling or waiting before retrying.
- **302 on file content GET**: Box redirects to the actual download URL. If the client doesn't follow redirects, surface the Location header.
- **429 Rate Limit**: Zip downloads and session termination endpoints explicitly return 429. Surface the Retry-After header value.
- **401 on shared items**: Token may have expired. Surface OAuth refresh flow before retrying.
- **Chunked upload session expiry**: `session_expires_at` is returned on creation. Flag if upload is taking long relative to expiry.
- **Legal hold 202 on delete**: Deletion is async and queued. Surface that the policy isn't immediately removed.
- **AI 500 errors**: These indicate AI model failures, not server errors. Surface as "AI processing unavailable" rather than generic server error.

## Playbook

### 1. Upload a Large File via Chunked Upload

1. Call `POST /files/upload_sessions` with `folder_id`, `file_name`, and `file_size` to create a session
2. Note the returned `part_size` and `total_parts` from the 201 response
3. Split the file into chunks of `part_size` bytes
4. For each chunk, call `PUT /files/upload_sessions/{upload_session_id}` with the `digest` (SHA1) and `content-range` header
5. After all parts upload, call `POST /files/upload_sessions/{upload_session_id}/commit` with the `digest` of the full file and array of `parts`
6. If commit returns 202, poll `GET /files/upload_sessions/{upload_session_id}` until `num_parts_processed` equals `total_parts`, then retry commit
7. On 201, the file is ready in `entries[0]`

### 2. Share a File Externally with Expiring Link

1. Call `GET /files/{file_id}` to confirm the file exists and you have access
2. Call `PUT /files/{file_id}#add_shared_link` with `fields=shared_link` and body: `shared_link: { access: "open", unshared_at: "<expiry_datetime>", permissions: { can_download: true } }`
3. Extract the shared link URL from `shared_link.url` in the response
4. To later revoke access, call `PUT /files/{file_id}#remove_shared_link` with `fields=shared_link` and body: `shared_link: null`

### 3. Set Up Metadata-Driven Search

1. Create a metadata template: `POST /metadata_templates/schema` with `scope: "enterprise"`, `displayName`, and `fields` array defining your custom attributes
2. Apply metadata to files: `POST /files/{file_id}/metadata/enterprise/{template_key}` with field values in the body
3. Optionally set a cascade policy: `POST /metadata_cascade_policies` with `folder_id`, `scope: "enterprise"`, and `templateKey` to auto-apply to folder contents
4. Query using `POST /metadata_queries/execute_read` with `from: "enterprise_{template_key}"`, `ancestor_folder_id`, and a `query` string using SQL-like syntax against your metadata fields

### 4. Assign and Track a Review Task

1. Create a task on a file: `POST /tasks` with `item: { id: "<file_id>", type: "file" }`, `action: "review"`, `message`, and optional `due_at`
2. Assign the task: `POST /task_assignments` with `task: { id: "<task_id>", type: "task" }` and `assign_to: { login: "user@example.com" }`
3. Check assignment status: `GET /tasks/{task_id}/assignments` and inspect each entry's `resolution_state`
4. Assignee completes their review: `PUT /task_assignments/{task_assignment_id}` with `resolution_state: "approved"` or `"rejected"`
5. Verify completion: `GET /tasks/{task_id}` and check `is_completed` flag

### 5. Use Box AI to Summarize Documents

1. Identify target files by searching or listing: `GET /search?query=quarterly+report&file_extensions=pdf,docx`
2. Gather file IDs from `entries[].id` in the search results
3. Call `POST /ai/ask` with `mode: "multiple_item_qa"`, `prompt: "Summarize the key findings"`, and `items` array containing each file's `id` and `type: "file"`
4. If the response is 204, the AI had insufficient content -- try with fewer or different files
5. For follow-up questions, include the previous exchange in `dialogue_history` to maintain conversational context


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object
- Error responses use types: `bad_request`, `forbidden`, `not_found`, `operation_blocked_temporary`

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
