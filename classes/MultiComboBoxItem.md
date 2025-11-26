# MultiComboBoxItem Documentation

[← Back to API Index](../reference.md)

---

## Class: MultiComboBoxItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
A MultiComboBoxItem is a combo box that allows the user to select multiple options. Each selected option is represented as a button that can be clicked to deselect the option. The relative layout of the buttons to the combo box is specified with the [MultiComboBoxItem.layoutStyle](#attr-multicomboboxitemlayoutstyle) attribute. The buttons will be kept in the order that they were added, with the most recently added button being adjacent to the combo box. `MultiComboBoxItem` uses the [AutoChild](../reference.md#type-autochild) pattern to construct the [comboBox](#attr-multicomboboxitemcombobox) and the [buttons](#attr-multicomboboxitembutton) so that they can be easily customized. For example, you can customize the criteria used to fetch by overriding [ComboBoxItem.getPickListFilterCriteria](ComboBoxItem.md#method-comboboxitemgetpicklistfiltercriteria) via [comboBoxProperties](#attr-multicomboboxitemcombobox).

### See Also

- [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)

---
## ClassAttr: MultiComboBoxItem.defaultHint

### Description
The default hint string.

### Groups

- i18nMessages

**Flags**: R

---
## Attr: MultiComboBoxItem.pickListConstructor

### Description
The Class to use when creating a picker of [type "list"](PickList.md#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickListMenu](PickListMenu.md#class-picklistmenu).

### Groups

- pickList

**Flags**: IR

---
## Attr: MultiComboBoxItem.valueMap

### Description
The `valueMap` of the combo box.

### See Also

- [FormItem.valueMap](FormItem.md#attr-formitemvaluemap)

**Flags**: IRW

---
## Attr: MultiComboBoxItem.deselectedButtonStyle

### Description
When [showDeletions](FormItem.md#attr-formitemshowdeletions) is `true`, the [Button.baseStyle](Button.md#attr-buttonbasestyle) used on [buttons](#attr-multicomboboxitembutton) for values that have been deleted (also called "deselected buttons").

If unset, then the `baseStyle` of deselected buttons is not changed.

**NOTE:** Deselected buttons are also disabled, so styling should be provided for the `deselectedButtonStyle` + "Disabled" style name.

### See Also

- [MultiComboBoxItem.pendingButtonStyle](#attr-multicomboboxitempendingbuttonstyle)

**Flags**: IR

---
## Attr: MultiComboBoxItem.addUnknownValues

### Description
Similar to [ComboBoxItem.addUnknownValues](ComboBoxItem.md#attr-comboboxitemaddunknownvalues), controls whether additional values can be added to the ComboBox or whether the user must choose from the available values in the picklist only.

If this setting is changed after the MultiComboBoxItem has been created, the current value of the item is reset to null and all buttons for non-default values (values not in the [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue) array) are removed.

**Flags**: IRW

---
## Attr: MultiComboBoxItem.pendingButtonStyle

### Description
When [showPending](FormItem.md#attr-formitemshowpending) is `true`, the [Button.baseStyle](Button.md#attr-buttonbasestyle) used on [buttons](#attr-multicomboboxitembutton) that are in the "Pending" visual state.

If unset, then the `baseStyle` of pending buttons is not changed.

### See Also

- [MultiComboBoxItem.deselectedButtonStyle](#attr-multicomboboxitemdeselectedbuttonstyle)

**Flags**: IR

---
## Attr: MultiComboBoxItem.optionDataSource

### Description
The `optionDataSource` of the combo box.

### See Also

- [ComboBoxItem.optionDataSource](ComboBoxItem.md#attr-comboboxitemoptiondatasource)

**Flags**: IR

---
## Attr: MultiComboBoxItem.button

### Description
An [AutoChild](../reference.md#type-autochild) attribute used to create the buttons in the MultiComboBoxItem.

**Flags**: RA

---
## Attr: MultiComboBoxItem.pickTreeConstructor

### Description
The Class to use when creating a picker of [type "tree"](PickList.md#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickTreeMenu](../reference.md#class-picktreemenu).

**Flags**: IR

---
## Attr: MultiComboBoxItem.displayField

### Description
The `displayField` of the combo box.

### See Also

- [ComboBoxItem.displayField](ComboBoxItem.md#attr-comboboxitemdisplayfield)

**Flags**: IRA

---
## Attr: MultiComboBoxItem.valueField

### Description
The `valueField` of the combo box.

### See Also

- [ComboBoxItem.valueField](ComboBoxItem.md#attr-comboboxitemvaluefield)

**Flags**: IR

---
## Attr: MultiComboBoxItem.shouldSaveValue

### Description
Should this item's value be saved in the form's values and hence returned from [form.getValues()](DynamicForm.md#method-dynamicformgetvalues)?

`shouldSaveValue:false` is used to mark formItems which do not correspond to the underlying data model and should not save a value into the form's [values](DynamicForm.md#attr-dynamicformvalues). Example includes visual separators, password re-type fields, or checkboxes used to show/hide other form items.

A `shouldSaveValue:false` item should be given a value either via [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue) or by calling [form.setValue(item, value)](DynamicForm.md#method-dynamicformsetvalue) or [formItem.setValue(value)](FormItem.md#method-formitemsetvalue). Providing a value via [form.values](DynamicForm.md#attr-dynamicformvalues) or [form.setValues()](DynamicForm.md#method-dynamicformsetvalues) will automatically switch the item to `shouldSaveValue:true`.

Note that

*   if an item is shouldSaveValue true, but has no name, a warning is logged, and shouldSaveValue will be set to false.

### Groups

- formValues

**Flags**: IR

---
## Attr: MultiComboBoxItem.autoFitButtons

### Description
Specifies whether to autofit the buttons in the MultiComboBoxItem. The default value is true if [MultiComboBoxItem.layoutStyle](#attr-multicomboboxitemlayoutstyle) is "flow", but false for a layoutStyle of "vertical" or "verticalReverse". If the `layoutStyle` is "horizontal" or "horizontalReverse" then the buttons will autofit regardless of the setting of this property.

**Flags**: IR

---
## Attr: MultiComboBoxItem.autoFetchData

### Description
Should the MultiComboBoxItem fetch data from the [data source](#attr-multicomboboxitemoptiondatasource) immediately or wait until the user first opens the pickList.

### See Also

- [ComboBoxItem.autoFetchData](ComboBoxItem.md#attr-comboboxitemautofetchdata)

**Flags**: IR

---
## Attr: MultiComboBoxItem.optionOperationId

### Description
If this item has a specified `optionDataSource`, this attribute may be set to specify an explicit [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) when performing a fetch against the option dataSource to pick up display value mapping.

### Groups

- databinding

**Flags**: IR

---
## Attr: MultiComboBoxItem.layoutStyle

### Description
Specifies the layout style of the combo box and the buttons in the MultiComboBoxItem. Available values are "flow" (the default), "horizontal", "horizontalReverse", "vertical", and "verticalReverse".

*   **"flow"**:  The buttons appear to the left of the combo box. When there is no more room, the combo box and/or buttons flow onto a new line. The buttons autoFit by default.
*   **"horizontal"**:  The combo box appears on right and buttons are horizontally stacked directly left of it. The buttons must autofit.
*   **"horizontalReverse"**:  Like "horizontal" but the combo box appears on the left. The buttons must autofit.
*   **"vertical"**:  The combo box appears on top and buttons are stacked beneath it. Buttons do not autofit by default.
*   **"verticalReverse"**:  Like "vertical" but the combo box appears at bottom. The buttons do not autofit by default.

**Flags**: IRW

---
## Attr: MultiComboBoxItem.comboForm

### Description
The [DynamicForm](DynamicForm.md#class-dynamicform) holding the [comboBox](#attr-multicomboboxitemcombobox).

**Flags**: RA

---
## Attr: MultiComboBoxItem.rootNodeId

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), this is the [id](SelectItem.md#attr-selectitemvaluefield) of the record to use as the [root](Tree.md#attr-treerootvalue) node.

**Flags**: IRW

---
## Attr: MultiComboBoxItem.comboBoxWidth

### Description
Specifies the size of the combo box field.

Note that this attribute only has an effect in "flow", "horizontal", and "horizontalReverse" [modes](#attr-multicomboboxitemlayoutstyle). In the other modes, the combo box is as wide as the overall MultiComboBoxItem.

**Flags**: IRW

---
## Attr: MultiComboBoxItem.autoOpenTree

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), which nodes should be opened automatically. Options are:

*   "none" - no nodes are opened automatically
*   "root" - opens the [top-level node](PickList.md#attr-picklistrootnodeid) - in databound tree-pickers, this node is always hidden
*   "all" - when [loading data on demand](ResultTree.md#attr-resulttreeloaddataondemand), opens the [top-level node](PickList.md#attr-picklistrootnodeid) and all of it's direct descendants - otherwise, opens all loaded nodes

**Flags**: IRW

---
## Attr: MultiComboBoxItem.alwaysExitOnTab

### Description
If true, hitting tab always exits the field, and will also add a value to the list of selected values if there is match (and depending on the setting for [addUnknownValues](#attr-multicomboboxitemaddunknownvalues)).

If false, if the user has typed in a value and hits tab, focus remains in the field. If there is a match or if [MultiComboBoxItem.addUnknownValues](#attr-multicomboboxitemaddunknownvalues) is true, a value will be added. Otherwise, the input cursor remains at the end of the entered value.

**Flags**: IR

---
## Attr: MultiComboBoxItem.useInsertionOrder

### Description
Specifies whether to arrange the buttons of the MultiComboBoxItem in the order that they were selected (the default), or to sort the buttons by [MultiComboBoxItem.displayField](#attr-multicomboboxitemdisplayfield).

**Flags**: IR

---
## Attr: MultiComboBoxItem.comboBox

### Description
An [AutoChild](../reference.md#type-autochild) attribute to create the combo box in a MultiComboBoxItem.

**Flags**: RA

---
## Attr: MultiComboBoxItem.dataSetType

### Description
Whether to show the picker as a flat list, or a collapsible tree.

The default value, "list", will use an instance of the [pickListConstructor](PickList.md#attr-picklistpicklistconstructor) as the picker - "tree" will show an instance of [pickTreeConstructor](PickList.md#attr-picklistpicktreeconstructor).

**Flags**: IR

---
## Attr: MultiComboBoxItem.valueLayout

### Description
The layout used to arrange the [comboForm](#attr-multicomboboxitemcomboform) and the buttons representing the values of the MultiComboBoxItem. Note that the constructor cannot be changed (setting a valueLayoutConstructor has no effect) because the exact layout class used depends on the current [layout style](#attr-multicomboboxitemlayoutstyle).

**Flags**: RA

---
## Method: MultiComboBoxItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this `MultiComboBoxItem` should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, when displayed in the pending state and a [pendingButtonStyle](#attr-multicomboboxitempendingbuttonstyle) is set, then:

*   If [useInsertionOrder](#attr-multicomboboxitemuseinsertionorder) is `false`, buttons for any new values will have their [baseStyle](Button.md#attr-buttonbasestyle) set to `pendingButtonStyle`; otherwise
*   (`useInsertionOrder` is `true`) buttons for values will have their [baseStyle](Button.md#attr-buttonbasestyle) set to `pendingButtonStyle` if either the value is new or it is in a different place within the value array.

Returning `false` will cancel this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing `DynamicForm` instance. |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this"). |
| pendingStatus | [boolean](../reference.md#type-boolean) | false | — | `true` if the item should show its pending visual state; `false` otherwise. |
| newValue | [Any](#type-any) | false | — | the current form item value. |
| value | [Any](#type-any) | false | — | the value that would be restored by a call to [DynamicForm.resetValues](DynamicForm.md#method-dynamicformresetvalues). |

### Returns

`[boolean](../reference.md#type-boolean)` — `false` to cancel the default behavior.

---
## Method: MultiComboBoxItem.showValue

### Description
This method will be called whenever this FormItem's value is being set via a programmatic call to e.g: [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues) or [FormItem.setValue](FormItem.md#method-formitemsetvalue) and may be overridden by CanvasItems intended to support displaying data values to update the embedded Canvas to reflect the value passed in.

The value of a MultiComboBoxItem to the form is an array of valueField values corresponding to the selected combo box options.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| displayValue | [Any](#type-any) | false | — | new display value for the item. This is the value after applying any custom formatter or valueMap |
| dataValue | [Any](#type-any) | false | — | underlying data value for the item |
| form | [DynamicForm](#type-dynamicform) | false | — | the dynamicForm in which this item is contained |
| item | [CanvasItem](#type-canvasitem) | false | — | the live form item instance |

---
## Method: MultiComboBoxItem.setLayoutStyle

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| layoutStyle | [MultiComboBoxLayoutStyle](../reference_2.md#type-multicomboboxlayoutstyle) | false | — | the new layout style |

### See Also

- [MultiComboBoxItem.layoutStyle](#attr-multicomboboxitemlayoutstyle)

---
## Method: MultiComboBoxItem.setAutoFitButtons

### Description
Sets the [MultiComboBoxItem.autoFitButtons](#attr-multicomboboxitemautofitbuttons) property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoFitButtons | [boolean](../reference.md#type-boolean) | false | — | whether to autofit the buttons |

---
