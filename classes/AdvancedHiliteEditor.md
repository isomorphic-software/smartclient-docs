# AdvancedHiliteEditor Documentation

[← Back to API Index](../reference.md)

---

## Class: AdvancedHiliteEditor

*Inherits from:* [VStack](../reference.md#class-vstack)

### Description
A widget for editing a single, advanced [hilite rule](HiliteRule.md#class-hiliterule) for use by [dataBoundComponents](../reference.md#interface-databoundcomponent). Where a simple hilite provides configuration of a single criterion and either foreground or background color for application to a single field, an advanced hilite can specify more complex criteria which can both test and affect multiple fields and allow both background and foreground colors to be specified in a single rule.

_**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](../kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

---
## Attr: AdvancedHiliteEditor.invalidHilitePrompt

### Description
The message to show when the user clicks "Save" without entering any criteria.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.filterGroupTitle

### Description
The title for the Filter group.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.cancelButtonTitle

### Description
The title text for the [cancelButton](#attr-advancedhiliteeditorcancelbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.callback

### Description
The callback to fire when the [saveButton](#attr-advancedhiliteeditorsavebutton) is clicked.

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.appearanceGroupTitle

### Description
The title for the Appearance group.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.cancelButton

### Description
AutoChild [ImgButton](ImgButton.md#class-imgbutton) that cancels this AdvancedHiliteEditor without saving any changes, firing the [callback](#attr-advancedhiliteeditorcallback) with a null parameter.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `advancedHiliteEditor.cancelButtonProperties`.

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.filterBuilder

### Description
AutoChild [FilterBuilder](FilterBuilder.md#class-filterbuilder) for configuring the criteria for this Hilite.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `advancedHiliteEditor.filterBuilderProperties`.

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.hiliteIcons

### Description
Specifies a list of icons that can be used in hilites.

`hiliteIcons` should be specified as an Array of [SCImgURL](../reference_2.md#type-scimgurl). When present, [hilite rules](HiliteRule.md#class-hiliterule) will offer the user a drop down for picking one of these icons.

If the user picks an icon, the created hiliting rule will have [Hilite.icon](Hilite.md#attr-hiliteicon) set to the chosen icon. [ListGridField.hiliteIconPosition](ListGridField.md#attr-listgridfieldhiliteiconposition) controls where the icon will appear for that field -- the default is that it appears in front of the normal cell content.

**Flags**: IRW

---
## Attr: AdvancedHiliteEditor.hiliteForm

### Description
AutoChild [DynamicForm](DynamicForm.md#class-dynamicform) for configuring the details of this Hilite.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `advancedHiliteEditor.hiliteFormProperties`.

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.targetFieldsItemTitle

### Description
The title for the Target Field(s) picker.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.saveButton

### Description
AutoChild [ImgButton](ImgButton.md#class-imgbutton) that accepts this Hilite and fires the [callback](#attr-advancedhiliteeditorcallback).

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `advancedHiliteEditor.saveButtonProperties`.

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.title

### Description
The title text shown in the header bar of this editor's dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AdvancedHiliteEditor.saveButtonTitle

### Description
The title text for the [saveButton](#attr-advancedhiliteeditorsavebutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Method: AdvancedHiliteEditor.saveHilite

### Description
Save changes and fire the [callback](#attr-advancedhiliteeditorcallback).

---
## Method: AdvancedHiliteEditor.cancelEditing

### Description
Discard changes and fire the [callback](#attr-advancedhiliteeditorcallback) with a null parameter.

---
