# ListPropertiesPane Documentation

[← Back to API Index](../reference.md)

---

## Class: ListPropertiesPane

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
Pane containing controls for editing the style of HTML lists in a [RichTextEditor](RichTextEditor.md#class-richtexteditor).

Cannot be directly used; shown in documentation only for skinning purposes.

---
## Attr: ListPropertiesPane.startNumberForm

### Description
Form used to show the [startNumberField](#attr-listpropertiespanestartnumberfield) for configuring the starting value of a list.

**Flags**: R

---
## Attr: ListPropertiesPane.sampleTileLayout

### Description
Shows available bullet options as a series of tiles.

**Flags**: R

---
## Attr: ListPropertiesPane.startNumberFieldTitle

### Description
The [title](FormItem.md#attr-formitemtitle) of the [startNumberField](#attr-listpropertiespanestartnumberfield).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListPropertiesPane.sampleTile

### Description
Tile used to demonstrate each bullet style.

**Flags**: R

---
## Attr: ListPropertiesPane.startNumberField

### Description
[SpinnerItem](SpinnerItem.md#class-spinneritem) used to modify the starting value of the list.

[startNumberFieldTitle](#attr-listpropertiespanestartnumberfieldtitle) is a [passthrough](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) for the field's [title](FormItem.md#attr-formitemtitle).

**Flags**: R

---
## Attr: ListPropertiesPane.listProperties

### Description
The properties corresponding to the currently-selected list configuration.

**Flags**: IRW

---
## Method: ListPropertiesPane.listPropertiesChanged

### Description
Notification method fired when the pane's [ListPropertiesPane.listProperties](#attr-listpropertiespanelistproperties) changes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| listProperties | [ListProperties](#type-listproperties) | false | — | the new list configuration properties |

---
