---
name: amazon-polly
description: "Amazon Polly API skill. Use when working with Amazon Polly for lexicons, voices, synthesisTasks. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Polly
API version: 2016-06-10

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /v1/voices -- verify access
3. POST /v1/synthesisTasks -- create first synthesisTasks

## Endpoints

9 endpoints across 4 groups. See references/api-spec.lap for full details.

### lexicons
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v1/lexicons/{LexiconName} | Deletes the specified pronunciation lexicon stored in an Amazon Web Services Region. A lexicon which has been deleted is not available for speech synthesis, nor is it possible to retrieve it using either the GetLexicon or ListLexicon APIs. For more information, see Managing Lexicons. |
| GET | /v1/lexicons/{LexiconName} | Returns the content of the specified pronunciation lexicon stored in an Amazon Web Services Region. For more information, see Managing Lexicons. |
| GET | /v1/lexicons | Returns a list of pronunciation lexicons stored in an Amazon Web Services Region. For more information, see Managing Lexicons. |
| PUT | /v1/lexicons/{LexiconName} | Stores a pronunciation lexicon in an Amazon Web Services Region. If a lexicon with the same name already exists in the region, it is overwritten by the new lexicon. Lexicon operations have eventual consistency, therefore, it might take some time before the lexicon is available to the SynthesizeSpeech operation. For more information, see Managing Lexicons. |

### voices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/voices | Returns the list of voices that are available for use when requesting speech synthesis. Each voice speaks a specified language, is either male or female, and is identified by an ID, which is the ASCII version of the voice name.  When synthesizing speech ( SynthesizeSpeech ), you provide the voice ID for the voice you want from the list of voices returned by DescribeVoices. For example, you want your news reader application to read news in a specific language, but giving a user the option to choose the voice. Using the DescribeVoices operation you can provide the user with a list of available voices to select from.  You can optionally specify a language code to filter the available voices. For example, if you specify en-US, the operation returns a list of all available US English voices.  This operation requires permissions to perform the polly:DescribeVoices action. |

### synthesisTasks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/synthesisTasks/{TaskId} | Retrieves a specific SpeechSynthesisTask object based on its TaskID. This object contains information about the given speech synthesis task, including the status of the task, and a link to the S3 bucket containing the output of the task. |
| GET | /v1/synthesisTasks | Returns a list of SpeechSynthesisTask objects ordered by their creation date. This operation can filter the tasks by their status, for example, allowing users to list only tasks that are completed. |
| POST | /v1/synthesisTasks | Allows the creation of an asynchronous synthesis task, by starting a new SpeechSynthesisTask. This operation requires all the standard information needed for speech synthesis, plus the name of an Amazon S3 bucket for the service to store the output of the synthesis task and two optional parameters (OutputS3KeyPrefix and SnsTopicArn). Once the synthesis task is created, this operation will return a SpeechSynthesisTask object, which will include an identifier of this task as well as the current status. The SpeechSynthesisTask object is available for 72 hours after starting the asynchronous synthesis task. |

### speech
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/speech | Synthesizes UTF-8 input, plain text or SSML, to a stream of bytes. SSML input must be valid, well-formed SSML. Some alphabets might not be available with all the voices (for example, Cyrillic might not be read at all by English voices) unless phoneme mapping is used. For more information, see How it Works. |

## Enhanced Skill Content
## Question Mapping

- "What voices are available for text-to-speech?" -> GET /v1/voices
- "Which voices support neural engine?" -> GET /v1/voices (filter Engine=neural)
- "List voices for a specific language like French?" -> GET /v1/voices (filter LanguageCode=fr-FR)
- "Convert this text to speech audio?" -> POST /v1/speech
- "Generate speech using SSML markup?" -> POST /v1/speech (TextType=ssml)
- "Start a long-form speech synthesis job?" -> POST /v1/synthesisTasks
- "What is the status of my synthesis task?" -> GET /v1/synthesisTasks/{TaskId}
- "List all my running synthesis tasks?" -> GET /v1/synthesisTasks (Status=inProgress)
- "What pronunciation lexicons do I have?" -> GET /v1/lexicons
- "Get the contents of a specific lexicon?" -> GET /v1/lexicons/{LexiconName}
- "Upload a custom pronunciation lexicon?" -> PUT /v1/lexicons/{LexiconName}
- "Delete a lexicon I no longer need?" -> DELETE /v1/lexicons/{LexiconName}
- "How many characters did my last synthesis use?" -> GET /v1/synthesisTasks/{TaskId} (check RequestCharacters)
- "Where is the output file for my synthesis task?" -> GET /v1/synthesisTasks/{TaskId} (check OutputUri)
- "Synthesize speech with a custom lexicon applied?" -> POST /v1/speech (include LexiconNames)

