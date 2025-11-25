# GetPropertiesTask Documentation

[← Back to API Index](../main.md)

---

## Class: GetPropertiesTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Gets the value properties from a component and makes them available within the workflow as the [last task output](../main_2.md#type-taskinputexpression). Using [bindOutput](ProcessElement.md#attr-processelementbindoutput), these values can also be placed into the [process state](Process.md#attr-processstate).

For a canvas the [componentId](ComponentTask.md#attr-componenttaskcomponentid) specifies everything necessary to identify the target. For a form control more information is needed. The [componentId](ComponentTask.md#attr-componenttaskcomponentid) identifies the container (i.e. DynamicForm) and the individual field is specified as [targetFieldName](#attr-getpropertiestasktargetfieldname).

The next task might be a save operation on a DataSource, or SetPropertiesTask to copy settings from one component to another.

GetPropertiesTask _is an advanced and rarely used task_. If you need a component property to be dynamic, you can configure that property as a [Dynamic Property](Class.md#attr-classdynamicproperties) without the need for a Workflow. _Dynamic Properties_ created this way automatically update as your users make changes.

---
## Attr: GetPropertiesTask.targetFieldName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a DynamicForm, this property specifies the name of the target field.

**Flags**: IR

---
## Attr: GetPropertiesTask.properties

### Description
Properties to be retrieved from [componentId](ComponentTask.md#attr-componenttaskcomponentid).

**Flags**: IR

---
