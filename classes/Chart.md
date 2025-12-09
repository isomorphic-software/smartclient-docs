# Chart Documentation

[← Back to API Index](../reference.md)

---

## ClassAttr: Chart.allChartTypes

### Description
All [ChartTypes](../reference.md#type-charttype) that are supported by this class. Should be defined by concrete implementations of the charting interface.

**Flags**: R

---
## Attr: Chart.stacked

### Description
Whether to use stacking for charts where this makes sense (bar, column, line and radar charts). If stacked is not set and two facets are supplied, clustering is assumed.

**Flags**: IR

---
## Attr: Chart.chartType

### Description
Type of chart to draw, see [ChartType](../reference.md#type-charttype) for a list of known types.

**Flags**: IRW

---
## Attr: Chart.subTitle

### Description
Subtitle for the chart as a whole, typically used to describe fixed facet values (such as "for Q1, 1999").

The subTitle should appear under the title in less emphasized text.

**Flags**: IR

---
## Attr: Chart.valueProperty

### Description
Property in each record that holds a data value.

Not used if there is an inline facet, see [Chart.data](#attr-chartdata).

**Flags**: IR

---
## Attr: Chart.shouldAnimateShow

### Description
Whether the chart should animate when shown (eg, bars or columns grow into place)

### Groups

- chartAppearance

**Flags**: IR

---
## Attr: Chart.labelValues

### Description
Whether to show labels on each individual value (bar, column or line point)

### Groups

- chartAppearance

**Flags**: IR

---
## Attr: Chart.facets

### Description
An Array of facets, exactly analogous to [CubeGrid.facets](CubeGrid.md#attr-cubegridfacets), except that:

*   the "inlinedValues" property can be set on a facet to change data representation as described under [Chart.data](#attr-chartdata).
*   for a non-inlined facet, Charts support auto-derivation of facetValues from the data.

**Flags**: IR

---
## Attr: Chart.data

### Description
Dataset for this chart.

Two basic formats are supported:

*   "Standard model": `data` is an array of CellRecords where each record contains one data value. Each record also contains a property named after each facetId whose value is a facetValueId from that facet.
    
    For example, with a facet with id "regions" and facetValues "west", "north" and "east", and with [Chart.valueProperty](#attr-chartvalueproperty) with it's default value "\_value", the `data` property could be:
    
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

**Flags**: IR

---
## Attr: Chart.title

### Description
Title for the chart as a whole.

**Flags**: IR

---
## Attr: Chart.threeD

### Description
Whether to show chart in a 3D appearance, for charts that support this.

### Groups

- chartAppearance

**Flags**: IR

---
## Attr: Chart.valueTitle

### Description
A label for the data values, such as "Sales in Thousands", typically used as the label for the value axis.

**Flags**: IR

---
## Method: Chart.setData

### Description
Change the dataset for this chart on the fly. May or may not be supported by concrete chart implementations.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Array of CellRecord](#type-array-of-cellrecord)|[CellRecord](#type-cellrecord) | false | — | new dataset |

---
## Method: Chart.getFacet

### Description
Get a facet definition by facetId.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | the id of the facet to retrieve |

### Returns

`[Facet](#type-facet)` — the Facet if found, or null

### See Also

- [Facet](../reference_2.md#object-facet)

---
## Method: Chart.getFacetValue

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

- [FacetValue](../reference.md#object-facetvalue)

---
## Method: Chart.setupChart

### Description
General facet and data model setup, including auto-derivation of facetValues from data if necessary. Should be called by any concrete charting implementation before calling any other Chart method.

---
## Method: Chart.getValue

### Description
Lookup a data value by the set of matching facetValues expressed as a [FacetValueMap](../reference.md#object-facetvaluemap). Automatically handles the [inlinedFacet](#attr-chartdata), if any.

This method is designed to be called by a concrete Chart implementation.

As a special case, if [Chart.data](#attr-chartdata) is a single Object and the only facet is [inlined](#attr-chartdata), any value can be used as the single facetId required. For example, a legal FacetValueMap in this case would be {inlined:"west"}.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [FacetValueMap](#type-facetvaluemap) | false | — | set of facetValues describing the data value to retrieve |

### Returns

`[Any](#type-any)` — matching value from the dataset, or null if no value exists

---
