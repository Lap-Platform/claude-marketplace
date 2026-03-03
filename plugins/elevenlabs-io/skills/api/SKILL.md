---
name: elevenlabs-api-documentation
description: "ElevenLabs API Documentation API skill. Use when working with ElevenLabs API Documentation for history, sound-generation, audio-isolation. Covers 258 endpoints."
version: 1.0.0
generator: lapsh
---

# ElevenLabs API Documentation
API version: 1.0

## Auth
ApiKey xi-api-key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /v1/history -- verify access
3. POST /v1/history/download -- create first download

## Endpoints

258 endpoints across 25 groups. See references/api-spec.lap for full details.

### history
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/history | List Generated Items |
| GET | /v1/history/{history_item_id} | Get History Item |
| DELETE | /v1/history/{history_item_id} | Delete History Item |
| GET | /v1/history/{history_item_id}/audio | Get Audio From History Item |
| POST | /v1/history/download | Download History Items |

### sound-generation
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/sound-generation | Sound Generation |

### audio-isolation
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/audio-isolation | Audio Isolation |
| POST | /v1/audio-isolation/stream | Audio Isolation Stream |

### voices
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v1/voices/{voice_id}/samples/{sample_id} | Delete Sample |
| GET | /v1/voices/{voice_id}/samples/{sample_id}/audio | Get Audio From Sample |
| GET | /v1/voices | List Voices |
| GET | /v2/voices | Get Voices V2 |
| GET | /v1/voices/settings/default | Get Default Voice Settings. |
| GET | /v1/voices/{voice_id}/settings | Get Voice Settings |
| GET | /v1/voices/{voice_id} | Get Voice |
| DELETE | /v1/voices/{voice_id} | Delete Voice |
| POST | /v1/voices/{voice_id}/settings/edit | Edit Voice Settings |
| POST | /v1/voices/add | Add Voice |
| POST | /v1/voices/{voice_id}/edit | Edit Voice |
| POST | /v1/voices/add/{public_user_id}/{voice_id} | Add Shared Voice |
| POST | /v1/voices/pvc | Create Pvc Voice |
| POST | /v1/voices/pvc/{voice_id} | Edit Pvc Voice |
| POST | /v1/voices/pvc/{voice_id}/samples | Add Samples To Pvc Voice |
| POST | /v1/voices/pvc/{voice_id}/samples/{sample_id} | Update Pvc Voice Sample |
| DELETE | /v1/voices/pvc/{voice_id}/samples/{sample_id} | Delete Pvc Voice Sample |
| GET | /v1/voices/pvc/{voice_id}/samples/{sample_id}/audio | Retrieve Voice Sample Audio |
| GET | /v1/voices/pvc/{voice_id}/samples/{sample_id}/waveform | Retrieve Voice Sample Visual Waveform |
| GET | /v1/voices/pvc/{voice_id}/samples/{sample_id}/speakers | Retrieve Speaker Separation Status |
| POST | /v1/voices/pvc/{voice_id}/samples/{sample_id}/separate-speakers | Start Speaker Separation |
| GET | /v1/voices/pvc/{voice_id}/samples/{sample_id}/speakers/{speaker_id}/audio | Retrieve Separated Speaker Audio |
| GET | /v1/voices/pvc/{voice_id}/captcha | Get Pvc Voice Captcha |
| POST | /v1/voices/pvc/{voice_id}/captcha | Verify Pvc Voice Captcha |
| POST | /v1/voices/pvc/{voice_id}/train | Run Pvc Training |
| POST | /v1/voices/pvc/{voice_id}/verification | Request Manual Verification |

### text-to-speech
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/text-to-speech/{voice_id} | Text To Speech |
| POST | /v1/text-to-speech/{voice_id}/with-timestamps | Text To Speech With Timestamps |
| POST | /v1/text-to-speech/{voice_id}/stream | Text To Speech Streaming |
| POST | /v1/text-to-speech/{voice_id}/stream/with-timestamps | Text To Speech Streaming With Timestamps |

