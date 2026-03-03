---
name: telnyx-api
description: "Telnyx API skill. Use when working with Telnyx for .well-known, 10dlc, access_ip_address. Covers 946 endpoints."
version: 1.0.0
generator: lapsh
---

# Telnyx API
API version: 2.0.0

## Auth
Bearer bearer | OAuth2 | Bearer bearer | Bearer bearer

## Base URL
https://api.telnyx.com/v2

## Setup
1. Set Authorization header with your Bearer token
2. GET /.well-known/oauth-authorization-server -- verify access
3. POST /10dlc/brand -- create first brand

## Endpoints

946 endpoints across 154 groups. See references/api-spec.lap for full details.

### .well-known
| Method | Path | Description |
|--------|------|-------------|
| GET | /.well-known/oauth-authorization-server | Authorization server metadata |
| GET | /.well-known/oauth-protected-resource | Protected resource metadata |

### 10dlc
| Method | Path | Description |
|--------|------|-------------|
| GET | /10dlc/brand | List Brands |
| POST | /10dlc/brand | Create Brand |
| GET | /10dlc/brand/feedback/{brandId} | Get Brand Feedback By Id |
| GET | /10dlc/brand/smsOtp/{referenceId} | Get Brand SMS OTP Status |
| DELETE | /10dlc/brand/{brandId} | Delete Brand |
| GET | /10dlc/brand/{brandId} | Get Brand |
| PUT | /10dlc/brand/{brandId} | Update Brand |
| POST | /10dlc/brand/{brandId}/2faEmail | Resend brand 2FA email |
| GET | /10dlc/brand/{brandId}/externalVetting | List External Vettings |
| POST | /10dlc/brand/{brandId}/externalVetting | Order Brand External Vetting |
| PUT | /10dlc/brand/{brandId}/externalVetting | Import External Vetting Record |
| PUT | /10dlc/brand/{brandId}/revet | Revet Brand |
| GET | /10dlc/brand/{brandId}/smsOtp | Get Brand SMS OTP Status by Brand ID |
| POST | /10dlc/brand/{brandId}/smsOtp | Trigger Brand SMS OTP |
| PUT | /10dlc/brand/{brandId}/smsOtp | Verify Brand SMS OTP |
| GET | /10dlc/campaign | List Campaigns |
| POST | /10dlc/campaign/acceptSharing/{campaignId} | Accept Shared Campaign |
| GET | /10dlc/campaign/usecase/cost | Get Campaign Cost |
| DELETE | /10dlc/campaign/{campaignId} | Deactivate campaign |
| GET | /10dlc/campaign/{campaignId} | Get campaign |
| PUT | /10dlc/campaign/{campaignId} | Update campaign |
| POST | /10dlc/campaign/{campaignId}/appeal | Submit campaign appeal for manual review |
| GET | /10dlc/campaign/{campaignId}/mnoMetadata | Get Campaign Mno Metadata |
| GET | /10dlc/campaign/{campaignId}/operationStatus | Get campaign operation status |
| GET | /10dlc/campaign/{campaignId}/osr/attributes | Get OSR campaign attributes |
| GET | /10dlc/campaign/{campaignId}/sharing | Get Sharing Status |
| POST | /10dlc/campaignBuilder | Submit Campaign |
| GET | /10dlc/campaignBuilder/brand/{brandId}/usecase/{usecase} | Qualify By Usecase |
| GET | /10dlc/enum/{endpoint} | Get Enum |
| GET | /10dlc/partnerCampaign/sharedByMe | List shared partner campaigns |
| GET | /10dlc/partnerCampaign/{campaignId}/sharing | Get Sharing Status |
| GET | /10dlc/partner_campaigns | List Shared Campaigns |
| GET | /10dlc/partner_campaigns/{campaignId} | Get Single Shared Campaign |
| PATCH | /10dlc/partner_campaigns/{campaignId} | Update Single Shared Campaign |
| POST | /10dlc/phoneNumberAssignmentByProfile | Assign Messaging Profile To Campaign |
| GET | /10dlc/phoneNumberAssignmentByProfile/{taskId} | Get Assignment Task Status |
| GET | /10dlc/phoneNumberAssignmentByProfile/{taskId}/phoneNumbers | Get Phone Number Status |
| GET | /10dlc/phone_number_campaigns | List phone number campaigns |
| POST | /10dlc/phone_number_campaigns | Create New Phone Number Campaign |
| DELETE | /10dlc/phone_number_campaigns/{phoneNumber} | Delete Phone Number Campaign |
| GET | /10dlc/phone_number_campaigns/{phoneNumber} | Get Single Phone Number Campaign |
| PUT | /10dlc/phone_number_campaigns/{phoneNumber} | Create New Phone Number Campaign |

### access_ip_address
| Method | Path | Description |
|--------|------|-------------|
| GET | /access_ip_address | List all Access IP Addresses |
| POST | /access_ip_address | Create new Access IP Address |
| DELETE | /access_ip_address/{access_ip_address_id} | Delete access IP address |
| GET | /access_ip_address/{access_ip_address_id} | Retrieve an access IP address |

### access_ip_ranges
| Method | Path | Description |
|--------|------|-------------|
| GET | /access_ip_ranges | List all Access IP Ranges |
| POST | /access_ip_ranges | Create new Access IP Range |
| DELETE | /access_ip_ranges/{access_ip_range_id} | Delete access IP ranges |

### actions
| Method | Path | Description |
|--------|------|-------------|
| POST | /actions/purchase/esims | Purchase eSIMs |
| POST | /actions/register/sim_cards | Register SIM cards |

### addresses
| Method | Path | Description |
|--------|------|-------------|
| GET | /addresses | List all addresses |
| POST | /addresses | Creates an address |
| POST | /addresses/actions/validate | Validate an address |
| DELETE | /addresses/{id} | Deletes an address |
| GET | /addresses/{id} | Retrieve an address |
| POST | /addresses/{id}/actions/accept_suggestions | Accepts this address suggestion as a new emergency address for Operator Connect and finishes the uploads of the numbers associated with it to Microsoft. |

### advanced_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /advanced_orders | List Advanced Orders |
| POST | /advanced_orders | Create Advanced Order |
| PATCH | /advanced_orders/{advanced-order-id}/requirement_group | Update Advanced Order |
| GET | /advanced_orders/{order_id} | Get Advanced Order |

