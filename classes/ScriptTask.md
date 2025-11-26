# ScriptTask Documentation

[← Back to API Index](../reference.md)

---

## Class: ScriptTask

*Inherits from:* [Task](Task.md#class-task)

### Description
Task that executes arbitrary code, either synchronous or asynchronous. Override the [execute()](#method-scripttaskexecute) method to provide custom logic.

---
## Attr: ScriptTask.isAsync

### Description
Whether the script task is asynchronous. A synchronous task is expected to return data directly from execute() and is considered complete once the execute() method exits.

An asynchronous task is expected to start processing in execute(), and will not be considered complete [ScriptTask.setOutput](#method-scripttasksetoutput) is called.

**Flags**: IR

---
## Attr: ScriptTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)?

See [taskInputExpressions](../reference_2.md#type-taskinputexpression) for details on the transient state outputs.

Note that this property does not affect the task at all but is an indicator to the user and to the workflow editor of the behavior of the task as coded (See [Process.passThruTaskOutput](Process.md#method-processpassthrutaskoutput)).

**Flags**: IR

---
## Method: ScriptTask.execute

### Description
Execute the task. The return value, if not `undefined`, will be written as the output.

For an asynchronous task, the return value is ignored and the task should call [ScriptTask.setOutput](#method-scripttasksetoutput) to continue the process with the next task.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| input | [Any](#type-any) | false | — | the task input |
| inputRecord | [Record](#type-record) | false | — | the task input record if `inputs` is specified. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output) |

### Returns

`[Any](#type-any)` — the task output. For multiple field output, call [ScriptTask.setOutput](#method-scripttasksetoutput) instead, and return null

---
## Method: ScriptTask.setOutput

### Description
Sets the task output available to the next task via [Process.getLastTaskOutput](Process.md#method-processgetlasttaskoutput) or more commonly, with a [TaskInputExpression](../reference_2.md#type-taskinputexpression) property. If [outputFieldList](Task.md#attr-taskoutputfieldlist) is specified, the output will also be written to the specified fields in the process state (See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output)).

To have the output written as-is to the process state, see [bindOutput](ProcessElement.md#attr-processelementbindoutput).

NOTE: for an [asynchronous task](#attr-scripttaskisasync), calling `setOutput()` indicates the task is complete.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| output | [Any](#type-any) | true | — | output record to provide to the next task |

### Groups

- taskIO

---
