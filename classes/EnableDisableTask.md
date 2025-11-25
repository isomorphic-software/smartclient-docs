# EnableDisableTask Documentation

[← Back to API Index](../main.md)

---

## Class: EnableDisableTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Enable or disable a button, tab or form field.

For a button the [componentId](ComponentTask.md#attr-componenttaskcomponentid) specifies everything necessary to identify the target.

For a tab or form control more information is needed. The [componentId](ComponentTask.md#attr-componenttaskcomponentid) identifies the container (i.e. TabSet or DynamicForm) and the individual component is specified as:

*   Tab - [targetTabName](#attr-enabledisabletasktargettabname) references the [Tab.name](Tab.md#attr-tabname).
*   FormItem - [targetFieldName](#attr-enabledisabletasktargetfieldname) for [FormItem.name](FormItem.md#attr-formitemname).

### See Also

- [Button.setDisabled](Button.md#method-buttonsetdisabled)
- [TabSet.disableTab](TabSet.md#method-tabsetdisabletab)
- [TabSet.enableTab](TabSet.md#method-tabsetenabletab)
- [FormItem.setDisabled](FormItem.md#method-formitemsetdisabled)

---
## Attr: EnableDisableTask.disable

### Description
Should the target be disabled?

**Flags**: IR

---
## Attr: EnableDisableTask.targetFieldName

### Description
Field to enable/disable.

**Flags**: IR

---
## Attr: EnableDisableTask.targetTabName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a TabSet, this property specifies the name or ID of the target tab to assign new title.

**Flags**: IR

---
