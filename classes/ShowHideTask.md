# ShowHideTask Documentation

[← Back to API Index](../main.md)

---

## Class: ShowHideTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Show or hide a component. When showing, reveals any hidden parents as well.

### See Also

- [Canvas.show](Canvas.md#method-canvasshow)
- [Canvas.hide](Canvas.md#method-canvashide)
- [FormItem.show](FormItem.md#method-formitemshow)
- [FormItem.hide](FormItem.md#method-formitemhide)

---
## Attr: ShowHideTask.targetSectionName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a SectionStack, this property specifies the name of the target section. Alternately, the target section can be specified by using [ShowHideTask.targetSectionTitle](#attr-showhidetasktargetsectiontitle).

**Flags**: IR

---
## Attr: ShowHideTask.showRecursively

### Description
Set to `false` to not show a component's parents.

**Flags**: IR

---
## Attr: ShowHideTask.targetTabName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a TabSet, this property specifies the name or ID of the target tab to assign new title.

**Flags**: IR

---
## Attr: ShowHideTask.targetFieldName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a DynamicForm, this property specifies the name of the target field to assign new title.

**Flags**: IR

---
## Attr: ShowHideTask.moveFocusToTarget

### Description
Should focus be moved to target component when showing?

**Flags**: IR

---
## Attr: ShowHideTask.targetSectionTitle

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a SectionStack, this property specifies the title of the target section. Alternately, the target section can be specified by using [ShowHideTask.targetSectionName](#attr-showhidetasktargetsectionname).

**Flags**: IR

---
## Attr: ShowHideTask.hide

### Description
Should the target form item be hidden?

**Flags**: IR

---
## Attr: ShowHideTask.scrollIntoView

### Description
Set to `false` to prevent scrolling the component into view when showing.

**Flags**: IR

---
