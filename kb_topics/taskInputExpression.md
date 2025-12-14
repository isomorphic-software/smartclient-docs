# Task Input Expressions

[← Back to API Index](../reference.md)

---

## KB Topic: Task Input Expressions

### Description
In some tasks, the input to the task needs to be passed to a service being called by the task, to a user-visible form, or other consumers of the input data. A TaskInputExpression can be used to do this declaratively.

A TaskInputExpression is a String prefixed with "$input", "$inputRecord", "$ruleScope", "$state" or "$last" followed by an optional dot-separated hierarchical path, which can specify either an atomic data value (String, Number) or Record from the input data. For example, if the [Process.state](../classes/Process.md#attr-processstate) represented in JSON were:

```
 {
    orderId:5,
    orderItems: [
       {name:"Pencils", quantity:3, itemId:2344}
    ],
    orderUser: { name:"Henry Winkle", address:"...", ... }
 }
 
```
.. and a task specified an `inputField` of "orderId" and an inputFieldList of "orderItems","orderUser", then:

*   $input is the value 5
*   $inputRecord.orderUser.name is "Henry Winkle"
*   $inputRecord.orderItems\[0\] is the first orderItems Record ({name:"Pencils", ... })

"$ruleScope" can be used to pull values from a [ruleScope](../classes/Canvas.md#attr-canvasrulescope) [ruleContext](../classes/Canvas.md#method-canvasgetrulecontext) when configured in [Process.ruleScope](../classes/Process.md#attr-processrulescope).

*   $ruleScope.property references the ruleContext "property" field

The other two sources of input are "$state" and "$last". The former references the contents of the [Process.state](../classes/Process.md#attr-processstate) and the latter the [transient state](../classes/Process.md#attr-processstate).

*   $state is the full contents of the process state
*   $state.orderId is the "orderId" field of the process state (5 from the example above)
*   $last is the full output of the previous task executed in the process
*   $last.property is the "property" field of the previous task executed in the process
*   $last\[service\].property or $last\[ServiceTask\].property references the last "ServiceTask" output in the "property" field
*   $ruleScope.property references the ruleScope "property" field

#### Transient state outputs
Most tasks pass the output from the _previous_ task as their output (i.e. passed through) making it easy to refer to earlier output without referencing the task type. Tasks that work with records or interact with the user, however, typically provide task-specific output as detailed below:

*   **ServiceTask**: the contents of dsResponse.data.
*   **ScriptTask**: the result of [execute()](../classes/ScriptTask.md#method-scripttaskexecute) or, for an asynchronous task, the value passed to [setOutputRecord()](../classes/ScriptTask.md#method-scripttasksetoutputrecord) or [setOutputData()](../classes/ScriptTask.md#method-scripttasksetoutputdata).
*   **StateTask**: the value assigned to the outputField.
*   **UserTask**: the values of the targetForm or targetVM when the task completes.
*   **AskForValueTask**: an object with "value" and "canceled" properties.
*   **FetchRelatedDataTask**: the first fetched record.
*   **GridFetchDataTask**: the contents of dsResponse.data.
*   **GridTransferSelectedTask**: the first transfered record.
*   **GridSelectRecordsTask**: on a select, the set of newly selected records, even if other records are also selected. On a deselect, the entire set of de-selected records.
*   **FetchRelatedDataTask**: the first fetched related record.
*   **FormSaveDataTask**: an object with "valuesValid" and "errors" properties.
*   **FormValidateValuesTask**: an object with "valuesValid" and "errors" properties.
*   **GetPropertiesTask**: an object with selected properties and values retrieved.

---
