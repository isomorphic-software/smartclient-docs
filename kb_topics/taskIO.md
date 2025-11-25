# Task Input / Output

[← Back to API Index](../main.md)

---

## KB Topic: Task Input / Output

### Description
#### Input
Tasks require "inputs" to do their work, just like a method call. For example, [GridFetchDataTask](../classes/GridFetchDataTask.md#class-gridfetchdatatask) requires [criteria](../classes/GridFetchDataTask.md#attr-gridfetchdatataskcriteria).

For built-in tasks, you can typically use [TaskInputExpressions](../main_2.md#type-taskinputexpression) to declare that the inputs of a task are drawn from [Process.state](../classes/Process.md#attr-processstate), the [output](../classes/Task.md#method-tasksetoutput) of a previous task in the process, or from global context such as [ruleScope](../classes/Process.md#attr-processrulescope). See the docs for each task for details.

If you are implementing your own task and want to support `TaskInputExpressions` for the data required by your task, use +link{task.getExpressionValue(_expression_)}.

You can also use the property [Task.inputs](../classes/Task.md#attr-taskinputs) to automatically support `TaskInputExpressions`: call [getInputRecord()](../classes/Task.md#method-taskgetinputrecord) to get the values of the provided expressions.

#### Output
A task can call [Task.setOutput](../classes/Task.md#method-tasksetoutput) to provide outputs which other tasks can use via `TaskInputExpressions` or programmatically via APIs such as [Process.getLastTaskOutput](../classes/Process.md#method-processgetlasttaskoutput).

Using the property [Task.outputField](../classes/Task.md#attr-taskoutputfield) and/or [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist) allows certain properties of the output, from setOutput(), to be written into the [Process.state](../classes/Process.md#attr-processstate). Use [Task.outputField](../classes/Task.md#attr-taskoutputfield) to specify the field in the process state where the task output should be written. Or, for more complex tasks, use [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist) to specify multiple fields.

You can also use the property [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression) to write task output directly into a [DataBoundComponent](../main.md#interface-databoundcomponent) instead of or in addition to the process state.

An output expression is a String prefixed with "$" followed by the DataBoundComponent ID and optionally followed by a dot-separated field name. When no optional field name is specified, the task output is written to the target component using setValues() or setData(). With the optional field name, the task output is written to the target with setFieldValue() or setEditValue(). For a ListGrid the row is either the current edit row or the one selected row.

As an example, consider a DynamicForm with ID of "orderHeader". By specifying an `outputExpression` as "$orderHeader" for a fetch DSRequestTask the response record will be assigned directly to the DynamicForm.

#### Inputs examples
`inputRecord` represents the result of the `inputs` extracted from the process state.

If the [Process.state](../classes/Process.md#attr-processstate) represented in JSON is:

```
 {
    orderId:5,
    orderItems: [
       {name:"Pencils", quantity:3, itemId:2344}
    ],
    orderUser: { name:"Henry Winkle", address:"...", ... }
 }
 
```
Consider these input definitions and resulting `inputRecord`:

*   inputs: "orderId"
    *   inputRecord: { orderId: 5 }
*   inputs: \[ "orderUser.name", "orderUser" \]
    *   inputRecord: { name: "Henry Winkle", orderUser: { name: "Henry Winkle", address: ... }
*   inputs: "orderUser"
    *   inputRecord: { name: "Henry Winkle", address: ... }
*   inputs: \[ "orderUser" \]
    *   inputRecord: { orderUser: { name: "Henry Winkle", address: ... } }

### Related

- [Task.getInputRecord](../classes/Task.md#method-taskgetinputrecord)
- [Task.getExpressionValue](../classes/Task.md#method-taskgetexpressionvalue)
- [ScriptTask.setOutput](../classes/ScriptTask.md#method-scripttasksetoutput)
- [Task.inputs](../classes/Task.md#attr-taskinputs)
- [Task.inputFieldList](../classes/Task.md#attr-taskinputfieldlist)
- [Task.outputField](../classes/Task.md#attr-taskoutputfield)
- [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist)
- [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression)
- [DSRequestTask.criteria](../classes/DSRequestTask.md#attr-dsrequesttaskcriteria)
- [DSRequestTask.outputField](../classes/DSRequestTask.md#attr-dsrequesttaskoutputfield)
- [DSRequestTask.outputFieldList](../classes/DSRequestTask.md#attr-dsrequesttaskoutputfieldlist)

---