### ai
| Method | Path | Description |
|--------|------|-------------|
| GET | /ai/assistants | List assistants |
| POST | /ai/assistants | Create an assistant |
| POST | /ai/assistants/import | Import assistants from external provider |
| GET | /ai/assistants/tests | List assistant tests with pagination |
| POST | /ai/assistants/tests | Create a new assistant test |
| GET | /ai/assistants/tests/test-suites | Get all test suite names |
| GET | /ai/assistants/tests/test-suites/{suite_name}/runs | Get test suite run history |
| POST | /ai/assistants/tests/test-suites/{suite_name}/runs | Trigger test suite execution |
| DELETE | /ai/assistants/tests/{test_id} | Delete an assistant test |
| GET | /ai/assistants/tests/{test_id} | Get assistant test by ID |
| PUT | /ai/assistants/tests/{test_id} | Update an assistant test |
| GET | /ai/assistants/tests/{test_id}/runs | Get test run history for a specific test |
| POST | /ai/assistants/tests/{test_id}/runs | Trigger a manual test run |
| GET | /ai/assistants/tests/{test_id}/runs/{run_id} | Get specific test run details |
| DELETE | /ai/assistants/{assistant_id} | Delete an assistant |
| GET | /ai/assistants/{assistant_id} | Get an assistant |
| POST | /ai/assistants/{assistant_id} | Update an assistant |
| DELETE | /ai/assistants/{assistant_id}/canary-deploys | Delete Canary Deploy |
| GET | /ai/assistants/{assistant_id}/canary-deploys | Get Canary Deploy |
| POST | /ai/assistants/{assistant_id}/canary-deploys | Create Canary Deploy |
| PUT | /ai/assistants/{assistant_id}/canary-deploys | Update Canary Deploy |
| POST | /ai/assistants/{assistant_id}/chat | Assistant Chat (BETA) |
| POST | /ai/assistants/{assistant_id}/chat/sms | Assistant Sms Chat |
| POST | /ai/assistants/{assistant_id}/clone | Clone Assistant |
| GET | /ai/assistants/{assistant_id}/scheduled_events | List scheduled events |
| POST | /ai/assistants/{assistant_id}/scheduled_events | Create a scheduled event |
| DELETE | /ai/assistants/{assistant_id}/scheduled_events/{event_id} | Delete a scheduled event |
| GET | /ai/assistants/{assistant_id}/scheduled_events/{event_id} | Get a scheduled event |
| GET | /ai/assistants/{assistant_id}/texml | Get assistant texml |
| POST | /ai/assistants/{assistant_id}/tools/{tool_id}/test | Test Assistant Tool |
| GET | /ai/assistants/{assistant_id}/versions | Get all versions of an assistant |
| DELETE | /ai/assistants/{assistant_id}/versions/{version_id} | Delete a specific assistant version |
| GET | /ai/assistants/{assistant_id}/versions/{version_id} | Get a specific assistant version |
| POST | /ai/assistants/{assistant_id}/versions/{version_id} | Update a specific assistant version |
| POST | /ai/assistants/{assistant_id}/versions/{version_id}/promote | Promote an assistant version to main |
| POST | /ai/audio/transcriptions | Transcribe speech to text |
| POST | /ai/chat/completions | Create a chat completion |
| GET | /ai/clusters | List all clusters |
| POST | /ai/clusters | Compute new clusters |
| DELETE | /ai/clusters/{task_id} | Delete a cluster |
| GET | /ai/clusters/{task_id} | Fetch a cluster |
| GET | /ai/clusters/{task_id}/graph | Fetch a cluster visualization |
| GET | /ai/conversations | List conversations |
| POST | /ai/conversations | Create a conversation |
| GET | /ai/conversations/insight-groups | Get Insight Template Groups |
| POST | /ai/conversations/insight-groups | Create Insight Template Group |
| DELETE | /ai/conversations/insight-groups/{group_id} | Delete Insight Template Group |
| GET | /ai/conversations/insight-groups/{group_id} | Get Insight Template Group |
| PUT | /ai/conversations/insight-groups/{group_id} | Update Insight Template Group |
| POST | /ai/conversations/insight-groups/{group_id}/insights/{insight_id}/assign | Assign Insight Template To Group |
| DELETE | /ai/conversations/insight-groups/{group_id}/insights/{insight_id}/unassign | Unassign Insight Template From Group |
| GET | /ai/conversations/insights | Get Insight Templates |
| POST | /ai/conversations/insights | Create Insight Template |
| DELETE | /ai/conversations/insights/{insight_id} | Delete Insight Template |
| GET | /ai/conversations/insights/{insight_id} | Get Insight Template |
| PUT | /ai/conversations/insights/{insight_id} | Update Insight Template |
| DELETE | /ai/conversations/{conversation_id} | Delete a conversation |
| GET | /ai/conversations/{conversation_id} | Get a conversation |
| PUT | /ai/conversations/{conversation_id} | Update conversation metadata |
| GET | /ai/conversations/{conversation_id}/conversations-insights | Get insights for a conversation |
| POST | /ai/conversations/{conversation_id}/message | Create Message |
| GET | /ai/conversations/{conversation_id}/messages | Get conversation messages |
| GET | /ai/embeddings | Get Tasks by Status |
| POST | /ai/embeddings | Embed documents |
| GET | /ai/embeddings/buckets | List embedded buckets |
| DELETE | /ai/embeddings/buckets/{bucket_name} | Disable AI for an Embedded Bucket |
| GET | /ai/embeddings/buckets/{bucket_name} | Get file-level embedding statuses for a bucket |
| POST | /ai/embeddings/similarity-search | Search for documents |
| POST | /ai/embeddings/url | Embed URL content |
| GET | /ai/embeddings/{task_id} | Get an embedding task's status |
| GET | /ai/fine_tuning/jobs | List fine tuning jobs |
| POST | /ai/fine_tuning/jobs | Create a fine tuning job |
| GET | /ai/fine_tuning/jobs/{job_id} | Get a fine tuning job |
| POST | /ai/fine_tuning/jobs/{job_id}/cancel | Cancel a fine tuning job |
| GET | /ai/integrations | List Integrations |
| GET | /ai/integrations/connections | List User Integrations |
| DELETE | /ai/integrations/connections/{user_connection_id} | Delete Integration Connection |
| GET | /ai/integrations/connections/{user_connection_id} | Get User Integration connection By Id |
| GET | /ai/integrations/{integration_id} | List Integration By Id |
| GET | /ai/mcp_servers | List MCP Servers |
| POST | /ai/mcp_servers | Create MCP Server |
| DELETE | /ai/mcp_servers/{mcp_server_id} | Delete MCP Server |
| GET | /ai/mcp_servers/{mcp_server_id} | Get MCP Server |
| PUT | /ai/mcp_servers/{mcp_server_id} | Update MCP Server |
| GET | /ai/missions | List missions |
| POST | /ai/missions | Create mission |
| GET | /ai/missions/events | List recent events |
| GET | /ai/missions/runs | List recent runs |
| DELETE | /ai/missions/{mission_id} | Delete mission |
| GET | /ai/missions/{mission_id} | Get mission |
| PUT | /ai/missions/{mission_id} | Update mission |
| POST | /ai/missions/{mission_id}/clone | Clone mission |
| GET | /ai/missions/{mission_id}/knowledge-bases | List knowledge bases |
| POST | /ai/missions/{mission_id}/knowledge-bases | Create knowledge base |
| DELETE | /ai/missions/{mission_id}/knowledge-bases/{knowledge_base_id} | Delete knowledge base |
| GET | /ai/missions/{mission_id}/knowledge-bases/{knowledge_base_id} | Get knowledge base |
| PUT | /ai/missions/{mission_id}/knowledge-bases/{knowledge_base_id} | Update knowledge base |
| GET | /ai/missions/{mission_id}/mcp-servers | List MCP servers |
| POST | /ai/missions/{mission_id}/mcp-servers | Create MCP server |
| DELETE | /ai/missions/{mission_id}/mcp-servers/{mcp_server_id} | Delete MCP server |
| GET | /ai/missions/{mission_id}/mcp-servers/{mcp_server_id} | Get MCP server |
| PUT | /ai/missions/{mission_id}/mcp-servers/{mcp_server_id} | Update MCP server |
| GET | /ai/missions/{mission_id}/runs | List runs for mission |
| POST | /ai/missions/{mission_id}/runs | Start a run |
| GET | /ai/missions/{mission_id}/runs/{run_id} | Get run details |
| PATCH | /ai/missions/{mission_id}/runs/{run_id} | Update run |
| POST | /ai/missions/{mission_id}/runs/{run_id}/cancel | Cancel run |
| GET | /ai/missions/{mission_id}/runs/{run_id}/events | List events |
| POST | /ai/missions/{mission_id}/runs/{run_id}/events | Log event |
| GET | /ai/missions/{mission_id}/runs/{run_id}/events/{event_id} | Get event details |
| POST | /ai/missions/{mission_id}/runs/{run_id}/pause | Pause run |
| GET | /ai/missions/{mission_id}/runs/{run_id}/plan | Get plan |
| POST | /ai/missions/{mission_id}/runs/{run_id}/plan | Create initial plan |
| POST | /ai/missions/{mission_id}/runs/{run_id}/plan/steps | Add step(s) to plan |
| GET | /ai/missions/{mission_id}/runs/{run_id}/plan/steps/{step_id} | Get step details |
| PATCH | /ai/missions/{mission_id}/runs/{run_id}/plan/steps/{step_id} | Update step status |
| POST | /ai/missions/{mission_id}/runs/{run_id}/resume | Resume run |
| GET | /ai/missions/{mission_id}/runs/{run_id}/telnyx-agents | List linked Telnyx agents |
| POST | /ai/missions/{mission_id}/runs/{run_id}/telnyx-agents | Link Telnyx agent to run |
| DELETE | /ai/missions/{mission_id}/runs/{run_id}/telnyx-agents/{telnyx_agent_id} | Unlink Telnyx agent |
| GET | /ai/missions/{mission_id}/tools | List tools |
| POST | /ai/missions/{mission_id}/tools | Create tool |
| DELETE | /ai/missions/{mission_id}/tools/{tool_id} | Delete tool |
| GET | /ai/missions/{mission_id}/tools/{tool_id} | Get tool |
| PUT | /ai/missions/{mission_id}/tools/{tool_id} | Update tool |
| GET | /ai/models | Get available models |
| POST | /ai/openai/embeddings | Create embeddings |
| GET | /ai/openai/embeddings/models | List embedding models |
| POST | /ai/summarize | Summarize file content |

### alphanumeric_sender_ids
| Method | Path | Description |
|--------|------|-------------|
| GET | /alphanumeric_sender_ids | List alphanumeric sender IDs |
| POST | /alphanumeric_sender_ids | Create an alphanumeric sender ID |
| DELETE | /alphanumeric_sender_ids/{id} | Delete an alphanumeric sender ID |
| GET | /alphanumeric_sender_ids/{id} | Retrieve an alphanumeric sender ID |

### audit_events
| Method | Path | Description |
|--------|------|-------------|
| GET | /audit_events | List Audit Logs |

### authentication_providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /authentication_providers | List all SSO authentication providers |
| POST | /authentication_providers | Creates an authentication provider |
| DELETE | /authentication_providers/{id} | Deletes an authentication provider |
| GET | /authentication_providers/{id} | Retrieve an authentication provider |
| PATCH | /authentication_providers/{id} | Update an authentication provider |

### available_phone_number_blocks
| Method | Path | Description |
|--------|------|-------------|
| GET | /available_phone_number_blocks | List available phone number blocks |

### available_phone_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /available_phone_numbers | List available phone numbers |

### balance
| Method | Path | Description |
|--------|------|-------------|
| GET | /balance | Get user balance details |

### billing_groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /billing_groups | List all billing groups |
| POST | /billing_groups | Create a billing group |
| DELETE | /billing_groups/{id} | Delete a billing group |
| GET | /billing_groups/{id} | Get a billing group |
| PATCH | /billing_groups/{id} | Update a billing group |

### bulk_sim_card_actions
| Method | Path | Description |
|--------|------|-------------|
| GET | /bulk_sim_card_actions | List bulk SIM card actions |
| GET | /bulk_sim_card_actions/{id} | Get bulk SIM card action details |

### bundle_pricing
| Method | Path | Description |
|--------|------|-------------|
| GET | /bundle_pricing/billing_bundles | Retrieve Bundles |
| GET | /bundle_pricing/billing_bundles/{bundle_id} | Get Bundle By Id |
| GET | /bundle_pricing/user_bundles | Get User Bundles |
| POST | /bundle_pricing/user_bundles/bulk | Create User Bundles |
| GET | /bundle_pricing/user_bundles/unused | Get Unused User Bundles |
| DELETE | /bundle_pricing/user_bundles/{user_bundle_id} | Deactivate User Bundle |
| GET | /bundle_pricing/user_bundles/{user_bundle_id} | Get User Bundle by Id |
| GET | /bundle_pricing/user_bundles/{user_bundle_id}/resources | Get User Bundle Resources |

### call_control_applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /call_control_applications | List call control applications |
| POST | /call_control_applications | Create a call control application |
| DELETE | /call_control_applications/{id} | Delete a call control application |
| GET | /call_control_applications/{id} | Retrieve a call control application |
| PATCH | /call_control_applications/{id} | Update a call control application |

### call_events
| Method | Path | Description |
|--------|------|-------------|
| GET | /call_events | List call events |

### calls
| Method | Path | Description |
|--------|------|-------------|
| POST | /calls | Dial |
| GET | /calls/{call_control_id} | Retrieve a call status |
| POST | /calls/{call_control_id}/actions/ai_assistant_add_messages | Add messages to AI Assistant |
| POST | /calls/{call_control_id}/actions/ai_assistant_start | Start AI Assistant |
| POST | /calls/{call_control_id}/actions/ai_assistant_stop | Stop AI Assistant |
| POST | /calls/{call_control_id}/actions/answer | Answer call |
| POST | /calls/{call_control_id}/actions/bridge | Bridge calls |
| PUT | /calls/{call_control_id}/actions/client_state_update | Update client state |
| POST | /calls/{call_control_id}/actions/enqueue | Enqueue call |
| POST | /calls/{call_control_id}/actions/fork_start | Forking start |
| POST | /calls/{call_control_id}/actions/fork_stop | Forking stop |
| POST | /calls/{call_control_id}/actions/gather | Gather |
| POST | /calls/{call_control_id}/actions/gather_stop | Gather stop |
| POST | /calls/{call_control_id}/actions/gather_using_ai | Gather using AI |
| POST | /calls/{call_control_id}/actions/gather_using_audio | Gather using audio |
| POST | /calls/{call_control_id}/actions/gather_using_speak | Gather using speak |
| POST | /calls/{call_control_id}/actions/hangup | Hangup call |
| POST | /calls/{call_control_id}/actions/leave_queue | Remove call from a queue |
| POST | /calls/{call_control_id}/actions/playback_start | Play audio URL |
| POST | /calls/{call_control_id}/actions/playback_stop | Stop audio playback |
| POST | /calls/{call_control_id}/actions/record_pause | Record pause |
| POST | /calls/{call_control_id}/actions/record_resume | Record resume |
| POST | /calls/{call_control_id}/actions/record_start | Recording start |
| POST | /calls/{call_control_id}/actions/record_stop | Recording stop |
| POST | /calls/{call_control_id}/actions/refer | SIP Refer a call |
| POST | /calls/{call_control_id}/actions/reject | Reject a call |
| POST | /calls/{call_control_id}/actions/send_dtmf | Send DTMF |
| POST | /calls/{call_control_id}/actions/send_sip_info | Send SIP info |
| POST | /calls/{call_control_id}/actions/siprec_start | SIPREC start |
| POST | /calls/{call_control_id}/actions/siprec_stop | SIPREC stop |
| POST | /calls/{call_control_id}/actions/speak | Speak text |
| POST | /calls/{call_control_id}/actions/streaming_start | Streaming start |
| POST | /calls/{call_control_id}/actions/streaming_stop | Streaming stop |
| POST | /calls/{call_control_id}/actions/suppression_start | Noise Suppression Start (BETA) |
| POST | /calls/{call_control_id}/actions/suppression_stop | Noise Suppression Stop (BETA) |
| POST | /calls/{call_control_id}/actions/switch_supervisor_role | Switch supervisor role |
| POST | /calls/{call_control_id}/actions/transcription_start | Transcription start |
| POST | /calls/{call_control_id}/actions/transcription_stop | Transcription stop |
| POST | /calls/{call_control_id}/actions/transfer | Transfer call |

