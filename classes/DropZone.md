# DropZone Documentation

[← Back to API Index](../reference.md)

---

## Class: DropZone

*Inherits from:* [Label](Label.md#class-label)

### Description
Base class for drop zones that accept HTML5 drag-and-drop of files and/or content.

DropZone extends Label (StatefulCanvas), providing standard state-based styling for drag interactions. Subclasses can accept file drops ([canDropFiles](#candropfiles)), content drops ([canDropContent](#candropcontent)), or both.

For file-specific features like thumbnails, progress bars, and rich validation, see [FileDropZone](FileDropZone.md#class-filedropzone). For skin snapshot import, see [SkinSnapshotDropZone](#class-skinsnapshotdropzone).

---
## ClassAttr: DropZone.emptyDropAreaMessage

### Description
Default message shown when the drop zone is empty.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DropZone.baseStyle

### Description
Base CSS class for the drop zone. Supports state suffixes: Over, Disabled.

**Flags**: IR

---
## Attr: DropZone.acceptedFileTypes

### Description
Array of accepted MIME types (e.g., \["image/\*", "application/pdf"\]). If null, all file types are accepted when [DropZone.canDropFiles](#attr-dropzonecandropfiles) is true.

**Flags**: IR

---
## Attr: DropZone.canDropFiles

### Description
Whether this drop zone accepts file drops from the desktop. When true, the [DropZone.fileDrop](#method-dropzonefiledrop) notification fires when files are dropped.

**Flags**: IR

---
## Attr: DropZone.align

### Description
Horizontal alignment for drop zone content.

**Flags**: IR

---
## Attr: DropZone.canDropContent

### Description
Whether this drop zone accepts content drops (text, HTML) from other applications. When true, the [DropZone.contentDrop](#method-dropzonecontentdrop) notification fires when content is dropped.

**Flags**: IR

---
## Attr: DropZone.valign

### Description
Vertical alignment for drop zone content.

**Flags**: IR

---
## Method: DropZone.contentDrop

### Description
Notification fired when content (text, HTML) is dropped from another application. Only fires when [DropZone.canDropContent](#attr-dropzonecandropcontent) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| content | [String](#type-string) | false | — | The dropped content |

---
## Method: DropZone.fileDrop

### Description
Notification fired when files are dropped onto the drop zone. Only fires when [DropZone.canDropFiles](#attr-dropzonecandropfiles) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| files | [Array of File](#type-array-of-file) | false | — | JavaScript File objects that were dropped |

---
