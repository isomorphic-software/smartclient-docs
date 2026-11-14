# Chart Data Export

[← Back to API Index](../reference.md)

---

## KB Topic: Chart Data Export

### Description
A [FacetChart](../classes/FacetChart.md#class-facetchart) included in a data export does not export its raw fetched records — a facet key column plus a measure column whose header is a field name, where a count aggregated onto an id field reads as an ID rather than a tally. Instead the chart exports **the table its chart conveys**, in an **export shape** matched to the chart's semantics:

*   magnitude charts (column, bar, pie, doughnut, radar) export a ranked share-of-whole comparison: resolved labels, the measure named by its computation, percent of total, rank, and a Total row;
*   time series — line and area charts, and **any** chart whose primary facet is a date, datetime or time field — export chronologically with change-vs-prior columns, never ranked (ranking periods would destroy the chronology that is the chart's point);
*   scatter and bubble charts export one row per point: a leading identity column so outlying points can be named, then the raw X / Y / size values, unaggregated;
*   two-facet charts export a category-by-series matrix — one column per series value, a Total column, and, for stacked charts, a percentage block showing each cell's share of its row;
*   a distribution of the measure's values, bucketed into bins with cumulative percentages, is available on request.

The shape and its columns are **inferred** from the chart: its [chartType](../classes/FacetChart.md#attr-facetchartcharttype), its facets' field types, and what the measure's aggregation makes valid — a summed Total over averages, or a running total of minimums, is never emitted, whatever is requested. [FacetChart.chartExportSettings](../classes/FacetChart.md#attr-facetchartchartexportsettings) overrides any aspect: [ChartExportShape](../reference_2.md#type-chartexportshape) picks the shape (including "raw" for the unreconstructed fetch) and the [ChartExportSettings](../reference.md#object-chartexportsettings) toggles add or remove individual columns.

All of this happens in the chart's [getExportSpec()](../classes/DataBoundComponent.md#method-databoundcomponentgetexportspec) override, computed over a fresh fetch of the chart's own aggregation, so it applies wherever a chart is exported through [Canvas.exportDescendantData](../classes/Canvas_1.md#method-canvasexportdescendantdata) — and it is the shipped example of a component substituting a semantically richer export than its raw data.

### Related

- [ChartExportShape](../reference_2.md#type-chartexportshape)
- [ChartExportSortMode](../reference.md#type-chartexportsortmode)
- [ChartExportSettings](../reference.md#object-chartexportsettings)
- [ChartExportSettings.shape](../classes/ChartExportSettings.md#attr-chartexportsettingsshape)
- [ChartExportSettings.includePercentages](../classes/ChartExportSettings.md#attr-chartexportsettingsincludepercentages)
- [ChartExportSettings.includeTotalColumn](../classes/ChartExportSettings.md#attr-chartexportsettingsincludetotalcolumn)
- [ChartExportSettings.includeSummaryRow](../classes/ChartExportSettings.md#attr-chartexportsettingsincludesummaryrow)
- [ChartExportSettings.includeRank](../classes/ChartExportSettings.md#attr-chartexportsettingsincluderank)
- [ChartExportSettings.includeCodes](../classes/ChartExportSettings.md#attr-chartexportsettingsincludecodes)
- [ChartExportSettings.includeDelta](../classes/ChartExportSettings.md#attr-chartexportsettingsincludedelta)
- [ChartExportSettings.includeRunningTotal](../classes/ChartExportSettings.md#attr-chartexportsettingsincluderunningtotal)
- [ChartExportSettings.includeCumulative](../classes/ChartExportSettings.md#attr-chartexportsettingsincludecumulative)
- [ChartExportSettings.includeIdentity](../classes/ChartExportSettings.md#attr-chartexportsettingsincludeidentity)
- [ChartExportSettings.movingAverage](../classes/ChartExportSettings.md#attr-chartexportsettingsmovingaverage)
- [ChartExportSettings.sort](../classes/ChartExportSettings.md#attr-chartexportsettingssort)
- [FacetChart.chartExportSettings](../classes/FacetChart.md#attr-facetchartchartexportsettings)

### See Also

- [exporting](exporting.md#kb-topic-exporting)
- [descendantDataExport](descendantDataExport.md#kb-topic-descendant-data-export)

---