### channel_zones
| Method | Path | Description |
|--------|------|-------------|
| GET | /channel_zones | List your voice channels for non-US zones |
| PUT | /channel_zones/{channel_zone_id} | Update voice channels for non-US Zones |

### charges_breakdown
| Method | Path | Description |
|--------|------|-------------|
| GET | /charges_breakdown | Get monthly charges breakdown |

### charges_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /charges_summary | Get monthly charges summary |

### comments
| Method | Path | Description |
|--------|------|-------------|
| GET | /comments | Retrieve all comments |
| POST | /comments | Create a comment |
| GET | /comments/{id} | Retrieve a comment |
| PATCH | /comments/{id}/read | Mark a comment as read |

### conferences
| Method | Path | Description |
|--------|------|-------------|
| GET | /conferences | List conferences |
| POST | /conferences | Create conference |
| GET | /conferences/{conference_id}/participants | List conference participants |
| GET | /conferences/{id} | Retrieve a conference |
| POST | /conferences/{id}/actions/end | End a conference |
| POST | /conferences/{id}/actions/gather_using_audio | Gather DTMF using audio prompt in a conference |
| POST | /conferences/{id}/actions/hold | Hold conference participants |
| POST | /conferences/{id}/actions/join | Join a conference |
| POST | /conferences/{id}/actions/leave | Leave a conference |
| POST | /conferences/{id}/actions/mute | Mute conference participants |
| POST | /conferences/{id}/actions/play | Play audio to conference participants |
| POST | /conferences/{id}/actions/record_pause | Conference recording pause |
| POST | /conferences/{id}/actions/record_resume | Conference recording resume |
| POST | /conferences/{id}/actions/record_start | Conference recording start |
| POST | /conferences/{id}/actions/record_stop | Conference recording stop |
| POST | /conferences/{id}/actions/send_dtmf | Send DTMF to conference participants |
| POST | /conferences/{id}/actions/speak | Speak text to conference participants |
| POST | /conferences/{id}/actions/stop | Stop audio being played on the conference |
| POST | /conferences/{id}/actions/unhold | Unhold conference participants |
| POST | /conferences/{id}/actions/unmute | Unmute conference participants |
| POST | /conferences/{id}/actions/update | Update conference participant |
| GET | /conferences/{id}/participants/{participant_id} | Retrieve a conference participant |
| PATCH | /conferences/{id}/participants/{participant_id} | Update a conference participant |

### connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /connections | List connections |
| GET | /connections/{connection_id}/active_calls | List all active calls for given connection |
| GET | /connections/{id} | Retrieve a connection |

### country_coverage
| Method | Path | Description |
|--------|------|-------------|
| GET | /country_coverage | Get country coverage |
| GET | /country_coverage/countries/{country_code} | Get coverage for a specific country |

### credential_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /credential_connections | List credential connections |
| POST | /credential_connections | Create a credential connection |
| DELETE | /credential_connections/{id} | Delete a credential connection |
| GET | /credential_connections/{id} | Retrieve a credential connection |
| PATCH | /credential_connections/{id} | Update a credential connection |
| POST | /credential_connections/{id}/actions/check_registration_status | Check a Credential Connection Registration Status |

### custom_storage_credentials
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /custom_storage_credentials/{connection_id} | Delete a stored credential |
| GET | /custom_storage_credentials/{connection_id} | Retrieve a stored credential |
| POST | /custom_storage_credentials/{connection_id} | Create a custom storage credential |
| PUT | /custom_storage_credentials/{connection_id} | Update a stored credential |

### customer_service_records
| Method | Path | Description |
|--------|------|-------------|
| GET | /customer_service_records | List customer service records |
| POST | /customer_service_records | Create a customer service record |
| POST | /customer_service_records/phone_number_coverages | Verify CSR phone number coverage |
| GET | /customer_service_records/{customer_service_record_id} | Get a customer service record |

### detail_records
| Method | Path | Description |
|--------|------|-------------|
| GET | /detail_records | Search detail records |

### dialogflow_connections
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /dialogflow_connections/{connection_id} | Delete stored Dialogflow Connection |
| GET | /dialogflow_connections/{connection_id} | Retrieve stored Dialogflow Connection |
| POST | /dialogflow_connections/{connection_id} | Create a Dialogflow Connection |
| PUT | /dialogflow_connections/{connection_id} | Update stored Dialogflow Connection |

### document_links
| Method | Path | Description |
|--------|------|-------------|
| GET | /document_links | List all document links |

### documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /documents | List all documents |
| POST | /documents | Upload a document |
| DELETE | /documents/{id} | Delete a document |
| GET | /documents/{id} | Retrieve a document |
| PATCH | /documents/{id} | Update a document |
| GET | /documents/{id}/download | Download a document |
| GET | /documents/{id}/download_link | Generate a temporary download link for a document |

### dynamic_emergency_addresses
| Method | Path | Description |
|--------|------|-------------|
| GET | /dynamic_emergency_addresses | List dynamic emergency addresses |
| POST | /dynamic_emergency_addresses | Create a dynamic emergency address. |
| DELETE | /dynamic_emergency_addresses/{id} | Delete a dynamic emergency address |
| GET | /dynamic_emergency_addresses/{id} | Get a dynamic emergency address |

### dynamic_emergency_endpoints
| Method | Path | Description |
|--------|------|-------------|
| GET | /dynamic_emergency_endpoints | List dynamic emergency endpoints |
| POST | /dynamic_emergency_endpoints | Create a dynamic emergency endpoint. |
| DELETE | /dynamic_emergency_endpoints/{id} | Delete a dynamic emergency endpoint |
| GET | /dynamic_emergency_endpoints/{id} | Get a dynamic emergency endpoint |

### external_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /external_connections | List all External Connections |
| POST | /external_connections | Creates an External Connection |
| GET | /external_connections/log_messages | List all log messages |
| DELETE | /external_connections/log_messages/{id} | Dismiss a log message |
| GET | /external_connections/log_messages/{id} | Retrieve a log message |
| DELETE | /external_connections/{id} | Deletes an External Connection |
| GET | /external_connections/{id} | Retrieve an External Connection |
| PATCH | /external_connections/{id} | Update an External Connection |
| GET | /external_connections/{id}/civic_addresses | List all civic addresses and locations |
| GET | /external_connections/{id}/civic_addresses/{address_id} | Retrieve a Civic Address |
| PATCH | /external_connections/{id}/locations/{location_id} | Update a location's static emergency address |
| GET | /external_connections/{id}/phone_numbers | List all phone numbers |
| GET | /external_connections/{id}/phone_numbers/{phone_number_id} | Retrieve a phone number |
| PATCH | /external_connections/{id}/phone_numbers/{phone_number_id} | Update a phone number |
| GET | /external_connections/{id}/releases | List all Releases |
| GET | /external_connections/{id}/releases/{release_id} | Retrieve a Release request |
| GET | /external_connections/{id}/uploads | List all Upload requests |
| POST | /external_connections/{id}/uploads | Creates an Upload request |
| POST | /external_connections/{id}/uploads/refresh | Refresh the status of all Upload requests |
| GET | /external_connections/{id}/uploads/status | Get the count of pending upload requests |
| GET | /external_connections/{id}/uploads/{ticket_id} | Retrieve an Upload request |
| POST | /external_connections/{id}/uploads/{ticket_id}/retry | Retry an Upload request |

### fax_applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /fax_applications | List all Fax Applications |
| POST | /fax_applications | Creates a Fax Application |
| DELETE | /fax_applications/{id} | Deletes a Fax Application |
| GET | /fax_applications/{id} | Retrieve a Fax Application |
| PATCH | /fax_applications/{id} | Update a Fax Application |

### faxes
| Method | Path | Description |
|--------|------|-------------|
| GET | /faxes | View a list of faxes |
| POST | /faxes | Send a fax |
| DELETE | /faxes/{id} | Delete a fax |
| GET | /faxes/{id} | View a fax |
| POST | /faxes/{id}/actions/cancel | Cancel a fax |
| POST | /faxes/{id}/actions/refresh | Refresh a fax |

### fqdn_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /fqdn_connections | List FQDN connections |
| POST | /fqdn_connections | Create an FQDN connection |
| DELETE | /fqdn_connections/{id} | Delete an FQDN connection |
| GET | /fqdn_connections/{id} | Retrieve an FQDN connection |
| PATCH | /fqdn_connections/{id} | Update an FQDN connection |

### fqdns
| Method | Path | Description |
|--------|------|-------------|
| GET | /fqdns | List FQDNs |
| POST | /fqdns | Create an FQDN |
| DELETE | /fqdns/{id} | Delete an FQDN |
| GET | /fqdns/{id} | Retrieve an FQDN |
| PATCH | /fqdns/{id} | Update an FQDN |

### global_ip_allowed_ports
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_allowed_ports | List all Global IP Allowed Ports |

### global_ip_assignment_health
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_assignment_health | Global IP Assignment Health Check Metrics |

### global_ip_assignments
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_assignments | List all Global IP assignments |
| POST | /global_ip_assignments | Create a Global IP assignment |
| DELETE | /global_ip_assignments/{id} | Delete a Global IP assignment |
| GET | /global_ip_assignments/{id} | Retrieve a Global IP |
| PATCH | /global_ip_assignments/{id} | Update a Global IP assignment |

