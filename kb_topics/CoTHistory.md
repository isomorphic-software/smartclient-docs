# CoTHistory

[← Back to API Index](../reference.md)

---

## KB Topic: CoTHistory

### Description
The history mechanism automatically maintains a list of recent actions taken by an AI as part of a [CoTProcess](../classes/CoTProcess.md#class-cotprocess), to help the AI maintain context when it needs to execute a series of [CoTTasks](../classes/CoTTask.md#class-cottask) as part of an overall, logical task.

What is recorded: (a) transitions (the model emitted {goTo,intent,stepAfter}), and (b) successful non‑transition results that were validated and applied to [state](../classes/Process.md#attr-processstate) (for example via [CoTTask.stateUpdates](#attr-cottaskstateupdates)).

History storage: The primary list is kept on the process as [history](#attr-cotprocesshistory). For ease of serialization and prompt access, a bounded mirror is also maintained at `process.state.history`. Both lists are append‑only during a run. Limits are controlled by [CoTProcess.historyMaxItems](#attr-cotprocesshistorymaxitems) (memory) and [CoTProcess.stateHistoryMaxItems](#attr-cotprocessstatehistorymaxitems) (state mirror).

### Related

- [CoTProcess.addHistory](../classes/CoTProcess.md#method-cotprocessaddhistory)

---
