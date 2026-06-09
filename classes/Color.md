# Color Documentation

[← Back to API Index](../reference.md)

---

## Attr: Color.ok_h

### Description
Oklch hue angle, 0-360 degrees. This is the value that the `hue` key in [adjust()](Colors.md#classmethod-colorsadjust) and [complement()](Colors.md#classmethod-colorscomplement) operate on. The oklch hue wheel: red ~30, yellow ~90, green ~145, cyan ~195, blue ~265, purple ~310.

This differs from the HSL [h](#attr-colorh) because oklch redistributes hue angles for perceptual uniformity - equal angular steps produce equal perceived color changes.

**Flags**: R

---
## Attr: Color.l

### Description
HSL lightness, 0 (black) to 100 (white), as a percentage.

**Flags**: R

---
## Attr: Color.h

### Description
HSL hue angle, 0-360 degrees. Standard CSS hue wheel: red 0/360, yellow 60, green 120, cyan 180, blue 240, magenta 300.

**Flags**: R

---
## Attr: Color.b

### Description
Blue component, 0-255.

**Flags**: R

---
## Attr: Color.format

### Description
The format detected from the source string used to create this Color (e.g. "hex", "rgb", "hsl", "oklch"). Used as the default output format by [getString()](#method-colorgetstring).

**Flags**: R

---
## Attr: Color.hex

### Description
Pre-computed hex string representation of this color (e.g. "#3366cc"). Includes an alpha component ("#3366ccbf") only when semi-transparent. This is the most commonly needed output format and avoids repeated [getString("hex")](#method-colorgetstring) calls.

**Flags**: R

---
## Attr: Color.ok_L

### Description
Oklch perceptual lightness, 0 (black) to 1 (white). This is the value that [lighten()](Colors.md#classmethod-colorslighten)/[darken()](Colors.md#classmethod-colorsdarken) and the `lightness` key in [adjust()](Colors.md#classmethod-colorsadjust) operate on. Oklch lightness is perceptually uniform - equal numeric steps produce equal perceived brightness changes, unlike HSL [l](#attr-colorl).

**Flags**: R

---
## Attr: Color.r

### Description
Red component, 0-255.

**Flags**: R

---
## Attr: Color.alpha

### Description
Opacity, 0 (fully transparent) to 1 (fully opaque).

**Flags**: R

---
## Attr: Color.ok_C

### Description
Oklch chroma (color intensity), typically 0 (gray) to ~0.4 (vivid). This is the value that [saturate()](Colors.md#classmethod-colorssaturate)/[desaturate()](Colors.md#classmethod-colorsdesaturate) and the `saturation` key in [adjust()](Colors.md#classmethod-colorsadjust) operate on.

**Flags**: R

---
## Attr: Color.s

### Description
HSL saturation, 0 (gray) to 100 (fully saturated), as a percentage.

**Flags**: R

---
## Attr: Color.g

### Description
Green component, 0-255.

**Flags**: R

---
## Method: Color.complement

### Description
Returns a new Color with hue rotated 180 degrees (oklch h + 180).

### Returns

`[Color](#type-color)` — new Color object

### See Also

- [Colors.complement](Colors.md#classmethod-colorscomplement)

---
## Method: Color.getString

### Description
Returns a CSS color string in the specified format, defaulting to the source format detected when this Color was created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format - defaults to [Color.format](#attr-colorformat) |

### Returns

`[String](#type-string)` — CSS color string

---
## Method: Color.saturate

### Description
Returns a new Color with chroma increased (oklch C increased).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| amount | [int](../reference.md#type-int) | false | — | percentage to saturate, 0-100 |

### Returns

`[Color](#type-color)` — new Color object

### See Also

- [Colors.saturate](Colors.md#classmethod-colorssaturate)

---
## Method: Color.equals

### Description
Returns true if this color is visually identical to another (same RGB + alpha).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| other | [String](#type-string)|[Color](#type-color) | false | — | color to compare |

### Returns

`[boolean](../reference.md#type-boolean)` — —

### See Also

- [Colors.equals](Colors.md#classmethod-colorsequals)

---
## Method: Color.isDark

### Description
Returns true if this color is perceptually dark (oklch L < 0.6).

### Returns

`[boolean](../reference.md#type-boolean)` — —

### See Also

- [Colors.isDark](Colors.md#classmethod-colorsisdark)

---
## Method: Color.desaturate

### Description
Returns a new Color with chroma decreased (oklch C decreased).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| amount | [int](../reference.md#type-int) | false | — | percentage to desaturate, 0-100 |

### Returns

`[Color](#type-color)` — new Color object

### See Also

- [Colors.desaturate](Colors.md#classmethod-colorsdesaturate)

---
## Method: Color.setAlpha

### Description
Returns a new Color with the specified alpha value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| alpha | [Double](../reference.md#type-double) | false | — | new alpha, 0-1 |

### Returns

`[Color](#type-color)` — new Color object

---
## Method: Color.lighten

### Description
Returns a new Color lightened by the given amount (oklch L increased).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| amount | [int](../reference.md#type-int) | false | — | percentage to lighten, 0-100 |

### Returns

`[Color](#type-color)` — new Color object

### See Also

- [Colors.lighten](Colors.md#classmethod-colorslighten)

---
## Method: Color.adjust

### Description
Returns a new Color with the specified oklch deltas applied. Supports both friendly keys (`lightness`, `saturation`, `hue`, `alpha`) and raw oklch keys (`L`, `C`, `h`).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| deltas | [Object](../reference.md#type-object) | false | — | adjustments to apply - see [Colors.adjust](Colors.md#classmethod-colorsadjust) |

### Returns

`[Color](#type-color)` — new Color object

### See Also

- [Colors.adjust](Colors.md#classmethod-colorsadjust)

---
## Method: Color.contrast

### Description
Returns the approximate perceptual contrast ratio between this color and another (oklch-based).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| other | [String](#type-string)|[Color](#type-color) | false | — | color to compare against |

### Returns

`[Double](../reference.md#type-double)` — approximate contrast ratio (>= 1.0), or null if other is invalid

### See Also

- [Colors.contrast](Colors.md#classmethod-colorscontrast)

---
## Method: Color.isValid

### Description
Returns true if this Color was successfully parsed from valid input. Invalid Colors (created from unparseable input) have all properties defaulting to black (#000000). Use this to check user-supplied color strings without needing null checks.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the color was parsed successfully

---
## Method: Color.darken

### Description
Returns a new Color darkened by the given amount (oklch L decreased).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| amount | [int](../reference.md#type-int) | false | — | percentage to darken, 0-100 |

### Returns

`[Color](#type-color)` — new Color object

### See Also

- [Colors.darken](Colors.md#classmethod-colorsdarken)

---