### text-to-dialogue
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/text-to-dialogue | Text To Dialogue (Multi-Voice) |
| POST | /v1/text-to-dialogue/stream | Text To Dialogue (Multi-Voice) Streaming |
| POST | /v1/text-to-dialogue/stream/with-timestamps | Text To Dialogue Streaming With Timestamps |
| POST | /v1/text-to-dialogue/with-timestamps | Text To Dialogue With Timestamps |

### speech-to-speech
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/speech-to-speech/{voice_id} | Speech To Speech |
| POST | /v1/speech-to-speech/{voice_id}/stream | Speech To Speech Streaming |

### text-to-voice
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/text-to-voice/create-previews | Generate A Voice Preview From Description |
| POST | /v1/text-to-voice | Create A New Voice From Voice Preview |
| POST | /v1/text-to-voice/design | Design A Voice. |
| POST | /v1/text-to-voice/{voice_id}/remix | Remix A Voice. |
| GET | /v1/text-to-voice/{generated_voice_id}/stream | Text To Voice Preview Streaming |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/user/subscription | Get User Subscription Info |
| GET | /v1/user | Get User Info |

### studio
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/studio/podcasts | Create Podcast |
| POST | /v1/studio/projects/{project_id}/pronunciation-dictionaries | Create Pronunciation Dictionaries |
| GET | /v1/studio/projects | List Studio Projects |
| POST | /v1/studio/projects | Create Studio Project |
| POST | /v1/studio/projects/{project_id} | Update Studio Project |
| GET | /v1/studio/projects/{project_id} | Get Studio Project |
| DELETE | /v1/studio/projects/{project_id} | Delete Studio Project |
| POST | /v1/studio/projects/{project_id}/content | Update Studio Project Content |
| POST | /v1/studio/projects/{project_id}/convert | Convert Studio Project |
| GET | /v1/studio/projects/{project_id}/snapshots | List Studio Project Snapshots |
| GET | /v1/studio/projects/{project_id}/snapshots/{project_snapshot_id} | Get Project Snapshot |
| POST | /v1/studio/projects/{project_id}/snapshots/{project_snapshot_id}/stream | Stream Studio Project Audio |
| POST | /v1/studio/projects/{project_id}/snapshots/{project_snapshot_id}/archive | Stream Archive With Studio Project Audio |
| GET | /v1/studio/projects/{project_id}/chapters | List Chapters |
| POST | /v1/studio/projects/{project_id}/chapters | Create Chapter |
| GET | /v1/studio/projects/{project_id}/chapters/{chapter_id} | Get Chapter |
| POST | /v1/studio/projects/{project_id}/chapters/{chapter_id} | Update Chapter |
| DELETE | /v1/studio/projects/{project_id}/chapters/{chapter_id} | Delete Chapter |
| POST | /v1/studio/projects/{project_id}/chapters/{chapter_id}/convert | Convert Chapter |
| GET | /v1/studio/projects/{project_id}/chapters/{chapter_id}/snapshots | List Chapter Snapshots |
| GET | /v1/studio/projects/{project_id}/chapters/{chapter_id}/snapshots/{chapter_snapshot_id} | Get Chapter Snapshot |
| POST | /v1/studio/projects/{project_id}/chapters/{chapter_id}/snapshots/{chapter_snapshot_id}/stream | Stream Chapter Audio |
| GET | /v1/studio/projects/{project_id}/muted-tracks | Get Project Muted Tracks |

