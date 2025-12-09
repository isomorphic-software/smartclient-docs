# ImgTab Documentation

[← Back to API Index](../reference.md)

---

## Class: ImgTab

*Inherits from:* [StretchImgButton](StretchImgButton.md#class-stretchimgbutton)

### Description
Specialized StretchImgButton used by TabSet/TabBar for tabs

---
## Attr: ImgTab.skinImgDir

### Description
Base path for the images. **Note** that when used within a TabSet, the [TabSet.tabBarPosition](TabSet.md#attr-tabsettabbarposition) is appended as an additional path segment, yielding "images/Tab/top/" et al.

**Flags**: IRW

---
## Attr: ImgTab.showRollOver

### Description
Should we visibly change state when the mouse goes over this tab

**Flags**: IRW

---
## Attr: ImgTab.align

### Description
Alignment of title text

### Groups

- positioning

**Flags**: IRW

---
## Attr: ImgTab.labelSkinImgDir

### Description
Base path for images shown within this ImgTab's label. This will be used for icons (such as the close icon) by default.

**Flags**: IRW

---
## Attr: ImgTab.showFocus

### Description
Should we visibly change state when the tab receives keyboard focus?

**Deprecated**

**Flags**: IRW

---
## Attr: ImgTab.showFocused

### Description
Should we visibly change state when the tab receives keyboard focus?

**Flags**: IRW

---
## Attr: ImgTab.capSize

### Description
How big are the end pieces by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: ImgTab.baseStyle

### Description
—

**Flags**: IR

---
## Attr: ImgTab.src

### Description
Base URL for tab images

**Flags**: IRW

---
## Attr: ImgTab.titleStyle

### Description
Like [StretchImgButton.titleStyle](StretchImgButton.md#attr-stretchimgbuttontitlestyle), can set to provide a separate style for the title text.

If set and the ImgTab is [vertical](StretchImgButton.md#attr-stretchimgbuttonvertical), a "v" will be automatically prepended to the style name (hence "tabTitle" -> "vtabTitle").

**Flags**: IR

---
