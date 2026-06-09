# AIDelegator Documentation

[← Back to API Index](../reference.md)

---

## Class: AIDelegator

*Inherits from:* [CoTProcess](CoTProcess.md#class-cotprocess)

### Description
A lightweight [CoTProcess](CoTProcess.md#class-cotprocess) that routes user requests to the most appropriate registered [AI service](#type-aiservicedescriptor). It uses a single CoT step to ask the AI which service best matches the user's intent, then invokes that service with the original prompt and the AI's rationale.

Typical usage is via the convenience method [AI.delegate](AI.md#classmethod-aidelegate) rather than creating an AIDelegator directly. See the [AI Assist overview](../kb_topics/aiAssist.md#kb-topic-ai-assist) for the registration and routing model.

The prompts the Delegator uses are customizable via [AI.delegatorPrompts](AI.md#classattr-aidelegatorprompts). Registered services are discovered via [AI.getAIServicesForContext](AI.md#classmethod-aigetaiservicesforcontext), which walks the component hierarchy and merges with global services.

### Groups

- CoT

### See Also

- [AI.delegate](AI.md#classmethod-aidelegate)
- [AI.delegatorPrompts](AI.md#classattr-aidelegatorprompts)
- [aiAssist](../kb_topics/aiAssist.md#kb-topic-ai-assist)

---
## Attr: AIDelegator.optionalPrompts

### Description
Contains a "serviceList" prompt part built dynamically from the registered services at creation time.

**Flags**: IR

---
## Attr: AIDelegator.introPrompt

### Description
Intro prompt for the Delegator, sourced from the customizable [AI.delegatorPrompts](AI.md#classattr-aidelegatorprompts) at creation time.

**Flags**: IR

---
