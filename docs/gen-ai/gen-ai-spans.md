<!--- Hugo front matter used to generate the website version of this page:
linkTitle: Spans
--->

# Semantic conventions for generative client AI spans

**Status**: [Development][DocumentStatus]

<!-- toc -->

- [Spans](#spans)
  - [GenAI span](#genai-span)
  - [Execute Tool Span](#execute-tool-span)
- [Capturing inputs and outputs](#capturing-inputs-and-outputs)

<!-- tocstop -->

A request to an Generative AI is modeled as a span in a trace.

## Spans

### GenAI span

The span contains input data and metadata for a request to a GenAI model.
Each attribute represents a concept that is common to most Generative AI clients.
Many of these attributes only apply to specific GenAI operations.

For example, GenAI embeddings requests don't use output tokens,
so `gen_ai.usage.output_tokens` does not apply to embeddings operations.

<!-- semconv span.gen_ai.client -->
<!-- NOTE: THIS TEXT IS AUTOGENERATED. DO NOT EDIT BY HAND. -->
<!-- see templates/registry/markdown/snippet.md.j2 -->
<!-- prettier-ignore-start -->
<!-- markdownlint-capture -->
<!-- markdownlint-disable -->

**Status:** ![Development](https://img.shields.io/badge/-development-blue)

This span represents a client call to Generative AI model or service.

**Span name** SHOULD be `{gen_ai.operation.name} {gen_ai.request.model}`.
Semantic conventions for individual GenAI systems and frameworks MAY specify different span name format
and MUST follow the overall [guidelines for span names](https://github.com/open-telemetry/opentelemetry-specification/tree/v1.37.0/specification/trace/api.md#span).

**Span kind** SHOULD be `CLIENT`and MAY be set to `INTERNAL` on spans representing
call to models running in the same process. It's RECOMMENDED to use `CLIENT` kind
when the GenAI system being instrumented usually runs in a different process than its
client or when the GenAI call happens over instrumented protocol such as HTTP.

**Span status** SHOULD follow the [Recording Errors](/docs/general/recording-errors.md) document.

| Attribute  | Type | Description  | Examples  | [Requirement Level](https://opentelemetry.io/docs/specs/semconv/general/attribute-requirement-level/) | Stability |
|---|---|---|---|---|---|
| [`gen_ai.operation.name`](/docs/attributes-registry/gen-ai.md) | string | The name of the operation being performed. [1] | `chat`; `generate_content`; `text_completion` | `Required` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.system`](/docs/attributes-registry/gen-ai.md) | string | The Generative AI product as identified by the client or server instrumentation. [2] | `openai` | `Required` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`error.type`](/docs/attributes-registry/error.md) | string | Describes a class of error the operation ended with. [3] | `timeout`; `java.net.UnknownHostException`; `server_certificate_invalid`; `500` | `Conditionally Required` if the operation ended in an error | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |
| [`gen_ai.output.type`](/docs/attributes-registry/gen-ai.md) | string | Represents the content type requested by the client. [4] | `text`; `json`; `image` | `Conditionally Required` [5] | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.choice.count`](/docs/attributes-registry/gen-ai.md) | int | The target number of candidate completions to return. | `3` | `Conditionally Required` if available, in the request, and !=1 | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.model`](/docs/attributes-registry/gen-ai.md) | string | The name of the GenAI model a request is being made to. [6] | `gpt-4` | `Conditionally Required` If available. | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.seed`](/docs/attributes-registry/gen-ai.md) | int | Requests with same seed value more likely to return same result. | `100` | `Conditionally Required` if applicable and if the request includes a seed | ![Development](https://img.shields.io/badge/-development-blue) |
| [`server.port`](/docs/attributes-registry/server.md) | int | GenAI server port. [7] | `80`; `8080`; `443` | `Conditionally Required` If `server.address` is set. | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |
| [`gen_ai.request.encoding_formats`](/docs/attributes-registry/gen-ai.md) | string[] | The encoding formats requested in an embeddings operation, if specified. [8] | `["base64"]`; `["float", "binary"]` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.frequency_penalty`](/docs/attributes-registry/gen-ai.md) | double | The frequency penalty setting for the GenAI request. | `0.1` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.max_tokens`](/docs/attributes-registry/gen-ai.md) | int | The maximum number of tokens the model generates for a request. | `100` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.presence_penalty`](/docs/attributes-registry/gen-ai.md) | double | The presence penalty setting for the GenAI request. | `0.1` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.stop_sequences`](/docs/attributes-registry/gen-ai.md) | string[] | List of sequences that the model will use to stop generating further tokens. | `["forest", "lived"]` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.temperature`](/docs/attributes-registry/gen-ai.md) | double | The temperature setting for the GenAI request. | `0.0` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.top_k`](/docs/attributes-registry/gen-ai.md) | double | The top_k sampling setting for the GenAI request. | `1.0` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.request.top_p`](/docs/attributes-registry/gen-ai.md) | double | The top_p sampling setting for the GenAI request. | `1.0` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.response.finish_reasons`](/docs/attributes-registry/gen-ai.md) | string[] | Array of reasons the model stopped generating tokens, corresponding to each generation received. | `["stop"]`; `["stop", "length"]` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.response.id`](/docs/attributes-registry/gen-ai.md) | string | The unique identifier for the completion. | `chatcmpl-123` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.response.model`](/docs/attributes-registry/gen-ai.md) | string | The name of the model that generated the response. [9] | `gpt-4-0613` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.usage.input_tokens`](/docs/attributes-registry/gen-ai.md) | int | The number of tokens used in the GenAI input (prompt). | `100` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.usage.output_tokens`](/docs/attributes-registry/gen-ai.md) | int | The number of tokens used in the GenAI response (completion). | `180` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |
| [`server.address`](/docs/attributes-registry/server.md) | string | GenAI server address. [10] | `example.com`; `10.1.2.80`; `/tmp/my.sock` | `Recommended` | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |

