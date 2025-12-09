# IconImgButton Documentation

[← Back to API Index](../reference.md)

---

## Class: IconImgButton

*Inherits from:* [ImgButton](ImgButton.md#class-imgbutton)

### Description
A specialized subclass of [ImgButton](ImgButton.md#class-imgbutton) designed to show an icon that launches a [context menu](Canvas.md#attr-canvascontextmenu) when clicked. The icon is specified as the [src](#attr-iconimgbuttonsrc) property.

### See Also

- [StatefulCanvas.showMenuOnClick](StatefulCanvas.md#attr-statefulcanvasshowmenuonclick)

---
## Attr: IconImgButton.showMenuOnClick

### Description
If true, this widget will fire [showContextMenu()](Canvas.md#method-canvasshowcontextmenu) to show the [context menu](Canvas.md#attr-canvascontextmenu) if one is defined, rather than [click()](Canvas.md#method-canvasclick), when the left mouse is clicked.

Note that this property has a different interpretation in [IconButton](../reference.md#class-iconbutton) as [IconButton.showMenuOnClick](RibbonButton.md#attr-ribbonbuttonshowmenuonclick).

### Groups

- menu

**Flags**: IRW

---
## Attr: IconImgButton.src

### Description
The base filename or stateful image configuration for the image. Note that as the [state](StatefulCanvas.md#attr-statefulcanvasstate) of the component changes, the image displayed will be updated as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images).

### Groups

- appearance

**Flags**: IRW

---
