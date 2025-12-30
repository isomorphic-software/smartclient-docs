# Gauge Documentation

[← Back to API Index](../reference.md)

---

## Class: Gauge

*Inherits from:* [DrawPane](DrawPane.md#class-drawpane)

### Description
The Gauge widget class implements a graphical speedometer-style gauge for displaying a measurement by means of a needle on a dial. The dial is divided into sectors, each having its own color and value.

**NOTE:** you must load the Drawing [Optional Module](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) before you can use Gauge.

---
## Attr: Gauge.dialRadius

### Description
Radius in pixels of the dial.

**Flags**: IRW

---
## Attr: Gauge.borderColor

### Description
Color for gauge sector borders.

### See Also

- [DrawItem.lineColor](DrawItem.md#attr-drawitemlinecolor)

**Flags**: IR

---
## Attr: Gauge.drawnClockwise

### Description
Whether the sectors are drawn clockwise, and increasing the value causes the needle to move clockwise.

**Flags**: IRW

---
## Attr: Gauge.sectorShape

### Description
MultiAutoChild representing the sectors drawn to show different segments of the gauge.

**Flags**: IR

---
## Attr: Gauge.value

### Description
The current value on the dial.

**Flags**: IRW

---
## Attr: Gauge.sectorColors

### Description
Array of preset fill colors used by the default implementation of [Gauge.getDefaultFillColor](#method-gaugegetdefaultfillcolor) to initialize the fill color of new sectors.

The default array of colors is:

| #AFFFFF | #008080 | #AAAFFF | #FF0000 | #FFCC99 | #800080 |
|---|---|---|---|---|---|

### See Also

- [DrawItem.fillColor](DrawItem.md#attr-drawitemfillcolor)

**Flags**: IR

---
## Attr: Gauge.minValue

### Description
The minimum dial value.

**Flags**: IRW

---
## Attr: Gauge.needle

### Description
AutoChild representing the needle shape that points to the gauge's current value. Default is to use a DrawTriangle.

**Flags**: IR

---
## Attr: Gauge.tickLine

### Description
MultiAutoChild representing the tick marks drawn along the circumference of the gauge. Default is to use DrawLine.

**Flags**: IR

---
## Attr: Gauge.numMinorTicks

### Description
The number of minor tick lines.

**Flags**: IRW

---
## Attr: Gauge.pivotPointHeight

### Description
Default height of the [Gauge.pivotPoint](#attr-gaugepivotpoint) if no specific pivotPoint is specified.

Can be specified as a numeric pixel value, or a String percentage value.

**Flags**: IR

---
## Attr: Gauge.labelPrefix

### Description
The label prefix.

### See Also

- [Gauge.formatLabelContents](#method-gaugeformatlabelcontents)

**Flags**: IRW

---
## Attr: Gauge.borderWidth

### Description
Pixel width for gauge sector borders.

### See Also

- [DrawItem.lineWidth](DrawItem.md#attr-drawitemlinewidth)

**Flags**: IR

---
## Attr: Gauge.valueLabel

### Description
MultiAutoChild representing the labels used to different data points on the gauge.

**Flags**: IR

---
## Attr: Gauge.pivotShape

### Description
AutoChild representing the shape drawn at the [Gauge.pivotPoint](#attr-gaugepivotpoint) (where all sectors of the gauge meet).

**Flags**: IR

---
## Attr: Gauge.pivotPoint

### Description
The pivot point of the needle.

**Flags**: IRW

---
## Attr: Gauge.labelSuffix

### Description
The label suffix.

### See Also

- [Gauge.formatLabelContents](#method-gaugeformatlabelcontents)

**Flags**: IRW

---
## Attr: Gauge.maxValue

### Description
The maximum dial value.

**Flags**: IRW

---
## Attr: Gauge.sectors

### Description
The GaugeSectors contained in this Gauge. If this this property is not specified, the gauge will be created with a default sector filling the gauge.

**Flags**: IRW

---
## Attr: Gauge.numMajorTicks

### Description
The number of major tick lines.

**Flags**: IRW

---
## Attr: Gauge.fontSize

### Description
Font size of sector labels. Must be at least 3.

### See Also

- [DrawLabel.fontSize](DrawLabel.md#attr-drawlabelfontsize)

**Flags**: IR

---
## Method: Gauge.setDialRadius

### Description
All DrawItems currently associated with this Gauge are destroyed and new DrawItems are created instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dialRadius | [float](../reference.md#type-float) | false | — | Radius in pixels of the dial |

---
## Method: Gauge.setDrawnClockwise

### Description
Sets the [drawnClockwise](#attr-gaugedrawnclockwise) property and redraws the gauge.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| drawnClockwise | [boolean](../reference.md#type-boolean) | false | — | whether the sectors are drawn clockwise. |

---
## Method: Gauge.addSector

### Description
Adds a new sector.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newSector | [GaugeSector](#type-gaugesector)|[double](../reference.md#type-double) | false | — | the new GaugeSector or the new sector's value. This is formatted with [Gauge.formatLabelContents](#method-gaugeformatlabelcontents) to get its label. |

### Returns

`[int](../reference.md#type-int)` — the index of the newly-added sector.

---
## Method: Gauge.formatLabelContents

### Description
Formats a value as a string to be used as the contents of a [DrawLabel](DrawLabel.md#class-drawlabel). The default implementation prepends [labelPrefix](#attr-gaugelabelprefix) and appends [labelSuffix](#attr-gaugelabelsuffix) to `value`.

**NOTE:** If a subclass overrides this, then whenever it changes the way that values are formatted, it must call [Gauge.reformatLabelContents](#method-gaugereformatlabelcontents).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../reference.md#type-float) | false | — | the value to format. |

### Returns

`[String](#type-string)` — label contents.

**Flags**: A

---
## Method: Gauge.setLabelPrefix

### Description
Sets the [labelPrefix](#attr-gaugelabelprefix) property and re-creates all sector labels.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelPrefix | [String](#type-string) | false | — | the new label prefix. |

---
## Method: Gauge.setMinValue

### Description
Sets the minimum dial value, rescaling all sectors and the dial value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| minValue | [float](../reference.md#type-float) | false | — | the new minimum dial value. Must be at least 1 less than the maximum dial value. If `minValue` is not at least 1 less than the maximum value, then it is set to `maxValue - 1`. |

---
## Method: Gauge.setSectors

### Description
Sets the sectors for this gauge.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectors | [Array of GaugeSector](#type-array-of-gaugesector) | false | — | the sectors to show on the gauge. |

---
## Method: Gauge.setPivotPoint

### Description
All DrawItems currently associated with this Gauge are destroyed and new DrawItems are created instead.

The pivot point is set by default by choosing 1/2 of width and 70% of height of the Gauge. See [pivotPointHeight](#attr-gaugepivotpointheight)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| point | [Point](#type-point) | false | — | The pivot point of the needle |

---
## Method: Gauge.getNumSectors

### Description
Gets the number of sectors.

### Returns

`[int](../reference.md#type-int)` — the number of sectors on this gauge.

---
## Method: Gauge.getSectorLabelContents

### Description
Gets the label contents of the label for the sector at sectorIndex.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectorIndex | [int](../reference.md#type-int) | false | — | index of the target sector. |

### Returns

`[String](#type-string)` — the label contents of the sector's label.

---
## Method: Gauge.reformatLabelContents

### Description
Resets the contents of all labels. This involves calling [Gauge.formatLabelContents](#method-gaugeformatlabelcontents) to get the label contents for each corresponding value and repositioning the label.

**Flags**: A

---
## Method: Gauge.getSectorFillColor

### Description
Gets the fill color of the sector at index `sectorIndex`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectorIndex | [int](../reference.md#type-int) | false | — | index of the target sector. |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — the fill color of the sector at `sectorIndex`.

### See Also

- [DrawItem.fillColor](DrawItem.md#attr-drawitemfillcolor)

---
## Method: Gauge.getSectorValue

### Description
Gets the value of the sector at `sectorIndex`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectorIndex | [int](../reference.md#type-int) | false | — | index of the target sector. |

### Returns

`[float](../reference.md#type-float)` — the value of the sector at `sectorIndex`.

---
## Method: Gauge.setNumMinorTicks

### Description
Sets the number of minor tick lines.

**NOTE:** To divide the dial into _n_ regions, you will need _n_ + 1 ticks. For example, if the minimum value is 0 and the maximum value is 100, then to place minor tick lines at 0, 1, 2, 3, 4, 5, ..., 99, 100, you need 101 (100 + 1) minor ticks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| numMinorTicks | [int](../reference.md#type-int) | false | — | the number of minor tick lines to draw. Must be either 0 or an integer greater than or equal to 2. |

---
## Method: Gauge.getDefaultFillColor

### Description
Gets the default fill color for the sector at index `sectorIndex`. The default implementation cycles through [sectorColors](#attr-gaugesectorcolors) using modular arithmetic.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectorIndex | [int](../reference.md#type-int) | false | — | index of the target sector. |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — a fill color.

**Flags**: A

---
## Method: Gauge.setNumMajorTicks

### Description
Sets the number of major tick lines.

**NOTE:** To divide the dial into _n_ regions, you will need _n_ + 1 ticks. For example, if the minimum value is 0 and the maximum value is 100, then to place major tick lines at 0, 10, 20, 30, ..., 90, 100, you need 11 (10 + 1) major ticks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| numMajorTicks | [int](../reference.md#type-int) | false | — | the number of major tick lines to draw. Must be either 0 or an integer greater than or equal to 2. |

---
## Method: Gauge.setSectorFillColor

### Description
Sets the fill color of the sector at `sectorIndex`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectorIndex | [int](../reference.md#type-int) | false | — | index of the target sector. |
| fillColor | [CSSColor](../reference_2.md#type-csscolor) | false | — | the new fill color. |

### See Also

- [DrawItem.setFillColor](DrawItem.md#method-drawitemsetfillcolor)

---
## Method: Gauge.removeSector

### Description
Removes the sector at sectorIndex.

**NOTE:** There must always be one sector and it is not possible to remove the sole remaining sector. Calling this method to attempt to remove the sole remaining sector is a no-op.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sectorIndex | [int](../reference.md#type-int) | false | — | the index of the sector to remove. |

---
## Method: Gauge.setMaxValue

### Description
Sets the maximum dial value, rescaling all sectors and the dial value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| maxValue | [float](../reference.md#type-float) | false | — | the new maximum dial value. Must be at least 1 greater than the minimum dial value. If `maxValue` is not at least 1 greater than the minimum value, then it is set to `1 + minValue`. |

---
## Method: Gauge.setLabelSuffix

### Description
Sets the [labelSuffix](#attr-gaugelabelsuffix) property and re-creates all sector labels.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelSuffix | [String](#type-string) | false | — | the new label suffix. |

---
## Method: Gauge.setValue

### Description
Sets the value on the dial that the needle is displaying.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [float](../reference.md#type-float) | false | — | the new dial value. Must be between [minValue](#attr-gaugeminvalue) and [maxValue](#attr-gaugemaxvalue). |

---
