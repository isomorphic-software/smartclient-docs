# CoTHistory

[← Back to API Index](../reference.md)

---

## KB Topic: CoTHistory

### Description
The history mechanism automatically maintains a list of the last N actions taking by an AI as part of executing a [CoTProcess](../classes/CoTProcess.md#class-cotprocess), to help the AI maintain context when it needs to execute a series of [CoTTasks](../classes/CoTTask.md#class-cottask) as part of an overall, logical task.

This is needed to support the more predictable ["AI Workflow"](CoTExecutionModels.md#kb-topic-cotexecutionmodels) execution model for enterprise AI workflows.

#### What is recorded
History is tracked automatically for: (a) transitions (the model emitted {goTo,intent,stepAfter}), and (b) successful non‑transition results that were validated and applied to [state](../classes/Process.md#attr-processstate) (for example via [CoTTask.stateUpdates](../classes/CoTTask.md#attr-cottaskstateupdates)).

#### History storage
The primary list is kept on the process as [history](../classes/CoTProcess.md#attr-cotprocesshistory). For ease of serialization and prompt access, a bounded mirror is also maintained at `process.state.history`. Both lists are append‑only during a run.

#### Including history in prompts
History is typically referenced from [standard prompt template](../classes/CoTTask.md#attr-cottaskprompt) via the "${promptPart('history')}", which includes the [CoTProcess.historyPrimer](../classes/CoTProcess.md#attr-cotprocesshistoryprimer) and history data.

#### Manual entries
Add entries programmatically via [CoTProcess.addHistory](../classes/CoTProcess.md#method-cotprocessaddhistory). This appends to the process history and mirrors to `state.history` within configured limits.
```
 process.addHistory({
   taskID: task.ID,
   summary: "Added field 'orderDate'",
   ts: Date.now()
 });
 
```

#### Maximum history entries
The in‑memory maximum is controlled by [CoTProcess.historyMaxItems](../classes/CoTProcess.md#attr-cotprocesshistorymaxitems). The mirrored `state.history` maximum is controlled by [CoTProcess.stateHistoryMaxItems](../classes/CoTProcess.md#attr-cotprocessstatehistorymaxitems) and defaults to the in‑memory maximum if unset. Older entries are dropped when limits are reached. Implementations may summarize older entries into a compact note before dropping them.

#### Truncation in Partial Prompts
When generating [partial prompts](CoTPartialPrompt.md#kb-topic-cotpartialprompt), history can be truncated via [PartialPromptConfig.truncateHistory](../classes/PartialPromptConfig.md#attr-partialpromptconfigtruncatehistory) to include only the N most recent entries. This is useful when debugging recent actions without including the full history.

### Related

- [CoTProcess.addHistory](../classes/CoTProcess.md#method-cotprocessaddhistory)

---
