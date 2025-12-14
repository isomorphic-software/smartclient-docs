# UserTask Documentation

[← Back to API Index](../reference.md)

---

## Class: UserTask

*Inherits from:* [Task](Task.md#class-task)

### Description
A task that involves showing a user interface to the end user allowing the user to view and input data and press a button (or do some other UI gesture) to complete the task.

A UserTask takes the following steps:

*   Optionally show() or otherwise make visible the [targetView](#attr-usertasktargetview) or [inlineView](#attr-usertaskinlineview)
*   Provide values to either a [DynamicForm](DynamicForm.md#class-dynamicform) designated as the [targetForm](#attr-usertasktargetform) or to a [ValuesManager](ValuesManager.md#class-valuesmanager) designated as the [targetVM](#attr-usertasktargetvm), via [setValues()](ValuesManager.md#method-valuesmanagersetvalues)
*   Waits for notification of completion or cancellation. The UserTask is notified of completion if a [SubmitItem](../reference.md#class-submititem) is pressed in either the `targetForm` or any form that is a member of the `targetVM`. Likewise a [CancelItem](../reference.md#class-cancelitem) triggers cancellation. Direct calls to [DynamicForm.cancelEditing](DynamicForm.md#method-dynamicformcancelediting) or [DynamicForm.completeEditing](DynamicForm.md#method-dynamicformcompleteediting) achieve the same result.
*   if cancellation occurs, the process continues to the [cancelElement](#attr-usertaskcancelelement) if specified. Otherwise the workflow is immediately finished.
*   if completion occurs, values are retrieved from the form or valuesManager and applied to the process state based on [outputField](Task.md#attr-taskoutputfield), [outputFieldList](Task.md#attr-taskoutputfieldlist) or [inputField](Task.md#attr-taskinputfield), in that order.

---
## Attr: UserTask.previousElement

### Description
Previous workflow [sequence](Process.md#attr-processsequences) or [element](Process.md#attr-processelements) that is helpful for wizards. This element will be executed if [UserTask.goToPrevious](#method-usertaskgotoprevious) method of userTask will be invoked. You can get userTask for attached form by using [userTask](DynamicForm.md#attr-dynamicformusertask) property.

**Flags**: IR

---
## Attr: UserTask.cancelElement

### Description
Next element to proceed to if the task is cancelled because the [UserTask.targetForm](#attr-usertasktargetform) or [UserTask.targetVM](#attr-usertasktargetvm) had `cancelEditing()` called on it.

if no value is provided the workflow immediately completes.

**Flags**: IR

---
## Attr: UserTask.targetView

### Description
Widget that should be shown to allow user input. If this widget is a DynamicForm, it will also be automatically used as the [UserTask.targetForm](#attr-usertasktargetform) unless either `targetForm` or [UserTask.targetVM](#attr-usertasktargetvm) is set.

`UserTask` will automatically handle various scenarios of the `targetView` not currently visible or draw()n, according to the following rules:

*   if the view itself is marked hidden, it will be show()n
*   if the view is inside a hidden parent, the parent will be show()n
*   if the view is the [Tab.pane](Tab.md#attr-tabpane) of a tab in a TabSet, the tab will be selected
*   if the view is listed in [SectionStackSection.items](SectionStackSection.md#attr-sectionstacksectionitems) for a which is either collapsed or hidden section, the section will be shown and expanded
*   if the view is listed in [Window.items](Window.md#attr-windowitems) for a Window, the Window will be shown
*   if any of these conditions apply to any parent of the targetView, the rules will be applied to that parent as well. For example, the targetView is in a collapsed section inside a tab which is not selected, the section will be expanded **and** the tab selected

### See Also

- [UserTask.inlineView](#attr-usertaskinlineview)

**Flags**: IR

---
## Attr: UserTask.targetForm

### Description
DynamicForm that should be populated with data and that should provide the data for the task outputs. If [UserTask.targetView](#attr-usertasktargetview) is a DynamicForm and would also be the targetForm, the targetForm attribute can be left unset.

Use [UserTask.targetVM](#attr-usertasktargetvm) to use a [ValuesManager](ValuesManager.md#class-valuesmanager) instead.

**Flags**: IR

---
## Attr: UserTask.inlineView

### Description
An inline definition of the form. Can be used in place of [UserTask.targetView](#attr-usertasktargetview) to encode form directly in process xml.

**Flags**: IRW

---
## Attr: UserTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)?

See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state outputs.

Note that this property does not affect the task at all but is an indicator to the user and to the workflow editor of the behavior of the task as coded (See [Process.passThruTaskOutput](Process.md#method-processpassthrutaskoutput)).

**Flags**: IR

---
## Attr: UserTask.saveToServer

### Description
If saveToServer is set then the associated form ([UserTask.targetForm](#attr-usertasktargetform)) will perform the normal [DynamicForm.submit](DynamicForm.md#method-dynamicformsubmit) actions when submitted (typically from a [SubmitItem](../reference.md#class-submititem)). By default the form submit action is bypassed.

**Flags**: IR

---
## Attr: UserTask.wizard

### Description
If wizard is set then associated form will be hidden after user goes to next or prev step of current workflow.

**Flags**: IR

---
## Attr: UserTask.targetVM

### Description
Optional ValuesManager which will receive task inputs and provide task outputs.

Use [UserTask.targetForm](#attr-usertasktargetform) instead if you want to use a DynamicForm.

**Flags**: IR

---
## Method: UserTask.goToPrevious

### Description
Set [UserTask.previousElement](#attr-usertaskpreviouselement) as next element of workflow. This method could be used to create wizard-like UI behavior.

---
## Method: UserTask.completeEditing

### Description
Finish editing and store edited values in [process state](Process.md#attr-processstate).

---
## Method: UserTask.cancelEditing

### Description
Revert any changes made in a form and finish this userTask execution. [UserTask.cancelElement](#attr-usertaskcancelelement) will be proceed as the next element of current process.

---
