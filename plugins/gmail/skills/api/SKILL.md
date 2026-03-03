---
name: gmail-api
description: "Gmail API skill. Use when working with Gmail for gmail. Covers 79 endpoints."
version: 1.0.0
generator: lapsh
---

# Gmail API
API version: v1

## Auth
OAuth2 | OAuth2

## Base URL
https://gmail.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /gmail/v1/users/{userId}/drafts -- verify access
3. POST /gmail/v1/users/{userId}/drafts -- create first drafts

## Endpoints

79 endpoints across 1 groups. See references/api-spec.lap for full details.

### gmail
| Method | Path | Description |
|--------|------|-------------|
| GET | /gmail/v1/users/{userId}/drafts | Lists the drafts in the user's mailbox. |
| POST | /gmail/v1/users/{userId}/drafts | Creates a new draft with the `DRAFT` label. |
| POST | /gmail/v1/users/{userId}/drafts/send | Sends the specified, existing draft to the recipients in the `To`, `Cc`, and `Bcc` headers. |
| DELETE | /gmail/v1/users/{userId}/drafts/{id} | Immediately and permanently deletes the specified draft. Does not simply trash it. |
| GET | /gmail/v1/users/{userId}/drafts/{id} | Gets the specified draft. |
| PUT | /gmail/v1/users/{userId}/drafts/{id} | Replaces a draft's content. |
| GET | /gmail/v1/users/{userId}/history | Lists the history of all changes to the given mailbox. History results are returned in chronological order (increasing `historyId`). |
| GET | /gmail/v1/users/{userId}/labels | Lists all labels in the user's mailbox. |
| POST | /gmail/v1/users/{userId}/labels | Creates a new label. |
| DELETE | /gmail/v1/users/{userId}/labels/{id} | Immediately and permanently deletes the specified label and removes it from any messages and threads that it is applied to. |
| GET | /gmail/v1/users/{userId}/labels/{id} | Gets the specified label. |
| PATCH | /gmail/v1/users/{userId}/labels/{id} | Patch the specified label. |
| PUT | /gmail/v1/users/{userId}/labels/{id} | Updates the specified label. |
| GET | /gmail/v1/users/{userId}/messages | Lists the messages in the user's mailbox. |
| POST | /gmail/v1/users/{userId}/messages | Directly inserts a message into only this user's mailbox similar to `IMAP APPEND`, bypassing most scanning and classification. Does not send a message. |
| POST | /gmail/v1/users/{userId}/messages/batchDelete | Deletes many messages by message ID. Provides no guarantees that messages were not already deleted or even existed at all. |
| POST | /gmail/v1/users/{userId}/messages/batchModify | Modifies the labels on the specified messages. |
| POST | /gmail/v1/users/{userId}/messages/import | Imports a message into only this user's mailbox, with standard email delivery scanning and classification similar to receiving via SMTP. This method doesn't perform SPF checks, so it might not work for some spam messages, such as those attempting to perform domain spoofing. This method does not send a message. Note: This function doesn't trigger forwarding rules or filters set up by the user. |
| POST | /gmail/v1/users/{userId}/messages/send | Sends the specified message to the recipients in the `To`, `Cc`, and `Bcc` headers. For example usage, see [Sending email](https://developers.google.com/gmail/api/guides/sending). |
| DELETE | /gmail/v1/users/{userId}/messages/{id} | Immediately and permanently deletes the specified message. This operation cannot be undone. Prefer `messages.trash` instead. |
| GET | /gmail/v1/users/{userId}/messages/{id} | Gets the specified message. |
| POST | /gmail/v1/users/{userId}/messages/{id}/modify | Modifies the labels on the specified message. |
| POST | /gmail/v1/users/{userId}/messages/{id}/trash | Moves the specified message to the trash. |
| POST | /gmail/v1/users/{userId}/messages/{id}/untrash | Removes the specified message from the trash. |
| GET | /gmail/v1/users/{userId}/messages/{messageId}/attachments/{id} | Gets the specified message attachment. |
| GET | /gmail/v1/users/{userId}/profile | Gets the current user's Gmail profile. |
| GET | /gmail/v1/users/{userId}/settings/autoForwarding | Gets the auto-forwarding setting for the specified account. |
| PUT | /gmail/v1/users/{userId}/settings/autoForwarding | Updates the auto-forwarding setting for the specified account. A verified forwarding address must be specified when auto-forwarding is enabled. This method is only available to service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/cse/identities | Lists the client-side encrypted identities for an authenticated user. |
| POST | /gmail/v1/users/{userId}/settings/cse/identities | Creates and configures a client-side encryption identity that's authorized to send mail from the user account. Google publishes the S/MIME certificate to a shared domain-wide directory so that people within a Google Workspace organization can encrypt and send mail to the identity. |
| DELETE | /gmail/v1/users/{userId}/settings/cse/identities/{cseEmailAddress} | Deletes a client-side encryption identity. The authenticated user can no longer use the identity to send encrypted messages. You cannot restore the identity after you delete it. Instead, use the CreateCseIdentity method to create another identity with the same configuration. |
| GET | /gmail/v1/users/{userId}/settings/cse/identities/{cseEmailAddress} | Retrieves a client-side encryption identity configuration. |
| PATCH | /gmail/v1/users/{userId}/settings/cse/identities/{emailAddress} | Associates a different key pair with an existing client-side encryption identity. The updated key pair must validate against Google's [S/MIME certificate profiles](https://support.google.com/a/answer/7300887). |
| GET | /gmail/v1/users/{userId}/settings/cse/keypairs | Lists client-side encryption key pairs for an authenticated user. |
| POST | /gmail/v1/users/{userId}/settings/cse/keypairs | Creates and uploads a client-side encryption S/MIME public key certificate chain and private key metadata for the authenticated user. |
| GET | /gmail/v1/users/{userId}/settings/cse/keypairs/{keyPairId} | Retrieves an existing client-side encryption key pair. |
| POST | /gmail/v1/users/{userId}/settings/cse/keypairs/{keyPairId}:disable | Turns off a client-side encryption key pair. The authenticated user can no longer use the key pair to decrypt incoming CSE message texts or sign outgoing CSE mail. To regain access, use the EnableCseKeyPair to turn on the key pair. After 30 days, you can permanently delete the key pair by using the ObliterateCseKeyPair method. |
| POST | /gmail/v1/users/{userId}/settings/cse/keypairs/{keyPairId}:enable | Turns on a client-side encryption key pair that was turned off. The key pair becomes active again for any associated client-side encryption identities. |
| POST | /gmail/v1/users/{userId}/settings/cse/keypairs/{keyPairId}:obliterate | Deletes a client-side encryption key pair permanently and immediately. You can only permanently delete key pairs that have been turned off for more than 30 days. To turn off a key pair, use the DisableCseKeyPair method. Gmail can't restore or decrypt any messages that were encrypted by an obliterated key. Authenticated users and Google Workspace administrators lose access to reading the encrypted messages. |
| GET | /gmail/v1/users/{userId}/settings/delegates | Lists the delegates for the specified account. This method is only available to service account clients that have been delegated domain-wide authority. |
| POST | /gmail/v1/users/{userId}/settings/delegates | Adds a delegate with its verification status set directly to `accepted`, without sending any verification email. The delegate user must be a member of the same Google Workspace organization as the delegator user. Gmail imposes limitations on the number of delegates and delegators each user in a Google Workspace organization can have. These limits depend on your organization, but in general each user can have up to 25 delegates and up to 10 delegators. Note that a delegate user must be referred to by their primary email address, and not an email alias. Also note that when a new delegate is created, there may be up to a one minute delay before the new delegate is available for use. This method is only available to service account clients that have been delegated domain-wide authority. |
| DELETE | /gmail/v1/users/{userId}/settings/delegates/{delegateEmail} | Removes the specified delegate (which can be of any verification status), and revokes any verification that may have been required for using it. Note that a delegate user must be referred to by their primary email address, and not an email alias. This method is only available to service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/delegates/{delegateEmail} | Gets the specified delegate. Note that a delegate user must be referred to by their primary email address, and not an email alias. This method is only available to service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/filters | Lists the message filters of a Gmail user. |
| POST | /gmail/v1/users/{userId}/settings/filters | Creates a filter. Note: you can only create a maximum of 1,000 filters. |
| DELETE | /gmail/v1/users/{userId}/settings/filters/{id} | Immediately and permanently deletes the specified filter. |
| GET | /gmail/v1/users/{userId}/settings/filters/{id} | Gets a filter. |
| GET | /gmail/v1/users/{userId}/settings/forwardingAddresses | Lists the forwarding addresses for the specified account. |
| POST | /gmail/v1/users/{userId}/settings/forwardingAddresses | Creates a forwarding address. If ownership verification is required, a message will be sent to the recipient and the resource's verification status will be set to `pending`; otherwise, the resource will be created with verification status set to `accepted`. This method is only available to service account clients that have been delegated domain-wide authority. |
| DELETE | /gmail/v1/users/{userId}/settings/forwardingAddresses/{forwardingEmail} | Deletes the specified forwarding address and revokes any verification that may have been required. This method is only available to service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/forwardingAddresses/{forwardingEmail} | Gets the specified forwarding address. |
| GET | /gmail/v1/users/{userId}/settings/imap | Gets IMAP settings. |
| PUT | /gmail/v1/users/{userId}/settings/imap | Updates IMAP settings. |
| GET | /gmail/v1/users/{userId}/settings/language | Gets language settings. |
| PUT | /gmail/v1/users/{userId}/settings/language | Updates language settings. If successful, the return object contains the `displayLanguage` that was saved for the user, which may differ from the value passed into the request. This is because the requested `displayLanguage` may not be directly supported by Gmail but have a close variant that is, and so the variant may be chosen and saved instead. |
| GET | /gmail/v1/users/{userId}/settings/pop | Gets POP settings. |
| PUT | /gmail/v1/users/{userId}/settings/pop | Updates POP settings. |
| GET | /gmail/v1/users/{userId}/settings/sendAs | Lists the send-as aliases for the specified account. The result includes the primary send-as address associated with the account as well as any custom "from" aliases. |
| POST | /gmail/v1/users/{userId}/settings/sendAs | Creates a custom "from" send-as alias. If an SMTP MSA is specified, Gmail will attempt to connect to the SMTP service to validate the configuration before creating the alias. If ownership verification is required for the alias, a message will be sent to the email address and the resource's verification status will be set to `pending`; otherwise, the resource will be created with verification status set to `accepted`. If a signature is provided, Gmail will sanitize the HTML before saving it with the alias. This method is only available to service account clients that have been delegated domain-wide authority. |
| DELETE | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail} | Deletes the specified send-as alias. Revokes any verification that may have been required for using it. This method is only available to service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail} | Gets the specified send-as alias. Fails with an HTTP 404 error if the specified address is not a member of the collection. |
| PATCH | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail} | Patch the specified send-as alias. |
| PUT | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail} | Updates a send-as alias. If a signature is provided, Gmail will sanitize the HTML before saving it with the alias. Addresses other than the primary address for the account can only be updated by service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail}/smimeInfo | Lists S/MIME configs for the specified send-as alias. |
| POST | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail}/smimeInfo | Insert (upload) the given S/MIME config for the specified send-as alias. Note that pkcs12 format is required for the key. |
| DELETE | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail}/smimeInfo/{id} | Deletes the specified S/MIME config for the specified send-as alias. |
| GET | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail}/smimeInfo/{id} | Gets the specified S/MIME config for the specified send-as alias. |
| POST | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail}/smimeInfo/{id}/setDefault | Sets the default S/MIME config for the specified send-as alias. |
| POST | /gmail/v1/users/{userId}/settings/sendAs/{sendAsEmail}/verify | Sends a verification email to the specified send-as alias address. The verification status must be `pending`. This method is only available to service account clients that have been delegated domain-wide authority. |
| GET | /gmail/v1/users/{userId}/settings/vacation | Gets vacation responder settings. |
| PUT | /gmail/v1/users/{userId}/settings/vacation | Updates vacation responder settings. |
| POST | /gmail/v1/users/{userId}/stop | Stop receiving push notifications for the given user mailbox. |
| GET | /gmail/v1/users/{userId}/threads | Lists the threads in the user's mailbox. |
| DELETE | /gmail/v1/users/{userId}/threads/{id} | Immediately and permanently deletes the specified thread. Any messages that belong to the thread are also deleted. This operation cannot be undone. Prefer `threads.trash` instead. |
| GET | /gmail/v1/users/{userId}/threads/{id} | Gets the specified thread. |
| POST | /gmail/v1/users/{userId}/threads/{id}/modify | Modifies the labels applied to the thread. This applies to all messages in the thread. |
| POST | /gmail/v1/users/{userId}/threads/{id}/trash | Moves the specified thread to the trash. Any messages that belong to the thread are also moved to the trash. |
| POST | /gmail/v1/users/{userId}/threads/{id}/untrash | Removes the specified thread from the trash. Any messages that belong to the thread are also removed from the trash. |
| POST | /gmail/v1/users/{userId}/watch | Set up or update a push notification watch on the given user mailbox. |

