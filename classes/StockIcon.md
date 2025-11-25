# StockIcon Documentation

[← Back to API Index](../main.md)

---

## Attr: StockIcon.fromSrc

### Description
An [SCImgURL](../main.md#type-scimgurl) that resolves to a known image file-path. When that file-path is requested at runtime, it will be mapped to this stockIcon and replaced with the icon represented by [StockIcon.src](#attr-stockiconsrc).

This attribute is optional, but most built-in stockIcons set this value to one of the image-paths in a skin's _images_ directory (\[SKINIMG\] prefix).

Values applied to this property should be either a fixed path or a relative path prefixed with a shortcut like \[APPIMG\] or \[SKINIMG\]. If your files are relative to your application bootstrap, use \[APP\] as a prefix, because image-paths like "icons/logo.png" are not relative to your page, as you might expect - instead, they're relative to your [appImgDir](Page.md#classmethod-pagegetappimgdir) which is typically \[APP\]/images/.

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: StockIcon.group

### Description
Optional name of a [group](#object-stockicongroup) to which this stockIcon belongs. Can be used for filtering or grouped-display in widgets like the [ImagePicker](#class-imagepicker).

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: StockIcon.src

### Description
The current source assigned to this stockIcon. When developers use the [name](#attr-stockiconname) of a stockIcon as the src-string for any [image-property](../main.md#type-scimgurl), this is the image-src that will be used.

When [StockIcon.fromSrc](#attr-stockiconfromsrc) is set, as it is for most built-in stockIcons, any request for the file-path it represents is mapped to this stockIcon and will render `stockIcon.src` instead.

If this attribute is set, it serves as an initial default.

If this attribute is not set, the default for most built-in icons, it will default to the full-path represented by the `stockIcon.fromSrc`.

You may set this attribute to the special value "empty" to provide a StockIcon which has no mapping and will not render any HTML by default, unless you assign a different src via a call to [Media.updateIconMappings](Media.md#classmethod-mediaupdateiconmappings) or in an [IconSet](../main.md#object-iconset) passed to [Media.useMedia](Media.md#classmethod-mediausemedia). In this way, if one skin applies a src for this stockIcon, it will be shown - if another skin doesn't apply a src, it won't render HTML at all. For example, a Button would not show empty space where the icon should be.

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: StockIcon.index

### Description
Optional index used for sorting in some widgets like the [ImagePicker](#class-imagepicker).

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: StockIcon.name

### Description
The unique name for this icon, which must be a valid JavaScript Identifier and may be used by developers as the src-string for any [image-property](../main.md#type-scimgurl), to show whatever image is [currently assigned](#attr-stockiconsrc) to that stockIcon-name. For example, [button.icon](StatefulCanvas.md#attr-statefulcanvasicon): "Edit" or [img.src](Img.md#attr-imgsrc): "Accept"

### Groups

- media
- stockIcons

**Flags**: IR

---
