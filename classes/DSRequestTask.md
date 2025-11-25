# DSRequestTask Documentation

[← Back to API Index](../main.md)

---

## Class: DSRequestTask

*Inherits from:* [Task](Task.md#class-task)

### Description
A DSRequestTask (previously called ServiceTask) is an element of a [Process](Process.md#class-process) which calls a DataSource operation, optionally using part of the [process state](Process.md#attr-processstate) as inputs or storing outputs in the process state. A special "export" [operationType](#attr-dsrequesttaskoperationtype) is supported to perform a server export based on criteria.

By default, a DSRequestTask takes the data indicated by [inputs](Task.md#attr-taskinputs) as detailed in [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output) and uses the `inputRecord` as [DSRequest.data](DSRequest.md#attr-dsrequestdata). This means the input data becomes [Criteria](../main_2.md#type-criteria) for "fetch" and "export" operations, new record values for an "add" operation, etc.

Alternatively, you can set [DSRequestTask.criteria](#attr-dsrequesttaskcriteria) for a "fetch" and "export" operations, or [DSRequestTask.values](#attr-dsrequesttaskvalues) for other operationTypes. In both cases, you can use simple expressions like $input._fieldName_ to take portions of the input data and use it as part of the criteria or values.

OutputData and outputFieldList work as filters. You should determine which properties should be fetched into the process state. If you want to load all data without defining every property manually, you can pass a name started with '$'. The fetched record or records will be placed as a record or an array of records by the name without this specific symbol.

For example, if you specify 'id' and 'name' in outputFieldList, only these properties will be fetched in the process state. If you pass '$orderHeader' in outputField a whole record will be stored in the process state under the 'orderHeader' key.

---
## Attr: DSRequestTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)?

See [taskInputExpressions](../main_2.md#type-taskinputexpression) for details on the transient state outputs.

Note that this property does not affect the task at all but is an indicator to the user and to the workflow editor of the behavior of the task as coded (See [Process.passThruTaskOutput](Process.md#method-processpassthrutaskoutput)).

**Flags**: IR

---
## Attr: DSRequestTask.outputField

### Description
Field in the [process state](Process.md#attr-processstate) where this task writes outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

See [DSRequestTask.outputFieldList](#attr-dsrequesttaskoutputfieldlist) for a shorthand method to save the full operation response data.

### Groups

- taskIO

**Flags**: IR

---
## Attr: DSRequestTask.sort

### Description
An array of [SortSpecifier](../main_2.md#object-sortspecifier) objects used to set up the sort configuration for a fetch.

**Flags**: IR

---
## Attr: DSRequestTask.values

### Description
Values to be submitted for "update", "add" and "remove" operations.

Similar to [Criteria](../main_2.md#type-criteria), data values prefixed with "$" will be treated as a [TaskInputExpression](../main_2.md#type-taskinputexpression). Use [DSRequestTask.fixedValues](#attr-dsrequesttaskfixedvalues) for any values that start with "$" but should be treated as a literal.

**Flags**: IR

---
## Attr: DSRequestTask.fixedValues

### Description
Values to be submitted as part of the DSRequest, regardless of inputs to the task. Will be combined with the data from the [Task.inputs](Task.md#attr-taskinputs) or with [DSRequestTask.values](#attr-dsrequesttaskvalues) if specified, via simple copying of fields, with `fixedValues` overwriting values provided by the `inputs`, but explicitly specified [DSRequestTask.values](#attr-dsrequesttaskvalues) overriding `fixedValues`.

**Flags**: IR

---
## Attr: DSRequestTask.criteria

### Description
Criteria (including AdvancedCriteria) to use for "fetch" and "export" operations.

Data values in this criteria prefixed with "$" will be treated as dynamic expressions which can access the inputs to this task as $input - see [TaskInputExpression](../main_2.md#type-taskinputexpression). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

If any data value should not be treated as dynamic (for example, a "$" should be taken as literal), you can place it in [DSRequestTask.fixedCriteria](#attr-dsrequesttaskfixedcriteria) instead.

Ignored for any operationType other than "fetch" and "export". Update or delete operations should place the primary key to update in [DSRequestTask.values](#attr-dsrequesttaskvalues).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

### Groups

- taskIO

**Flags**: IR

---
## Attr: DSRequestTask.dataSource

### Description
DataSource ID or DataSource instance to be used.

**Flags**: IR

---
## Attr: DSRequestTask.operationId

### Description
The [operationId](OperationBinding.md#attr-operationbindingoperationid) to invoke.

**Flags**: IR

---
## Attr: DSRequestTask.exportFormat

### Description
The format in which the data should be exported. See [ExportFormat](../main_2.md#type-exportformat) for more information.

**Flags**: IR

---
## Attr: DSRequestTask.summaryFunctions

### Description
A mapping from field names to [summary functions](../main_2.md#type-summaryfunction) to be applied to each field for a fetch.

See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [DSRequestTask.groupBy](#attr-dsrequesttaskgroupby)

**Flags**: IR

---
## Attr: DSRequestTask.groupBy

### Description
List of fields to group by for a fetch.

See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [DSRequestTask.summaryFunctions](#attr-dsrequesttasksummaryfunctions)

**Flags**: IR

---
## Attr: DSRequestTask.outputFieldList

### Description
List of multiple fields in the [process state](Process.md#attr-processstate) where this task will write outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

If [DSRequestTask.outputField](#attr-dsrequesttaskoutputfield) is also specified, it will be implicitly added to the `outputFieldList` if it is not already present.

In addition to pulling individual fields from the task operation result and placing them into the process state the full response data can also be written into the process state without specifying individual fields. Prefix a destination field path with a "$" (ex. $orderHeader) causes the entire `dsResponse.data` to be saved.

### Groups

- taskIO

**Flags**: IR

---
## Attr: DSRequestTask.operationType

### Description
Type of operation to invoke. A special "export" operation type is supported to perform a server export based on criteria.

**Flags**: IR

---
## Attr: DSRequestTask.fixedCriteria

### Description
Criteria to be submitted as part of the DSRequest, regardless of inputs to the task. Will be combined with the data from the [Task.inputs](Task.md#attr-taskinputs) or with [DSRequestTask.criteria](#attr-dsrequesttaskcriteria) if specified, via [DataSource.combineCriteria](DataSource.md#classmethod-datasourcecombinecriteria).

**Flags**: IR

---
## Attr: DSRequestTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises from DataSource operation.

**Flags**: IR

---
