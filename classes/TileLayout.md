# TileLayout Documentation

[← Back to API Index](../main.md)

---

## Class: TileLayout

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Lays out a series of components, called "tiles", in a grid with multiple tiles per row.

---
## Attr: TileLayout.tileSize

### Description
Size of each tile in pixels. Depending on the [TileLayoutPolicy](../main.md#type-tilelayoutpolicy), `tileSize` may be taken as a maximum, minimum or exact size of tiles, or may be irrelevant.

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
## Attr: TileLayout.showDragLine

### Description
Set false to prevent the [TileLayout.dragLine](#attr-tilelayoutdragline) autochild from showing during dragging.

**Flags**: IRW

---
## Attr: TileLayout.tilesPerLine

### Description
Number of tiles to show in each line. Auto-derived from [TileLayout.tileSize](#attr-tilelayouttilesize) for some layout modes. See [TileLayoutPolicy](../main.md#type-tilelayoutpolicy). This can also affect [TileLayout.tileWidth](#attr-tilelayouttilewidth) or [TileLayout.tileHeight](#attr-tilelayouttileheight). See those properties for details.

### Groups

- layoutPolicy

**Flags**: IRW

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
Width of each tile in pixels. See [TileLayout.tileSize](#attr-tilelayouttilesize). If [TileLayoutPolicy](../main.md#type-tilelayoutpolicy) is "fit", [TileLayout.expandMargins](#attr-tilelayoutexpandmargins) is false, [TileLayout.tilesPerLine](#attr-tilelayouttilesperline) is set, [Orientation](../main_2.md#type-orientation) is "horizontal", and tileWidth is not set, tileWidth will be computed automatically based on [TileLayout.tilesPerLine](#attr-tilelayouttilesperline).

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
## Attr: TileLayout.dragDataAction

### Description
Indicates what to do with data dragged into another DataBoundComponent. See DragDataAction type for details.

### Groups

- dragging

**Flags**: IRW

---
## Attr: TileLayout.tileHeight

### Description
Height of each tile in pixels. See [TileLayout.tileSize](#attr-tilelayouttilesize). If [TileLayoutPolicy](../main.md#type-tilelayoutpolicy) is "fit", [TileLayout.expandMargins](#attr-tilelayoutexpandmargins) is false, [TileLayout.tilesPerLine](#attr-tilelayouttilesperline) is set, [Orientation](../main_2.md#type-orientation) is "vertical", and tileHeight is not set, tileHeight will be computed automatically based on [TileLayout.tilesPerLine](#attr-tilelayouttilesperline).

### Groups

- sizing

**Flags**: IR

---
## Attr: TileLayout.dragLineStyle

### Description
The CSS class applied to the [TileLayout.dragLine](#attr-tilelayoutdragline) autochild.

**Flags**: IR

---
## Attr: TileLayout.dragLineThickness

### Description
Thickness of the [TileLayout.dragLine](#attr-tilelayoutdragline) autochild.

**Flags**: IRW

---
## Attr: TileLayout.layoutMargin

### Description
A margin left around the outside of all tiles.

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.overflow

### Description
Normal [Overflow](../main.md#type-overflow) settings can be used on TileLayouts, for example, an overflow:auto TileLayout will scroll if members exceed its specified size, whereas an overflow:visible TileLayout will grow to accommodate members.

### Groups

- sizing

**Flags**: IRW

---
## Attr: TileLayout.autoWrapLines

### Description
When [LayoutPolicy](../main_2.md#type-layoutpolicy) is "flow", should we automatically start a new line when there's not enough room to fit the next tile on the same line?

If set to false, a new line will only be started if a tile specifies [tile.startLine](Canvas.md#attr-canvasstartline) or [tile.endLine](Canvas.md#attr-canvasendline).

### Groups

- layoutPolicy

**Flags**: IR

---
## Attr: TileLayout.tiles

### Description
List of tiles to lay out.

**Flags**: IR

---
## Attr: TileLayout.expandMargins

### Description
With [LayoutPolicy](../main_2.md#type-layoutpolicy):"fit", should margins be expanded so that tiles fill the available space in the TileLayout on the breadth axis? This can also affect [TileLayout.tileWidth](#attr-tilelayouttilewidth) or [TileLayout.tileHeight](#attr-tilelayouttileheight). See those properties for details.

### Groups

- layoutMargin

**Flags**: IR

---
## Attr: TileLayout.orientation

### Description
Direction of tiling. See also [TileLayoutPolicy](../main.md#type-tilelayoutpolicy).

### Groups

- layoutPolicy

**Flags**: IR

---
## Attr: TileLayout.layoutPolicy

### Description
Policy for laying out tiles. See [TileLayoutPolicy](../main.md#type-tilelayoutpolicy) for options.

### Groups

- layoutPolicy

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
| index | [int](../main.md#type-int) | false | — | index of the tile |

### Returns

`[Canvas](#type-canvas)` — the tile

---
## Method: TileLayout.setTileSize

### Description
Sets the height and width of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| size | [int](../main.md#type-int) | false | — | size |

### Groups

- tileLayout

---
## Method: TileLayout.setTileVMargin

### Description
Sets the vertical margin of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [Integer](../main_2.md#type-integer) | false | — | margin |

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
| index | [Integer](../main_2.md#type-integer) | true | — | position where the tile should be added. Defaults to adding the tile at the end. |

---
## Method: TileLayout.transformTileRect

### Description
Transforms the input tile [relative rect](Canvas.md#method-canvassetrect) to an absolute page rect that you can apply to your own drop indicator canvas. The supplied rect is automatically clipped along the direction perpendicular to the layout's [TileLayout.orientation](#attr-tilelayoutorientation) if it extends beyond the visible edges of the layout, just like the [TileLayout.dragLine](#attr-tilelayoutdragline) autochild.

**Note:** Only code your own drop indicator if you can't get what you need by customizing and [styling](#attr-tilelayoutdraglinestyle) the built-in [TileLayout.dragLine](#attr-tilelayoutdragline) autochild!

To build your own:

*   Create a separate indicator [Canvas](Canvas.md#class-canvas), positioned off screen with the appropriate color, opacity, and [style](Canvas.md#attr-canvasstylename) that you want. Set the indicator's [dropTarget](Canvas.md#attr-canvasdroptarget) to be the layout so the indicator is ignored as a target itself.
*   Override [dropMove()](Canvas.md#method-canvasdropmove) to call [TileLayout.getDropIndex](#method-tilelayoutgetdropindex), retrieve the tile, get the ${isc.DocUtils.linkForRef('method:Canvas.setRect','tile\\'s relative rect')}, and modify the rect as you need to size your indicator properly.
*   You'll have to manually handle the case of the drop index pointing beyond the last record, perhaps by grabbing the last tile rect, but narrowing it to the opposite side.
*   Pass the modified rect to this method to clip and transform it to an absolute rect, and then [set that new rect](Canvas.md#method-canvassetrect) into your drop indicator and [show()](Canvas.md#method-canvasshow) it.
*   You will need to [hide()](Canvas.md#method-canvashide) the drop indicator in [dropOut()](Canvas.md#method-canvasdropout).

Sample code that can be added to the SmartClient Showcase "Basic Tiling" sample:

```
    showDragLine: false,
    canReorderTiles: true,

    showDropIndicator : function (left, top, width, height) {
        if (!this.dropIndicator) {
            this.dropIndicator = isc.Canvas.create({
                top: -1000, opacity: 40, 
                autoDraw: true, dropTarget: this,
                backgroundColor:"yellow"
            });
        }
        var rect = this.transformTileRect(left, top, width, height);
        this.dropIndicator.setRect(rect);
        this.dropIndicator.show();
    },

    dropMove: function() {
        this.Super("dropMove",arguments);

        var index = this.getDropIndex(),
            length = this.data.getLength();

        // you can drop after last tile (special case)
        var after = index >= length;
        if (after) index = length - 1;

        // transform tile rect to indicator rect
        var tile = this.getTile(index);
        if (tile) {
            var left = tile.getLeft(),  width = tile.getVisibleWidth(),
                top  = tile.getTop(),  height = tile.getVisibleHeight()
            ;
            // to show drop after last tile, shift indicator over
            if (after) left += width - 20;

            // now show the indicator
            this.showDropIndicator(left, top, 20, height);
        }
    },

    dropOut : function() {
        this.Super("dropOut", arguments);

        if (this.dropIndicator) {
            this.dropIndicator.hide();
        }
    },

    destroy : function () {
        this.Super("destroy", arguments);

        if (this.dropIndicator) {
            this.dropIndicator.destroy();
        }
    },
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number)|[Array of number](#type-array-of-number) | false | — | new left coordinate, Array of coordinates in parameter order, If an Array is passed, the remaining parameters are ignored. |
| top | [number](#type-number) | true | — | new top coordinate |
| width | [number](#type-number) | true | — | new width |
| height | [number](#type-number) | true | — | new height |

### Returns

`[Array of number](#type-array-of-number)` — \[left, top, width, height\]

**Flags**: A

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
## Method: TileLayout.setTileHeight

### Description
Sets the height of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Integer](../main_2.md#type-integer) | false | — | height |

### Groups

- tileLayout

---
## Method: TileLayout.setTileHMargin

### Description
Sets the horizontal margin of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [Integer](../main_2.md#type-integer) | false | — | margin |

### Groups

- tileLayout

---
## Method: TileLayout.removeTile

### Description
Remove a tile from the layout.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tileID | [Canvas](#type-canvas)|[int](../main.md#type-int)|[ID](#type-id) | false | — | index or String ID of the tile |

### Returns

`[boolean](../main.md#type-boolean)` — whether a tile was found and removed

---
## Method: TileLayout.getDragData

### Description
During a drag-and-drop interaction, this method returns the set of records being dragged out of the component. In the default implementation, this is the list of currently selected records.

This method is consulted by [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop).

NOTE: If this component is a [multi-linked](Tree.md#method-treeismultilinktree) `TreeGrid`, this method returns a list of [NodeLocator](../main_2.md#object-nodelocator)s rather than a list of records. Each `nodeLocator` contains a pointer to the associated record in its `node` property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [DataBoundComponent](#type-databoundcomponent) | false | — | source component from which the records will be transferred |

### Returns

`[Array of Record](#type-array-of-record)` — Array of [Record](../main.md#object-record)s that are currently selected.

### Groups

- dragging
- data

---
## Method: TileLayout.getDropIndex

### Description
Returns the tile index of the tile that would currently be dropped on by the drag in process. Returns one beyond the last valid index to indicate a drop after all tiles. Except for that special case, a non-null index returned by this method may be passed to [TileLayout.getTile](#method-tilelayoutgettile) to get the corresponding visible tile.

### Returns

`[int](../main.md#type-int)` — tile index of tile that would currently be dropped on, or the tile count for a drop after all tiles

### See Also

- [TileLayout.transformTileRect](#method-tilelayouttransformtilerect)

---
## Method: TileLayout.setTileMargin

### Description
Sets the vertical and horizontal margin of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [int](../main.md#type-int) | false | — | margin |

### Groups

- tileLayout

---
## Method: TileLayout.setTileWidth

### Description
Sets the width of tiles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../main_2.md#type-integer) | false | — | width |

### Groups

- tileLayout

---
## Method: TileLayout.setTilesPerLine

### Description
Sets the number of tiles per line.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tilesPerLine | [Integer](../main_2.md#type-integer) | false | — | New [TileLayout.tilesPerLine](#attr-tilelayouttilesperline) value |

### Groups

- tileLayout

---