### global_ip_assignments_usage
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_assignments_usage | Global IP Assignment Usage Metrics |

### global_ip_health_check_types
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_health_check_types | List all Global IP Health check types |

### global_ip_health_checks
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_health_checks | List all Global IP health checks |
| POST | /global_ip_health_checks | Create a Global IP health check |
| DELETE | /global_ip_health_checks/{id} | Delete a Global IP health check |
| GET | /global_ip_health_checks/{id} | Retrieve a Global IP health check |

### global_ip_latency
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_latency | Global IP Latency Metrics |

### global_ip_protocols
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_protocols | List all Global IP Protocols |

### global_ip_usage
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ip_usage | Global IP Usage Metrics |

### global_ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /global_ips | List all Global IPs |
| POST | /global_ips | Create a Global IP |
| DELETE | /global_ips/{id} | Delete a Global IP |
| GET | /global_ips/{id} | Retrieve a Global IP |

### inbound_channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /inbound_channels | List your voice channels for US Zone |
| PATCH | /inbound_channels | Update voice channels for US Zone |

### inexplicit_number_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /inexplicit_number_orders | List inexplicit number orders |
| POST | /inexplicit_number_orders | Create an inexplicit number order |
| GET | /inexplicit_number_orders/{id} | Retrieve an inexplicit number order |

### integration_secrets
| Method | Path | Description |
|--------|------|-------------|
| GET | /integration_secrets | List integration secrets |
| POST | /integration_secrets | Create a secret |
| DELETE | /integration_secrets/{id} | Delete an integration secret |

### inventory_coverage
| Method | Path | Description |
|--------|------|-------------|
| GET | /inventory_coverage | Create an inventory coverage request |

### invoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /invoices | List invoices |
| GET | /invoices/{id} | Get invoice by ID |

### ip_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /ip_connections | List Ip connections |
| POST | /ip_connections | Create an Ip connection |
| DELETE | /ip_connections/{id} | Delete an Ip connection |
| GET | /ip_connections/{id} | Retrieve an Ip connection |
| PATCH | /ip_connections/{id} | Update an Ip connection |

### ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /ips | List Ips |
| POST | /ips | Create an Ip |
| DELETE | /ips/{id} | Delete an Ip |
| GET | /ips/{id} | Retrieve an Ip |
| PATCH | /ips/{id} | Update an Ip |

### ledger_billing_group_reports
| Method | Path | Description |
|--------|------|-------------|
| POST | /ledger_billing_group_reports | Create a ledger billing group report |
| GET | /ledger_billing_group_reports/{id} | Get a ledger billing group report |

### legacy
| Method | Path | Description |
|--------|------|-------------|
| GET | /legacy/reporting/batch_detail_records/messaging | Get all MDR detailed report requests |
| POST | /legacy/reporting/batch_detail_records/messaging | Create a new MDR detailed report request |
| DELETE | /legacy/reporting/batch_detail_records/messaging/{id} | Delete a MDR detailed report request |
| GET | /legacy/reporting/batch_detail_records/messaging/{id} | Get a specific MDR detailed report request |
| GET | /legacy/reporting/batch_detail_records/speech_to_text | Get all Speech to Text batch report requests |
| POST | /legacy/reporting/batch_detail_records/speech_to_text | Create a new Speech to Text batch report request |
| DELETE | /legacy/reporting/batch_detail_records/speech_to_text/{id} | Delete a Speech to Text batch report request |
| GET | /legacy/reporting/batch_detail_records/speech_to_text/{id} | Get a specific Speech to Text batch report request |
| GET | /legacy/reporting/batch_detail_records/voice | Get all CDR report requests |
| POST | /legacy/reporting/batch_detail_records/voice | Create a new CDR report request |
| GET | /legacy/reporting/batch_detail_records/voice/fields | Get available CDR report fields |
| DELETE | /legacy/reporting/batch_detail_records/voice/{id} | Delete a CDR report request |
| GET | /legacy/reporting/batch_detail_records/voice/{id} | Get a specific CDR report request |
| GET | /legacy/reporting/usage_reports/messaging | List MDR usage reports |
| POST | /legacy/reporting/usage_reports/messaging | Create a new legacy usage V2 MDR report request |
| DELETE | /legacy/reporting/usage_reports/messaging/{id} | Delete a V2 legacy usage MDR report request |
| GET | /legacy/reporting/usage_reports/messaging/{id} | Get an MDR usage report |
| GET | /legacy/reporting/usage_reports/number_lookup | List telco data usage reports |
| POST | /legacy/reporting/usage_reports/number_lookup | Submit telco data usage report |
| DELETE | /legacy/reporting/usage_reports/number_lookup/{id} | Delete telco data usage report |
| GET | /legacy/reporting/usage_reports/number_lookup/{id} | Get telco data usage report by ID |
| GET | /legacy/reporting/usage_reports/speech_to_text | Get speech to text usage report |
| GET | /legacy/reporting/usage_reports/voice | List CDR usage reports |
| POST | /legacy/reporting/usage_reports/voice | Create a new legacy usage V2 CDR report request |
| DELETE | /legacy/reporting/usage_reports/voice/{id} | Delete a V2 legacy usage CDR report request |
| GET | /legacy/reporting/usage_reports/voice/{id} | Get a CDR usage report |

### list
| Method | Path | Description |
|--------|------|-------------|
| GET | /list | List All Numbers using Channel Billing |
| GET | /list/{channel_zone_id} | List Numbers using Channel Billing for a specific Zone |

### managed_accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /managed_accounts | Lists accounts managed by the current user. |
| POST | /managed_accounts | Create a new managed account. |
| GET | /managed_accounts/allocatable_global_outbound_channels | Display information about allocatable global outbound channels for the current user. |
| GET | /managed_accounts/{id} | Retrieve a managed account |
| PATCH | /managed_accounts/{id} | Update a managed account |
| POST | /managed_accounts/{id}/actions/disable | Disables a managed account |
| POST | /managed_accounts/{id}/actions/enable | Enables a managed account |
| PATCH | /managed_accounts/{id}/update_global_channel_limit | Update the amount of allocatable global outbound channels allocated to a specific managed account. |

### media
| Method | Path | Description |
|--------|------|-------------|
| GET | /media | List uploaded media |
| POST | /media | Upload media |
| DELETE | /media/{media_name} | Deletes stored media |
| GET | /media/{media_name} | Retrieve stored media |
| PUT | /media/{media_name} | Update stored media |
| GET | /media/{media_name}/download | Download stored media |

### messages
| Method | Path | Description |
|--------|------|-------------|
| POST | /messages | Send a message |
| POST | /messages/alphanumeric_sender_id | Send a message using an alphanumeric sender ID |
| GET | /messages/group/{message_id} | Retrieve group MMS messages |
| POST | /messages/group_mms | Send a group MMS message |
| POST | /messages/long_code | Send a long code message |
| POST | /messages/number_pool | Send a message using number pool |
| POST | /messages/rcs | Send an RCS message |
| GET | /messages/rcs/deeplinks/{agent_id} | Generate RCS deeplink |
| POST | /messages/schedule | Schedule a message |
| POST | /messages/short_code | Send a short code message |
| POST | /messages/whatsapp | Send a Whatsapp message |
| DELETE | /messages/{id} | Cancel a scheduled message |
| GET | /messages/{id} | Retrieve a message |

### messaging
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging/rcs/agents | List all RCS agents |
| GET | /messaging/rcs/agents/{id} | Retrieve an RCS agent |
| PATCH | /messaging/rcs/agents/{id} | Modify an RCS agent |
| POST | /messaging/rcs/bulk_capabilities | Check RCS capabilities (batch) |
| GET | /messaging/rcs/capabilities/{agent_id}/{phone_number} | Check RCS capabilities |
| PUT | /messaging/rcs/test_number_invite/{id}/{phone_number} | Add RCS test number |

### messaging_hosted_number_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_hosted_number_orders | List messaging hosted number orders |
| POST | /messaging_hosted_number_orders | Create a messaging hosted number order |
| POST | /messaging_hosted_number_orders/eligibility_numbers_check | Check hosted messaging eligibility |
| DELETE | /messaging_hosted_number_orders/{id} | Delete a messaging hosted number order |
| GET | /messaging_hosted_number_orders/{id} | Retrieve a messaging hosted number order |
| POST | /messaging_hosted_number_orders/{id}/actions/file_upload | Upload hosted number document |
| POST | /messaging_hosted_number_orders/{id}/validation_codes | Validate hosted number codes |
| POST | /messaging_hosted_number_orders/{id}/verification_codes | Create hosted number verification codes |

### messaging_hosted_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_hosted_numbers | List messaging hosted numbers |
| DELETE | /messaging_hosted_numbers/{id} | Delete a messaging hosted number |
| GET | /messaging_hosted_numbers/{id} | Retrieve a messaging hosted number |
| PATCH | /messaging_hosted_numbers/{id} | Update a messaging hosted number |

### messaging_numbers_bulk_updates
| Method | Path | Description |
|--------|------|-------------|
| POST | /messaging_numbers_bulk_updates | Bulk update phone number profiles |
| GET | /messaging_numbers_bulk_updates/{order_id} | Retrieve bulk update status |

### messaging_optouts
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_optouts | List opt-outs |

### messaging_profile_metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_profile_metrics | List high-level messaging profile metrics |

### messaging_profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_profiles | List messaging profiles |
| POST | /messaging_profiles | Create a messaging profile |
| DELETE | /messaging_profiles/{id} | Delete a messaging profile |
| GET | /messaging_profiles/{id} | Retrieve a messaging profile |
| PATCH | /messaging_profiles/{id} | Update a messaging profile |
| POST | /messaging_profiles/{id}/actions/regenerate_secret | Regenerate messaging profile secret |
| GET | /messaging_profiles/{id}/alphanumeric_sender_ids | List alphanumeric sender IDs for a messaging profile |
| GET | /messaging_profiles/{id}/metrics | Get detailed messaging profile metrics |
| GET | /messaging_profiles/{id}/phone_numbers | List phone numbers associated with a messaging profile |
| GET | /messaging_profiles/{id}/short_codes | List short codes associated with a messaging profile |
| GET | /messaging_profiles/{profile_id}/autoresp_configs | List Auto-Response Settings |
| POST | /messaging_profiles/{profile_id}/autoresp_configs | Create auto-response setting |
| DELETE | /messaging_profiles/{profile_id}/autoresp_configs/{autoresp_cfg_id} | Delete Auto-Response Setting |
| GET | /messaging_profiles/{profile_id}/autoresp_configs/{autoresp_cfg_id} | Get Auto-Response Setting |
| PUT | /messaging_profiles/{profile_id}/autoresp_configs/{autoresp_cfg_id} | Update Auto-Response Setting |