### dubbing
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/dubbing/resource/{dubbing_id} | Get The Dubbing Resource For An Id. |
| POST | /v1/dubbing/resource/{dubbing_id}/language | Add A Language To The Resource |
| POST | /v1/dubbing/resource/{dubbing_id}/speaker/{speaker_id}/segment | Create A Segment For The Speaker |
| PATCH | /v1/dubbing/resource/{dubbing_id}/segment/{segment_id}/{language} | Modify A Single Segment |
| POST | /v1/dubbing/resource/{dubbing_id}/migrate-segments | Move Segments Between Speakers |
| DELETE | /v1/dubbing/resource/{dubbing_id}/segment/{segment_id} | Deletes A Single Segment |
| POST | /v1/dubbing/resource/{dubbing_id}/transcribe | Transcribes Segments |
| POST | /v1/dubbing/resource/{dubbing_id}/translate | Translates All Or Some Segments And Languages |
| POST | /v1/dubbing/resource/{dubbing_id}/dub | Dubs All Or Some Segments And Languages |
| PATCH | /v1/dubbing/resource/{dubbing_id}/speaker/{speaker_id} | Update Metadata For A Speaker |
| POST | /v1/dubbing/resource/{dubbing_id}/speaker | Create A New Speaker |
| GET | /v1/dubbing/resource/{dubbing_id}/speaker/{speaker_id}/similar-voices | Search The Elevenlabs Library For Voices Similar To A Speaker. |
| POST | /v1/dubbing/resource/{dubbing_id}/render/{language} | Render Audio Or Video For The Given Language |
| GET | /v1/dubbing | List Dubs |
| POST | /v1/dubbing | Dub A Video Or An Audio File |
| GET | /v1/dubbing/{dubbing_id} | Get Dubbing |
| DELETE | /v1/dubbing/{dubbing_id} | Delete Dubbing |
| GET | /v1/dubbing/{dubbing_id}/audio/{language_code} | Get Dubbed File |
| GET | /v1/dubbing/{dubbing_id}/transcript/{language_code} | Get Dubbed Transcript |
| GET | /v1/dubbing/{dubbing_id}/transcripts/{language_code}/format/{format_type} | Retrieve A Transcript |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/models | Get Models |

### audio-native
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/audio-native | Creates Audio Native Enabled Project. |
| GET | /v1/audio-native/{project_id}/settings | Get Audio Native Project Settings |
| POST | /v1/audio-native/{project_id}/content | Update Audio-Native Project Content |
| POST | /v1/audio-native/content | Update Audio-Native Content From Url |

### shared-voices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/shared-voices | Get Voices |

### similar-voices
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/similar-voices | Get Similar Library Voices |

### usage
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/usage/character-stats | Get Characters Usage Metrics |

### pronunciation-dictionaries
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/pronunciation-dictionaries/add-from-file | Add A Pronunciation Dictionary |
| POST | /v1/pronunciation-dictionaries/add-from-rules | Add A Pronunciation Dictionary |
| PATCH | /v1/pronunciation-dictionaries/{pronunciation_dictionary_id} | Update Pronunciation Dictionary |
| GET | /v1/pronunciation-dictionaries/{pronunciation_dictionary_id} | Get Metadata For A Pronunciation Dictionary |
| POST | /v1/pronunciation-dictionaries/{pronunciation_dictionary_id}/set-rules | Set Rules On The Pronunciation Dictionary |
| POST | /v1/pronunciation-dictionaries/{pronunciation_dictionary_id}/add-rules | Add Rules To The Pronunciation Dictionary |
| POST | /v1/pronunciation-dictionaries/{pronunciation_dictionary_id}/remove-rules | Remove Rules From The Pronunciation Dictionary |
| GET | /v1/pronunciation-dictionaries/{dictionary_id}/{version_id}/download | Get A Pls File With A Pronunciation Dictionary Version Rules |
| GET | /v1/pronunciation-dictionaries | Get Pronunciation Dictionaries |

### service-accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/service-accounts/{service_account_user_id}/api-keys | Get Service Account Api Keys Route |
| POST | /v1/service-accounts/{service_account_user_id}/api-keys | Create Service Account Api Key |
| PATCH | /v1/service-accounts/{service_account_user_id}/api-keys/{api_key_id} | Edit Service Account Api Key |
| DELETE | /v1/service-accounts/{service_account_user_id}/api-keys/{api_key_id} | Delete Service Account Api Key |
| GET | /v1/service-accounts | Get Workspace Service Accounts |

