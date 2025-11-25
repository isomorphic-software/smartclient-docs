# TextItemEditProxy Documentation

[← Back to API Index](../main.md)

---

## Class: TextItemEditProxy

*Inherits from:* [FormItemEditProxy](FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [TextItems](TextItem.md#class-textitem) and [StaticTextItems](StaticTextItem.md#class-statictextitem) when editMode is enabled.

### Groups

- devTools

---
## Method: TextItemEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `defaultValue`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component defaultValue |

---
## Method: TextItemEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's `defaultValue`.

---