## Enhanced Skill Content
## Question Mapping

- "How do I search for emails matching a query?" -> GET /gmail/v1/users/{userId}/messages (use `q` parameter with Gmail search syntax)
- "How do I send an email?" -> POST /gmail/v1/users/{userId}/messages/send
- "How do I read a specific email?" -> GET /gmail/v1/users/{userId}/messages/{id} (use `format` to control detail level)
- "How do I download an attachment?" -> GET /gmail/v1/users/{userId}/messages/{messageId}/attachments/{id}
- "How do I delete multiple emails at once?" -> POST /gmail/v1/users/{userId}/messages/batchDelete
- "How do I move emails to trash?" -> POST /gmail/v1/users/{userId}/messages/{id}/trash
- "How do I create a label and apply it to messages?" -> POST /gmail/v1/users/{userId}/labels then POST /gmail/v1/users/{userId}/messages/{id}/modify with `addLabelIds`
- "How do I list all drafts?" -> GET /gmail/v1/users/{userId}/drafts
- "How do I get my mailbox stats?" -> GET /gmail/v1/users/{userId}/profile
- "How do I set up a vacation auto-reply?" -> PUT /gmail/v1/users/{userId}/settings/vacation
- "How do I create a filter to auto-label incoming mail?" -> POST /gmail/v1/users/{userId}/settings/filters
- "How do I check what changed since my last sync?" -> GET /gmail/v1/users/{userId}/history (provide `startHistoryId`)
- "How do I get all messages in a thread?" -> GET /gmail/v1/users/{userId}/threads/{id}
- "How do I add a delegate to my account?" -> POST /gmail/v1/users/{userId}/settings/delegates
- "How do I set up push notifications for new mail?" -> POST /gmail/v1/users/{userId}/watch (requires a Pub/Sub `topicName`)

