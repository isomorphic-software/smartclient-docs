# FacetValue Documentation

[← Back to API Index](../reference.md)

---

## Attr: FacetValue.isMinimizeValue

### Description
Used to determine which facetValue is to be shown when the facet is minimized.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid). See [CubeGrid.canMinimizeFacets](CubeGrid.md#attr-cubegridcanminimizefacets).

**Flags**: IR

---
## Attr: FacetValue.titleHilite

### Description
Hilite style to apply to the title for this facetValue.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid). See [CubeGrid.hilites](CubeGrid.md#attr-cubegridhilites).

**Flags**: IR

---
## Attr: FacetValue.selectionBoundary

### Description
Selection boundary determining what facets / facetValues can be selected together by drag selection / shift+click selection.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: FacetValue.collapsed

### Description
For tree facets, initial collapse state for this node. Defaults to [Facet.collapsed](Facet.md#attr-facetcollapsed).

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: FacetValue.width

### Description
Width of the cube grid facetValue in pixels.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: FacetValue.cellAlign

### Description
Default alignment of cells (in the body) for this facetValue.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) (see, for example, [CubeGrid.cellAlign](CubeGrid.md#attr-cubegridcellalign)).

**Flags**: IR

---
## Attr: FacetValue.align

### Description
Default alignment for facet label title and cells for this facetValue. Can be overridden by setting titleAlign or cellAlign on the facetValue.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) (see, for example, [CubeGrid.facetValueAlign](CubeGrid.md#attr-cubegridfacetvaluealign)).

**Flags**: IR

---
## Attr: FacetValue.borderBefore

### Description
CSS line style to apply as a border before this facetValue.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: FacetValue.canCollapse

### Description
For individual parent facetValues within a hierarchical facet, this flag controls whether an expand/collapse control will be shown.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) (see, for example, [CubeGrid.canCollapseFacets](CubeGrid.md#attr-cubegridcancollapsefacets)).

**Flags**: IR

---
## Attr: FacetValue.id

### Description
id of this facetValue. Any string or number.

**Flags**: IRW

---
## Attr: FacetValue.title

### Description
User-visible title of this facetValue. Shown on the field header.

**Flags**: IRW

---
## Attr: FacetValue.canEdit

### Description
Whether cells for this facetValue can be edited. Defaults to [CubeGrid.canEdit](CubeGrid.md#attr-cubegridcanedit).

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IRW

---
## Attr: FacetValue.canMinimize

### Description
If [facet minimizing](CubeGrid.md#attr-cubegridcanminimizefacets) is enabled, whether this facet value should show controls to minimize the next facet. Generally a tree facet should not also allow minimizing the next facet the interaction of the two types of collapsing can be confusing.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) (see, for example, [CubeGrid.canMinimizeFacets](CubeGrid.md#attr-cubegridcanminimizefacets)).

**Flags**: IR

---
## Attr: FacetValue.borderAfter

### Description
CSS line style to apply as a border after this facetValue.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: FacetValue.minimized

### Description
Initial [minimize state](CubeGrid.md#attr-cubegridcanminimizefacets) for this node. Defaults to [Facet.minimized](Facet.md#attr-facetminimized).

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: FacetValue.parentId

### Description
For tree facets ([facet.isTree](Facet.md#attr-facetistree)), id of this facetValue's parent facetValue.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IRA

---
## Method: FacetValue.formatCellValue

### Description
Formatter to apply to values displayed for cells under this facetValue.

Can only be set on the [metric facet](CubeGrid.md#attr-cubegridmetricfacetid) or, if no metric facet is specified, on the innermost column facet.

If a single, grid-wide formatting style is desired, implement [grid.formatCellValue()](ListGrid_2.md#method-listgridformatcellvalue) instead.

**Note:** This method is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value for the cell being |
| record | [CellRecord](#type-cellrecord) | false | — | record object for the cell. Note: If this is a new cell that has not been saved, in an editable grid, it has no associated record object. In this case the edit values will be passed in as this parameter. |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number for the cell. |

### Returns

`[String](#type-string)` — formatted value to display in the cell.

---
## Method: FacetValue.getCellValue

### Description
Callout to determine custom value to display for cells displayed for this facetValue.

Can only be set on the [metric facet](CubeGrid.md#attr-cubegridmetricfacetid) or, if no metric facet is specified, on the innermost column facet.

**Note:** This method is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [CubeGrid](#type-cubegrid) | false | — | this facetValue's CubeGrid |
| record | [Object](../reference.md#type-object) | false | — | cell record |
| rowNum | [number](#type-number) | false | — | row value for the cell |
| colNum | [number](#type-number) | false | — | column value for the cell |

### Returns

`[String](#type-string)` — HTML to display

---
