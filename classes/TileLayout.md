# TileLayout Documentation

[← Back to API Index](../reference.md)

---

## Class: TileLayout

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Lays out a series of components, called "tiles", in a grid with multiple tiles per row.

---
## Attr: TileLayout.layoutMargin

### Description
A margin left around the outside of all tiles.

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.tileSize

### Description
Size of each tile in pixels. Depending on the [LayoutPolicy](../reference.md#type-layoutpolicy), `tileSize` may be taken as a maximum, minimum or exact size of tiles, or may be irrelevant.

Width and height may be separately set via [TileLayout.tileHeight](#attr-tilelayouttileheight) and [TileLayout.tileWidth](#attr-tilelayouttilewidth).

### Groups

- sizing

**Flags**: IR

---
## Attr: TileLayout.paddingAsLayoutMargin

### Description
If this widget has padding specified (as [this.padding](Canvas.md#attr-canvaspadding) or in the CSS style applied to this layout), should it show up as space outside the members, similar to layoutMargin?

If this setting is false, padding will not affect member positioning (as CSS padding normally does not affect absolutely positioned children). Leaving this setting true allows a designer to more effectively control layout purely from CSS.

Note that [Layout.layoutMargin](Layout.md#attr-layoutlayoutmargin) if specified, takes precedence over this value.

### Groups

- layoutMargin

**Flags**: IRWA

---
## Attr: TileLayout.overflow

### Description
Normal [Overflow](../reference.md#type-overflow) settings can be used on TileLayouts, for example, an overflow:auto TileLayout will scroll if members exceed its specified size, whereas an overflow:visible TileLayout will grow to accommodate members.

### Groups

- sizing

**Flags**: IRW

---
## Attr: TileLayout.autoWrapLines

### Description
When [LayoutPolicy](../reference.md#type-layoutpolicy) is "flow", should we automatically start a new line when there's not enough room to fit the next tile on the same line?

If set to false, a new line will only be started if a tile specifies [tile.startLine](Canvas.md#attr-canvasstartline) or [tile.endLine](Canvas.md#attr-canvasendline).

### Groups

- layoutPolicy

**Flags**: IR

---
## Attr: TileLayout.tilesPerLine

### Description
Number of tiles to show in each line. Auto-derived from [TileLayout.tileSize](#attr-tilelayouttilesize) for some layout modes. See [TileLayoutPolicy](../reference.md#type-tilelayoutpolicy). This can also affect [TileLayout.tileWidth](#attr-tilelayouttilewidth) or [TileLayout.tileHeight](#attr-tilelayouttileheight). See those properties for details.

### Groups

- layoutPolicy

**Flags**: IRW

---
## Attr: TileLayout.tiles

### Description
List of tiles to lay out.

**Flags**: IR

---
## Attr: TileLayout.tileMargin

### Description
Margin in between tiles. Can be set on a per-axis basis with [TileLayout.tileHMargin](#attr-tilelayouttilehmargin) and [TileLayout.tileVMargin](#attr-tilelayouttilevmargin).

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.tileWidth

### Description
Width of each tile in pixels. See [TileLayout.tileSize](#attr-tilelayouttilesize). If [LayoutPolicy](../reference.md#type-layoutpolicy) is "fit", [TileLayout.expandMargins](#attr-tilelayoutexpandmargins) is false, [TileLayout.tilesPerLine](#attr-tilelayouttilesperline) is set, [Orientation](../reference.md#type-orientation) is "horizontal", and tileWidth is not set, tileWidth will be computed automatically based on [TileLayout.tilesPerLine](#attr-tilelayouttilesperline).

### Groups

- sizing

**Flags**: IR

---
## Attr: TileLayout.tileVMargin

### Description
Vertical margin in between tiles. See [TileLayout.tileMargin](#attr-tilelayouttilemargin).

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.animateTileChange

### Description
If set, tiles animate to their new positions when a tile is added, removed, or reordered via drag and drop.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: TileLayout.expandMargins

### Description
With [LayoutPolicy](../reference.md#type-layoutpolicy):"fit", should margins be expanded so that tiles fill the available space in the TileLayout on the breadth axis? This can also affect [TileLayout.tileWidth](#attr-tilelayouttilewidth) or [TileLayout.tileHeight](#attr-tilelayouttileheight). See those properties for details.

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.orientation

### Description
Direction of tiling. See also [TileLayoutPolicy](../reference.md#type-tilelayoutpolicy).

### Groups

- layoutPolicy

**Flags**: IR

---
## Attr: TileLayout.dragDataAction

### Description
Indicates what to do with data dragged into another DataBoundComponent. See DragDataAction type for details.

### Groups

- dragging

**Flags**: IRW

---
## Attr: TileLayout.layoutPolicy

### Description
Policy for laying out tiles. See [TileLayoutPolicy](../reference.md#type-tilelayoutpolicy) for options.

### Groups

- layoutPolicy

**Flags**: IR

---
## Attr: TileLayout.tileHeight

### Description
Height of each tile in pixels. See [TileLayout.tileSize](#attr-tilelayouttilesize). If [LayoutPolicy](../reference.md#type-layoutpolicy) is "fit", [TileLayout.expandMargins](#attr-tilelayoutexpandmargins) is false, [TileLayout.tilesPerLine](#attr-tilelayouttilesperline) is set, [Orientation](../reference.md#type-orientation) is "vertical", and tileHeight is not set, tileHeight will be computed automatically based on [TileLayout.tilesPerLine](#attr-tilelayouttilesperline).

### Groups

- sizing

**Flags**: IR

---
## Attr: TileLayout.tileHMargin

### Description
Horizontal margin in between tiles. See [TileLayout.tileMargin](#attr-tilelayouttilemargin).

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.dragLine

### Description
Canvas used to display a drop indicator when a another canvas is dragged over this widget.

**Flags**: R

---
## Method: TileLayout.getTile

### Description
Retrieve a tile by index.

The TileLayout consistently uses this method to access tiles, in order to allow subclasses to create tiles on demand.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [int](../reference.md#type-int) | false | — | index of the tile |

### Returns

`[Canvas](#type-canvas)` — the tile

---
## Method: TileLayout.setTileHeight

### Description
Sets the height of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Integer](../reference_2.md#type-integer) | false | — | height |

### Groups

- tileLayout

---
## Method: TileLayout.setTileSize

### Description
Sets the height and width of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| size | [int](../reference.md#type-int) | false | — | size |

### Groups

- tileLayout

---
## Method: TileLayout.setTileHMargin

### Description
Sets the horizontal margin of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [Integer](../reference_2.md#type-integer) | false | — | margin |

### Groups

- tileLayout

---
## Method: TileLayout.setTileVMargin

### Description
Sets the vertical margin of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [Integer](../reference_2.md#type-integer) | false | — | margin |

### Groups

- tileLayout

---
## Method: TileLayout.addTile

### Description
Add a tile to the layout, dynamically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tile | [Canvas](#type-canvas) | false | — | new tile to add |
| index | [Integer](../reference_2.md#type-integer) | true | — | position where the tile should be added. Defaults to adding the tile at the end. |

---
## Method: TileLayout.removeTile

### Description
Remove a tile from the layout.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tileID | [Canvas](#type-canvas)|[int](../reference.md#type-int)|[ID](#type-id) | false | — | index or String ID of the tile |

### Returns

`[boolean](../reference.md#type-boolean)` — whether a tile was found and removed

---
## Method: TileLayout.getDragData

### Description
During a drag-and-drop interaction, this method returns the set of records being dragged out of the component. In the default implementation, this is the list of currently selected records.

This method is consulted by [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop).

NOTE: If this component is a [multi-linked](Tree.md#method-treeismultilinktree) `TreeGrid`, this method returns a list of [NodeLocator](../reference_2.md#object-nodelocator)s rather than a list of records. Each `nodeLocator` contains a pointer to the associated record in its `node` property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [DataBoundComponent](#type-databoundcomponent) | false | — | source component from which the records will be transferred |

### Returns

`[Array of Record](#type-array-of-record)` — Array of [Record](../reference.md#object-record)s that are currently selected.

### Groups

- dragging
- data

---
## Method: TileLayout.transferDragData

### Description
During a drag-and-drop interaction, this method is called to transfer a set of records that were dropped onto some other component. This method is called after the set of records has been copied to the other component. Whether or not this component's data is modified is determined by the value of [DataBoundComponent.dragDataAction](DataBoundComponent.md#attr-databoundcomponentdragdataaction).

With a `dragDataAction` of "move", a databound component will issue "remove" dsRequests against its DataSource to actually remove the data, via [DataSource.removeData](DataSource.md#method-datasourceremovedata).

### Returns

`[Array](#type-array)` — Array of objects that were dragged out of this ListGrid.

### See Also

- [DataBoundComponent.getDragData](DataBoundComponent.md#method-databoundcomponentgetdragdata)
- [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop)

---
## Method: TileLayout.setTileMargin

### Description
Sets the vertical and horizontal margin of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [int](../reference.md#type-int) | false | — | margin |

### Groups

- tileLayout

---
## Method: TileLayout.setTileWidth

### Description
Sets the width of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer) | false | — | width |

### Groups

- tileLayout

---
## Method: TileLayout.setTilesPerLine

### Description
Sets the number of tiles per line.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tilesPerLine | [Integer](../reference_2.md#type-integer) | false | — | New [TileLayout.tilesPerLine](#attr-tilelayouttilesperline) value |

### Groups

- tileLayout

---