## Response Tips

- **Messages & Drafts lists**: Paginated via `nextPageToken`; pass it as `pageToken` to get the next page. `resultSizeEstimate` is approximate, not exact -- do not use it as a total count.
- **Message detail**: The `payload` object is recursive -- `parts` contains nested `parts` for multipart MIME. Body `data` is base64url-encoded. Use `format=metadata` with `metadataHeaders` to cheaply fetch only specific headers (Subject, From, Date).
- **Threads**: The `messages` array contains full message objects in chronological order. The thread-level `snippet` reflects the latest message.
- **History**: Returns change records (messagesAdded, labelsAdded, etc.) as maps inside the `history` array. An empty `history` array with a new `historyId` means no changes.
- **Labels**: System labels (INBOX, SENT, TRASH, SPAM) have `type: "system"` and cannot be deleted or renamed. Only user-created labels are mutable.
- **Settings (sendAs, delegates, forwarding)**: `verificationStatus` must be `"accepted"` before the resource becomes active. Pending resources are non-functional.
- **Batch operations**: `batchDelete` and `batchModify` return empty 200 responses -- success is implied by absence of error. Invalid IDs are silently ignored.
- **Attachments**: The `data` field is base64url-encoded (not standard base64). Decode with URL-safe alphabet before writing to disk.

