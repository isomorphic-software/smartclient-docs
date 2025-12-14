# CoTPromptScope

[← Back to API Index](../reference.md)

---

## KB Topic: CoTPromptScope

### Description
A common set of context variables and helper functions are available when using templates for [CoTTask.prompt](#attr-cottaskprompt), [CoTProcess.optionalPrompts](#attr-cotprocessoptionalprompts) entries, and [CoTTask.taskPrompt](#attr-cottasktaskprompt).

Context variables:

*   **task** — the current [CoTTask](../classes/CoTTask.md#class-cottask) instance (ID, title, description, etc)
*   **process** — the owning [CoTProcess](../classes/CoTProcess.md#class-cotprocess) instance (ID, policies, etc)
*   **goal** — equivalent to process.goal
*   **state** — the shared [CoTProcess.state](../classes/Process.md#attr-processstate) object for the workflow
*   **inputs** — inputs to this task if specified as [task.inputs](#cottaskinputs); the same data returned by [task.getInputRecord](#method-taskgetinputrecord) (may be absent if inputs were not defined)

Helper functions:

*   **json(x)** — render a compact JSON representation of x suitable for inclusion in a prompt
*   **promptPart(nameOrNames, omitNewlines?)** / **prt(...)** — insert one or more prompt parts as returned by [CoTProcess.getPromptPart](../classes/CoTProcess.md#method-cotprocessgetpromptpart).

---
