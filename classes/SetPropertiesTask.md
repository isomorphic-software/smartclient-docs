# SetPropertiesTask Documentation

[← Back to API Index](../reference.md)

---

## Class: SetPropertiesTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Gets the value properties from a component and makes them available within the workflow as the [last task output](../reference_2.md#type-taskinputexpression).

For a canvas the [componentId](ComponentTask.md#attr-componenttaskcomponentid) specifies everything necessary to identify the target. For a form control more information is needed. The [componentId](ComponentTask.md#attr-componenttaskcomponentid) identifies the container (i.e. DynamicForm) and the individual field is specified as [targetFieldName](#attr-setpropertiestasktargetfieldname).

SetPropertiesTask _is an advanced and rarely used task_. If you need a component property to be dynamic, you can configure that property as a [Dynamic Property](Class.md#attr-classdynamicproperties) without the need for a Workflow. _Dynamic Properties_ created this way automatically update as your users make changes.

---
## Attr: SetPropertiesTask.properties

### Description
Properties and associated values to be set on [componentId](ComponentTask.md#attr-componenttaskcomponentid).

**Flags**: IR

---
## Attr: SetPropertiesTask.targetFieldName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a DynamicForm, this property optionally specifies the name of the target field.

**Flags**: IR

---