## Anomaly Flags

- **Rate limit errors (HTTP 429)**: Gmail enforces per-user and per-project quotas. Surface 429 responses immediately and suggest exponential backoff. Batch endpoints count as one quota unit per message, not per call.
- **History gap (HTTP 404 on history)**: If `startHistoryId` is too old, the API returns 404. Surface this and advise the agent to do a full resync instead of incremental.
- **Delegation verification stuck**: If `verificationStatus` remains `"pending"` after delegate creation, flag that the delegate must accept from their own account.
- **Watch expiration approaching**: The `expiration` field from `/watch` is a Unix timestamp (ms). Proactively warn when it is within 24 hours of expiry -- push notifications will silently stop.
- **Oversized batch requests**: `batchDelete` and `batchModify` accept up to 1000 IDs. If the caller passes more, flag it before the call fails.
- **Permanent delete vs trash**: `DELETE /messages/{id}` is irreversible (permanent delete). If the intent seems to be "move to trash," flag the difference and suggest `/messages/{id}/trash` instead.
- **S/MIME certificate expiration**: When `expiration` on an S/MIME info object is in the past, surface that the certificate is expired and encryption will fail.
- **Label count limits**: Gmail allows up to ~500 user labels. If label creation fails, surface this as a likely quota issue.

## Playbook