**[1] `gen_ai.operation.name`:** If one of the predefined values applies, but specific system uses a different name it's RECOMMENDED to document it in the semantic conventions for specific GenAI system and use system-specific name in the instrumentation. If a different name is not documented, instrumentation libraries SHOULD use applicable predefined value.

**[2] `gen_ai.system`:** The `gen_ai.system` describes a family of GenAI models with specific model identified
by `gen_ai.request.model` and `gen_ai.response.model` attributes.

The actual GenAI product may differ from the one identified by the client.
Multiple systems, including Azure OpenAI and Gemini, are accessible by OpenAI client
libraries. In such cases, the `gen_ai.system` is set to `openai` based on the
instrumentation's best knowledge, instead of the actual system. The `server.address`
attribute may help identify the actual system in use for `openai`.

For custom model, a custom friendly name SHOULD be used.
If none of these options apply, the `gen_ai.system` SHOULD be set to `_OTHER`.

**[3] `error.type`:** The `error.type` SHOULD match the error code returned by the Generative AI provider or the client library,
the canonical name of exception that occurred, or another low-cardinality error identifier.
Instrumentations SHOULD document the list of errors they report.

**[4] `gen_ai.output.type`:** This attribute SHOULD be used when the client requests output of a specific type. The model may return zero or more outputs of this type.
This attribute specifies the output modality and not the actual output format. For example, if an image is requested, the actual output could be a URL pointing to an image file.
Additional output format details may be recorded in the future in the `gen_ai.output.{type}.*` attributes.

**[5] `gen_ai.output.type`:** when applicable and if the request includes an output format.

**[6] `gen_ai.request.model`:** The name of the GenAI model a request is being made to. If the model is supplied by a vendor, then the value must be the exact name of the model requested. If the model is a fine-tuned custom model, the value should have a more specific name than the base model that's been fine-tuned.

**[7] `server.port`:** When observed from the client side, and when communicating through an intermediary, `server.port` SHOULD represent the server port behind any intermediaries, for example proxies, if it's available.

**[8] `gen_ai.request.encoding_formats`:** In some GenAI systems the encoding formats are called embedding types. Also, some GenAI systems only accept a single format per request.

**[9] `gen_ai.response.model`:** If available. The name of the GenAI model that provided the response. If the model is supplied by a vendor, then the value must be the exact name of the model actually used. If the model is a fine-tuned custom model, the value should have a more specific name than the base model that's been fine-tuned.

**[10] `server.address`:** When observed from the client side, and when communicating through an intermediary, `server.address` SHOULD represent the server address behind any intermediaries, for example proxies, if it's available.

---

`error.type` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `_OTHER` | A fallback error value to be used when the instrumentation doesn't define a custom value. | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |

---

