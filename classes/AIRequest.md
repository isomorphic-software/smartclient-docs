# AIRequest Documentation

[← Back to API Index](../main.md)

---

## Attr: AIRequest.cancellationController

### Description
If provided, the [CancellationController](CancellationController.md#class-cancellationcontroller) that will be looked to for whether the AI request is canceled.

**Flags**: IR

---
## Attr: AIRequest.historyConclusion

### Description
When this engine does not support multiple messages, all of the messages of the request must be concatenated together. This text is included verbatim before the concatenation of all-but-the-last non-system message.

**Flags**: IR

---
## Attr: AIRequest.responseType

### Description
The type of content expected from AI.

If this type is "number", then the response from AI is constrained by [AIRequest.responseMinimum](#attr-airequestresponseminimum) and [AIRequest.responseMaximum](#attr-airequestresponsemaximum).

**Flags**: IR

---
## Attr: AIRequest.responseMinimum

### Description
When the [AIRequest.responseType](#attr-airequestresponsetype) is "number", the minimum value that the response may take. If not specified, then there is no minimum.

**Flags**: IR

---
## Attr: AIRequest.historyIntroduction

### Description
When this engine does not support multiple messages, all of the messages of the request must be concatenated together. This text is included verbatim before the concatenation of all-but-the-last non-system message.

**Flags**: IR

---
## Attr: AIRequest.temperature

### Description
A number from 0 to 1 representing how much variability or creativity in responses AI should generate. 0 is little-to-no variation. 1 is high variation.

**Flags**: IR

---
## Attr: AIRequest.messages

### Description
List of messages forming the request.

**Flags**: IR

---
## Attr: AIRequest.prompt

### Description
Prompt text to AI. If [AIRequest.messages](#attr-airequestmessages) are also provided, then this prompt is appended as another message with type "text" and source "user" when submitted to AI.

**Flags**: IR

---
## Attr: AIRequest.responseMaximum

### Description
When the [AIRequest.responseType](#attr-airequestresponsetype) is "number", the maximum value that the response may take. If not specified, then there is no maximum.

**Flags**: IR

---
## Attr: AIRequest.historyDelimiters

### Description
When this engine does not support multiple messages, all of the messages of the request must be concatenated together. This maps the [AIMessageSource](../main.md#type-aimessagesource) to the delimiter to be used to enclose the content of the message.

**Flags**: IR

---
