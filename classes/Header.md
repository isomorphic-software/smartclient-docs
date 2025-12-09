# Header Documentation

[← Back to API Index](../reference.md)

---

## Class: Header

*Inherits from:* [ToolStrip](ToolStrip.md#class-toolstrip)

### Description
Component for showing a header with an optional [title](#attr-headertitle). Styling matches a [HeaderItem](HeaderItem.md#class-headeritem).

This header is a special type of ToolStrip, so any ToolStrip controls can be added to the Header. Consider also the SectionStack and SectionHeader if you want expand/collapse behavior or multiple sections.

---
## Attr: Header.titleLabel

### Description
Label autoChild for [title](#attr-headertitle) display.

This can be customized via the standard [AutoChild](../reference.md#type-autochild) pattern.

**Flags**: IR

---
## Attr: Header.title

### Description
Title to show for the header. If configured, a Label is automatically created as the first member using the style `headerItem` to match the styling of the header itself and a [HeaderItem](HeaderItem.md#class-headeritem).

### See Also

- [Header.titleLabel](#attr-headertitlelabel)

**Flags**: IWR

---
## Attr: Header.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Method: Header.setTitle

### Description
Setter for the [title](#attr-headertitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | the new title HTML. |

---
