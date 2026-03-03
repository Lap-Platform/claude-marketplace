---
name: amazon-lex-runtime-v2
description: "Amazon Lex Runtime V2 API skill. Use when working with Amazon Lex Runtime V2 for bots. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Lex Runtime V2
API version: 2020-08-07

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId} -- verify access
3. POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId} -- create first sessions

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### bots
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId} | Removes session information for a specified bot, alias, and user ID.  You can use this operation to restart a conversation with a bot. When you remove a session, the entire history of the session is removed so that you can start again. You don't need to delete a session. Sessions have a time limit and will expire. Set the session time limit when you create the bot. The default is 5 minutes, but you can specify anything between 1 minute and 24 hours. If you specify a bot or alias ID that doesn't exist, you receive a BadRequestException.  If the locale doesn't exist in the bot, or if the locale hasn't been enables for the alias, you receive a BadRequestException. |
| GET | /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId} | Returns session information for a specified bot, alias, and user. For example, you can use this operation to retrieve session information for a user that has left a long-running session in use. If the bot, alias, or session identifier doesn't exist, Amazon Lex V2 returns a BadRequestException. If the locale doesn't exist or is not enabled for the alias, you receive a BadRequestException. |
| POST | /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId} | Creates a new session or modifies an existing session with an Amazon Lex V2 bot. Use this operation to enable your application to set the state of the bot. |
| POST | /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/text | Sends user input to Amazon Lex V2. Client applications use this API to send requests to Amazon Lex V2 at runtime. Amazon Lex V2 then interprets the user input using the machine learning model that it build for the bot. In response, Amazon Lex V2 returns the next message to convey to the user and an optional response card to display. If the optional post-fulfillment response is specified, the messages are returned as follows. For more information, see PostFulfillmentStatusSpecification.    Success message - Returned if the Lambda function completes successfully and the intent state is fulfilled or ready fulfillment if the message is present.    Failed message - The failed message is returned if the Lambda function throws an exception or if the Lambda function returns a failed intent state without a message.    Timeout message - If you don't configure a timeout message and a timeout, and the Lambda function doesn't return within 30 seconds, the timeout message is returned. If you configure a timeout, the timeout message is returned when the period times out.    For more information, see Completion message. |
| POST | /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/utterance | Sends user input to Amazon Lex V2. You can send text or speech. Clients use this API to send text and audio requests to Amazon Lex V2 at runtime. Amazon Lex V2 interprets the user input using the machine learning model built for the bot. The following request fields must be compressed with gzip and then base64 encoded before you send them to Amazon Lex V2.    requestAttributes   sessionState   The following response fields are compressed using gzip and then base64 encoded by Amazon Lex V2. Before you can use these fields, you must decode and decompress them.    inputTranscript   interpretations   messages   requestAttributes   sessionState   The example contains a Java application that compresses and encodes a Java object to send to Amazon Lex V2, and a second that decodes and decompresses a response from Amazon Lex V2. If the optional post-fulfillment response is specified, the messages are returned as follows. For more information, see PostFulfillmentStatusSpecification.    Success message - Returned if the Lambda function completes successfully and the intent state is fulfilled or ready fulfillment if the message is present.    Failed message - The failed message is returned if the Lambda function throws an exception or if the Lambda function returns a failed intent state without a message.    Timeout message - If you don't configure a timeout message and a timeout, and the Lambda function doesn't return within 30 seconds, the timeout message is returned. If you configure a timeout, the timeout message is returned when the period times out.    For more information, see Completion message. |

## Enhanced Skill Content
## Question Mapping

- "How do I send a text message to my Lex bot?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/text
- "How do I send audio/voice input to a Lex bot?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/utterance
- "How do I get the current session state for a user?" -> GET /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}
- "How do I check what intent was recognized?" -> GET /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}
- "How do I end or reset a conversation session?" -> DELETE /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}
- "How do I set session attributes or override dialog state?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}
- "How do I check which slots have been filled so far?" -> GET /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}
- "How do I force the bot to elicit a specific slot?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}
- "How do I implement speech-to-text with Lex?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/utterance
- "How do I get the bot's response messages after user input?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/text
- "How do I pass runtime hints to improve slot recognition?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/text
- "How do I handle a multi-bot setup and know which bot responded?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}/text
- "How do I restore a session with custom dialog state?" -> POST /bots/{botId}/botAliases/{botAliasId}/botLocales/{localeId}/sessions/{sessionId}

## Response Tips

