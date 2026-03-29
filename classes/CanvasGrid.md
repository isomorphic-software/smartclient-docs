# CanvasGrid Documentation

[← Back to API Index](../reference.md)

---

## Class: CanvasGrid

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
This is part of the [ListGrid](ListGrid_1.md#class-listgrid) prerender system and cannot be used directly.

### Groups

- performance

### See Also

- [preRender](#prerender)

---
## Attr: CanvasGrid.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_2.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

**Flags**: IRW

---
## Attr: CanvasGrid.useFormattedValues

### Description
When true, cell values are obtained via [ListGrid.getDefaultFormattedValue](ListGrid_2.md#method-listgridgetdefaultformattedvalue) instead of raw record\[field.name\]. This applies valueMaps, displayField substitution, format strings, and type-specific formatters — producing output that more closely matches what the HTML grid renders. Adds ~63% total render overhead due to per-cell calls into the ListGrid formatting pipeline.

**Flags**: IR

---
## Attr: CanvasGrid.typicalCharSample

### Description
Reference string used to measure average character width for text clipping decisions during canvas pre-rendering. The measured average width of this string determines how many characters fit in each cell before an ellipsis is shown.

The default string weights characters by approximate English letter frequency (Lewand corpus) so that the measured average closely tracks real cell content. Each letter appears in proportion to its frequency rank: "e" and "t" appear 3 times, mid-frequency letters like "d" and "l" twice, and rare letters like "z" and "q" once. Digits, space, and common punctuation are included since they dominate formatted values (dates, currency, IDs). A small uppercase contingent (~15%) prevents over-clipping on headings and abbreviations.

Custom strings can be set to bias the measurement toward a specific character distribution — for example, CJK-heavy content or all-numeric columns. The string should be representative of actual cell content: characters that appear more often in data should appear more often in the sample.

### See Also

- [CanvasGrid.clipFillRatio](#attr-canvasgridclipfillratio)

**Flags**: IR

---
## Attr: CanvasGrid.clipFillRatio

### Description
Controls how aggressively text fills each cell before being clipped with an ellipsis during canvas pre-rendering.

Canvas pre-rendering estimates text width from average character width rather than measuring each string individually. This is O(1) per cell but introduces uncertainty from proportional font character width variation. In a typical UI font (Calibri 12px), character widths range from 3px ("i", "l", ".") to 11px ("W", "@") — a 3.7:1 ratio. Ten narrow characters like "llllllllll" occupy 30px while ten wide characters like "WWWWWWWWWW" occupy 110px — 3.7x wider for the same character count.

The default value (1.07) adds a 7% bias toward showing more text. The frequency-weighted [CanvasGrid.typicalCharSample](#attr-canvasgridtypicalcharsample) produces an average character width that includes uppercase letters and wide punctuation, making it ~7% wider than typical grid data (which is dominated by lowercase, digits, and short codes). The 7% compensates so that the canvas shows the same character count as CSS text-overflow:ellipsis. Because canvas is a temporary preview replaced by exact HTML rendering, occasional overflow into the right cell padding is acceptable.

Decrease toward 0.90 to apply a wider safety margin at the cost of shorter visible text. Increase above 1.10 only if data is predominantly narrow characters (digits, lowercase) and the canvas preview appears to clip too aggressively.

**Flags**: IR

---
## Attr: CanvasGrid.showDetailFields

### Description
Whether to show fields marked `detail:true` when a DataBoundComponent is given a DataSource but no `component.fields`.

The `detail` property is used on DataSource fields to mark fields that shouldn't appear by default in a view that tries to show many records in a small space.

### Groups

- databinding

**Flags**: IR

---
## Attr: CanvasGrid.matchFieldAlignment

### Description
When true, canvas pre-rendering applies the same field-level text alignment as the HTML grid — numbers and dates are right-aligned, icons are centered, and text is left-aligned, matching [listGrid.getFieldCellAlign](#method-listgridgetfieldcellalign).

Set to false to left-align all text in the canvas preview. Performance impact is negligible (<1%).

**Flags**: IR

---
## Attr: CanvasGrid.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference_2.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: CanvasGrid.useExactClipping

### Description
When true, text clipping uses per-cell `ctx.measureText()` to determine the exact pixel width of each value, producing pixel-perfect clipping that fills cells as fully as the HTML grid does. This eliminates the uncertainty inherent in average-character-width estimation (see [CanvasGrid.clipFillRatio](#attr-canvasgridclipfillratio)).

The cost is at most one `measureText()` call per visible cell. Cells whose text certainly fits (based on maxCharWidth) skip the call entirely. Cells that overflow are truncated using a proportional estimate from the single measurement — no additional `measureText()` calls.

### See Also

- [CanvasGrid.clipFillRatio](#attr-canvasgridclipfillratio)

**Flags**: IR

---
