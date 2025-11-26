# SetTitleTask Documentation

[← Back to API Index](../reference.md)

---

## Class: SetTitleTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Sets the title of a tab, section, window, label, button, form control or facet chart.

For a label, button, window, or chart the [componentId](ComponentTask.md#attr-componenttaskcomponentid) specifies everything necessary to identify the target.

For a tab, section or form control more information is needed. The [componentId](ComponentTask.md#attr-componenttaskcomponentid) identifies the container (i.e. TabSet, SectionStack or DynamicForm) and the individual component is specified as:

*   Tab - [targetTabName](#attr-settitletasktargettabname) references the [Tab.name](Tab.md#attr-tabname).
*   Section - [targetSectionName](#attr-settitletasktargetsectionname) for [SectionStackSection.name](SectionStackSection.md#attr-sectionstacksectionname) or [targetSectionTitle](#attr-settitletasktargetsectiontitle) for [SectionStackSection.title](SectionStackSection.md#attr-sectionstacksectiontitle).
*   FormItem - [targetFieldName](#attr-settitletasktargetfieldname) for [FormItem.name](FormItem.md#attr-formitemname).

### See Also

- [TabSet.setTabTitle](TabSet.md#method-tabsetsettabtitle)
- [SectionStack.setSectionTitle](SectionStack.md#method-sectionstacksetsectiontitle)
- [Window.setTitle](Window.md#method-windowsettitle)
- [FacetChart.title](FacetChart.md#attr-facetcharttitle)
- [Label.setContents](Label.md#method-labelsetcontents)
- [Button.setTitle](Button.md#method-buttonsettitle)
- [FormItem.title](FormItem.md#attr-formitemtitle)

---
## Attr: SetTitleTask.targetFieldName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a DynamicForm, this property specifies the name of the target field to assign new title.

**Flags**: IR

---
## Attr: SetTitleTask.targetSectionName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a SectionStack, this property specifies the name of the target section. Alternately, the target section can be specified by using [SetTitleTask.targetSectionTitle](#attr-settitletasktargetsectiontitle).

**Flags**: IR

---
## Attr: SetTitleTask.title

### Description
Title to assign to component. To assign a dynamic value see [SetTitleTask.textFormula](#attr-settitletasktextformula).

**Flags**: IR

---
## Attr: SetTitleTask.textFormula

### Description
Formula to be used to calculate the component title. Use [SetTitleTask.title](#attr-settitletasktitle) property to assign a static title instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: SetTitleTask.targetTabName

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a TabSet, this property specifies the name or ID of the target tab to assign new title.

**Flags**: IR

---
## Attr: SetTitleTask.targetSectionTitle

### Description
If [componentId](ComponentTask.md#attr-componenttaskcomponentid) targets a SectionStack, this property specifies the title of the target section. Alternately, the target section can be specified by using [SetTitleTask.targetSectionName](#attr-settitletasktargetsectionname).

**Flags**: IR

---
