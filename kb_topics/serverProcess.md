# Server-Side Process Execution

[← Back to API Index](../reference.md)

---

## KB Topic: Server-Side Process Execution

### Description
**Server-Side Process Execution**

[OperationBinding.process](../classes/OperationBinding.md#attr-operationbindingprocess) allows a declarative [Process](../classes/Process.md#class-process) workflow to execute server-side as an alternative to [OperationBinding.script](../classes/OperationBinding.md#attr-operationbindingscript) or a [DMI](../reference_2.md#object-serverobject). The workflow is defined in the same XML format used by the [WorkflowEditor](#class-workfloweditor), making it visually editable by non-programmers.

**When to Use Each Approach**

| Approach | Best For | Editable? |
|---|---|---|
| process | Multi-step declarative logic: validate, branch, CRUD across DataSources, send email | Yes (WorkflowEditor) |
| script | Imperative logic: complex calculations, string manipulation, calling Java APIs directly | Code only |
| DMI (serverObject) | Heavy Java logic: third-party library integration, complex transactions, performance-critical paths | Code only |

**Input State**

The process receives automatic input state from the DSRequest:

*   `criteria`: Request criteria
*   `values`: Request values (add/update)
*   `oldValues`: Previous values (update)
*   `operationType`: "fetch", "add", "update", or "remove"
*   `dsName`: DataSource ID
*   `operationId`: The operationBinding's operationId

These are available in [TaskInputExpressions](../reference_2.md#type-taskinputexpression) as `$criteria`, `$values`, etc.

**Output / Response**

The process produces a DSResponse via precedence:

1.  If `process.state.dsResponse` is set → used directly
2.  Else, output of last [DSRequestTask](../classes/DSRequestTask.md#class-dsrequesttask) that ran → its dsResponse.data
3.  Else → empty STATUS\_SUCCESS

**Error Handling**

If any task fails and has no [DSRequestTask.failureElement](../classes/DSRequestTask.md#attr-dsrequesttaskfailureelement), the process aborts immediately and returns STATUS\_FAILURE. If the operation participates in a transaction ([OperationBinding.autoJoinTransactions](../classes/OperationBinding.md#attr-operationbindingautojointransactions)), the transaction rolls back.

**Server-Side Task Compatibility**

Only tasks that operate on data, logic, or communication work server-side. UI tasks (FormSetValuesTask, ShowHideTask, GridFetchDataTask, etc.) are NOT available and will log a warning if encountered.

**Performance**

Process execution uses server-side JavaScript context pooling. First invocation per pool slot incurs module loading overhead; subsequent invocations reuse the pre-loaded context with near-zero overhead beyond the actual DataSource operations.

### Related

- [DSRequestTask](../classes/DSRequestTask.md#class-dsrequesttask)
- [DSFetchTask](../reference.md#class-dsfetchtask)
- [DSAddTask](../reference.md#class-dsaddtask)
- [DSUpdateTask](../reference.md#class-dsupdatetask)
- [DSRemoveTask](../reference.md#class-dsremovetask)
- [ScriptTask](../classes/ScriptTask.md#class-scripttask)
- [DecisionTask](../classes/DecisionTask.md#class-decisiontask)
- [MultiDecisionTask](../classes/MultiDecisionTask.md#class-multidecisiontask)
- [StateTask](../classes/StateTask.md#class-statetask)
- [StartProcessTask](../classes/StartProcessTask.md#class-startprocesstask)
- [SubProcessTask](../classes/SubProcessTask.md#class-subprocesstask)
- [EndProcessTask](../reference.md#class-endprocesstask)
- [SendEmailTask](../classes/SendEmailTask.md#class-sendemailtask)
- [SendSMSTask](../classes/SendSMSTask.md#class-sendsmstask)
- [DefaultOperationTask](../classes/DefaultOperationTask.md#class-defaultoperationtask)
- [OperationBinding.process](../classes/OperationBinding.md#attr-operationbindingprocess)
- [Process.dataSources](../classes/Process.md#attr-processdatasources)
- [ScriptTask.language](../classes/ScriptTask.md#attr-scripttasklanguage)
- [ScriptTask.dataSources](../classes/ScriptTask.md#attr-scripttaskdatasources)

### See Also

- [OperationBinding.process](../classes/OperationBinding.md#attr-operationbindingprocess)
- [OperationBinding.script](../classes/OperationBinding.md#attr-operationbindingscript)

---
