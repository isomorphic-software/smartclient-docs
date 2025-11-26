# CoT

[← Back to API Index](../reference.md)

---

## KB Topic: CoT

### Description
A CoT (Chain of Thought) is an AI workflow in which an LLM is repeatedly called and asked to perform a series of small tasks as part of a larger goal.

In SmartClient, [CoTTask](../classes/CoTTask.md#class-cottask) and [CoTProcess](../classes/CoTProcess.md#class-cotprocess) add declarative AI-based workflow features on top of core declarative workflow features of [Process](../classes/Process.md#class-process) and [Task](../classes/Task.md#class-task).

Specifically, `CoTTask` implements a default approach to prompt assembly within a CoT, has the logic to contact an AI (LLM), automatically manages AI-driven [transitions](../classes/CoTTask.md#attr-cottasktransitions) between states of the workflow, and has features for declaratively updating the shared [Process.state](../classes/Process.md#attr-processstate), including a [history mechanism](CoTHistory.md#kb-topic-cothistory) to help the AI maintain context as it moves through the workflow (see [CoTExecutionModels](CoTExecutionModels.md#kb-topic-cotexecutionmodels)).

`CoTProcess` extends the existing `Process` class with some features to coordinate with `CoTTask`, such as providing [prompt pieces that are common to all tasks](../classes/CoTTask.md#attr-cottaskprompt) as well as centrally defining [CoTProcess.optionalPrompts](../classes/CoTProcess.md#attr-cotprocessoptionalprompts) prompt parts that might be used by multiple tasks.

### Related

- [CoTProcess.getPromptPart](../classes/CoTProcess.md#method-cotprocessgetpromptpart)
- [CoTProcess](../classes/CoTProcess.md#class-cotprocess)
- [CoTTask](../classes/CoTTask.md#class-cottask)

---
