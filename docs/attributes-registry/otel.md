<!-- NOTE: THIS FILE IS AUTOGENERATED. DO NOT EDIT BY HAND. -->
<!-- see templates/registry/markdown/attribute_namespace.md.j2 -->

# OTel

- [OTel Attributes](#otel-attributes)
- [OTel Scope Attributes](#otel-scope-attributes)
- [Deprecated OTel Library Attributes](#deprecated-otel-library-attributes)

## OTel Attributes

Attributes reserved for OpenTelemetry

| Attribute | Type | Description | Examples | Stability |
|---|---|---|---|---|
| <a id="otel-status-code" href="#otel-status-code">`otel.status_code`</a> | string | Name of the code, either "OK" or "ERROR". MUST NOT be set if the status code is UNSET. | `OK`; `ERROR` | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |
| <a id="otel-status-description" href="#otel-status-description">`otel.status_description`</a> | string | Description of the Status if it has a value, otherwise not set. | `resource not found` | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |

---

`otel.status_code` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `ERROR` | The operation contains an error. | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |
| `OK` | The operation has been validated by an Application developer or Operator to have completed successfully. | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |

## OTel Scope Attributes

Attributes used by non-OTLP exporters to represent OpenTelemetry Scope's concepts.

| Attribute | Type | Description | Examples | Stability |
|---|---|---|---|---|
| <a id="otel-scope-name" href="#otel-scope-name">`otel.scope.name`</a> | string | The name of the instrumentation scope - (`InstrumentationScope.Name` in OTLP). | `io.opentelemetry.contrib.mongodb` | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |
| <a id="otel-scope-version" href="#otel-scope-version">`otel.scope.version`</a> | string | The version of the instrumentation scope - (`InstrumentationScope.Version` in OTLP). | `1.0.0` | ![Stable](https://img.shields.io/badge/-stable-lightgreen) |

## Deprecated OTel Library Attributes

Describes deprecated otel.library attributes.

| Attribute | Type | Description | Examples | Stability |
|---|---|---|---|---|
| <a id="otel-library-name" href="#otel-library-name">`otel.library.name`</a> | string | Deprecated. Use the `otel.scope.name` attribute | `io.opentelemetry.contrib.mongodb` | ![Deprecated](https://img.shields.io/badge/-deprecated-red)<br>Use the `otel.scope.name` attribute. |
| <a id="otel-library-version" href="#otel-library-version">`otel.library.version`</a> | string | Deprecated. Use the `otel.scope.version` attribute. | `1.0.0` | ![Deprecated](https://img.shields.io/badge/-deprecated-red)<br>Use the `otel.scope.version` attribute. |
