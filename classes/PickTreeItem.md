# PickTreeItem Documentation

[← Back to API Index](../main.md)

---

## Class: PickTreeItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
FormItem that allows picking a value from a hierarchical data model.

---
## Attr: PickTreeItem.valueTree

### Description
A [Tree](Tree.md#class-tree) of options from which the user can select.

**Flags**: IR

---
## Attr: PickTreeItem.emptyDisplayValue

### Description
Text to display when this form item has a null or undefined value.

If the formItem has a databound pickList, and its [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) or [FormItem.valueField](FormItem.md#attr-formitemvaluefield) (if the former isn't set) has an undefined emptyCellValue field, that field will automatically be set using the emptyDisplayValue property.

If the emptyDisplayValue is null (the default) then this item will use the standard title of the tree menu button that is shown when no values are selected.

### Groups

- display_values

**Flags**: IRW

---
## Attr: PickTreeItem.pendingButtonStyle

### Description
When [showPending](FormItem.md#attr-formitemshowpending) is `true`, the [Button.baseStyle](Button.md#attr-buttonbasestyle) of the [button](#attr-picktreeitembutton) when in the "Pending" visual state.

If unset, then the `baseStyle` of the button is not changed.

**Flags**: IR

---
## Attr: PickTreeItem.shouldSaveValue

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
## Attr: PickTreeItem.emptyMenuMessage

### Description
This message will be displayed as a single, disabled option in any empty menu/submenu created from this item's data tree.

**Flags**: IRA

---
## Attr: PickTreeItem.button

### Description
The visible button created by a PickTreeItem is an [AutoChild](../main.md#type-autochild) of type [TreeMenuButton](TreeMenuButton.md#class-treemenubutton) by default.

**Flags**: R

---
## Attr: PickTreeItem.readOnlyDisplay

### Description
If [FormItem.canEdit](FormItem.md#attr-formitemcanedit) is set to `false`, how should this item be displayed to the user?

For PickTreeItems, this setting affects only the item's title - the button itself will always appear disabled when canEdit is false, since buttons don't provide `readOnly` or `static` appearances.

**Flags**: IRW

---
## Attr: PickTreeItem.dataSource

### Description
If specified, the tree of possible options will be derived from the dataSource as a ResultTree, rather than using this.valueTree. Options can be loaded on demand or up front according tp [PickTreeItem.loadDataOnDemand](#attr-picktreeitemloaddataondemand).

**Flags**: IRA

---
## Attr: PickTreeItem.loadDataOnDemand

### Description
If this is a databound item, should the load our set of possible options be loaded on demand (as submenus are displayed), or upfront?

**Flags**: IRA

---
## Attr: PickTreeItem.dataProperties

### Description
For a `PickTreeItem` that uses a DataSource, these properties will be passed to the automatically-created ResultTree. This can be used for various customizations such as modifying the automatically-chosen [Tree.parentIdField](Tree.md#attr-treeparentidfield).

### Groups

- databinding

**Flags**: IR

---
## Attr: PickTreeItem.optionDataSource

### Description
If set, this FormItem will map stored values to display values as though a [ValueMap](../main_2.md#type-valuemap) were specified, by fetching records from the specified `optionDataSource` and extracting the [valueField](FormItem.md#attr-formitemvaluefield) and [displayField](FormItem.md#attr-formitemdisplayfield) in loaded records, to derive one valueMap entry per record loaded from the optionDataSource.

With the default setting of [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues), fetches will be initiated against the optionDataSource any time the FormItem has a non-null value and no corresponding display value is available. This includes when the form is first initialized, as well as any subsequent calls to [FormItem.setValue](FormItem.md#method-formitemsetvalue), such as may happen when [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) is called. Retrieved values are automatically cached by the FormItem.

Note that if a normal, static [valueMap](FormItem.md#attr-formitemvaluemap) is **also** specified for the field (either directly in the form item or as part of the field definition in the dataSource), it will be preferred to the data derived from the optionDataSource for whatever mappings are present.

In a databound form, if [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) is specified for a FormItem and `optionDataSource` is unset, `optionDataSource` will default to the form's current DataSource

### Groups

- display_values

### See Also

- [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

**Flags**: IRW

---
## Attr: PickTreeItem.canSelectParentItems

### Description
If true, clicking or pressing Enter on a menu item that has a submenu will select that item (with standard behavior of hiding the menus, calling click handlers, etc) instead of showing the submenu.

### Groups

- selection

**Flags**: IRW

---
## Attr: PickTreeItem.valueField

### Description
Which field in the tree-data should be returned as this item's value? If unspecified, the path will be used

**Flags**: IR

---
## Attr: PickTreeItem.displayField

### Description
Specifies an alternative field from which display values should be retrieved for this item.

If this item is not databound ([PickTreeItem.dataSource](#attr-picktreeitemdatasource) is unset), this is implemented by picking up the value of the specified field from the [PickTreeItem.valueTree](#attr-picktreeitemvaluetree).

Otherwise this item will attempt to map its underlying value to a display value by retrieving a record from the [PickTreeItem.dataSource](#attr-picktreeitemdatasource) where the [PickTreeItem.valueField](#attr-picktreeitemvaluefield) matches this item's value, and displaying the `displayField` value from that record.

**Flags**: IR

---
## Method: PickTreeItem.setValueTree

### Description
Setter to change the [PickTreeItem.valueTree](#attr-picktreeitemvaluetree) at runtime

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valueTree | [Tree](#type-tree) | false | — | new value tree for the item |

---
## Method: PickTreeItem.setEmptyDisplayValue

### Description
Setter for [PickTreeItem.emptyDisplayValue](#attr-picktreeitememptydisplayvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| emptyDisplayValue | [HTMLString](../main.md#type-htmlstring) | false | — | — |

### Groups

- display_values

---
## Method: PickTreeItem.fetchData

### Description
Only applies to databound items (see [PickTreeItem.optionDataSource](#attr-picktreeitemoptiondatasource)).  
Performs a fetch type operation on this item's DataSource to retrieve/refresh the tree of data displayed as rows in this items menu.

---
## Method: PickTreeItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this `PickTreeItem` should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, when displayed in the pending state and a [pendingButtonStyle](#attr-picktreeitempendingbuttonstyle) is set, then the [button](#attr-picktreeitembutton)'s [baseStyle](Button.md#attr-buttonbasestyle) is set to `pendingButtonStyle`. Returning `false` will cancel this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing `DynamicForm` instance. |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this"). |
| pendingStatus | [boolean](../main.md#type-boolean) | false | — | `true` if the item should show its pending visual state; `false` otherwise. |
| newValue | [Any](#type-any) | false | — | the current form item value. |
| value | [Any](#type-any) | false | — | the value that would be restored by a call to [DynamicForm.resetValues](DynamicForm.md#method-dynamicformresetvalues). |

### Returns

`[boolean](../main.md#type-boolean)` — `false` to cancel the default behavior.

---
