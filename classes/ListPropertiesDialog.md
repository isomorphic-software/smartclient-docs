# ListPropertiesDialog Documentation

[← Back to API Index](../reference.md)

---

## Class: ListPropertiesDialog

*Inherits from:* [Window](Window.md#class-window)

### Description
Dialog shown for editing properties of HTML lists in a [RichTextEditor](RichTextEditor.md#class-richtexteditor). Contains a [ListPropertiesPane](ListPropertiesPane.md#class-listpropertiespane).

Cannot be directly used; shown in documentation only for skinning purposes.

---
## Attr: ListPropertiesDialog.cancelButton

### Description
The Cancel button. When clicked, the [cancelClick](#method-listpropertiesdialogcancelclick) event is fired.

[cancelButtonTitle](#attr-listpropertiesdialogcancelbuttontitle) is a [passthrough](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) for the button's [title](Button.md#attr-buttontitle).

**Flags**: R

---
## Attr: ListPropertiesDialog.title

### Description
The title of this ListPropertiesDialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListPropertiesDialog.applyButton

### Description
The Apply button. When clicked, the [applyClick](#method-listpropertiesdialogapplyclick) event is fired.

[applyButtonTitle](#attr-listpropertiesdialogapplybuttontitle) is a [passthrough](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) for the button's [title](Button.md#attr-buttontitle).

**Flags**: R

---
## Attr: ListPropertiesDialog.listPropertiesPane

### Description
The [ListPropertiesPane](ListPropertiesPane.md#class-listpropertiespane) contained by this ListPropertiesDialog.

**Flags**: R

---
## Attr: ListPropertiesDialog.cancelButtonTitle

### Description
The title of the [Cancel button](#attr-listpropertiesdialogcancelbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListPropertiesDialog.applyButtonTitle

### Description
The title of the [Apply button](#attr-listpropertiesdialogapplybutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Method: ListPropertiesDialog.applyClick

### Description
Notification method fired when the [Apply button](#attr-listpropertiesdialogapplybutton) is clicked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| listProperties | [ListProperties](#type-listproperties) | false | — | the list properties to apply |

---
## Method: ListPropertiesDialog.cancelClick

### Description
Notification method fired when the [Cancel button](#attr-listpropertiesdialogcancelbutton) is clicked.

---
