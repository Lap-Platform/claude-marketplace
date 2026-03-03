---
name: telegram-bot-api
description: "Telegram Bot API skill. Use when working with Telegram Bot for getUpdates, setWebhook, deleteWebhook. Covers 74 endpoints."
version: 1.0.0
generator: lapsh
---

# Telegram Bot API
API version: 5.0.0

## Auth
No authentication required.

## Base URL
https://api.telegram.org/bot{token}

## Setup
1. No auth setup needed
3. POST /getUpdates -- create first getUpdates

## Endpoints

74 endpoints across 74 groups. See references/api-spec.lap for full details.

### getUpdates
| Method | Path | Description |
|--------|------|-------------|
| POST | /getUpdates | Use this method to receive incoming updates using long polling ([wiki](https://en.wikipedia.org/wiki/Push_technology#Long_polling)). An Array of [Update](https://core.telegram.org/bots/api/#update) objects is returned. |

### setWebhook
| Method | Path | Description |
|--------|------|-------------|
| POST | /setWebhook | Use this method to specify a url and receive incoming updates via an outgoing webhook. Whenever there is an update for the bot, we will send an HTTPS POST request to the specified url, containing a JSON-serialized [Update](https://core.telegram.org/bots/api/#update). In case of an unsuccessful request, we will give up after a reasonable amount of attempts. Returns *True* on success. |

### deleteWebhook
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteWebhook | Use this method to remove webhook integration if you decide to switch back to [getUpdates](https://core.telegram.org/bots/api/#getupdates). Returns *True* on success. |

### getWebhookInfo
| Method | Path | Description |
|--------|------|-------------|
| POST | /getWebhookInfo | Use this method to get current webhook status. Requires no parameters. On success, returns a [WebhookInfo](https://core.telegram.org/bots/api/#webhookinfo) object. If the bot is using [getUpdates](https://core.telegram.org/bots/api/#getupdates), will return an object with the *url* field empty. |

### getMe
| Method | Path | Description |
|--------|------|-------------|
| POST | /getMe | A simple method for testing your bot's auth token. Requires no parameters. Returns basic information about the bot in form of a [User](https://core.telegram.org/bots/api/#user) object. |

### logOut
| Method | Path | Description |
|--------|------|-------------|
| POST | /logOut | Use this method to log out from the cloud Bot API server before launching the bot locally. You **must** log out the bot before running it locally, otherwise there is no guarantee that the bot will receive updates. After a successful call, you can immediately log in on a local server, but will not be able to log in back to the cloud Bot API server for 10 minutes. Returns *True* on success. Requires no parameters. |

### close
| Method | Path | Description |
|--------|------|-------------|
| POST | /close | Use this method to close the bot instance before moving it from one local server to another. You need to delete the webhook before calling this method to ensure that the bot isn't launched again after server restart. The method will return error 429 in the first 10 minutes after the bot is launched. Returns *True* on success. Requires no parameters. |

### sendMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendMessage | Use this method to send text messages. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### forwardMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /forwardMessage | Use this method to forward messages of any kind. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### copyMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /copyMessage | Use this method to copy messages of any kind. The method is analogous to the method [forwardMessages](https://core.telegram.org/bots/api/#forwardmessages), but the copied message doesn't have a link to the original message. Returns the [MessageId](https://core.telegram.org/bots/api/#messageid) of the sent message on success. |

### sendPhoto
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendPhoto | Use this method to send photos. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### sendAudio
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendAudio | Use this method to send audio files, if you want Telegram clients to display them in the music player. Your audio must be in the .MP3 or .M4A format. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. Bots can currently send audio files of up to 50 MB in size, this limit may be changed in the future. |

### sendDocument
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendDocument | Use this method to send general files. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. Bots can currently send files of any type of up to 50 MB in size, this limit may be changed in the future. |

### sendVideo
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendVideo | Use this method to send video files, Telegram clients support mp4 videos (other formats may be sent as [Document](https://core.telegram.org/bots/api/#document)). On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. Bots can currently send video files of up to 50 MB in size, this limit may be changed in the future. |

### sendAnimation
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendAnimation | Use this method to send animation files (GIF or H.264/MPEG-4 AVC video without sound). On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. Bots can currently send animation files of up to 50 MB in size, this limit may be changed in the future. |

### sendVoice
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendVoice | Use this method to send audio files, if you want Telegram clients to display the file as a playable voice message. For this to work, your audio must be in an .OGG file encoded with OPUS (other formats may be sent as [Audio](https://core.telegram.org/bots/api/#audio) or [Document](https://core.telegram.org/bots/api/#document)). On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. Bots can currently send voice messages of up to 50 MB in size, this limit may be changed in the future. |

### sendVideoNote
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendVideoNote | As of [v.4.0](https://telegram.org/blog/video-messages-and-telescope), Telegram clients support rounded square mp4 videos of up to 1 minute long. Use this method to send video messages. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### sendMediaGroup
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendMediaGroup | Use this method to send a group of photos, videos, documents or audios as an album. Documents and audio files can be only grouped in an album with messages of the same type. On success, an array of [Messages](https://core.telegram.org/bots/api/#message) that were sent is returned. |

### sendLocation
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendLocation | Use this method to send point on the map. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### editMessageLiveLocation
| Method | Path | Description |
|--------|------|-------------|
| POST | /editMessageLiveLocation | Use this method to edit live location messages. A location can be edited until its *live\_period* expires or editing is explicitly disabled by a call to [stopMessageLiveLocation](https://core.telegram.org/bots/api/#stopmessagelivelocation). On success, if the edited message is not an inline message, the edited [Message](https://core.telegram.org/bots/api/#message) is returned, otherwise *True* is returned. |

### stopMessageLiveLocation
| Method | Path | Description |
|--------|------|-------------|
| POST | /stopMessageLiveLocation | Use this method to stop updating a live location message before *live\_period* expires. On success, if the message was sent by the bot, the sent [Message](https://core.telegram.org/bots/api/#message) is returned, otherwise *True* is returned. |

### sendVenue
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendVenue | Use this method to send information about a venue. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### sendContact
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendContact | Use this method to send phone contacts. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### sendPoll
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendPoll | Use this method to send a native poll. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### sendDice
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendDice | Use this method to send an animated emoji that will display a random value. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### sendChatAction
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendChatAction | Use this method when you need to tell the user that something is happening on the bot's side. The status is set for 5 seconds or less (when a message arrives from your bot, Telegram clients clear its typing status). Returns *True* on success. |

### getUserProfilePhotos
| Method | Path | Description |
|--------|------|-------------|
| POST | /getUserProfilePhotos | Use this method to get a list of profile pictures for a user. Returns a [UserProfilePhotos](https://core.telegram.org/bots/api/#userprofilephotos) object. |

### getFile
| Method | Path | Description |
|--------|------|-------------|
| POST | /getFile | Use this method to get basic info about a file and prepare it for downloading. For the moment, bots can download files of up to 20MB in size. On success, a [File](https://core.telegram.org/bots/api/#file) object is returned. The file can then be downloaded via the link `https://api.telegram.org/file/bot<token>/<file_path>`, where `<file_path>` is taken from the response. It is guaranteed that the link will be valid for at least 1 hour. When the link expires, a new one can be requested by calling [getFile](https://core.telegram.org/bots/api/#getfile) again. |

### kickChatMember
| Method | Path | Description |
|--------|------|-------------|
| POST | /kickChatMember | Use this method to kick a user from a group, a supergroup or a channel. In the case of supergroups and channels, the user will not be able to return to the group on their own using invite links, etc., unless [unbanned](https://core.telegram.org/bots/api/#unbanchatmember) first. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Returns *True* on success. |

### unbanChatMember
| Method | Path | Description |
|--------|------|-------------|
| POST | /unbanChatMember | Use this method to unban a previously kicked user in a supergroup or channel. The user will **not** return to the group or channel automatically, but will be able to join via link, etc. The bot must be an administrator for this to work. By default, this method guarantees that after the call the user is not a member of the chat, but will be able to join it. So if the user is a member of the chat they will also be **removed** from the chat. If you don't want this, use the parameter *only\_if\_banned*. Returns *True* on success. |

### restrictChatMember
| Method | Path | Description |
|--------|------|-------------|
| POST | /restrictChatMember | Use this method to restrict a user in a supergroup. The bot must be an administrator in the supergroup for this to work and must have the appropriate admin rights. Pass *True* for all permissions to lift restrictions from a user. Returns *True* on success. |

### promoteChatMember
| Method | Path | Description |
|--------|------|-------------|
| POST | /promoteChatMember | Use this method to promote or demote a user in a supergroup or a channel. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Pass *False* for all boolean parameters to demote a user. Returns *True* on success. |

### setChatAdministratorCustomTitle
| Method | Path | Description |
|--------|------|-------------|
| POST | /setChatAdministratorCustomTitle | Use this method to set a custom title for an administrator in a supergroup promoted by the bot. Returns *True* on success. |

### setChatPermissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /setChatPermissions | Use this method to set default chat permissions for all members. The bot must be an administrator in the group or a supergroup for this to work and must have the *can\_restrict\_members* admin rights. Returns *True* on success. |

### exportChatInviteLink
| Method | Path | Description |
|--------|------|-------------|
| POST | /exportChatInviteLink | Use this method to generate a new invite link for a chat; any previously generated link is revoked. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Returns the new invite link as *String* on success. |

### setChatPhoto
| Method | Path | Description |
|--------|------|-------------|
| POST | /setChatPhoto | Use this method to set a new profile photo for the chat. Photos can't be changed for private chats. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Returns *True* on success. |

### deleteChatPhoto
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteChatPhoto | Use this method to delete a chat photo. Photos can't be changed for private chats. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Returns *True* on success. |

### setChatTitle
| Method | Path | Description |
|--------|------|-------------|
| POST | /setChatTitle | Use this method to change the title of a chat. Titles can't be changed for private chats. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Returns *True* on success. |

### setChatDescription
| Method | Path | Description |
|--------|------|-------------|
| POST | /setChatDescription | Use this method to change the description of a group, a supergroup or a channel. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Returns *True* on success. |

### pinChatMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /pinChatMessage | Use this method to add a message to the list of pinned messages in a chat. If the chat is not a private chat, the bot must be an administrator in the chat for this to work and must have the 'can\_pin\_messages' admin right in a supergroup or 'can\_edit\_messages' admin right in a channel. Returns *True* on success. |

### unpinChatMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /unpinChatMessage | Use this method to remove a message from the list of pinned messages in a chat. If the chat is not a private chat, the bot must be an administrator in the chat for this to work and must have the 'can\_pin\_messages' admin right in a supergroup or 'can\_edit\_messages' admin right in a channel. Returns *True* on success. |

### unpinAllChatMessages
| Method | Path | Description |
|--------|------|-------------|
| POST | /unpinAllChatMessages | Use this method to clear the list of pinned messages in a chat. If the chat is not a private chat, the bot must be an administrator in the chat for this to work and must have the 'can\_pin\_messages' admin right in a supergroup or 'can\_edit\_messages' admin right in a channel. Returns *True* on success. |

### leaveChat
| Method | Path | Description |
|--------|------|-------------|
| POST | /leaveChat | Use this method for your bot to leave a group, supergroup or channel. Returns *True* on success. |

### getChat
| Method | Path | Description |
|--------|------|-------------|
| POST | /getChat | Use this method to get up to date information about the chat (current name of the user for one-on-one conversations, current username of a user, group or channel, etc.). Returns a [Chat](https://core.telegram.org/bots/api/#chat) object on success. |

### getChatAdministrators
| Method | Path | Description |
|--------|------|-------------|
| POST | /getChatAdministrators | Use this method to get a list of administrators in a chat. On success, returns an Array of [ChatMember](https://core.telegram.org/bots/api/#chatmember) objects that contains information about all chat administrators except other bots. If the chat is a group or a supergroup and no administrators were appointed, only the creator will be returned. |

### getChatMembersCount
| Method | Path | Description |
|--------|------|-------------|
| POST | /getChatMembersCount | Use this method to get the number of members in a chat. Returns *Int* on success. |

### getChatMember
| Method | Path | Description |
|--------|------|-------------|
| POST | /getChatMember | Use this method to get information about a member of a chat. Returns a [ChatMember](https://core.telegram.org/bots/api/#chatmember) object on success. |

### setChatStickerSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /setChatStickerSet | Use this method to set a new group sticker set for a supergroup. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Use the field *can\_set\_sticker\_set* optionally returned in [getChat](https://core.telegram.org/bots/api/#getchat) requests to check if the bot can use this method. Returns *True* on success. |

### deleteChatStickerSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteChatStickerSet | Use this method to delete a group sticker set from a supergroup. The bot must be an administrator in the chat for this to work and must have the appropriate admin rights. Use the field *can\_set\_sticker\_set* optionally returned in [getChat](https://core.telegram.org/bots/api/#getchat) requests to check if the bot can use this method. Returns *True* on success. |

### answerCallbackQuery
| Method | Path | Description |
|--------|------|-------------|
| POST | /answerCallbackQuery | Use this method to send answers to callback queries sent from [inline keyboards](/bots#inline-keyboards-and-on-the-fly-updating). The answer will be displayed to the user as a notification at the top of the chat screen or as an alert. On success, *True* is returned. |

### setMyCommands
| Method | Path | Description |
|--------|------|-------------|
| POST | /setMyCommands | Use this method to change the list of the bot's commands. Returns *True* on success. |

### getMyCommands
| Method | Path | Description |
|--------|------|-------------|
| POST | /getMyCommands | Use this method to get the current list of the bot's commands. Requires no parameters. Returns Array of [BotCommand](https://core.telegram.org/bots/api/#botcommand) on success. |

### editMessageText
| Method | Path | Description |
|--------|------|-------------|
| POST | /editMessageText | Use this method to edit text and [game](https://core.telegram.org/bots/api/#games) messages. On success, if the edited message is not an inline message, the edited [Message](https://core.telegram.org/bots/api/#message) is returned, otherwise *True* is returned. |

### editMessageCaption
| Method | Path | Description |
|--------|------|-------------|
| POST | /editMessageCaption | Use this method to edit captions of messages. On success, if the edited message is not an inline message, the edited [Message](https://core.telegram.org/bots/api/#message) is returned, otherwise *True* is returned. |

### editMessageMedia
| Method | Path | Description |
|--------|------|-------------|
| POST | /editMessageMedia | Use this method to edit animation, audio, document, photo, or video messages. If a message is part of a message album, then it can be edited only to an audio for audio albums, only to a document for document albums and to a photo or a video otherwise. When an inline message is edited, a new file can't be uploaded. Use a previously uploaded file via its file\_id or specify a URL. On success, if the edited message was sent by the bot, the edited [Message](https://core.telegram.org/bots/api/#message) is returned, otherwise *True* is returned. |

### editMessageReplyMarkup
| Method | Path | Description |
|--------|------|-------------|
| POST | /editMessageReplyMarkup | Use this method to edit only the reply markup of messages. On success, if the edited message is not an inline message, the edited [Message](https://core.telegram.org/bots/api/#message) is returned, otherwise *True* is returned. |

### stopPoll
| Method | Path | Description |
|--------|------|-------------|
| POST | /stopPoll | Use this method to stop a poll which was sent by the bot. On success, the stopped [Poll](https://core.telegram.org/bots/api/#poll) with the final results is returned. |

### deleteMessage
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteMessage | Use this method to delete a message, including service messages, with the following limitations: |

### sendSticker
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendSticker | Use this method to send static .WEBP or [animated](https://telegram.org/blog/animated-stickers) .TGS stickers. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### getStickerSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /getStickerSet | Use this method to get a sticker set. On success, a [StickerSet](https://core.telegram.org/bots/api/#stickerset) object is returned. |

### uploadStickerFile
| Method | Path | Description |
|--------|------|-------------|
| POST | /uploadStickerFile | Use this method to upload a .PNG file with a sticker for later use in *createNewStickerSet* and *addStickerToSet* methods (can be used multiple times). Returns the uploaded [File](https://core.telegram.org/bots/api/#file) on success. |

### createNewStickerSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /createNewStickerSet | Use this method to create a new sticker set owned by a user. The bot will be able to edit the sticker set thus created. You **must** use exactly one of the fields *png\_sticker* or *tgs\_sticker*. Returns *True* on success. |

### addStickerToSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /addStickerToSet | Use this method to add a new sticker to a set created by the bot. You **must** use exactly one of the fields *png\_sticker* or *tgs\_sticker*. Animated stickers can be added to animated sticker sets and only to them. Animated sticker sets can have up to 50 stickers. Static sticker sets can have up to 120 stickers. Returns *True* on success. |

### setStickerPositionInSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /setStickerPositionInSet | Use this method to move a sticker in a set created by the bot to a specific position. Returns *True* on success. |

### deleteStickerFromSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteStickerFromSet | Use this method to delete a sticker from a set created by the bot. Returns *True* on success. |

### setStickerSetThumb
| Method | Path | Description |
|--------|------|-------------|
| POST | /setStickerSetThumb | Use this method to set the thumbnail of a sticker set. Animated thumbnails can be set for animated sticker sets only. Returns *True* on success. |

### answerInlineQuery
| Method | Path | Description |
|--------|------|-------------|
| POST | /answerInlineQuery | Use this method to send answers to an inline query. On success, *True* is returned. |

### sendInvoice
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendInvoice | Use this method to send invoices. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### answerShippingQuery
| Method | Path | Description |
|--------|------|-------------|
| POST | /answerShippingQuery | If you sent an invoice requesting a shipping address and the parameter *is\_flexible* was specified, the Bot API will send an [Update](https://core.telegram.org/bots/api/#update) with a *shipping\_query* field to the bot. Use this method to reply to shipping queries. On success, True is returned. |

### answerPreCheckoutQuery
| Method | Path | Description |
|--------|------|-------------|
| POST | /answerPreCheckoutQuery | Once the user has confirmed their payment and shipping details, the Bot API sends the final confirmation in the form of an [Update](https://core.telegram.org/bots/api/#update) with the field *pre\_checkout\_query*. Use this method to respond to such pre-checkout queries. On success, True is returned. **Note:** The Bot API must receive an answer within 10 seconds after the pre-checkout query was sent. |

### setPassportDataErrors
| Method | Path | Description |
|--------|------|-------------|
| POST | /setPassportDataErrors | Informs a user that some of the Telegram Passport elements they provided contains errors. The user will not be able to re-submit their Passport to you until the errors are fixed (the contents of the field for which you returned the error must change). Returns *True* on success. |

### sendGame
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendGame | Use this method to send a game. On success, the sent [Message](https://core.telegram.org/bots/api/#message) is returned. |

### setGameScore
| Method | Path | Description |
|--------|------|-------------|
| POST | /setGameScore | Use this method to set the score of the specified user in a game. On success, if the message was sent by the bot, returns the edited [Message](https://core.telegram.org/bots/api/#message), otherwise returns *True*. Returns an error, if the new score is not greater than the user's current score in the chat and *force* is *False*. |

### getGameHighScores
| Method | Path | Description |
|--------|------|-------------|
| POST | /getGameHighScores | Use this method to get data for high score tables. Will return the score of the specified user and several of their neighbors in a game. On success, returns an *Array* of [GameHighScore](https://core.telegram.org/bots/api/#gamehighscore) objects. |

## Enhanced Skill Content
## Question Mapping

- "How do I send a text message to a user or group?" -> POST /sendMessage
- "How do I check for new incoming messages?" -> POST /getUpdates
- "How do I get information about my bot?" -> POST /getMe
- "How do I forward a message from one chat to another?" -> POST /forwardMessage
- "How do I download a file that a user sent?" -> POST /getFile
- "How do I kick or ban a user from a group?" -> POST /kickChatMember
- "How do I set up a webhook to receive updates?" -> POST /setWebhook
- "How do I send multiple photos or videos at once?" -> POST /sendMediaGroup
- "How do I edit a message the bot already sent?" -> POST /editMessageText
- "How do I create a poll or quiz in a chat?" -> POST /sendPoll
- "How do I get the list of admins in a group?" -> POST /getChatAdministrators
- "How do I send an invoice for payment?" -> POST /sendInvoice
- "How do I respond to a callback button press?" -> POST /answerCallbackQuery
- "How do I share a live location that updates?" -> POST /sendLocation (with live_period)
- "How do I delete a message?" -> POST /deleteMessage

## Response Tips

- **All endpoints**: Every response wraps in `{ok: bool, result: ...}` -- always check `ok` before reading `result`; on failure, `description` and `error_code` fields appear instead.
- **Message-sending endpoints** (sendMessage, sendPhoto, etc.): `result` is a deeply nested Message object -- extract `result.message_id` to reference later; media fields (photo, document, video) contain `file_id` for re-sending and `file_unique_id` for deduplication.
- **getUpdates**: `result` is an array of Update objects -- track the highest `update_id` and pass `offset = update_id + 1` on next call to acknowledge; no built-in pagination beyond this.
- **Edit endpoints** (editMessageText, editMessageCaption, etc.): `result` is either a Message object (regular messages) or `true` (inline messages) -- type-check before parsing.
- **Boolean endpoints** (kickChatMember, setChatPermissions, etc.): `result` is simply `true` on success -- no additional data returned.
- **getFile**: The returned `file_path` is relative -- construct the download URL as `https://api.telegram.org/file/bot{token}/{file_path}`.
- **Payments** (answerShippingQuery, answerPreCheckoutQuery): Pass `ok: false` with `error_message` to reject -- omitting `error_message` when `ok` is false causes silent failures.

## Anomaly Flags

- **`ok: false` responses**: Surface the `error_code` and `description` immediately -- common codes are 400 (bad request), 401 (invalid token), 403 (bot lacks permissions), 429 (rate limited with `retry_after` seconds).
- **429 Too Many Requests**: Extract `retry_after` from the error response and warn the user about the cooldown period before retrying.
- **getWebhookInfo `pending_update_count`**: If this grows steadily, the webhook endpoint is failing to process updates -- surface counts above 100 as a warning.
- **getWebhookInfo `last_error_message`**: Surface any non-empty value -- indicates Telegram cannot reach the webhook URL.
- **`migrate_to_chat_id` in responses**: Indicates a group was upgraded to a supergroup -- the agent should flag this and suggest updating the stored chat_id.
- **`kickChatMember` naming**: This is the legacy name (renamed to `banChatMember` in newer API versions) -- flag if the user is on a newer Bot API version.
- **File size limits**: `getFile` only works for files up to 20MB -- surface a warning if attempting to download larger files.
- **`left_chat_member` or `new_chat_members` in updates**: These indicate membership changes that may affect bot functionality -- surface when the bot itself is removed.

## Playbook

### Send a Message with Inline Keyboard Buttons

1. Call POST /sendMessage with `chat_id`, `text`, and `reply_markup` set to `{"inline_keyboard": [[{"text": "Click me", "callback_data": "btn1"}]]}`.
2. Store the returned `result.message_id` for later editing.
3. When the user presses the button, receive a callback_query update via /getUpdates or webhook.
4. Call POST /answerCallbackQuery with the `callback_query_id` to dismiss the loading indicator.
5. Optionally call POST /editMessageText to update the original message based on the button pressed.

### Set Up Webhook-Based Updates

1. Call POST /getWebhookInfo to check current webhook status.
2. If a webhook is already set that you want to replace, call POST /deleteWebhook first (optionally with `drop_pending_updates: true`).
3. Call POST /setWebhook with your HTTPS URL as a parameter.
4. Verify success by calling POST /getWebhookInfo again -- confirm `url` matches and `last_error_message` is empty.
5. Monitor `pending_update_count` periodically to ensure your server is processing updates.

### Moderate a Group Chat

1. Call POST /getChat with the `chat_id` to retrieve current group settings and permissions.
2. To restrict a user, call POST /restrictChatMember with `user_id` and a `permissions` object setting specific booleans (e.g., `can_send_messages: false`).
3. To ban a user, call POST /kickChatMember with `user_id` and optionally `until_date` for a temporary ban.
4. To promote a user to admin, call POST /promoteChatMember with the desired permission flags.
5. Optionally call POST /setChatAdministratorCustomTitle to assign a visible title to the new admin.

### Send and Track a Live Location

1. Call POST /sendLocation with `chat_id`, `latitude`, `longitude`, and `live_period` (60-86400 seconds).
2. Store the returned `result.message_id` and `result.chat.id`.
3. Periodically call POST /editMessageLiveLocation with updated `latitude`, `longitude`, `chat_id`, and `message_id`.
4. When tracking is complete, call POST /stopMessageLiveLocation with `chat_id` and `message_id` to finalize.

### Process a Payment

1. Call POST /sendInvoice with `chat_id`, `title`, `description`, `payload`, `provider_token`, `currency`, and `prices` array.
2. When a shipping query arrives (if `is_flexible` was true), call POST /answerShippingQuery with `shipping_query_id`, `ok: true`, and available `shipping_options`.
3. When a pre-checkout query arrives, validate the order and call POST /answerPreCheckoutQuery with `pre_checkout_query_id` and `ok: true` (or `ok: false` with `error_message` to reject).
4. After successful payment, a message with `successful_payment` will arrive in updates -- extract `telegram_payment_charge_id` and `provider_payment_charge_id` for records.
5. If passport data is required, handle errors via POST /setPassportDataErrors to notify the user of issues with their submitted documents.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
