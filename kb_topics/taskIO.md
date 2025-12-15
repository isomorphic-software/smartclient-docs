# Task Input / Output

[← Back to API Index](../reference.md)

---

## KB Topic: Task Input / Output

### Description
Each task has "inputs", which are copied from the [Process state](../classes/Process.md#attr-processstate) when the task is started, and "outputs", which are atomically applied to the Process state when a task is completed.

Tasks can use [Task.inputField](../classes/Task.md#attr-taskinputfield) to specify the field from the Process state that should be used as inputs, and [Task.outputField](../classes/Task.md#attr-taskoutputfield) to specify the field in the Process state that the task should write output.

More complex tasks can take multiple fields from the process state via [Task.inputFieldList](../classes/Task.md#attr-taskinputfieldlist) and write to multiple fields of the process state via [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist). In this case, the task is said to have an "input Record" and/or "output Record", which is a copy of the process state Record with only the fields listed in the `inputFieldList` copied.

When both `inputField` and `inputFieldList` are specified, the inputField is considered the "primary" input field and will be used automatically by various Task subclasses.

An additional option for output is provided in [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression) to write task output directly into another [DataBoundComponent](../reference.md#interface-databoundcomponent) instead of or in addition to the process state. See details below.

#### inputField and inputFieldList examples
`inputData` represents the result of the `inputField` processing and `inputRecord` represents the result of the `inputFieldList`.

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
Consider these input definitions and resulting `inputData` and `inputRecord`:

*   inputField: orderId
    *   inputData: 5
    *   inputRecord: { orderId: 5 }
*   inputField: orderUser.name, inputFieldList: \[ "orderUser" \]
    *   inputData: "Henry Winkle"
    *   inputRecord: { name: "Henry Winkle", orderUser: { name: "Henry Winkle", address: ... }
*   inputField: orderUser
    *   inputData: { name: "Henry Winkle", address: ... }
    *   inputRecord: { orderUser: { name: "Henry Winkle", address: ... } }
*   inputFieldList: \[ "orderUser" \]
    *   inputData: null
    *   inputRecord: { orderUser: { name: "Henry Winkle", address: ... } }

Notice that `inputField` is implicitly added to the `inputRecord` as a field with the same name.

#### Field paths
Specifying an input or output field as a dataPath allows a hierarchical process state to be flattened into the task input or expanded from the task output.

#### Output expressions
An [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression) can be specified to write task output directly into another [DataBoundComponent](../reference.md#interface-databoundcomponent) instead of or in addition to the process state.

An output expression is a String prefixed with "$" followed by the DataBoundComponent ID and optionally followed by a dot-separated field name. When no optional field name is specified the task output is written to the target component using setValues() or setData(). With the optional field name, the task output is written to the target with setFieldValue() or setEditValue(). For a ListGrid the row is either the current edit row or the one selected row.

As an example, consider a DynamicForm with ID of "orderHeader". By specifying an `outputExpression` as "$orderHeader" for a fetch ServiceTask the response record will be assigned directly to the DynamicForm.

### Related

- [ScriptTask.getInputData](../classes/ScriptTask.md#method-scripttaskgetinputdata)
- [ScriptTask.setOutputData](../classes/ScriptTask.md#method-scripttasksetoutputdata)
- [ScriptTask.getInputRecord](../classes/ScriptTask.md#method-scripttaskgetinputrecord)
- [ScriptTask.setOutputRecord](../classes/ScriptTask.md#method-scripttasksetoutputrecord)
- [Task.inputField](../classes/Task.md#attr-taskinputfield)
- [Task.inputFieldList](../classes/Task.md#attr-taskinputfieldlist)
- [Task.outputField](../classes/Task.md#attr-taskoutputfield)
- [Task.outputFieldList](../classes/Task.md#attr-taskoutputfieldlist)
- [Task.outputExpression](../classes/Task.md#attr-taskoutputexpression)
- [ServiceTask.criteria](../classes/ServiceTask.md#attr-servicetaskcriteria)
- [ServiceTask.outputField](../classes/ServiceTask.md#attr-servicetaskoutputfield)
- [ServiceTask.outputFieldList](../classes/ServiceTask.md#attr-servicetaskoutputfieldlist)

---
