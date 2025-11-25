# FacetChart Documentation

[← Back to API Index](../main.md)

---

## Class: FacetChart

*Inherits from:* [DrawPane](DrawPane.md#class-drawpane)

### Description
HTML5-based charting engine, implementing all [chartTypes](Chart.md#attr-chartcharttype) of the [Chart](../main_2.md#interface-chart) interface.

Can be used directly, or specified as [ListGrid.chartConstructor](ListGrid_1.md#attr-listgridchartconstructor) or [CubeGrid.chartConstructor](CubeGrid.md#attr-cubegridchartconstructor).

**NOTE:** you must load the standard Drawing and [Optional](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) Charts modules before you can use FacetChart. Also, the Charts Module is available in Pro Edition or better, please see [smartclient.com/product](http://www.smartclient.com/product) for licensing information.

To create a FacetChart, set [FacetChart.facets](#attr-facetchartfacets) to an Array of Facet objects describing the chart dimensions and [FacetChart.valueProperty](#attr-facetchartvalueproperty) to value field name. For example:

```
 isc.FacetChart.create({
     facets: [{
         id: "season",    // the key used for this facet in the data above
         title: "Season"  // the user-visible title you want in the chart
     }],
     valueProperty: "temp", // the property in our data that is the numerical value to chart
     data: [
         {season: "Spring", temp: 79},
         {season: "Summer", temp: 102},
         {season: "Autumn", temp: 81},
         {season: "Winter", temp: 59}
     ],
     title: "Average temperature in Las Vegas"
 });
 
```

A [DataSource](DataSource.md#class-datasource) may be provided instead of inline [data](#attr-facetchartdata) to use the chart as a [DataBoundComponent](../main.md#interface-databoundcomponent). In this case, [facetFields](#attr-facetchartfacetfields) may be provided instead of [facets](#attr-facetchartfacets), to specify which DataSource fields to use as the facets. If neither is set, the framework will attempt to auto-derive the [facetFields](#attr-facetchartfacetfields). The [valueProperty](#attr-facetchartvalueproperty) will also be auto-derived for databound charts if it hasn't been set in the chart instance.

The following SDK examples demonstrate charts with a single facet:

*   *Log Scaling* example,
*   *Interactive Data Points* example, and
*   *Adding Element* example.

See the following SDK examples for examples of charts with multiple facets:

*   *Simple Chart* example,
*   *Multi-Series Chart* example, and
*   *Dynamic Data* example.

#### the Inlined Facet

Having an "inlined facet" is another method to provide data to the chart. In this case each CellRecord contains multiple data values; one facet definition is considered "inlined", meaning that the facetValueIds from this facet appear as properties in each Record, and each such property holds one data value. In this case the singular `valueProperty` is ignored. For example:

```
 isc.FacetChart.create({
     facets: [
         {
             inlinedValues: true,
             values: [
                 {id: "spring", title: "Spring"},
                 {id: "summer", title: "Summer"},
                 {id: "autumn", title: "Autumn"},
                 {id: "winter", title: "Winter"}
             ]
         }
     ],
     data: [
         {spring: 79, summer: 102, autumn: 81, winter: 59}
     ],
     title: "Average temperature in Las Vegas"
 });
 
```
Example with two facets:
```
 isc.FacetChart.create({
     facets: [
         {
             inlinedValues: true,
             values: [
                 {id: "spring", title: "Spring"},
                 {id: "summer", title: "Summer"},
                 {id: "autumn", title: "Autumn"},
                 {id: "winter", title: "Winter"}
             ]
         },
         {id: "city"}
     ],
     data: [
         {city: "Las Vegas", spring: 79, summer: 102, autumn: 81, winter: 59},
         {city: "New York", spring: 60, summer: 83, autumn: 66, winter: 40}
     ],
     stacked: false,
     title: "Average temperatures"
 });
 
```

#### Dual axis or multi-axis charts

FacetChart supports drawing multiple vertical axes. This is commonly used to show values with different units (for example: sales in dollars, total units shipped) and/or very different ranges (for example: gross revenue, profit) on the same chart. Each set of values, referred to as a "metric", gets its own axis and gradation marks.

To use multiple axes, you add an additional facet called the "metric facet" that specifies each axis to be plotted as a facetValueId. The metric facet is an inlined facet, so as with inlined facets in general, each CellRecord has a value for each facetValueId of the metric facet. You then set [extraAxisMetrics](#attr-facetchartextraaxismetrics) to the list of metrics that should be plotted as additional axes.

For example, if you were plotting revenue and profit for each month of the year, you would have one facet named "metric" with facetValueIds "revenue" and "profit" and a second facet "month". Each CellRecord would have the revenue and profit for one month, stored under the properties "revenue" and "profit". Setting `extraAxisMetrics` to \["profit"\] would cause profit to be plotted as the second axis. See the *Dual Axis* SDK sample for an example.

You can have multiple extra axes and the additional axes and gradation tics will be drawn at increasing distances from the chart. By default, the first metric is drawn as a column chart and subsequent metrics are drawn as lines; you can override this via [extraAxisSettings](#attr-facetchartextraaxissettings). See the *3+ Axes* SDK sample for an example of multiple extra axes.

Multi-axis, multi-facet charts are also allowed. Extending the previous example, you might add a new facet "company", for a total of 3 facets. Each CellRecord would have "revenue" and "profit" for one combination of "company" and "month". The default appearance in this case would show revenue as clustered columns (one cluster per month, one column per company) and would show profit as multiple lines (one per company). See the *Multi-Series* SDK sample for an example of a multi-axis, multi-facet chart.

#### Mixed plots
In some cases you want to show some data series as one shape and other data series as another shape _but use the same axis_. This is commonly used when one series is of a fundamentally different kind than the other series (for example, a projection or average) but still has the same scale.

To achieve a mixed plot like this, define it as a multi-axis chart as explained above, but set [MetricSettings.showAxis](MetricSettings.md#attr-metricsettingsshowaxis) false to avoid a second axis appearing, and set [MetricSettings.matchGradations](MetricSettings.md#attr-metricsettingsmatchgradations) to cause the same gradations to be used for both plots.

See the *Mixed Plots* SDK example.

#### Histogram Charts

A "histogram" chart is similar to a [stacked](#attr-facetchartstacked) "column" chart, showing multiple facet values vertically for each position along the x-axis / [data label facet](#method-facetchartgetdatalabelfacet), but instead of each vertical facet value being defined only by a length, a "histogram" chart defines a _segment_ for each, represented by both a start point (the ["value property"](#attr-facetchartvalueproperty)) and an end point (the ["endValue metric"](#attr-facetchartendvaluemetric)).

Segments may overlap, with the last segment drawn receiving the highest z-ordering. To override this default behavior, values may be provided using an additional metric - [FacetChart.zIndexMetric](#attr-facetchartzindexmetric) - whose value must be a non-negative integer no greater than [FacetChart.maxDataZIndex](#attr-facetchartmaxdatazindex).

#### Scatter Charts

Scatter charts differ from other chart types in that both axes represent continuous numeric data rather than a discrete set of facet values (like months of the year). For this reason Scatter charts use the same concept of a "metric" facet as is used by Dual-Axis charts, where the metric facet is expected to have exactly two metrics: the [xAxisMetric](#attr-facetchartxaxismetric) and [yAxisMetric](#attr-facetchartyaxismetric).

Unlike all other chart types, a scatter plot may be specified with only the metric facet. However one additional facet can be defined, which allows multiple sets of x,y points to be drawn in different colors, analogous to the different colors of a multi-series line chart.

See the *Scatter Plot* SDK example.

**Date values on the X axis**

FacetChart also supports scatter charts where the x-axis represents date- or time-valued data and the y-axis represents numeric data, as normal. To enable this mode all records in the data must have values for the facetValueId of the [xAxisMetric](#attr-facetchartxaxismetric) that are true Date objects, not Strings or `null`s. For these charts, vertical lines are drawn to represent a sequence of significant datetime values on the x-axis, such as the first day of the month or week. The mechanism used to select these Dates and format them into the x-axis labels is the same mechanism used by charts with [labelCollapseMode](#attr-facetchartlabelcollapsemode) set to "time".

#### Bubble Charts

A "bubble" chart is a type of scatter chart where the _size_ of each rendered data point represents an additional metric value, allowing 3 continuous data values to be visualized together. When using `chartType:"Bubble"`, the additional metric is configured via [pointSizeMetric](#attr-facetchartpointsizemetric). Points will be sized between the [minDataPointSize](#attr-facetchartmindatapointsize) and [maxDataPointSize](#attr-facetchartmaxdatapointsize), optionally with [logarithmic scaling](#attr-facetchartlogscalepointsize). A legend will be included showing how point size represents data values, and a multi-facet Bubble chart can optionally use a different shape for each `facetValue` via [useMultiplePointShapes](#attr-facetchartusemultiplepointshapes).

Variable-size points can also be used with other, non-scatter chart types (such as "Line" or "Radar") when [showDataPoints](#attr-facetchartshowdatapoints) is enabled, by setting `pointSizeMetric` to the [FacetValue.id](FacetValue.md#attr-facetvalueid) of a [facetValue](Facet.md#attr-facetvalues) of the metric facet. In this case, a legend for point sizes is not shown by default, but can be enabled via [showPointSizeLegend](#attr-facetchartshowpointsizelegend).

Whenever drawing variable size data points, by default, the largest data points are drawn first so that smaller data points are less likely to be completely occluded by larger data points, but this can be disabled by setting [autoSortBubblePoints](#attr-facetchartautosortbubblepoints) to `false`. Visual appearance of data points can be further customized by setting the [bubbleProperties](#attr-facetchartbubbleproperties).

See the *Bubble Chart* SDK example.

#### Color Scale Charts

FacetChart supports rendering an additional metric value as the _color_ of each data point. This feature requires that [showDataPoints](#attr-facetchartshowdatapoints) be enabled and is configured via [colorScaleMetric](#attr-facetchartcolorscalemetric). Instead of data points being drawn using a separate color for each `facetValue` of the legend facet, the data points will be drawn using a color interpolated between the [scaleStartColor](#attr-facetchartscalestartcolor) and [scaleEndColor](#attr-facetchartscaleendcolor), optionally with [logarithmic scaling](#attr-facetchartlogscalepointcolor). A legend is included by default via [showColorScaleLegend](#attr-facetchartshowcolorscalelegend) that shows how the data values are mapped to a color via a gradient over the range of colors used in the chart. Visual appearance of data points in color scale charts can be further customized by setting the [bubbleProperties](#attr-facetchartbubbleproperties), just as with bubble charts.

Note that when color is being used to show values of the `colorScaleMetric` then color cannot be used to distinguish between different `facetValues`. Therefore color scale charts cannot have a (non-metric) legend facet.

See the *Color Scale Chart* SDK example.

#### Three-Facet Bar and Column Charts

Bar and Column charts support having three facets declared, unlike most other charts supporting data labels, which only allow two. With three facets, the first two are shown as [data label facets](#method-facetchartgetdatalabelfacet), as separate rows of labels, and the third facet is used as the [legend facet](#method-facetchartgetlegendfacet).

You can use features such as [stacking](#attr-facetchartstacked) and [extra axes](#attr-facetchartextraaxissettings) with a three-facet Bar or Column chart, but certain chart settings are incompatible:

*   [Zooming](#attr-facetchartcanzoom) isn't supported
*   [Inline labels](#attr-facetchartshowinlinelabels) aren't supported
*   The only mode supported for [label collapsing](#attr-facetchartlabelcollapsemode) is "sample".

In addition, with a three-facet chart, you can only call [FacetChart.setChartType](#method-facetchartsetcharttype) to switch between Bar and Column charts. Switching to other types is not supported.

Take a look at [this example](https://www.smartclient.com/smartclient-latest/showcase/?id=threeFacetBarChart) to see this feature in action.

#### Notes on printing

FacetCharts support printing on all supported desktop browsers. When using Pro Edition or better with the SmartClient Server Framework installed, charts can also be exported to PDF via [RPCManager.exportContent](RPCManager.md#classmethod-rpcmanagerexportcontent) or to images via [RPCManager.exportImage](RPCManager.md#classmethod-rpcmanagerexportimage).

---
## ClassAttr: FacetChart.invalidPolynomialDegreeMessage

### Description
Warning message issued when an invalid polynomial degree is entered into the prompt dialog created by the `"Polynomial Degree..."` option in the context menu for scatter plots.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.allChartTypes

### Description
All [ChartTypes](../main.md#type-charttype) that are supported by this class. Should be defined by concrete implementations of the charting interface.

**Flags**: R

---
## ClassAttr: FacetChart.chartTypeColumnTitle

### Description
Title for the `"Column"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeLineTitle

### Description
Title for the `"Line"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.polynomialRegressionLinesContextMenuItemTitle

### Description
Title for the `"Polynomial Curve"` option of the `"Regression Lines"` option in the context menu for scatter plots.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeRadarTitle

### Description
Title for the `"Radar"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.swapFacetsContextMenuItemTitle

### Description
Title for the `"Swap Facets"` item in the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeContextMenuItemTitle

### Description
Title for the `"Chart Type"` submenu in the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeBubbleTitle

### Description
Title for the `"Bubble"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.stackContextMenuItemTitle

### Description
Title for the `"Stack"` submenu in the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.linearRegressionLinesContextMenuItemTitle

### Description
Title for the `"Straight Line"` option of the `"Regression Lines"` option in the context menu for scatter plots.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.fillContextMenuItemTitle

### Description
Title for the `"Fill"` submenu in the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.stackAutoContextMenuItemTitle

### Description
Title for the `"Auto"` item in the [Stack](#classattr-facetchartstackcontextmenuitemtitle) submenu of the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.regressionLinesContextMenuItemTitle

### Description
Title for the `"Regression Lines"` option of the context menu for scatter plots.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.fillUnfilledContextMenuItemTitle

### Description
Title for the `"Unfilled"` item in the [Fill](#classattr-facetchartfillcontextmenuitemtitle) submenu of the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.fillFilledContextMenuItemTitle

### Description
Title for the `"Filled"` item in the [Fill](#classattr-facetchartfillcontextmenuitemtitle) submenu of the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeBarTitle

### Description
Title for the `"Bar"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeHistogramTitle

### Description
Title for the `"Histogram"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.proportionalContextMenuItemTitle

### Description
Title for the `"Proportional"` option of the context menu for charts that support [proportional rendering mode](#attr-facetchartproportional).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.stackStackedContextMenuItemTitle

### Description
Title for the `"Stacked"` item in the [Stack](#classattr-facetchartstackcontextmenuitemtitle) submenu of the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.stackUnstackedContextMenuItemTitle

### Description
Title for the `"Unstacked"` item in the [Stack](#classattr-facetchartstackcontextmenuitemtitle) submenu of the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypePieTitle

### Description
Title for the `"Pie"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.polynomialDegreeRegressionLinesContextMenuItemTitle

### Description
Title for the `"Polynomial Degree..."` option of the `"Regression Lines"` option in the context menu for scatter plots.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.polynomialDegreePrompt

### Description
Message of the prompt created by the `"Polynomial Degree..."` option in the context menu for scatter plots to ask the user for a polynomial degree to use for polynomial regression.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeDoughnutTitle

### Description
Title for the `"Doughnut"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.hideRegressionLinesContextMenuItemTitle

### Description
Title for the `"None"` option of the `"Regression Lines"` option in the context menu for scatter plots.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeScatterTitle

### Description
Title for the `"Scatter"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.fillAutoContextMenuItemTitle

### Description
Title for the `"Auto"` item in the [Fill](#classattr-facetchartfillcontextmenuitemtitle) submenu of the context menu for non-scatter/bubble charts.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: FacetChart.chartTypeAreaTitle

### Description
Title for the `"Area"` item in the `"Chart Type"` submenu in the context menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FacetChart.facetFields

### Description
Specifies what [DataSource](DataSource.md#class-datasource) fields to use as the chart [FacetChart.facets](#attr-facetchartfacets) for a databound chart. If [FacetChart.facets](#attr-facetchartfacets) is also explicitly set, [FacetChart.facetFields](#attr-facetchartfacetfields) is definitive but [Facet](Facet.md#class-facet) properties will be picked up from [FacetChart.facets](#attr-facetchartfacets) also present in the [FacetChart.facetFields](#attr-facetchartfacetfields).

If neither this property nor [FacetChart.facets](#attr-facetchartfacets) is set, a databound chart will attempt to auto-derive [FacetChart.facetFields](#attr-facetchartfacetfields) from the DataSource fields. The first two text or text-derived fields in the DataSource will be assumed to be the [FacetChart.facetFields](#attr-facetchartfacetfields).

### See Also

- [FacetChart.valueProperty](#attr-facetchartvalueproperty)

**Flags**: IR

---
## Attr: FacetChart.logBase

### Description
When [FacetChart.useLogGradations](#attr-facetchartuseloggradations), base value for logarithmic gradation lines. Gradation lines will be shown at every power of this value plus intervening values specified by [FacetChart.logGradations](#attr-facetchartloggradations).

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.autoSortBubblePoints

### Description
Whether to draw data points in order of descending [point size](#attr-facetchartpointsizemetric) so that small values are less likely to be completely occluded by larger values. Set this to `false` to draw the data points in the same order that they appear in the data.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.extraAxisLabelAlign

### Description
Horizontal alignment of labels shown in extra y-axes, shown to the right of the chart.

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.showRegressionLine

### Description
For scatter plots only, whether to display a regression curve that best fits the data of the two metric facet values.

The type of regression curve used depends on the [RegressionLineType](../main_2.md#type-regressionlinetype) property, which can be:

*   **"line"** – to draw a linear regression curve, or
*   **"polynomial"** – to draw a polynomial regression curve (of degree [FacetChart.regressionPolynomialDegree](#attr-facetchartregressionpolynomialdegree)).

Note that the regression is computed using all of the data points and it does not depend on the values of any non-metric facets. For example, adding a legend facet will not change the regression curve.

See [http://en.wikipedia.org/wiki/Simple\_linear\_regression](http://en.wikipedia.org/wiki/Simple_linear_regression). See [http://en.wikipedia.org/wiki/Polynomial\_regression](http://en.wikipedia.org/wiki/Polynomial_regression).

### Groups

- statistics

### See Also

- [FacetChart.xAxisMetric](#attr-facetchartxaxismetric)
- [FacetChart.yAxisMetric](#attr-facetchartyaxismetric)
- [FacetChart.regressionLineProperties](#attr-facetchartregressionlineproperties)

**Flags**: IRW

---
## Attr: FacetChart.valueAxisLabelProperties

### Description
Properties for labels of value axis.

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.facets

### Description
An Array of facets, exactly analogous to [CubeGrid.facets](CubeGrid.md#attr-cubegridfacets), except that:

*   the "inlinedValues" property can be set on a facet to change data representation as described under [Chart.data](Chart.md#attr-chartdata).
*   for a non-inlined facet, Charts support auto-derivation of facetValues from the data.

In all chart types except "Bubble" and "Scatter", the chart displays a value for each discrete value of one facet (i.e. single-facet charts) or it displays a value for each combination of discrete values of two facets (multi-facet charts). The two discrete facets are the [data label facet](#method-facetchartgetdatalabelfacet) and the [legend facet](#method-facetchartgetlegendfacet). They are named based on where the [values](Facet.md#attr-facetvalues) of the facet appear in the chart. The facet whose values are rendered as labels along the data axis or in the main chart area is the data label facet, and the facet whose values are rendered in the legend is the legend facet.

For single-facet charts, most chart types have a data label facet as the first facet but no legend facet. Single-facet Pie charts have a legend facet as the first facet but no data label facet. Bubble and Scatter plots may have a legend facet as the second facet, after the metric facet.

In all multi-facet charts, the data label facet is always first and the legend facet is second. In most chart types the data label facet and the legend facet may be swapped on the fly by the user clicking on the "Swap Facets" item of the context menu.

In the case of [Bar and Column Charts](#class-facetchart), up to three facets are supported, where the first two facets in that case are taken as the data label facets, and the third facet as the legend facet. This works by positioning both data label facets on the same axis, in a way that clearly shows which inner facet values are associated with each outer facet value.

For databound charts, [FacetChart.facetFields](#attr-facetchartfacetfields) may be specified instead of this property. If both are provided, [FacetChart.facetFields](#attr-facetchartfacetfields) is definitive but [Facet](Facet.md#class-facet) properties will be picked up from [FacetChart.facets](#attr-facetchartfacets) also present in the [FacetChart.facetFields](#attr-facetchartfacetfields).

**Flags**: IR

---
## Attr: FacetChart.logScalePointColor

### Description
Whether to use logarithmic scaling for the [color scale](#attr-facetchartcolorscalemetric) of the data points. Defaults to the value of [FacetChart.logScale](#attr-facetchartlogscale).

### Groups

- dataPoints

### See Also

- [FacetChart.pointColorLogBase](#attr-facetchartpointcolorlogbase)

**Flags**: IR

---
## Attr: FacetChart.colorMutePercent

### Description
Should be set to a number between -100 and 100. If set, all colors in the chart are "muted" by this percentage by shifting them toward white (or for negative numbers, toward black).

**Flags**: IR

---
## Attr: FacetChart.dataPointProperties

### Description
Common properties to apply for all data points (see [FacetChart.showDataPoints](#attr-facetchartshowdatapoints)).

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.zoomChartSlider

### Description
Slider controls shown on the mini-chart which is created when [FacetChart.canZoom](#attr-facetchartcanzoom) is enabled.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.radarRotateLabels

### Description
This property controls whether to rotate the labels on the [data label facet](#method-facetchartgetdatalabelfacet) of radar or [FacetChart.stacked](#attr-facetchartstacked) pie charts so that each label is parallel to its radial gradation (these are the labels that appear around the perimeter). For now, "auto" means the same thing as "always" - but this may change in the future if heuristics are added to determine when the affected labels are likely to overlap and not be legible. If rotateLabels is "never" then the labels will not be rotated.

### Groups

- labelsAndTitles

### See Also

- [FacetChart.rotateLabels](#attr-facetchartrotatelabels)
- [FacetChart.radialLabelOffset](#attr-facetchartradiallabeloffset)

**Flags**: IR

---
## Attr: FacetChart.canZoom

### Description
Enables "zooming" on the X axis, specifically, only a portion of the overall dataset is shown in the main chart, and a [second smaller chart](#attr-facetchartzoomchart) appears with slider controls allowing a range to be selected for display in the main chart.

A [labelCollapseMode](#attr-facetchartlabelcollapsemode) is automatically enabled if unset and is based on the type of the first non-null data value.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.showDataValuesMode

### Description
Strategy for determining whether and when to show data-values - either in the chart, near the shape representing a value (above columns of a column chart for example, or adjacent to points in a line chart), in hovers, or some combination of both, including [automatic rotation](#attr-facetchartrotatedatavalues) where supported.

Depending on the chart type, there are different options for showing data-values - eg, [stacked-charts](#attr-facetchartstacked) cannot show values inline in the chart-body; column-charts can, and they can rotate titles if they're wider than their columns; pie charts can show some data-values in the chart but not others; all the types can show values in hovers.

If set to _never_, then data-values will never be shown; _inChartOnly_ allows data-values in the chart-body, where supported and where they will fit, but suppresses them in hovers and _inHoverOnly_ always shows all data-values in hovers.

If set to _auto_, first try to show values in the chart, where the chart-type supports it, and where they'll fit. If they don't all fit, show the ones that do, including rotating them if necessary, if the chart-type allows it, and then switch on hovers as well, as needed. This mode is particularly useful in situations where the chart-type can be changed by the user.

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.tickMarkToValueAxisMargin

### Description
Margin between the tick marks and the labels of the [extra value axes](#attr-facetchartextraaxismetrics).

### Groups

- ticks

**Flags**: IR

---
## Attr: FacetChart.showValueOnHover

### Description
Shows the value of the nearest data value in a floating label whenever the mouse moves within the main chart area. The visual element representing the data value will also be emphasized by brightening or highlighting it (appearance differs by chart type).

Calculates nearest value based on [FacetChart.getNearestDrawnValue](#method-facetchartgetnearestdrawnvalue).

The data value will be formatted using [FacetChart.formatDataValue](#method-facetchartformatdatavalue). The label's appearance is controlled by [FacetChart.hoverLabelProperties](#attr-facetcharthoverlabelproperties).

### Groups

- appearance

**Deprecated**

**Flags**: IR

---
## Attr: FacetChart.maxBarThickness

### Description
Bars will not be drawn over this thickness, instead, margins will be increased.

### Groups

- barChart

### See Also

- [FacetChart.getMinClusterSize](#method-facetchartgetminclustersize)

**Flags**: IR

---
## Attr: FacetChart.drawTitleBackground

### Description
should a background color be set behind the Title. Use [FacetChart.titleBackgroundProperties](#attr-facetcharttitlebackgroundproperties) to set these values if this is true.

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.standardDeviations

### Description
When [FacetChart.showStandardDeviationLines](#attr-facetchartshowstandarddeviationlines) is set, the number of standard deviation lines drawn and their respective standard deviation away from the mean are specified by this property. The default is to display lines corresponding to the mean plus or minus one standard deviation.

Note that having zero in this list of standard deviations is identical to drawing a line at the mean.

For example assume that chart1 and chart2 both plot data with mean 1 and standard deviation 0.1. chart1 will draw a blue line at the value 1 and two red lines at the values 0.7 and 1.2. chart2 will draw three red lines at values 0.9, 1.0, and 1.1.

```
 isc.FacetChart.create({
     ID: "chart1",
     standardDeviations: [-3, 2],
     showExpectedValueLine: true,
     showStandardDeviationLines: true,
     expectedValueLineProperties: { lineColor: "blue" },
     standardDeviationLineProperties: { lineColor: "red" },
     // ...
 });

 isc.FacetChart.create({
     ID: "chart2",
     standardDeviations: [-1, 0, 1],
     showExpectedValueLine: false,
     showStandardDeviationLines: true,
     expectedValueLineProperties: { lineColor: "blue" },
     standardDeviationLineProperties: { lineColor: "red" },
     // ...
 });
 
```

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.gradationZeroLineProperties

### Description
Properties for the gradation line drawn for zero (slightly thicker by default).

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.hoverRectProperties

### Description
Properties for rectangle that draws behind of a floating hover label that represents the data value. See [FacetChart.showValueOnHover](#attr-facetchartshowvalueonhover) for more details.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.dataLabelFacetsMargin

### Description
Determines separation between the set of inner data labels and the set of outer data labels for charts that support multiple data label facets. See the discussion of "Three Facet Bar and Column Charts" in the [overview](#class-facetchart).

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.lowErrorMetric

### Description
`lowErrorMetric` and [FacetChart.highErrorMetric](#attr-facetcharthigherrormetric) can be used to cause error bars to appear above and below the main data point.

`lowErrorMetric` and `highErrorMetric` provide the name of an additional attributes that appears in each Record holding the low error value and high error value respectively.

Error bars are supported for single-axis charts only.

### See Also

- [FacetChart.metricFacetId](#attr-facetchartmetricfacetid)

**Flags**: IR

---
## Attr: FacetChart.legendLabelProperties

### Description
Properties for labels shown next to legend color swatches.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.drawTitleBoundary

### Description
Whether a boundary should be drawn below the title area for circumstances where the chart area already has an outer border. If the chart has no outer border, then the [FacetChart.titleBackgroundProperties](#attr-facetcharttitlebackgroundproperties) settings should be used instead.

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.scaleStartColor

### Description
The starting color of the color scale when the data points are colored according to a [color scale metric](#attr-facetchartcolorscalemetric). If neither this property nor the [scaleEndColor](#attr-facetchartscaleendcolor) is set then the whole color range is used by default.

Note that using CSS color shortcuts (e.g. "lightblue") is not allowed for this property.

### Groups

- dataPoints

**Flags**: IRW

---
## Attr: FacetChart.legendRectHeight

### Description
If drawing a border around the legend, the height of the drawn Rectangle.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.logScale

### Description
Whether to use logarithmic scaling for values.

Logarithmic scale charts show an equivalent percentage increase as equivalent distance on the chart. That is, 10 and 100 are the same distance apart as 100 and 1000 (each being a 10 times or 1000% increase).

**Flags**: IR

---
## Attr: FacetChart.legendAlign

### Description
Horizontal alignment of the chart's [legend widget](#attr-facetchartshowlegend).

### Groups

- legend

**Flags**: IRW

---
## Attr: FacetChart.dataLineType

### Description
How to draw lines between adjacent data points in Line and Scatter charts. See [DataLineType](../main_2.md#type-datalinetype).

Does not apply to boundary lines for shapes in Area or Radar plots.

**Flags**: IRW

---
## Attr: FacetChart.logGradations

### Description
When [FacetChart.useLogGradations](#attr-facetchartuseloggradations) is set, gradation lines to show in between powers, expressed as a series of integer or float values between 1 and [FacetChart.logBase](#attr-facetchartlogbase).

Some common possibilities (for base 10):

```
    [ 1 ] // show only orders of magnitude (0.1, 1, 10, 100, etc)
    [ 1, 5 ] // show only orders of magnitude plus halfway mark
    [ 1, 2, 4, 8 ] // show powers of 2 between orders
    [ 1, 2.5, 5, 7.5 ] // show quarters
 
```
Or base 2:
```
    [ 1 ]
    [ 1, 1.5 ]
 
```

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.shadowProperties

### Description
Properties for shadows.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.dataPointSize

### Description
Size in pixels for data points drawn for line, area, radar and other chart types.

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.valueLineProperties

### Description
Properties for a "value line" - a line shows where a particular discrete value is placed, eg, vertical lines connecting points of a line chart to the X axis, or radial lines in a Radar chart.

**Flags**: IR

---
## Attr: FacetChart.allowedChartTypes

### Description
Other [chart types](../main.md#type-charttype) that the end user will be allowed to switch to, using the built-in context menu.

The actual list of ChartTypes displayed in the context menu may be a subset of `allowedChartTypes`, since the FacetChart will automatically disallow certain modes that are clearly invalid, for example, not allowing switching to Pie mode if either [FacetChart.canZoom](#attr-facetchartcanzoom) is enabled, or if the chart is [multi-axis](#attr-facetchartextraaxismetrics).

**Flags**: IRW

---
## Attr: FacetChart.dataShapeProperties

### Description
Properties for data shapes (filled areas in area or radar charts).

**Flags**: IR

---
## Attr: FacetChart.tickLength

### Description
Length of the tick marks used when either [FacetChart.showXTicks](#attr-facetchartshowxticks) or [FacetChart.showYTicks](#attr-facetchartshowyticks) is enabled, or when [extra value axes](#attr-facetchartextraaxismetrics) are in use.

If minor tick marks are also shown, their length is controlled by [FacetChart.minorTickLength](#attr-facetchartminorticklength).

### Groups

- ticks

**Flags**: IRW

---
## Attr: FacetChart.dataMargin

### Description
For rectangular charts (bar, column, line), margin around the inside of the main chart area, so that data elements are not flush to edge.

### Groups

- chartFeatures

**Flags**: IR

---
## Attr: FacetChart.showScatterLines

### Description
Whether to draw lines between adjacent data points in "Scatter" plots. See also [DataLineType](../main_2.md#type-datalinetype) for enabling smoothing.

**Flags**: IRW

---
## Attr: FacetChart.brightenPercent

### Description
When [FacetChart.highlightDataValues](#attr-facetcharthighlightdatavalues) is true, sets the percentage by which to brighten filled data-shapes in some [chart-types](#attr-facetchartcharttype) as the mouse is moved over the chart. Affects Bar, Column, Pie and Doughnut charts, and will brighten either the shape's fill-color or its border-color, depending on the value of [FacetChart.brightenAllOnHover](#attr-facetchartbrightenallonhover).

Valid values are between 0 and 100, inclusive.

The property default may vary based on the currently loaded skin.

### See Also

- [FacetChart.dataShapeProperties](#attr-facetchartdatashapeproperties)
- [FacetChart.dataOutlineProperties](#attr-facetchartdataoutlineproperties)

**Flags**: IRW

---
## Attr: FacetChart.gradationGaps

### Description
Candidate gradation gaps to evaluate when trying to determine what gradations should be displayed on the primary axis, which is typically the y (vertical) axis except for Bar charts.

Candidates are expressed as a series of numbers between 1 and 10, representing boundaries within a given order of magnitude (power of 10).

For example, the setting \[1, 2.5, 5\] means that, for a chart showing values that are only between 0 and 1, gradations of 0.1, 0.25 and 0.5 would be evaluated to see which is a closer fit given the [FacetChart.pixelsPerGradation](#attr-facetchartpixelspergradation) setting and the chart's height. The same setting, with a chart showing values from 0 to 1,000,000 would imply that gradation gaps of 100,000, 250,000 and 500,000 would be evaluated.

### Groups

- gradations

**Flags**: IRW

---
## Attr: FacetChart.chartRectMargin

### Description
Margin around the main chart rect: between title and chart, between chart and axis labels, and chart rect and right edge of chart.

### Groups

- chartFeatures

**Flags**: IR

---
## Attr: FacetChart.autoScrollData

### Description
For some [chart-types](#attr-facetchartcharttype), should the chart body be automatically expanded and scrollbars introduced according to data?

When true for a column, histogram, line, or area chart that has [facet values displayed along the x-axis](#method-facetchartgetdatalabelfacet), the chart expands horizontally, showing a scroll bar, if that's needed to make room for the facet value labels or, for column and histogram charts, to make space for the [minimum configured bar \\n thicknesses](#method-facetchartgetminclustersize) or the margins between them.

When true for a Bar chart, expansion and scrollbar are vertical, and also make space for the [minimum configured bar thicknesses](#method-facetchartgetminclustersize) or the margins between them.

Note that this feature is incompatible with the following properties:

*   [LabelCollapseMode](../main.md#type-labelcollapsemode) (other than the default of "none")
*   [FacetChart.rotateLabels](#attr-facetchartrotatelabels) (in "auto" mode)
*   [canDragScroll](DrawPane.md#attr-drawpanecandragscroll)
*   [FacetChart.canZoom](#attr-facetchartcanzoom)

If [FacetChart.rotateLabels](#attr-facetchartrotatelabels) is set to "auto" it will be treated as "never" if `autoScrollData` has been set. If any of the other properties have non-default values, a warning will be logged and `autoScrollData` will be disabled. The factors used to drive expansion can be limited by setting [AutoScrollDataApproach](../main.md#type-autoscrolldataapproach). You can also enforce a minimum size for the chart-content, and scrollbars will be introduced if this widget shrinks below that size. See [autoScrollContent](#attr-facetchartautoscrollcontent), along with [minContentWidth](#attr-facetchartmincontentwidth) and [minContentHeight](#attr-facetchartmincontentheight).

### See Also

- [FacetChart.canZoom](#attr-facetchartcanzoom)
- [FacetChart.rotateLabels](#attr-facetchartrotatelabels)
- [LabelCollapseMode](../main.md#type-labelcollapsemode)
- [FacetChart.getMinClusterSize](#method-facetchartgetminclustersize)
- [DrawPane.canDragScroll](DrawPane.md#attr-drawpanecandragscroll)

**Flags**: IRW

---
## Attr: FacetChart.dataFetchMode

### Description
FacetCharts do not yet support paging, and will fetch all records that meet the criteria.

### Groups

- databinding

**Flags**: IRW

---
## Attr: FacetChart.radialLabelOffset

### Description
Distance in pixels that radial labels are offset from the outside of the circle. Default can vary depending upon [ChartType](../main.md#type-charttype) and [FacetChart.radarRotateLabels](#attr-facetchartradarrotatelabels).

### Groups

- chartProperties

**Flags**: IR

---
## Attr: FacetChart.allowBubbleGradients

### Description
Setting this flag to `false` prevents the chart from drawing fill gradients into the bubbles of each data point. This flag is required to be set for IE8 and earlier in order to draw bubble charts displaying high volumes of data.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.showPointSizeLegend

### Description
Whether to show an additional legend to the right of the chart to indicate [point size](#attr-facetchartpointsizemetric). The default is `true` for bubble charts and `false` for all other chart types.

### Groups

- dataPoints

### See Also

- [FacetChart.pointSizeGradations](#attr-facetchartpointsizegradations)
- [FacetChart.usePointSizeLogGradations](#attr-facetchartusepointsizeloggradations)
- [FacetChart.pointSizeLogGradations](#attr-facetchartpointsizeloggradations)
- [FacetChart.showBubbleLegendPerShape](#attr-facetchartshowbubblelegendpershape)

**Flags**: IR

---
## Attr: FacetChart.showStatisticsOverData

### Description
If set, the [mean line](#attr-facetchartshowexpectedvalueline), [standard deviation lines](#attr-facetchartshowstandarddeviationlines), [standard deviation bands](#attr-facetchartbandedstandarddeviations), and [regression curves](#attr-facetchartshowregressionline) are drawn on top of the data rather than underneath.

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.legendMargin

### Description
Space between the legend and the chart rect or axis labels (whatever the legend is adjacent to.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.centerLegend

### Description
Whether to place the [chart legend](#attr-facetchartshowlegend) with respect to the full, scrollable width of the chart when [FacetChart.autoScrollData](#attr-facetchartautoscrolldata) is active. The default of false means that the legend will be placed in the visible, non-overflowed region of the chart, for greater visibility.

Note that alignment of the legend itself is governed by [legendAlign](#attr-facetchartlegendalign).

Note that this setting has no impact on axis labeling, which always occurs with respect to the full, expanded width of the chart.

### Groups

- legend

### See Also

- [FacetChart.showLegend](#attr-facetchartshowlegend)
- [FacetChart.centerTitle](#attr-facetchartcentertitle)
- [FacetChart.autoScrollData](#attr-facetchartautoscrolldata)

**Deprecated**

**Flags**: IR

---
## Attr: FacetChart.titleProperties

### Description
Properties for title label.

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.xAxisMetric

### Description
For scatter charts only, the "id" of the metric facet value to use for the x-axis.

The default x-axis metric is the second value of the metric facet.

**Flags**: IR

---
## Attr: FacetChart.fetchRequestProperties

### Description
If [FacetChart.autoFetchData](#attr-facetchartautofetchdata) is `true`, this attribute allows the developer to declaratively specify [DSRequest](../main_2.md#object-dsrequest) properties for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

Note that any properties governing more specific request attributes for the initial fetch (such as [FacetChart.autoFetchTextMatchStyle](#attr-facetchartautofetchtextmatchstyle) and initial sort specifiers) will be applied on top of this properties block.

### Groups

- databinding

**Flags**: IR

---
## Attr: FacetChart.showXTicks

### Description
When set, ticks are shown for the X (horizontal) axis for Scatter plots or Bar charts.

### Groups

- ticks

### See Also

- [FacetChart.showYTicks](#attr-facetchartshowyticks)

**Flags**: IRW

---
## Attr: FacetChart.zoomSelectionChartProperties

### Description
Properties to further configure the [FacetChart.zoomSelectionChart](#attr-facetchartzoomselectionchart).

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.regressionPolynomialDegree

### Description
For scatter plots only, specify the degree of polynomial to use for any polynomial regression that is calculated.

### Groups

- statistics

**Flags**: IRW

---
## Attr: FacetChart.legendRectProperties

### Description
Properties for rectangle around the legend as a whole.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.showDataPoints

### Description
For Line, Area, Radar, Scatter or Bubble charts, whether to show data points for each individual data value.

If shown, the [FacetChart.pointClick](#method-facetchartpointclick) and [FacetChart.getPointHoverHTML](#method-facetchartgetpointhoverhtml) APIs can be used to create interactivity.

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.showStandardDeviationLines

### Description
Display multiple [standard deviations](#method-facetchartgetstddev) away from the mean as lines. The exact deviations to display can be customized with [FacetChart.standardDeviations](#attr-facetchartstandarddeviations).

Note that these standard deviations are computed using all of the data points, pooled across all facets. The computation relies only on the values of the main value axis metric and the [probability metric](#attr-facetchartprobabilitymetric).

See [http://en.wikipedia.org/wiki/Standard\_deviation](http://en.wikipedia.org/wiki/Standard_deviation).

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.minDataPointSize

### Description
The minimum allowed data point size when controlled by [FacetChart.pointSizeMetric](#attr-facetchartpointsizemetric).

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.barProperties

### Description
Properties for bar

### Groups

- barChart

**Flags**: IRW

---
## Attr: FacetChart.hoverLabelProperties

### Description
Properties for text in a floating label that represents the data value shown whenever the mouse moves withing the main chart area when [FacetChart.showValueOnHover](#attr-facetchartshowvalueonhover) is enabled.

### Groups

- appearance

### See Also

- [FacetChart.hoverLabelPadding](#attr-facetcharthoverlabelpadding)

**Flags**: IR

---
## Attr: FacetChart.pieBorderProperties

### Description
Properties for the border around a pie chart.

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.autoScrollContent

### Description
When set to true, introduces scrollbars when this widget is smaller than the specified chart-content minimum [width](#attr-facetchartmincontentwidth) or [height](#attr-facetchartmincontentheight). These minimum sizes limit all chart-content, including data and labels, titles and legends.

See [autoScrollData](#attr-facetchartautoscrolldata) for a means to introduce scrolling according to the data being displayed.

**Flags**: IRW

---
## Attr: FacetChart.showDataLabels

### Description
If set to `false`, data labels for values are entirely omitted.

This property would generally only be set to `false` if several small charts are shown together and the data labels are drawn elsewhere on the screen (above an entire stack of charts, for instance) or are otherwise implicit.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.rotateDataValues

### Description
This property controls whether to rotate the labels shown for data-values in [Column-type charts](../main.md#type-charttype). "auto" will rotate all data-values if any of them are wider than their columns. In all cases, whether rotated or not, data-values are hidden and instead shown in hovers if any of them exceed their bar's width.

### Groups

- labelsAndTitles

### See Also

- [FacetChart.rotateLabels](#attr-facetchartrotatelabels)

**Flags**: IRW

---
## Attr: FacetChart.minBarThickness

### Description
If bars would be smaller than this size, margins are reduced until bars overlap.

### Groups

- barChart

### See Also

- [FacetChart.getMinClusterSize](#method-facetchartgetminclustersize)

**Flags**: IR

---
## Attr: FacetChart.valueProperty

### Description
Property in each record that holds a data value. For databound charts, if `valueProperty` isn't set in the chart instance, it will be auto-derived from the [DataSource](DataSource.md#class-datasource) fields. The first numeric-typed DataSource field will be assumed to be the `valueProperty`.

Not used if there is an inline facet, see [Chart.data](Chart.md#attr-chartdata).

### Groups

- databinding

### See Also

- [FacetChart.facetFields](#attr-facetchartfacetfields)

**Flags**: IR

---
## Attr: FacetChart.majorTickGradations

### Description
List of tick marks that should be drawn as major ticks, expressed as a series of numbers between 1 and 10, representing boundaries within a given order of magnitude (power of 10). These numbers must be multiples of [FacetChart.gradationGaps](#attr-facetchartgradationgaps), or no ticks will end up as minor ticks.

The default setting of \[1\] means that major ticks are used for powers of 10 only. A setting of \[1,5\] would mean that major ticks are also used at half-orders of magnitude, such as 0.5 or 50. For example, if used with a [FacetChart.gradationGaps](#attr-facetchartgradationgaps) setting of \[1,2.5\] for a chart showing values between 0 and 1, this would result in major ticks at 0, 1 and 0.5, and minor ticks at 0.25 and 0.75.

See also [FacetChart.majorTickTimeIntervals](#attr-facetchartmajorticktimeintervals) for controlling major vs minor ticks for the X-axis of time/date-valued Scatter plots.

### Groups

- ticks

**Flags**: IR

---
## Attr: FacetChart.labelCollapseMode

### Description
What to do when there are too many data points to be able to show labels for every data point at the current chart size - see [LabelCollapseMode](../main.md#type-labelcollapsemode).

Each of the possible strategies is re-applied when the user resizes the chart as a whole, so if labels are omitted the user can make them visible via resize or zoom.

If the labelCollapseMode is "numeric" then vertical lines will be drawn at gradation values automatically chosen by the chart.

If the labelCollapseMode is "time" then vertical lines are drawn to represent a sequence of significant datetime values on the x-axis, such as the first day of the month or week. The chart automatically chooses the sequence of Dates such that the spacing between them expresses the smallest granularity of time possible while still allowing the axis labels to make good use of the space. If, for example, the Date values in the data span a few years in time then the chart may select January 1 of the same year of the earliest data point and every January 1 thereafter (in range of the data) as the sequence of Dates and label each Date by the four-digit year. If the time span of the data values is on the order of minutes then the chart may select multiples of 15 minutes as the seqeunce of Dates. FacetChart currently supports the following granularities of time: years, quarters, months, weeks, days, hours, half-hours, quarter-hours, 5 minutes, minutes, 30 seconds, and 15 seconds.

The format of the Date labels is fixed by FacetChart. In particular, [FacetChart.formatAxisValue](#method-facetchartformataxisvalue) will not be called on values for the x-axis. However, FacetChart uses [DateUtil.shortMonthNames](DateUtil.md#classattr-dateutilshortmonthnames) for the time granularities of quarters, months, and weeks, uses the [default short time format](Time.md#classmethod-timesetshortdisplayformat) to format labels for time granularities from minutes to hours, and uses the [default time format](Time.md#classmethod-timesetnormaldisplayformat) to format labels for the time granularities of 15 seconds and 30 seconds. The label format can be customized by changing these three formatters. Also note that for the time granularity of weeks the sequence of Dates will be the first day of each week, as specified by [DateUtil.setFirstDayOfWeek](DateUtil.md#classmethod-dateutilsetfirstdayofweek).

Note that if the labelCollapseMode is "time" or "numeric" then the [data](#attr-facetchartdata) must be initially sorted with the [data label facet](#method-facetchartgetdatalabelfacet)'s values in ascending order.

### Groups

- zoom

### See Also

- [FacetChart.formatAxisValue](#method-facetchartformataxisvalue)

**Flags**: IR

---
## Attr: FacetChart.gradationTickMarkLength

### Description
—

### Groups

- gradations

### See Also

- [FacetChart.tickLength](#attr-facetchartticklength)

**Deprecated**

**Flags**: IR

---
## Attr: FacetChart.titleBoundaryProperties

### Description
Properties for bottom boundary of the title area, when there is already an outer container around the whole chart. see [FacetChart.drawTitleBoundary](#attr-facetchartdrawtitleboundary)

### Groups

- chartTitle

**Flags**: IR

---
## Attr: FacetChart.xAxisStartValue

### Description
For Bubble and Scatter charts only, the start value for the x-axis.

Defaults to 0, or to a value that makes good use of horizontal space based on [FacetChart.minXDataSpreadPercent](#attr-facetchartminxdataspreadpercent).

If the x-axis metric is date-valued, this value should be a date (typically applies to Scatter charts only).

### See Also

- [FacetChart.axisStartValue](#attr-facetchartaxisstartvalue)

**Flags**: IR

---
## Attr: FacetChart.minChartHeight

### Description
Minimum height for this chart instance.

**Flags**: IR

---
## Attr: FacetChart.showDataAxisLabel

### Description
Whether to show a label for the data axis as a whole (the data axis is where labels for each data point appear). If true, [Facet.title](Facet.md#attr-facettitle) for the data label facet will be shown as the label.

Automatically disabled for non-rectangular charts (eg Pie, Radar).

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.formatStringFacetValueIds

### Description
Whether to call [FacetChart.formatAxisValue](#method-facetchartformataxisvalue) or [FacetChart.formatFacetValueId](#method-facetchartformatfacetvalueid) on a facet value id when the id is a string. Can be set false to allow the formatting function(s) to be written without having to handle the string case.

### See Also

- [FacetChart.formatAxisValue](#method-facetchartformataxisvalue)
- [FacetChart.formatFacetValueId](#method-facetchartformatfacetvalueid)

**Flags**: IRW

---
## Attr: FacetChart.pixelsPerGradation

### Description
Ideal number of pixels to leave between each gradation on the primary axis, which is typically the y (vertical) axis except for Bar charts.

The chart will detect the range of values being displayed and available pixels on the vertical axis, and generate gradations that are spaced _approximately_ `pixelsPerGradations` apart. Note that the Framework will attempt to approach the specified target gap from above - the chart will never be drawn with gradations spaced closer than `pixelsPerGradation`.

### Groups

- gradations

### See Also

- [FacetChart.otherAxisPixelsPerGradation](#attr-facetchartotheraxispixelspergradation)

**Flags**: IRW

---
## Attr: FacetChart.endValueMetric

### Description
Specifies the attribute in the metric facet that will define the end point of segments in a histogram chart. The start point is set via the [FacetChart.valueProperty](#attr-facetchartvalueproperty).

### Groups

- histogramChart

### See Also

- [FacetChart.metricFacetId](#attr-facetchartmetricfacetid)

**Flags**: IR

---
## Attr: FacetChart.hoverLabelPadding

### Description
An extra amount of padding to show around the [hoverLabel](#attr-facetcharthoverlabelproperties) when [showValueOnHover](#attr-facetchartshowvalueonhover) is enabled.

### Groups

- appearance

**Flags**: IRA

---
## Attr: FacetChart.majorTickTimeIntervals

### Description
When ticks are being [shown on the X axis](#attr-facetchartshowxticks) for a Scatter plot where the X axis uses time/date values, controls the intervals which are shown as major ticks.

The intervals are specified as Strings, in the same way as [FacetChart.otherAxisGradationTimes](#attr-facetchartotheraxisgradationtimes).

For any given interval, the first major tick is shown for the next greatest time unit. For example, for interval such as "2h" (2 hours), the first major tick starts on the day boundary (whether that day boundary is visible in the chart or not).

By default, all ticks are shown as major ticks.

### Groups

- ticks

**Flags**: IRW

---
## Attr: FacetChart.brightenAllOnHover

### Description
When [FacetChart.highlightDataValues](#attr-facetcharthighlightdatavalues) is true, should the whole draw-area of the data-value be brightened by [a percentage](#attr-facetchartbrightenpercent), or just its border?

By default, only the border around the draw-area is brightened.

Only affects Bar, Column, Pie and Doughnut [chart-types](#attr-facetchartcharttype).

**Flags**: IRW

---
## Attr: FacetChart.pointColorLogBase

### Description
When [FacetChart.logScalePointColor](#attr-facetchartlogscalepointcolor) is `true`, this property specifies the base value for logarithmic [color scale metric](#attr-facetchartcolorscalemetric) values.

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.showDetailFields

### Description
This [DataBoundComponent](../main.md#interface-databoundcomponent) property is not applicable to charts.

**Flags**: IR

---
## Attr: FacetChart.useSymmetricStandardDeviations

### Description
Whether to display both the positive and negative of the [standard deviations](#attr-facetchartstandarddeviations).

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.showLegend

### Description
The legend is automatically shown for charts that need it (generally, multi-series charts) but can be forced off by setting showLegend to false.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.gradationLineProperties

### Description
Properties for gradation lines

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.titlePadding

### Description
if aligning the title left or right, the amount of space before (for left aligned) or after (for right aligned) to pad the title from the border edge

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.axisStartValue

### Description
Start value for the primary axis of the chart.

If set to an explicit value, this will be respected. If unset, the axis start value will default to 0, or to a value that makes good use of vertical space based on [FacetChart.minDataSpreadPercent](#attr-facetchartmindataspreadpercent).

For multi-axis charts, Bubble charts, and Scatter charts, the `facetChart.axisStartValue` affects only the **first** axis of the chart. Start values for other axes of multi-axis charts can be set on a per-axis basis via [MetricSettings.axisStartValue](MetricSettings.md#attr-metricsettingsaxisstartvalue). For Scatter charts, the [FacetChart.xAxisStartValue](#attr-facetchartxaxisstartvalue) property must be used to set the start value of the x-axis.

Note that if this chart's data includes points that fall below this value, they are ommitted and effectively treated as null values. For charts showing a data line, developers may wish to set [FacetChart.discontinuousLines](#attr-facetchartdiscontinuouslines) to true in this case.

**Flags**: IR

---
## Attr: FacetChart.zoomStartPosition

### Description
For a [zoomed chart](#attr-facetchartcanzoom), determines what portion of the overall dataset should be initially shown in the main chart.

Default is to show the end of the dataset if the X axis shows time and includes today's date, otherwise to show the start of the dataset.

Set this property to override this default, or use [FacetChart.zoomStartValue](#attr-facetchartzoomstartvalue) and [FacetChart.zoomEndValue](#attr-facetchartzoomendvalue) to start with a particular range.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.pieLabelLineExtent

### Description
How far label lines stick out of the pie radius in a Pie chart in stacked mode.

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.scaleEndColor

### Description
The ending color of the color scale when the data points are colored according to a [color scale metric](#attr-facetchartcolorscalemetric). If neither this property nor the [scaleStartColor](#attr-facetchartscalestartcolor) is set then the whole color range is used by default.

Note that using CSS color shortcuts (e.g. "lightblue") is not allowed for this property.

### Groups

- dataPoints

**Flags**: IRW

---
## Attr: FacetChart.autoScrollDataApproach

### Description
If set, overrides the default behavior of [FacetChart.autoScrollData](#attr-facetchartautoscrolldata), potentially limiting what factors drive the automatic expansion of the chart. (The "both" setting is no different than the default of null.)

When labels are on the x-axis, and if you're sizing bars very tightly to labels by defining [FacetChart.getMinClusterSize](#method-facetchartgetminclustersize), you may not want label-driven expansion, as the default separation assigned between them is very generous, and is based on the widest labels. (You may also set [FacetChart.minLabelGap](#attr-facetchartminlabelgap) to gain more control over the separation.)

### See Also

- [FacetChart.autoScrollData](#attr-facetchartautoscrolldata)

**Flags**: IRW

---
## Attr: FacetChart.dataLineProperties

### Description
Properties for lines that show data (as opposed to gradations or borders around the data area).

**Flags**: IR

---
## Attr: FacetChart.yAxisLabelAlign

### Description
Horizontal alignment of y-axis labels, shown to the left of the chart.

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.minorTickLength

### Description
Length of minor ticks marks shown along axis, if [minor tick marks](#attr-facetchartshowminorticks) are enabled.

### Groups

- ticks

### See Also

- [FacetChart.tickLength](#attr-facetchartticklength)

**Flags**: IRW

---
## Attr: FacetChart.minXDataSpreadPercent

### Description
For scatter charts only, if all data points would be spread across less than [FacetChart.minXDataSpreadPercent](#attr-facetchartminxdataspreadpercent) of the x-axis, the start value of x-axis will be automatically adjusted to make better use of space.

Setting an explicit [FacetChart.xAxisStartValue](#attr-facetchartxaxisstartvalue) disables this behavior, as does setting `minXDataSpreadPercent` to 0.

### See Also

- [FacetChart.minDataSpreadPercent](#attr-facetchartmindataspreadpercent)

**Flags**: IR

---
## Attr: FacetChart.otherAxisGradationGaps

### Description
Like [FacetChart.gradationGaps](#attr-facetchartgradationgaps), except allows control of gradations for the X (horizontal) axis, for Scatter charts only.

See also [FacetChart.otherAxisGradationTimes](#attr-facetchartotheraxisgradationtimes) for control of gradations when the X axis is time-valued.

Defaults to the value of [FacetChart.pixelsPerGradation](#attr-facetchartpixelspergradation) if unset.

### Groups

- gradations

**Flags**: IRW

---
## Attr: FacetChart.zoomEndValue

### Description
For a [zoomed chart](#attr-facetchartcanzoom), end value of the data range shown in the main chart. If [FacetChart.zoomStartValue](#attr-facetchartzoomstartvalue) is not also set on intialization (or if [setZoomStartValue(null)](#method-facetchartsetzoomstartvalue) is called after initialization) then the range shown will be from the beginning of the dataset up to `zoomEndValue`.

The value provided should be a value in the range of the facet for the X axis, for example, for a time-based axis, a Date instance, for a numeric axis, a Number, for an axis that just has text labels (such as city names), a String.

### Groups

- zoom

**Flags**: IRW

---
## Attr: FacetChart.zoomShowSelection

### Description
Whether the selected range should be shown in a different style, which can be configured via [FacetChart.zoomSelectionChartProperties](#attr-facetchartzoomselectionchartproperties). This has performance consequences and makes the rendering of the mini-chart slightly slower.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.outerLabelFacetLineProperties

### Description
Properties for the lines drawn to show the span of outer data label facet values, if present.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.clusterMarginRatio

### Description
For clustered charts, ratio between margins between individual bars and margins between clusters.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.stacked

### Description
Whether to use stacking for charts where this makes sense (column, area, pie, line and radar charts). If stacked is not set and two facets are supplied, clustering is assumed. If null (the default), line charts will be unstacked, and others will be stacked.

### Groups

- chartType

**Flags**: IRW

---
## Attr: FacetChart.drawLegendBoundary

### Description
Whether a boundary should be drawn above the Legend area for circumstances where the chart area already has an outer border. If the chart has no outer border, then the [FacetChart.legendRectProperties](#attr-facetchartlegendrectproperties) settings should be used instead.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.proportional

### Description
For multi-facet charts, render data values as a proportion of the sum of all data values that have the same label.

Gradation labels will be switched to show percentage instead of absolute values.

This setting is valid only for Column, Bar, Area and Radar chart types and only in [stacked](#attr-facetchartstacked) mode. Stacked columns will be as tall as the chart rect and stacked bars will be as wide as the chart rect. Area and Radar charts will be completely filled except for facet values where all values are 0.

**Flags**: IRW

---
## Attr: FacetChart.showExpectedValueLine

### Description
Display a line at the [mean value](#method-facetchartgetmean).

Note that this expected value is computed using all of the data points, pooled across all facets. The computation relies only on the values of the main value axis metric and the [probability metric](#attr-facetchartprobabilitymetric).

See [http://en.wikipedia.org/wiki/Expected\_value](http://en.wikipedia.org/wiki/Expected_value).

**Flags**: IR

---
## Attr: FacetChart.regressionLineProperties

### Description
Properties for the [regression line](#attr-facetchartshowregressionline).

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.zoomStartValue

### Description
For a [zoomed chart](#attr-facetchartcanzoom), start value of the data range shown in the main chart. If [FacetChart.zoomEndValue](#attr-facetchartzoomendvalue) is not also set on initialization (or if [setZoomEndValue(null)](#method-facetchartsetzoomendvalue) is called after initialization) then the range shown will be from `zoomStartValue` to the end of the dataset.

The value provided should be a value in the range of the facet for the X axis, for example, for a time-based axis, a Date instance, for a numeric axis, a Number, for an axis that just has text labels (such as city names), a String.

### Groups

- zoom

**Flags**: IRW

---
## Attr: FacetChart.legendTextPadding

### Description
Padding between color swatch and its label.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.probabilityMetric

### Description
The "id" of the metric facet value that assigns a probability to each combination of facets and their values. Each probability must be a non-negative number. These probabilities are used by all methods of FacetChart that calculate statistical values (e.g. [FacetChart.getMean](#method-facetchartgetmean) and [FacetChart.getStdDev](#method-facetchartgetstddev)). The default value of this property is null which causes the FacetChart to assign probabilities to the data records according to a uniform probability distribution.

Note that the FacetChart handles cases where the sum total of all probabilities in the [FacetChart.data](#attr-facetchartdata) is not exactly one by scaling the assigned probabilities.

### Groups

- statistics

### See Also

- [FacetChart.getMean](#method-facetchartgetmean)
- [FacetChart.getMedian](#method-facetchartgetmedian)
- [FacetChart.getStdDev](#method-facetchartgetstddev)
- [FacetChart.getVariance](#method-facetchartgetvariance)

**Flags**: IR

---
## Attr: FacetChart.barMargin

### Description
Distance between bars. May be reduced if bars would be smaller than [FacetChart.minBarThickness](#attr-facetchartminbarthickness).

### Groups

- barChart

**Flags**: IR

---
## Attr: FacetChart.dataOutlineProperties

### Description
Properties for lines that outline a data shape (in filled charts such as area or radar charts).

**Flags**: IR

---
## Attr: FacetChart.dataLabelToValueAxisMargin

### Description
Margin between the edge of the chart and the data labels of the data label axis. This will default to the [chart margin](#attr-facetchartchartrectmargin) if unset and should not exceed it. Setting this property to some valid non-null value has the impact of moving the data labels towards to chart, away from the axis label.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.expectedValueLineProperties

### Description
Properties for the [line drawn at the mean value](#attr-facetchartshowexpectedvalueline).

Note that for rectangular charts the properties are for a [DrawLine](DrawLine.md#class-drawline), and for radar charts the properties are for a [DrawOval](DrawOval.md#class-drawoval).

**Flags**: IR

---
## Attr: FacetChart.showDataValues

### Description
Should data values be shown as text labels near the shape representing the value, for example, above columns of a column chart, or adjacent to points in a line chart?

If set to false, then data values will not be shown.

If set to true, data values will be shown unless the data density is high enough that labels will potentially overlap, in which case, data values will not be shown and hovers will be shown instead, in the same way as [FacetChart.showValueOnHover](#attr-facetchartshowvalueonhover) shows hovers.

### Groups

- labelsAndTitles

**Deprecated**

**Flags**: IR

---
## Attr: FacetChart.printZoomChart

### Description
Should the [zoom chart](#attr-facetchartcanzoom) be printed with this `FacetChart`? If `true`, then the SVG string returned by [DrawPane.getSvgString](DrawPane.md#method-drawpanegetsvgstring) will include the zoom chart's SVG as well.

### Groups

- printing

**Flags**: IRWA

---
## Attr: FacetChart.standardDeviationBandProperties

### Description
An Array of DrawRect properties to specify the bands between the [standard deviation lines](#attr-facetchartshowstandarddeviationlines). The length of the Array must be one less than the length of the [FacetChart.standardDeviations](#attr-facetchartstandarddeviations) Array.

Having no band between certain standard deviations from the mean can be specified by having a null element at the corresponding index of this Array.

Note that if [FacetChart.useSymmetricStandardDeviations](#attr-facetchartusesymmetricstandarddeviations) is set then for each standard deviation band that is drawn a corresponding band will also be drawn on the opposite side of the mean line.

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.showShadows

### Description
Whether to automatically show shadows for various charts.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.showInlineLabels

### Description
Causes labels for the X axis to be shown above the axis and to the right of the gradation line they label, making for a vertically more compact chart at the risk of gradation labels being partially obscured by data values. Also causes the last label to be skipped (nowhere to place it).

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.titleAlign

### Description
Horizontal alignment of the chart's [title](#attr-facetcharttitle) with respect to the the visible chart-width.

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.titleRectHeight

### Description
The height of the bordered rect around the title - defaults to 0 (assuming no border)

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.doughnutRatio

### Description
If showing a doughnut hole (see [FacetChart.showDoughnut](#attr-facetchartshowdoughnut)), ratio of the size of the doughnut hole to the size of the overall pie chart, as a number between 0 to 1.

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.zIndexMetric

### Description
Specifies the attribute in the metric facet that will define the z-ordering of the segments in a histogram chart. If the z-ordering isn't specified, it will be assigned based on data order, with the last data point ordered above the first. Relative z-ordering is only important between segments within the same data label facet, since segments that differ in their data label facet value should never overlap,

Note that zIndex values should be integers between 0 and [FacetChart.maxDataZIndex](#attr-facetchartmaxdatazindex), inclusive, and don't directly map to the [DrawItem.zIndex](DrawItem.md#attr-drawitemzindex) values of the underlying [DrawRect](DrawRect.md#class-drawrect)s. This allows the Framework to use automatic z-ordering in the chart logic without any additional sorting or overhead that would otherwise be required.

### Groups

- histogramChart

### See Also

- [FacetChart.metricFacetId](#attr-facetchartmetricfacetid)
- [FacetChart.maxDataZIndex](#attr-facetchartmaxdatazindex)
- [FacetChart.getDataLabelFacet](#method-facetchartgetdatalabelfacet)

**Flags**: IRW

---
## Attr: FacetChart.showValueAxisLabel

### Description
Whether to show the [FacetChart.valueTitle](#attr-facetchartvaluetitle) (or, in the case of [proportional rendering mode](#attr-facetchartproportional), the [FacetChart.proportionalAxisLabel](#attr-facetchartproportionalaxislabel)) as a label on the value axis.

Automatically disabled for non-rectangular charts (eg Pie, Radar).

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.zoomSelectionChart

### Description
Mini-chart created when [FacetChart.canZoom](#attr-facetchartcanzoom) is enabled. This chart represents the currently selected range of data shown in the main chart.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.valueAxisMargin

### Description
Margin between [multiple value axes](#attr-facetchartextraaxismetrics).

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.highlightDataValues

### Description
Should the draw-area of nearby filled data-value shapes be highlighted as the mouse is moved over some [chart-types](#attr-facetchartcharttype)?

When set to true, data-shapes in Bar, Column, Pie and Doughnut charts can be highlighted by [brightening](#attr-facetchartbrightenallonhover) their fill or border colors by a [percentage](#attr-facetchartbrightenpercent), and by applying a [shadow](#attr-facetchartdatavaluehovershadow) around them.

**Flags**: IRW

---
## Attr: FacetChart.maxDataPointSize

### Description
The maximum allowed data point size when controlled by [FacetChart.pointSizeMetric](#attr-facetchartpointsizemetric).

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.padChartRectByCornerRadius

### Description
If [FacetChart.showChartRect](#attr-facetchartshowchartrect) is enabled and if [FacetChart.chartRectProperties](#attr-facetchartchartrectproperties) specifies a nonzero [rounding](DrawRect.md#attr-drawrectrounding), whether the padding around the inside of the chart rect. should include at least the radius of the rounded corner.

### Groups

- chartFeatures

**Flags**: IR

---
## Attr: FacetChart.axisEndValue

### Description
End value for the primary axis of the chart.

If set to an explicit value, this will be respected. If unset, the axis end value will default to a value large enough to the largest data point, rounded up to the nearest (next) gradation.

For multi-axis charts, Bubble charts, and Scatter charts, the `facetChart.axisEndValue` affects only the **first** axis of the chart. End values for other axes of multi-axis charts can be set on a per-axis basis via [MetricSettings.xAxisEndValue](MetricSettings.md#attr-metricsettingsxaxisendvalue). For Scatter charts, the [FacetChart.xAxisEndValue](#attr-facetchartxaxisendvalue) property must be used to set the end value of the x-axis.

Note that if this chart's data includes points that fall above this value, they are ommitted and effectively treated as null values. For charts showing a data line, developers may wish to set [FacetChart.discontinuousLines](#attr-facetchartdiscontinuouslines) to true in this case.

**Flags**: IR

---
## Attr: FacetChart.extraAxisMetrics

### Description
Defines the set of metrics that will be plotted as additional vertical axes. See the main [FacetChart](#class-facetchart) docs for an overview of how multi-axis charts are used.

Each metric corresponds to different value property of the data records and superimposes its drawn data onto the chart rectangle. The value properties are called metrics, and they can be either the [FacetChart.valueProperty](#attr-facetchartvalueproperty) or the "id" of a [FacetValue](../main.md#object-facetvalue) of the inlined [Facet](Facet.md#class-facet) (which is then called the metric facet). Each value axis has its own gradations that are shown as tick marks along the length of the axis. This property, extraAxisMetrics, specifies the metrics to use for additional value axes to the main value axis.

The additional value axis may have their own gradations, chart type, log scale, data colors and gradients, and other chart properties. These properties are specified with the [FacetChart.extraAxisSettings](#attr-facetchartextraaxissettings) property.

Value axes, including the main value axis, are labelled in the legend along with representations of the charted data. The labels are taken from the [FacetValue.title](FacetValue.md#attr-facetvaluetitle) of each metric's FacetValue (or the [FacetChart.valueTitle](#attr-facetchartvaluetitle) if the metric is the [FacetChart.valueProperty](#attr-facetchartvalueproperty)).

The order of the metrics determines the position of the corresponding axes on the chart as well as the z-ordering of the corresponding data lines. The first and second extra value axes are placed to the right of the chart rectangle, and any remaining extra value axes are placed to the left of the main value axis (and therefore to the left of the chart rectangle).

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.logScalePointSize

### Description
Whether to use logarithmic scaling for the [data point sizes](#attr-facetchartpointsizemetric). Defaults to the value of [FacetChart.logScale](#attr-facetchartlogscale).

### Groups

- dataPoints

### See Also

- [FacetChart.pointSizeLogBase](#attr-facetchartpointsizelogbase)

**Flags**: IR

---
## Attr: FacetChart.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../main_2.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

### See Also

- [FacetChart.facetFields](#attr-facetchartfacetfields)

**Flags**: IRW

---
## Attr: FacetChart.pointSizeLogGradations

### Description
When [FacetChart.usePointSizeLogGradations](#attr-facetchartusepointsizeloggradations) is set, this property specifies the [pointSizeMetric](#attr-facetchartpointsizemetric) value gradations to show in the [point size legend](#attr-facetchartshowpointsizelegend) in between powers, expressed as a series of integer or float values between 1 and [FacetChart.pointSizeLogBase](#attr-facetchartpointsizelogbase).

### Groups

- gradations

### See Also

- [FacetChart.logGradations](#attr-facetchartloggradations)

**Flags**: IR

---
## Attr: FacetChart.extraAxisSettings

### Description
For charts will multiple vertical axes, optionally provides settings for how each [extra axis metric](#attr-facetchartextraaxismetrics) is plotted. See the main [FacetChart](#class-facetchart) docs for an overview of how multi-axis charts are used.

The chart of each metric's values may be of any rectangular chart type that uses a vertical value axis ("Column", "Area", or "Line" - "Histogram" is not supported). Because the charts will be superimposed over the same drawing area, there can only be one "Column" chart and one "Area" chart. The column chart is placed on the bottom followed by the area chart, and then the line charts are drawn on top in the order of their metric in the [FacetChart.extraAxisMetrics](#attr-facetchartextraaxismetrics) array. If the [chartType](MetricSettings.md#attr-metricsettingscharttype)s are left unspecified then by default the first metric will be drawn as columns and the remaining will be drawn as lines.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.errorBarWidth

### Description
Width of the horizontal line of the "T"-shape portion of the error bar).

**Flags**: IR

---
## Attr: FacetChart.dataColors

### Description
An array of colors to use for a series of visual elements representing data (eg columns, bars, pie slices), any of which may be adjacent to any other.

Colors must be in the format of a leading hash (#) plus 6 hexadecimal digits, for example, "#FFFFFF" is white, "#FF0000" is pure red.

**Flags**: IRW

---
## Attr: FacetChart.bandedBackground

### Description
Whether to show alternating color bands in the background of chart. See [FacetChart.backgroundBandProperties](#attr-facetchartbackgroundbandproperties).

**Flags**: IR

---
## Attr: FacetChart.zoomChartHeight

### Description
Height of the [FacetChart.zoomChart](#attr-facetchartzoomchart). The zoomChart is always as wide as the main chart.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.legendPadding

### Description
Padding around the legend as a whole.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.pieRingBorderProperties

### Description
Properties for pie ring border

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.decimalPrecision

### Description
Default precision used when formatting float numbers for axis labels

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.rotateLabels

### Description
This property controls whether to rotate the labels on the X-axis. If rotateLabels is "always" then all of the data labels will be rotated by 90 degrees. If rotateLabels is "auto" (the default) then the labels will only be rotated if it is required in order for the labels to be legible and non-overlapping. If rotateLabels is "never" then the labels will not be rotated.

Note that automatic rotation is incompatible with setting [FacetChart.getMinClusterSize](#method-facetchartgetminclustersize), so that "auto" will be treated as "never" if that method has been specified on a column, bar, or histogram chart.

### Groups

- labelsAndTitles

### See Also

- [FacetChart.radarRotateLabels](#attr-facetchartradarrotatelabels)

**Flags**: IR

---
## Attr: FacetChart.highErrorMetric

### Description
See [FacetChart.lowErrorMetric](#attr-facetchartlowerrormetric).

**Flags**: IR

---
## Attr: FacetChart.showTitle

### Description
Whether to show a title.

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.pointSizeGradations

### Description
When a [point size legend](#attr-facetchartshowpointsizelegend) is shown, this property controls the number of gradations of the [pointSizeMetric](#attr-facetchartpointsizemetric) that the chart tries to display.

Note that if [FacetChart.usePointSizeLogGradations](#attr-facetchartusepointsizeloggradations) is set then the number of gradations is not given by this property but rather by the entries of [FacetChart.pointSizeLogGradations](#attr-facetchartpointsizeloggradations).

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.useMultiplePointShapes

### Description
Whether the chart should use multiple shapes to show data points. If set to `true` then the chart is allowed to use all [supported shapes](#attr-facetchartpointshapes): circles, squares, diamonds, and triangles. If set to `false` then just the first supported shape (circles, for example) will be used. The default is `false` for bubble charts and [color scale charts](#attr-facetchartcolorscalemetric) and `true` for all other chart types.

### Groups

- dataPoints

**Flags**: IRW

---
## Attr: FacetChart.showBubbleLegendPerShape

### Description
Whether to draw multiple bubble legends horizontally stacked to the right of the chart, one per shape type.

Note that this setting has no effect if [FacetChart.useMultiplePointShapes](#attr-facetchartusemultiplepointshapes) is disabled.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.bubbleHoverMaxDistance

### Description
Maximum distance from the \*outer radius\* of the nearest bubble when hover will be shown.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.dataValueHoverShadow

### Description
When [FacetChart.highlightDataValues](#attr-facetcharthighlightdatavalues) is true, this attribute can be set to a [DrawItem shadow](../main.md#object-shadow) to show around the draw-area of nearby filled data-value shapes as the mouse is moved around in Bar, Column, Pie and Doughnut [chart-types](#attr-facetchartcharttype).

**Flags**: IRW

---
## Attr: FacetChart.pieStartAngle

### Description
Default angle in degrees where pie charts start drawing sectors to represent data values. Default of 0 places the first value starting from the "east" position. Use 270 or -90 for north.

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.pointSizeMetric

### Description
For charts where [FacetChart.showDataPoints](#attr-facetchartshowdatapoints) is enabled, this property specifies an additional metric (i.e. an "id" of a metric facet value) that determines the size of the data points drawn. For example, when a circle is drawn to represent a data point then the size of the data point is the diameter of the circle, in pixels.

The size is calculated by linearly scaling the value of the `pointSizeMetric` of the point between the [FacetChart.minDataPointSize](#attr-facetchartmindatapointsize) and [FacetChart.maxDataPointSize](#attr-facetchartmaxdatapointsize). The data point that has the lowest value for the `pointSizeMetric` will be drawn as a shape `minDataPointSize` pixels in size, and the data point that has the highest value for the `pointSizeMetric` will be drawn as a shape `maxDataPointSize` pixels in size.

Using a log-scale to calulate the size of the data points is achieved by enabling [FacetChart.logScalePointSize](#attr-facetchartlogscalepointsize).

If the [ChartType](../main.md#type-charttype) is `"Bubble"` then the default `pointSizeMetric` is `"pointSize"`.

Note that setting `pointSizeMetric` to non-`null` implicitly enables [FacetChart.showDataPoints](#attr-facetchartshowdatapoints).

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.standardDeviationLineProperties

### Description
Properties for the [standard deviation lines](#attr-facetchartshowstandarddeviationlines).

Note that for rectangular charts the properties are for a [DrawLine](DrawLine.md#class-drawline), and for radar charts the properties are for a [DrawOval](DrawOval.md#class-drawoval).

### Groups

- statistics

**Flags**: IR

---
## Attr: FacetChart.filled

### Description
Whether shapes are filled, for example, whether a multi-series line chart appears as a stack of filled regions as opposed to just multiple lines.

If unset, fills will be automatically used when there are multiple facets and stacking is active (so Line and Radar charts will show stacked regions).

You can explicitly set filled:false to create multi-facet Line or Radar charts where translucent regions overlap, or filled:true to fill in a single-facet Line or Radar chart.

### Groups

- chartType

**Flags**: IRW

---
## Attr: FacetChart.xAxisEndValue

### Description
For Bubble and Scatter charts only, the end value for the x-axis.

If set to an explicit value, this will be respected. If unset, the axis end value will default to a value large enough to show the largest data point.

If the x-axis metric is date-valued, this value should be a date (typically applies to Scatter charts only).

### See Also

- [FacetChart.axisEndValue](#attr-facetchartaxisendvalue)

**Flags**: IR

---
## Attr: FacetChart.otherAxisPixelsPerGradation

### Description
Ideal number of pixels to leave between each gradation on the x (horizontal axis), for Scatter plots only.

Defaults to the value of [FacetChart.pixelsPerGradation](#attr-facetchartpixelspergradation) if unset.

### Groups

- gradations

### See Also

- [FacetChart.pixelsPerGradation](#attr-facetchartpixelspergradation)

**Flags**: IRW

---
## Attr: FacetChart.initialCriteria

### Description
Criteria to be used when [FacetChart.autoFetchData](#attr-facetchartautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: FacetChart.errorLineProperties

### Description
Properties of the lines used to draw error bars (short, horizontal lines at the low and high metric values, and a vertical connecting line).

Note that the [lineColor](DrawItem.md#attr-drawitemlinecolor) property has no effect as the color of the error bars is derived from the color of the data line.

### See Also

- [FacetChart.errorBarColorMutePercent](#attr-facetcharterrorbarcolormutepercent)

**Flags**: IR

---
## Attr: FacetChart.minLabelGap

### Description
Minimum gap between labels on the X axis before some labels are omitted or larger time granularity is shown (eg show days instead of hours) based on the [FacetChart.labelCollapseMode](#attr-facetchartlabelcollapsemode).

Default is based on label orientation. If labels are vertical, the minimum gap is the height of half a line of text. If horizontal it's the width of 4 "X" letters.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.metricFacetId

### Description
Specifies the "id" of the default metric facet value. The default metric is used with [FacetChart.lowErrorMetric](#attr-facetchartlowerrormetric) and [FacetChart.highErrorMetric](#attr-facetcharthigherrormetric) when showing error bars.

**Flags**: IR

---
## Attr: FacetChart.gradationLabelProperties

### Description
Properties for gradation labels

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.showYTicks

### Description
When set, ticks are shown for the Y (vertical) axis if it's a value axis.

Normally, ticks are not shown for the primary axis, since [gradation lines](#method-facetchartgetgradations) show value demarcations. Gradation lines are always show for [extra value axes](#attr-facetchartextraaxismetrics) in multi-axis charts (since there are no gradation lines for the additional axes).

[FacetChart.showXTicks](#attr-facetchartshowxticks) can be used to control whether ticks are shown for the horizontal axis, for certain chart types. See also [FacetChart.majorTickGradations](#attr-facetchartmajortickgradations) for control of which ticks are shown as major vs minor ticks.

### Groups

- ticks

**Flags**: IRW

---
## Attr: FacetChart.dataAxisLabelDelimiter

### Description
Determines how inner and outer data axis labels are separated for charts that support multiple data label facets. See the discussion of "Three Facet Bar and Column Charts" in the [overview](#class-facetchart).

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.useLogGradations

### Description
Whether to use classic logarithmic gradations, where each order of magnitude is shown as a gradation as well as a few intervening lines. Gradations also begin and end on an order of magnitude. For example, 1,2,4,6,8,10,20,40,60,80,100.

Default gradations can be overridden via [FacetChart.logBase](#attr-facetchartlogbase) and [FacetChart.logGradations](#attr-facetchartloggradations).

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.pieLabelAngleStart

### Description
Angle where first label is placed in a Pie chart in stacked mode, in degrees.

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.dataLabelProperties

### Description
Properties for data label

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.maxDataZIndex

### Description
Maximum allowed zIndex that can be specified through [FacetChart.zIndexMetric](#attr-facetchartzindexmetric) in a histogram chart. Any zIndex values exceeding this property will be internally clipped so as to not exceed it. While this property can be increased, note that very large values may hit limitations related to the browser's implementation of the current [DrawPane.drawingType](DrawPane.md#attr-drawpanedrawingtype).

### Groups

- histogramChart

### See Also

- [ChartType](../main.md#type-charttype)
- [FacetChart.zIndexMetric](#attr-facetchartzindexmetric)

**Flags**: IR

---
## Attr: FacetChart.showRadarGradationLabels

### Description
Whether to show gradation labels in radar charts.

### Groups

- radarChart

**Flags**: IR

---
## Attr: FacetChart.radarBackgroundProperties

### Description
Properties for radar background

### Groups

- radarChart

**Flags**: IR

---
## Attr: FacetChart.zoomMutePercent

### Description
[FacetChart.colorMutePercent](#attr-facetchartcolormutepercent) to use for the [FacetChart.zoomChart](#attr-facetchartzoomchart).

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.colorScaleMetric

### Description
For charts where [FacetChart.showDataPoints](#attr-facetchartshowdatapoints) is enabled, this property specifies an additional metric (i.e. an "id" of a metric facet value) that causes the data points to be colored from [FacetChart.scaleStartColor](#attr-facetchartscalestartcolor) to [FacetChart.scaleEndColor](#attr-facetchartscaleendcolor) based on a linear scale over the values of this metric. Log-scaling for color scale is also supported with [FacetChart.logScalePointColor](#attr-facetchartlogscalepointcolor).

**Flags**: IR

---
## Attr: FacetChart.minDataSpreadPercent

### Description
If all data values would be spread across less than [FacetChart.minDataSpreadPercent](#attr-facetchartmindataspreadpercent) of the axis, the start values of axes will be automatically adjusted to make better use of space.

For example, if a column chart has all data values between 500,000 and 500,100, if the axis starts at 0, differences in column heights will be visually indistinguishable. In this case, since all data values appear in well under 30% of the axis length, the default `minDataSpreadPercent` setting would cause the axis to start at a value that would make the column heights obviously different (for example, starting the axis as 500,000).

Setting an explicit [FacetChart.axisStartValue](#attr-facetchartaxisstartvalue) or [FacetChart.axisEndValue](#attr-facetchartaxisendvalue), disables this behavior, as does setting `minDataSpreadPercent` to 0.

For multi-axis charts, use [MetricSettings.minDataSpreadPercent](MetricSettings.md#attr-metricsettingsmindataspreadpercent) for per-axis settings.

For Bubble and Scatter charts, `minDataSpreadPercent` affects only the y-axis of the chart. The property [FacetChart.minXDataSpreadPercent](#attr-facetchartminxdataspreadpercent) must be used to enable the corresponding feature for the x-axis.

**Flags**: IR

---
## Attr: FacetChart.canMoveAxes

### Description
Whether the positions of value axes can be changed. The default is true for charts with three or more vertical, value axes.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.pointShapes

### Description
For charts where [FacetChart.showDataPoints](#attr-facetchartshowdatapoints) is enabled, this property specifies an array of geometric shapes to draw for the data points of each series.

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.data

### Description
Dataset for this chart.

Two basic formats are supported:

*   "Standard model": `data` is an array of CellRecords where each record contains one data value. Each record also contains a property named after each facetId whose value is a facetValueId from that facet.
    
    For example, with a facet with id "regions" and facetValues "west", "north" and "east", and with [FacetChart.valueProperty](#attr-facetchartvalueproperty) with it's default value "\_value", the `data` property could be:
    
    ```
        isc.Chart.create({
           facets:[{ id:"regions" }],
           data : [
              {regions:"west", _value:4},
              {regions:"north", _value:2},
              {regions:"east", _value:5}
           ]
        })
    ```
    If there were a second facet with id "product" and facetValues "cars" and "trucks", a Chart with a complete set of values would be:
    ```
        isc.Chart.create({
           facets:[{ id:"regions" }, { id:"product" }],
           data : [
              {product:"cars", regions:"west", _value:4},
              {product:"cars", regions:"north", _value:2},
              {product:"cars", regions:"east", _value:5},
              {product:"trucks", regions:"west", _value:1},
              {product:"trucks", regions:"north", _value:9},
              {product:"trucks", regions:"east", _value:3}
           ]
        })
    ```
    This 2 facet (or "2 dimensional") dataset, if rendered as a bar chart, would use stacked or clustered bars and a legend.
    
*   "Inlined facet": `data` is a single CellRecord or Array of CellRecords where each record contains multiple data values. In this case, one facet definition is considered "inlined", meaning that the facetValueIds from this facet appear as properties in each record, and each such property holds one data value. For example, a complete chart definition whose dataset is equivalent to the previous example would be:
    ```
        isc.Chart.create({
           facets: [{ 
              inlinedValues:true,
              values : [ { id:"west" }, { id:"north" }, { id : "east" } ]
           }],
           data : { west:4, north:5, east:2 }
        })
    ```
    Note that the property "inlinedValues" must be set on the facet definition, and the set of facetValueIds must be specified outside of the data array (with the "standard model", facetValueIds can be automatically derived from the data).
    
    A two facet chart with an inlined facet can be defined as follows:
    
    ```
        isc.Chart.create({
           facets: [
             { 
                inlinedValues:true,
                values : [ { id:"west" }, { id:"north" }, { id : "east" } ]
             }, 
             { id:"product" }
           ],
           data : [
               { product:"cars", west:4, north:5, east:2 },
               { product:"trucks", west:1, north:9, east:3 }
           ]
        })
    ```
    

Comparing between the formats, the "standard model" format treats all facets identically, which can be of use when integrating with server technology that likewise treats all facets identically. The "inlined facet" format is a more compact data representation and allows easier conversion from data displayed in a ListGrid.

### See Also

- [DataSource](DataSource.md#class-datasource)

**Flags**: IWR

---
## Attr: FacetChart.showDoughnut

### Description
Whether to show a "doughnut hole" in the middle of pie charts. Defaults to whether chartType is set to "Doughnut" (shown) vs "Pie" (not shown) but can be forced on or off via `showDoughnut`.

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.minContentHeight

### Description
When [autoScrollContent](#attr-facetchartautoscrollcontent) is true, limits the minimum height of the chart-content, including data, labels, title and legends. If this widget is sized smaller than this height, scrollbars are introduced to reach the hidden content. See [minContentWidth](#attr-facetchartmincontentwidth) to affect the minimum horizontal content-size.

**Flags**: IRW

---
## Attr: FacetChart.matchBarChartDataLineColor

### Description
Setting to define whether the border around the bar chart area should be the same color as the main chart area.

**Flags**: IRW

---
## Attr: FacetChart.regressionLineType

### Description
Regression algorithm used for the [regression line](#attr-facetchartshowregressionline).

### Groups

- statistics

**Flags**: IRW

---
## Attr: FacetChart.pieLabelLineProperties

### Description
Properties for pie label line

### Groups

- pieChart

**Flags**: IRW

---
## Attr: FacetChart.otherAxisGradationTimes

### Description
For charts that have a date/time-valued X-axis, gradations can instead be specified as Strings, consisting of a number and trailing letter code, where the letter code indicates the unit of time. Valid time units are "ms" (millisecond), "s" (second), "mn" (minute), "h" (hour), "d" (day), "w" (week), "m" (month), "q" (quarter, 3-months), "y" (year).

When time units are used, there is no way to scale the same unit to a much larger or smaller range of time (as there is with numeric gradations). For example, a setting of "30mn" meaning "30 minutes" does not mean that 30 hours is a natural choice for chart with a longer timeline (days should obviously be chosen instead). Therefore, when specifying time gradations, candidate gradations must be provided for the entire possible displayed range. If insufficient gradations are specified, this can result in unreadable charts; for example, if the largest available gradation is "15mn" and the chart is showing a full week's data in around 500px, there will be more than one gradation per pixel, and labels will be drawn on top of each other.

To prevent this, be sure to specify enough gradations to cover the all time ranges your chart may need to display. However, if gradations are not specified for granularities under 1 second or over 1 year, further gradations will be chosen based on using [FacetChart.otherAxisGradationGaps](#attr-facetchartotheraxisgradationgaps) to choose fractions of seconds or multiples of years.

The default setting is effectively:

```
 ["1s", "15s", "30s", "1mn", "5mn", "15mn", "30mn", "1h", "1d", "1w", "1m", "1q", "1y"]
 
```

### Groups

- gradations

**Flags**: IRW

---
## Attr: FacetChart.gradationLabelPadding

### Description
Padding from edge of Y the Axis Label.

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.autoFetchTextMatchStyle

### Description
If [FacetChart.autoFetchData](#attr-facetchartautofetchdata) is `true`, this attribute allows the developer to specify a textMatchStyle for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

### Groups

- databinding

**Flags**: IR

---
## Attr: FacetChart.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: FacetChart.pieSliceProperties

### Description
Properties for pie slices

### Groups

- pieChart

**Flags**: IR

---
## Attr: FacetChart.dataGradients

### Description
A dictionary of gradients to use for a series of visual elements representing data (eg columns, bars, pie slices), any of which may be adjacent to any other.

**Flags**: IR

---
## Attr: FacetChart.yAxisLabelPadding

### Description
Padding between each swatch and label pair.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.pointSizeLogBase

### Description
When [FacetChart.logScalePointSize](#attr-facetchartlogscalepointsize) is true, base value for logarithmic point size metric values.

### Groups

- dataPoints

**Flags**: IR

---
## Attr: FacetChart.valueTitle

### Description
A label for the data values, such as "Sales in Thousands", typically used as the label for the value axis.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: FacetChart.chartRectProperties

### Description
Properties for chart rect. By default, [rounding](DrawRect.md#attr-drawrectrounding) of the chart rect. causes the gradation lines to be automatically inset from the edge so that they do not run right along the curve. Set [FacetChart.padChartRectByCornerRadius](#attr-facetchartpadchartrectbycornerradius) to `false` to change this default.

### Groups

- chartFeatures

**Flags**: IRW

---
## Attr: FacetChart.doughnutHoleProperties

### Description
Properties for doughnut hole

### Groups

- pieChart

**Flags**: IRW

---
## Attr: FacetChart.autoRotateLabels

### Description
Whether to automatically rotate labels if needed in order to make them legible and non-overlapping.

### Groups

- labelsAndTitles

**Deprecated**

**Flags**: IR

---
## Attr: FacetChart.showChartRect

### Description
Whether to show a rectangular shape around the area of the chart where data is plotted.

### Groups

- chartFeatures

**Flags**: IR

---
## Attr: FacetChart.zoomChart

### Description
Mini-chart created to allow zooming when [FacetChart.canZoom](#attr-facetchartcanzoom) is enabled.

This chart automatically has certain visual tweaks applied, including [FacetChart.showInlineLabels](#attr-facetchartshowinlinelabels), [muted colors](#attr-facetchartzoommutepercent) and [logarithmic scaling](#attr-facetchartzoomlogscale). It can be further configured via [FacetChart.zoomChartProperties](#attr-facetchartzoomchartproperties).

The selected range from this chart defaults to being shown with distinct styling as well (if [FacetChart.zoomShowSelection](#attr-facetchartzoomshowselection) is set), which can be controlled via [FacetChart.zoomSelectionChartProperties](#attr-facetchartzoomselectionchartproperties).

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.dataAxisLabelProperties

### Description
Properties for labels of data axis.

### Groups

- labelsAndTitles

**Flags**: IRW

---
## Attr: FacetChart.legendSwatchProperties

### Description
Properties for the swatches of color shown in the legend.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.chartType

### Description
See [ChartType](../main.md#type-charttype) for a list of known types - Column, Bar, Line, Pie, Doughnut, Area, Radar, and Histogram charts are supported.

### Groups

- chartType

**Flags**: IRW

---
## Attr: FacetChart.styleName

### Description
Default styleName for the chart.

**Flags**: IRW

---
## Attr: FacetChart.title

### Description
Title for the chart as a whole.

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.minContentWidth

### Description
When [autoScrollContent](#attr-facetchartautoscrollcontent) is true, limits the minimum width of the chart-content, including data, labels, titles and legends. If this widget is sized smaller than this width, scrollbars are introduced to reach the hidden content. See [minContentHeight](#attr-facetchartmincontentheight) to affect the minimum vertical content-size.

**Flags**: IRW

---
## Attr: FacetChart.legendBoundaryProperties

### Description
Properties for top boundary of the legend are, when there is already an outer container around the whole chart. see [FacetChart.drawLegendBoundary](#attr-facetchartdrawlegendboundary)

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.zoomChartProperties

### Description
Properties to further configure the [FacetChart.zoomChart](#attr-facetchartzoomchart).

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.showGradationsOverData

### Description
If set, gradation lines are drawn on top of data rather than underneath.

### Groups

- gradations

**Flags**: IR

---
## Attr: FacetChart.backgroundBandProperties

### Description
Properties for background band

**Flags**: IR

---
## Attr: FacetChart.proportionalAxisLabel

### Description
Default title for the value axis label when the chart is in [proportional rendering mode](#attr-facetchartproportional). This title will be used unless the [legend facet](#method-facetchartgetlegendfacet) defines a [proportionalTitle](Facet.md#attr-facetproportionaltitle).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FacetChart.showColorScaleLegend

### Description
Whether to show an additional legend underneath the chart to indicate color values. The default is `true` if a valid [colorScaleMetric](#attr-facetchartcolorscalemetric) is specified.

### Groups

- legend

### See Also

- [FacetChart.scaleStartColor](#attr-facetchartscalestartcolor)
- [FacetChart.scaleEndColor](#attr-facetchartscaleendcolor)

**Flags**: IR

---
## Attr: FacetChart.legendItemPadding

### Description
Padding between each swatch and label pair.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.centerTitle

### Description
Whether to place the [chart title](#attr-facetchartshowtitle) with respect to the full, scrollable width of the chart when [FacetChart.autoScrollData](#attr-facetchartautoscrolldata) is active. The default of false means that the title will be placed in the visible, non-overflowed region of the chart, for greater visibility.

Note that alignment of the title itself is governed by [titleAlign](#attr-facetcharttitlealign).

### Groups

- chartTitle

### See Also

- [FacetChart.title](#attr-facetcharttitle)
- [FacetChart.showTitle](#attr-facetchartshowtitle)
- [FacetChart.centerLegend](#attr-facetchartcenterlegend)
- [FacetChart.autoScrollData](#attr-facetchartautoscrolldata)

**Deprecated**

**Flags**: IR

---
## Attr: FacetChart.titleBackgroundProperties

### Description
Properties for title background (if being drawn).

### Groups

- chartTitle

**Flags**: IRW

---
## Attr: FacetChart.zoomLogScale

### Description
By default when [FacetChart.canZoom](#attr-facetchartcanzoom) is enabled, the [FacetChart.zoomChart](#attr-facetchartzoomchart) uses logarithmic scaling so that spikes in the data don't result in a zoomed chart that is mostly a flat line.

Logarithmic scaling is automatically disabled if the dataset spans zero (eg, has negative and positive values) as this can't be shown in a logarithmic scale.

Set `zoomLogScale` to explicitly enable or disable logarithmic scaling.

### Groups

- zoom

**Flags**: IR

---
## Attr: FacetChart.legendSwatchSize

### Description
Size of individual color swatches in legend.

### Groups

- legend

**Flags**: IR

---
## Attr: FacetChart.discontinuousLines

### Description
Whether to treat non-numeric values in the dataset as indicating a break in the data line. If set to `false` then null values are ignored. Defaults to `true` for [filled](#attr-facetchartfilled) charts and to `false` for line charts.

**Flags**: IRW

---
## Attr: FacetChart.bubbleProperties

### Description
Properties for the shapes displayed around the data points (for example, in a bubble chart).

When either the [pointSizeMetric](#attr-facetchartpointsizemetric) or the [colorScaleMetric](#attr-facetchartcolorscalemetric) is active the default `bubbleProperties` displays each data points with a linear gradient.

### Groups

- appearance

**Flags**: IR

---
## Attr: FacetChart.yAxisMetric

### Description
For scatter charts only, the "id" of the metric facet value to use for the y-axis.

The default y-axis metric is the first value of the metric facet.

**Flags**: IR

---
## Attr: FacetChart.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [FacetChart.initialCriteria](#attr-facetchartinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle). Additional request properties may be specified using [FacetChart.fetchRequestProperties](#attr-facetchartfetchrequestproperties).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_2.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [FacetChart.initialCriteria](#attr-facetchartinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_2.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: FacetChart.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: FacetChart.useAutoGradients

### Description
Causes the chart to use the colors specified in [FacetChart.dataColors](#attr-facetchartdatacolors) but specify chart-specific gradients based on the primary data color per chart type.

**Flags**: IR

---
## Attr: FacetChart.usePointSizeLogGradations

### Description
Whether to use classic logarithmic gradations, where each order of magnitude is shown as a gradation as well as a few intervening values, for the [pointSizeMetric](#attr-facetchartpointsizemetric) values displayed in the [point size legend](#attr-facetchartshowpointsizelegend). Gradations also begin and end on an order of magnitude. For example, 1, 2, 4, 6, 8, 10, 20, 40, 60, 80, 100.

Default gradations can be overridden via [FacetChart.pointSizeLogBase](#attr-facetchartpointsizelogbase) and [FacetChart.pointSizeLogGradations](#attr-facetchartpointsizeloggradations).

### Groups

- gradations

### See Also

- [FacetChart.useLogGradations](#attr-facetchartuseloggradations)

**Flags**: IR

---
## Attr: FacetChart.errorBarColorMutePercent

### Description
This property helps specify the color of the error bars and its value must be a number between -100 and 100. Error bars have the same color as the data line, but the colors are actually "muted" by this percentage by shifting them toward white (or for negative numbers, toward black). The default is to darken the data colors by 60% to get the error bar colors.

**Flags**: IR

---
## Attr: FacetChart.minChartWidth

### Description
Minimum width for this chart instance.

**Flags**: IR

---
## Attr: FacetChart.showMinorTicks

### Description
If [ticks](#attr-facetchartshowyticks) are being shown, controls whether a distinction is made between major and minor tick marks.

If minor ticks are used, by default, major ticks are used for powers of 10 and minor ticks are used for other gradations. See [FacetChart.majorTickGradations](#attr-facetchartmajortickgradations) for control over which ticks are rendered as major vs minor ticks.

### Groups

- ticks

**Flags**: IRW

---
## Attr: FacetChart.bandedStandardDeviations

### Description
Whether to show color bands between the [standard deviation](#attr-facetchartstandarddeviations) lines.

Standard deviation bands are not available for pie or radar charts.

### Groups

- statistics

### See Also

- [FacetChart.standardDeviationBandProperties](#attr-facetchartstandarddeviationbandproperties)

**Flags**: IR

---
## Method: FacetChart.getDataLineWidth

### Description
Specifies the width to use for data lines in the chart. No default implementation. If not defined or null is returned, the line width will be set by the appropriate chart properties, such as [FacetChart.dataLineProperties](#attr-facetchartdatalineproperties), [FacetChart.barProperties](#attr-facetchartbarproperties), or [FacetChart.bubbleProperties](#attr-facetchartbubbleproperties).

Note that this method is simply an override point, since it has no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to target |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to target |
| purpose | [String](#type-string) | false | — | purpose for the requested width - such as "legend", "line", "area", "points", etc. |

### Returns

`[int](../main.md#type-int)` — width to use for data lines or null to use [ChartType](../main.md#type-charttype) default

### See Also

- [DrawItem.lineWidth](DrawItem.md#attr-drawitemlinewidth)
- [FacetChart.getDataLineColor](#method-facetchartgetdatalinecolor)

---
## Method: FacetChart.setDataColors

### Description
Setter for [FacetChart.dataColors](#attr-facetchartdatacolors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataColors | [Array of CSSColor](#type-array-of-csscolor) | false | — | New set of data colors |

---
## Method: FacetChart.getMinChartHeight

### Description
Returns the [minimum height](#attr-facetchartminchartheight) for the chart body.

---
## Method: FacetChart.getMinContentWidth

### Description
Returns the [FacetChart.minContentWidth](#attr-facetchartmincontentwidth) for this facet chart when [FacetChart.autoScrollContent](#attr-facetchartautoscrollcontent) is enabled.

### Returns

`[int](../main.md#type-int)` — Min content width

---
## Method: FacetChart.getChartWidth

### Description
Get the width of the central chart area, where data elements appear.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recalc | [boolean](../main.md#type-boolean) | false | — | if false then cached value will be returned, otherwise will be recalculated. |

### Returns

`[float](../main.md#type-float)` — the width of the central chart area.

---
## Method: FacetChart.getMax

### Description
Calculate the maximum of the data from a single metric.

The first argument, criteria, determines which metric is used to calculate the maximum. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |

### Returns

`[Float](../main.md#type-float)` — the maximum of the data values

---
## Method: FacetChart.zoomTo

### Description
For a [zoomed chart](#attr-facetchartcanzoom), simultaneously sets the [zoomStartValue](#method-facetchartsetzoomstartvalue) and [zoomEndValue](#method-facetchartsetzoomendvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startValue | [Any](#type-any) | false | — | starting value for the data range shown in the main chart |
| endValue | [Any](#type-any) | false | — | ending value for the data range shown in the main chart |

### Groups

- zoom

---
## Method: FacetChart.getMean

### Description
Calculate the mean, or expected value, of the data over a single metric. See [http://en.wikipedia.org/wiki/Expected\_value](http://en.wikipedia.org/wiki/Expected_value).

The first argument, criteria, determines which metric is used to calculate the mean. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |

### Returns

`[Float](../main.md#type-float)` — the mean of the data values

---
## Method: FacetChart.getPercentile

### Description
Calculate a percentile of the data over a single metric. See [http://en.wikipedia.org/wiki/Percentile](http://en.wikipedia.org/wiki/Percentile).

The first argument, criteria, determines which metric is used to calculate a percentile. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

The second argument is the percentile to calculate and it must be a number from 0 to 100.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |
| percentile | [float](../main.md#type-float) | false | — | the percentile to calculate |

### Returns

`[Float](../main.md#type-float)` — a percentile of the data values

---
## Method: FacetChart.setOtherAxisGradationTimes

### Description
Setter for [FacetChart.otherAxisGradationTimes](#attr-facetchartotheraxisgradationtimes).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| otherAxisGradationTimes | [Array of String](#type-array-of-string) | false | — | new [FacetChart.otherAxisGradationTimes](#attr-facetchartotheraxisgradationtimes) value |

### Groups

- gradations

---
## Method: FacetChart.getDataGradient

### Description
Get a gradient from the [FacetChart.dataGradients](#attr-facetchartdatagradients) Array.

Override to provide a dynamic gradient generation scheme.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to be colored |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to be colored |
| purpose | [String](#type-string) | false | — | purpose for the requested gradient - such as "legend", "line", "area", "points", etc. |

### Returns

`[String](#type-string)` — the gradient identifier

---
## Method: FacetChart.zoomChanged

### Description
Fires when the end user changes the zoom position in a [zoomed chart](#attr-facetchartcanzoom).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startValue | [Any](#type-any) | false | — | starting value for the data range shown in the main chart |
| endValue | [Any](#type-any) | false | — | ending value for the data range shown in the main chart |

### Groups

- zoom

---
## Method: FacetChart.setData

### Description
Provides a new data set to the chart after it has been created or drawn. The FacetChart will redraw to show the new data automatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [List of CellRecord](#type-list-of-cellrecord) | false | — | data to show in the chart |

### Groups

- data

---
## Method: FacetChart.getLegendFacet

### Description
Returns the [Facet](Facet.md#class-facet) in the list of [facets](#attr-facetchartfacets) whose [values](Facet.md#attr-facetvalues) are rendered in the chart's legend.

Most single-facet charts do not have a legend facet. The exceptions are that single-facet Pie/Doughnut charts have a legend facet as the first facet and Bubble and Scatter charts may optionally have a legend facet as the second facet, after the metric facet.

In all multi-facet charts, the legend facet is the second facet.

Note that the user may swap the legend facet and the [data label facet](#method-facetchartgetdatalabelfacet) in most chart types using the context menu.

### Returns

`[Facet](#type-facet)` — the legend facet, or `null` if there is no such facet

### Groups

- legend

### See Also

- [FacetChart.facets](#attr-facetchartfacets)

---
## Method: FacetChart.formatDataValue

### Description
Return the text string to display in labels [in the chart-body or in hovers](#attr-facetchartshowdatavaluesmode) given the raw value for the metric displayed on the value axis.

This method may also be passed the [context](../main.md#type-formattingcontext) for which the value is being formatted, the record associated with the value and the id of its [facet](#attr-facetchartfacets).

Note that the rendering of values for gradation labels is handled by [FacetChart.formatAxisValue](#method-facetchartformataxisvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value of the metric |
| context | [FormattingContext](../main.md#type-formattingcontext) | true | — | context in which the value is being displayed |
| record | [Record](#type-record) | true | — | cell record for the data value |
| facetId | [String](#type-string) | true | — | facet ID for the data value |

### Returns

`[String](#type-string)` — the text to display.

### Groups

- display_values

---
## Method: FacetChart.getPolynomialRegressionFunction

### Description
For scatter plots only, get a Function from the specified independent variable X to the specified dependent variable Y that defines the polynomial that best fits the data. See [http://en.wikipedia.org/wiki/Polynomial\_regression](http://en.wikipedia.org/wiki/Polynomial_regression).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degree | [Integer](../main_2.md#type-integer) | true | — | the degree of the polynomial. Defaults to [FacetChart.regressionPolynomialDegree](#attr-facetchartregressionpolynomialdegree). |
| xMetric | [String](#type-string) | true | — | ID of an inlined facet value to use as the independent variable. Defaults to the [x-axis metric](#attr-facetchartxaxismetric). |
| yMetric | [String](#type-string) | true | — | ID of an inlined facet value to use as the dependent variable. Defaults to the [y-axis metric](#attr-facetchartyaxismetric). |

---
## Method: FacetChart.getDataLabelHoverHTML

### Description
Called when the mouse hovers over a data label, that is, a text label showing values from the first facet. For example, the labels underneath the X-axis of a column chart, labelling each column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValue | [FacetValue](#type-facetvalue) | false | — | facetValue that was hovered |

### Returns

`[HTMLString](../main.md#type-htmlstring)` — hover text to be shown. Return null to avoid a hover being shown

---
## Method: FacetChart.setOtherAxisPixelsPerGradation

### Description
Setter for [FacetChart.otherAxisPixelsPerGradation](#attr-facetchartotheraxispixelspergradation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pixelsPerGradation | [int](../main.md#type-int) | false | — | new [FacetChart.otherAxisPixelsPerGradation](#attr-facetchartotheraxispixelspergradation) value |

### Groups

- gradations

---
## Method: FacetChart.getMin

### Description
Calculate the minimum of the data from a single metric.

The first argument, criteria, determines which metric is used to calculate the minimum. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |

### Returns

`[Float](../main.md#type-float)` — the minimum of the data values

---
## Method: FacetChart.setTickLength

### Description
Setter for [FacetChart.tickLength](#attr-facetchartticklength).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tickLength | [int](../main.md#type-int) | false | — | new [FacetChart.tickLength](#attr-facetchartticklength) value |

### Groups

- ticks

---
## Method: FacetChart.getDrawnValue

### Description
Returns rendering information for the data value specified by the passed facet values.

If called before [FacetChart.chartDrawn](#method-facetchartchartdrawn), logs a warning and returns null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facet values of desired data value |

### Returns

`[DrawnValue](#type-drawnvalue)` — the drawn value, or null for invalid arguments / incorrect timing of call

---
## Method: FacetChart.formatSegmentLabel

### Description
Defines the format of the label for a segment in a histogram chart. By default, it simply returns a label of the form "Y1 to Y2" describing the start and end values, applying [FacetChart.formatDataValue](#method-facetchartformatdatavalue) to format the values.

Note that this method has no impact on the facet value labels appearing on the horizontal axis of the histogram chart.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startValue | [Any](#type-any) | false | — | raw start value of the segment |
| endValue | [Any](#type-any) | false | — | raw end value of the segment |

### Returns

`[String](#type-string)` — the text to display.

### Groups

- display_values
- histogramChart

---
## Method: FacetChart.getVariance

### Description
Calculate the variance of the data from a single metric. See [http://en.wikipedia.org/wiki/Variance](http://en.wikipedia.org/wiki/Variance).

The first argument, criteria, determines which metric is used to calculate the variance. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |
| population | [boolean](../main.md#type-boolean) | false | — | false to calculate a sample variance, true to calculate a population variance |

### Returns

`[Float](../main.md#type-float)` — the variance of the data values

---
## Method: FacetChart.fetchRelatedData

### Description
Based on the relationship between the DataSource this component is bound to and the DataSource specified as the "schema" argument, call fetchData() to retrieve records in this grid that are related to the passed-in record.

Relationships between DataSources are declared via [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey).

For example, given two related DataSources "orders" and "orderItems", where we want to fetch the "orderItems" that belong to a given "order". "orderItems" should declare a field that is a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) to the "orders" table (for example, it might be named "orderId" with foreignKey="orders.id"). Then, to load the records related to a given "order", call fetchRelatedData() on the component bound to "orderItems", pass the "orders" DataSource as the "schema" and pass a record from the "orders" DataSource as the "record" argument.

Note that multiple foreign keys into the schema are supported by this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | DataSource record |
| schema | [Canvas](#type-canvas)|[DataSource](#type-datasource)|[ID](#type-id) | false | — | schema of the DataSource record, or DataBoundComponent already bound to that schema |
| callback | [DSCallback](../main_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: FacetChart.setAutoScrollData

### Description
Sets [FacetChart.autoScrollData](#attr-facetchartautoscrolldata) and updates the chart.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoScrollData | [boolean](../main.md#type-boolean) | false | — | whether chart should automatically expand and show scrollbars to accommodate content. |

---
## Method: FacetChart.getNearestDrawnValues

### Description
Returns an array of [DrawnValue](../main_2.md#object-drawnvalue) objects containing rendering information for the data values having each metric that are shown nearest to the passed coordinates.

Passed X and Y coordinates should be relative to the FacetChart. If neither an X or Y coordinate is passed, both X and Y will use the current [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx) and [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety).

The behavior for different chart types is the same as [FacetChart.getNearestDrawnValue](#method-facetchartgetnearestdrawnvalue). This method also logs a warning and returns null if called before [FacetChart.chartDrawn](#method-facetchartchartdrawn).

To get the nearest DrawnValues only if they contain the given coordinates, you can either use the [FacetChart.getDrawnValuesAtPoint](#method-facetchartgetdrawnvaluesatpoint) API or check whether each DrawnValue in the returned array contains the point by calling [FacetChart.drawnValueContainsPoint](#method-facetchartdrawnvaluecontainspoint).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | true | — | X coordinate. If this parameter is specified, then `y` is a required parameter. |
| y | [Integer](../main_2.md#type-integer) | true | — | Y coordinate |

### Returns

`[Array of DrawnValue](#type-array-of-drawnvalue)` — the nearest drawn values for each metric, or null for invalid arguments / incorrect timing of call

### See Also

- [FacetChart.getDrawnValuesAtPoint](#method-facetchartgetdrawnvaluesatpoint)

---
## Method: FacetChart.getChartLeft

### Description
Get the left margin of the central chart area, where data elements appear.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Returns

`[float](../main.md#type-float)` — left margin of the central chart area

---
## Method: FacetChart.getFacetValue

### Description
Get facet value definition by facetId and facetValueId.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | the id of the facet to retrieve |
| facetValueId | [String](#type-string) | false | — | the id of the facet value to retrieve |

### Returns

`[FacetValue](#type-facetvalue)` — the FacetValue if found, or null

### See Also

- [FacetValue](../main.md#object-facetvalue)

---
## Method: FacetChart.setZIndexMetric

### Description
Method to change the current [FacetChart.zIndexMetric](#attr-facetchartzindexmetric) - see property for more details. Will redraw the chart if drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zIndexMetric | [String](#type-string) | false | — | name of zIndex metric |

### Groups

- histogramChart

---
## Method: FacetChart.setAutoScrollContent

### Description
Sets [FacetChart.autoScrollContent](#attr-facetchartautoscrollcontent) and updates the chart.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoScrollContent | [boolean](../main.md#type-boolean) | false | — | whether the chart should automatically show scrollbars when it's size is smaller than the minimum content [width](#attr-facetchartmincontentwidth) or [height](#attr-facetchartmincontentheight). |

---
## Method: FacetChart.setPixelsPerGradation

### Description
Setter for [FacetChart.pixelsPerGradation](#attr-facetchartpixelspergradation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pixelsPerGradation | [int](../main.md#type-int) | false | — | new [FacetChart.pixelsPerGradation](#attr-facetchartpixelspergradation) value |

### Groups

- gradations

---
## Method: FacetChart.getMinChartWidth

### Description
Returns the [minimum width](#attr-facetchartminchartwidth) for the chart body.

---
## Method: FacetChart.getChartHeight

### Description
Get the height the central chart area, where data elements appear.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recalc | [boolean](../main.md#type-boolean) | false | — | if false then cached value will be returned, otherwise will be recalculated. |

### Returns

`[float](../main.md#type-float)` — the width of the central chart area.

---
## Method: FacetChart.setShowYTicks

### Description
Setter for [FacetChart.showYTicks](#attr-facetchartshowyticks).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showTicks | [boolean](../main.md#type-boolean) | false | — | new [FacetChart.showYTicks](#attr-facetchartshowyticks) value |

### Groups

- ticks

---
## Method: FacetChart.getSimpleLinearRegressionFunction

### Description
For scatter plots only, get a Function from the specified independent variable X to the specified dependent variable Y that defines the line that best fits the data. See [http://en.wikipedia.org/wiki/Simple\_linear\_regression](http://en.wikipedia.org/wiki/Simple_linear_regression).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| xMetric | [String](#type-string) | true | — | ID of an inlined facet value to use as the independent variable. Defaults to the [x-axis metric](#attr-facetchartxaxismetric). |
| yMetric | [String](#type-string) | true | — | ID of an inlined facet value to use as the dependent variable. Defaults to the [y-axis metric](#attr-facetchartyaxismetric). |

---
## Method: FacetChart.getNearestDrawnValue

### Description
Returns rendering information for the data value that is shown nearest to the passed coordinates, as a [DrawnValue](../main_2.md#object-drawnvalue) object.

Passed X and Y coordinates should be relative to the FacetChart. If neither an X or Y coordinate is passed, both X and Y will use the current [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx) and [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety).

If called before [FacetChart.chartDrawn](#method-facetchartchartdrawn), logs a warning and returns null. For a chart with multiple vertical axes, returns the nearest point from the first metric only (see [FacetChart overview](#class-facetchart)). For scatter charts, returns a DrawnValue where the [value](DrawnValue.md#attr-drawnvaluevalue) is from the [y-axis metric](#attr-facetchartyaxismetric).

To get the nearest DrawnValue only if it contains the given coordinates, you can either use the [FacetChart.getDrawnValueAtPoint](#method-facetchartgetdrawnvalueatpoint) API or call [FacetChart.drawnValueContainsPoint](#method-facetchartdrawnvaluecontainspoint) on the return value.

Behavior for different chart types is as follows:

#### Bar / Column

Returns the centerpoint of the end of the nearest bar or column by considering the Y coordinate (bar) or X coordinate (column) only.

#### Line / Area

Returns the nearest point based on which data label is nearest to the passed X coordinate. For multi-series charts, if Y coordinate is not passed the data point returned is from the series that has the highest value at the data label.

#### Radar

Returns the data point nearest the passed coordinates by straight line distance. Passing only one coordinate will cause a warning to be logged and null to be returned; passing neither coordinate is allowed (`getOffsetX/Y` will be used).

#### Pie

Returns the data point for the segment that would be hit if a line were drawn from the passed coordinates to the center of the pie.

If there are multiple stacked pies, uses the pie that contains the passed coordinates, otherwise the outermost pie.

If there are multiple non-stacked pies, uses the pie that is nearest the passed coordinates by straight-line distance to the center of the pie.

Passing only one coordinate will cause a warning to be logged and null to be returned; passing neither coordinate is allowed (`getOffsetX/Y` will be used).

If the chart is a [multi-axis chart](#attr-facetchartextraaxismetrics) then this method takes an optional parameter, `metric`, which causes this method to return a `DrawnValue` from the specified metric. If a metric is not passed then the first metric of the metric facet will be used (or just the [FacetChart.valueProperty](#attr-facetchartvalueproperty) if there is no metric facet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | true | — | X coordinate. If this parameter is specified, then `y` is a required parameter. |
| y | [Integer](../main_2.md#type-integer) | true | — | Y coordinate |
| metric | [String](#type-string) | true | — | metric over which to determine the drawn value |

### Returns

`[DrawnValue](#type-drawnvalue)` — the nearest drawn value, or null for invalid arguments / incorrect timing of call

---
## Method: FacetChart.setZoomEndValue

### Description
Setter for [FacetChart.zoomEndValue](#attr-facetchartzoomendvalue).

Note that the [FacetChart.zoomStartValue](#attr-facetchartzoomstartvalue) and [FacetChart.zoomEndValue](#attr-facetchartzoomendvalue) may be set simultaneously using [FacetChart.zoomTo](#method-facetchartzoomto).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zoomEndValue | [Any](#type-any) | false | — | New end value for the data range shown in the main chart |

### Groups

- zoom

---
## Method: FacetChart.getDrawnValues

### Description
Returns rendering information for the data values specified by the passed facet values.

If called before [FacetChart.chartDrawn](#method-facetchartchartdrawn), logs a warning and returns null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | true | — | facet values of desired DrawnValues. If no FacetValueMap is provided, then all DrawnValues are returned. |

### Returns

`[Array of DrawnValue](#type-array-of-drawnvalue)` — the DrawnValues, or null for invalid arguments / incorrect timing of call

---
## Method: FacetChart.getPrintHTML

### Description
Retrieves printable HTML for this component and all printable subcomponents.

By default any Canvas with children will simply collect the printable HTML of its children by calling getPrintHTML() on each child that is considered [printable](Canvas.md#attr-canvasshouldprint).

If overriding this method for a custom component, you should **either** return a String of printable HTML string directly **or** return null, and fire the callback (if provided) using [Class.fireCallback](Class.md#method-classfirecallback).

To return an empty print representation, return an empty string ("") rather than null.

The `printProperties` argument, if passed, must be passed to any subcomponents on which `getPrintHTML()` is called.

**Notes on printing**

To print a `FacetChart` for export on IE8 and earlier, it is important to pass [PrintProperties](../main_2.md#object-printproperties) with [printForExport](PrintProperties.md#attr-printpropertiesprintforexport):true:

```
var exportHTML = chart.getPrintHTML({ printForExport:true });
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| printProperties | [PrintProperties](#type-printproperties) | true | — | properties to configure printing behavior - may be null. |
| callback | [Callback](../main.md#type-callback) | true | — | optional callback. This is required to handle cases where HTML generation is asynchronous - if a method generates HTML asynchronously, it should return null, and fire the specified callback on completion of HTML generation. The first parameter `HTML` should contain the generated print HTML. The callback is only called if null is returned. Furthermore, the default getPrintHTML() implementation always returns null and fires the callback when a callback is provided. |

### Returns

`[HTMLString](../main.md#type-htmlstring)` — null if the print HTML is being generated asynchronously and/or a callback is provided; otherwise, the direct print HTML for this component (but note that returning direct print HTML is a deprecated feature).

### Groups

- printing

**Flags**: A

---
## Method: FacetChart.legendHover

### Description
Fires when the mouse hovers over a color swatch or its label in the legend area of the chart.

The [FacetValue](../main.md#object-facetvalue) that the user is hovering over is provided. If the chart is a [multi-axis chart](#attr-facetchartextraaxismetrics), the [FacetValue](../main.md#object-facetvalue) for the hovered-over metric will also be provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValue | [FacetValue](#type-facetvalue) | false | — | facetValue that the mouse is over |
| metricFacetValue | [FacetValue](#type-facetvalue) | false | — | for a multi-axis chart, facetValue representing the hovered-over metric. Null if chart is not multi-axis |

### Groups

- legend

---
## Method: FacetChart.setProportional

### Description
Setter for [FacetChart.proportional](#attr-facetchartproportional).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| proportional | [boolean](../main.md#type-boolean) | false | — | Whether the chart should now use proportional mode. |

---
## Method: FacetChart.getFacet

### Description
Get a facet definition by facetId.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | the id of the facet to retrieve |

### Returns

`[Facet](#type-facet)` — the Facet if found, or null

### See Also

- [Facet](Facet.md#class-facet)

---
## Method: FacetChart.setScaleStartColor

### Description
Setter for [FacetChart.scaleStartColor](#attr-facetchartscalestartcolor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| scaleStartColor | [CSSColor](../main_2.md#type-csscolor) | false | — | The new start color for the color scale. |

### Groups

- dataPoints

---
## Method: FacetChart.getChartTop

### Description
Get the top coordinate of the central chart area, where data elements appear.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Returns

`[float](../main.md#type-float)` — The top coordinate of the central chart area

---
## Method: FacetChart.setShowMinorTicks

### Description
Setter for [FacetChart.showMinorTicks](#attr-facetchartshowminorticks).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showMinorTicks | [boolean](../main.md#type-boolean) | false | — | new [FacetChart.showMinorTicks](#attr-facetchartshowminorticks) value |

### Groups

- ticks

---
## Method: FacetChart.getXCoord

### Description
Returns the X coordinate where the passed data value either was or would be drawn. For example, this would be the X coordinate where a bar would end in a bar chart.

This is only allowed to be called after [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

If the [chartType](#attr-facetchartcharttype) is "Bar", "Bubble", or "Scatter" then the `value` argument should be a number. For other rectangular charts, this method expects a [FacetValueMap](../main.md#object-facetvaluemap) that uniquely identifies the data cell whose X-axis coordinate is to be retrieved.

Note that when [canZoom](#attr-facetchartcanzoom) is enabled, this API is valid only for data values between [zoomStartValue](#attr-facetchartzoomstartvalue) and [zoomEndValue](#attr-facetchartzoomendvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../main.md#type-float)|[FacetValueMap](#type-facetvaluemap) | false | — | the value to be drawn. |

### Returns

`[Float](../main.md#type-float)` — the X coordinate where the passed data value would be drawn; or null if the passed `FacetValueMap` does not identify a currently-drawn data cell.

---
## Method: FacetChart.setShowXTicks

### Description
Setter for [FacetChart.showXTicks](#attr-facetchartshowxticks).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showTicks | [boolean](../main.md#type-boolean) | false | — | new [FacetChart.showXTicks](#attr-facetchartshowxticks) value |

### Groups

- ticks

---
## Method: FacetChart.getDrawnValuesAtPoint

### Description
Returns an array of [DrawnValue](../main_2.md#object-drawnvalue) objects for the data values of each metric that are shown nearest to the passed coordinates, but only if they're under the given coordinates, or under the current mouse event coordinates if no coordinates are passed. This method is similar to [FacetChart.getNearestDrawnValues](#method-facetchartgetnearestdrawnvalues), but DrawnValues are only included in the returned array if they're under the coordinates.

See [FacetChart.drawnValueContainsPoint](#method-facetchartdrawnvaluecontainspoint) for the criteria that determine whether a DrawnValue is under (contains) the coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | true | — | X coordinate. If this parameter is specified, then `y` is a required parameter. |
| y | [Integer](../main_2.md#type-integer) | true | — | Y coordinate |

### Returns

`[Array of DrawnValue](#type-array-of-drawnvalue)` — the nearest DrawnValues that are under the given coordinates (or current mouse event coordinates), or null for invalid arguments / incorrect timing of call.

---
## Method: FacetChart.setScaleEndColor

### Description
Setter for [FacetChart.scaleEndColor](#attr-facetchartscaleendcolor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| scaleEndColor | [CSSColor](../main_2.md#type-csscolor) | false | — | The new end color for the color scale. |

### Groups

- dataPoints

---
## Method: FacetChart.legendClick

### Description
Fires when the user clicks on the legend area of the chart.

If the user specifically clicks on a color swatch or it's label, the [FacetValue](../main.md#object-facetvalue) clicked on will be provided.

If the chart is a [multi-axis chart](#attr-facetchartextraaxismetrics), the [FacetValue](../main.md#object-facetvalue) for the clicked-on metric will also be provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValue | [FacetValue](#type-facetvalue) | false | — | facetValue that was clicked, or null if click was in empty space |
| metricFacetValue | [FacetValue](#type-facetvalue) | false | — | for a multi-axis chart, facetValue representing the clicked metric. Null if click is in empty space or chart is not multi-axis |

### Groups

- legend

---
## Method: FacetChart.getDataLineColor

### Description
Specifies the color to use for data lines in the chart. No default implementation. If not defined or null is returned, the Framework will default to value of [FacetChart.getDataColor](#method-facetchartgetdatacolor).

Note that this method is simply an override point, since it has no default implementation - must return a color in the format of of a leading hash (#) plus 6 hexadecimal digits as specified for [FacetChart.dataColors](#attr-facetchartdatacolors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to be colored |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to be colored |
| purpose | [String](#type-string) | false | — | purpose for the requested color - such as "legend", "line", "area", "points", etc. |

### Returns

`[CSSColor](../main_2.md#type-csscolor)` — color to use for data lines or null to default to [FacetChart.getDataColor](#method-facetchartgetdatacolor)

### See Also

- [FacetChart.getDataColor](#method-facetchartgetdatacolor)
- [FacetChart.getDataLineWidth](#method-facetchartgetdatalinewidth)

---
## Method: FacetChart.getMinContentHeight

### Description
Returns the [FacetChart.minContentHeight](#attr-facetchartmincontentheight) for this facet chart when [FacetChart.autoScrollContent](#attr-facetchartautoscrollcontent) is enabled.

### Returns

`[int](../main.md#type-int)` — Min content height

---
## Method: FacetChart.setMinorTickLength

### Description
Setter for [FacetChart.minorTickLength](#attr-facetchartminorticklength).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| minorTickLength | [int](../main.md#type-int) | false | — | new [FacetChart.minorTickLength](#attr-facetchartminorticklength) value |

### Groups

- ticks

---
## Method: FacetChart.dataLabelClick

### Description
Fires when the user clicks on a data label, that is, a text label showing values from the first facet. For example, the labels underneath the X-axis of a column chart, labelling each column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValue | [FacetValue](#type-facetvalue) | false | — | facetValue that was clicked, or null if click was in empty space |
| facetValueId | [Any](#type-any) | false | — | id of the facetValue that was clicked. This is provided for convenience as it is already available in facetValue. |

---
## Method: FacetChart.getChartCenter

### Description
Returns the centerpoint for radar charts and pie charts.

Note that unstacked pie charts draw multiple pies, each with their own centers.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Returns

`[Point](#type-point)` — the centerpoint for radar charts and pie charts.

---
## Method: FacetChart.setAutoScrollDataApproach

### Description
Sets [AutoScrollDataApproach](../main.md#type-autoscrolldataapproach) and updates the chart.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoScrollDataApproach | [AutoScrollDataApproach](../main.md#type-autoscrolldataapproach) | false | — | what should drive horizontal expansion of the chart? |

---
## Method: FacetChart.getChartRadius

### Description
Returns the radius for radar charts and pie charts. For stacked pie charts this is radius of the outermost pie.

Note that unstacked pie charts draw multiple pies, each with their own radii.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Returns

`[float](../main.md#type-float)` — the radius for radar charts and pie charts.

---
## Method: FacetChart.setMajorTickGradations

### Description
Setter for [FacetChart.majorTickGradations](#attr-facetchartmajortickgradations).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| majorTickGradations | [Array of Float](#type-array-of-float) | false | — | new [FacetChart.majorTickGradations](#attr-facetchartmajortickgradations) value |

### Groups

- ticks

---
## Method: FacetChart.setMajorTickTimeIntervals

### Description
Setter for [FacetChart.majorTickTimeIntervals](#attr-facetchartmajorticktimeintervals).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| majorTickTimeIntervals | [Array of String](#type-array-of-string) | false | — | new [FacetChart.majorTickTimeIntervals](#attr-facetchartmajorticktimeintervals) value |

### Groups

- ticks

---
## Method: FacetChart.dataLabelHover

### Description
Fires when the mouse hovers over a data label, that is, a text label showing values from the first facet. For example, the labels underneath the X-axis of a column chart, labelling each column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValue | [FacetValue](#type-facetvalue) | false | — | facetValue that was hovered |

### Groups

- appearance

---
## Method: FacetChart.setUseMultiplePointShapes

### Description
Setter for [FacetChart.useMultiplePointShapes](#attr-facetchartusemultiplepointshapes).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| useMultiplePointShapes | [boolean](../main.md#type-boolean) | false | — | Whether the chart should now use multiple shapes to show data points. |

### Groups

- dataPoints

---
## Method: FacetChart.setDataLineType

### Description
Method to change the current [dataLineType](../main.md#type-charttype). Will redraw the chart if drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataLineType | [DataLineType](../main_2.md#type-datalinetype) | false | — | ow to draw lines between adjacent data points in Line and Scatter charts |

---
## Method: FacetChart.formatFacetValueId

### Description
Return the text string to display for facet value labels that appear in chart legends or as labels for [FacetChart.chartType](#attr-facetchartcharttype)s that have circumference or non-axis labels, such as for example "Pie" or "Radar" charts.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value of the metric |
| facet | [Facet](#type-facet) | false | — | facet containing the value |

### Returns

`[String](#type-string)` — the text to display.

### See Also

- [FacetChart.formatAxisValue](#method-facetchartformataxisvalue)
- [FacetChart.formatStringFacetValueIds](#attr-facetchartformatstringfacetvalueids)

---
## Method: FacetChart.pointClick

### Description
When [FacetChart.showDataPoints](#attr-facetchartshowdatapoints) is true, fires when a point is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../main.md#type-float) | false | — | the value at the point |
| record | [Record](#type-record) | false | — | the record at the point |
| metricId | [String](#type-string) | false | — | the ID of the metric at the point |

---
## Method: FacetChart.setStacked

### Description
Method to change [stacked](#attr-facetchartstacked). Use null to apply a default value for the current [chartType](../main.md#type-charttype).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stacked | [Boolean](#type-boolean) | false | — | new value |

### Groups

- chartType

---
## Method: FacetChart.setGradationGaps

### Description
Setter for [FacetChart.gradationGaps](#attr-facetchartgradationgaps).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradationGaps | [Array of Float](#type-array-of-float) | false | — | new [FacetChart.gradationGaps](#attr-facetchartgradationgaps) value |

### Groups

- gradations

---
## Method: FacetChart.chartDrawn

### Description
Called when all elements of the chart (data lines / shapes, gradations, legend, labels etc) have completed drawing.

See [FacetChart.chartBackgroundDrawn](#method-facetchartchartbackgrounddrawn) for usage information.

---
## Method: FacetChart.formatAxisValue

### Description
Return the text string to display along the axes for [gradation labels](#attr-facetchartgradationlabelproperties) or facet value labels given the raw metric value or facet value id.

Note that this formatter will be called for the gradation labels on an axis, including those generated for [LabelCollapseMode](../main.md#type-labelcollapsemode) "numeric". It also will be called for each facet value along the linear axes of a chart (vertical or horizontal) when [LabelCollapseMode](../main.md#type-labelcollapsemode) is _not_ active, unless a [FacetValue.title](FacetValue.md#attr-facetvaluetitle) has been specified (in [Facet.values](Facet.md#attr-facetvalues)) or the raw value is a string and [FacetChart.formatStringFacetValueIds](#attr-facetchartformatstringfacetvalueids) is false.

Note that the rendering of values in hovers or via [FacetChart.showDataValues](#attr-facetchartshowdatavalues) is handled by [FacetChart.formatDataValue](#method-facetchartformatdatavalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value of the metric or facet value id |
| forHorizontalAxis | [boolean](../main.md#type-boolean) | false | — | whether the raw value is for the horizontal/x-axis (true) or for the vertical/y-axis (false) |

### Returns

`[String](#type-string)` — the text to display.

### Groups

- display_values

### See Also

- [FacetChart.formatFacetValueId](#method-facetchartformatfacetvalueid)
- [MetricSettings.formatAxisValue](MetricSettings.md#method-metricsettingsformataxisvalue)

---
## Method: FacetChart.valueClick

### Description
Fires when a data value is clicked, and provides information about the data value that was clicked as a [DrawnValue](../main_2.md#object-drawnvalue) object.

Specifically, this fires for clicks on pie slices, bars or columns, areas, lines or points (in a Bubble or Scatter plot).

If there are multiple data values at the clicked position, you can use [FacetChart.getNearestDrawnValues](#method-facetchartgetnearestdrawnvalues) to discover the full list of values at the current coordinate (pass in [getOffsetX/Y()](Canvas.md#method-canvasgetoffsetx) for the coordinates).

If you want to create behaviors for clicking or moving _near_ shapes without requiring a direct hit, implement a standard [Canvas.click](Canvas.md#method-canvasclick) handler on the FacetChart as a whole and use [FacetChart.getNearestDrawnValue](#method-facetchartgetnearestdrawnvalue) to discover the nearest data values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| drawnValue | [DrawnValue](#type-drawnvalue) | false | — | information about the value that was clicked |

---
## Method: FacetChart.setShowScatterLines

### Description
Method to change the current [showScatterLines](../main.md#type-charttype). Will redraw the chart if drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showScatterLines | [Boolean](#type-boolean) | false | — | whether to draw lines between adjacent data points in "Scatter" plots |

---
## Method: FacetChart.chartBackgroundDrawn

### Description
Called when most elements of the chart _other than data_ data have been drawn, including gradations and legend.

This notification will be fired each time the chart is redrawn (due to resize, data change, etc). If you want to draw additional information on the chart using [DrawPane](DrawPane.md#class-drawpane) (FacetChart's superclass) and various [DrawItem](DrawItem.md#class-drawitem)s, you should do in response to this notification. Due to auto-sizing, APIs that are typically used to position custom DrawItems (such as [FacetChart.getChartLeft](#method-facetchartgetchartleft)) may return bad values if called at other times.

Additional DrawItems added in this method will appear underneath data elements such as bars or columns. See [FacetChart.chartDrawn](#method-facetchartchartdrawn) for placing DrawItems on top of data elements.

---
## Method: FacetChart.getMinClusterSize

### Description
Returns the minimum cluster size (for clustered charts), or minimum bar thickness (for histogram or stacked charts) for the specified [data label\\n facet](#method-facetchartgetdatalabelfacet) value. Only applicable to a column, bar, or histogram chart. No default implementation. Both this minimum and [FacetChart.minBarThickness](#attr-facetchartminbarthickness) are used together to determine the effective minimum of the cluster or bar stack.

Per-facet-value minimum cluster sizes aren't supported for [multi-axis](../main_2.md#object-metricsettings) charts, in which multiple chart types are overlaid onto the same chart.

Note that this method is simply an override point, since it has no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | data label axis index of cluster or bar stack |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | data label facet value id of cluster or bar stack |

### Returns

`[int](../main.md#type-int)` — minimum for the specified cluster or bar stack

### Groups

- barChart

### See Also

- [FacetChart.rotateLabels](#attr-facetchartrotatelabels)

---
## Method: FacetChart.getDataColor

### Description
Get a color from the [FacetChart.dataColors](#attr-facetchartdatacolors) Array.

Override to provide a dynamic color generation scheme.

In most cases, the method is passed the associated data Record, which can be used to retrieve the value being processed.

Must return a color in the format of a leading hash (#) plus 6 hexadecimal digits as specified for [FacetChart.dataColors](#attr-facetchartdatacolors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to be colored |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to be colored |
| purpose | [String](#type-string) | false | — | purpose for the requested color - such as "legend", "line", "area", "points", etc. |
| record | [Record](#type-record) | true | — | record associated with this call |

### Returns

`[CSSColor](../main_2.md#type-csscolor)` — —

### See Also

- [FacetChart.getDataLineColor](#method-facetchartgetdatalinecolor)
- [FacetChart.getDataGradient](#method-facetchartgetdatagradient)

---
## Method: FacetChart.setShowRegressionLine

### Description
Setter for [FacetChart.showRegressionLine](#attr-facetchartshowregressionline).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showRegressionLine | [Boolean](#type-boolean) | false | — | New value for this.showRegressionLine. |

---
## Method: FacetChart.getMedian

### Description
Calculate the median of the data over a single metric. See [http://en.wikipedia.org/wiki/Median](http://en.wikipedia.org/wiki/Median).

The first argument, criteria, determines which metric is used to calculate the median. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |

### Returns

`[Float](../main.md#type-float)` — the median of the data values

---
## Method: FacetChart.getDataLabelFacet

### Description
Returns the [Facet](Facet.md#class-facet) in the list of [facets](#attr-facetchartfacets) whose [values](Facet.md#attr-facetvalues) are rendered as labels along the data axis of the chart or in the main chart area.

Most single-facet charts and all multi-facet charts have the data label facet as their first facet. The exceptions are that single-facet Pie/Doughnut charts and Bubble and Scatter charts do not have data label facets.

Note that the user may swap the data label facet and the [legend facet](#method-facetchartgetlegendfacet) in most chart types using the context menu.

### Returns

`[Facet](#type-facet)` — the data label facet, or `null` if there is no such facet

### See Also

- [FacetChart.facets](#attr-facetchartfacets)

---
## Method: FacetChart.setZoomStartValue

### Description
Setter for [FacetChart.zoomStartValue](#attr-facetchartzoomstartvalue).

Note that the [FacetChart.zoomStartValue](#attr-facetchartzoomstartvalue) and [FacetChart.zoomEndValue](#attr-facetchartzoomendvalue) may be set simultaneously using [FacetChart.zoomTo](#method-facetchartzoomto).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zoomStartValue | [Any](#type-any) | false | — | New start value for the data range shown in the main chart |

### Groups

- zoom

---
## Method: FacetChart.setFilled

### Description
Method to change [filled](#attr-facetchartfilled). Use null to apply a default value for the current [chartType](../main.md#type-charttype).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| filled | [Boolean](#type-boolean) | false | — | new value |

### Groups

- chartType

---
## Method: FacetChart.invalidateCache

### Description
Invalidate the current data cache for this databound component via a call to the dataset's `invalidateCache()` method, for example, [ResultSet.invalidateCache](ResultSet.md#method-resultsetinvalidatecache).

**NOTE:** there is no need to call `invalidateCache()` when a save operation is performed on a DataSource. Automatic cache synchronization features will automatically update caches - see [ResultSet](ResultSet.md#class-resultset) for details. If automatic cache synchronization isn't working, troubleshoot the problem using the steps suggested [in the FAQ](http://forums.smartclient.com/showthread.php?t=8159#aGrid) rather than just calling invalidateCache(). Calling `invalidateCache()` unnecessarily causes extra server load and added code complexity.

Calling `invalidateCache()` will automatically cause a new fetch to be performed with the current set of criteria if data had been previously fetched and the component is currently drawn with data visible - there is no need to manually call fetchData() after invalidateCache() and this could result in duplicate fetches.

While data is being re-loaded after a call to `invalidateCache()`, the widget is in a state similar to initial data load - it doesn't know the total length of the dataset and any APIs that act on records or row indices will necessarily fail and should not be called. To detect that the widget is in this state, call [ResultSet.lengthIsKnown](ResultSet.md#method-resultsetlengthisknown).

`invalidateCache()` only has an effect if this components dataset is a data manager class that manages a cache (eg ResultSet or ResultTree). If data was provided as a simple Array or List, invalidateCache() does nothing.

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](ListGrid_2.md#method-listgridrefreshdata)

---
## Method: FacetChart.setRegressionLineType

### Description
Setter for [RegressionLineType](../main_2.md#type-regressionlinetype).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| regressionLineType | [RegressionLineType](../main_2.md#type-regressionlinetype) | false | — | New value for this.regressionLineType |

---
## Method: FacetChart.getNumDataPoints

### Description
Count the number of data points.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [FacetValueMap](#type-facetvaluemap) | true | — | a set of facetValues describing a slice of the data |

### Returns

`[Integer](../main_2.md#type-integer)` — the number of data values

---
## Method: FacetChart.getPointHoverHTML

### Description
When [FacetChart.showDataPoints](#attr-facetchartshowdatapoints) is true and the mouse hovers over a point, this method is called and may return HTML to show in a hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../main.md#type-float) | false | — | the value at the point |
| record | [Record](#type-record) | false | — | the record at the point |
| metricId | [String](#type-string) | false | — | the ID of the metric at the point |

### Returns

`[HTMLString](../main.md#type-htmlstring)` — String of HTML to show in a hover

---
## Method: FacetChart.getLegendHoverHTML

### Description
Called when the mouse hovers over a color swatch or its label in the legend area of the chart.

The [FacetValue](../main.md#object-facetvalue) that the user is hovering over is provided. If the chart is a [multi-axis chart](#attr-facetchartextraaxismetrics), the [FacetValue](../main.md#object-facetvalue) for the hovered-over metric will also be provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValue | [FacetValue](#type-facetvalue) | false | — | facetValue that the mouse is over |
| metricFacetValue | [FacetValue](#type-facetvalue) | false | — | for a multi-axis chart, facetValue representing the hovered-over metric. Null if chart is not multi-axis |

### Returns

`[HTMLString](../main.md#type-htmlstring)` — hover text to be shown. Return null to avoid a hover being shown

### Groups

- legend

---
## Method: FacetChart.setRegressionPolynomialDegree

### Description
Setter for [FacetChart.regressionPolynomialDegree](#attr-facetchartregressionpolynomialdegree).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| regressionPolynomialDegree | [Number](#type-number) | false | — | New value for this.regressionPolynomialDegree. |

---
## Method: FacetChart.getDrawnValueAtPoint

### Description
Returns a [DrawnValue](../main_2.md#object-drawnvalue) object for the data value that is shown nearest to the passed coordinates only if it's under the given coordinates, or under the current mouse event coordinates if no coordinates are passed. This method is similar to [FacetChart.getNearestDrawnValue](#method-facetchartgetnearestdrawnvalue), but the DrawnValue is only returned if it's under the coordinates.

See [FacetChart.drawnValueContainsPoint](#method-facetchartdrawnvaluecontainspoint) for the criteria that determine whether a DrawnValue is under (contains) the coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | true | — | X coordinate. If this parameter is specified, then `y` is a required parameter. |
| y | [Integer](../main_2.md#type-integer) | true | — | Y coordinate |
| metric | [String](#type-string) | true | — | metric over which to determine the drawn value |

### Returns

`[DrawnValue](#type-drawnvalue)` — the nearest drawn value if under the given coordinates (or current mouse event coordinates) or null if not under the coordinates, or for invalid arguments / incorrect timing of call.

---
## Method: FacetChart.getRange

### Description
Calculate the range of the data from a single metric.

The first argument, criteria, determines which metric is used to calculate the range. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |

### Returns

`[Float](../main.md#type-float)` — the range of the data values

---
## Method: FacetChart.fetchData

### Description
Retrieves data from the DataSource that matches the specified criteria.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

When `fetchData()` is first called, if data has not already been provided via [setData()](ListGrid_2.md#method-listgridsetdata), this method will create a [ResultSet](ResultSet.md#class-resultset), which will be configured based on component settings such as [DataBoundComponent.fetchOperation](DataBoundComponent.md#attr-databoundcomponentfetchoperation) and [DataBoundComponent.dataPageSize](DataBoundComponent.md#attr-databoundcomponentdatapagesize), as well as the general purpose [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). The created ResultSet will automatically send a DSRequest to retrieve data from [listGrid.dataSource](ListGrid_1.md#attr-listgriddatasource), and from then on will automatically manage paging through large datasets, as well as performing filtering and sorting operations inside the browser when possible - see the [ResultSet](ResultSet.md#class-resultset) docs for details.

**NOTE:** do not use **both** [autoFetchData:true](DataBoundComponent.md#attr-databoundcomponentautofetchdata) **and** a call to `fetchData()` - this may result in two DSRequests to fetch data. Use either [autoFetchData](DataBoundComponent.md#attr-databoundcomponentautofetchdata) and [Criteria](../main_2.md#type-criteria) **or** a manual call to fetchData() passing criteria.

Whether a ResultSet was automatically created or provided via [setData()](ListGrid_2.md#method-listgridsetdata), subsequent calls to fetchData() will simply call [ResultSet.setCriteria](ResultSet.md#method-resultsetsetcriteria).

Changes to criteria may or may not result in a DSRequest to the server due to [client-side filtering](ResultSet.md#attr-resultsetuseclientfiltering). You can call [willFetchData(criteria)](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine if new criteria will result in a server fetch.

If you need to force data to be re-fetched, you can call [invalidateCache()](ListGrid_2.md#method-listgridinvalidatecache) and new data will automatically be fetched from the server using the current criteria and sort direction. **NOTE:** when using `invalidateCache()` there is no need to **also** call `fetchData()` and in fact this could produce unexpected results.

This method takes an optional callback parameter (set to a [DSCallback](../main_2.md#type-dscallback)) to fire when the fetch completes. Note that this callback will not fire if no server fetch is performed. In this case the data is updated synchronously, so as soon as this method completes you can interact with the new data. If necessary, you can use [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine whether or not a server fetch will occur when `fetchData()` is called with new criteria.

In addition to the callback parameter for this method, developers can use [dataArrived()](ListGrid_2.md#method-listgriddataarrived) to be notified every time data is loaded.

By default, this method assumes a [TextMatchStyle](../main_2.md#type-textmatchstyle) of "exact"; that can be overridden by supplying a different value in the requestProperties parameter. See [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata);

**Changing the request properties**

Changes to [TextMatchStyle](../main_2.md#type-textmatchstyle) made via `requestProperties` will be honored in combination with the fetch criteria, possibly invalidating cache and triggering a server request if needed, as documented for [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata). In contrast, changes to [operationId](DSRequest.md#attr-dsrequestoperationid) in the request properties will cause the [ResultSet](ResultSet.md#class-resultset) or [ResultTree](ResultTree.md#class-resulttree) to be rebuilt, always refetching from the server. However, changes to other request properties after the initial fetch won't be detected, and no fetch will get triggered based on that new request context.

To pick up such changes, we recommend that you call [setData(\[\])](#method-facetchartsetdata) (passing an empty array to ensure the data model is cleared), and then call this method to fetch again. If you try to do it by calling [invalidateCache()](ListGrid_2.md#method-listgridinvalidatecache), you may see duplicate fetches if you haven't already updated the data context by calling this method with the new request properties, and fail to do so before the component is [redrawn](Canvas.md#method-canvasredraw).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../main_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../main_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](ListGrid_2.md#method-listgridrefreshdata)

---
## Method: FacetChart.getYCoord

### Description
Returns the Y coordinate where the passed data value either was or would be drawn. For example, this would be the Y coordinate that a line would pass through on a line chart, or the top of a column on a column chart.

This is only allowed to be called after [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

If the [chartType](#attr-facetchartcharttype) is "Area", "Bubble", "Column", "Histogram", "Line", or "Scatter" then the `value` argument should be a number. For "Bar" charts this method expects a [FacetValueMap](../main.md#object-facetvaluemap) that uniquely identifies the data cell whose Y-axis coordinate is to be retrieved.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../main.md#type-float)|[FacetValueMap](#type-facetvaluemap) | false | — | the value to be drawn. |

### Returns

`[Float](../main.md#type-float)` — the Y coordinate where the passed data value would be drawn.

---
## Method: FacetChart.drawnValueContainsPoint

### Description
Returns whether a given [DrawnValue](../main_2.md#object-drawnvalue) contains a point. The point's X and Y coordinates may be passed into this method, or, if unspecified, the coordinates used are the current mouse event coordinates.

For Area, Bubble, Line, Radar, and Scatter charts, a DrawnValue is considered to contain a point if the Euclidean distance from the DrawnValue's center ([x](DrawnValue.md#attr-drawnvaluex), [y](DrawnValue.md#attr-drawnvaluey)) to the point is less than [this.dataPointSize](#attr-facetchartdatapointsize). For Pie charts, the DrawnValue is considered to contain a point if the point is within the pie slice. Similarly, for Doughnut charts, the DrawnValue is considered to contain a point if the point is within the pie slice and not in the doughnut hole. For Bar and Column charts, the DrawnValue is considered to contain a point if the point is within the bar or column, respectively. Note that for stacked Bar and Column charts, the point must also be in the stacked portion as opposed to anywhere within the bar or column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| drawnValue | [DrawnValue](#type-drawnvalue) | false | — | the DrawnValue to check. The DrawnValue must be a valid DrawnValue from this chart. |
| x | [Integer](../main_2.md#type-integer) | true | — | X coordinate of the point. If this parameter is specified, then `y` is a required parameter. |
| y | [Integer](../main_2.md#type-integer) | true | — | Y coordinate of the point |

### Returns

`[Boolean](#type-boolean)` — true if the DrawnValue contains the point at the given X, Y coordinates (or current mouse event coordinates); false if the DrawnValue does not contain the point; null for invalid parameters.

---
## Method: FacetChart.setOtherAxisGradationGaps

### Description
Setter for [FacetChart.otherAxisGradationGaps](#attr-facetchartotheraxisgradationgaps).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradationGaps | [Array of Float](#type-array-of-float) | false | — | new [FacetChart.otherAxisGradationGaps](#attr-facetchartotheraxisgradationgaps) value |

### Groups

- gradations

---
## Method: FacetChart.getGradations

### Description
Return an array of the gradation values used in the current chart. Pass these values to [FacetChart.getXCoord](#method-facetchartgetxcoord) / [FacetChart.getYCoord](#method-facetchartgetycoord) (depending on the orientation of the chart) to discover the coordinates where gradations are drawn.

This is only allowed to be called when [FacetChart.chartDrawn](#method-facetchartchartdrawn) fires.

### Returns

`[Array of float](#type-array-of-float)` — an array of gradation values used in the current chart.

### Groups

- gradations

---
## Method: FacetChart.setChartType

### Description
Method to change the current [chartType](../main.md#type-charttype). Will redraw the chart if drawn. Will use default settings for the new chart type for [stacked](#attr-facetchartstacked) and [filled](#attr-facetchartfilled) if those values are null.

Note that for [multi-axis](#attr-facetchartextraaxismetrics) charts this method changes the `chartType` for the main value axis only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| chartType | [ChartType](../main.md#type-charttype) | false | — | new chart type |

### Groups

- chartType

---
## Method: FacetChart.getStdDev

### Description
Calculate the standard deviation of the data from a single metric. See [http://en.wikipedia.org/wiki/Standard\_deviation](http://en.wikipedia.org/wiki/Standard_deviation).

The first argument, criteria, determines which metric is used to calculate the standard deviation. The criteria may be a String that is the "id" of some [FacetValue](../main.md#object-facetvalue) of the metric facet, or a [FacetValueMap](../main.md#object-facetvaluemap) that contains an entry for the metric facet, or null to use the [FacetChart.valueProperty](#attr-facetchartvalueproperty). A FacetValueMap criteria may also be used to restrict the calculation to a slice of the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [String](#type-string)|[FacetValueMap](#type-facetvaluemap) | false | — | the "id" of a metric facet value, or a set of mappings describing the data over which to calculate, or null |
| population | [boolean](../main.md#type-boolean) | false | — | false to calculate a sample standard deviation, true to calculate a population standard deviation |

### Returns

`[Float](../main.md#type-float)` — the standard deviation of the data values

---