### 1. Search and Read Emails

1. Call `GET /gmail/v1/users/me/messages` with `q` set to a Gmail search query (e.g., `from:alice@example.com after:2025/01/01 has:attachment`).
2. Iterate through `messages` array; each entry contains only `id` and `threadId`.
3. For each message of interest, call `GET /gmail/v1/users/me/messages/{id}` with `format=full` to get headers, body, and attachments.
4. If `nextPageToken` is present, repeat step 1 with `pageToken` to fetch the next page.
5. To download attachments, extract `attachmentId` from the message `payload.parts` and call `GET /gmail/v1/users/me/messages/{messageId}/attachments/{id}`.

### 2. Compose, Draft, and Send an Email

1. Build a base64url-encoded RFC 2822 message with To, From, Subject, and body.
2. Call `POST /gmail/v1/users/me/drafts` with the `raw` field containing the encoded message to save as draft.
3. Optionally update the draft via `PUT /gmail/v1/users/me/drafts/{id}` with revised content.
4. When ready, call `POST /gmail/v1/users/me/drafts/send` with the draft `id` to send it.
5. Alternatively, skip drafting and call `POST /gmail/v1/users/me/messages/send` directly with the `raw` message.

### 3. Organize with Labels and Filters

1. Call `GET /gmail/v1/users/me/labels` to list existing labels and check if the target label exists.
2. If not, call `POST /gmail/v1/users/me/labels` with `name`, `labelListVisibility`, and optionally `color`.
3. Apply the label to existing messages: call `POST /gmail/v1/users/me/messages/batchModify` with `ids` and `addLabelIds`.
4. To auto-label future messages, call `POST /gmail/v1/users/me/settings/filters` with `criteria` (e.g., `from`, `subject`, `query`) and `action.addLabelIds`.

### 4. Incremental Sync with History

1. On first sync, call `GET /gmail/v1/users/me/profile` and store the returned `historyId`.
2. On subsequent syncs, call `GET /gmail/v1/users/me/history` with `startHistoryId` set to the stored value.
3. Process the `history` array -- each record describes messages added, deleted, or labels changed.
4. Update `startHistoryId` to the `historyId` from the response for the next sync cycle.
5. If the API returns 404 (history too old), fall back to a full `GET /messages` listing and store the fresh `historyId`.

### 5. Set Up Push Notifications

1. Create a Google Cloud Pub/Sub topic and grant `gmail-api-push@system.gserviceaccount.com` publish permissions.
2. Call `POST /gmail/v1/users/me/watch` with `topicName` set to `projects/{project}/topics/{topic}` and optionally `labelIds` + `labelFilterAction` to filter.
3. Store the returned `expiration` timestamp and schedule a renewal before it lapses (typically every 7 days).
4. When a Pub/Sub notification arrives, extract `historyId` from the payload and run the incremental sync playbook (above) to fetch changes.
5. To stop notifications, call `POST /gmail/v1/users/me/stop`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
