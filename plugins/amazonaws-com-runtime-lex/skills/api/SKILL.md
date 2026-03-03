---
name: amazon-lex-runtime-service
description: "Amazon Lex Runtime Service API skill. Use when working with Amazon Lex Runtime Service for bot. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Lex Runtime Service
API version: 2016-11-28

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /bot/{botName}/alias/{botAlias}/user/{userId}/session/ -- verify access
3. POST /bot/{botName}/alias/{botAlias}/user/{userId}/content -- create first content

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### bot
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /bot/{botName}/alias/{botAlias}/user/{userId}/session | Removes session information for a specified bot, alias, and user ID. |
| GET | /bot/{botName}/alias/{botAlias}/user/{userId}/session/ | Returns session information for a specified bot, alias, and user ID. |
| POST | /bot/{botName}/alias/{botAlias}/user/{userId}/content | Sends user input (text or speech) to Amazon Lex. Clients use this API to send text and audio requests to Amazon Lex at runtime. Amazon Lex interprets the user input using the machine learning model that it built for the bot.  The PostContent operation supports audio input at 8kHz and 16kHz. You can use 8kHz audio to achieve higher speech recognition accuracy in telephone audio applications.   In response, Amazon Lex returns the next message to convey to the user. Consider the following example messages:     For a user input "I would like a pizza," Amazon Lex might return a response with a message eliciting slot data (for example, PizzaSize): "What size pizza would you like?".     After the user provides all of the pizza order information, Amazon Lex might return a response with a message to get user confirmation: "Order the pizza?".     After the user replies "Yes" to the confirmation prompt, Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered.".     Not all Amazon Lex messages require a response from the user. For example, conclusion statements do not require a response. Some messages require only a yes or no response. In addition to the message, Amazon Lex provides additional context about the message in the response that you can use to enhance client behavior, such as displaying the appropriate client user interface. Consider the following examples:     If the message is to elicit slot data, Amazon Lex returns the following context information:     x-amz-lex-dialog-state header set to ElicitSlot     x-amz-lex-intent-name header set to the intent name in the current context     x-amz-lex-slot-to-elicit header set to the slot name for which the message is eliciting information     x-amz-lex-slots header set to a map of slots configured for the intent with their current values       If the message is a confirmation prompt, the x-amz-lex-dialog-state header is set to Confirmation and the x-amz-lex-slot-to-elicit header is omitted.     If the message is a clarification prompt configured for the intent, indicating that the user intent is not understood, the x-amz-dialog-state header is set to ElicitIntent and the x-amz-slot-to-elicit header is omitted.     In addition, Amazon Lex also returns your application-specific sessionAttributes. For more information, see Managing Conversation Context. |
| POST | /bot/{botName}/alias/{botAlias}/user/{userId}/text | Sends user input to Amazon Lex. Client applications can use this API to send requests to Amazon Lex at runtime. Amazon Lex then interprets the user input using the machine learning model it built for the bot.   In response, Amazon Lex returns the next message to convey to the user an optional responseCard to display. Consider the following example messages:     For a user input "I would like a pizza", Amazon Lex might return a response with a message eliciting slot data (for example, PizzaSize): "What size pizza would you like?"     After the user provides all of the pizza order information, Amazon Lex might return a response with a message to obtain user confirmation "Proceed with the pizza order?".     After the user replies to a confirmation prompt with a "yes", Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered.".     Not all Amazon Lex messages require a user response. For example, a conclusion statement does not require a response. Some messages require only a "yes" or "no" user response. In addition to the message, Amazon Lex provides additional context about the message in the response that you might use to enhance client behavior, for example, to display the appropriate client user interface. These are the slotToElicit, dialogState, intentName, and slots fields in the response. Consider the following examples:    If the message is to elicit slot data, Amazon Lex returns the following context information:    dialogState set to ElicitSlot     intentName set to the intent name in the current context     slotToElicit set to the slot name for which the message is eliciting information     slots set to a map of slots, configured for the intent, with currently known values       If the message is a confirmation prompt, the dialogState is set to ConfirmIntent and SlotToElicit is set to null.    If the message is a clarification prompt (configured for the intent) that indicates that user intent is not understood, the dialogState is set to ElicitIntent and slotToElicit is set to null.     In addition, Amazon Lex also returns your application-specific sessionAttributes. For more information, see Managing Conversation Context. |
| POST | /bot/{botName}/alias/{botAlias}/user/{userId}/session | Creates a new session or modifies an existing session with an Amazon Lex bot. Use this operation to enable your application to set the state of the bot. For more information, see Managing Sessions. |

## Enhanced Skill Content
## Question Mapping

- "How do I send a text message to a Lex bot?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/text
- "How do I send audio or voice input to a Lex bot?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/content
- "How do I check the current session state for a user?" -> GET /bot/{botName}/alias/{botAlias}/user/{userId}/session/
- "How do I end or reset a conversation with a bot?" -> DELETE /bot/{botName}/alias/{botAlias}/user/{userId}/session
- "How do I manually set dialog state or session attributes?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/session
- "How do I get the slots filled so far in a conversation?" -> GET /bot/{botName}/alias/{botAlias}/user/{userId}/session/
- "How do I implement a multi-turn conversation loop?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/text (repeated calls)
- "How do I get sentiment analysis for user input?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/text
- "How do I see which intents the bot considered besides the top match?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/text
- "How do I force the bot into a specific intent or slot-elicitation state?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/session
- "How do I filter session history by checkpoint label?" -> GET /bot/{botName}/alias/{botAlias}/user/{userId}/session/ (with checkpointLabelFilter)
- "How do I get response cards with buttons from the bot?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/text
- "How do I pass custom request attributes to the bot?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/text (with requestAttributes)
- "How do I get an audio response from the bot instead of text?" -> POST /bot/{botName}/alias/{botAlias}/user/{userId}/content (set Accept header)