### workspace
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/workspace/groups/search | Search User Groups |
| POST | /v1/workspace/groups/{group_id}/members/remove | Delete Member From User Group |
| POST | /v1/workspace/groups/{group_id}/members | Add Member To User Group |
| POST | /v1/workspace/invites/add | Invite User |
| POST | /v1/workspace/invites/add-bulk | Invite Multiple Users |
| DELETE | /v1/workspace/invites | Delete Existing Invitation |
| POST | /v1/workspace/members | Update Member |
| GET | /v1/workspace/resources/{resource_id} | Get Resource |
| POST | /v1/workspace/resources/{resource_id}/share | Share Workspace Resource |
| POST | /v1/workspace/resources/{resource_id}/unshare | Unshare Workspace Resource |
| GET | /v1/workspace/webhooks | List Workspace Webhooks |
| POST | /v1/workspace/webhooks | Create Workspace Webhook |
| PATCH | /v1/workspace/webhooks/{webhook_id} | Update Workspace Webhook |
| DELETE | /v1/workspace/webhooks/{webhook_id} | Delete Workspace Webhook |

### speech-to-text
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/speech-to-text | Speech To Text |
| GET | /v1/speech-to-text/transcripts/{transcription_id} | Get Transcript By Id |
| DELETE | /v1/speech-to-text/transcripts/{transcription_id} | Delete Transcript By Id |

### single-use-token
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/single-use-token/{token_type} | Create Single Use Token |

### forced-alignment
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/forced-alignment | Create Forced Alignment |

