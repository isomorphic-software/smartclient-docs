# ComponentTask Documentation

[← Back to API Index](../reference.md)

---

## Class: ComponentTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Base class for tasks that target SmartClient UI-specific operations.

Note: This task is not for direct use - use one of the subclasses instead.

---
## Attr: ComponentTask.unsupportedComponentMessage

### Description
The default message to be reported with [getInvalidTaskMessage()](ProcessElement.md#method-processelementgetinvalidtaskmessage) when a target component type is not supported for the task.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ComponentTask.componentBaseClass

### Description
Base class of components that this task targets. The [ComponentTask.componentId](#attr-componenttaskcomponentid) must be an instance of one of the classes.

**Flags**: IR

---
## Attr: ComponentTask.componentRequiresDataSource

### Description
Must target components of this task have a DataSource?

**Flags**: IR

---
## Attr: ComponentTask.targetBaseClass

### Description
Base class of components and any required or optional scope that this task targets. The [ComponentTask.componentId](#attr-componenttaskcomponentid) may not be an instance itself but when combined with the additional scope (targetFieldName, targetSectionName, ...) the actual target must be an instance of one of the classes.

This can be used by an editor to limit or verify the user's selection.

**Flags**: IR

---
## Attr: ComponentTask.componentId

### Description
ID of component targeted by this task.

**Flags**: IR

---
## Method: ComponentTask.getTargetComponent

### Description
Returns the actual component specified by [ComponentTask.componentId](#attr-componenttaskcomponentid) for this task. Unless `skipValidation` is true, the component type is validated against [ComponentTask.componentBaseClass](#attr-componenttaskcomponentbaseclass) and only returned if it matches. Null is returned otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the process that is handling the workflow |
| skipValidation | [Boolean](#type-boolean) | true | — | skip validation against componentBaseClass? |

---
