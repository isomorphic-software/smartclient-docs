# FormSaveDataTask Documentation

[← Back to API Index](../reference.md)

---

## Class: FormSaveDataTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Saves changes made in a form (validates first).

### See Also

- [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata)

---
## Attr: FormSaveDataTask.unboundNotifyMessage

### Description
The default message to be shown when a target form is not bound to a DataSource.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FormSaveDataTask.clearAfterSave

### Description
The form will be [cleared](DynamicForm.md#method-dynamicformclearvalues) after a successful save unless this property is set to `false`.

**Flags**: IR

---
## Attr: FormSaveDataTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)?

See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state outputs.

Note that this property does not affect the task at all but is an indicator to the user and to the workflow editor of the behavior of the task as coded (See [Process.passThruTaskOutput](Process.md#method-processpassthrutaskoutput)).

**Flags**: IR

---
## Attr: FormSaveDataTask.boundNotifyMessage

### Description
The default message to be shown when a target form is bound to a DataSource.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FormSaveDataTask.requestProperties

### Description
Additional properties to set on the DSRequest that will be issued to perform save.

Note that `willHandleError` will always be set `true`.

**Flags**: IR

---
## Attr: FormSaveDataTask.showNotification

### Description
Should a notification message (defined as notifyMessage) be shown after save completes successfully?

**Flags**: IR

---
## Attr: FormSaveDataTask.notifyType

### Description
NotifyType for [FormSaveDataTask.notifyMessage](#attr-formsavedatatasknotifymessage).

**Flags**: IR

---
## Attr: FormSaveDataTask.notifyMessage

### Description
The message to be shown when save completes if [FormSaveDataTask.showNotification](#attr-formsavedatataskshownotification) is set. If no message is configured a default message is used based on the whether the form is bound to a DataSource or not: [FormSaveDataTask.boundNotifyMessage](#attr-formsavedatataskboundnotifymessage) or [FormSaveDataTask.unboundNotifyMessage](#attr-formsavedatataskunboundnotifymessage).

**Flags**: IR

---
## Attr: FormSaveDataTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises from operation.

**Flags**: IR

---
## Attr: FormSaveDataTask.notifyPosition

### Description
Where to show the message, specified as an edge ("T", "B", "R", "L") similar to [Canvas.snapTo](Canvas.md#attr-canvassnapto), or "C" for center. The message will be shown at the center of the edge specified (or the very center for "C").

**Flags**: IR

---
