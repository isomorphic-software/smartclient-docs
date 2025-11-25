# TabSetEditProxy Documentation

[← Back to API Index](../main.md)

---

## Class: TabSetEditProxy

*Inherits from:* [CanvasEditProxy](../main.md#class-canvaseditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [TabSet](TabSet.md#class-tabset) objects when editMode is enabled.

### Groups

- devTools

---
## Method: TabSetEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns a comma-separated list of tab titles. A " \[x\]" suffix is added for any tab with `canClose` enabled.

---
## Method: TabSetEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Takes a comma-separated list of tab titles. Add " \[x\]" to a title to enable `canClose` for the tab.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component state |

---
