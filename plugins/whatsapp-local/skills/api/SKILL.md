---
name: whatsapp-business-api
description: "WhatsApp Business API skill. Use when working with WhatsApp Business for users, settings, account. Covers 55 endpoints."
version: 1.0.0
generator: lapsh
---

# WhatsApp Business API
API version: 1.0

## Auth
Bearer basic | Bearer bearer

## Base URL
http://example.com/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /settings/application -- verify access
3. POST /users/login -- create first login

## Endpoints

55 endpoints across 12 groups. See references/api-spec.lap for full details.

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users/login | Login-User |
| POST | /users | Create-User |
| GET | /users/{UserUsername} | Get-User |
| PUT | /users/{UserUsername} | Update-User |
| DELETE | /users/{UserUsername} | Delete-User |
| POST | /users/logout | Logout-User |

### settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /settings/application | Get-Application-Settings |
| DELETE | /settings/application | Reset-Application-Settings |
| PATCH | /settings/application | Update-Application-Settings |
| GET | /settings/application/media/providers | Get-Media-Providers |
| POST | /settings/application/media/providers | Update-Media-Providers |
| DELETE | /settings/application/media/providers/{ProviderName} | Delete-Media-Providers |
| POST | /settings/backup | Backup-Settings |
| POST | /settings/restore | Restore-Settings |
| GET | /settings/business/profile | Get-Business-Profile |
| POST | /settings/business/profile | Update-Business-Profile |
| GET | /settings/profile/about | Get-Profile-About |
| PATCH | /settings/profile/about | Update-Profile-About |
| POST | /settings/account/two-step | Enable-Two-Step |
| DELETE | /settings/account/two-step | Disable-Two-Step |
| GET | /settings/profile/photo | Get-Profile-Photo |
| POST | /settings/profile/photo | Update-Profile-Photo |
| DELETE | /settings/profile/photo | Delete-Profile-Photo |

### account
| Method | Path | Description |
|--------|------|-------------|
| POST | /account/shards | Set-Shards |
| POST | /account/verify | Register-Account |
| POST | /account | Request-Code |

### contacts
| Method | Path | Description |
|--------|------|-------------|
| POST | /contacts | Check-Contact |

### messages
| Method | Path | Description |
|--------|------|-------------|
| POST | /messages | Send-Message |
| PUT | /messages/{MessageID} | Mark-Message-As-Read |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | Get-All-Groups |
| POST | /groups | Create-Group |
| GET | /groups/{GroupId} | Get-Group-Info |
| PUT | /groups/{GroupId} | Update-Group-Info |
| GET | /groups/{GroupId}/invite | Get-Group-Invite |
| DELETE | /groups/{GroupId}/invite | Delete-Group-Invite |
| DELETE | /groups/{GroupId}/participants | Remove-Group-Participant |
| POST | /groups/{GroupId}/leave | Leave-Group |
| GET | /groups/{GroupId}/icon | Get-Group-Icon-Binary |
| POST | /groups/{GroupId}/icon | Set-Group-Icon |
| DELETE | /groups/{GroupId}/icon | Delete-Group-Icon |
| DELETE | /groups/{GroupId}/admins | Demote-Group-Admin |
| PATCH | /groups/{GroupId}/admins | Promote-To-Group-Admin |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Check-Health |

### media
| Method | Path | Description |
|--------|------|-------------|
| POST | /media | Upload-Media |
| GET | /media/{MediaId} | Download-Media |
| DELETE | /media/{MediaId} | Delete-Media |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats/app | Get-App-Stats |
| GET | /stats/db | Get-DB-Stats |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics | Get-Metrics (since v2.21.3) |

### support
| Method | Path | Description |
|--------|------|-------------|
| GET | /support | Get-Support-Info |

### certificates
| Method | Path | Description |
|--------|------|-------------|
| GET | /certificates/external/ca | Download-CA-Certificate |
| POST | /certificates/external | Upload-Certificate |
| GET | /certificates/webhooks/ca | Download Webhook CA Certificate |
| POST | /certificates/webhooks/ca | Upload Webhook CA Certificate |
| DELETE | /certificates/webhooks/ca | Delete Webhook CA Certificate |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the WhatsApp API?" -> POST /users/login
- "How do I create a new admin user?" -> POST /users
- "How do I send a text message to a phone number?" -> POST /messages
- "How do I send an image or document to someone?" -> POST /messages
- "How do I mark a message as read?" -> PUT /messages/{MessageID}
- "How do I check if the WhatsApp service is running?" -> GET /health
- "How do I update my business profile info?" -> POST /settings/business/profile
- "How do I create a new group and add members?" -> POST /groups
- "How do I remove someone from a group?" -> DELETE /groups/{GroupId}/participants
- "How do I register my phone number with WhatsApp?" -> POST /account
- "How do I upload media for sending?" -> POST /media
- "How do I back up my application settings?" -> POST /settings/backup
- "How do I enable two-step verification?" -> POST /settings/account/two-step
- "How do I check contacts for WhatsApp availability?" -> POST /contacts
- "How do I view app or database statistics?" -> GET /stats/app

