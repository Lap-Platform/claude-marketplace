---
name: amazon-sagemaker-runtime
description: "Amazon SageMaker Runtime API skill. Use when working with Amazon SageMaker Runtime for endpoints. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon SageMaker Runtime
API version: 2017-05-13

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /endpoints/{EndpointName}/invocations -- create first invocations

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### endpoints
| Method | Path | Description |
|--------|------|-------------|
| POST | /endpoints/{EndpointName}/invocations | After you deploy a model into production using Amazon SageMaker hosting services, your client applications use this API to get inferences from the model hosted at the specified endpoint.  For an overview of Amazon SageMaker, see How It Works.  Amazon SageMaker strips all POST headers except those supported by the API. Amazon SageMaker might add additional headers. You should not rely on the behavior of headers outside those enumerated in the request syntax.  Calls to InvokeEndpoint are authenticated by using Amazon Web Services Signature Version 4. For information, see Authenticating Requests (Amazon Web Services Signature Version 4) in the Amazon S3 API Reference. A customer's model containers must respond to requests within 60 seconds. The model itself can have a maximum processing time of 60 seconds before responding to invocations. If your model is going to take 50-60 seconds of processing time, the SDK socket timeout should be set to be 70 seconds.  Endpoints are scoped to an individual account, and are not public. The URL does not contain the account ID, but Amazon SageMaker determines the account ID from the authentication token that is supplied by the caller. |
| POST | /endpoints/{EndpointName}/async-invocations | After you deploy a model into production using Amazon SageMaker hosting services, your client applications use this API to get inferences from the model hosted at the specified endpoint in an asynchronous manner. Inference requests sent to this API are enqueued for asynchronous processing. The processing of the inference request may or may not complete before you receive a response from this API. The response from this API will not contain the result of the inference request but contain information about where you can locate it. Amazon SageMaker strips all POST headers except those supported by the API. Amazon SageMaker might add additional headers. You should not rely on the behavior of headers outside those enumerated in the request syntax.  Calls to InvokeEndpointAsync are authenticated by using Amazon Web Services Signature Version 4. For information, see Authenticating Requests (Amazon Web Services Signature Version 4) in the Amazon S3 API Reference. |
| POST | /endpoints/{EndpointName}/invocations-response-stream | Invokes a model at the specified endpoint to return the inference response as a stream. The inference stream provides the response payload incrementally as a series of parts. Before you can get an inference stream, you must have access to a model that's deployed using Amazon SageMaker hosting services, and the container for that model must support inference streaming. For more information that can help you use this API, see the following sections in the Amazon SageMaker Developer Guide:   For information about how to add streaming support to a model, see How Containers Serve Requests.   For information about how to process the streaming response, see Invoke real-time endpoints.   Before you can use this operation, your IAM permissions must allow the sagemaker:InvokeEndpoint action. For more information about Amazon SageMaker actions for IAM policies, see Actions, resources, and condition keys for Amazon SageMaker in the IAM Service Authorization Reference. Amazon SageMaker strips all POST headers except those supported by the API. Amazon SageMaker might add additional headers. You should not rely on the behavior of headers outside those enumerated in the request syntax.  Calls to InvokeEndpointWithResponseStream are authenticated by using Amazon Web Services Signature Version 4. For information, see Authenticating Requests (Amazon Web Services Signature Version 4) in the Amazon S3 API Reference. |

## Enhanced Skill Content
## Question Mapping

- "How do I invoke a SageMaker endpoint?" -> POST /endpoints/{EndpointName}/invocations
- "How do I get a prediction from my model?" -> POST /endpoints/{EndpointName}/invocations
- "How do I call a specific model on a multi-model endpoint?" -> POST /endpoints/{EndpointName}/invocations (set X-Amzn-SageMaker-Target-Model header)
- "How do I invoke a specific variant of my endpoint?" -> POST /endpoints/{EndpointName}/invocations (set X-Amzn-SageMaker-Target-Variant header)
- "How do I run async inference on large payloads?" -> POST /endpoints/{EndpointName}/async-invocations
- "How do I invoke an endpoint without waiting for the response?" -> POST /endpoints/{EndpointName}/async-invocations
- "How do I set a timeout for async inference?" -> POST /endpoints/{EndpointName}/async-invocations (set X-Amzn-SageMaker-InvocationTimeoutSeconds header)
- "How do I set a TTL so my async request expires?" -> POST /endpoints/{EndpointName}/async-invocations (set X-Amzn-SageMaker-RequestTTLSeconds header)
- "How do I stream responses from a SageMaker endpoint?" -> POST /endpoints/{EndpointName}/invocations-response-stream
- "How do I get real-time token-by-token output from my LLM endpoint?" -> POST /endpoints/{EndpointName}/invocations-response-stream
- "How do I get explainability data with my prediction?" -> POST /endpoints/{EndpointName}/invocations (set X-Amzn-SageMaker-Enable-Explanations header)
- "How do I route to a specific inference component?" -> POST /endpoints/{EndpointName}/invocations (set X-Amzn-SageMaker-Inference-Component header)
- "How do I pass custom metadata through an invocation?" -> POST /endpoints/{EndpointName}/invocations (set X-Amzn-SageMaker-Custom-Attributes header)
- "Where do I find the output of my async invocation?" -> POST /endpoints/{EndpointName}/async-invocations (check OutputLocation in response)