### convai
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/convai/conversation/get-signed-url | Get Signed Url |
| GET | /v1/convai/conversation/get_signed_url | Get Signed Url |
| GET | /v1/convai/conversation/token | Get Webrtc Token |
| POST | /v1/convai/twilio/outbound-call | Handle An Outbound Call Via Twilio |
| POST | /v1/convai/twilio/register-call | Register A Twilio Call And Return Twiml |
| POST | /v1/convai/whatsapp/outbound-call | Make An Outbound Call Via Whatsapp |
| POST | /v1/convai/whatsapp/outbound-message | Send An Outbound Message Via Whatsapp |
| POST | /v1/convai/agents/create | Create Agent |
| GET | /v1/convai/agents/summaries | Get Agent Summaries |
| GET | /v1/convai/agents/{agent_id} | Get Agent |
| PATCH | /v1/convai/agents/{agent_id} | Patches An Agent Settings |
| DELETE | /v1/convai/agents/{agent_id} | Delete Agent |
| GET | /v1/convai/agents/{agent_id}/widget | Get Agent Widget Config |
| GET | /v1/convai/agents/{agent_id}/link | Get Shareable Agent Link |
| POST | /v1/convai/agents/{agent_id}/avatar | Post Agent Avatar |
| GET | /v1/convai/agents | List Agents |
| GET | /v1/convai/agent/{agent_id}/knowledge-base/size | Returns The Size Of The Agent'S Knowledge Base |
| POST | /v1/convai/agent/{agent_id}/llm-usage/calculate | Calculate Expected Llm Usage For An Agent |
| POST | /v1/convai/agents/{agent_id}/duplicate | Duplicate Agent |
| POST | /v1/convai/agents/{agent_id}/simulate-conversation | Simulates A Conversation |
| POST | /v1/convai/agents/{agent_id}/simulate-conversation/stream | Simulates A Conversation (Stream) |
| POST | /v1/convai/agent-testing/create | Create Agent Response Test |
| GET | /v1/convai/agent-testing/{test_id} | Get Agent Response Test By Id |
| PUT | /v1/convai/agent-testing/{test_id} | Update Agent Response Test |
| DELETE | /v1/convai/agent-testing/{test_id} | Delete Agent Response Test |
| POST | /v1/convai/agent-testing/summaries | Get Agent Response Test Summaries By Ids |
| GET | /v1/convai/agent-testing | List Agent Response Tests |
| GET | /v1/convai/test-invocations | List Test Invocations |
| POST | /v1/convai/agents/{agent_id}/run-tests | Run Tests On The Agent |
| GET | /v1/convai/test-invocations/{test_invocation_id} | Get Test Invocation |
| POST | /v1/convai/test-invocations/{test_invocation_id}/resubmit | Resubmit Tests |
| GET | /v1/convai/conversations | Get Conversations |
| GET | /v1/convai/users | Get Conversation Users |
| GET | /v1/convai/conversations/{conversation_id} | Get Conversation Details |
| DELETE | /v1/convai/conversations/{conversation_id} | Delete Conversation |
| GET | /v1/convai/conversations/{conversation_id}/audio | Get Conversation Audio |
| POST | /v1/convai/conversations/{conversation_id}/feedback | Send Conversation Feedback |
| GET | /v1/convai/conversations/messages/text-search | Text Search Conversation Messages |
| GET | /v1/convai/conversations/messages/smart-search | Smart Search Conversation Messages |
| POST | /v1/convai/phone-numbers | Import Phone Number |
| GET | /v1/convai/phone-numbers | List Phone Numbers |
| GET | /v1/convai/phone-numbers/{phone_number_id} | Get Phone Number |
| DELETE | /v1/convai/phone-numbers/{phone_number_id} | Delete Phone Number |
| PATCH | /v1/convai/phone-numbers/{phone_number_id} | Update Phone Number |
| POST | /v1/convai/llm-usage/calculate | Calculate Expected Llm Usage |
| GET | /v1/convai/llm/list | List Available Llms |
| POST | /v1/convai/conversations/{conversation_id}/files | Upload File |
| DELETE | /v1/convai/conversations/{conversation_id}/files/{file_id} | Delete File Upload |
| GET | /v1/convai/analytics/live-count | Get Live Count |
| GET | /v1/convai/knowledge-base/summaries | Get Knowledge Base Summaries By Ids |
| POST | /v1/convai/knowledge-base | Add To Knowledge Base |
| GET | /v1/convai/knowledge-base | Get Knowledge Base List |
| POST | /v1/convai/knowledge-base/url | Create Url Document |
| POST | /v1/convai/knowledge-base/file | Create File Document |
| POST | /v1/convai/knowledge-base/text | Create Text Document |
| POST | /v1/convai/knowledge-base/folder | Create Folder |
| PATCH | /v1/convai/knowledge-base/{documentation_id} | Update Document |
| GET | /v1/convai/knowledge-base/{documentation_id} | Get Documentation From Knowledge Base |
| DELETE | /v1/convai/knowledge-base/{documentation_id} | Delete Knowledge Base Document Or Folder |
| POST | /v1/convai/knowledge-base/rag-index | Compute Rag Indexes In Batch |
| GET | /v1/convai/knowledge-base/rag-index | Get Rag Index Overview. |
| POST | /v1/convai/knowledge-base/{documentation_id}/rag-index | Compute Rag Index. |
| GET | /v1/convai/knowledge-base/{documentation_id}/rag-index | Get Rag Indexes Of The Specified Knowledgebase Document. |
| DELETE | /v1/convai/knowledge-base/{documentation_id}/rag-index/{rag_index_id} | Delete Rag Index. |
| GET | /v1/convai/knowledge-base/{documentation_id}/dependent-agents | Get Dependent Agents List |
| GET | /v1/convai/knowledge-base/{documentation_id}/content | Get Document Content |
| GET | /v1/convai/knowledge-base/{documentation_id}/source-file-url | Get Document Source File Url |
| GET | /v1/convai/knowledge-base/{documentation_id}/chunk/{chunk_id} | Get Documentation Chunk From Knowledge Base |
| POST | /v1/convai/knowledge-base/{document_id}/move | Move Entity To Folder |
| POST | /v1/convai/knowledge-base/bulk-move | Bulk Move Entities To Folder |
| POST | /v1/convai/tools | Add Tool |
| GET | /v1/convai/tools | Get Tools |
| GET | /v1/convai/tools/{tool_id} | Get Tool |
| PATCH | /v1/convai/tools/{tool_id} | Update Tool |
| DELETE | /v1/convai/tools/{tool_id} | Delete Tool |
| GET | /v1/convai/tools/{tool_id}/dependent-agents | Get Dependent Agents List |
| GET | /v1/convai/settings | Get Convai Settings |
| PATCH | /v1/convai/settings | Update Convai Settings |
| GET | /v1/convai/settings/dashboard | Get Convai Dashboard Settings |
| PATCH | /v1/convai/settings/dashboard | Update Convai Dashboard Settings |
| POST | /v1/convai/secrets | Create Convai Workspace Secret |
| GET | /v1/convai/secrets | Get Convai Workspace Secrets |
| DELETE | /v1/convai/secrets/{secret_id} | Delete Convai Workspace Secret |
| PATCH | /v1/convai/secrets/{secret_id} | Update Convai Workspace Secret |
| POST | /v1/convai/batch-calling/submit | Submit A Batch Call Request. |
| GET | /v1/convai/batch-calling/workspace | Get All Batch Calls For A Workspace. |
| GET | /v1/convai/batch-calling/{batch_id} | Get A Batch Call By Id. |
| DELETE | /v1/convai/batch-calling/{batch_id} | Delete A Batch Call. |
| POST | /v1/convai/batch-calling/{batch_id}/cancel | Cancel A Batch Call. |
| POST | /v1/convai/batch-calling/{batch_id}/retry | Retry A Batch Call. |
| POST | /v1/convai/sip-trunk/outbound-call | Handle An Outbound Call Via Sip Trunk |
| POST | /v1/convai/mcp-servers | Create Mcp Server |
| GET | /v1/convai/mcp-servers | List Mcp Servers |
| GET | /v1/convai/mcp-servers/{mcp_server_id} | Get Mcp Server |
| DELETE | /v1/convai/mcp-servers/{mcp_server_id} | Delete Mcp Server |
| PATCH | /v1/convai/mcp-servers/{mcp_server_id} | Update Mcp Server Configuration |
| GET | /v1/convai/mcp-servers/{mcp_server_id}/tools | List Mcp Server Tools |
| PATCH | /v1/convai/mcp-servers/{mcp_server_id}/approval-policy | Update Mcp Server Approval Policy |
| POST | /v1/convai/mcp-servers/{mcp_server_id}/tool-approvals | Create Mcp Server Tool Approval |
| DELETE | /v1/convai/mcp-servers/{mcp_server_id}/tool-approvals/{tool_name} | Delete Mcp Server Tool Approval |
| POST | /v1/convai/mcp-servers/{mcp_server_id}/tool-configs | Create Mcp Tool Configuration Override |
| GET | /v1/convai/mcp-servers/{mcp_server_id}/tool-configs/{tool_name} | Get Mcp Tool Configuration Override |
| PATCH | /v1/convai/mcp-servers/{mcp_server_id}/tool-configs/{tool_name} | Update Mcp Tool Configuration Override |
| DELETE | /v1/convai/mcp-servers/{mcp_server_id}/tool-configs/{tool_name} | Delete Mcp Tool Configuration Override |
| GET | /v1/convai/whatsapp-accounts/{phone_number_id} | Get Whatsapp Account |
| PATCH | /v1/convai/whatsapp-accounts/{phone_number_id} | Update Whatsapp Account |
| DELETE | /v1/convai/whatsapp-accounts/{phone_number_id} | Delete Whatsapp Account |
| GET | /v1/convai/whatsapp-accounts | List Whatsapp Accounts |
| POST | /v1/convai/agents/{agent_id}/branches | Create A New Branch |
| GET | /v1/convai/agents/{agent_id}/branches | List Agent Branches |
| GET | /v1/convai/agents/{agent_id}/branches/{branch_id} | Get Agent Branch |
| PATCH | /v1/convai/agents/{agent_id}/branches/{branch_id} | Update Agent Branch |
| POST | /v1/convai/agents/{agent_id}/branches/{source_branch_id}/merge | Merge A Branch Into A Target Branch |
| POST | /v1/convai/agents/{agent_id}/deployments | Create Or Update Deployments |
| POST | /v1/convai/agents/{agent_id}/drafts | Create Agent Draft |
| DELETE | /v1/convai/agents/{agent_id}/drafts | Delete Agent Draft |