## Response Tips

- **Voices**: Paginated via `NextToken`; always check for it and loop until absent. Each `Voice` object varies by engine support.
- **Speech**: Returns raw `AudioStream` bytes with `ContentType` header indicating format (e.g., `audio/mpeg`); `RequestCharacters` tracks billing usage.
- **Synthesis Tasks**: `TaskStatus` cycles through `scheduled` -> `inProgress` -> `completed` or `failed`; check `TaskStatusReason` on failure. List endpoint supports `MaxResults` for page size.
- **Lexicons**: `LexiconAttributes` nests metadata separately from `Content`; `LexemesCount` and `Size` help gauge lexicon complexity. List is paginated via `NextToken`.

## Anomaly Flags

- **Task failure**: Surface immediately when `TaskStatus` is `failed` -- include `TaskStatusReason` for diagnosis.
- **Character consumption spikes**: Flag when `RequestCharacters` on a synthesis task is unusually high relative to prior tasks, as Polly bills per character.
- **Empty voice list**: If GET /v1/voices returns no results for a given engine/language combo, warn that the combination may be unsupported rather than silently proceeding.
- **Stale tasks**: Flag synthesis tasks stuck in `scheduled` or `inProgress` for an extended period (compare `CreationTime` to now).
- **Lexicon size limits**: Surface when `LexemesCount` or `Size` in lexicon attributes approaches AWS service limits (max 4,000 lexemes, 100 KB).
- **Pagination truncation**: Warn if a `NextToken` is present but the caller did not request subsequent pages -- results are incomplete.
- **Deprecated engine usage**: If the caller uses `standard` engine where `neural` or `generative` is available for that voice, suggest upgrading for better quality.

## Playbook

### 1. Convert Text to Speech (Quick Synthesis)

1. Call GET /v1/voices with desired `LanguageCode` and `Engine` to find a suitable `VoiceId`.
2. Call POST /v1/speech with `OutputFormat` (e.g., `mp3`), `Text`, and the chosen `VoiceId`.
3. Read the `AudioStream` bytes from the response and save to a file.
4. Check `RequestCharacters` to track usage against billing.

### 2. Run a Long-Form Synthesis Job

1. Call POST /v1/synthesisTasks with `Text`, `VoiceId`, `OutputFormat`, and `OutputS3BucketName` (plus optional `OutputS3KeyPrefix`).
2. Note the `TaskId` from the response.
3. Poll GET /v1/synthesisTasks/{TaskId} until `TaskStatus` is `completed` or `failed`.
4. On completion, retrieve the audio file from the S3 location in `OutputUri`.
5. On failure, read `TaskStatusReason` and adjust parameters before retrying.

### 3. Manage Custom Pronunciation Lexicons

1. Author a PLS (Pronunciation Lexicon Specification) XML document with custom pronunciations.
2. Call PUT /v1/lexicons/{LexiconName} with `Content` set to the PLS XML.
3. Verify upload by calling GET /v1/lexicons/{LexiconName} and inspecting `LexiconAttributes`.
4. Use the lexicon in synthesis by passing its name in `LexiconNames` on POST /v1/speech or POST /v1/synthesisTasks.
5. Clean up unused lexicons with DELETE /v1/lexicons/{LexiconName}.

### 4. Audit and Monitor All Synthesis Tasks

1. Call GET /v1/synthesisTasks with `MaxResults` set to your desired page size.
2. Loop using `NextToken` until all tasks are retrieved.
3. Filter by `Status` (e.g., `failed`) to find tasks needing attention.
4. For each failed task, call GET /v1/synthesisTasks/{TaskId} to get full details and `TaskStatusReason`.
5. Sum `RequestCharacters` across tasks to estimate billing for the period.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
