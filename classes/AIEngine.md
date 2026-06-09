# AIEngine Documentation

[← Back to API Index](../reference.md)

---

## Class: AIEngine

### Description
Provides access to a particular generative AI model.

---
## Attr: AIEngine.supportsTemperature

### Description
Whether this model supports [temperature](#attr-aienginetemperature). If this is false, any `temperature` configured at engine or reuqest level will be ignored

**Flags**: IR

---
## Attr: AIEngine.temperature

### Description
Optional temperature of the model. This is a number between 0 and 1 denoting how much variation to receive in results.

### See Also

- [AIEngine.supportsTemperature](#attr-aienginesupportstemperature)

**Flags**: IR

---
## Attr: AIEngine.name

### Description
The local name of this engine.

**Flags**: IR

---
## Attr: AIEngine.engineId

### Description
The unique ID of this engine.

**Flags**: IR

---
## Attr: AIEngine.provider

### Description
The provider of this engine. Typically this is the name of the company or organization that provides access to the AI model.

**Flags**: IR

---
## Method: AIEngine.canSupportVisionRequests

### Description
Whether this AI engine can handle vision requests, or requests where one or more of the messages is an image.

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if this AI engine can handle vision requests; `false` otherwise.

---
## Method: AIEngine.isAPIKeyError

### Description
Returns `true` if the given raw AI response represents an API key authentication failure from the provider (e.g. invalid key, missing key, or permission denied). The base implementation recognises the OpenAI-compatible error shape used by OpenAI and most OpenAI-API-compatible providers.

Override this method in [AIEngine](#class-aiengine) subclasses to add provider-specific recognition logic.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rawResponse | [String](#type-string)|[Object](../reference.md#type-object) | false | — | The raw provider error response, as received by [getErrorResponseInfo](#geterrorresponseinfo). |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if this is an API key / authentication error.

### See Also

- [getErrorResponseInfo](#geterrorresponseinfo)

---
## Method: AIEngine.couldSupportRequest

### Description
Determines whether this engine could support the given request.

The reason for the uncertainty is that the implementation may use estimates (e.g. the number of tokens in a given message, as applied to input token limits), or an AI may decide to refuse to respond to the request.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| aiRequest | [AIRequest](#type-airequest) | false | — | The request to check. |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if this AIEngine could support the request; `false` otherwise.

---
## Method: AIEngine.sendRequest

### Description
Sends a request to this AI engine.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| aiRequest | [AIRequest](#type-airequest) | false | — | The request. |
| callback | [AIResponseCallback](#type-airesponsecallback) | false | — | The callback to fire with the response. |

---
