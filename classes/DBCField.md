# DBCField Documentation

[← Back to API Index](../reference.md)

---

## Attr: DBCField.valueMap

### Description
A [ValueMap](../reference_2.md#type-valuemap) is a set of legal values for a field.

The valueMap can be specified as either an Array of legal values, or as an [Object](../reference.md#type-object) where each property maps a stored value to a user-displayable value.

To enforce that a field should be constrained to only the values in the valueMap, either declare [field.type](DataSourceField.md#attr-datasourcefieldtype) as "enum", or use a [ValidatorType](../reference.md#type-validatortype) of "isOneOf" with explicitly listed values. Otherwise, although a normal [SelectItem](SelectItem.md#class-selectitem) control will only allow values from the valueMap to be entered, other controls such as a [ComboBox](ComboBoxItem.md#class-comboboxitem) will allow other values to be entered.

In XML, a valueMap that specifies only a list of legal values is specified as follows:

```
   <valueMap>
   	<value>Pens & Pencils</value>
   	<value>Stationery</value>
   	<value>Computer Products</value>
   	<value>Furniture</value>
   	<value>Misc</value>
   </valueMap>
 
```
A ValueMap that specifies stored values mapped to user-visible values is specified as follows:
```
   <valueMap>
   	<value ID="1">Pens & Pencils</value>
   	<value ID="2">Stationery</value>
   	<value ID="3">Computer Products</value>
   	<value ID="4">Furniture</value>
   	<value ID="5">Misc</value>
   </valueMap>
 
```

### Groups

- dataType

**Flags**: IR

---
## Attr: DBCField.timeFormatter

### Description
Preferred time-format to apply to date type values within this field. If this property is specified on a field displayed within a dataBound component such as a [ListGrid](ListGrid_1.md#class-listgrid) or [DynamicForm](DynamicForm.md#class-dynamicform), any dates displayed in this field will be formatted as times using the appropriate format.

This is most commonly only applied to fields specified as type `"time"` though if no explicit [FormItem.dateFormatter](FormItem.md#attr-formitemdateformatter) is specified it will be respected for other fields as well.

See [ListGridField.timeFormatter](ListGridField.md#attr-listgridfieldtimeformatter) and [FormItem.timeFormatter](FormItem.md#attr-formitemtimeformatter) for more information.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: DBCField.displayField

### Description
When records from this dataSource are displayed in a dataBoundComponent such as a [ListGrid](ListGrid_1.md#class-listgrid), the `displayField` attribute may be used to cause some field to display a value from another field in the record.

This is typically used for editable [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) fields. In this scenario, a dataSource field has a foreignKey field which stores an ID value used to identify records in another, related dataSource. Rather than display this ID to users, developers may wish to display another, user-friendly field from the related record. This is easy to achieve by having a second field on the dataSource which will be populated with the "display value" from this related dataSource, and using `dataSourceField.displayField` to show this value. The [DataSourceField.includeFrom](DataSourceField.md#attr-datasourcefieldincludefrom) feature handles populating this field automatically for dataSources backed by the [SmartClient Server](../kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration). See the "Editing included fields" section of the [DataSourceField.includeFrom](DataSourceField.md#attr-datasourcefieldincludefrom) documentation for more on editing included foreignKey fields.

Editable dataSourceFields with a specified `displayField` and `foreignKey` will typically be edited using a [SelectItem](SelectItem.md#class-selectitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem). In this case, in addition to identifying the field to use as a static display value within the record being edited, `displayField` will also identify which field on the related dataSource to use as a display field when showing a set of options to the user. This behavior may be modified in a couple of ways:

*   The [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) attribute may be used to handle the case where the name of the field used as a displayField within the dataSource is different from the name of the included/equivalent field in the related dataSource.
*   The [DataSourceField.useLocalDisplayFieldValue](DataSourceField.md#attr-datasourcefielduselocaldisplayfieldvalue) attribute may be explicitly set to false to avoid picking up a display value from the local record altogether. Instead the displayField will be used only to derive the display value from a related record from the optionDataSource

For more on how FormItems use the displayField property, see [FormItem.displayField](FormItem.md#attr-formitemdisplayfield).

### Groups

- dataSourceRelations

**Flags**: IR

---
## Attr: DBCField.dateFormatter

### Description
Preferred display format to use for date type values within this field. If this property is set on a field displayed in a databound component such as a [DynamicForm](DynamicForm.md#class-dynamicform) or [ListGrid](ListGrid_1.md#class-listgrid) it will be respected (See [FormItem.dateFormatter](FormItem.md#attr-formitemdateformatter) and [ListGridField.dateFormatter](ListGridField.md#attr-listgridfielddateformatter)).

Note that this property is also honored when exporting directly to Excel spreadsheets (ie, when using XLS or XLSX/OOXML form, **not** CSV); "date" and "datetime" fields with this property set will deliver real dates and formatting information to Excel, rather than formatted strings or unformatted dates.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: DBCField.name

### Description
Name of this field. Must be unique within the [DataBoundComponent](../reference.md#interface-databoundcomponent) as well as a valid JavaScript identifier. See [FieldName](../reference.md#type-fieldname) for details and how to check for validity.

The name of the field is usually also the property in each record which holds the record's value for the field.

### Groups

- data

**Flags**: IR

---
