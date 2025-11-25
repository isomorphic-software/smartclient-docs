# FacetChartEditProxy Documentation

[← Back to API Index](../main.md)

---

## Class: FacetChartEditProxy

*Inherits from:* [EditProxy](EditProxy.md#class-editproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [FacetCharts](FacetChart.md#class-facetchart) when editMode is enabled.

### Groups

- devTools

---
## Attr: FacetChartEditProxy.dataSeparatorChar

### Description
If [inline editing](../main.md#type-inlineeditevent) for this chart edits the [FacetChart.data](FacetChart.md#attr-facetchartdata), character that should be used as a separator between values, or between pairs of label vs values.

The [dataEscapeChar](#attr-facetcharteditproxydataescapechar) can be used to enter the separator char as part of a field name or value.

**Flags**: IR

---
## Attr: FacetChartEditProxy.dataEscapeChar

### Description
If [inline editing](../main.md#type-inlineeditevent) for this chart edits the [FacetChart.data](FacetChart.md#attr-facetchartdata), character that can be used to enter literal separator chars (such as the [dataSeparatorChar](#attr-facetcharteditproxydataseparatorchar)).

Repeat this character twice to enter it literally. For example, with the default of "\\", inputting "\\\\" would result in a literal backslash in the value.

**Flags**: IR

---
## Attr: FacetChartEditProxy.dataDisplaySeparatorChar

### Description
If [inline editing](../main.md#type-inlineeditevent) for this chart edits the [FacetChart.data](FacetChart.md#attr-facetchartdata), character that should be used as a separator for entering label vs value entries.

With the default of ":", the following input defines four values with titles:

```
      North:10, South:20, East:30, West:40
 
```

The [dataEscapeChar](#attr-facetcharteditproxydataescapechar) can be used to enter literal colon characters.

**Flags**: IR

---
## Method: FacetChartEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `facets` and `data`.

Lines starting with "--" or "==" are considered titles. A single title is used as the chart title. Titles are matched to the next series of data. If titles are provided for each series, a legend will be shown.

Series data can be entered as a list of values separated by commas (see [dataSeparatorChar](#attr-facetcharteditproxydataseparatorchar)) or as a valueMap-style list of `label:value` pairs. The first data series defines the number of chart values and the titles, if provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component data |

---
## Method: FacetChartEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

---