### music
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/music/plan | Generate Composition Plan |
| POST | /v1/music | Compose Music |
| POST | /v1/music/detailed | Compose Music With A Detailed Response |
| POST | /v1/music/stream | Stream Composed Music |
| POST | /v1/music/upload | Upload Music |
| POST | /v1/music/stem-separation | Stem Separation |

### docs
| Method | Path | Description |
|--------|------|-------------|
| GET | /docs | Redirect To Mintlify |

## Enhanced Skill Content
## Question Mapping

- "How do I convert text to speech?" -> POST /v1/text-to-speech/{voice_id}
- "How can I stream audio in real time?" -> POST /v1/text-to-speech/{voice_id}/stream
- "What voices are available in my account?" -> GET /v2/voices
- "How many characters do I have left this month?" -> GET /v1/user/subscription
- "How do I clone my voice?" -> POST /v1/voices/pvc
- "Can I generate a sound effect from a text description?" -> POST /v1/sound-generation
- "How do I dub a video into another language?" -> POST /v1/dubbing
- "How do I create a conversational AI agent?" -> POST /v1/convai/agents/create
- "How do I check my generation history?" -> GET /v1/history
- "How do I generate music from a prompt?" -> POST /v1/music
- "How do I get word-level timestamps for generated speech?" -> POST /v1/text-to-speech/{voice_id}/with-timestamps
- "How do I design a new voice from a description?" -> POST /v1/text-to-voice/create-previews
- "How do I transcribe an audio file?" -> POST /v1/speech-to-text
- "How do I create a multi-speaker dialogue?" -> POST /v1/text-to-dialogue
- "How do I remove background noise from audio?" -> POST /v1/audio-isolation

