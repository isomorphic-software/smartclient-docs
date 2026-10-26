# Task Input / Output

[← Back to API Index](../reference.md)

---

## KB Topic: Task Input / Output

### Description
#### Input
Tasks require "inputs" to do their work, just like a method call. For example, [GridFetchDataTask](../classes/GridFetchDataTask.md#class-gridfetchdatatask) requires [criteria](../classes/GridFetchDataTask.md#attr-gridfetchdatataskcriteria).

For built-in tasks, you can typically use [TaskInputExpressions](../reference_2.md#type-taskinputexpression) to declare that the inputs of a task are drawn from [Process.state](../classes/Process.md#attr-processstate), the [output](../classes/Task.md#method-tasksetoutput) of a previous task in the process, or from global context such as [ruleScope](../classes/Process.md#attr-processrulescope). See the docs for each task for details.

If you are implementing your own task and want to support `TaskInputExpressions` for the data required by your task, use [Task.getExpressionValue](../classes/Task.md#method-taskgetexpressionvalue), or [Task.getCriteriaExpressionValue](../classes/Task.md#method-taskgetcriteriaexpressionvalue) for criteria. [Task.getState](../classes/Task.md#method-taskgetstate) reads a value from the process state directly.

You can also use the property [Task.inputs](../classes/Task.md#attr-taskinputs) to automatically support `TaskInputExpressions`: call [getInputRecord()](../classes/Task.md#method-taskgetinputrecord) to get the values of the provided expressions.

The input record is built from the task's declared inputs as follows:

*   an Array [inputs](../classes/Task.md#attr-taskinputs) (or the deprecated [Task.inputFieldList](../classes/Task.md#attr-taskinputfieldlist)) stores each value under the last segment of its path;
*   an Object `inputs` sets each key, as a [StatePath](../reference_2.md#type-statepath), to the value of its expression;
*   a single String `inputs` becomes `$input`. A Record value supplies the fields of the input record, merged with any `inputFieldList` entries; any other value is stored under the last segment of the path.
*   with nothing declared, the input record is a shallow copy of the whole [Process.state](../classes/Process.md#attr-processstate). Top-level fields may be changed in the copy, but nested objects are shared with the process state.

In a [TaskInputExpression](../reference_2.md#type-taskinputexpression), `$input` refers to the task's input: the input record, or, when `inputs` is a single String, the value that String refers to (`null` if it is missing).

[DSRequestTask](../classes/DSRequestTask.md#class-dsrequesttask) resolves `$input` the same way in its [criteria](../classes/DSRequestTask.md#attr-dsrequesttaskcriteria) and [values](../classes/DSRequestTask.md#attr-dsrequesttaskvalues), but only declared inputs are used as its implicit request data: a task with no `inputs`, `criteria` or `values` sends no data. [DecisionTask](../classes/DecisionTask.md#class-decisiontask) and [MultiDecisionTask](../classes/MultiDecisionTask.md#class-multidecisiontask) have no `inputs`; in their criteria, `$input` refers to the whole process state.

#### Output
A task can call [Task.setOutput](../classes/Task.md#method-tasksetoutput) to provide outputs which other tasks can use via `TaskInputExpressions` or programmatically via APIs such as [Process.getLastTaskOutput](../classes/Process.md#method-processgetlasttaskoutput).

Using the property [Task.outputField](../classes/Task.md#attr-taskoutputfield) and/or [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist) allows certain properties of the output, from setOutput(), to be written into the [Process.state](../classes/Process.md#attr-processstate). Use [Task.outputField](../classes/Task.md#attr-taskoutputfield) to specify the field in the process state where the task output should be written. Or, for more complex tasks, use [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist) to specify multiple fields.

To store the whole output as-is, set [ProcessElement.bindOutput](../classes/ProcessElement.md#attr-processelementbindoutput) to a [StatePath](../reference_2.md#type-statepath): whenever the task's output is recorded - including the output a pass-through task forwards from the previous task - it is also written to that path in the process state. For example, `bindOutput: "lastOrder"` on a fetch DSRequestTask keeps the fetched record in `process.state.lastOrder`, and `bindOutput: "orders[]"` appends each output to an Array. Unlike `outputField`, no properties are picked out of the output.

You can also use the property [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression) to write task output directly into a [DataBoundComponent](../reference.md#interface-databoundcomponent) instead of or in addition to the process state.

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
*   inputs: { "customer.name": "orderUser.name", "quantity": 1 }
    *   inputRecord: { customer: { name: "Henry Winkle" }, quantity: 1 }
*   no inputs
    *   inputRecord: { orderId: 5, orderItems: \[ ... \], orderUser: { ... } }

### Related

- [Task.getInputRecord](../classes/Task.md#method-taskgetinputrecord)
- [Task.getExpressionValue](../classes/Task.md#method-taskgetexpressionvalue)
- [Task.getCriteriaExpressionValue](../classes/Task.md#method-taskgetcriteriaexpressionvalue)
- [Process.getExpressionValue](../classes/Process.md#method-processgetexpressionvalue)
- [ScriptTask.setOutput](../classes/ScriptTask.md#method-scripttasksetoutput)
- [Task.inputs](../classes/Task.md#attr-taskinputs)
- [Task.inputFieldList](../classes/Task.md#attr-taskinputfieldlist)
- [Task.outputField](../classes/Task.md#attr-taskoutputfield)
- [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist)
- [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression)
- [DSRequestTask.criteria](../classes/DSRequestTask.md#attr-dsrequesttaskcriteria)
- [DSRequestTask.outputField](../classes/DSRequestTask.md#attr-dsrequesttaskoutputfield)
- [DSRequestTask.outputFieldList](../classes/DSRequestTask.md#attr-dsrequesttaskoutputfieldlist)
- [HumanTask.inputs](../classes/HumanTask.md#attr-humantaskinputs)
- [HumanTask.outputs](../classes/HumanTask.md#attr-humantaskoutputs)
- [DefaultOperationTask.outputField](../classes/DefaultOperationTask.md#attr-defaultoperationtaskoutputfield)

---
