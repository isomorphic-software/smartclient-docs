# SimpleTile Documentation

[← Back to API Index](../main.md)

---

## Class: SimpleTile

*Inherits from:* [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas)

### Description
Default class used by a [TileGrid](TileGrid.md#class-tilegrid) to render each tile. See [TileGrid.tile](TileGrid.md#attr-tilegridtile).

SimpleTiles should not be created directly, instead, use a TileGrid and provide data and SimpleTile instances are created for you.

---
## Attr: SimpleTile.creator

### Description
The [TileGrid](TileGrid.md#class-tilegrid) that created this SimpleTile. This property will be null if the tile was created by a user-provided [TileGrid.createTile](TileGrid.md#method-tilegridcreatetile) method.

### See Also

- [SimpleTile.tileGrid](#attr-simpletiletilegrid)

**Deprecated**

**Flags**: IR

---
## Attr: SimpleTile.tileGrid

### Description
The [TileGrid](TileGrid.md#class-tilegrid) that created this SimpleTile.

**Flags**: IR

---
## Attr: SimpleTile.baseStyle

### Description
CSS style for the tile as a whole. As with [StatefulCanvas.baseStyle](StatefulCanvas.md#attr-statefulcanvasbasestyle), suffixes are appended to this style to represent various states ("Over", "Selected", etc).

**Flags**: IR

---
## Method: SimpleTile.getInnerHTML

### Description
The default implementation will call [TileGrid.getTileHTML](TileGrid.md#method-tilegridgettilehtml).

### Returns

`[HTMLString](../main.md#type-htmlstring)` — HTML contents for the tile, as a String

---
## Method: SimpleTile.getRecord

### Description
Return the record that this tile should render.

NOTE: a TileGrid that is doing data paging may reuse tiles with different records, so a subclass of SimpleTile should not cache the record returned by getRecord().

### Returns

`[TileRecord](#type-tilerecord)` — the TileRecord associated with this tile

---
