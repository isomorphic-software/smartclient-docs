# SearchForm Documentation

[← Back to API Index](../reference.md)

---

## Class: SearchForm

*Inherits from:* [DynamicForm](DynamicForm.md#class-dynamicform)

### Description
A SearchForm is a DynamicForm specialized for a user to enter search criteria.

All DynamicForm properties and methods work on SearchForm. SearchForm extends and specializes DynamicForm for searching; for example, SearchForm sets `hiliteRequiredFields` false by default because fields are typically not required in a search.

### See Also

- [DynamicForm](DynamicForm.md#class-dynamicform)

---
## Attr: SearchForm.canEditFieldAttribute

### Description
This property is overridden in SearchForm to allow editing of dataSource fields marked as `canFilter:true` by default.

### See Also

- [DataBoundComponent.canEditFieldAttribute](DataBoundComponent.md#attr-databoundcomponentcaneditfieldattribute)

**Flags**: IRA

---
## Attr: SearchForm.showFilterFieldsOnly

### Description
If this attribute is true any [canFilter:false](DataSourceField.md#attr-datasourcefieldcanfilter) fields specified on the dataSource will not be shown unless explicitly included in this component's [fields array](DataBoundComponent.md#attr-databoundcomponentfields)

**Flags**: IRWA

---
## Attr: SearchForm.searchOnEnter

### Description
Causes the [SearchForm.search](#method-searchformsearch) event to be triggered when the user presses the Enter key in any field of this form.

This is the same as the [saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) property of [DynamicForm](DynamicForm.md#class-dynamicform) - setting either property to true will cause the [SearchForm.search](#method-searchformsearch) event to fire on Enter keypress.

### Groups

- search

**Flags**: IRW

---
## Attr: SearchForm.storeDisplayValues

### Description
For editable fields with a specified [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) and [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), if the user selects a new value (typically from PickList based item such as a SelectItem), should the selected displayValue be updated on the record being edited in addition to the value for the actual item.  
Note that this only applies for fields using [local display field values](FormItem.md#attr-formitemuselocaldisplayfieldvalue).

Overriden to be false for `searchForm`s. It is typically not necessary to have the display value as well as the data value be included in generated criteria when a user selects a new value from a field with a specified [FormItem.displayField](FormItem.md#attr-formitemdisplayfield).

See [DynamicForm.storeDisplayValues](DynamicForm.md#attr-dynamicformstoredisplayvalues) for more information on this property.

**Flags**: IRWA

---
## Attr: SearchForm.criteriaChangedDelay

### Description
Delay in milliseconds between user changing the criteria in the form and the [SearchForm.criteriaChanged](#method-searchformcriteriachanged) notification method being fired. Set to zero to respond to criteria changes synchronously after [DynamicForm.itemChanged](DynamicForm.md#method-dynamicformitemchanged).

**Flags**: IRWA

---
## Method: SearchForm.criteriaChanged

### Description
Notification method fired when the criteria are modified in this SearchForm. As the user edits values, this method will be fired after a [configurable delay](#attr-searchformcriteriachangeddelay).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference.md#type-criteria) | false | — | Current criteria of the form (matches [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria)) |
| form | [SearchForm](#type-searchform) | false | — | the SearchForm being edited |

---
## Method: SearchForm.search

### Description
Notification event fired indicating that a user is attempting to perform a search. This is fired when a SearchForm is submitted either from a click on a [SubmitItem](../reference.md#class-submititem) in the form, or from an Enter keypress if [SearchForm.searchOnEnter](#attr-searchformsearchonenter) or [DynamicForm.saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference.md#type-criteria) | false | — | the search criteria from the form |
| form | [SearchForm](#type-searchform) | false | — | the form being submitted |

### Groups

- search

### See Also

- [DynamicForm.submit](DynamicForm.md#method-dynamicformsubmit)
- [DynamicForm.submitValues](DynamicForm.md#method-dynamicformsubmitvalues)

---
