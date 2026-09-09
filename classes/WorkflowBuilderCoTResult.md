# WorkflowBuilderCoTResult Documentation

[← Back to API Index](../reference.md)

---

## Attr: WorkflowBuilderCoTResult.addedEditNode

### Description
Convenience alias for the _last_ entry's `addedEditNode` in [addedSteps](#attr-workflowbuildercotresultaddedsteps) (absent if `addedSteps` is empty).

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.explorationHistory

### Description
Exploration entries accumulated this call (the input [explorationHistory](WorkflowBuilderCoTParams.md#attr-workflowbuildercotparamsexplorationhistory) plus, if exploration ran, one new entry per explored step). Only the most recent entry carries the full result sample; earlier entries are trimmed to a one-line summary.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.addedTaskType

### Description
Convenience alias for the _last_ entry's `addedTaskType` in [addedSteps](#attr-workflowbuildercotresultaddedsteps).

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.refusalReason

### Description
Present only when [refused](#attr-workflowbuildercotresultrefused) is `true`; a short natural-language explanation suitable for display to the end user.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.failureHandlerTitle

### Description
Convenience alias for the _last_ entry's `failureHandlerTitle` in [addedSteps](#attr-workflowbuildercotresultaddedsteps), when present.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.addedSteps

### Description
One entry per step actually added this invocation, oldest first, each `{addedEditNode, addedTaskType, addedTitle}`. In [singleStep](WorkflowBuilderCoTParams.md#attr-workflowbuildercotparamssinglestep) mode, or when the default decomposition only ever needed one step, this has exactly one entry. An entry additionally carries `failureHandlerEditNode`/`failureHandlerTitle` when that step's intent named explicit failure handling (see [stepIntent](WorkflowBuilderCoTParams.md#attr-workflowbuildercotparamsstepintent)) - the sibling [ShowNotificationTask](ShowNotificationTask.md#class-shownotificationtask) EditNode committed alongside it, wired via `failureElement`, not chained into the normal flow.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.refused

### Description
`true` when `stepIntent` (or, mid-decomposition, the current step decided by `decideNextStep`) does not map to any available DataSource operation, UI action, or branch point, or when `maxDecomposedSteps` was reached. This ends the session but is a **partial success, not a rollback** - whatever steps are already in [addedSteps](#attr-workflowbuildercotresultaddedsteps) stay in the Workflow.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.addedTitle

### Description
Convenience alias for the _last_ entry's `addedTitle` in [addedSteps](#attr-workflowbuildercotresultaddedsteps).

**Flags**: IR

---
## Attr: WorkflowBuilderCoTResult.failureHandlerEditNode

### Description
Convenience alias for the _last_ entry's `failureHandlerEditNode` in [addedSteps](#attr-workflowbuildercotresultaddedsteps), when present.

**Flags**: IR

---
