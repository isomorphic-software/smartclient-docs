# SelectOtherItem Documentation

[← Back to API Index](../reference.md)

---

## Class: SelectOtherItem

### Description
FormItem that shows a list of options, plus an "Other..." option that allows them to enter another value.

Note - SelectOtherItem does not support using an [optionDataSource](SelectItem.md#attr-selectitemoptiondatasource), instead, use a normal [SelectItem](SelectItem.md#class-selectitem) and use the [specialValues](SelectItem.md#attr-selectitemspecialvalues) to implement a way to add new DataSource records to the [optionDataSource](SelectItem.md#attr-selectitemoptiondatasource). This creates a UI more appropriate to [optionDataSource](SelectItem.md#attr-selectitemoptiondatasource): the [otherValue](#attr-selectotheritemothervalue) option or options can be placed at the top of the list, so that scrolling to the bottom of a long list is not required. In addition, the [specialValues](SelectItem.md#attr-selectitemspecialvalues) system allows you to open a custom form or other UI for adding new DataSource records, rather than just the simple single-value input dialog of SelectOtherItem.

---
## Attr: SelectOtherItem.selectOtherPrompt

### Description
Title to show in prompt for "other" value. Note this is a dynamic string. JavaScript content is supported within `${...}` tags, with local variables for `item` (a pointer to this item) and `value` a pointer to the currently selected item value.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SelectOtherItem.separatorTitle

### Description
Title for the separator between normal items and the `Other...` item in the drop down list. Selecting this item will not change the FormItem's value.

### Groups

- appearance

**Flags**: IRW

---
## Attr: SelectOtherItem.otherTitle

### Description
Title for the `Other...` item. When this item is selected, the user will be shown a prompt allowing them to enter a new value for the item.

### Groups

- appearance
- i18nMessages

**Flags**: IRW

---
## Attr: SelectOtherItem.otherValue

### Description
Data value for the `Other...` item. If necessary this value may be changed to ensure it doesn't collide with any data values in this item's [valueMap](FormItem.md#attr-formitemvaluemap).

### Groups

- appearance

**Flags**: IRWA

---
## Attr: SelectOtherItem.dialogWidth

### Description
Width for the "other value" prompt dialog.

**Flags**: IRW

---
## Attr: SelectOtherItem.separatorValue

### Description
Value for the separator item between normal items and the `Other...` value. If necessary the value may be changed to ensure it doesn't collide with any data values in this item's [valueMap](FormItem.md#attr-formitemvaluemap).

### Groups

- appearance

**Flags**: IRWA

---
