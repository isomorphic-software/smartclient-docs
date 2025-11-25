# Task Documentation

[← Back to API Index](../main.md)

---

## Class: Task

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
A Task is an abstract superclass for all Task types that can be involved in a Process, such as a [DSRequestTask](DSRequestTask.md#class-dsrequesttask).

---
## Attr: Task.inputFieldList

### Description
List of multiple fields from the [process state](Process.md#attr-processstate) which are provided as input data to this task. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Deprecated**

**Flags**: IR

---
## Attr: Task.outputFieldList

### Description
List of multiple fields in the [process state](Process.md#attr-processstate) where this task will write outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

If [Task.outputField](#attr-taskoutputfield) is also specified, it will be implicitly added to the `outputFieldList` if it is not already present.

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.outputExpression

### Description
Special expression to write task output directly into a [DataBoundComponent](../main.md#interface-databoundcomponent). See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.inputs

### Description
Defines how fields in the [process state](Process.md#attr-processstate) are extracted for the input record to this task.

When `inputs` is an object, the keys are the [setter paths](../main_2.md#type-setterpath) of the fields to be set in the input record, and the values are literals or [taskInputExpressions](../main_2.md#type-taskinputexpression). See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.strictPaths

### Description
If set to true, the task will not allow any intermediate state to be set via [Task.setState](#method-tasksetstate) that is not explicitly defined first. This requirement can be overridden by an optional value in the [Task.setState](#method-tasksetstate) call.

This setting can be applied to the entire process with [Process.strictPaths](Process.md#attr-processstrictpaths).

**Flags**: IWR

---
## Attr: Task.outputField

### Description
Field in the [process state](Process.md#attr-processstate) where this task writes outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
## Method: Task.getInputRecord

### Description
Get all inputs to the task as specified by the [inputs](#attr-taskinputs), as a Record.

### Returns

`[Record](#type-record)` — input record

### Groups

- taskIO

---
## Method: Task.setOutput

### Description
Sets the task output available to the next task via [Process.getLastTaskOutput](Process.md#method-processgetlasttaskoutput) or more commonly, with a [TaskInputExpression](../main_2.md#type-taskinputexpression) property. If [outputFieldList](#attr-taskoutputfieldlist) is specified, the output will also be written to the specified fields in the process state (See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output)).

To have the output written as-is to the process state, see [bindOutput](ProcessElement.md#attr-processelementbindoutput).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| output | [Any](#type-any) | false | — | output record to provide to next task |

---
## Method: Task.getState

### Description
Returns a value from the [process state](Process.md#attr-processstate). Values can be written into the process state by [Task.setState](#method-tasksetstate), setting [ProcessElement.bindOutput](ProcessElement.md#attr-processelementbindoutput), or various task output settings (See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| statePath | [String](#type-string) | false | — | path to the value in the process state to set. Segments are separated by a decimal point (.) |

### Returns

`[Any](#type-any)` — the value found at the path

---
## Method: Task.setState

### Description
Sets a [process state](Process.md#attr-processstate) value for later reference with [Process.getStateVariable](Process.md#method-processgetstatevariable) or more commonly with a [TaskInputExpression](../main_2.md#type-taskinputexpression) property.

The path, which is one or more valid identifiers separated by periods, is used to identify the variable. By appending an empty pair of brackets (\[\]) the value will be placed into an existing or new array at the specified path.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stateVariablePath | [String](#type-string) | false | — | path to the variable in the process state to set. segments are separated by a decimal point (.) |
| value | [TaskInputExpression](../main_2.md#type-taskinputexpression)|[Any](#type-any) | false | — | the value to save |
| strict | [Boolean](#type-boolean) | false | — | if true, the path must exist in the state to be set. If false, the path will be created if it does not exist. Defaults to `process.strictPaths` when null. |

---
## Method: Task.getExpressionValue

### Description
Get the value of a [inputExpression](../main_2.md#type-taskinputexpression).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | expression to evaluate |

### Returns

`[Any](#type-any)` — value of expression

### Groups

- taskIO

---
