# WorkflowBuilderAddedStep Documentation

[← Back to API Index](../reference.md)

---

## Attr: WorkflowBuilderAddedStep.addedTitle

### Description
The resolved title of the added step - see [OperationBinding.title](OperationBinding.md#attr-operationbindingtitle) and [DataSource.getAutoTitle](DataSource_1.md#method-datasourcegetautotitle) for how a DataSource-operation step's title is resolved.

**Flags**: IR

---
## Attr: WorkflowBuilderAddedStep.failureHandlerTitle

### Description
Present only alongside [failureHandlerEditNode](#attr-workflowbuilderaddedstepfailurehandlereditnode) - the resolved title of that failure-handling step.

**Flags**: IR

---
## Attr: WorkflowBuilderAddedStep.addedTaskType

### Description
The Task class added for this step (e.g. `"DSFetchTask"`, `"DSUpdateTask"`, `"SelectTabTask"`).

**Flags**: IR

---
## Attr: WorkflowBuilderAddedStep.failureHandlerEditNode

### Description
Present only when this step's intent named explicit failure handling - the sibling [ShowNotificationTask](ShowNotificationTask.md#class-shownotificationtask) EditNode committed alongside it, wired via [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement).

**Flags**: IR

---
## Attr: WorkflowBuilderAddedStep.addedEditNode

### Description
The [EditNode](../reference.md#object-editnode) added to the Workflow's [EditContext](EditContext.md#class-editcontext) for this step.

**Flags**: IR

---
