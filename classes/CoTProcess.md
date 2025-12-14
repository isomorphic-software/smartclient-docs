# CoTProcess Documentation

[← Back to API Index](../reference.md)

---

## Class: CoTProcess

*Inherits from:* [Process](Process.md#class-process)

### Description
CoTProcess coordinates with [CoTTask](CoTTask.md#class-cottask) by providing default prompt parts (see [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart)) and global handling used by CoTTasks that run inside a CoTProcess (for example, shared goal/context, history visibility, and declarative prompt fragments).

CoTProcess overrides [Process.defaultTaskConstructor](#processdefaulttaskconstructor) so plain Objects in [Process.tasks](#processtasks) or sequences become [CoTTask](CoTTask.md#class-cottask) by default unless they specify their own constructor.

Use [CoTProcess.optionalPrompts](#attr-cotprocessoptionalprompts) for fragments shared by several - but not all - tasks. Those tasks can use [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart) to obtain those prompt segments, including via the in-template helpers `promptPart()` / `prt()`.

History: CoTProcess maintains a bounded [history](#attr-cotprocesshistory) list (mirrored to `state.history`) so prompts can include recent AI actions. See [CoTHistory](../kb_topics/CoTHistory.md#kb-topic-cothistory) for what is recorded, how it is stored, and how to include it (for example, `${promptPart('history')}`). Primer text for history is customizable via [CoTProcess.historyPrimer](#attr-cotprocesshistoryprimer).

Further features:

*   Engine selection: [CoTProcess.aiEngineId](#attr-cotprocessaiengineid) (tasks may override with [CoTTask.aiEngineId](#attr-cottaskaiengineid); system default [AI.defaultAIEngineId](#aidefaultaiengineid))
*   Retry policy: [CoTProcess.maxRetries](#attr-cotprocessmaxretries) (task override [CoTTask.maxRetries](#attr-cottaskmaxretries))
*   Execution models overview: [CoTExecutionModels](../kb_topics/CoTExecutionModels.md#kb-topic-cotexecutionmodels)
*   CoTTask step authoring: [CoTTask](CoTTask.md#class-cottask)

### Groups

- CoT

---
## Method: CoTProcess.getPromptPart

### Description
Returns a named prompt fragment or concatenation of fragments for inclusion in task prompts. Built-in names:

*   **"goal"** – primer from [CoTProcess.goalPrimer](#attr-cotprocessgoalprimer), then [CoTProcess.goal](#attr-cotprocessgoal).
*   **"history"** – primer from [CoTProcess.historyPrimer](#attr-cotprocesshistoryprimer), then recent entries (omitted if [noHistory](#attr-cotprocessnohistory) is true)
*   **"transitions"** – [CoTProcess.transitionsPrimer](#attr-cotprocesstransitionsprimer) followed by the current task’s transitions
*   **"errors"** – primer from [CoTProcess.errorsPrimer](#attr-cotprocesserrorsprimer) (or [CoTTask.errorsPrimer](#attr-cottaskerrorsprimer)), then current validation errors if any
*   **"goalData"** – the raw [CoTProcess.goal](#attr-cotprocessgoal) value.

Names matching keys in [CoTProcess.optionalPrompts](#attr-cotprocessoptionalprompts) return that text. Pass an Array of names to concatenate multiple parts. Set `omitNewlines` to true to omit surrounding newlines.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| names | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | One or more fragment names |
| omitNewlines | [Boolean](#type-boolean) | false | — | If true, do not surround with newlines |

### Returns

`[String](#type-string)` — Assembled fragment(s)

### Groups

- CoT

---
## Method: CoTProcess.addHistory

### Description
Add a history entry to [history](#attr-cotprocesshistory) and, if within limits, mirror to state.history. Honors [CoTProcess.noHistory](#attr-cotprocessnohistory). Entries beyond [CoTProcess.historyMaxItems](#attr-cotprocesshistorymaxitems) are discarded; the state mirror obeys [CoTProcess.stateHistoryMaxItems](#attr-cotprocessstatehistorymaxitems) (or historyMaxItems if null).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| entry | [CoTHistoryEntry](#type-cothistoryentry) | false | — | Entry to append |

### Groups

- CoTHistory

---
