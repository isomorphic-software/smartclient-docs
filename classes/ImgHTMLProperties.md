# ImgHTMLProperties Documentation

[← Back to API Index](../reference.md)

---

## Attr: ImgHTMLProperties.imgDir

### Description
Specifies the image-specific image directory to override the default.

**Flags**: IRW

---
## Attr: ImgHTMLProperties.width

### Description
Specifies the width of the image.

**Flags**: IRW

---
## Attr: ImgHTMLProperties.extraStuff

### Description
Specifies the additional attributes to write in the tag. Event-related attributes should be added to [ImgHTMLProperties.eventStuff](#attr-imghtmlpropertieseventstuff) instead to guarantee proper behavior when using SVG via regular .svg image files.

**Flags**: IRW

---
## Attr: ImgHTMLProperties.src

### Description
Specifies the URL of the image local to the skin or application directory.

**Flags**: IRW

---
## Attr: ImgHTMLProperties.name

### Description
Specifies the name of the image. This is an identifier unique to the canvas, and subsequent calls to `[Canvas.getImage](Canvas.md#method-canvasgetimage)` and `[Canvas.setImage](Canvas.md#method-canvassetimage)` with this name will act on the image object created using this `ImgHTMLProperties` object.

**Flags**: IRW

---
## Attr: ImgHTMLProperties.height

### Description
Specifies the height of the image.

**Flags**: IRW

---
## Attr: ImgHTMLProperties.eventStuff

### Description
Specifies the additional event-related attributes to write in the tag.

### See Also

- [ImgHTMLProperties.extraStuff](#attr-imghtmlpropertiesextrastuff)

**Flags**: IRW

---