### messaging_tollfree
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_tollfree/verification/requests | List Verification Requests |
| POST | /messaging_tollfree/verification/requests | Submit Verification Request |
| DELETE | /messaging_tollfree/verification/requests/{id} | Delete Verification Request |
| GET | /messaging_tollfree/verification/requests/{id} | Get Verification Request |
| PATCH | /messaging_tollfree/verification/requests/{id} | Update Verification Request |
| GET | /messaging_tollfree/verification/requests/{id}/status_history | Get Verification Request Status History |

### messaging_url_domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /messaging_url_domains | List messaging URL domains |

### mobile_network_operators
| Method | Path | Description |
|--------|------|-------------|
| GET | /mobile_network_operators | List mobile network operators |

### mobile_phone_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /mobile_phone_numbers/messaging | List mobile phone numbers with messaging settings |
| GET | /mobile_phone_numbers/{id}/messaging | Retrieve a mobile phone number with messaging settings |
| GET | /v2/mobile_phone_numbers | List Mobile Phone Numbers |
| GET | /v2/mobile_phone_numbers/{id} | Retrieve a Mobile Phone Number |
| PATCH | /v2/mobile_phone_numbers/{id} | Update a Mobile Phone Number |

### mobile_push_credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /mobile_push_credentials | List mobile push credentials |
| POST | /mobile_push_credentials | Creates a new mobile push credential |
| DELETE | /mobile_push_credentials/{push_credential_id} | Deletes a mobile push credential |
| GET | /mobile_push_credentials/{push_credential_id} | Retrieves a mobile push credential |

### network_coverage
| Method | Path | Description |
|--------|------|-------------|
| GET | /network_coverage | List network coverage locations |

### networks
| Method | Path | Description |
|--------|------|-------------|
| GET | /networks | List all Networks |
| POST | /networks | Create a Network |
| DELETE | /networks/{id} | Delete a Network |
| GET | /networks/{id} | Retrieve a Network |
| PATCH | /networks/{id} | Update a Network |
| DELETE | /networks/{id}/default_gateway | Delete Default Gateway. |
| GET | /networks/{id}/default_gateway | Get Default Gateway status. |
| POST | /networks/{id}/default_gateway | Create Default Gateway. |
| GET | /networks/{id}/network_interfaces | List all Interfaces for a Network. |

### notification_channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification_channels | List notification channels |
| POST | /notification_channels | Create a notification channel |
| DELETE | /notification_channels/{id} | Delete a notification channel |
| GET | /notification_channels/{id} | Get a notification channel |
| PATCH | /notification_channels/{id} | Update a notification channel |

### notification_event_conditions
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification_event_conditions | List all Notifications Events Conditions |

### notification_events
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification_events | List all Notifications Events |

### notification_profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification_profiles | List all Notifications Profiles |
| POST | /notification_profiles | Create a notification profile |
| DELETE | /notification_profiles/{id} | Delete a notification profile |
| GET | /notification_profiles/{id} | Get a notification profile |
| PATCH | /notification_profiles/{id} | Update a notification profile |

### notification_settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification_settings | List notification settings |
| POST | /notification_settings | Add a Notification Setting |
| DELETE | /notification_settings/{id} | Delete a notification setting |
| GET | /notification_settings/{id} | Get a notification setting |

### number_block_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /number_block_orders | List number block orders |
| POST | /number_block_orders | Create a number block order |
| GET | /number_block_orders/{number_block_order_id} | Retrieve a number block order |

### number_lookup
| Method | Path | Description |
|--------|------|-------------|
| GET | /number_lookup/{phone_number} | Lookup phone number data |

### number_order_phone_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /number_order_phone_numbers | Retrieve a list of phone numbers associated to orders |
| POST | /number_order_phone_numbers/{id}/requirement_group | Update requirement group for a phone number order |
| GET | /number_order_phone_numbers/{number_order_phone_number_id} | Retrieve a single phone number within a number order. |
| PATCH | /number_order_phone_numbers/{number_order_phone_number_id} | Update requirements for a single phone number within a number order. |

### number_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /number_orders | List number orders |
| POST | /number_orders | Create a number order |
| GET | /number_orders/{number_order_id} | Retrieve a number order |
| PATCH | /number_orders/{number_order_id} | Update a number order |

### number_reservations
| Method | Path | Description |
|--------|------|-------------|
| GET | /number_reservations | List number reservations |
| POST | /number_reservations | Create a number reservation |
| GET | /number_reservations/{number_reservation_id} | Retrieve a number reservation |
| POST | /number_reservations/{number_reservation_id}/actions/extend | Extend a number reservation |

### numbers_features
| Method | Path | Description |
|--------|------|-------------|
| POST | /numbers_features | Retrieve the features for a list of numbers |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth/authorize | OAuth authorization endpoint |
| GET | /oauth/consent/{consent_token} | Get OAuth consent token |
| POST | /oauth/grants | Create OAuth grant |
| POST | /oauth/introspect | Token introspection |
| GET | /oauth/jwks | JSON Web Key Set |
| POST | /oauth/register | Dynamic client registration |
| POST | /oauth/token | OAuth token endpoint |

### oauth_clients
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth_clients | List OAuth clients |
| POST | /oauth_clients | Create OAuth client |
| DELETE | /oauth_clients/{id} | Delete OAuth client |
| GET | /oauth_clients/{id} | Get OAuth client |
| PUT | /oauth_clients/{id} | Update OAuth client |

### oauth_grants
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth_grants | List OAuth grants |
| DELETE | /oauth_grants/{id} | Revoke OAuth grant |
| GET | /oauth_grants/{id} | Get OAuth grant |

### operator_connect
| Method | Path | Description |
|--------|------|-------------|
| POST | /operator_connect/actions/refresh | Refresh Operator Connect integration |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations/users | List organization users |
| GET | /organizations/users/users_groups_report | Get organization users groups report |
| GET | /organizations/users/{id} | Get organization user |
| POST | /organizations/users/{id}/actions/remove | Delete organization user |

### ota_updates
| Method | Path | Description |
|--------|------|-------------|
| GET | /ota_updates | List OTA updates |
| GET | /ota_updates/{id} | Get OTA update |

### outbound_voice_profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /outbound_voice_profiles | Get all outbound voice profiles |
| POST | /outbound_voice_profiles | Create an outbound voice profile |
| DELETE | /outbound_voice_profiles/{id} | Delete an outbound voice profile |
| GET | /outbound_voice_profiles/{id} | Retrieve an outbound voice profile |
| PATCH | /outbound_voice_profiles/{id} | Updates an existing outbound voice profile. |

### payment
| Method | Path | Description |
|--------|------|-------------|
| GET | /payment/auto_recharge_prefs | List auto recharge preferences |
| PATCH | /payment/auto_recharge_prefs | Update auto recharge preferences |
| POST | /v2/payment/stored_payment_transactions | Create a stored payment transaction |

### phone_number_blocks
| Method | Path | Description |
|--------|------|-------------|
| GET | /phone_number_blocks/jobs | Lists the phone number blocks jobs |
| POST | /phone_number_blocks/jobs/delete_phone_number_block | Deletes all numbers associated with a phone number block |
| GET | /phone_number_blocks/jobs/{id} | Retrieves a phone number blocks job |

### phone_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /phone_numbers | List phone numbers |
| POST | /phone_numbers/actions/verify_ownership | Verify ownership of phone numbers |
| GET | /phone_numbers/csv_downloads | List CSV downloads |
| POST | /phone_numbers/csv_downloads | Create a CSV download |
| GET | /phone_numbers/csv_downloads/{id} | Retrieve a CSV download |
| GET | /phone_numbers/jobs | Lists the phone numbers jobs |
| POST | /phone_numbers/jobs/delete_phone_numbers | Delete a batch of numbers |
| POST | /phone_numbers/jobs/update_emergency_settings | Update the emergency settings from a batch of numbers |
| POST | /phone_numbers/jobs/update_phone_numbers | Update a batch of numbers |
| GET | /phone_numbers/jobs/{id} | Retrieve a phone numbers job |
| GET | /phone_numbers/messaging | List phone numbers with messaging settings |
| GET | /phone_numbers/slim | Slim List phone numbers |
| GET | /phone_numbers/voice | List phone numbers with voice settings |
| DELETE | /phone_numbers/{id} | Delete a phone number |
| GET | /phone_numbers/{id} | Retrieve a phone number |
| PATCH | /phone_numbers/{id} | Update a phone number |
| PATCH | /phone_numbers/{id}/actions/bundle_status_change | Change the bundle status for a phone number (set to being in a bundle or remove from a bundle) |
| POST | /phone_numbers/{id}/actions/enable_emergency | Enable emergency for a phone number |
| GET | /phone_numbers/{id}/messaging | Retrieve a phone number with messaging settings |
| PATCH | /phone_numbers/{id}/messaging | Update the messaging profile and/or messaging product of a phone number |
| GET | /phone_numbers/{id}/voice | Retrieve a phone number with voice settings |
| PATCH | /phone_numbers/{id}/voice | Update a phone number with voice settings |
| GET | /phone_numbers/{phone_number_id}/voicemail | Get voicemail |
| PATCH | /phone_numbers/{phone_number_id}/voicemail | Update voicemail |
| POST | /phone_numbers/{phone_number_id}/voicemail | Create voicemail |

### phone_numbers_regulatory_requirements
| Method | Path | Description |
|--------|------|-------------|
| GET | /phone_numbers_regulatory_requirements | Retrieve regulatory requirements for a list of phone numbers |

### portability_checks
| Method | Path | Description |
|--------|------|-------------|
| POST | /portability_checks | Run a portability check |

### porting
| Method | Path | Description |
|--------|------|-------------|
| GET | /porting/events | List all porting events |
| GET | /porting/events/{id} | Show a porting event |
| POST | /porting/events/{id}/republish | Republish a porting event |
| POST | /porting/loa_configuration/preview | Preview the LOA configuration parameters |
| GET | /porting/loa_configurations | List LOA configurations |
| POST | /porting/loa_configurations | Create a LOA configuration |
| DELETE | /porting/loa_configurations/{id} | Delete a LOA configuration |
| GET | /porting/loa_configurations/{id} | Retrieve a LOA configuration |
| PATCH | /porting/loa_configurations/{id} | Update a LOA configuration |
| GET | /porting/loa_configurations/{id}/preview | Preview a LOA configuration |
| GET | /porting/reports | List porting related reports |
| POST | /porting/reports | Create a porting related report |
| GET | /porting/reports/{id} | Retrieve a report |
| GET | /porting/uk_carriers | List available carriers in the UK |

