# Media Documentation

[← Back to API Index](../reference.md)

---

## Class: Media

### Description
Constants and APIs for managing icons and fonts in your application.

---
## ClassAttr: Media.svgDefaultSize

### Description
The default-size in pixels for any request for an SVG symbol that doesn't provide any sizes (none of width/height/imageWidth/imageHeight on the widget or "size" in the src-string). In this way, unsized SVGs will render at a useable default size, rather than at browser-default size, which is 300x150 and never desirable.

### Groups

- svgSymbols

**Flags**: IR

---
## ClassAttr: Media.svgAutoScale

### Description
When true automatically scales "size" attributes specified in SVG src-strings.

### Groups

- svgSymbols

**Flags**: IR

---
## ClassAttr: Media.iconSets

### Description
A list of [IconSets](../reference.md#object-iconset) that are available for use by passing their names to [Media.useMedia](#classmethod-mediausemedia).

The framework has two builtin IconSets

*   "skin", which does not apply any mappings and uses the icons from the skin's "images/" directory
*   "svg", which installs an _IconSet_, based on Google's Material-Symbols, with [mappings](IconSet.md#attr-iconsetmappings) that replace all framework usage of on-disk image files from the "images/" directory with [SVG symbols](../kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview) from a single .svg file. These SVG graphics are available at various weights and in outlined and filled styles which you can access by including them separated by colons in your call to [useMedia()](#classmethod-mediausemedia) - for example, "svg:100", "svg:filled" or "svg:500:outlined"

### Groups

- media
- stockIcons

**Flags**: IR

---
## ClassAttr: Media.svgUseDefaultSize

### Description
When true, causes SVGs with no divinable size to render at a useable [default size](#classattr-mediasvgdefaultsize), rather than at browser-default size, which is 300x150 and never desirable.

### Groups

- svgSymbols

**Flags**: IR

---
## ClassMethod: Media.getIconSet

### Description
Retrieves an [IconSet](../reference.md#object-iconset) that was previously registered with [addIconSet()](#classmethod-mediaaddiconset) or passed to [useMedia()](#classmethod-mediausemedia).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| iconSet | [String](#type-string)|[IconSet](#type-iconset) | false | — | an [IconSet](../reference.md#object-iconset) or its [name](IconSet.md#attr-iconsetname) |

### Groups

- stockIcons
- media

---
## ClassMethod: Media.useMedia

### Description
Installs an [IconSet](../reference.md#object-iconset) by adding its list of [custom stockIcons](IconSet.md#attr-iconsetstockicons) and/or applying its set of [stockIcon-mappings](IconSet.md#attr-iconsetmappings) that modify the images used by existing [stockIcons](../reference_2.md#object-stockicon).

Typically, this will take effect immediately with no further action by the developer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| iconSet | [String](#type-string)|[IconSet](#type-iconset) | false | — | a new [IconSet](../reference.md#object-iconset), or the [name](IconSet.md#attr-iconsetname) of one previously [registered](#classmethod-mediaaddiconset) |

### Groups

- stockIcons
- media

---
## ClassMethod: Media.getStockIconNames

### Description
Returns an array of the [names](StockIcon.md#attr-stockiconname) of all registered [stockIcons](../reference_2.md#object-stockicon). These are the names which can be used as src-string values for [image attributes](../reference.md#type-scimgurl).

### Groups

- stockIcons
- media

---
## ClassMethod: Media.updateIconMapping

### Description
Updates the [src-string](StockIcon.md#attr-stockiconsrc) currently assigned to the passed [icon-name](StockIcon.md#attr-stockiconname).

Changes the src that will be rendered when the passed icon-name or it's [StockIcon.fromSrc](StockIcon.md#attr-stockiconfromsrc) are used as the value of an [image-src](../reference.md#type-scimgurl) property, such as [Button.icon](Button.md#attr-buttonicon) or [Img.src](Img.md#attr-imgsrc).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | the name of the stockIcon to modify |
| newSrc | [String](#type-string) | false | — | the new [src-string](../reference.md#type-scimgurl) for the passed icon-name |

### Groups

- stockIcons
- media

---
## ClassMethod: Media.addIconSet

### Description
Adds an [IconSet](../reference.md#object-iconset) to the [global list](#classattr-mediaiconsets) for future use by passing its name to [useMedia()](#classmethod-mediausemedia).

If an IconSet has not been registered with this method, you may pass the object itself to _Media.useMedia()_ to have it registered and applied right away.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| iconSet | [IconSet](#type-iconset) | false | — | the [IconSet](../reference.md#object-iconset) to add |

### Groups

- stockIcons
- media

---
## ClassMethod: Media.addStockIcons

### Description
Registers a list of new [stockIcons](../reference_2.md#object-stockicon) for use in an application.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icons | [Array of StockIcon](#type-array-of-stockicon) | false | — | the [StockIcons](../reference_2.md#object-stockicon) to add |

### Groups

- stockIcons
- media

---
## ClassMethod: Media.updateIconMappings

### Description
Updates the [src-strings](StockIcon.md#attr-stockiconsrc) currently assigned to one or more [StockIcons](../reference_2.md#object-stockicon). The _mappings_ parameter should be a map of StockIcon-name to [any valid src-string](../reference.md#type-scimgurl).

Once updated, the icons named in the map will render their respective new images when their [names](StockIcon.md#attr-stockiconname) or [fromSrc-values](StockIcon.md#attr-stockiconfromsrc) are used as the value of an image-src property, such as [Button.icon](Button.md#attr-buttonicon) or [Img.src](Img.md#attr-imgsrc).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| mappings | [Object](../reference.md#type-object) | false | — | a map of StockIcon-names to new src-strings |

### Groups

- stockIcons
- media

---
## ClassMethod: Media.getStockIcon

### Description
Returns the [stockIcon](../reference_2.md#object-stockicon) with the passed name, or null if the name is unused.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| iconName | [String](#type-string) | false | — | the name of the [StockIcon](../reference_2.md#object-stockicon) to return |

### Groups

- stockIcons
- media

---
