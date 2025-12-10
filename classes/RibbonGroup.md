# RibbonGroup Documentation

[← Back to API Index](../reference.md)

---

## Class: RibbonGroup

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A widget that groups [RibbonButtons](RibbonButton.md#class-ribbonbutton)s for use in [RibbonBars](RibbonBar.md#class-ribbonbar).

---
## Attr: RibbonGroup.styleName

### Description
CSS class applied to this RibbonGroup.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RibbonGroup.label

### Description
AutoChild [Label](Label.md#class-label) used to display the [title text](#attr-ribbongrouptitle) for this group.

Can be customized via the standard [AutoChild](../reference.md#type-autochild) pattern, and various convenience APIs exist for configuring it after initial draw: see [setShowTitle](#method-ribbongroupsetshowtitle), [setTitle](#method-ribbongroupsettitle), [setTitleAlign](#method-ribbongroupsettitlealign), [setTitleHeight](#method-ribbongroupsettitleheight), [setTitleOrientation](#method-ribbongroupsettitleorientation) and [setTitleStyle](#method-ribbongroupsettitlestyle).

**Flags**: IR

---
## Attr: RibbonGroup.titleHeight

### Description
Controls the height of the [title label](#attr-ribbongrouplabel) in this group.

**Flags**: IRW

---
## Attr: RibbonGroup.numRows

### Description
The number of rows of controls to display in each column. Each control will take one row in a [columnLayout](#attr-ribbongroupcolumnlayout) by default, but those that support the feature may specify `rowSpan` to override that.

Note that settings like this, which affect the group's layout, are not applied directly if changed at runtime - a call to [reflowControls](#method-ribbongroupreflowcontrols) will force the group to reflow.

**Flags**: IRW

---
## Attr: RibbonGroup.titleAlign

### Description
Controls the horizontal alignment of the group's [title-text](#attr-ribbongrouptitle), within its [label](#attr-ribbongrouplabel). Setting this attribute overrides the default specified by [groupTitleAlign](RibbonBar.md#attr-ribbonbargrouptitlealign) on the containing [RibbonBar](RibbonBar.md#class-ribbonbar).

### Groups

- ribbonGroup

**Flags**: IRW

---
## Attr: RibbonGroup.rowHeight

### Description
The height of rows in each column.

**Flags**: IRW

---
## Attr: RibbonGroup.titleOrientation

### Description
Controls the [vertical orientation](#attr-ribbongrouptitleorientation) of this group's [title label](#attr-ribbongrouplabel). Setting this attribute overrides the default specified by [groupTitleOrientation](RibbonBar.md#attr-ribbonbargrouptitleorientation) on the containing [RibbonBar](RibbonBar.md#class-ribbonbar).

### Groups

- ribbonGroup

**Flags**: IRW

---
## Attr: RibbonGroup.autoSizeToTitle

### Description
By default, `RibbonGroups` are assigned a minimum width that allows the entire title to be visible. To prevent this behavior and have group-titles cut off when they're wider than the buttons they contain, set this attribute to false

### Groups

- title

**Flags**: IR

---
## Attr: RibbonGroup.labelConstructor

### Description
SmartClient class for the [title label](#attr-ribbongrouplabel) AutoChild.

**Flags**: IRA

---
## Attr: RibbonGroup.controls

### Description
The array of controls to show in this group.

### Groups

- ribbonGroup

**Flags**: IRW

---
## Attr: RibbonGroup.titleStyle

### Description
CSS class applied to the [title label](#attr-ribbongrouplabel) in this group.

**Flags**: IRW

---
## Attr: RibbonGroup.labelLayout

### Description
HLayout autoChild that houses the [label](#attr-ribbongrouplabel) in which the [title text](#attr-ribbongrouptitle) is displayed.

This can be customized via the standard [AutoChild](../reference.md#type-autochild) pattern.

**Flags**: IR

---
## Attr: RibbonGroup.body

### Description
HLayout autoChild that manages multiple [VLayouts](#attr-ribbongroupcolumnlayout) containing controls.

**Flags**: IR

---
## Attr: RibbonGroup.bodyConstructor

### Description
SmartClient class for the body.

**Flags**: IRA

---
## Attr: RibbonGroup.titleProperties

### Description
AutoChild properties for fine customization of the [title label](#attr-ribbongrouplabel).

**Deprecated**

**Flags**: IRW

---
## Attr: RibbonGroup.newControlConstructor

### Description
Widget class for controls [created automatically](#method-ribbongroupcreatecontrol) by this RibbonGroup. Since [such controls](#attr-ribbongroupnewcontrolconstructor) are created via the autoChild system, they can be further customized via the newControlProperties property.

### Groups

- ribbonGroup

**Flags**: IR

---
## Attr: RibbonGroup.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: RibbonGroup.title

### Description
The title text to display in this group's [title label](#attr-ribbongrouplabel).

### Groups

- ribbonGroup

**Flags**: IRW

---
## Attr: RibbonGroup.columnLayout

### Description
AutoChild VLayouts created automatically by groups. Each manages a single column of child controls in the group. Child controls that support `rowSpan` may specify it in order to occupy more than one row in a single column. See [numRows](#attr-ribbongroupnumrows) for related information.

**Flags**: IR

---
## Attr: RibbonGroup.newControlDefaults

### Description
Properties used by [createControl](#method-ribbongroupcreatecontrol) when creating new controls.

### Groups

- ribbonGroup

**Flags**: IR

---
## Method: RibbonGroup.setTitleOrientation

### Description
This method forcibly sets the [vertical orientation](#attr-ribbongrouptitleorientation) of this group's [title label](#attr-ribbongrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [VerticalAlignment](../reference.md#type-verticalalignment) | false | — | the new orientation for the title, either bottom or top |

### Groups

- ribbonGroup

---
## Method: RibbonGroup.setTitleStyle

### Description
This method forcibly sets the [CSS class name](#attr-ribbongrouptitlestyle) for this group's [title label](#attr-ribbongrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | false | — | the CSS class to apply to the [title label](#attr-ribbongrouplabel). |

---
## Method: RibbonGroup.reflowControls

### Description
Forces this group to reflow following changes to attributes that affect layout, like [numRows](#attr-ribbongroupnumrows).

---
## Method: RibbonGroup.getControlColumn

### Description
Return the [column widget](#attr-ribbongroupcolumnlayout) that contains the passed control.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | the control to find in this group |

### Returns

`[Layout](#type-layout)` — the column widget containing the passed control

---
## Method: RibbonGroup.removeControl

### Description
Removes a control from this `RibbonGroup`, destroying an existing [column](#attr-ribbongroupcolumnlayout) if this is the last widget in that column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | a widget to remove from this group |

---
## Method: RibbonGroup.setTitle

### Description
Sets the [text](#attr-ribbongrouptitle) to display in this group's [title label](#attr-ribbongrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [String](#type-string) | false | — | The new title for this group |

---
## Method: RibbonGroup.setShowTitle

### Description
This method forcibly shows or hides this group's [title label](#attr-ribbongrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showTitle | [boolean](../reference.md#type-boolean) | false | — | should the title be shown or hidden? |

---
## Method: RibbonGroup.setTitleAlign

### Description
This method forcibly sets the horizontal alignment of the [title-text](#attr-ribbongrouptitle), within the [title label](#attr-ribbongrouplabel), after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| align | [Alignment](../reference_2.md#type-alignment) | false | — | the new alignment for the text, left or right |

### Groups

- ribbonGroup

---
## Method: RibbonGroup.addControls

### Description
Adds an array of controls to this group, creating new [columns](#attr-ribbongroupcolumnlayout) as necessary, according to each control's `rowSpan` value and the group's [numRows](#attr-ribbongroupnumrows) value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| controls | [Array of Canvas](#type-array-of-canvas) | false | — | an array of widgets to add to this group |

---
## Method: RibbonGroup.addControl

### Description
Adds a control to this `RibbonGroup`, creating a new [column](#attr-ribbongroupcolumnlayout) as necessary, according to the control's `rowSpan` value and the group's [numRows](#attr-ribbongroupnumrows) value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | a widget to add to this group |
| index | [Integer](../reference_2.md#type-integer) | true | — | optional insertion index for this control |

---
## Method: RibbonGroup.setTitleHeight

### Description
This method forcibly sets the height of this group's [title label](#attr-ribbongrouplabel) after initial draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| titleHeight | [int](../reference.md#type-int) | false | — | the new height for the [title label](#attr-ribbongrouplabel) |

---
## Method: RibbonGroup.setControls

### Description
Clears the array of controls and then adds the passed array to this group, creating new [columns](#attr-ribbongroupcolumnlayout) as necessary, according to each control's `rowSpan` attribute and the group's [numRows](#attr-ribbongroupnumrows) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| controls | [Array of Canvas](#type-array-of-canvas) | false | — | an array of widgets to add to this group |

---
## Method: RibbonGroup.createControl

### Description
Creates a new control and adds it to this RibbonGroup. The control is created using the autoChild system, according to the specified [constructor](#attr-ribbongroupnewcontrolconstructor) and the passed properties are applied to it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| properties | [Canvas Properties](#type-canvas-properties) | false | — | properties to apply to the new control |
| position | [Integer](../reference_2.md#type-integer) | true | — | the index at which to insert the new control |

---
