# AIEngine Documentation

[← Back to API Index](../main.md)

---

## Class: AIEngine

### Description
Provides access to a particular generative AI model.

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

`[boolean](../main.md#type-boolean)` — `true` if this AI engine can handle vision requests; `false` otherwise.

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

`[boolean](../main.md#type-boolean)` — `true` if this AIEngine could support the request; `false` otherwise.

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