### porting_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /porting_orders | List all porting orders |
| POST | /porting_orders | Create a porting order |
| GET | /porting_orders/exception_types | List all exception types |
| GET | /porting_orders/phone_number_configurations | List all phone number configurations |
| POST | /porting_orders/phone_number_configurations | Create a list of phone number configurations |
| DELETE | /porting_orders/{id} | Delete a porting order |
| GET | /porting_orders/{id} | Retrieve a porting order |
| PATCH | /porting_orders/{id} | Edit a porting order |
| POST | /porting_orders/{id}/actions/activate | Activate every number in a porting order asynchronously. |
| POST | /porting_orders/{id}/actions/cancel | Cancel a porting order |
| POST | /porting_orders/{id}/actions/confirm | Submit a porting order. |
| POST | /porting_orders/{id}/actions/share | Share a porting order |
| GET | /porting_orders/{id}/activation_jobs | List all porting activation jobs |
| GET | /porting_orders/{id}/activation_jobs/{activationJobId} | Retrieve a porting activation job |
| PATCH | /porting_orders/{id}/activation_jobs/{activationJobId} | Update a porting activation job |
| GET | /porting_orders/{id}/additional_documents | List additional documents |
| POST | /porting_orders/{id}/additional_documents | Create a list of additional documents |
| DELETE | /porting_orders/{id}/additional_documents/{additional_document_id} | Delete an additional document |
| GET | /porting_orders/{id}/allowed_foc_windows | List allowed FOC dates |
| GET | /porting_orders/{id}/comments | List all comments of a porting order |
| POST | /porting_orders/{id}/comments | Create a comment for a porting order |
| GET | /porting_orders/{id}/loa_template | Download a porting order loa template |
| GET | /porting_orders/{id}/requirements | List porting order requirements |
| GET | /porting_orders/{id}/sub_request | Retrieve the associated V1 sub_request_id and port_request_id |
| GET | /porting_orders/{id}/verification_codes | List verification codes |
| POST | /porting_orders/{id}/verification_codes/send | Send the verification codes |
| POST | /porting_orders/{id}/verification_codes/verify | Verify the verification code for a list of phone numbers |
| GET | /porting_orders/{porting_order_id}/action_requirements | List action requirements for a porting order |
| POST | /porting_orders/{porting_order_id}/action_requirements/{id}/initiate | Initiate an action requirement |
| GET | /porting_orders/{porting_order_id}/associated_phone_numbers | List all associated phone numbers |
| POST | /porting_orders/{porting_order_id}/associated_phone_numbers | Create an associated phone number |
| DELETE | /porting_orders/{porting_order_id}/associated_phone_numbers/{id} | Delete an associated phone number |
| GET | /porting_orders/{porting_order_id}/phone_number_blocks | List all phone number blocks |
| POST | /porting_orders/{porting_order_id}/phone_number_blocks | Create a phone number block |
| DELETE | /porting_orders/{porting_order_id}/phone_number_blocks/{id} | Delete a phone number block |
| GET | /porting_orders/{porting_order_id}/phone_number_extensions | List all phone number extensions |
| POST | /porting_orders/{porting_order_id}/phone_number_extensions | Create a phone number extension |
| DELETE | /porting_orders/{porting_order_id}/phone_number_extensions/{id} | Delete a phone number extension |

### porting_phone_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /porting_phone_numbers | List all porting phone numbers |

### portouts
| Method | Path | Description |
|--------|------|-------------|
| GET | /portouts | List portout requests |
| GET | /portouts/events | List all port-out events |
| GET | /portouts/events/{id} | Show a port-out event |
| POST | /portouts/events/{id}/republish | Republish a port-out event |
| GET | /portouts/rejections/{portout_id} | List eligible port-out rejection codes for a specific order |
| GET | /portouts/reports | List port-out related reports |
| POST | /portouts/reports | Create a port-out related report |
| GET | /portouts/reports/{id} | Retrieve a report |
| GET | /portouts/{id} | Get a portout request |
| GET | /portouts/{id}/comments | List all comments for a portout request |
| POST | /portouts/{id}/comments | Create a comment on a portout request |
| GET | /portouts/{id}/supporting_documents | List supporting documents on a portout request |
| POST | /portouts/{id}/supporting_documents | Create a list of supporting documents on a portout request |
| PATCH | /portouts/{id}/{status} | Update Status |

### private_wireless_gateways
| Method | Path | Description |
|--------|------|-------------|
| GET | /private_wireless_gateways | Get all Private Wireless Gateways |
| POST | /private_wireless_gateways | Create a Private Wireless Gateway |
| DELETE | /private_wireless_gateways/{id} | Delete a Private Wireless Gateway |
| GET | /private_wireless_gateways/{id} | Get a Private Wireless Gateway |

### public_internet_gateways
| Method | Path | Description |
|--------|------|-------------|
| GET | /public_internet_gateways | List all Public Internet Gateways |
| POST | /public_internet_gateways | Create a Public Internet Gateway |
| DELETE | /public_internet_gateways/{id} | Delete a Public Internet Gateway |
| GET | /public_internet_gateways/{id} | Retrieve a Public Internet Gateway |

### queues
| Method | Path | Description |
|--------|------|-------------|
| GET | /queues | List queues |
| POST | /queues | Create a queue |
| DELETE | /queues/{queue_name} | Delete a queue |
| GET | /queues/{queue_name} | Retrieve a call queue |
| POST | /queues/{queue_name} | Update a queue |
| GET | /queues/{queue_name}/calls | Retrieve calls from a queue |
| DELETE | /queues/{queue_name}/calls/{call_control_id} | Force remove a call from a queue |
| GET | /queues/{queue_name}/calls/{call_control_id} | Retrieve a call from a queue |
| PATCH | /queues/{queue_name}/calls/{call_control_id} | Update queued call |

### recording_transcriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /recording_transcriptions | List all recording transcriptions |
| DELETE | /recording_transcriptions/{recording_transcription_id} | Delete a recording transcription |
| GET | /recording_transcriptions/{recording_transcription_id} | Retrieve a recording transcription |

### recordings
| Method | Path | Description |
|--------|------|-------------|
| GET | /recordings | List all call recordings |
| POST | /recordings/actions/delete | Delete a list of call recordings |
| DELETE | /recordings/{recording_id} | Delete a call recording |
| GET | /recordings/{recording_id} | Retrieve a call recording |

### regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /regions | List all Regions |

### regulatory_requirements
| Method | Path | Description |
|--------|------|-------------|
| GET | /regulatory_requirements | Retrieve regulatory requirements |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /reports/cdr_usage_reports/sync | Generates and fetches CDR Usage Reports |
| GET | /reports/mdr_usage_reports | Fetch all Messaging usage reports |
| POST | /reports/mdr_usage_reports | Create MDR Usage Report |
| GET | /reports/mdr_usage_reports/sync | Generate and fetch MDR Usage Report |
| DELETE | /reports/mdr_usage_reports/{id} | Delete MDR Usage Report |
| GET | /reports/mdr_usage_reports/{id} | Retrieve messaging report |
| GET | /reports/mdrs | Fetch all Mdr records |
| GET | /reports/wdrs | Fetches all Wdr records |

### requirement_groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /requirement_groups | List requirement groups |
| POST | /requirement_groups | Create a new requirement group |
| DELETE | /requirement_groups/{id} | Delete a requirement group by ID |
| GET | /requirement_groups/{id} | Get a single requirement group by ID |
| PATCH | /requirement_groups/{id} | Update requirement values in requirement group |
| POST | /requirement_groups/{id}/submit_for_approval | Submit a Requirement Group for Approval |

### requirement_types
| Method | Path | Description |
|--------|------|-------------|
| GET | /requirement_types | List all requirement types |
| GET | /requirement_types/{id} | Retrieve a requirement types |

### requirements
| Method | Path | Description |
|--------|------|-------------|
| GET | /requirements | List all requirements |
| GET | /requirements/{id} | Retrieve a document requirement |

### room_compositions
| Method | Path | Description |
|--------|------|-------------|
| GET | /room_compositions | View a list of room compositions. |
| POST | /room_compositions | Create a room composition. |
| DELETE | /room_compositions/{room_composition_id} | Delete a room composition. |
| GET | /room_compositions/{room_composition_id} | View a room composition. |

### room_participants
| Method | Path | Description |
|--------|------|-------------|
| GET | /room_participants | View a list of room participants. |
| GET | /room_participants/{room_participant_id} | View a room participant. |

### room_recordings
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /room_recordings | Delete several room recordings in a bulk. |
| GET | /room_recordings | View a list of room recordings. |
| DELETE | /room_recordings/{room_recording_id} | Delete a room recording. |
| GET | /room_recordings/{room_recording_id} | View a room recording. |

### room_sessions
| Method | Path | Description |
|--------|------|-------------|
| GET | /room_sessions | View a list of room sessions. |
| GET | /room_sessions/{room_session_id} | View a room session. |
| POST | /room_sessions/{room_session_id}/actions/end | End a room session. |
| POST | /room_sessions/{room_session_id}/actions/kick | Kick participants from a room session. |
| POST | /room_sessions/{room_session_id}/actions/mute | Mute participants in room session. |
| POST | /room_sessions/{room_session_id}/actions/unmute | Unmute participants in room session. |
| GET | /room_sessions/{room_session_id}/participants | View a list of room participants. |

### rooms
| Method | Path | Description |
|--------|------|-------------|
| GET | /rooms | View a list of rooms. |
| POST | /rooms | Create a room. |
| DELETE | /rooms/{room_id} | Delete a room. |
| GET | /rooms/{room_id} | View a room. |
| PATCH | /rooms/{room_id} | Update a room. |
| POST | /rooms/{room_id}/actions/generate_join_client_token | Create Client Token to join a room. |
| POST | /rooms/{room_id}/actions/refresh_client_token | Refresh Client Token to join a room. |
| GET | /rooms/{room_id}/sessions | View a list of room sessions. |

### seti
| Method | Path | Description |
|--------|------|-------------|
| GET | /seti/black_box_test_results | Retrieve Black Box Test Results |

### short_codes
| Method | Path | Description |
|--------|------|-------------|
| GET | /short_codes | List short codes |
| GET | /short_codes/{id} | Retrieve a short code |
| PATCH | /short_codes/{id} | Update short code |

### sim_card_actions
| Method | Path | Description |
|--------|------|-------------|
| GET | /sim_card_actions | List SIM card actions |
| GET | /sim_card_actions/{id} | Get SIM card action details |

### sim_card_data_usage_notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /sim_card_data_usage_notifications | List SIM card data usage notifications |
| POST | /sim_card_data_usage_notifications | Create a new SIM card data usage notification |
| DELETE | /sim_card_data_usage_notifications/{id} | Delete SIM card data usage notifications |
| GET | /sim_card_data_usage_notifications/{id} | Get a single SIM card data usage notification |
| PATCH | /sim_card_data_usage_notifications/{id} | Updates information for a SIM Card Data Usage Notification |