## Response Tips

- **Text responses** (POST .../text): Check `dialogState` to determine next action -- `ElicitSlot` means ask for `slotToElicit`, `ReadyForFulfillment` means all slots collected, `Fulfilled` means done. `alternativeIntents` and `nluIntentConfidence.score` help gauge ambiguity.
- **Content/audio responses** (POST .../content): Most fields are returned as JSON-encoded strings in headers, not structured objects; parse `slots`, `sessionAttributes`, and `activeContexts` from their string representations. `audioStream` in the body is binary.
- **Session reads** (GET .../session): `recentIntentSummaryView` is an array of past intents -- empty array means fresh session. `dialogAction` reflects what the bot is currently waiting for.
- **Session writes** (POST .../session): Response mirrors the content endpoint format with string-encoded headers; `audioStream` is only present if `Accept` was set to an audio type.
- **Session deletes** (DELETE .../session): A 200 with `sessionId` confirms cleanup. Null fields in the response are normal -- only populated fields were actively tracked.

## Anomaly Flags

- **`dialogState: "Failed"`**: The bot could not understand the input after retries -- surface immediately and suggest rephrasing or resetting the session.
- **Low `nluIntentConfidence.score`** (below 0.5): The bot is guessing -- flag that the matched intent may be unreliable and `alternativeIntents` should be reviewed.
- **`alternativeIntents` present with similar scores**: Multiple intents are competing -- warn that disambiguation may be needed.
- **`sentimentResponse.sentimentLabel` is `NEGATIVE` or `MIXED`**: User frustration signal -- surface for human handoff consideration.
- **`encodedMessage` present but `message` absent**: Response contains characters outside the ASCII set -- agent should use `encodedMessage` (Base64-decoded) instead.
- **Session not found on DELETE (404/`sessionId` null)**: Session already expired or never existed -- flag that TTL may have elapsed.
- **`slotToElicit` set but `message` is empty**: Bot expects a slot value but provided no prompt -- likely a bot configuration issue worth flagging.
- **Repeated `ElicitSlot` for the same slot across turns**: The bot is stuck in a loop -- surface after 3 consecutive identical elicitations.

## Playbook

### 1. Basic Text Conversation Loop

1. Call `POST /bot/{botName}/alias/{botAlias}/user/{userId}/text` with `inputText` set to the user's message.
2. Read `dialogState` from the response.
3. If `ElicitSlot`: display `message` to the user, note `slotToElicit`, and loop back to step 1 with the user's answer.
4. If `ConfirmIntent`: display the confirmation prompt from `message`, loop back with "yes" or "no".
5. If `ReadyForFulfillment`: extract all values from `slots` and proceed with business logic.
6. If `Fulfilled` or `Failed`: display `message` and end the conversation or call DELETE to reset.

### 2. Voice/Audio Interaction

1. Set `Content-Type` to the audio format (e.g., `audio/l16; rate=16000; channels=1`).
2. Set `Accept` to desired response format (e.g., `audio/mpeg` for MP3 playback).
3. Call `POST /bot/{botName}/alias/{botAlias}/user/{userId}/content` with raw audio bytes as `inputStream`.
4. Read `dialogState` and `inputTranscript` from response headers to confirm what was understood.
5. Play back `audioStream` from the response body to the user.
6. Repeat until `dialogState` reaches `Fulfilled` or `ReadyForFulfillment`.

### 3. Mid-Conversation Session Override

1. Call `GET /bot/{botName}/alias/{botAlias}/user/{userId}/session/` to inspect current state, slots, and `dialogAction`.
2. Modify `sessionAttributes` or `dialogAction` as needed (e.g., pre-fill a slot, switch intent).
3. Call `POST /bot/{botName}/alias/{botAlias}/user/{userId}/session` with the updated `dialogAction` and `sessionAttributes`.
4. Resume the conversation with `POST .../text` -- the bot will continue from the overridden state.

### 4. Intent Confidence Validation Before Fulfillment

1. Send user input via `POST /bot/{botName}/alias/{botAlias}/user/{userId}/text`.
2. Check `nluIntentConfidence.score` -- if below your threshold (e.g., 0.7), do not proceed to fulfillment.
3. Review `alternativeIntents` for better matches; if a close competitor exists, ask the user to clarify.
4. If confidence is acceptable and `dialogState` is `ReadyForFulfillment`, proceed with the `slots` map.

### 5. Clean Session Reset

1. Call `DELETE /bot/{botName}/alias/{botAlias}/user/{userId}/session` to wipe all session state.
2. Confirm the response returns a `sessionId` (indicates successful cleanup).
3. Optionally call `POST .../session` to pre-seed `sessionAttributes` or `activeContexts` for the fresh session.
4. Begin the new conversation with `POST .../text` or `POST .../content`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
