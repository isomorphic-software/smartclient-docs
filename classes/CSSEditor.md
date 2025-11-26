# CSSEditor Documentation

[← Back to API Index](../reference.md)

---

## Class: CSSEditor

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A [Layout](Layout.md#class-layout)-based component for editing groups of [styling settings](../reference.md#object-stylesetting). Changes are reflected in a preview canvas and can be retrieved as a block of [properties](#method-csseditorgetcssproperties) or as a string of [CSS text](#method-csseditorgetcsstext).

**Note:** this feature requires [SmartClient Enterprise](https://www.smartclient.com/product/).

---
## Attr: CSSEditor.groups

### Description
The set of [StyleGroup](../reference.md#object-stylegroup)s to show for editing.

**Flags**: IRW

---
## Attr: CSSEditor.values

### Description
The set of values to apply to editors.

**Flags**: IRW

---
## Method: CSSEditor.editCancelled

### Description
Notification fired when the cancelButton is clicked.

---
## Method: CSSEditor.getCSSText

### Description
Returns the values being edited as a single string of [CSSText](../reference_2.md#type-csstext).

### Returns

`[CSSText](../reference_2.md#type-csstext)` — string of CSS

---
## Method: CSSEditor.getCSSProperties

### Description
Returns the values being edited as a block of CSS properties.

### Returns

`[Object](../reference.md#type-object)` — an ordinary object representing the current values from the editor

---
## Method: CSSEditor.editComplete

### Description
Notification fired when the okButton is clicked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [Object](../reference.md#type-object) | false | — | ordinary JS object with the final settings |

---
## Method: CSSEditor.valuesChanged

### Description
Notification fired when values in the editor are changed. The latest values are passed in the `values` parameter. You can use [getCSSText()](#method-csseditorgetcsstext) to retrieve the values as a single piece of [CSS-text](../reference_2.md#type-csstext).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | ordinary JS object with properties representing the settings following an edit |

---
## Method: CSSEditor.setGroups

### Description
Set the list of [style-groups](../reference.md#object-stylegroup) to display for editing. The parameter can be an array of valid StyleGroups (or objects with at least a "name" property), or a list of the names of predefined groups.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groups | [Array of Object](#type-array-of-object)|[Array of String](#type-array-of-string) | false | — | array of StyleGroup objects or names |

---
## Method: CSSEditor.clearGroups

### Description
Clear the current [style-groups](../reference.md#object-stylegroup) from the editor.

---
