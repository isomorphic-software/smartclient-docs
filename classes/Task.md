# Task Documentation

[← Back to API Index](../reference.md)

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
Special expression to write task output directly into a [DataBoundComponent](../reference.md#interface-databoundcomponent). See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.inputs

### Description
Defines how fields in the [process state](Process.md#attr-processstate) are extracted for the [input record](#method-taskgetinputrecord) to this task. `inputs` may be:

*   a single [StatePath](../reference_2.md#type-statepath) or [TaskInputExpression](../reference_2.md#type-taskinputexpression): the value it refers to is the task's `$input`. If that value is a Record, its fields form the input record; otherwise the value is stored in the input record under the last segment of the path.
*   an Array of `StatePaths`: each value is stored in the input record under the last segment of its path.
*   an Object: each key is a [StatePath](../reference_2.md#type-statepath) (in its setter form) into the input record, and each value is a [TaskInputExpression](../reference_2.md#type-taskinputexpression), a [StatePath](../reference_2.md#type-statepath) into [Process.state](Process.md#attr-processstate), or, for a non-String value, a literal. Because a String value is always resolved, a literal String cannot be supplied this way. `$input` cannot be referenced here, since it is the result of these `inputs`.

When neither `inputs` nor the deprecated [Task.inputFieldList](#attr-taskinputfieldlist) is set, the input record is the entire process state. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output) for details and examples.

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
Get all inputs to the task as specified by the [inputs](#attr-taskinputs), as a Record. When the task declares no `inputs`, the input record is a shallow copy of the entire [Process.state](Process.md#attr-processstate): fields can be added to or replaced in the returned record without affecting the process state, but nested objects are shared with it and must not be modified. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output) for how each form of `inputs` contributes to the input record.

Outside of a running process, for example while a task is being edited, there is no state to draw from and declared inputs have no values.

### Returns

`[Record](#type-record)` — input record

### Groups

- taskIO

---
## Method: Task.getCriteriaExpressionValue

### Description
Get the value of a Criteria or AdvancedCriteria by resolving any values containing [taskInputExpression](../reference_2.md#type-taskinputexpression)s. The criteria passed in is not modified; a resolved copy is returned.

Data values in the criteria prefixed with "$" will be treated as dynamic expressions as detailed in [TaskInputExpression](../reference_2.md#type-taskinputexpression). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue). To use a literal value starting with "$", escape it with a backslash: the value `\$last` resolves to the String `$last`.

For AdvancedCriteria only, when [Process.ruleScope](Process.md#attr-processrulescope) is set, a [dynamic criteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) containing [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) values is also resolved against the ruleScope component's [ruleContext](Canvas_1.md#method-canvasgetrulecontext).

Returns null when called outside of a running process.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria) | false | — | criteria to resolve |

### Returns

`[Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria)` — resolved copy of criteria

### Groups

- taskIO

---
## Method: Task.setOutput

### Description
Sets the task output available to the next task via [Process.getLastTaskOutput](Process.md#method-processgetlasttaskoutput) or more commonly, with a [TaskInputExpression](../reference_2.md#type-taskinputexpression) property. If [outputFieldList](#attr-taskoutputfieldlist) is specified, the output will also be written to the specified fields in the process state (See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output)).

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
| statePath | [StatePath](../reference_2.md#type-statepath) | false | — | path to the value in the process state to retrieve |

### Returns

`[Any](#type-any)` — the value found at the path

---
## Method: Task.setState

### Description
Sets a [process state](Process.md#attr-processstate) value for later reference with [Process.getStateVariable](Process.md#method-processgetstatevariable) or more commonly, with a [TaskInputExpression](../reference_2.md#type-taskinputexpression) property.

The path, which is one or more valid identifiers separated by periods, is used to identify the variable. By appending an empty pair of brackets (\[\]) the value will be placed into an existing or new array at the specified path.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| statePath | [StatePath](../reference_2.md#type-statepath) | false | — | path to the variable in the process state to set. segments are separated by a decimal point (.) |
| value | [TaskInputExpression](../reference_2.md#type-taskinputexpression)|[Any](#type-any) | false | — | the value to save |
| strict | [Boolean](#type-boolean) | false | — | if true, every intermediate segment of the path must already exist in the state; the final segment is always created or replaced. If false, missing intermediate objects are created. Defaults to [Task.strictPaths](#attr-taskstrictpaths), then [Process.strictPaths](Process.md#attr-processstrictpaths), when null. |

---
## Method: Task.getExpressionValue

### Description
Get the value of a [inputExpression](../reference_2.md#type-taskinputexpression). A String that does not start with "$" is treated as a [StatePath](../reference_2.md#type-statepath) into [Process.state](Process.md#attr-processstate); any other non-null value is a literal and returned unchanged. Expressions are resolved as by [Process.getExpressionValue](Process.md#method-processgetexpressionvalue), plus `$input`, drawn from this task's [inputs](#attr-taskinputs).

Outside of a running process a String expression resolves to null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [TaskInputExpression](../reference_2.md#type-taskinputexpression)|[Any](#type-any) | false | — | expression to evaluate, or a StatePath |

### Returns

`[Any](#type-any)` — value of expression

### Groups

- taskIO

---
