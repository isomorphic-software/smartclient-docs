# ToolStripGroup Documentation

[← Back to API Index](../reference.md)

---

## Class: ToolStripGroup

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A widget that groups other controls for use in [tool-strips](ToolStrip.md#class-toolstrip).

---
## Attr: ToolStripGroup.titleProperties

### Description
AutoChild properties for fine customization of the [title label](#attr-toolstripgrouplabel).

**Deprecated**

**Flags**: IRW

---
## Attr: ToolStripGroup.columnLayout

### Description
AutoChild VLayouts created automatically by groups. Each manages a single column of child controls in the group. Child controls that support `rowSpan` may specify it in order to occupy more than one row in a single column. See [numRows](#attr-toolstripgroupnumrows) for related information.

**Flags**: IR

---
## Attr: ToolStripGroup.label

### Description
AutoChild [Label](Label.md#class-label) used to display the [title text](#attr-toolstripgrouptitle) for this group.

Can be customized via the standard [AutoChild](../reference.md#type-autochild) pattern, and various convenience APIs exist for configuring it after initial draw: see [setShowTitle](#method-toolstripgroupsetshowtitle), [setTitle](#method-toolstripgroupsettitle), [setTitleAlign](#method-toolstripgroupsettitlealign), [setTitleHeight](#method-toolstripgroupsettitleheight), [setTitleOrientation](#method-toolstripgroupsettitleorientation) and [setTitleStyle](#method-toolstripgroupsettitlestyle).

**Flags**: IR

---
## Attr: ToolStripGroup.styleName

### Description
CSS class applied to this ToolStripGroup.

**Flags**: IRW

---
## Attr: ToolStripGroup.labelLayout

### Description
HLayout autoChild that houses the [label](#attr-toolstripgrouplabel) in which the [title text](#attr-toolstripgrouptitle) is displayed.

This can be customized via the standard [AutoChild](../reference.md#type-autochild) pattern.

**Flags**: IR

---
## Attr: ToolStripGroup.titleOrientation

### Description
Controls the [vertical orientation](#attr-toolstripgrouptitleorientation) of this group's [title label](#attr-toolstripgrouplabel). Setting this attribute overrides the default specified by [groupTitleOrientation](ToolStrip.md#attr-toolstripgrouptitlealign) on the containing [ToolStrip](ToolStrip.md#class-toolstrip).

**Flags**: IRW

---
## Attr: ToolStripGroup.labelConstructor

### Description
SmartClient class for the [title label](#attr-toolstripgrouplabel) AutoChild.

**Flags**: IRA

---
## Attr: ToolStripGroup.numRows

### Description
The number of rows of controls to display in each column. Each control will take one row in a [columnLayout](#attr-toolstripgroupcolumnlayout) by default, but those that support the feature may specify `rowSpan` to override that.

Note that settings like this, which affect the group's layout, are not applied directly if changed at runtime - a call to [reflowControls](#method-toolstripgroupreflowcontrols) will force the group to reflow.

**Flags**: IRW

---
## Attr: ToolStripGroup.title

### Description
The title text to display in this group's [title label](#attr-toolstripgrouplabel).

**Flags**: IRW

---
## Attr: ToolStripGroup.titleAlign

### Description
Controls the horizontal alignment of the group's [title-text](#attr-toolstripgrouptitle), within its [label](#attr-toolstripgrouplabel). Setting this attribute overrides the default specified by [groupTitleAlign](ToolStrip.md#attr-toolstripgrouptitlealign) on the containing [ToolStrip](ToolStrip.md#class-toolstrip).

**Flags**: IRW

---
## Attr: ToolStripGroup.rowHeight

### Description
The height of rows in each column.

**Flags**: IRW

---
## Attr: ToolStripGroup.titleHeight

### Description
Controls the height of the [title label](#attr-toolstripgrouplabel) in this group.

**Flags**: IRW

---
## Attr: ToolStripGroup.bodyConstructor

### Description
SmartClient class for the body.

**Flags**: IRA

---
## Attr: ToolStripGroup.body

### Description
HLayout autoChild that manages multiple [VLayouts](#attr-toolstripgroupcolumnlayout) containing controls.

**Flags**: IR

---
## Attr: ToolStripGroup.autoSizeToTitle

### Description
By default, ToolStripGroups are assigned a minimum width that allows the entire title to be visible. To prevent this bahavior and have group-titles cut off when they're wider than the buttons they contain, set this attribute to false

**Flags**: IR

---
## Attr: ToolStripGroup.titleStyle

### Description
CSS class applied to the [title label](#attr-toolstripgrouplabel) in this group.

**Flags**: IRW

---
## Attr: ToolStripGroup.controls

### Description
The array of controls to show in this group.

**Flags**: IRW

---
## Method: ToolStripGroup.getControlColumn

### Description
Return the [column widget](#attr-toolstripgroupcolumnlayout) that contains the passed control.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | the control to find in this group |

### Returns

`[Layout](#type-layout)` — the column widget containing the passed control

---
## Method: ToolStripGroup.removeControl

### Description
Removes a control from this toolStripGroup, destroying an existing [column](#attr-toolstripgroupcolumnlayout) if this is the last widget in that column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | a widget to remove from this group |

---
## Method: ToolStripGroup.reflowControls

### Description
Forces this group to reflow following changes to attributes that affect layout, like [numRows](#attr-toolstripgroupnumrows).

---
## Method: ToolStripGroup.setTitleHeight

### Description
This method forcibly sets the height of this group's [title label](#attr-toolstripgrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| titleHeight | [int](../reference.md#type-int) | false | — | the new height for the [title label](#attr-toolstripgrouplabel) |

---
## Method: ToolStripGroup.setTitleStyle

### Description
This method forcibly sets the [CSS class name](#attr-toolstripgrouptitlestyle) for this group's [title label](#attr-toolstripgrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | false | — | the CSS class to apply to the [title label](#attr-toolstripgrouplabel). |

---
## Method: ToolStripGroup.setTitle

### Description
Sets the [text](#attr-toolstripgrouptitle) to display in this group's [title label](#attr-toolstripgrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [String](#type-string) | false | — | The new title for this group |

---
## Method: ToolStripGroup.setShowTitle

### Description
This method forcibly shows or hides this group's [title label](#attr-toolstripgrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showTitle | [boolean](../reference.md#type-boolean) | false | — | should the title be shown or hidden? |

---
## Method: ToolStripGroup.setTitleAlign

### Description
This method forcibly sets the horizontal alignment of the [title-text](#attr-toolstripgrouptitle), within the [title label](#attr-toolstripgrouplabel), after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| align | [Alignment](../reference.md#type-alignment) | false | — | the new alignment for the text, left or right |

---
## Method: ToolStripGroup.addControl

### Description
Adds a control to this toolStripGroup, creating a new [column](#attr-toolstripgroupcolumnlayout) as necessary, according to the control's `rowSpan` value and the group's [numRows](#attr-toolstripgroupnumrows) value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | a widget to add to this group |
| index | [Integer](../reference_2.md#type-integer) | true | — | optional insertion index for this control |

---
## Method: ToolStripGroup.setTitleOrientation

### Description
This method forcibly sets the [vertical orientation](#attr-toolstripgrouptitleorientation) of this group's [title label](#attr-toolstripgrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [VerticalAlignment](../reference.md#type-verticalalignment) | false | — | the new orientation for the title, either bottom or top |

---
## Method: ToolStripGroup.addControls

### Description
Adds an array of controls to this group, creating new [columns](#attr-toolstripgroupcolumnlayout) as necessary, according to each control's `rowSpan` value and the group's [numRows](#attr-toolstripgroupnumrows) value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| controls | [Array of Canvas](#type-array-of-canvas) | false | — | an array of widgets to add to this group |

---
## Method: ToolStripGroup.setControls

### Description
Clears the array of controls and then adds the passed array to this toolStripGroup, creating new [columns](#attr-toolstripgroupcolumnlayout) as necessary, according to each control's `rowSpan` attribute and the group's [numRows](#attr-toolstripgroupnumrows) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| controls | [Array of Canvas](#type-array-of-canvas) | false | — | an array of widgets to add to this group |

---
