# RichTextCanvas Documentation

[← Back to API Index](../reference.md)

---

## Class: RichTextCanvas

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Canvas to be used for Rich Text Editing

---
## Attr: RichTextCanvas.styleName

### Description
The CSS class applied to this widget as a whole. The editable HTML within this widget will appear with this styling applied to it, but it should be noted that this css class is not part of that HTML, so applying the generated content to other components will not pick up styling attributes defined in this class automatically.

**Flags**: IRW

---
## Attr: RichTextCanvas.useDesignMode

### Description
Should this editor use a separate IFRAME with special cross-browser support for editing HTML content? By default, the value is auto-detected according to browser details. If set to false, the editor falls back to normal browser contentEditable behavior, which may differ between browsers.

**Flags**: IRA

---
## Attr: RichTextCanvas.moveFocusOnTab

### Description
If the user presses the "Tab" key, should focus be taken from this editor? If set to `false` a "Tab" keypress will cause a Tab character to be inserted into the text, and focus will be left in the edit area.

**Flags**: IRW

---
## Attr: RichTextCanvas.styleWithCSS

### Description
When true, applies style attributes in markup instead of presentation elements.

**Flags**: IRA

---
## Method: RichTextCanvas.convertSelectionToUnorderedList

### Description
Converts the selection to an unordered list. If the selection is within an ordered list, the ordered list is converted to an unordered list.

---
## Method: RichTextCanvas.applyListProperties

### Description
Applies the given [ListProperties](../reference.md#object-listproperties) to the currently selected HTML list, if any. If there is no list selected, then this method does nothing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| listProperties | [ListProperties](#type-listproperties) | false | — | the list configuration to apply |

**Flags**: A

---
## Method: RichTextCanvas.convertSelectionToOrderedList

### Description
Converts the selection to an ordered list. If the selection is within an unordered list, the unordered list is converted to an ordered list.

---
## Method: RichTextCanvas.outdentSelection

### Description
Decreases the indent for the currently selected paragraph. Within a list, decreases the list level or breaks out of the list.

---
## Method: RichTextCanvas.indentSelection

### Description
Increases the indent for the currently selected paragraph. Within a list, increases the list level.

---
