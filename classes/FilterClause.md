# FilterClause Documentation

[← Back to API Index](../reference.md)

---

## Class: FilterClause

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A horizontal, Layout-based widget that allows a user to input a single criterion based on one field and one operator.

Note that FilterClauses must be used in conjunction with a [FilterBuilder](FilterBuilder.md#class-filterbuilder). By default the FilterBuilder will auto-generate its clauses based on specified criteria, but for advanced usage a FilterClause may be instantiated directly and passed to a filterBuilder via [FilterBuilder.addClause](FilterBuilder.md#method-filterbuilderaddclause).

---
## Attr: FilterClause.fieldPickerProperties

### Description
Properties to combine with the [FieldPicker](FieldPicker.md#class-fieldpicker) autoChild FormItem.

**Flags**: IR

---
## Attr: FilterClause.fieldPickerTitle

### Description
The title for the [field-picker](FieldPicker.md#class-fieldpicker) select-item.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.operatorPickerTitle

### Description
The title for the operator-picker select-item.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.operatorPickerProperties

### Description
Properties to combine with the [FilterClause.operatorPicker](#attr-filterclauseoperatorpicker) autoChild FormItem.

**Flags**: IR

---
## Attr: FilterClause.validateOnChange

### Description
If true (the default), validates the entered value when it changes, to make sure it is a a valid value of its type (valid string, number, and so on). No other validation is carried out. If you switch this property off, it is still possible to validate the `FilterClause` by calling [FilterClause.validate](#method-filterclausevalidate) from your own code.

**Flags**: IR

---
## Attr: FilterClause.valueSetHint

### Description
A hint to show in the value-item when using an operator that takes an array of values.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.showFieldTitles

### Description
If true (the default), show field titles in the drop-down box used to select a field for querying. If false, show actual field names instead.

**Flags**: IR

---
## Attr: FilterClause.fieldPicker

### Description
AutoChild for the [FormItem](FormItem.md#class-formitem) that allows a user to pick a DataSource field when creating filter clauses.

This will be a [SelectItem](SelectItem.md#class-selectitem) by default, or a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) if [FilterBuilder.fieldDataSource](FilterBuilder.md#attr-filterbuilderfielddatasource) has been specified.

**Flags**: IR

---
## Attr: FilterClause.valueItemListHint

### Description
A hint to show in the value-item when using an operator that allows users to select values from a list.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.valueItemTitle

### Description
The title for the value-item.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.operatorPicker

### Description
AutoChild for the [FormItem](FormItem.md#class-formitem) that allows a user to select the operator when creating filter clauses. Each clause will create an operatorPicker automatically. To customize this item, use [FilterClause.operatorPickerProperties](#attr-filterclauseoperatorpickerproperties)

**Flags**: IR

---
## Attr: FilterClause.removeButton

### Description
The clause removal ImgButton that appears before this clause if [FilterClause.showRemoveButton](#attr-filterclauseshowremovebutton) is set.

**Flags**: IR

---
## Attr: FilterClause.removeButtonPrompt

### Description
The hover prompt text for the remove button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.clause

### Description
AutoChild containing the UI for the filter-properties in this FilterClause.

**Flags**: IR

---
## Attr: FilterClause.showRemoveButton

### Description
If set, show a button for this clause allowing it to be removed.

**Flags**: IR

---
## Attr: FilterClause.valueItemTextHint

### Description
A hint to show in the value-item when using an operator that takes user-entered values.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterClause.criterion

### Description
Initial criterion for this FilterClause.

When initialized with a criterion, the clause will be automatically set up for editing the supplied criterion.

Note that an empty or partial criterion is allowed, for example, it may specify [Criterion.fieldName](Criterion.md#attr-criterionfieldname) only and will generate an expression with the operator not chosen.

**Flags**: IRW

---
## Attr: FilterClause.valueItemFieldHint

### Description
A hint to show in the value-item when using an operator that allows users to select field-names from a list.

### Groups

- i18nMessages

**Flags**: IR

---
## Method: FilterClause.getCriterion

### Description
Return the criterion specified by this FilterClause.

### Returns

`[Criteria](../reference_2.md#type-criteria)` — The single criterion for this FilterClause

---
## Method: FilterClause.getFilterBuilder

### Description
Returns the [filterBuilder](FilterBuilder.md#class-filterbuilder) containing this clause, or null if this filterClause is not embedded in a filterBuilder.

---
## Method: FilterClause.getValueFieldProperties

### Description
Override to return properties for the FormItem(s) used for the "value" field displayed in this filterClause.

Default implementation simply calls [FilterBuilder.getValueFieldProperties](FilterBuilder.md#method-filterbuildergetvaluefieldproperties) on the filterBuilder in which this clause is displayed.

Note that the [Operator.valueType](Operator.md#attr-operatorvaluetype) impacts when this method is called. For operators with valueType `"fieldType"` or `"custom"`, a single value field is displayed. For operators with valueType `"valueRange"` two value-field items are displayed (one for the start and one for the end position). The `valueItemType` parameter may be used to determine which form item is being generated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [FieldType](../reference_2.md#type-fieldtype) | false | — | type of the DataSource field for this filter row |
| fieldName | [String](#type-string) | false | — | name of the DataSource field for this filter row |
| operatorId | [OperatorId](../reference.md#type-operatorid) | false | — | [OperatorId](../reference.md#type-operatorid) for the chosen operator |
| itemType | [ValueItemType](../reference.md#type-valueitemtype) | false | — | What valueItem is being generated. |

### Returns

`[FormItem Properties](#type-formitem-properties)` — properties for the value field

---
## Method: FilterClause.validate

### Description
Validate this clause.

### Returns

`[Boolean](#type-boolean)` — true if if the clause is valid, false otherwise

---
## Method: FilterClause.remove

### Description
Remove this clause by destroy()ing it.

---
## Method: FilterClause.getFieldOperators

### Description
Get the list of [operatorIds](../reference.md#type-operatorid) that are valid for this field. By default, calls through to the same method on [filterBuilder](FilterBuilder.md#method-filterbuildergetfieldoperators), which defaults to all operators returned by [DataSource.getFieldOperators](DataSource.md#method-datasourcegetfieldoperators).

Called whenever the fieldName is changed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | the name of the field for which to return the set of available operators |

### Returns

`[Array of OperatorId](#type-array-of-operatorid)` — valid operators for this field

---
