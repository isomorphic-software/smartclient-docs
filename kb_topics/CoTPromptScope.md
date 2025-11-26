# CoTPromptScope

[← Back to API Index](../reference.md)

---

## KB Topic: CoTPromptScope

### Description
A common set of context variables and helper functions are available when using templates for [CoTTask.prompt](../classes/CoTTask.md#attr-cottaskprompt), [CoTProcess.optionalPrompts](../classes/CoTProcess.md#attr-cotprocessoptionalprompts) entries, and [CoTTask.taskPrompt](../classes/CoTTask.md#attr-cottasktaskprompt).

#### Context variables
The following objects/values are always available to template expressions:

*   **task** — the current [CoTTask](../classes/CoTTask.md#class-cottask) instance (ID, title, description, etc)
*   **process** — the owning [CoTProcess](../classes/CoTProcess.md#class-cotprocess) instance (ID, policies, etc)
*   **goal** — equivalent to process.goal
*   **state** — the shared [CoTProcess.state](../classes/Process.md#attr-processstate) object for the workflow
*   **inputs** — inputs to this task if specified as [task.inputs](../classes/Task.md#attr-taskinputs); the same data returned by [Task.getInputRecord](../classes/Task.md#method-taskgetinputrecord) (may be absent if inputs were not defined)

#### Helper functions

*   **json(x)** — render a compact JSON representation of `x` suitable for inclusion in a prompt (intended for small/medium objects).
*   **promptPart(nameOrNames, omitNewlines?)** / **prt(...)** — insert one or more prompt parts as returned by [CoTProcess.getPromptPart](../classes/CoTProcess.md#method-cotprocessgetpromptpart).

---
