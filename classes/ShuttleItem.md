# ShuttleItem Documentation

[← Back to API Index](../reference.md)

---

## Class: ShuttleItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
[Shuttle](Shuttle.md#class-shuttle)-based form item for choosing values from a list of options.

Options for the Shuttle should be derived from an [optionDataSource](FormItem.md#attr-formitemoptiondatasource).

---
## Attr: ShuttleItem.valueField

### Description
The value field for a shuttle item will be applied to the [Shuttle](Shuttle.md#class-shuttle) as [Shuttle.valueField](Shuttle.md#attr-shuttlevaluefield).

If no explicit valueField was specified it may be automatically derived - see [FormItem.getValueFieldName](FormItem.md#method-formitemgetvaluefieldname) for details.

**Flags**: IR

---
## Attr: ShuttleItem.width

### Description
Width of the FormItem. Can be either a number indicating a fixed width in pixels, or "\*" indicating the FormItem fills the space allocated to it's column (or columns, for a [column spanning](FormItem.md#attr-formitemcolspan) item). You may also use "100%" as a synonym for "\*", but other percentages are not supported.

Note that for "absolute" item layout rather than the default "table" layout, the rules for specifying the width are slightly different. All percent sizes are allowed, but not "\*". See [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout) for further details.

See the [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout) overview for details.

### Groups

- formLayout

### See Also

- [FormItem.linearWidth](FormItem.md#attr-formitemlinearwidth)
- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)
- [FormItem.height](FormItem.md#attr-formitemheight)
- [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout)

**Flags**: IRW

---
## Attr: ShuttleItem.displayField

### Description
If set, this item will display a value from another field to the user instead of showing the underlying data value for the [field name](FormItem.md#attr-formitemname).

This property is used in two ways:

The item will display the displayField value from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues) if [FormItem.useLocalDisplayFieldValue](FormItem.md#attr-formitemuselocaldisplayfieldvalue) is true, (or if unset and the conditions outlined in the documentation for that property are met).

If this field has an [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property is used by default to identify which value to use as a display value in records from this related dataSource. In this usage the specified displayField must be explicitly defined in the optionDataSource to be used - see [getDisplayFieldName()](FormItem.md#method-formitemgetdisplayfieldname) for more on this behavior.  
If not using [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue), the display value for this item will be derived by performing a fetch against the [option dataSource](FormItem.md#method-formitemgetoptiondatasource) to find a record where the [value field](FormItem.md#method-formitemgetvaluefieldname) matches this item's value, and use the `displayField` value from that record.  
In addition to this, PickList-based form items that provide a list of possible options such as the [SelectItem](SelectItem.md#class-selectitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) will show the `displayField` values to the user by default, allowing them to choose a new data value (see [FormItem.valueField](FormItem.md#attr-formitemvaluefield)) from a list of user-friendly display values.

This essentially allows the specified `optionDataSource` to be used as a server based [valueMap](../reference.md#kb-topic-valuemap).

If [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, selecting a new value will update both the value for this field and the associated display-field value on the record being edited.

Note: Developers may specify the [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) property in addition to `displayField`. This is useful for cases where the display field name in the local dataSource differs from the display field name in the optionDataSource. See the documentation for [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) for more on this.  
If a foreignDisplayField is specified, as with just displayField, if [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, when the user chooses a value the associated display-field value on the record being edited will be updated. In this case it would be set to the foreignDisplayField value from the related record. This means foreignDisplayField is always expected to be set to the equivalent field in the related dataSources.  
Developers looking to display some _other_ arbitrary field(s) from the related dataSource during editing should consider using custom [PickList.pickListFields](PickList.md#attr-picklistpicklistfields) instead of setting a foreignDisplayField.

Note that if `optionDataSource` is set and no valid display field is specified, [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname) will return the dataSource title field by default.

If a displayField is specified for a freeform text based item (such as a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)), any user-entered value will be treated as a display value. In this scenario, items will derive the data value for the item from the first record where the displayField value matches the user-entered value. To avoid ambiguity, developers may wish to avoid this usage if display values are not unique.

### Groups

- databinding

### See Also

- [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname)
- [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

**Flags**: IR

---
## Attr: ShuttleItem.height

### Description
Height of the FormItem. Can be either a number indicating a fixed height in pixels, a percentage indicating a percentage of the overall form's height, or "\*" indicating take whatever remaining space is available. See the [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout) overview for details.

For form items having a [picker icon](FormItem.md#attr-formitemshowpickericon) (e.g. [SelectItem](SelectItem.md#class-selectitem), [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)) and [SpinnerItem](SpinnerItem.md#class-spinneritem)s, if there is no explicit [FormItem.pickerIconHeight](FormItem.md#attr-formitempickericonheight), the pickerIcon will be sized to match the available space based on the specified item height.  
Note that if spriting is being used, and the image to be displayed in these icons is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.  
Alternatively, the [pickerIconStyle](FormItem.md#attr-formitempickericonstyle) could be changed to a custom CSS style name, and in the case of [SpinnerItem](SpinnerItem.md#class-spinneritem)s, the [baseStyle](FormItemIcon.md#attr-formitemiconbasestyle) and [src](FormItemIcon.md#attr-formitemiconsrc) of the [SpinnerItem.increaseIcon](SpinnerItem.md#attr-spinneritemincreaseicon) and [SpinnerItem.decreaseIcon](SpinnerItem.md#attr-spinneritemdecreaseicon) AutoChildren could be customized.

Note that when FormItem is rendered as read-only with `readOnlyDisplay` as "static" the property [FormItem.staticHeight](FormItem.md#attr-formitemstaticheight) is used instead.

### Groups

- formLayout

### See Also

- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)
- [FormItem.width](FormItem.md#attr-formitemwidth)
- [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout)

**Flags**: IRW

---
## Attr: ShuttleItem.shuttle

### Description
The ShuttleItem generates a [Shuttle](Shuttle.md#class-shuttle) [AutoChild](../reference.md#type-autochild) as its [canvas](CanvasItem.md#attr-canvasitemcanvas).

**Flags**: R

---
## Attr: ShuttleItem.optionDataSource

### Description
The optionDataSource for a shuttle item will be applied to the [Shuttle](Shuttle.md#class-shuttle) as [Shuttle.dataSource](Shuttle.md#attr-shuttledatasource).

If no explicit optionDataSource was specified it may be automatically derived - see [FormItem.getOptionDataSource](FormItem.md#method-formitemgetoptiondatasource) for details.

**Flags**: IR

---
## Attr: ShuttleItem.shuttleFields

### Description
Which [Shuttle.fields](Shuttle.md#attr-shuttlefields) should be displayed in the [Shuttle](Shuttle.md#class-shuttle).

If not specified, the grids within the shuttle will show a single field containing the [displayField](FormItem.md#method-formitemgetdisplayfieldname), if specified otherwise the [valueField](FormItem.md#method-formitemgetvaluefieldname) for the item

**Flags**: IR

---
