# Facet Documentation

[← Back to API Index](../reference.md)

---

## Class: Facet

### Description
Facet definition object made use of by the [CubeGrid](CubeGrid.md#class-cubegrid) and [FacetChart](FacetChart.md#class-facetchart) classes.

---
## Attr: Facet.collapsed

### Description
For tree facets, default collapse state for parent nodes.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.borderAfter

### Description
CSS line style to apply as a border after this facet, eg "1px dashed blue"

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.cellAlign

### Description
Default alignment of cells (in the body) for this facet.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

### See Also

- [CubeGrid.cellAlign](CubeGrid.md#attr-cubegridcellalign)

**Flags**: IR

---
## Attr: Facet.borderBefore

### Description
CSS line style to apply as a border before this facet, eg "1px dashed blue"

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.canMinimize

### Description
If facet minimizing is enabled, whether this facet should show controls to minimize the next facet. Generally a tree facet should not also allow minimizing the next facet - the interaction of the two types of collapsing can be confusing.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid). See [CubeGrid.canMinimizeFacets](CubeGrid.md#attr-cubegridcanminimizefacets).

**Flags**: IR

---
## Attr: Facet.showParentsLast

### Description
Indicates internal hierarchy should be displayed in reverse of normal tree order (so that parents follow children).

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.indentVTree

### Description
Controls indenting for a [hierarchical](#attr-facetistree) column facet if set non-null, overrriding the value of [CubeGrid.indentVTreeFacets](CubeGrid.md#attr-cubegridindentvtreefacets).

### See Also

- [CubeGrid.vTreeFacetIndentDirection](CubeGrid.md#attr-cubegridvtreefacetindentdirection)

**Flags**: IR

---
## Attr: Facet.width

### Description
Integer number of pixels. For row facets, width of headers.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

### See Also

- [CubeGrid.defaultFacetWidth](CubeGrid.md#attr-cubegriddefaultfacetwidth)

**Flags**: IR

---
## Attr: Facet.height

### Description
Integer number of pixels. For column facets, specifies the height of header. Has no effect on row facets.

If this property conflicts with a [Facet.labelHeight](#attr-facetlabelheight), the greater of the two properties will be used for determining the height of the affected row.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.labelHeight

### Description
Integer number of pixels. For column facets other than the innermost, specifies the height of the header. For row facets, specifies the height of the row containing that row facet's label (which is the same row containing the innermost column facet if one or more column facets are present).

If this property conflicts with a [Facet.height](#attr-facetheight), the greater of the two properties will be used for determining the height of the affected row.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.summaryTitle

### Description
Title for facet summary.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.proportionalTitle

### Description
For [FacetCharts](FacetChart.md#class-facetchart) only, this property specifies the value axis label when a FacetChart is in [proportional rendering mode](FacetChart.md#attr-facetchartproportional) and has this facet as its [legend facet](FacetChart.md#method-facetchartgetlegendfacet). If the `proportionalTitle` is not specified then [FacetChart.proportionalAxisLabel](FacetChart.md#attr-facetchartproportionalaxislabel) is used as the default title.

**Flags**: IR

---
## Attr: Facet.canCollapse

### Description
For tree facets, whether expand/collapse controls should be shown.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) (see, for example, [CubeGrid.canCollapseFacets](CubeGrid.md#attr-cubegridcancollapsefacets)).

**Flags**: IR

---
## Attr: Facet.rollupValue

### Description
facetValueId of the rollup facetValue for this facet.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid). See [CubeGrid.rollupValue](CubeGrid.md#attr-cubegridrollupvalue).

**Flags**: IR

---
## Attr: Facet.minimized

### Description
Default [minimize state](CubeGrid.md#attr-cubegridcanminimizefacets) for parent nodes.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.titleAlign

### Description
Alignment of facet label title.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

### See Also

- [CubeGrid.facetTitleAlign](CubeGrid.md#attr-cubegridfacettitlealign)

**Flags**: IR

---
## Attr: Facet.inlinedValues

### Description
When applied to a [Chart](../reference.md#interface-chart), does the chart's data contain multiple values per record for this facet. See [Chart.data](Chart.md#attr-chartdata) for a full overview of `inlinedValues` behavior.

**Flags**: IRW

---
## Attr: Facet.id

### Description
id of this facet. Any string or number.

**Flags**: IR

---
## Attr: Facet.synchColumnLayout

### Description
If true, treat all values in this facet as a facetValueGroup - causes synched header reorder and resize.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) and is only supported when all of a facet's values are used.

**Flags**: IR

---
## Attr: Facet.title

### Description
User-visible title of this facet. Shown on the facet label in the CubeGrid.

**Flags**: IRW

---
## Attr: Facet.isTree

### Description
Marks this facet as a hierarchical facet.

If set, [facet.value](#attr-facetvalues) will be linked as for a [modelType:"parent"](Tree.md#attr-treemodeltype) Tree, using [facetValue.id](FacetValue.md#attr-facetvalueid) and [facetValue.parentId](FacetValue.md#attr-facetvalueparentid). Expand/collapse controls will be shown allowing navigation of the facet's values.

The CubeGrid's [load on demand](CubeGrid.md#attr-cubegriddatasource) system automatically avoids fetching data for facetValues that are not currently visible due to the expand/collapse state of a tree facet.

Initial open/close state can be controlled via [facet.collapsed](#attr-facetcollapsed) and [FacetValue.collapsed](FacetValue.md#attr-facetvaluecollapsed).

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.summaryValue

### Description
Value for facet summary.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.selectionBoundary

### Description
Selection boundary determining what facets / facetValues can be selected together by drag selection / shift+click selection.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid).

**Flags**: IR

---
## Attr: Facet.values

### Description
Array of facetValue definitions.

### See Also

- [FacetValue](../reference.md#object-facetvalue)

**Flags**: IRW

---
## Attr: Facet.align

### Description
Default alignment for facet label title, and cells for this facet. Can be overridden at the facetValue level, or by setting titleAlign or cellAlign on the facet.

**Note:** This property is specific to [CubeGrids](CubeGrid.md#class-cubegrid) (see, for example, [CubeGrid.facetValueAlign](CubeGrid.md#attr-cubegridfacetvaluealign)).

### See Also

- [Facet.titleAlign](#attr-facettitlealign)
- [Facet.cellAlign](#attr-facetcellalign)

**Flags**: IR

---
