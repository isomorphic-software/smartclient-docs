# SetSectionTitleTask Documentation

[← Back to API Index](../reference.md)

---

## Class: SetSectionTitleTask

*Inherits from:* [ComponentTask](../reference.md#class-componenttask)

### Description
Sets the title of a SectionStack section. The section is identified by specifying either the [SetSectionTitleTask.targetSectionName](#attr-setsectiontitletasktargetsectionname) or [SetSectionTitleTask.targetSectionTitle](#attr-setsectiontitletasktargetsectiontitle).

### See Also

- [SectionStack.setSectionTitle](SectionStack.md#method-sectionstacksetsectiontitle)

---
## Attr: SetSectionTitleTask.textFormula

### Description
Formula to be used to calculate the section title contents. Use [SetSectionTitleTask.title](#attr-setsectiontitletasktitle) property to assign a static title instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: SetSectionTitleTask.targetSectionName

### Description
The name of the target section.

**Flags**: IR

---
## Attr: SetSectionTitleTask.title

### Description
Title to assign to section. To assign a dynamic value see [SetSectionTitleTask.textFormula](#attr-setsectiontitletasktextformula).

**Flags**: IR

---
## Attr: SetSectionTitleTask.targetSectionTitle

### Description
The current title of the target section.

**Flags**: IR

---
