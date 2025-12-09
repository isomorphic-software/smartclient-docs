# SelectItemEditProxy Documentation

[← Back to API Index](../reference.md)

---

## Class: SelectItemEditProxy

*Inherits from:* [FormItemEditProxy](FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [SelectItems](SelectItem.md#class-selectitem) and [ComboBoxItems](ComboBoxItem.md#class-comboboxitem) when editMode is enabled.

### Groups

- devTools

---
## Method: SelectItemEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's valueMap one-per-line as specified in [FormItemEditProxy.valueMapDisplaySeparatorChar](FormItemEditProxy.md#attr-formitemeditproxyvaluemapdisplayseparatorchar). Current value(s) is indicated with [FormItemEditProxy.valueMapSelectedChar](FormItemEditProxy.md#attr-formitemeditproxyvaluemapselectedchar).

---
## Method: SelectItemEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's valueMap and current value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component valueMap |

---
