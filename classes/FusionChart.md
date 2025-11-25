# FusionChart Documentation

[← Back to API Index](../main.md)

---

## Class: FusionChart

*Inherits from:* [Flashlet](Flashlet.md#class-flashlet)

### Description
Component that wraps the FusionCharts charting engine.

Provides multiple-series (area, bar, column, line, radar) and single-series (doughnut, pie) chart types. These charts all depict a single continuous dimension (eg revenue), broken down by one or two discrete dimensions (eg product, region).

**NOTE:** you must load the PluginBridges and Charts [Optional Modules](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) before you can use FusionChart.

### See Also

- [loadingOptionalModules](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules)

---
## ClassAttr: FusionChart.allChartTypes

### Description
All [ChartTypes](../main.md#type-charttype) that are supported by this class. Should be defined by concrete implementations of the charting interface.

**Flags**: R

---
## Attr: FusionChart.chartURL

### Description
Full URL to the chart. Needed only if you have renamed the charts such that automatic URL formation won't work.

**Flags**: IR

---
## Attr: FusionChart.fusionVersion

### Description
Version of FusionCharts to assume. If version is "2.3", different names are used for the .swf files for each chart (to match the default names in FusionCharts 2.3), and a lower version of Flash is required (6.0).

**Flags**: IR

---
## Attr: FusionChart.chartsBaseURL

### Description
Base URL where FusionCharts are installed. SmartClient expects to find the FusionCharts ".swf" files under this URL.

The default value indicates that SmartClient will look for a FusionCharts directory parallel to the "isomorphic/" directory.

Note that the URL formation logic automatically compensates for various inconsistencies and typos in the default names for the chart .swf files, as well as differences between FusionCharts 2.3 and 3.0. The chart .swf files should be left exactly as found in the FusionCharts distribution. If you have renamed the charts for other purposes, you can set [FusionChart.chartURL](#attr-fusionchartcharturl) to the full path to any given chart type.

**Flags**: IR

---
## Attr: FusionChart.dataColors

### Description
An array of colors to use for a series of visual elements representing data (eg columns, bars, pie slices), any of which may be adjacent to any other.

Colors are expressed as hexadecimal RRGGBB Strings **with no leading '#' character**.

**Flags**: IR

---
## Attr: FusionChart.chartProperties

### Description
Properties to passthrough to the 'graph' element of the XML generated for FusionCharts.

Some automatic conversions are done:

*   boolean values become '0' and '1' as FusionCharts expects
*   color values with a leading '#' have the '#' stripped to match FusionCharts

**Flags**: IRA

---
## Method: FusionChart.getDataColor

### Description
Get a color from the [FusionChart.dataColors](#attr-fusionchartdatacolors) Array, or white ("FFFFFF") if the index is beyond the end of the Array.

Override to provide a dynamic color generation scheme.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Number](#type-number) | false | — | index of the visual element to be colored |

### Returns

`[String](#type-string)` — color value in hexadecimal RRGGBB format (with no leading '#')

---
