# AddScreenTask Documentation

[← Back to API Index](../reference.md)

---

## Class: AddScreenTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Adds a new screen instance to a Layout, as a new Tab in a TabSet or as a new Section in a SectionStack. When the target is a TabSet or SectionStack, a static [AddScreenTask.title](#attr-addscreentasktitle) or dynamic [AddScreenTask.titleFormula](#attr-addscreentasktitleformula) can be assigned for the new Tab or Section.

The new screen's [dataContext](Canvas.md#attr-canvasdatacontext) can be configured with [dataContextBinding](#attr-addscreentaskdatacontextbinding) evaluated in the scope of this task.

---
## Attr: AddScreenTask.screenName

### Description
Name of screen to be added.

**Flags**: IR

---
## Attr: AddScreenTask.title

### Description
Title of new SectionStackSection or TabSet when [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a SectionStack or TabSet. To use a dynamic title see [AddScreenTask.titleFormula](#attr-addscreentasktitleformula).

**Flags**: IR

---
## Attr: AddScreenTask.dataContextBinding

### Description
A [DataContextBinding](../reference.md#object-datacontextbinding) to be applied to the created screen via [Canvas.setDataContext](Canvas.md#method-canvassetdatacontext).

**Flags**: IR

---
## Attr: AddScreenTask.titleFormula

### Description
Formula to be used to calculate the title contents. Use [AddScreenTask.title](#attr-addscreentasktitle) property to assign a static title instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: AddScreenTask.canClose

### Description
Can the created SectionStackSection or TabSet be closed by the user?

**Flags**: IR

---
