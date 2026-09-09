# WorkflowBuilderCoTParams Documentation

[← Back to API Index](../reference.md)

---

## Attr: WorkflowBuilderCoTParams.editContext

### Description
The live EditContext the Workflow is being built in.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.dataSourceIDs

### Description
Array of DataSource IDs the AI may target.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.stepIntent

### Description
Natural-language description of the step to add. By default (see [singleStep](#attr-workflowbuildercotparamssinglestep)) this may describe a compound, multi-step goal; `decideNextStep` decomposes it. For a DataSource-operation step, may also explicitly describe failure handling (e.g. "...; if it fails, notify the user that the order could not be saved") - `pickStep` extracts that as an opt-in `failureIntent` and `configureFailureHandler` authors a [ShowNotificationTask](ShowNotificationTask.md#class-shownotificationtask) wired onto that one step's OWN [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement) (a Task-level handler, independent of [Process.errorTask](Process.md#attr-processerrortask)/ [Process.errorTaskRef](Process.md#attr-processerrortaskref), the separate Process-wide default - see [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask)). Only ever set when the intent explicitly names failure behavior; never invented.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.singleStep

### Description
When `true`, `stepIntent` is treated as exactly one atomic step (the original, pre-decomposition behavior) - no decomposition, no looping, and `decideNextStep` makes no AI call of its own. When absent/false (the default), `stepIntent` may describe a goal requiring several steps; the process keeps adding steps until the goal is satisfied or `maxDecomposedSteps` is reached.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.explorationSettings

### Description
Optional. When `{enabled:true}`, a candidate DataSource-fetch step is actually executed against the real DataSource before being committed, so its live result can inform this and later steps. `readOnlyOnly` (default `true` whenever exploration is enabled) restricts exploration to fetches only - add/update/remove candidates are refused without executing, since a write cannot be meaningfully "previewed" without actually performing it.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.uiEditContext

### Description
Optional. The EditContext of the UI the Workflow is attached to (NOT this Workflow's own [editContext](#attr-workflowbuildercotparamseditcontext) - a different EditContext, holding component EditNodes rather than task EditNodes). When supplied, checked first to resolve each candidate component - but NOT required for grounding: any component in [componentIDs](#attr-workflowbuildercotparamscomponentids) that resolves as a live, drawn global via [Canvas.getById](Canvas.md#classmethod-canvasgetbyid) is grounded with its own fields/tabs/DataSource schema regardless of whether `uiEditContext` is supplied at all.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.processEditNode

### Description
The root Process EditNode within [editContext](#attr-workflowbuildercotparamseditcontext) to append the new task under.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.dataSourceOperationsOnly

### Description
When `true`, restricts `pickStep` so the AI cannot select anything but a DSFetchTask/DSAddTask/DSUpdateTask/DSRemoveTask - UI actions, notifications, and branch points are not offered at all. An explicit, enforced restriction, not just an emergent property of omitting [componentIDs](#attr-workflowbuildercotparamscomponentids) (which only keeps UI-action step kinds out - branching and notification steps are still offered unconditionally once other conditions are met).

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.componentIDs

### Description
Optional array of UI component IDs the AI may target with a UI-action step ([FormSetFieldValueTask](../reference.md#class-formsetfieldvaluetask)/[GridSelectRecordsTask](GridSelectRecordsTask.md#class-gridselectrecordstask)/[SelectTabTask](../reference.md#class-selecttabtask)/ [ClickButtonTask](../reference.md#class-clickbuttontask), among others). When omitted or empty, `pickStep` does not offer UI-action step kinds at all - this process remains DataSource-operations-only unless a caller explicitly opts in.

**Flags**: IR

---
## Attr: WorkflowBuilderCoTParams.explorationHistory

### Description
Optional. Pass forward the [explorationHistory](WorkflowBuilderCoTResult.md#attr-workflowbuildercotresultexplorationhistory) output of a prior invocation to carry exploration context into a later step of the same multi-step build session - this process does not persist state between separate `create()` calls on its own.

**Flags**: IR

---