### sim_card_group_actions
| Method | Path | Description |
|--------|------|-------------|
| GET | /sim_card_group_actions | List SIM card group actions |
| GET | /sim_card_group_actions/{id} | Get SIM card group action details |

### sim_card_groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /sim_card_groups | Get all SIM card groups |
| POST | /sim_card_groups | Create a SIM card group |
| DELETE | /sim_card_groups/{id} | Delete a SIM card group |
| GET | /sim_card_groups/{id} | Get SIM card group |
| PATCH | /sim_card_groups/{id} | Update a SIM card group |
| POST | /sim_card_groups/{id}/actions/remove_private_wireless_gateway | Request Private Wireless Gateway removal from SIM card group |
| POST | /sim_card_groups/{id}/actions/remove_wireless_blocklist | Request Wireless Blocklist removal from SIM card group |
| POST | /sim_card_groups/{id}/actions/set_private_wireless_gateway | Request Private Wireless Gateway assignment for SIM card group |
| POST | /sim_card_groups/{id}/actions/set_wireless_blocklist | Request Wireless Blocklist assignment for SIM card group |

### sim_card_order_preview
| Method | Path | Description |
|--------|------|-------------|
| POST | /sim_card_order_preview | Preview SIM card orders |

### sim_card_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /sim_card_orders | Get all SIM card orders |
| POST | /sim_card_orders | Create a SIM card order |
| GET | /sim_card_orders/{id} | Get a single SIM card order |

### sim_cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /sim_cards | Get all SIM cards |
| POST | /sim_cards/actions/bulk_set_public_ips | Request bulk setting SIM card public IPs. |
| POST | /sim_cards/actions/validate_registration_codes | Validate SIM cards registration codes |
| DELETE | /sim_cards/{id} | Deletes a SIM card |
| GET | /sim_cards/{id} | Get SIM card |
| PATCH | /sim_cards/{id} | Update a SIM card |
| POST | /sim_cards/{id}/actions/disable | Request a SIM card disable |
| POST | /sim_cards/{id}/actions/enable | Request a SIM card enable |
| POST | /sim_cards/{id}/actions/remove_public_ip | Request removing a SIM card public IP |
| POST | /sim_cards/{id}/actions/set_public_ip | Request setting a SIM card public IP |
| POST | /sim_cards/{id}/actions/set_standby | Request setting a SIM card to standby |
| GET | /sim_cards/{id}/activation_code | Get activation code for an eSIM |
| GET | /sim_cards/{id}/device_details | Get SIM card device details |
| GET | /sim_cards/{id}/public_ip | Get SIM card public IP definition |
| GET | /sim_cards/{id}/wireless_connectivity_logs | List wireless connectivity logs |

### siprec_connectors
| Method | Path | Description |
|--------|------|-------------|
| POST | /siprec_connectors | Create a SIPREC connector |
| DELETE | /siprec_connectors/{connector_name} | Delete a SIPREC connector |
| GET | /siprec_connectors/{connector_name} | Retrieve a SIPREC connector |
| PUT | /siprec_connectors/{connector_name} | Update a SIPREC connector |

### speech-to-text
| Method | Path | Description |
|--------|------|-------------|
| GET | /speech-to-text/transcription | Speech to text over websocket |

### storage
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /storage/buckets/{bucketName}/ssl_certificate | Remove SSL Certificate |
| GET | /storage/buckets/{bucketName}/ssl_certificate | Get Bucket SSL Certificate |
| PUT | /storage/buckets/{bucketName}/ssl_certificate | Add SSL Certificate |
| GET | /storage/buckets/{bucketName}/usage/api | Get API Usage |
| GET | /storage/buckets/{bucketName}/usage/storage | Get Bucket Usage |
| POST | /storage/buckets/{bucketName}/{objectName}/presigned_url | Create Presigned Object URL |
| GET | /storage/migration_source_coverage | List Migration Source coverage |
| GET | /storage/migration_sources | List all Migration Sources |
| POST | /storage/migration_sources | Create a Migration Source |
| DELETE | /storage/migration_sources/{id} | Delete a Migration Source |
| GET | /storage/migration_sources/{id} | Get a Migration Source |
| GET | /storage/migrations | List all Migrations |
| POST | /storage/migrations | Create a Migration |
| GET | /storage/migrations/{id} | Get a Migration |
| POST | /storage/migrations/{id}/actions/stop | Stop a Migration |

### sub_number_orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /sub_number_orders | List sub number orders |
| POST | /sub_number_orders/{id}/requirement_group | Update requirement group for a sub number order |
| GET | /sub_number_orders/{sub_number_order_id} | Retrieve a sub number order |
| PATCH | /sub_number_orders/{sub_number_order_id} | Update a sub number order's requirements |
| PATCH | /sub_number_orders/{sub_number_order_id}/cancel | Cancel a sub number order |

### sub_number_orders_report
| Method | Path | Description |
|--------|------|-------------|
| POST | /sub_number_orders_report | Create a sub number orders report |
| GET | /sub_number_orders_report/{report_id} | Retrieve a sub number orders report |
| GET | /sub_number_orders_report/{report_id}/download | Download a sub number orders report |

### telephony_credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /telephony_credentials | List all credentials |
| POST | /telephony_credentials | Create a credential |
| DELETE | /telephony_credentials/{id} | Delete a credential |
| GET | /telephony_credentials/{id} | Get a credential |
| PATCH | /telephony_credentials/{id} | Update a credential |
| POST | /telephony_credentials/{id}/token | Create an Access Token. |

### texml
| Method | Path | Description |
|--------|------|-------------|
| GET | /texml/Accounts/{account_sid}/Calls | Fetch multiple call resources |
| POST | /texml/Accounts/{account_sid}/Calls | Initiate an outbound call |
| GET | /texml/Accounts/{account_sid}/Calls/{call_sid} | Fetch a call |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid} | Update call |
| GET | /texml/Accounts/{account_sid}/Calls/{call_sid}/Recordings.json | Fetch recordings for a call |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid}/Recordings.json | Request recording for a call |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid}/Recordings/{recording_sid}.json | Update recording on a call |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid}/Siprec.json | Request siprec session for a call |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid}/Siprec/{siprec_sid}.json | Updates siprec session for a call |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid}/Streams.json | Start streaming media from a call. |
| POST | /texml/Accounts/{account_sid}/Calls/{call_sid}/Streams/{streaming_sid}.json | Update streaming on a call |
| GET | /texml/Accounts/{account_sid}/Conferences | List conference resources |
| GET | /texml/Accounts/{account_sid}/Conferences/{conference_sid} | Fetch a conference resource |
| POST | /texml/Accounts/{account_sid}/Conferences/{conference_sid} | Update a conference resource |
| GET | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Participants | List conference participants |
| POST | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Participants | Dial a new conference participant |
| DELETE | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Participants/{call_sid_or_participant_label} | Delete a conference participant |
| GET | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Participants/{call_sid_or_participant_label} | Get conference participant resource |
| POST | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Participants/{call_sid_or_participant_label} | Update a conference participant |
| GET | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Recordings | List conference recordings |
| GET | /texml/Accounts/{account_sid}/Conferences/{conference_sid}/Recordings.json | Fetch recordings for a conference |
| GET | /texml/Accounts/{account_sid}/Queues | List queue resources |
| POST | /texml/Accounts/{account_sid}/Queues | Create a new queue |
| DELETE | /texml/Accounts/{account_sid}/Queues/{queue_sid} | Delete a queue resource |
| GET | /texml/Accounts/{account_sid}/Queues/{queue_sid} | Fetch a queue resource |
| POST | /texml/Accounts/{account_sid}/Queues/{queue_sid} | Update a queue resource |
| GET | /texml/Accounts/{account_sid}/Recordings.json | Fetch multiple recording resources |
| DELETE | /texml/Accounts/{account_sid}/Recordings/{recording_sid}.json | Delete recording resource |
| GET | /texml/Accounts/{account_sid}/Recordings/{recording_sid}.json | Fetch recording resource |
| GET | /texml/Accounts/{account_sid}/Transcriptions.json | List recording transcriptions |
| DELETE | /texml/Accounts/{account_sid}/Transcriptions/{recording_transcription_sid}.json | Delete a recording transcription |
| GET | /texml/Accounts/{account_sid}/Transcriptions/{recording_transcription_sid}.json | Fetch a recording transcription resource |
| POST | /texml/secrets | Create a TeXML secret |

### texml_applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /texml_applications | List all TeXML Applications |
| POST | /texml_applications | Creates a TeXML Application |
| DELETE | /texml_applications/{id} | Deletes a TeXML Application |
| GET | /texml_applications/{id} | Retrieve a TeXML Application |
| PATCH | /texml_applications/{id} | Update a TeXML Application |

### text-to-speech
| Method | Path | Description |
|--------|------|-------------|
| GET | /text-to-speech/speech | Stream text to speech over WebSocket |
| POST | /text-to-speech/speech | Generate speech from text |
| GET | /text-to-speech/voices | List available voices |

### usage_reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /usage_reports | Get Telnyx product usage data (BETA) |
| GET | /usage_reports/options | Get Usage Reports query options (BETA) |

### user_addresses
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_addresses | List all user addresses |
| POST | /user_addresses | Creates a user address |
| GET | /user_addresses/{id} | Retrieve a user address |

### user_tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_tags | List User Tags |

### mobile_voice_connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/mobile_voice_connections | List Mobile Voice Connections |
| POST | /v2/mobile_voice_connections | Create a Mobile Voice Connection |
| DELETE | /v2/mobile_voice_connections/{id} | Delete a Mobile Voice Connection |
| GET | /v2/mobile_voice_connections/{id} | Retrieve a Mobile Voice Connection |
| PATCH | /v2/mobile_voice_connections/{id} | Update a Mobile Voice Connection |

### verifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /verifications/by_phone_number/{phone_number} | List verifications by phone number |
| POST | /verifications/by_phone_number/{phone_number}/actions/verify | Verify verification code by phone number |
| POST | /verifications/call | Trigger Call verification |
| POST | /verifications/flashcall | Trigger Flash call verification |
| POST | /verifications/sms | Trigger SMS verification |
| GET | /verifications/{verification_id} | Retrieve verification |
| POST | /verifications/{verification_id}/actions/verify | Verify verification code by ID |

### verified_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /verified_numbers | List all Verified Numbers |
| POST | /verified_numbers | Request phone number verification |
| DELETE | /verified_numbers/{phone_number} | Delete a verified number |
| GET | /verified_numbers/{phone_number} | Retrieve a verified number |
| POST | /verified_numbers/{phone_number}/actions/verify | Submit verification code |

