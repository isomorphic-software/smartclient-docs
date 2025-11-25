# RibbonBar Documentation

[← Back to API Index](../main.md)

---

## Class: RibbonBar

*Inherits from:* [ToolStrip](ToolStrip.md#class-toolstrip)

### Description
A [ToolStrip-based](ToolStrip.md#class-toolstrip) class for showing [groups](RibbonGroup.md#class-ribbongroup) of [RibbonButtons](RibbonButton.md#class-ribbonbutton)s.

---
## Attr: RibbonBar.groupTitleOrientation

### Description
If set, this attribute affects the orientation of the titles in [RibbonGroups](RibbonGroup.md#class-ribbongroup) in this `RibbonBar`. You can override this at the [individual RibbonGroup](RibbonGroup.md#attr-ribbongrouptitleorientation) level.

### Groups

- ribbonGroup

**Flags**: IR

---
## Attr: RibbonBar.showGroupTitle

### Description
If set, this attribute affects whether [RibbonGroups](RibbonGroup.md#class-ribbongroup) in this `RibbonBar` show their header control. You can override this at the [individual RibbonGroup](RibbonGroup.md#method-ribbongroupsetshowtitle) level.

### Groups

- ribbonGroup

**Flags**: IR

---
## Attr: RibbonBar.groupTitleAlign

### Description
If set, this attribute affects the alignment of the titles in [RibbonGroups](RibbonGroup.md#class-ribbongroup) in this `RibbonBar`. You can override this at the [individual RibbonGroup](RibbonGroup.md#attr-ribbongrouptitlealign) level.

### Groups

- ribbonGroup

**Flags**: IR

---
## Method: RibbonBar.addGroup

### Description
Add a new group to this RibbonBar. You can either create your group externally and pass it in, or you can pass a properties block from which to automatically construct it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| group | [RibbonGroup](#type-ribbongroup) | false | — | the new group to add to this ribbon |
| position | [Integer](../main_2.md#type-integer) | true | — | the index at which to insert the new group |

### Groups

- ribbonGroup

---
