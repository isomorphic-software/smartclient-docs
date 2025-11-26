# FieldPickerWindow Documentation

[← Back to API Index](../reference.md)

---

## Class: FieldPickerWindow

*Inherits from:* [Window](Window.md#class-window)

### Description
A dialog for picking fields to display from among the available fields.

This is typically useful in scenarios where there are many more fields than can reasonably fit on screen. The application can start off displaying a few of the fields by default (such as the most commonly-needed fields), and show a FieldPickerWindow to allow the user to customize which fields to display as well as the order in which to display them.

---
## Attr: FieldPickerWindow.title

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPickerWindow.fieldPicker

### Description
A [FieldPicker](FieldPicker.md#class-fieldpicker) for altering the working field-set in a [Data-bound component](../reference.md#interface-databoundcomponent).

**Flags**: IR

---
## Attr: FieldPickerWindow.autoDismiss

### Description
By default, a FieldPickerWindow will close automatically if the mouse is clicked outside of it. To have the window shown with true modality, set this attribute to false.

**Flags**: IR

---
