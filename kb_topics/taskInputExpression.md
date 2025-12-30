# Task Input Expressions

[← Back to API Index](../reference.md)

---

## KB Topic: Task Input Expressions

### Description
In some tasks, the input to the task needs to be passed to a service being called by the task, to a user-visible form, or other consumers of the input data. A TaskInputExpression can be used to do this declaratively.

A TaskInputExpression is a String prefixed with "$input", "$inputRecord", "$last", or "$ruleScope" followed by an optional dot-separated hierarchical path, which can specify either an atomic data value (String, Number) or Record from the input data. For example, if the [Process.state](../classes/Process.md#attr-processstate) represented in JSON were:

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

The other two sources of input are "$last" and "$ruleScope". The former references the contents of the [transient state](../classes/Process.md#attr-processstate). Finally, "$ruleScope" can be used to pull values from a [ruleScope](../classes/Canvas.md#attr-canvasrulescope) when configured in [Process.ruleScope](../classes/Process.md#attr-processrulescope).

*   $last is the full output of the previous task executed in the process
*   $last\[service\].property or $last\[ServiceTask\].property references the last "ServiceTask" output in the "property" field
*   $ruleScope.property references the ruleScope "property" field

#### Transient state outputs
The transient state outputs of each task type referenced by "$last" above:

*   **DecisionGateway**: the output from the _previous_ task (passed through).
*   **ScriptTask**: the result of [execute()](../classes/ScriptTask.md#method-scripttaskexecute) or, for an asynchronous task, the value passed to [setOutputRecord()](../classes/ScriptTask.md#method-scripttasksetoutputrecord) or [setOutputData()](../classes/ScriptTask.md#method-scripttasksetoutputdata).
*   **ServiceTask**: the contents of dsResponse.data.
*   **StateTask**: the value assigned to the outputField.
*   **UserTask**: the values of the targetForm or targetVM when the task completes.
*   **XORGateway**: the output from the _previous_ task (passed through).

---