## Response Tips

- **users**: Login returns a bearer token for subsequent requests; store it for the session.
- **messages**: Responses confirm acceptance, not delivery; track message status via webhooks for delivery/read receipts.
- **settings**: GET returns nested maps (`settings.profile.about.text`); PATCH returns `meta` with API version and `errors` array -- check `errors` even on 200.
- **account**: Registration may return 201 (complete) or 202 (pending verification) -- branch on status code.
- **contacts**: Use `blocking: "wait"` for synchronous results; `"no_wait"` returns immediately and delivers results via webhook.
- **groups**: All group endpoints require the `GroupId` path parameter; list groups first with GET /groups to discover IDs.
- **media**: GET /media/{MediaId} returns binary content, not JSON; handle the response as a file download.
- **stats/metrics**: Accept an optional `format` query param; default format may vary -- specify explicitly for consistency.
- **certificates**: Responses are typically raw certificate data; handle as PEM/DER content rather than JSON.

## Anomaly Flags

- **Dual status codes on registration**: POST /account can return 201 or 202 -- surface which path was taken and whether verification (POST /account/verify) is still needed.
- **Webhook misconfiguration**: If `webhooks.url` in application settings is empty or unreachable, message delivery receipts and async contact results will be silently lost.
- **Unhealthy heartbeat intervals**: Flag if `unhealthy_interval` or `heartbeat_interval` in application settings are set to unusually low values (can cause false health alerts) or unusually high values (delayed failure detection).
- **Two-step verification state**: Surface when two-step verification is disabled (DELETE /settings/account/two-step was called) as this reduces account security.
- **Shard count changes**: POST /account/shards accepts powers of 2 (1-32); changing shards is disruptive -- flag if a shard change request is detected.
- **Auto-download media settings**: Warn if `media.auto_download` includes large media types that could consume storage rapidly.
- **Callback persist disabled**: If `callback_persist` is set to false, undelivered callbacks will be lost on restart -- flag this configuration risk.

## Playbook

### 1. Send a Text Message to a New Contact

1. Authenticate: POST /users/login with your credentials to obtain a bearer token.
2. Check contact availability: POST /contacts with `{"contacts": ["+1234567890"], "blocking": "wait"}`.
3. Send the message: POST /messages with `{"to": "1234567890", "type": "text", "text": {"body": "Hello!"}}`.
4. Monitor delivery: Listen on your configured webhook URL for status callbacks, or mark as read when replied to via PUT /messages/{MessageID}.

### 2. Set Up a New WhatsApp Business Account

1. Register phone number: POST /account with `{"cc": "1", "phone_number": "5551234567", "method": "sms", "cert": "<your_cert>"}`.
2. If 202 returned, verify: POST /account/verify with the SMS code received `{"code": "123456"}`.
3. Enable two-step verification: POST /settings/account/two-step with `{"pin": "123456"}`.
4. Set business profile: POST /settings/business/profile with address, description, email, vertical, and websites.
5. Set profile about text: PATCH /settings/profile/about with `{"text": "Your business tagline"}`.
6. Configure webhooks: PATCH /settings/application with `{"webhooks": {"url": "https://your-server.com/webhook"}}`.

### 3. Create and Manage a Group

1. Create group: POST /groups with `{"subject": "Team Chat"}` -- note the returned GroupId.
2. Get invite link: GET /groups/{GroupId}/invite to share with new members.
3. Set group icon: POST /groups/{GroupId}/icon with the image payload.
4. Promote admins: PATCH /groups/{GroupId}/admins with `{"wa_ids": ["member_wa_id"]}`.
5. To remove a member later: DELETE /groups/{GroupId}/participants with `{"wa_ids": ["member_wa_id"]}`.

### 4. Back Up and Restore Settings

1. Create backup: POST /settings/backup with `{"password": "secure_passphrase"}` -- save the returned `settings.data` string securely.
2. To restore: POST /settings/restore with `{"password": "secure_passphrase", "data": "<backup_data_string>"}`.
3. Verify restoration: GET /settings/application and GET /settings/business/profile to confirm settings are correct.

### 5. Upload and Send Media

1. Upload media file: POST /media with the file as multipart form data -- note the returned MediaId.
2. Send media message: POST /messages with `{"to": "1234567890", "type": "image", "image": {"id": "<MediaId>"}}` (substitute `type` and the corresponding field for document, video, or audio).
3. To retrieve media later: GET /media/{MediaId} to download the binary content.
4. Clean up: DELETE /media/{MediaId} when the media is no longer needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
