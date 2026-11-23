# IconSet Documentation

[← Back to API Index](../reference.md)

---

## Attr: IconSet.mappings

### Description
An optional JavaScript object that maps known [stockIcon-names](StockIcon.md#attr-stockiconname) to new src-strings, which may be of [any type](../reference_2.md#type-scimgurl). This set of mappings may be applied at runtime by passing the IconSet itself, or it's [name](#attr-iconsetname) if it's already been [registered](Media.md#classmethod-mediaaddiconset), to [useMedia](Media.md#classmethod-mediausemedia).

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: IconSet.stockIcons

### Description
An optional list of [custom icons](../reference_2.md#object-stockicon) which are made available for use directly in src-strings by [name](StockIcon.md#attr-stockiconname), like any other `stockIcon`.

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: IconSet.name

### Description
The unique name for this IconSet - must be a valid JavaScript Identifier. If the IconSet has been registered with [addIconSet()](Media.md#classmethod-mediaaddiconset), its name may be passed by developers in calls to [useMedia()](Media.md#classmethod-mediausemedia), in order to add its list of [stockIcons](#attr-iconsetstockicons) and/or apply its set of [mappings](#attr-iconsetmappings) to modify the images used by existing [stockIcons](../reference_2.md#object-stockicon).

### Groups

- media
- stockIcons

**Flags**: IR

---
## Attr: IconSet.baseSet

### Description
Whether this `IconSet` answers where the framework's own icons are sourced from. Only one base set is in force at a time, so installing one with [Media.useMedia](Media.md#classmethod-mediausemedia) replaces the one before it and makes it the current [Media.iconSet](#mediaiconset); the framework's "skin" and "svg" sets are the base sets.

An `IconSet` you define leaves this false. Such a set is an overlay: it contributes [new icons](#attr-iconsetstockicons), re-maps existing ones with [mappings](#attr-iconsetmappings), or both, and any number of them can be installed alongside whichever base set is in use - see [Media.installedIconSets](Media.md#classattr-mediainstallediconsets).

### Groups

- media
- stockIcons

**Flags**: IR

---