## Response Tips

- **Sync invocations:** Body is raw bytes in the model's output format; always check ContentType to know how to decode. InvokedProductionVariant tells you which variant actually served the request.
- **Async invocations:** Response is immediate with an OutputLocation (S3 URI) where results will appear; poll that location or use SNS notifications. If FailureLocation is populated, the inference failed and the error details are at that S3 path.
- **Streaming invocations:** Body is a ResponseStream with chunked PayloadPart events; read Bytes from each part incrementally. Mid-stream errors arrive as ModelStreamError or InternalStreamFailure events embedded in the stream itself, not as HTTP error codes.

## Anomaly Flags

- **ModelStreamError in stream:** Surface immediately -- the model returned an error mid-stream (ErrorCode + Message). Partial output received before this event may be incomplete or corrupted.
- **InternalStreamFailure:** Indicates an infrastructure-level failure during streaming; retry is likely appropriate. Flag to the user that the response was interrupted.
- **FailureLocation populated (async):** The async job failed. Proactively fetch and display the error from the S3 failure path rather than waiting for the user to discover it.
- **Missing InvokedProductionVariant:** If absent on a multi-variant endpoint, the routing may not be working as expected -- flag for investigation.
- **RequestTTLSeconds approaching or exceeded:** Warn when setting very short TTLs on async invocations, as requests may expire before processing begins during traffic spikes.
- **Content-Type mismatch:** If the request Content-Type does not match what the model container expects, invocations will fail with opaque errors. Flag when the response ContentType differs from the request Accept header.

## Playbook

### 1. Run a Synchronous Prediction

1. Prepare the input payload as bytes (JSON, CSV, or model-specific format)
2. Call `POST /endpoints/{EndpointName}/invocations` with the Body and appropriate Content-Type header
3. Read the response Body bytes and decode using the returned ContentType
4. Optionally check InvokedProductionVariant to confirm which variant handled the request

### 2. Run Async Inference for Large Payloads

1. Upload the input payload to S3 and note the S3 URI
2. Call `POST /endpoints/{EndpointName}/async-invocations` with X-Amzn-SageMaker-InputLocation set to the S3 URI
3. Capture OutputLocation from the 200 response
4. Poll the OutputLocation S3 path (or listen on SNS) until the result file appears
5. If FailureLocation is returned instead, fetch the error details from that S3 path and handle accordingly

### 3. Stream Real-Time LLM Output

1. Prepare the input payload (e.g., a prompt in the model's expected format)
2. Call `POST /endpoints/{EndpointName}/invocations-response-stream` with the Body and Content-Type
3. Read PayloadPart events from the ResponseStream, extracting Bytes from each chunk
4. Decode and display each chunk incrementally to the user
5. Watch for ModelStreamError or InternalStreamFailure events -- if received, stop processing and surface the error message

### 4. Invoke a Specific Model on a Multi-Model Endpoint

1. Identify the target model artifact path (the TargetModel value configured during deployment)
2. Call `POST /endpoints/{EndpointName}/invocations` with X-Amzn-SageMaker-Target-Model set to the model path
3. Include X-Amzn-SageMaker-Target-Container-Hostname if the endpoint runs multiple containers
4. Process the response as in a standard synchronous invocation

### 5. Invoke with Request Tracing and Custom Attributes

1. Generate a unique inference ID for tracing purposes
2. Call any invocation endpoint with X-Amzn-SageMaker-Inference-Id set to your trace ID
3. Set X-Amzn-SageMaker-Custom-Attributes with semicolon-delimited key=value pairs for pass-through metadata
4. Use the same Inference-Id to correlate requests across logs, async outputs, and monitoring dashboards


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object
- Error responses use types: InternalStreamFailure, ModelStreamError

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