### verify_profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /verify_profiles | List all Verify profiles |
| POST | /verify_profiles | Create a Verify profile |
| GET | /verify_profiles/templates | Retrieve Verify profile message templates |
| POST | /verify_profiles/templates | Create message template |
| PATCH | /verify_profiles/templates/{template_id} | Update message template |
| DELETE | /verify_profiles/{verify_profile_id} | Delete Verify profile |
| GET | /verify_profiles/{verify_profile_id} | Retrieve Verify profile |
| PATCH | /verify_profiles/{verify_profile_id} | Update Verify profile |

### virtual_cross_connects
| Method | Path | Description |
|--------|------|-------------|
| GET | /virtual_cross_connects | List all Virtual Cross Connects |
| POST | /virtual_cross_connects | Create a Virtual Cross Connect |
| DELETE | /virtual_cross_connects/{id} | Delete a Virtual Cross Connect |
| GET | /virtual_cross_connects/{id} | Retrieve a Virtual Cross Connect |
| PATCH | /virtual_cross_connects/{id} | Update the Virtual Cross Connect |

### virtual_cross_connects_coverage
| Method | Path | Description |
|--------|------|-------------|
| GET | /virtual_cross_connects_coverage | List Virtual Cross Connect Cloud Coverage |

### webhook_deliveries
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhook_deliveries | List webhook deliveries |
| GET | /webhook_deliveries/{id} | Find webhook_delivery details by ID |

### wireguard_interfaces
| Method | Path | Description |
|--------|------|-------------|
| GET | /wireguard_interfaces | List all WireGuard Interfaces |
| POST | /wireguard_interfaces | Create a WireGuard Interface |
| DELETE | /wireguard_interfaces/{id} | Delete a WireGuard Interface |
| GET | /wireguard_interfaces/{id} | Retrieve a WireGuard Interfaces |

### wireguard_peers
| Method | Path | Description |
|--------|------|-------------|
| GET | /wireguard_peers | List all WireGuard Peers |
| POST | /wireguard_peers | Create a WireGuard Peer |
| DELETE | /wireguard_peers/{id} | Delete the WireGuard Peer |
| GET | /wireguard_peers/{id} | Retrieve the WireGuard Peer |
| PATCH | /wireguard_peers/{id} | Update the WireGuard Peer |
| GET | /wireguard_peers/{id}/config | Retrieve Wireguard config template for Peer |

### wireless
| Method | Path | Description |
|--------|------|-------------|
| GET | /wireless/detail_records_reports | Get all Wireless Detail Records (WDRs) Reports |
| POST | /wireless/detail_records_reports | Create a Wireless Detail Records (WDRs) Report |
| DELETE | /wireless/detail_records_reports/{id} | Delete a Wireless Detail Record (WDR) Report |
| GET | /wireless/detail_records_reports/{id} | Get a Wireless Detail Record (WDR) Report |
| GET | /wireless/regions | Get all wireless regions |

### wireless_blocklist_values
| Method | Path | Description |
|--------|------|-------------|
| GET | /wireless_blocklist_values | Get all possible wireless blocklist values |

### wireless_blocklists
| Method | Path | Description |
|--------|------|-------------|
| GET | /wireless_blocklists | Get all Wireless Blocklists |
| PATCH | /wireless_blocklists | Update a Wireless Blocklist |
| POST | /wireless_blocklists | Create a Wireless Blocklist |
| DELETE | /wireless_blocklists/{id} | Delete a Wireless Blocklist |
| GET | /wireless_blocklists/{id} | Get a Wireless Blocklist |

## Enhanced Skill Content
## Question Mapping

- "How do I send an SMS message?" -> POST /messages
- "What phone numbers do I own?" -> GET /phone_numbers
- "How do I check my account balance?" -> GET /balance
- "Can I search for available phone numbers to buy?" -> GET /available_phone_numbers
- "How do I place an outbound call?" -> POST /calls
- "What is the status of my porting order?" -> GET /porting_orders/{id}
- "How do I create an AI assistant for voice calls?" -> POST /ai/assistants
- "How do I register a 10DLC brand?" -> POST /10dlc/brand
- "How do I look up carrier info for a number?" -> GET /number_lookup/{phone_number}
- "How do I send a fax?" -> POST /faxes
- "What are my active call conferences?" -> GET /conferences
- "How do I manage my SIM cards?" -> GET /sim_cards
- "How do I set up a messaging profile?" -> POST /messaging_profiles
- "How do I verify a phone number for 2FA?" -> POST /verifications/sms
- "How do I check my usage and charges?" -> GET /charges_summary

## Response Tips

- **Paginated lists** (phone_numbers, messages, sim_cards, etc.): All return `meta: {page_number, page_size, total_pages, total_results}` -- always check `total_pages` and loop with `page[number]` or `page` params to get complete results.
- **Call control actions** (calls/{id}/actions/*): Return `{data: {result: str}}` where result is typically `"ok"` -- a 200 does not mean the action completed, only that it was accepted; listen for webhooks for confirmation.
- **Async operations** (SIM actions, porting, bulk jobs): Return 202 with a task/job ID -- poll the corresponding GET endpoint or configure a webhook to track completion status.
- **10DLC endpoints**: Use TCR-style pagination with `page` and `recordsPerPage` (not the standard `page[number]`/`page[size]` pattern used elsewhere).
- **Error responses**: 422 is the most common error across the API indicating validation failure; 4XX errors on messaging endpoints are generic -- inspect the response body `errors` array for specific codes and messages.
- **TeXML endpoints**: Follow Twilio-compatible response shapes (e.g., `calls` array, `sid` instead of `id`, `uri` instead of `record_type`) -- do not mix with native v2 endpoint patterns.
- **AI/Assistants**: Responses contain deeply nested objects (`voice_settings`, `telephony_settings`, `transcription`) -- nullable fields are marked with `?` and should be checked before access.

## Anomaly Flags

- **Balance approaching zero**: After any billable operation, proactively check `GET /balance` and warn if `available_credit` drops below a reasonable threshold for the user's typical usage.
- **10DLC campaign status not ACTIVE**: Surface `failureReasons` and `submissionStatus` whenever a campaign's `status` is not progressing -- rejected campaigns block messaging on assigned numbers.
- **Porting order exceptions**: Flag any porting order where `requirements_met` is `false` or `status.details` contains error entries -- these stall port-ins silently.
- **SIM card actions stuck**: If `actions_in_progress` is `true` on a SIM card for an extended period, or if `status.value` shows an unexpected state, alert the user to check `sim_card_actions`.
- **Phone number emergency status**: Warn when `emergency_enabled` is `false` on numbers intended for voice service, or when `emergency_status` is not `active` after enabling.
- **Messaging profile daily spend limit**: Surface when `daily_spend_limit_enabled` is `true` and current spend is approaching the `daily_spend_limit` value.
- **Webhook delivery failures**: Periodically check `GET /webhook_deliveries` for failed delivery attempts that could indicate missed events.
- **Credential expiration**: Flag telephony credentials where `expired` is `true` or `expires_at` is approaching.
- **Number order requirements not met**: Alert when `requirements_met` is `false` on number orders, as these will not complete without regulatory document uploads.

## Playbook

### 1. Purchase and Configure a Phone Number for Messaging

1. Search for available numbers: `GET /available_phone_numbers?filter[country_code]=US&filter[features]=sms`
2. Create a messaging profile: `POST /messaging_profiles` with `name`, `whitelisted_destinations`, and `webhook_url`
3. Order the number: `POST /number_orders` with the chosen `phone_number` from step 1
4. Check order status: `GET /number_orders/{id}` -- wait until `status` is `success`
5. Assign messaging profile: `PATCH /phone_numbers/{id}/messaging` with `messaging_profile_id` from step 2
6. For US numbers, register a 10DLC brand (`POST /10dlc/brand`) and campaign (`POST /10dlc/campaignBuilder`), then assign the number (`POST /10dlc/phone_number_campaigns`)
7. Send a test message: `POST /messages` with `from`, `to`, and `text`

### 2. Set Up an AI Voice Assistant

1. Create the assistant: `POST /ai/assistants` with `name`, `model`, `instructions`, and `voice_settings` (including `voice`)
2. Create a call control or TeXML application: `POST /call_control_applications` with `webhook_event_url` pointing to your server
3. Assign a phone number to the application: `PATCH /phone_numbers/{id}` with `connection_id`
4. Test via chat: `POST /ai/assistants/{assistant_id}/chat` to validate instructions before going live
5. Optionally create versions: `GET /ai/assistants/{assistant_id}/versions` and use canary deploys (`POST /ai/assistants/{assistant_id}/canary-deploys`) for gradual rollout
6. Run automated tests: `POST /ai/assistants/tests` with rubric criteria, then `POST /ai/assistants/tests/{test_id}/runs`

### 3. Port Numbers Into Telnyx

1. Check portability: `POST /portability_checks` with the list of `phone_numbers`
2. Create the porting order: `POST /porting_orders` with `phone_numbers`
3. Fill in end-user details: `PATCH /porting_orders/{id}` with `end_user` (admin info, location) and `documents` (LOA, invoice)
4. Upload LOA document: `POST /documents` then reference the document ID in the porting order patch
5. Check requirements: `GET /porting_orders/{id}/requirements` and fulfill any outstanding items
6. Confirm the order: `POST /porting_orders/{id}/actions/confirm`
7. Monitor status via `GET /porting_orders/{id}` or configure `webhook_url` on the order -- watch for FOC date assignment
8. Activate when ready: `POST /porting_orders/{id}/actions/activate`

### 4. Send Verified SMS with 2FA (Verify API)

1. Create a verify profile: `POST /verify_profiles` with `name` and `sms` settings (code_length, app_name, whitelisted_destinations)
2. Trigger verification: `POST /verifications/sms` with `phone_number` and `verify_profile_id`
3. Collect the code from your user's input
4. Validate the code: `POST /verifications/{verification_id}/actions/verify` with the `code`
5. Check response: `response_code` of `accepted` means success; `rejected` means wrong code or expired

### 5. Manage IoT SIM Cards

1. Order physical SIMs: `POST /sim_card_orders` with `address_id` and `quantity` (preview cost first with `POST /sim_card_order_preview`)
2. Register received SIMs: `POST /actions/register/sim_cards` with `registration_codes` from the packaging
3. Create a SIM group: `POST /sim_card_groups` with `name` and optional `data_limit`
4. Assign SIMs to the group: `PATCH /sim_cards/{id}` with `sim_card_group_id`
5. Enable a SIM: `POST /sim_cards/{id}/actions/enable`
6. Set data usage alerts: `POST /sim_card_data_usage_notifications` with `sim_card_id` and `threshold`
7. Monitor usage: `GET /sim_cards/{id}` and check `current_billing_period_consumed_data`
8. For private networking, attach a gateway: `POST /sim_card_groups/{id}/actions/set_private_wireless_gateway`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
