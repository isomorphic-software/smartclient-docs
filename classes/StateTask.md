# StateTask Documentation

[← Back to API Index](../reference.md)

---

## Class: StateTask

*Inherits from:* [Task](Task.md#class-task)

### Description
StateTask can either copy fields of [Process.state](Process.md#attr-processstate) to other fields, or apply hardcoded values to [Process.state](Process.md#attr-processstate) via [StateTask.value](#attr-statetaskvalue).

Some examples:

*   inputField: "a", outputField: "b" - copies "a" to "b"
*   inputField: "a", outputField: "b", type: "integer" - copies "a" to "b" converting "a" to an integer
*   inputFieldList: \["a","b"\], outputField: \["c","d"\] - copies "a" and "b" to "c" and "d" respectively.

---
## Attr: StateTask.value

### Description
If a stateTask does not declare [inputField](Task.md#attr-taskinputfield), it must declare a `value` which should be assigned to the output field.

See [StateTask.type](#attr-statetasktype) for how the value is interpreted.

**Flags**: IR

---
## Attr: StateTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises, such as the output data not being convertible to the target [StateTask.type](#attr-statetasktype).

**Flags**: IR

---
## Attr: StateTask.type

### Description
Type of the value for stateTask.outputField.

This can be used in conjunction with [StateTask.value](#attr-statetaskvalue) to declare the type of the value, or can be used to convert the type of the [inputField](Task.md#attr-taskinputfield) to the declared type.

If no type is declared, the value from an inputField is unchanged or provided via a call to setValue() is unchanged.

A value specified for `stateTask.value` via an attribute in [componentXML](../kb_topics/componentXML.md#kb-topic-component-xml) (see [Process.loadProcess](Process.md#classmethod-processloadprocess)) is treated as a boolean if it is the exact string "true" or "false", treated as a "decimal" or "integer" if it parsable as a valid number, otherwise treated as a String. If these heuristics don't work in your case, just declare the type explicitly via `stateTask.type`.

A value of "record" type or "array" type can be declared in Component XML using the same formats allowed for [valueMap](DataSourceField.md#attr-datasourcefieldvaluemap). Each array value or record attribute value undergoes the same heuristics as for [StateTask.value](#attr-statetaskvalue) declared as an attribute.

[StateTask.type](#attr-statetasktype) is invalid to use with multiple outputFields.

**Flags**: IR

---
## Attr: StateTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)? See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state.

**Flags**: IR

---
## Attr: StateTask.outputExpression

### Description
Not applicable to a StateTask.

**Flags**: IR

---
