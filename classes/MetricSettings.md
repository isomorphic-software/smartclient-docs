# MetricSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: MetricSettings.filled

### Description
Whether shapes are filled, for example, whether a multi-series line chart appears as a stack of filled regions as opposed to just multiple lines.

If unset, fills will be automatically used when there are multiple facets and stacking is active (so Line and Radar charts will show stacked regions).

You can explicitly set filled:false to create multi-facet Line or Radar charts where translucent regions overlap, or filled:true to fill in a single-facet Line or Radar chart.

### Groups

- chartType

**Flags**: IRW

---
## Attr: MetricSettings.gradationZeroLineProperties

### Description
Properties for the gradation line drawn for zero (slightly thicker by default).

### Groups

- gradations

**Flags**: IR

---
## Attr: MetricSettings.logScale

### Description
Whether to use logarithmic scaling for values.

Logarithmic scale charts show an equivalent percentage increase as equivalent distance on the chart. That is, 10 and 100 are the same distance apart as 100 and 1000 (each being a 10 times or 1000% increase).

**Flags**: IR

---
## Attr: MetricSettings.fixedFacetValue

### Description
For a [single-facet](#attr-metricsettingsmultifacet) chart of an extra value axis, this property provides a constant facet value for the second facet. By varying the value of the other facet in multi-facet data, the chart obtains the series of values to plot. The default facet value is the first facet value of the second facet.

**Flags**: IR

---
## Attr: MetricSettings.showAxisLine

### Description
Whether to show an axis line for this extra value axis if it is not placed directly adjacent to the chart rect. The default setting is the value of the [showChartRect](FacetChart.md#attr-facetchartshowchartrect) property of the FacetChart.

**Flags**: IR

---
## Attr: MetricSettings.valueLineProperties

### Description
Properties for a "value line" - a line shows where a particular discrete value is placed, eg, vertical lines connecting points of a line chart to the X axis, or radial lines in a Radar chart.

**Flags**: IR

---
## Attr: MetricSettings.shadowProperties

### Description
Properties for shadows.

### Groups

- appearance

**Flags**: IR

---
## Attr: MetricSettings.gradationLineProperties

### Description
Properties for gradation lines

### Groups

- gradations

**Flags**: IR

---
## Attr: MetricSettings.proportionalAxisLabel

### Description
Default title for the value axis label when the chart is in [proportional rendering mode](#attr-metricsettingsproportional). This title will be used unless the [legend facet](FacetChart.md#method-facetchartgetlegendfacet) defines a [proportionalTitle](Facet.md#attr-facetproportionaltitle).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MetricSettings.axisLineProperties

### Description
Properties for the axis line drawn if this extra value axis is not positioned directly adjacent to the chart rect. The default is to match the [lineCap](DrawItem.md#attr-drawitemlinecap), [lineColor](DrawItem.md#attr-drawitemlinecolor), [lineOpacity](DrawItem.md#attr-drawitemlineopacity), [linePattern](DrawItem.md#attr-drawitemlinepattern), and [lineWidth](DrawItem.md#attr-drawitemlinewidth) of the FacetChart's [chart rect.](FacetChart.md#attr-facetchartchartrectproperties) for each axis line.

**Flags**: IR

---
## Attr: MetricSettings.dataLineProperties

### Description
Properties for lines that show data (as opposed to gradations or borders around the data area).

**Flags**: IR

---
## Attr: MetricSettings.dataOutlineProperties

### Description
Properties for lines that outline a data shape (in filled charts such as area or radar charts).

**Flags**: IR

---
## Attr: MetricSettings.dataGradients

### Description
A dictionary of gradients to use for a series of visual elements representing data (eg columns, bars, pie slices), any of which may be adjacent to any other.

**Flags**: IR

---
## Attr: MetricSettings.showShadows

### Description
Whether to automatically show shadows for various charts.

### Groups

- appearance

**Flags**: IR

---
## Attr: MetricSettings.dataPointSize

### Description
Size in pixels for data points drawn for line, area, radar and other chart types.

### Groups

- chartProperties

**Flags**: IR

---
## Attr: MetricSettings.showValueOnHover

### Description
Shows the value of the nearest data value in a floating label whenever the mouse moves within the main chart area. The visual element representing the data value will also be emphasized by brightening or highlighting it (appearance differs by chart type).

Calculates nearest value based on [FacetChart.getNearestDrawnValue](FacetChart.md#method-facetchartgetnearestdrawnvalue).

The data value will be formatted using [FacetChart.formatDataValue](FacetChart.md#method-facetchartformatdatavalue). The label's appearance is controlled by [FacetChart.hoverLabelProperties](FacetChart.md#attr-facetcharthoverlabelproperties).

### Groups

- appearance

**Deprecated**

**Flags**: IR

---
## Attr: MetricSettings.matchGradations

### Description
When this property is set to the metric of another MetricSettings object, the extra value axis and chart corresponding to these settings will use the same scale for the gradations as the extra value axis and chart of the other MetricSettings object. The value of `matchGradations` can only be one of the metrics of the metric facet whose values will be displayed by the chart.

### See Also

- [FacetChart.extraAxisMetrics](FacetChart.md#attr-facetchartextraaxismetrics)

**Flags**: IR

---
## Attr: MetricSettings.chartType

### Description
See [ChartType](../reference.md#type-charttype) for a list of known types - Column, Bar, Line, Pie, Doughnut, Area, Radar, and Histogram charts are supported.

### Groups

- chartType

**Flags**: IRW

---
## Attr: MetricSettings.axisStartValue

### Description
Same as [FacetChart.axisStartValue](FacetChart.md#attr-facetchartaxisstartvalue) but affects only one metric.

**Flags**: IR

---
## Attr: MetricSettings.dataColors

### Description
An array of colors to use for a series of visual elements representing data (eg columns, bars, pie slices), any of which may be adjacent to any other.

Colors must be in the format of a leading hash (#) plus 6 hexadecimal digits, for example, "#FFFFFF" is white, "#FF0000" is pure red.

**Flags**: IRW

---
## Attr: MetricSettings.proportional

### Description
For multi-facet charts, render data values as a proportion of the sum of all data values that have the same label.

Gradation labels will be switched to show percentage instead of absolute values.

This setting is valid only for Column, Bar, Area and Radar chart types and only in [stacked](#attr-metricsettingsstacked) mode. Stacked columns will be as tall as the chart rect and stacked bars will be as wide as the chart rect. Area and Radar charts will be completely filled except for facet values where all values are 0.

**Flags**: IRW

---
## Attr: MetricSettings.gradationLabelProperties

### Description
Properties for gradation labels

### Groups

- gradations

**Flags**: IR

---
## Attr: MetricSettings.valueAxisLabelProperties

### Description
Properties for labels of value axis.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: MetricSettings.showValueAxisLabel

### Description
Whether to show the [valueTitle](#attr-metricsettingsvaluetitle) (or, in the case of [proportional rendering mode](#attr-metricsettingsproportional), [MetricSettings.proportionalAxisLabel](#attr-metricsettingsproportionalaxislabel)) as a label on this extra value axis.

**Flags**: IR

---
## Attr: MetricSettings.dataShapeProperties

### Description
Properties for data shapes (filled areas in area or radar charts).

**Flags**: IR

---
## Attr: MetricSettings.minDataSpreadPercent

### Description
Same as [FacetChart.minDataSpreadPercent](FacetChart.md#attr-facetchartmindataspreadpercent) but affects only one metric. Default of null means that the chart-wide setting `facetChart.minDataSpreadPercent` will be used.

**Flags**: IR

---
## Attr: MetricSettings.stacked

### Description
If the [ChartType](../reference.md#type-charttype) is "Column" then the metric settings may include a setting for [FacetChart.stacked](FacetChart.md#attr-facetchartstacked).

### Groups

- chartType

**Flags**: IRW

---
## Attr: MetricSettings.showAxis

### Description
Whether to show the extra value axis.

**Flags**: IR

---
## Attr: MetricSettings.logBase

### Description
When [MetricSettings.useLogGradations](#attr-metricsettingsuseloggradations), base value for logarithmic gradation lines. Gradation lines will be shown at every power of this value plus intervening values specified by [MetricSettings.logGradations](#attr-metricsettingsloggradations).

### Groups

- gradations

**Flags**: IR

---
## Attr: MetricSettings.dataPointProperties

### Description
Common properties to apply for all data points (see [MetricSettings.showDataPoints](#attr-metricsettingsshowdatapoints)).

### Groups

- dataPoints

**Flags**: IR

---
## Attr: MetricSettings.showDataPoints

### Description
For Line, Area, Radar, Scatter or Bubble charts, whether to show data points for each individual data value.

If shown, the [MetricSettings.pointClick](#method-metricsettingspointclick) and [MetricSettings.getPointHoverHTML](#method-metricsettingsgetpointhoverhtml) APIs can be used to create interactivity.

### Groups

- chartProperties

**Flags**: IR

---
## Attr: MetricSettings.useLogGradations

### Description
Whether to use classic logarithmic gradations, where each order of magnitude is shown as a gradation as well as a few intervening lines. Gradations also begin and end on an order of magnitude. For example, 1,2,4,6,8,10,20,40,60,80,100.

Default gradations can be overridden via [MetricSettings.logBase](#attr-metricsettingslogbase) and [MetricSettings.logGradations](#attr-metricsettingsloggradations).

### Groups

- gradations

**Flags**: IR

---
## Attr: MetricSettings.xAxisEndValue

### Description
Same as [FacetChart.xAxisEndValue](FacetChart.md#attr-facetchartxaxisendvalue) but affects only one metric.

**Flags**: IR

---
## Attr: MetricSettings.legendLabel

### Description
For [single-facet](#attr-metricsettingsmultifacet) charts embedded in a multi-facet main chart, the `legendLabel` defines the text of the legend label for this chart. The default text is the [title](FacetValue.md#attr-facetvaluetitle) of the metric facet value of this value axis concatenated with the [title](FacetValue.md#attr-facetvaluetitle) of the [fixed facet value](#attr-metricsettingsfixedfacetvalue) in parentheses. Set the `legendLabel` to provide custom text for the legend label.

**Flags**: IR

---
## Attr: MetricSettings.decimalPrecision

### Description
The [FacetChart.decimalPrecision](FacetChart.md#attr-facetchartdecimalprecision) used to render the numeric labels of this metric axis.

**Flags**: IR

---
## Attr: MetricSettings.showDataValues

### Description
Should data values be shown as text labels near the shape representing the value, for example, above columns of a column chart, or adjacent to points in a line chart?

If set to false, then data values will not be shown.

If set to true, data values will be shown unless the data density is high enough that labels will potentially overlap, in which case, data values will not be shown and hovers will be shown instead, in the same way as [MetricSettings.showValueOnHover](#attr-metricsettingsshowvalueonhover) shows hovers.

### Groups

- labelsAndTitles

**Deprecated**

**Flags**: IR

---
## Attr: MetricSettings.multiFacet

### Description
Whether this extra value axis plots values while varying the facet values of just the first facet (single-facet) or both first and second facets (multi-facet).

**Flags**: IR

---
## Attr: MetricSettings.valueTitle

### Description
A label for the data values, such as "Sales in Thousands", typically used as the label for the value axis.

### Groups

- labelsAndTitles

**Flags**: IR

---
## Attr: MetricSettings.logGradations

### Description
When [MetricSettings.useLogGradations](#attr-metricsettingsuseloggradations) is set, gradation lines to show in between powers, expressed as a series of integer or float values between 1 and [MetricSettings.logBase](#attr-metricsettingslogbase).

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
## Method: MetricSettings.setStacked

### Description
Method to change [stacked](#attr-metricsettingsstacked). Use null to apply a default value for the current [chartType](../reference.md#type-charttype).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stacked | [Boolean](#type-boolean) | false | — | new value |

### Groups

- chartType

---
## Method: MetricSettings.getPointHoverHTML

### Description
When [MetricSettings.showDataPoints](#attr-metricsettingsshowdatapoints) is true and the mouse hovers over a point, this method is called and may return HTML to show in a hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../reference.md#type-float) | false | — | the value at the point |
| record | [Record](#type-record) | false | — | the record at the point |
| metricId | [String](#type-string) | false | — | the ID of the metric at the point |

### Returns

`[String](#type-string)` — String of HTML to show in a hover

---
## Method: MetricSettings.getDataGradient

### Description
Get a gradient from the [MetricSettings.dataGradients](#attr-metricsettingsdatagradients) Array.

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
## Method: MetricSettings.formatAxisValue

### Description
Return the text string to display in [gradation labels](#attr-metricsettingsgradationlabelproperties) given the raw value for the metric to show on the value axis. This formatter will only be called if the axis has gradation labels, meaning labels drawn at regular intervals not associated with any particular facet value.

Note that the rendering of values in hovers or via [MetricSettings.showDataValues](#attr-metricsettingsshowdatavalues) is handled by [MetricSettings.formatDataValue](#method-metricsettingsformatdatavalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value of the metric |

### Returns

`[String](#type-string)` — the text to display.

### Groups

- display_values

### See Also

- [FacetChart.formatAxisValue](FacetChart.md#method-facetchartformataxisvalue)

---
## Method: MetricSettings.setChartType

### Description
Method to change the current [chartType](../reference.md#type-charttype). Will redraw the chart if drawn. Will use default settings for the new chart type for [stacked](#attr-metricsettingsstacked) and [filled](#attr-metricsettingsfilled) if those values are null.

Note that for [multi-axis](FacetChart.md#attr-facetchartextraaxismetrics) charts this method changes the `chartType` for the main value axis only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| chartType | [ChartType](../reference.md#type-charttype) | false | — | new chart type |

### Groups

- chartType

---
## Method: MetricSettings.getDataLineWidth

### Description
Specifies the width to use for data lines in the chart. No default implementation. If not defined or null is returned, the line width will be set by the appropriate chart properties, such as [FacetChart.dataLineProperties](FacetChart.md#attr-facetchartdatalineproperties), [FacetChart.barProperties](FacetChart.md#attr-facetchartbarproperties), or [FacetChart.bubbleProperties](FacetChart.md#attr-facetchartbubbleproperties).

Note that this method is simply an override point, since it has no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to target |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to target |
| purpose | [String](#type-string) | false | — | purpose for the requested width - such as "legend", "line", "area", "points", etc. |

### Returns

`[int](../reference.md#type-int)` — width to use for data lines or null to use [ChartType](../reference.md#type-charttype) default

### See Also

- [DrawItem.lineWidth](DrawItem.md#attr-drawitemlinewidth)
- [MetricSettings.getDataLineColor](#method-metricsettingsgetdatalinecolor)

---
## Method: MetricSettings.formatDataValue

### Description
Return the text string to display in labels [in the chart-body or in hovers](FacetChart.md#attr-facetchartshowdatavaluesmode) given the raw value for the metric displayed on the value axis.

This method may also be passed the [context](../reference.md#type-formattingcontext) for which the value is being formatted, the record associated with the value and the id of its [facet](FacetChart.md#attr-facetchartfacets).

Note that the rendering of values for gradation labels is handled by [MetricSettings.formatAxisValue](#method-metricsettingsformataxisvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value of the metric |

### Returns

`[String](#type-string)` — the text to display.

### Groups

- display_values

---
## Method: MetricSettings.getYCoord

### Description
Returns the Y coordinate where the passed data value either was or would be drawn. For example, this would be the Y coordinate that a line would pass through on a line chart, or the top of a column on a column chart.

This is only allowed to be called after [FacetChart.chartDrawn](FacetChart.md#method-facetchartchartdrawn) fires.

If the [chartType](FacetChart.md#attr-facetchartcharttype) is "Area", "Bubble", "Column", "Histogram", "Line", or "Scatter" then the `value` argument should be a number. For "Bar" charts this method expects a [FacetValueMap](../reference.md#object-facetvaluemap) that uniquely identifies the data cell whose Y-axis coordinate is to be retrieved.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../reference.md#type-float) | false | — | the value to be drawn. |

### Returns

`[float](../reference.md#type-float)` — the Y coordinate where the passed data value would be drawn.

---
## Method: MetricSettings.pointClick

### Description
When [MetricSettings.showDataPoints](#attr-metricsettingsshowdatapoints) is true, fires when a point is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../reference.md#type-float) | false | — | the value at the point |
| record | [Record](#type-record) | false | — | the record at the point |
| metricId | [String](#type-string) | false | — | the ID of the metric at the point |

---
## Method: MetricSettings.getDataLineColor

### Description
Specifies the color to use for data lines in the chart. No default implementation. If not defined or null is returned, the Framework will default to value of [MetricSettings.getDataColor](#method-metricsettingsgetdatacolor).

Note that this method is simply an override point, since it has no default implementation - must return a color in the format of of a leading hash (#) plus 6 hexadecimal digits as specified for [MetricSettings.dataColors](#attr-metricsettingsdatacolors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to be colored |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to be colored |
| purpose | [String](#type-string) | false | — | purpose for the requested color - such as "legend", "line", "area", "points", etc. |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — color to use for data lines or null to default to [MetricSettings.getDataColor](#method-metricsettingsgetdatacolor)

### See Also

- [MetricSettings.getDataColor](#method-metricsettingsgetdatacolor)
- [MetricSettings.getDataLineWidth](#method-metricsettingsgetdatalinewidth)

---
## Method: MetricSettings.setDataColors

### Description
Setter for [MetricSettings.dataColors](#attr-metricsettingsdatacolors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataColors | [Array of CSSColor](#type-array-of-csscolor) | false | — | New set of data colors |

---
## Method: MetricSettings.setProportional

### Description
Setter for [MetricSettings.proportional](#attr-metricsettingsproportional).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| proportional | [boolean](../reference.md#type-boolean) | false | — | Whether the chart should now use proportional mode. |

---
## Method: MetricSettings.getDataColor

### Description
Get a color from the [MetricSettings.dataColors](#attr-metricsettingsdatacolors) Array.

Override to provide a dynamic color generation scheme.

In most cases, the method is passed the associated data Record, which can be used to retrieve the value being processed.

Must return a color in the format of a leading hash (#) plus 6 hexadecimal digits as specified for [MetricSettings.dataColors](#attr-metricsettingsdatacolors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the legend facet value to be colored |
| facetValueId | [String](#type-string)|[Number](#type-number)|[Date](#type-date) | false | — | id of the legend facet value to be colored |
| purpose | [String](#type-string) | false | — | purpose for the requested color - such as "legend", "line", "area", "points", etc. |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — —

### See Also

- [MetricSettings.getDataLineColor](#method-metricsettingsgetdatalinecolor)
- [MetricSettings.getDataGradient](#method-metricsettingsgetdatagradient)

---
## Method: MetricSettings.getGradations

### Description
Return an array of the gradation values used in the current chart. Pass these values to [MetricSettings.getXCoord](#method-metricsettingsgetxcoord) / [MetricSettings.getYCoord](#method-metricsettingsgetycoord) (depending on the orientation of the chart) to discover the coordinates where gradations are drawn.

This is only allowed to be called when [FacetChart.chartDrawn](FacetChart.md#method-facetchartchartdrawn) fires.

### Returns

`[Array of float](#type-array-of-float)` — an array of gradation values used in the current chart.

### Groups

- gradations

---
## Method: MetricSettings.getXCoord

### Description
Returns the X coordinate where the passed data value either was or would be drawn. For example, this would be the X coordinate where a bar would end in a bar chart.

This is only allowed to be called after [FacetChart.chartDrawn](FacetChart.md#method-facetchartchartdrawn) fires.

If the [chartType](FacetChart.md#attr-facetchartcharttype) is "Bar", "Bubble", or "Scatter" then the `value` argument should be a number. For other rectangular charts, this method expects a [FacetValueMap](../reference.md#object-facetvaluemap) that uniquely identifies the data cell whose X-axis coordinate is to be retrieved.

Note that when [canZoom](FacetChart.md#attr-facetchartcanzoom) is enabled, this API is valid only for data values between [zoomStartValue](FacetChart.md#attr-facetchartzoomstartvalue) and [zoomEndValue](FacetChart.md#attr-facetchartzoomendvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../reference.md#type-float)|[FacetValueMap](#type-facetvaluemap) | false | — | the value to be drawn. |

### Returns

`[Float](../reference.md#type-float)` — the X coordinate where the passed data value would be drawn; or null if the passed `FacetValueMap` does not identify a currently-drawn data cell.

---
## Method: MetricSettings.setFilled

### Description
Method to change [filled](#attr-metricsettingsfilled). Use null to apply a default value for the current [chartType](../reference.md#type-charttype).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| filled | [Boolean](#type-boolean) | false | — | new value |

### Groups

- chartType

---
