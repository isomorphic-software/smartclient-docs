# HiddenItem Documentation

[← Back to API Index](../reference.md)

---

## Class: HiddenItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
HiddenItems track a value but have no visible appearance and do not take up space in the form layout.

When using SmartClient databinding it is usually not necessary to use a HiddenItem, since the DynamicForm will track values for which no actual form control exists, and will submit these 'extra' values when [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) is called. HiddenItems only apply to forms that are submitted like ordinary HTML forms, via the [DynamicForm.submitForm](DynamicForm.md#method-dynamicformsubmitform) method.

---
## Attr: HiddenItem.alwaysFetchMissingValues

### Description
If this form item has a specified [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource) and [FormItem.fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) is true, when the item value changes, a fetch will be performed against the optionDataSource to retrieve the related record if [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) is specified and the new item value is not present in any valueMap explicitly specified on the item.

Setting this property to true means that a fetch will occur against the optionDataSource to retrieve the related record even if [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) is unset, or the item has a valueMap which explicitly contains this field's value.

An example of a use case where this might be set would be if [FormItem.formatValue](FormItem.md#method-formitemformatvalue) or [FormItem.formatEditorValue](FormItem.md#method-formitemformateditorvalue) were written to display properties from the [selected record](FormItem.md#method-formitemgetselectedrecord).

Note - for efficiency we cache the associated record once a fetch has been performed, meaning if the value changes, then reverts to a previously seen value, we do not kick off an additional fetch even if this property is true. If necessary this cache may be explicitly invalidated via a call to [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

Note: For hiddenItem [fetchMissingValues](#attr-hiddenitemfetchmissingvalues) is defaulted to `false` so developers wishing to get access to the record related to the current hiddenItem value would need to explicitly set both that property, and this one to true.

### Groups

- display_values

**Flags**: IRWA

---
## Attr: HiddenItem.colSpan

### Description
hidden fields don't take up any columns

### Groups

- appearance

**Flags**: IRW

---
## Attr: HiddenItem.rowSpan

### Description
hidden fields don't take up any rows

### Groups

- appearance

**Flags**: IRW

---
## Attr: HiddenItem.showTitle

### Description
we never show a separate title cell for hidden fields

### Groups

- appearance

**Flags**: IRW

---
## Attr: HiddenItem.fetchMissingValues

### Description
If this form item has a specified [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), should the item ever perform a fetch against this dataSource to retrieve the related record.

This is disabled by default for hiddenItems as there is typically no need to perform a fetch and retrieve a display-field value to show the user for a hidden item. This does mean that if a developer needs access to the related record for a hidden-item's value, they will need to enable both this setting and [FormItem.alwaysFetchMissingValues](FormItem.md#attr-formitemalwaysfetchmissingvalues).

### Groups

- display_values

### See Also

- [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource)
- [FormItem.getSelectedRecord](FormItem.md#method-formitemgetselectedrecord)
- [FormItem.filterLocally](FormItem.md#attr-formitemfilterlocally)

**Flags**: IRWA

---