## Response Tips

- **History endpoints**: Paginated via `start_after_history_item_id` cursor (not page numbers); check `has_more` to continue fetching. Audio endpoints return raw binary, not JSON.
- **Voice endpoints**: v2 uses `next_page_token` cursor pagination with `total_count`; v1 returns all voices at once. Voice objects nest `labels` as a map and `settings` as a sub-object.
- **TTS endpoints**: Non-timestamp variants return raw audio bytes (check `Content-Type` header). Timestamp variants return JSON with `audio_base64`, `alignment`, and `normalized_alignment`.
- **Dubbing endpoints**: Paginated via `cursor`/`has_more`. The resource endpoint returns deeply nested `speaker_tracks`, `speaker_segments`, and `renders` maps keyed by language. Errors 403/404/425 on audio download mean not-authorized, not-found, or still-processing.
- **ConvAI endpoints**: Agent config is deeply nested (conversation_config > agent > prompt > tools). Conversations and agents both use cursor pagination. 422 is the universal validation error.
- **Studio endpoints**: Projects contain chapters; snapshots represent converted audio. The `state` field tracks conversion progress. Content blocks are nested inside `content.blocks`.
- **Music endpoints**: `POST /v1/music/plan` returns a composition plan you feed into `POST /v1/music`. Raw audio is returned from the generation endpoint.
- **Subscription/User**: `character_count` vs `character_limit` gives current usage. `next_character_count_reset_unix` is the reset timestamp.

## Anomaly Flags

- **Character quota approaching**: Surface a warning when `character_count` exceeds 80% of `character_limit` (from `GET /v1/user/subscription`). Alert on `can_extend_character_limit: false` when near the cap.
- **Voice slot limits**: Flag when `voice_slots_used` equals `voice_limit` -- the next voice add will fail.
- **Dubbing still processing**: A 425 response on `GET /v1/dubbing/{dubbing_id}/audio/{language_code}` means the dub is not ready. Poll the status endpoint and surface estimated wait time based on `expected_duration_sec`.
- **Conversion failures**: Studio project/chapter conversion can fail silently. Check `state` field and `last_conversion_error` after calling convert endpoints.
- **PVC voice training state**: After uploading samples and calling train, the voice may take time. Surface the training status and captcha verification requirements proactively.
- **Model deprecation**: When using ConvAI LLMs, check `GET /v1/convai/llm/list` for `default_deprecation_config` -- warn if selected models are approaching fallback dates.
- **Rate limit / 422 patterns**: All endpoints return 422 on validation errors. Surface the specific field that failed rather than generic "request failed" messages.
- **Batch call status**: After submitting batch calls, monitor `status` field. Flag `failed` or stalled batches where `total_calls_finished` lags `total_calls_dispatched`.

