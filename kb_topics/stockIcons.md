# StockIcons Overview

[← Back to API Index](../main.md)

---

## KB Topic: StockIcons Overview

### Description
The _StockIcons_ system allows known graphics to be re-used throughout your projects by using their names in src-strings, instead of their URLs or sprite-strings - this avoids the need for hard-coded paths in source-code, and allows the actual image applied by the StockIcon name to be easily modified **_at runtime_** without trawling through code doing find-and-replace operations.

StockIcons can also map [from](../classes/StockIcon.md#attr-stockiconfromsrc) a known file-path, meaning that legacy paths in existing code don't need to be modified - if your code requests a file-path which is assigned to the _fromSrc_ of a known StockIcon, it will first be mapped to that StockIcon, and then it will render whatever image is [currently assigned](../classes/StockIcon.md#attr-stockiconsrc) to it.

The framework ships with [many such StockIcon-definitions](../classes/Media.md#classmethod-mediagetstockiconnames) that represent the numerous images available in the "images/" directory of a skin. You can use these builtin definitions in your code directly, by setting a widget's icon or src property to the name of a StockIcon. For example, to re-use the current skin's default "Edit" icon, you could set the image-source for a button's [icon](../classes/Button.md#attr-buttonicon) to "\[SKINIMG\]actions/edit.png" in your code. With StockIcons, you can use just the associated icon's name, "Edit" - for example:

```
 isc.Button.create({ icon: "Edit" });
 isc.Img.create({ src: "Edit" });
 
```

You can also provide additional customization along with the StockIcon-name. For example, if your StockIcons are mapped to [stylable SVG Symbols](svgSymbols.md#kb-topic-svg-symbols-overview) via [sprite-strings](../main.md#type-scspriteconfig) (our Shiva skin does this), you can add a colon (":") right after the StockIcon-name and then include any additional properties that are supported by SVG sprite-strings, to modify this instance of the base StockIcon definition.

```
 // make it red and semi-transparent
 isc.Button.create({ icon: "Edit:color:red;opacity:0.5;" });
 // set a size and show it upside-down
 isc.Img.create({ src: "Edit:size:24,24;rotate:180;" });
 
```

### Related

- [Media.getStockIcon](../classes/Media.md#classmethod-mediagetstockicon)
- [Media.getStockIconNames](../classes/Media.md#classmethod-mediagetstockiconnames)
- [Media.addStockIcons](../classes/Media.md#classmethod-mediaaddstockicons)
- [Media.updateIconMapping](../classes/Media.md#classmethod-mediaupdateiconmapping)
- [Media.updateIconMappings](../classes/Media.md#classmethod-mediaupdateiconmappings)
- [Media.getIconSet](../classes/Media.md#classmethod-mediageticonset)
- [Media.addIconSet](../classes/Media.md#classmethod-mediaaddiconset)
- [Media.useMedia](../classes/Media.md#classmethod-mediausemedia)
- [IconSet](../main.md#object-iconset)
- [StockIcon](../main_2.md#object-stockicon)
- [Media.iconSets](../classes/Media.md#classattr-mediaiconsets)
- [IconSet.name](../classes/IconSet.md#attr-iconsetname)
- [IconSet.mappings](../classes/IconSet.md#attr-iconsetmappings)
- [IconSet.stockIcons](../classes/IconSet.md#attr-iconsetstockicons)
- [StockIcon.name](../classes/StockIcon.md#attr-stockiconname)
- [StockIcon.src](../classes/StockIcon.md#attr-stockiconsrc)
- [StockIcon.fromSrc](../classes/StockIcon.md#attr-stockiconfromsrc)
- [StockIcon.group](../classes/StockIcon.md#attr-stockicongroup)
- [StockIcon.index](../classes/StockIcon.md#attr-stockiconindex)

---
