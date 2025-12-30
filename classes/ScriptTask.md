# ScriptTask Documentation

[← Back to API Index](../reference.md)

---

## Class: ScriptTask

*Inherits from:* [Task](Task.md#class-task)

### Description
Task that executes arbitrary code, either synchronous or asynchronous. Override the [execute()](#method-scripttaskexecute) method to provide custom logic.

---
## Attr: ScriptTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)? See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state.

**Flags**: IR

---
## Attr: ScriptTask.isAsync

### Description
Whether the script task is asynchronous. A synchronous task is expected to return data directly from execute() and is considered complete once the execute() method exits.

An asnychronous task is expected to start processing in execute(), and will not be considered complete until either [ScriptTask.setOutputData](#method-scripttasksetoutputdata) or [ScriptTask.setOutputRecord](#method-scripttasksetoutputrecord) is called.

**Flags**: IR

---
## Method: ScriptTask.execute

### Description
Execute the task.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| input | [Any](#type-any) | false | — | the task input |
| inputRecord | [Record](#type-record) | false | — | the task input record if an `inputFieldList` was specified. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output) |

### Returns

`[Any](#type-any)` — the task output. For multiple field output, call [ScriptTask.setOutputRecord](#method-scripttasksetoutputrecord) instead, and return null

---
## Method: ScriptTask.getInputData

### Description
Get the inputs to this task as specified by [Task.inputField](Task.md#attr-taskinputfield).

For a task with a [inputFieldList](Task.md#attr-taskinputfieldlist), use [ScriptTask.getInputRecord](#method-scripttaskgetinputrecord) to get access to other inputs.

### Returns

`[Any](#type-any)` — input data

### Groups

- taskIO

---
## Method: ScriptTask.getProcess

### Description
Get the process executing this task instance.

### Returns

`[Process](#type-process)` — the owning process

---
## Method: ScriptTask.setOutputRecord

### Description
Set all outputs of the task as specified by the [outputFieldList](Task.md#attr-taskoutputfieldlist), by providing a Record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| outputRecord | [Record](#type-record) | false | — | output record |

### Groups

- taskIO

---
## Method: ScriptTask.getInputRecord

### Description
Get all inputs to the task as specified by the [inputFieldList](Task.md#attr-taskinputfieldlist), as a Record.

### Returns

`[Record](#type-record)` — input data

### Groups

- taskIO

---
## Method: ScriptTask.setOutputData

### Description
Set the task output as specified by [Task.outputField](Task.md#attr-taskoutputfield).

NOTE: for an [asychronous task](#attr-scripttaskisasync), calling `setOutputData()` indicates the task is complete. For a task with [multiple outputs](Task.md#attr-taskoutputfieldlist), call [ScriptTask.setOutputRecord](#method-scripttasksetoutputrecord) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskOutput | [Any](#type-any) | false | — | task output |

### Groups

- taskIO

---