`gen_ai.operation.name` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `chat` | Chat completion operation such as [OpenAI Chat API](https://platform.openai.com/docs/api-reference/chat) | ![Development](https://img.shields.io/badge/-development-blue) |
| `create_agent` | Create GenAI agent | ![Development](https://img.shields.io/badge/-development-blue) |
| `embeddings` | Embeddings operation such as [OpenAI Create embeddings API](https://platform.openai.com/docs/api-reference/embeddings/create) | ![Development](https://img.shields.io/badge/-development-blue) |
| `execute_tool` | Execute a tool | ![Development](https://img.shields.io/badge/-development-blue) |
| `generate_content` | Multimodal content generation operation such as [Gemini Generate Content](https://ai.google.dev/api/generate-content) | ![Development](https://img.shields.io/badge/-development-blue) |
| `text_completion` | Text completions operation such as [OpenAI Completions API (Legacy)](https://platform.openai.com/docs/api-reference/completions) | ![Development](https://img.shields.io/badge/-development-blue) |

---

`gen_ai.output.type` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `image` | Image | ![Development](https://img.shields.io/badge/-development-blue) |
| `json` | JSON object with known or unknown schema | ![Development](https://img.shields.io/badge/-development-blue) |
| `speech` | Speech | ![Development](https://img.shields.io/badge/-development-blue) |
| `text` | Plain text | ![Development](https://img.shields.io/badge/-development-blue) |

---

`gen_ai.system` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `anthropic` | Anthropic | ![Development](https://img.shields.io/badge/-development-blue) |
| `aws.bedrock` | AWS Bedrock | ![Development](https://img.shields.io/badge/-development-blue) |
| `az.ai.inference` | Azure AI Inference | ![Development](https://img.shields.io/badge/-development-blue) |
| `az.ai.openai` | Azure OpenAI | ![Development](https://img.shields.io/badge/-development-blue) |
| `cohere` | Cohere | ![Development](https://img.shields.io/badge/-development-blue) |
| `deepseek` | DeepSeek | ![Development](https://img.shields.io/badge/-development-blue) |
| `gcp.gemini` | Gemini [11] | ![Development](https://img.shields.io/badge/-development-blue) |
| `gcp.gen_ai` | Any Google generative AI endpoint [12] | ![Development](https://img.shields.io/badge/-development-blue) |
| `gcp.vertex_ai` | Vertex AI [13] | ![Development](https://img.shields.io/badge/-development-blue) |
| `groq` | Groq | ![Development](https://img.shields.io/badge/-development-blue) |
| `ibm.watsonx.ai` | IBM Watsonx AI | ![Development](https://img.shields.io/badge/-development-blue) |
| `mistral_ai` | Mistral AI | ![Development](https://img.shields.io/badge/-development-blue) |
| `openai` | OpenAI | ![Development](https://img.shields.io/badge/-development-blue) |
| `perplexity` | Perplexity | ![Development](https://img.shields.io/badge/-development-blue) |
| `xai` | xAI | ![Development](https://img.shields.io/badge/-development-blue) |

**[11]:** This refers to the 'generativelanguage.googleapis.com' endpoint. Also known as the AI Studio API. May use common attributes prefixed with 'gcp.gen_ai.'.

**[12]:** May be used when specific backend is unknown. May use common attributes prefixed with 'gcp.gen_ai.'.

**[13]:** This refers to the 'aiplatform.googleapis.com' endpoint. May use common attributes prefixed with 'gcp.gen_ai.'.

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- END AUTOGENERATED TEXT -->
<!-- endsemconv -->

### Execute Tool Span

<!-- semconv span.gen_ai.execute_tool.internal -->
<!-- NOTE: THIS TEXT IS AUTOGENERATED. DO NOT EDIT BY HAND. -->
<!-- see templates/registry/markdown/snippet.md.j2 -->
<!-- prettier-ignore-start -->
<!-- markdownlint-capture -->
<!-- markdownlint-disable -->

**Status:** ![Development](https://img.shields.io/badge/-development-blue)

Describes tool execution span.

`gen_ai.operation.name` SHOULD be `execute_tool`.

**Span name** SHOULD be `execute_tool {gen_ai.tool.name}`.

GenAI instrumentations that are able to instrument tool execution call SHOULD do so.
However, it's common for tools to be executed by the application code. It's recommended
for the application developers to follow this semantic convention for tools invoked
by the application code.

**Span kind** SHOULD be `INTERNAL`.

**Span status** SHOULD follow the [Recording Errors](/docs/general/recording-errors.md) document.

| Attribute  | Type | Description  | Examples  | [Requirement Level](https://opentelemetry.io/docs/specs/semconv/general/attribute-requirement-level/) | Stability |
|---|---|---|---|---|---|
| [`error.type`](/docs/attributes-registry/error.md) | string | Describes a class of error the operation ended with. [1] | `timeout`; `java.net.UnknownHostException`; `server_certificate_invalid`; `500` | `Conditionally Required` if the operation ended in an error | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |
| [`gen_ai.tool.call.id`](/docs/attributes-registry/gen-ai.md) | string | The tool call identifier. | `call_mszuSIzqtI65i1wAUOE8w5H4` | `Recommended` if available | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.tool.description`](/docs/attributes-registry/gen-ai.md) | string | The tool description. | `Multiply two numbers` | `Recommended` if available | ![Development](https://img.shields.io/badge/-development-blue) |
| [`gen_ai.tool.name`](/docs/attributes-registry/gen-ai.md) | string | Name of the tool utilized by the agent. | `Flights` | `Recommended` | ![Development](https://img.shields.io/badge/-development-blue) |

**[1] `error.type`:** The `error.type` SHOULD match the error code returned by the Generative AI provider or the client library,
the canonical name of exception that occurred, or another low-cardinality error identifier.
Instrumentations SHOULD document the list of errors they report.

---

`error.type` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `_OTHER` | A fallback error value to be used when the instrumentation doesn't define a custom value. | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- END AUTOGENERATED TEXT -->
<!-- endsemconv -->

## Capturing inputs and outputs

User inputs and model responses may be recorded as events parented to GenAI operation span. See [Semantic Conventions for GenAI events](./gen-ai-events.md) for the details.

[DocumentStatus]: https://opentelemetry.io/docs/specs/otel/document-status
