# CoTExecutionModels

[← Back to API Index](../reference.md)

---

## KB Topic: CoTExecutionModels

### Description
SmartClient supports two broad patterns for AI-assisted apps:

*   **AIWorkflow** — a deterministic, testable workflow where each step is a [CoTTask](../classes/CoTTask.md#class-cottask) and transitions are explicit. This model emphasizes reliability, observability, and repeatability.
*   **AIToolbox** — an ad hoc, flexible toolset where the AI can decide among many capabilities dynamically. This model is great for rapid prototyping or lightweight integrations where flexibility matters more than determinism.

SmartClient supports both models, but we generally recommend AIWorkflow for enterprise tools where reliability and observability are critical, and AIToolbox for rapid prototyping or lightweight integrations where flexibility is more important than determinism. Often, an AIToolbox approach is used for prototyping and then evolves into an AIWorkflow approach as determinism, testability, and predictability become key for deployed tools.

See also: - [CoTProcess](../classes/CoTProcess.md#class-cotprocess) and [CoTTask](../classes/CoTTask.md#class-cottask) for the workflow APIs  
\- [CoT History](CoTHistory.md#kb-topic-cothistory) for how history is recorded and surfaced in prompts

---
