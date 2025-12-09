# EditProxy Documentation

[← Back to API Index](../reference.md)

---

## Class: EditProxy

### Description
An EditProxy is attached to an editable component when editMode is enabled. This proxy has methods and properties which affect the component during editing.

### Groups

- devTools

---
## Attr: EditProxy.useCopyPasteShortcuts

### Description
Whether to enable keyboard shortcuts to [copy](EditContext.md#method-editcontextcopyeditnodes) and [paste](EditContext.md#method-editcontextpasteeditnodes) `editNodes`.

Enabled by default if [selection of children](#attr-editproxycanselectchildren) is also enabled.

For pasting, if [EditContext.allowNestedDrops](EditContext.md#attr-editcontextallownesteddrops) is enabled, only one editNode is selected and it is a valid container for the contents of the clipboard, editNodes will be pasted as new children of the selected container. Otherwise, they will be pasted at the root level of the [editNodeTree](EditContext.md#method-editcontextgeteditnodetree).

`useCopyPasteShortcuts` may only be set on the root `editNode` within any one [editNodeTree](EditContext.md#method-editcontextgeteditnodetree).

**Flags**: IR

---
## Attr: EditProxy.canSelectChildren

### Description
Whether to allow selection of the children of this [EditNode](../reference.md#object-editnode). The appearance and behavior of selected components is controlled by [SelectedAppearance](../reference.md#type-selectedappearance), or centrally across an [EditContext](EditContext.md#class-editcontext) via [EditContext.selectedAppearance](EditContext.md#attr-editcontextselectedappearance).

Individual children can be marked non-selectable via setting [EditProxy.canSelect](#attr-editproxycanselect) to `false`.

Use the [EditContext](EditContext.md#class-editcontext) to access and manipulate the currently selected set of EditNodes, via APIs such as [EditContext.getSelectedEditNode](EditContext.md#method-editcontextgetselectededitnode), [EditContext.selectSingleEditNode](EditContext.md#method-editcontextselectsingleeditnode) and [EditContext.selectedEditNodesUpdated](EditContext.md#method-editcontextselectededitnodesupdated).

### See Also

- [EditContext.canSelectEditNodes](EditContext.md#attr-editcontextcanselecteditnodes)

**Flags**: IRW

---
## Attr: EditProxy.allowNestedDrops

### Description
This property acts as a component-specific override for the [EditContext.allowNestedDrops](EditContext.md#attr-editcontextallownesteddrops) property. Unless explicitly set to false, the [EditContext.allowNestedDrops](EditContext.md#attr-editcontextallownesteddrops) controls whether a drop can be made into this component.

**Flags**: IR

---
## Attr: EditProxy.showDragHandle

### Description
Should drag handles or thumb be shown when this component is selected? These are shown unless this property is set to `false`.

**Flags**: IR

---
## Attr: EditProxy.inlineEditEvent

### Description
Event that triggers inline editing, showing the [EditProxy.inlineEditForm](#attr-editproxyinlineeditform), which consists of a single text input (single or multi-line according to [EditProxy.inlineEditMultiline](#attr-editproxyinlineeditmultiline)) shown in the [EditProxy.inlineEditForm](#attr-editproxyinlineeditform) AutoChild.

The initial value in the form comes from [EditProxy.getInlineEditText](#method-editproxygetinlineedittext) and is applied via [EditProxy.setInlineEditText](#method-editproxysetinlineedittext).

Many [EditProxy](#class-editproxy) subclasses have built-in modes for inline editing.

**Flags**: IR

---
## Attr: EditProxy.hoopSelector

### Description
Hoop selector canvas used for selecting multiple components.

Common customization properties can be provided by [EditContext.hoopSelectorProperties](EditContext.md#attr-editcontexthoopselectorproperties).

**Flags**: IR

---
## Attr: EditProxy.childrenSnapToGrid

### Description
If not null the [Canvas.childrenSnapToGrid](Canvas.md#attr-canvaschildrensnaptogrid) on the component represented by this EditProxy is set to this value only while in edit mode. This allows snapToGrid functionality to be enforced during edit mode but not when live.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: EditProxy.inlineEditInstructions

### Description
Instructions that appear below the text entry area if inline editing is enabled. See [EditProxy.inlineEditEvent](#attr-editproxyinlineeditevent) and [EditProxy.inlineEditInstructionLabel](#attr-editproxyinlineeditinstructionlabel).

**Flags**: IR

---
## Attr: EditProxy.childrenSnapResizeToGrid

### Description
If not null the [Canvas.childrenSnapResizeToGrid](Canvas.md#attr-canvaschildrensnapresizetogrid) on the component represented by this EditProxy is set to this value only while in edit mode. This allows snapResizeToGrid functionality to be enforced during edit mode but not when live.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: EditProxy.inlineEditForm

### Description
See [EditProxy.inlineEditEvent](#attr-editproxyinlineeditevent).

**Flags**: IR

---
## Attr: EditProxy.selectedTintColor

### Description
Mask color applied to [editMask](#attr-editproxyeditmask) of selected component when [selectedAppearance](#attr-editproxyselectedappearance) is "tintMask". Default value is determined from [EditContext.selectedTintColor](EditContext.md#attr-editcontextselectedtintcolor).

### See Also

- [EditProxy.selectedTintOpacity](#attr-editproxyselectedtintopacity)

**Flags**: IR

---
## Attr: EditProxy.inlineEditOnDrop

### Description
Should the inline editor be shown when new component is first dropped?

**Flags**: IR

---
## Attr: EditProxy.bringToFrontOnSelect

### Description
Should component be brought to front when selected? Applies when [EditProxy.useEditMask](#attr-editproxyuseeditmask):true.

**Flags**: IR

---
## Attr: EditProxy.canSelect

### Description
Can this component be selected? Selection is allowed unless this property is set to `false`.

**Flags**: IR

---
## Attr: EditProxy.selectedLabelBackgroundColor

### Description
The background color for the selection outline label. The default is defined on [SelectionOutline](SelectionOutline.md#class-selectionoutline) or [EditContext.selectedLabelBackgroundColor](EditContext.md#attr-editcontextselectedlabelbackgroundcolor).

NOTE: A selected component label is only supported when [selectedAppearance](#attr-editproxyselectedappearance) is "outlineEdges".

**Flags**: IR

---
## Attr: EditProxy.editMask

### Description
An editMask is created for any component placed into editMode with [EditProxy.useEditMask](#attr-editproxyuseeditmask):true.

Common customization properties can be provided by [EditContext.editMaskProperties](EditContext.md#attr-editcontexteditmaskproperties).

**Flags**: IR

---
## Attr: EditProxy.supportsInlineEdit

### Description
Whether this EditProxy has an inline edit behavior, which allows an end user to configure a component by editing a simple text representation of its configuration.

For example, when inline edit is enabled, a [SelectItem](SelectItem.md#class-selectitem) allows [editing its valueMap](SelectItemEditProxy.md#method-selectitemeditproxygetinlineedittext) as a comma-separated string, and a [ListGrid](ListGrid_1.md#class-listgrid)'s columns and data can be edited as several lines of comma-separated headings and data values.

See [EditProxy.inlineEditEvent](#attr-editproxyinlineeditevent) for more details and configuration options.

**Flags**: IR

---
## Attr: EditProxy.selectedTintOpacity

### Description
Opacity applied to [editMask](#attr-editproxyeditmask) of selected component when [selectedAppearance](#attr-editproxyselectedappearance) is "tintMask".

### See Also

- [EditProxy.selectedTintColor](#attr-editproxyselectedtintcolor)

**Flags**: IR

---
## Attr: EditProxy.selectedAppearance

### Description
Appearance that is applied to selected component. Default value is determined from [EditContext.selectedAppearance](EditContext.md#attr-editcontextselectedappearance).

When value is `null` the appearance is determined by:

*   If multiple selection is enabled, "tintMask" is used
*   Otherwise, "outlineMask" is used

### See Also

- [EditProxy.selectedBorder](#attr-editproxyselectedborder)
- [EditProxy.selectedTintColor](#attr-editproxyselectedtintcolor)
- [EditProxy.selectedTintOpacity](#attr-editproxyselectedtintopacity)

**Flags**: IR

---
## Attr: EditProxy.inlineEditMultiline

### Description
Whether inline editing should be single or multi-line.

Single-line input appears at the control's top-left corner, multiline covers the control.

**Flags**: IR

---
## Attr: EditProxy.selectedBorder

### Description
Set the CSS border to be applied to the selection outline of the selected components. Default value is determined from [EditContext.selectedBorder](EditContext.md#attr-editcontextselectedborder). This property is used when [EditProxy.selectedAppearance](#attr-editproxyselectedappearance) is `outlineMask` or `outlineEdges`.

**Flags**: IR

---
## Attr: EditProxy.autoMaskChildren

### Description
When child nodes are added to an EditContext, should they be masked by setting [EditProxy.useEditMask](#attr-editproxyuseeditmask) `true` if not explicitly set?

**Flags**: IR

---
## Attr: EditProxy.inlineEditInstructionLabel

### Description
Label AutoChild used to display [EditProxy.inlineEditInstructions](#attr-editproxyinlineeditinstructions) below the text entry area if provided. Defaults to the same styling as the system [Hover](Hover.md#class-hover).

**Flags**: IR

---
## Attr: EditProxy.useEditMask

### Description
When `true` an [EditProxy.editMask](#attr-editproxyeditmask) will be auto-generated and placed over the component to allow selection, positioning and resizing.

If this property is not set it will enabled when added to an EditContext if its parent component has an editProxy and [EditProxy.autoMaskChildren](#attr-editproxyautomaskchildren) is `true`.

**Flags**: IR

---
## Attr: EditProxy.persistCoordinates

### Description
Changes to all child [liveObject](EditNode.md#attr-editnodeliveobject)'s position and size can be persisted to their [EditNodes](../reference.md#object-editnode) based on this attribute setting and [EditContext.persistCoordinates](EditContext.md#attr-editcontextpersistcoordinates). This applies to both programmatic calls and user interaction (drag reposition or drag resize).

The default value of `null` allows [EditContext.persistCoordinates](EditContext.md#attr-editcontextpersistcoordinates) to control all coordinate persistence. An explicit value of `false` overrides the EditContext setting so that no children of the component save coordinates.

All coordinate persisting can be disabled with [EditContext.persistCoordinates](EditContext.md#attr-editcontextpersistcoordinates). Additionally, all control of persistence can be deferred to each EditProxy by setting [EditContext.persistCoordinates](EditContext.md#attr-editcontextpersistcoordinates) to `null`.

**Flags**: IRW

---
## Method: EditProxy.showSelectedAppearance

### Description
This method applies the [selectedAppearance](#attr-editproxyselectedappearance) to the selected component or resets it to the non-selected appearance. Override this method to create a custom appearance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | true to show component as selected, false otherwise |

---
## Method: EditProxy.startInlineEditing

### Description
Manual means of triggering inline editing. See [InlineEditEvent](../reference.md#type-inlineeditevent).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| appendChar | [String](#type-string) | true | — | optional String to append to current value as editing starts |

---
## Method: EditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](#attr-editproxyinlineeditform) to commit the change.

For a canvas with `isGroup` enabled, the `groupTitle` is updated. Otherwise the `contents` is updated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component state |

---
## Method: EditProxy.setCanSelectChildren

### Description
Setter for [canSelectChildren](#attr-editproxycanselectchildren).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canSelect | [boolean](../reference.md#type-boolean) | false | — | the new canSelectChildren |

**Flags**: A

---
## Method: EditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](#attr-editproxyinlineeditform) to obtain the starting edit value.

For a canvas with `isGroup` enabled, the `groupTitle` is returned. Otherwise the `contents` is returned.

---