## Playbook

### 1. Generate Speech from Text and Download

1. List available voices: `GET /v2/voices` (filter by `voice_type` or `search` if needed).
2. Pick a voice_id from the results.
3. Check subscription: `GET /v1/user/subscription` to confirm enough characters remain.
4. Generate audio: `POST /v1/text-to-speech/{voice_id}` with your text, desired `model_id` (default `eleven_multilingual_v2`), and `output_format`.
5. Save the binary response as an audio file (Content-Type tells you the format).
6. Optionally verify the generation appeared in history: `GET /v1/history`.

### 2. Clone a Voice with Professional Voice Cloning (PVC)

1. Create the PVC voice: `POST /v1/voices/pvc` with name and language.
2. Upload audio samples: `POST /v1/voices/pvc/{voice_id}/samples` (multiple samples improve quality).
3. Review and trim each sample: `POST /v1/voices/pvc/{voice_id}/samples/{sample_id}` with trim parameters.
4. If multi-speaker audio, separate speakers: `POST /v1/voices/pvc/{voice_id}/samples/{sample_id}/separate-speakers`, then select the right speaker.
5. Complete captcha verification: `GET /v1/voices/pvc/{voice_id}/captcha` then `POST /v1/voices/pvc/{voice_id}/captcha`.
6. Submit for training: `POST /v1/voices/pvc/{voice_id}/train`.
7. Use the voice with TTS once training completes.

### 3. Dub a Video into Multiple Languages

1. Submit the dubbing job: `POST /v1/dubbing` with your source video/audio file and target languages.
2. Poll status: `GET /v1/dubbing/{dubbing_id}` until `status` is `dubbed`.
3. Review the resource: `GET /v1/dubbing/resource/{dubbing_id}` to inspect speaker segments and translations.
4. Edit segments if needed: `PATCH /v1/dubbing/resource/{dubbing_id}/segment/{segment_id}/{language}` to fix text or timing.
5. Re-dub edited segments: `POST /v1/dubbing/resource/{dubbing_id}/dub` with the changed segment IDs.
6. Render the final output: `POST /v1/dubbing/resource/{dubbing_id}/render/{language}` with desired format (mp4, mp3, etc.).
7. Download audio: `GET /v1/dubbing/{dubbing_id}/audio/{language_code}`.
8. Download transcript: `GET /v1/dubbing/{dubbing_id}/transcript/{language_code}` in srt/webvtt/json.

### 4. Build and Deploy a Conversational AI Agent

1. Create a knowledge base document: `POST /v1/convai/knowledge-base/url` or `/file` or `/text`.
2. Index it for RAG: `POST /v1/convai/knowledge-base/{documentation_id}/rag-index` with your embedding model.
3. Create a tool if the agent needs external actions: `POST /v1/convai/tools`.
4. Create the agent: `POST /v1/convai/agents/create` with conversation config (voice, prompt, knowledge base references, tool IDs).
5. Test with simulation: `POST /v1/convai/agents/{agent_id}/simulate-conversation` to validate behavior.
6. Get a widget config for embedding: `GET /v1/convai/agents/{agent_id}/widget`.
7. Monitor live conversations: `GET /v1/convai/conversations` filtered by `agent_id`, and check `GET /v1/convai/analytics/live-count`.

### 5. Generate Music from a Prompt

1. Plan the composition: `POST /v1/music/plan` with your text prompt to get style tags and sections.
2. Review and adjust the composition plan (modify sections, durations, styles).
3. Generate the track: `POST /v1/music` with the composition plan, or use `POST /v1/music/stream` for streaming output.
4. For detailed control with timestamps: `POST /v1/music/detailed` with `with_timestamps: true`.
5. Optionally separate stems: `POST /v1/music/stem-separation` to isolate vocals, drums, bass, etc.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
