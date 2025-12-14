# HiliteEditor Documentation

[← Back to API Index](../reference.md)

---

## Class: HiliteEditor

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A widget for defining and editing a set of [hilite rules](HiliteRule.md#class-hiliterule) for use by [dataBoundComponents](../reference.md#interface-databoundcomponent). Presents a list of available fields and allows editing of simple hilites directly and more complex hilites via [AdvancedHiliteEditor](AdvancedHiliteEditor.md#class-advancedhiliteeditor)s.

_**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](../kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

---
## Attr: HiliteEditor.hiliteRule

### Description
AutoChild [HiliteRule](HiliteRule.md#class-hiliterule) used to create new simple hilites.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteEditor.hiliteRuleProperties`.

**Flags**: IR

---
## Attr: HiliteEditor.fieldList

### Description
AutoChild [ListGrid](ListGrid_1.md#class-listgrid) showing the list of fields to create hilites for.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteEditor.fieldListProperties`.

**Flags**: IR

---
## Attr: HiliteEditor.callback

### Description
The callback to fire when [HiliteEditor.saveHilites](#method-hiliteeditorsavehilites) is called.

**Flags**: IR

---
## Attr: HiliteEditor.addAdvancedRuleButton

### Description
AutoChild [IButton](../reference.md#class-ibutton) that opens an [AdvancedHiliteEditor](AdvancedHiliteEditor.md#class-advancedhiliteeditor) to create a new advanced rule.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteEditor.addAdvancedRuleButtonProperties`.

**Flags**: IR

---
## Attr: HiliteEditor.addAdvancedRuleButtonTitle

### Description
The title text for the [add advanced rule](#attr-hiliteeditoraddadvancedrulebutton) button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteEditor.availableFieldsColumnTitle

### Description
The title for the 'Available Fields' column in the [fieldList](#attr-hiliteeditorfieldlist).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteEditor.cancelButton

### Description
AutoChild [ImgButton](ImgButton.md#class-imgbutton) that cancels this editor without saving any changes, firing the [callback](#attr-hiliteeditorcallback) with a null parameter.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteEditor.cancelButtonProperties`.

**Flags**: IR

---
## Attr: HiliteEditor.hiliteIcons

### Description
Specifies a list of icons that can be used in [hilites](../reference.md#object-hilite).

`hiliteIcons` should be specified as an Array of [SCImgURL](../reference.md#type-scimgurl). When present, [HiliteRule](HiliteRule.md#class-hiliterule)s will offer the user a drop down for picking one of these icons.

If the user picks an icon, the created hiliting rule will have [Hilite.icon](Hilite.md#attr-hiliteicon) set to the chosen icon. [ListGridField.hiliteIconPosition](ListGridField.md#attr-listgridfieldhiliteiconposition) controls where the icon will appear for that field -- the default is that it appears in front of the normal cell content.

**Flags**: IRW

---
## Attr: HiliteEditor.cancelButtonTitle

### Description
The title text for the [cancel button](#attr-hiliteeditorcancelbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteEditor.saveButtonTitle

### Description
The title text for the [saveButton](#attr-hiliteeditorsavebutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteEditor.saveButton

### Description
AutoChild [ImgButton](ImgButton.md#class-imgbutton) that saves the hilites in this editor and fires the [callback](#attr-hiliteeditorcallback).

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteEditor.saveButtonProperties`.

**Flags**: IR

---
## Method: HiliteEditor.saveHilites

### Description
Save the set of Hilites and fire the [callback](#attr-hiliteeditorcallback).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | the function to call when saving is complete |

---
## Method: HiliteEditor.clearHilites

### Description
Clear all Hilites from the editor.

---
## Method: HiliteEditor.setHilites

### Description
Initialize this editor with a set of Hilites.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | the array of hilite objects to apply |

---
## Method: HiliteEditor.removeRule

### Description
Removes the passed [HiliteRule](HiliteRule.md#class-hiliterule) from this editor.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hiliteRule | [HiliteRule](#type-hiliterule) | false | — | the hiliteRule to remove |

---
