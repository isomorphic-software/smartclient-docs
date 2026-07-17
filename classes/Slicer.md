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

*   **Enum** (field has a static valueMap): chip buttons if the value count is ≤ [Slicer.chipThreshold](#attr-slicerchipthreshold); otherwise [SetFilterItem](SetFilterItem.md#class-setfilteritem).
*   **Text / string** (no valueMap): with [Slicer.textMode](#attr-slicertextmode) `"list"` (the default) a [SetFilterItem](SetFilterItem.md#class-setfilteritem) wired to the bound DataSource as its `optionDataSource`; with `"search"` a plain [TextItem](TextItem.md#class-textitem) publishing a debounced `iContains` criterion.
*   **Date / datetime**: [DateRangeItem](DateRangeItem.md#class-daterangeitem) (supports absolute and relative dates).
*   **Boolean**: three-state [CheckboxItem](CheckboxItem.md#class-checkboxitem) (checked = true, unchecked = false, unset = no filter).
*   **Numeric** (integer / float): dual-thumb [RangeSlider](RangeSlider.md#class-rangeslider) for min/max range filtering.

---
## Attr: Slicer.setFilterForm

### Description
AutoChild form containing the [SetFilterItem](SetFilterItem.md#class-setfilteritem) for enum fields and for text fields in [Slicer.textMode](#attr-slicertextmode) `"list"` mode. Customize via `setFilterFormDefaults` / `setFilterFormProperties`.

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
Maximum number of distinct values for which an enum field (one with a static valueMap) renders as individual chip buttons. Above this threshold, a [SetFilterItem](SetFilterItem.md#class-setfilteritem) multi-select is used.

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
## Attr: Slicer.textMode

### Description
For text fields that have no [DataSourceField.valueMap](DataSourceField.md#attr-datasourcefieldvaluemap), controls which render mode the Slicer picks:

*   **"list"** (default) — fetch distinct values of the field from the bound DataSource and show a SetFilterItem for pick-from-list selection. Publishes an `inSet` AdvancedCriteria on change. Suits bounded categorical fields (organization / warehouse / segment names) where the author wants to see and click the actual values.
*   **"search"** — show a text input for free-form substring matching. Publishes an `iContains` AdvancedCriteria (case-insensitive) as the author types, debounced to avoid flooding. Suits high- cardinality or free-form text where a pick-list would be unwieldy.

Ignored for enum (has valueMap), date, datetime, boolean, and numeric fields — those have unambiguous render modes and are dispatched without consulting this attribute.

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
## Attr: Slicer.contributorID

### Description
Stable identifier used as this Slicer's key in the [dataContext](Canvas.md#attr-canvasdatacontext) [sharedCriteria](#canvassharedcriteria) bus. If unset (the default), a deterministic ID is generated from the Slicer's [Slicer.field](#attr-slicerfield) in the form `"slicer__dsID_._fieldName_"`.

An explicit value is only needed when two Slicers target the same DataSource and field (uncommon). Duplicate contributorIDs within the same dataContext produce a warning and last-writer-wins behavior.

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
## Attr: Slicer.filterRelated

### Description
Whether this Slicer's published criteria should also filter components bound to **related** DataSources — those whose DataSource has a [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) to the Slicer's target DataSource.

When `true` (the default), a Slicer on a reference DataSource (e.g. Organizations) automatically filters grids bound to transactional DataSources (e.g. Orders) via a `valueQuery` sub-criterion on their FK column.

Set to `false` to restrict the Slicer's criteria to only components bound to the Slicer's own DataSource.

### See Also

- [Canvas.setDataContextCriteria](Canvas.md#method-canvassetdatacontextcriteria)

**Flags**: IRW

---
## Method: Slicer.clearFilter

### Description
Clears the current Slicer selection, removing any filter criteria this Slicer has published.

---
