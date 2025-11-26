# DateItemEditProxy Documentation

[← Back to API Index](../reference.md)

---

## Class: DateItemEditProxy

*Inherits from:* [FormItemEditProxy](FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [DateItem](DateItem.md#class-dateitem) when editMode is enabled.

### Groups

- devTools

---
## Method: DateItemEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's value using [Date.toShortDate](Date.md#method-datetoshortdate).

---
## Method: DateItemEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `defaultValue`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component default value |

---