- **Session GET/Text/Utterance**: `interpretations` is an array ranked by confidence -- the first entry is the top match; always check `intent.state` (`ReadyForFulfillment`, `Failed`, `InProgress`) before acting.
- **Session PUT**: Returns serialized strings for `messages`, `sessionState`, and `requestAttributes` (not parsed objects) -- deserialize them before use.
- **Session DELETE**: Returns the IDs of the deleted session; a 200 with null fields means the session did not exist or was already expired.
- **Utterance (audio)**: Response fields like `messages`, `interpretations`, `sessionState` are JSON-encoded strings in headers/body; `audioStream` is raw binary -- handle Content-Type accordingly.
- **All endpoints**: Every path requires all four segments (`botId`, `botAliasId`, `localeId`, `sessionId`); a 404 typically means one of these identifiers is wrong, not that the resource is missing.

## Anomaly Flags

- **`intent.state` = `Failed`**: The bot could not match any intent -- surface this so the caller can implement a fallback or escalation path.
- **`dialogAction.type` = `Close`**: The conversation is ending -- warn if the caller continues sending input to a closed session.
- **`confirmationState` = `Denied`**: The user rejected the intent confirmation -- flag for retry or alternative flow logic.
- **Empty `interpretations` array**: No intents matched at all -- likely indicates the bot model needs retraining or the input was unintelligible.
- **`recognizedBotMember` present**: Response came from a delegated bot in a multi-bot setup -- surface bot name/ID so the caller knows which bot handled it.
- **`slotToElicit` set but slot already filled**: The bot is re-asking for a slot -- may indicate a validation failure or ambiguous input worth surfacing.
- **Audio `inputTranscript` empty or unexpected**: Speech recognition may have failed silently -- flag when transcript is blank despite audio input.

## Playbook

### 1. Send a Text Message and Process the Response

1. Construct the path using your `botId`, `botAliasId`, `localeId`, and `sessionId`.
2. POST to `.../sessions/{sessionId}/text` with `{"text": "user input here"}`.
3. Read `sessionState.dialogAction.type` to determine next step: `ElicitSlot` (ask user for more info), `ConfirmIntent` (ask user to confirm), `Delegate` (bot decides), or `Close` (done).
4. Display `messages[]` to the user -- iterate the array since the bot may return multiple message groups.
5. If `dialogAction.type` is `ReadyForFulfillment`, extract filled slots from `sessionState.intent.slots` and execute your business logic.

### 2. Implement a Voice Conversation Loop

1. POST to `.../sessions/{sessionId}/utterance` with `Content-Type: audio/pcm` (or supported format) and the audio bytes as `inputStream`.
2. Set `Response-Content-Type` to your desired audio output format (e.g., `audio/mpeg`).
3. Parse the response: read `inputTranscript` to verify what was heard, check `sessionState` (JSON string) for dialog state.
4. Play back `audioStream` to the user if present.
5. Repeat until `dialogAction.type` is `Close` or `ReadyForFulfillment`.

### 3. Override Session State Mid-Conversation

1. GET `.../sessions/{sessionId}` to retrieve the current session state.
2. Modify the returned `sessionState` object -- e.g., set `dialogAction.type` to `ElicitSlot` and `slotToElicit` to the desired slot name, or inject `sessionAttributes`.
3. POST (PUT) to `.../sessions/{sessionId}` with the modified `sessionState` in the body.
4. Optionally include `messages` to display a custom prompt to the user.
5. On the next user turn, the bot will continue from your overridden state.

### 4. Gracefully End and Clean Up a Session

1. GET `.../sessions/{sessionId}` to capture final session state, slot values, and attributes for logging.
2. Extract any fulfilled intent data from `sessionState.intent` for downstream processing.
3. DELETE `.../sessions/{sessionId}` to release server-side resources.
4. Verify the 200 response returns matching `sessionId` to confirm cleanup succeeded.

### 5. Handle Slot Elicitation with Runtime Hints

1. POST to `.../sessions/{sessionId}/text` with `text` and include `sessionState.runtimeHints.slotHints` to bias slot recognition (e.g., provide likely city names for a location slot).
2. Structure hints as nested maps: `{intentName: {slotName: {subSlotName: {runtimeHintValues: [{phrase: "hint"}]}}}}`.
3. Check the response `sessionState.intent.slots` to see if the hinted value was recognized.
4. If `dialogAction.type` is still `ElicitSlot` for the same slot, the hint did not match -- adjust hints or prompt the user differently.
5. Continue the loop until all required slots are filled and `intent.state` is `ReadyForFulfillment`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
