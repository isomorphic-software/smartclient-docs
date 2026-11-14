# ChartExportSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: ChartExportSettings.includeSummaryRow

### Description
The bottom summary row. What it shows follows the measure's aggregation: a Total for summed or counted measures, an Average for averaged ones; for minimums and maximums no summary row is valid and this setting is ignored.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeRank

### Description
Comparison only: the Rank column.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.sort

### Description
Row order, overriding the resolved shape's natural order.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeDelta

### Description
Trend only: the change-vs-prior-period columns (absolute and percent).

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeTotalColumn

### Description
Matrix only: the per-row Total column — the denominator of the matrix's percentage block.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeCumulative

### Description
Distribution only: the Cumulative % column.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeCodes

### Description
Comparison only: the raw Code column retained beside resolved labels (for joins and pivots against the source data). Only emitted when labels actually differ from the stored values.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeIdentity

### Description
Correlation only: a leading identity column naming each point's record (from the DataSource's title field), so outlying points can be identified.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.movingAverage

### Description
Trend only: when set, adds a moving-average column computed over this many periods.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includeRunningTotal

### Description
Trend only: the Running Total column. Valid only for summed or counted measures.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.includePercentages

### Description
Percentage columns: "% of Total" for a comparison or distribution, the percentage block (each cell's percent of its row's Total) for a stacked matrix.

### Groups

- chartExport

**Flags**: IR

---
## Attr: ChartExportSettings.shape

### Description
The export shape. When "auto", the shape is inferred from the chart -- see [ChartExportShape](../reference_2.md#type-chartexportshape) for the shapes and [ChartExportSettings](../reference.md#object-chartexportsettings) for how the inference works.

### Groups

- chartExport

**Flags**: IR

---
