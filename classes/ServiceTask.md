# ServiceTask Documentation

[← Back to API Index](../reference.md)

---

## Class: ServiceTask

*Inherits from:* [Task](Task.md#class-task)

### Description
A ServiceTask is an element of a [Process](Process.md#class-process) which calls a DataSource operation, optionally using part of the [process state](Process.md#attr-processstate) as inputs or storing outputs in the process state. A special "export" [operationType](#attr-servicetaskoperationtype) is supported to perform a server export based on criteria.

By default a ServiceTask takes the data indicated by [inputField](Task.md#attr-taskinputfield) and/or [inputFieldList](Task.md#attr-taskinputfieldlist) as detailed in [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output) and uses the `inputRecord` as [DSRequest.data](DSRequest.md#attr-dsrequestdata). This means the input data becomes [Criteria](../reference.md#type-criteria) for "fetch" and "export" operations, new record values for an "add" operation, etc. For simplicity, if no `inputFieldList` is provided and `inputField` specifies an object, `inputData` is used as `dsRequest.data`.

Alternatively, you can set [ServiceTask.criteria](#attr-servicetaskcriteria) for a "fetch" and "export" operations, or [ServiceTask.values](#attr-servicetaskvalues) for other operationTypes. In both cases, you have the ability to use simple expressions like $input._fieldName_ to take portions of the input data and use it as part of the criteria or values.

OutputData and outputFieldList work as filters. You should determine which properties should be fetched into the process state. If you want to load all data without defining every property manually you can pass a name started with '$' and fetched record or records will be placed as a record or an array of records by the name without this specific symbol.

For example if you specify 'id' and 'name' in outputFieldList, only these properties will be fetched in the process state. If you pass '$orderHeader' in outputField a whole record will be stored in process state under the 'orderHeader' key.

---
## Attr: ServiceTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises from DataSource operation.

**Flags**: IR

---
## Attr: ServiceTask.outputField

### Description
Field in the [process state](Process.md#attr-processstate) where this task writes outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

See [ServiceTask.outputFieldList](#attr-servicetaskoutputfieldlist) for a shorthand method to save the full operation response data.

### Groups

- taskIO

**Flags**: IR

---
## Attr: ServiceTask.fixedValues

### Description
Values to be submitted as part of the DSRequest, regardless of inputs to the task. Will be combined with the data from the [Task.inputField](Task.md#attr-taskinputfield) or with [ServiceTask.values](#attr-servicetaskvalues) if specified, via simple copying of fields, with `fixedValues` overwriting values provided by the `inputField`, but explicitly specified [ServiceTask.values](#attr-servicetaskvalues) overriding `fixedValues`.

**Flags**: IR

---
## Attr: ServiceTask.exportFormat

### Description
The format in which the data should be exported. See [ExportFormat](../reference.md#type-exportformat) for more information.

**Flags**: IR

---
## Attr: ServiceTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)? See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state.

**Flags**: IR

---
## Attr: ServiceTask.outputFieldList

### Description
List of multiple fields in the [process state](Process.md#attr-processstate) where this task will write outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

If [ServiceTask.outputField](#attr-servicetaskoutputfield) is also specified, it will be implicitly added to the `outputFieldList` if it is not already present.

In addition to pulling individual fields from the task operation result and placing them into the process state the full response data can also be written into the process state without specifying individual fields. Prefix a destination field path with a "$" (ex. $orderHeader) causes the entire `dsResponse.data` to be saved.

### Groups

- taskIO

**Flags**: IR

---
## Attr: ServiceTask.values

### Description
Values to be submitted for "update", "add" and "remove" operations.

Similar to [Criteria](../reference.md#type-criteria), data values prefixed with "$" will be treated as a [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions). Use [ServiceTask.fixedValues](#attr-servicetaskfixedvalues) for any values that start with "$" but should be treated as a literal.

**Flags**: IR

---
## Attr: ServiceTask.operationType

### Description
Type of operation to invoke. A special "export" operation type is supported to perform a server export based on criteria.

**Flags**: IR

---
## Attr: ServiceTask.criteria

### Description
Criteria (including AdvancedCriteria) to use for "fetch" and "export" operations.

Data values in this criteria prefixed with "$" will be treated as dynamic expressions which can access the inputs to this task as $input - see [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

If any data value should not be treated as dynamic (for example, a "$" should be taken as literal), you can place it in [ServiceTask.fixedCriteria](#attr-servicetaskfixedcriteria) instead.

Ignored for any operationType other than "fetch" and "export". Update or delete operations should place the primary key to update in [ServiceTask.values](#attr-servicetaskvalues).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

### Groups

- taskIO

**Flags**: IR

---
## Attr: ServiceTask.fixedCriteria

### Description
Criteria to be submitted as part of the DSRequest, regardless of inputs to the task. Will be combined with the data from the [Task.inputField](Task.md#attr-taskinputfield) or with [ServiceTask.criteria](#attr-servicetaskcriteria) if specified, via [DataSource.combineCriteria](DataSource.md#classmethod-datasourcecombinecriteria).

**Flags**: IR

---
## Attr: ServiceTask.dataSource

### Description
DataSource ID or DataSource instance to be used.

**Flags**: IR

---
## Attr: ServiceTask.operationId

### Description
The [operationId](OperationBinding.md#attr-operationbindingoperationid) to invoke.

**Flags**: IR

---
