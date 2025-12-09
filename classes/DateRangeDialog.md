# DateRangeDialog Documentation

[← Back to API Index](../reference.md)

---

## Class: DateRangeDialog

*Inherits from:* [Window](Window.md#class-window)

### Description
Simple modal dialog for collecting a date range from the end user.

---
## Attr: DateRangeDialog.rangeItem

### Description
—

**Flags**: IR

---
## Attr: DateRangeDialog.clearButton

### Description
Button used for clearing the dialog's values. Note that, since this is an [AutoChild](../reference.md#type-autochild), it can be configured using clearButtonDefaults and clearButtonProperties.

**Flags**: IR

---
## Attr: DateRangeDialog.cancelButtonTitle

### Description
The title for the "Cancel" button on this dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateRangeDialog.okButton

### Description
Button used for accepting the values entered into the dialog. Note that, since this is an [AutoChild](../reference.md#type-autochild), it can be configured using okButtonDefaults and okButtonProperties.

**Flags**: IR

---
## Attr: DateRangeDialog.clearButtonTitle

### Description
The title for the "Clear" button on this dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateRangeDialog.cancelButton

### Description
Button used for cancelling the dialog. Note that, since this is an [AutoChild](../reference.md#type-autochild), it can be configured using cancelButtonDefaults and cancelButtonProperties.

**Flags**: IR

---
## Attr: DateRangeDialog.okButtonTitle

### Description
The title for the "OK" button on this dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateRangeDialog.headerTitle

### Description
The title to display in the header-bar of this Dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassMethod: DateRangeDialog.askForRange

### Description
Helper method to launch a DateRangeDialog to have a date range input by the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| allowRelativeDates | [boolean](../reference.md#type-boolean) | false | — | whether to allow relative date entry via [RelativeDateItem](RelativeDateItem.md#class-relativedateitem)s, default true |
| rangeItemProperties | [DateRangeItem Properties](#type-daterangeitem-properties) | false | — | properties for the DateRangeItem |
| windowProperties | [DateRangeDialog Properties](#type-daterangedialog-properties) | false | — | properties for the Window |
| callback | [DateRangeCallback](#type-daterangecallback) | false | — | method to fire once user has input values, with a single parameter "criterion" of type [Criterion](../reference_2.md#object-criterion) |

---
