# Slicer Documentation

[← Back to API Index](../reference.md)

---

## Class: Slicer

*Inherits from:* [HLayout](../reference.md#class-hlayout)

### Description
A compact filter control that targets a single DataSource field and publishes selection criteria via [Canvas.setDataContextCriteria](Canvas.md#method-canvassetdatacontextcriteria).

Configure via [Slicer.field](#attr-slicerfield) using `dataSourceID.fieldName` dot notation:

```
     isc.Slicer.create({
         field: "supplyItem.category"
     });
 
```

The Slicer publishes criteria to the nearest ancestor with a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext), so all sibling [DBCs](../reference.md#interface-databoundcomponent) bound to the target DataSource automatically re-fetch.

Editor selection by resolved base type (via [SimpleType.getBaseType](#method-simpletypegetbasetype)):

*   **Enum** (field has a valueMap): chip buttons if count ≤ [Slicer.chipThreshold](#attr-slicerchipthreshold); otherwise [SetFilterItem](SetFilterItem.md#class-setfilteritem). When the count is unknown (dynamic valueMap requiring a fetch), a SetFilterItem is created first; if the loaded count turns out to be ≤ threshold, the SetFilterItem is replaced with chips.
*   **Date / datetime**: [DateRangeItem](DateRangeItem.md#class-daterangeitem) (supports absolute and relative dates).
*   **Boolean**: three-state [CheckboxItem](CheckboxItem.md#class-checkboxitem) (checked = true, unchecked = false, unset = no filter).
*   **Numeric** (integer / float): dual-thumb [RangeSlider](RangeSlider.md#class-rangeslider) for min/max range filtering.

---
## Attr: Slicer.setFilterForm

### Description
AutoChild form containing the [SetFilterItem](SetFilterItem.md#class-setfilteritem) for enum fields above [Slicer.chipThreshold](#attr-slicerchipthreshold). Customize via `setFilterFormDefaults` / `setFilterFormProperties`.

**Flags**: IR

---
## Attr: Slicer.useRadios

### Description
Convenience for single-select chip mode with radio-button visual styling. Equivalent to setting [multiSelect](#attr-slicermultiselect) `false`.

### See Also

- [Slicer.multiSelect](#attr-slicermultiselect)

**Flags**: IR

---
## Attr: Slicer.multiSelect

### Description
Whether chip buttons allow multiple simultaneous selections (the default) or enforce single-select. When false, clicking a chip deselects all others; re-clicking the active chip deselects it (clearing the filter).

[Slicer.useRadios](#attr-sliceruseradios) is a convenience that sets `multiSelect:false` and applies radio-button visual styling.

### See Also

- [Slicer.useRadios](#attr-sliceruseradios)

**Flags**: IR

---
## Attr: Slicer.minValue

### Description
Explicit minimum for the numeric range slider. If unset, the Slicer derives the minimum from the data via a fetch.

**Flags**: IR

---
## Attr: Slicer.dateRangeForm

### Description
AutoChild form containing the [DateRangeItem](DateRangeItem.md#class-daterangeitem) for date/datetime fields. Customize via `dateRangeFormDefaults` / `dateRangeFormProperties`.

**Flags**: IR

---
## Attr: Slicer.chipThreshold

### Description
Maximum number of distinct values for which the Slicer renders individual chip buttons. Above this threshold, a [SetFilterItem](SetFilterItem.md#class-setfilteritem) multi-select is used.

When the count is not known synchronously (no static valueMap), a SetFilterItem is created first to perform its own fetch. If the fetched count is at or below this threshold, the SetFilterItem is replaced with chips — no extra fetch is issued.

**Flags**: IR

---
## Attr: Slicer.maxValue

### Description
Explicit maximum for the numeric range slider. If unset, the Slicer derives the maximum from the data via a fetch.

**Flags**: IR

---
## Attr: Slicer.numericRange

### Description
AutoChild for the dual-thumb [RangeSlider](RangeSlider.md#class-rangeslider) used for integer and float fields. Customize via `numericRangeDefaults` / `numericRangeProperties`.

**Flags**: IR

---
## Attr: Slicer.value

### Description
The Slicer's current selection, expressed as the [AdvancedCriteria](../reference.md#object-advancedcriteria) it publishes to the [dataContext](Canvas.md#attr-canvasdatacontext). This is the serializable representation of the slice: it is captured into the edit node at serialization time (see [updateEditNode()](Canvas.md#method-canvasupdateeditnode)) so it round-trips through edit-node storage just like a [listGrid.criteria](#listgridcriteria), and on recreation the Slicer reflects it in its control and re-publishes it (see [draw()](Canvas.md#method-canvasdraw)). Holds `null` when nothing is selected.

**Flags**: IRW

---
## Attr: Slicer.field

### Description
The DataSource field to filter on, specified in `dataSourceID.fieldName` dot notation (e.g. `"supplyItem.category"` ).

The Slicer resolves the field's base type via [SimpleType.getBaseType](#method-simpletypegetbasetype) and renders the appropriate editor. All editors are [AutoChildren](../reference.md#type-autochild): [Slicer.chipButton](#attr-slicerchipbutton), [Slicer.dateRangeForm](#attr-slicerdaterangeform), [Slicer.setFilterForm](#attr-slicersetfilterform), [Slicer.booleanForm](#attr-slicerbooleanform), [Slicer.numericRange](#attr-slicernumericrange).

### See Also

- [Canvas.setDataContextCriteria](Canvas.md#method-canvassetdatacontextcriteria)

**Flags**: IR

---
## Attr: Slicer.booleanForm

### Description
AutoChild form containing the three-state [CheckboxItem](CheckboxItem.md#class-checkboxitem) for boolean fields. Customize via `booleanFormDefaults` / `booleanFormProperties`.

**Flags**: IR

---
## Attr: Slicer.chipButton

### Description
AutoChild for each chip button in the enum chip strip. Customize via `chipButtonDefaults` / `chipButtonProperties`.

**Flags**: IR

---
## Method: Slicer.clearFilter

### Description
Clears the current Slicer selection, removing any filter criteria this Slicer has published.

---
