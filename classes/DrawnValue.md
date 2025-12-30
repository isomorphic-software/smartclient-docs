# DrawnValue Documentation

[← Back to API Index](../reference.md)

---

## Attr: DrawnValue.barThickness

### Description
For bar and column charts, thickness of the bar representing this data value.

**Flags**: IR

---
## Attr: DrawnValue.radius

### Description
For pie mode only, the radius of the segment for the data value.

**Flags**: IR

---
## Attr: DrawnValue.record

### Description
The data record of the data point from which this `drawnValue` was created.

Note that a chart with an [inlined facet](Facet.md#attr-facetinlinedvalues) or a [multi-axis chart](FacetChart.md#attr-facetchartextraaxismetrics) may define multiple data points in the same record, each of which will correspond to a different `drawnValue`. The way to uniquely identify the data value of this particular `drawnValue` is to use the [DrawnValue.facetValues](#attr-drawnvaluefacetvalues).

**Flags**: IR

---
## Attr: DrawnValue.facetValues

### Description
FacetValues for the data value.

**Flags**: IR

---
## Attr: DrawnValue.value

### Description
Data value this `drawnValue` represents.

**Flags**: IR

---
## Attr: DrawnValue.y

### Description
Y coordinate where the data value is rendered. In pie mode, returns the Y coordinate of the center of the pie where the data value appears.

**Flags**: IR

---
## Attr: DrawnValue.endAngle

### Description
For pie mode only, start angle of the segment for the data value.

**Flags**: IR

---
## Attr: DrawnValue.startAngle

### Description
For pie mode only, start angle of the segment for the data value.

**Flags**: IR

---
## Attr: DrawnValue.x

### Description
X coordinate where the data value is rendered. In pie mode, returns the X coordinate of the center of the pie where the data value appears.

**Flags**: IR

---
