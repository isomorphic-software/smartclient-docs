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

#### How much history reaches the prompt
History is rendered in two zones. The most recent [CoTProcess.historyDetailItems](../classes/CoTProcess.md#attr-cotprocesshistorydetailitems) entries appear in full, with their `intent` and `stepAfter`. Every earlier entry appears as a single `action | result` line, capped at [CoTProcess.historyResultMaxChars](../classes/CoTProcess.md#attr-cotprocesshistoryresultmaxchars) characters. Nothing is omitted: a process uses this log to know what it has already done, so an entry that disappeared would be work the process would repeat.

Set [CoTProcess.historyDetailItems](../classes/CoTProcess.md#attr-cotprocesshistorydetailitems) to trade prompt size against detail, and [CoTProcess.noHistory](../classes/CoTProcess.md#attr-cotprocessnohistory) to leave history out of a prompt altogether.

#### Maximum history entries
[CoTProcess.historyMaxItems](../classes/CoTProcess.md#attr-cotprocesshistorymaxitems) is a retention ceiling on the in-memory list - a guard against a runaway process, not a way to bound the prompt. The mirrored `state.history` maximum is [CoTProcess.stateHistoryMaxItems](../classes/CoTProcess.md#attr-cotprocessstatehistorymaxitems), and defaults to the in-memory ceiling if unset.

#### Truncation in Partial Prompts
When generating [partial prompts](CoTPartialPrompt.md#kb-topic-cotpartialprompt), history can be truncated via [PartialPromptConfig.truncateHistory](../classes/PartialPromptConfig.md#attr-partialpromptconfigtruncatehistory) to include only the N most recent entries. This is useful when debugging recent actions without including the full history.

### Related

- [CoTProcess.addHistory](../classes/CoTProcess.md#method-cotprocessaddhistory)
- [CoTProcess.getHistoryParts](../classes/CoTProcess.md#method-cotprocessgethistoryparts)
- [CoTProcess.getCompactHistoryLines](../classes/CoTProcess.md#method-cotprocessgetcompacthistorylines)

---
