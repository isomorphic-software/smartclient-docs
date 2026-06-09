# Colors Documentation

[← Back to API Index](../reference.md)

---

## Class: Colors

### Description
Utility class for color format conversion, validation, and manipulation. Accepts any valid CSS color specification (hex, rgb/rgba, hsl/hsla, oklch, named colors, "transparent") and converts between formats.

**Core conversion**

*   [isColor(color, \[format\])](#classmethod-colorsiscolor) - validate a color string, optionally restricting to a specific format
*   [getColor(color)](#classmethod-colorsgetcolor) - convert to a structured object
*   [getString(color, format)](#classmethod-colorsgetstring) - convert to a CSS string

**Inspection and alpha**

*   [getFormat(color)](#classmethod-colorsgetformat) - detect the format of a color string
*   [getAlpha(color)](#classmethod-colorsgetalpha) - extract the alpha (opacity) component
*   [setAlpha(color, alpha)](#classmethod-colorssetalpha) - return a new color with a different alpha
*   [isDark(color)](#classmethod-colorsisdark) - perceptual light-vs-dark test (oklch-based)
*   [contrast(color1, color2)](#classmethod-colorscontrast) - approximate perceptual contrast ratio
*   [equals(color1, color2)](#classmethod-colorsequals) - same-color comparison across formats
*   [flatten(color, \[background\], \[outputFormat\])](#classmethod-colorsflatten) - composite semi-transparent color to opaque

**Manipulation** (all operate in oklch for perceptual uniformity)

*   [adjust(color, deltas)](#classmethod-colorsadjust) - general-purpose multi-axis adjustment
*   [lighten()](#classmethod-colorslighten) / [darken()](#classmethod-colorsdarken) - lightness
*   [saturate()](#classmethod-colorssaturate) / [desaturate()](#classmethod-colorsdesaturate) - chroma
*   [complement()](#classmethod-colorscomplement) - hue rotation by 180 degrees

**Palette generation**

*   [colorScale()](#classmethod-colorscolorscale) - multi-step gradient between two colors
*   [shades()](#classmethod-colorsshades) - lightness ramp from a single color
*   [mix()](#classmethod-colorsmix) - blend two colors at a given ratio
*   [mostReadable()](#classmethod-colorsmostreadable) - pick the highest-contrast candidate

**Color harmony**

*   [triad()](#classmethod-colorstriad) / [tetrad()](#classmethod-colorstetrad) - 3 or 4 evenly-spaced hues
*   [splitComplement()](#classmethod-colorssplitcomplement) - flanking the complement
*   [analogous()](#classmethod-colorsanalogous) - nearby hues

---
## ClassAttr: Colors.colorNames

### Description
Map of all CSS named colors to their hex equivalents, per the W3C CSS Color Level 3 spec. Keys are lowercase color names (e.g. "aliceblue", "coral", "rebeccapurple"); values are short or long hex strings (e.g. "#f0f8ff", "#ff7f50", "#663399").

**Flags**: IR

---
## ClassMethod: Colors.getAlpha

### Description
Returns the alpha (opacity) component of the given color as a float from 0.0 (fully transparent) to 1.0 (fully opaque). Returns null if the color is not valid.

Accepts any valid CSS color string or structured color object. Fully opaque colors that lack an explicit alpha component return 1.0. The keyword `"transparent"` returns 0.0.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |

### Returns

`[Double](../reference.md#type-double)` — alpha component (0.0 - 1.0), or null if invalid

---
## ClassMethod: Colors.isDark

### Description
Returns true if the given color is perceptually dark (i.e. would need light foreground text for readability), false if it is light. Uses oklch lightness, which is perceptually uniform - unlike RGB or HSL brightness, a threshold of 0.6 consistently separates light from dark colors across hues. Use `!isDark(color)` to test for lightness.

Returns null if the color is not valid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |

### Returns

`[Boolean](#type-boolean)` — true if perceptually dark, false if light, null if invalid

---
## ClassMethod: Colors.distance

### Description
Returns a number indicating how different two colors look to the human eye. A result of 0 means the colors are identical; larger values mean more noticeable difference. As a rough guide, values below 0.02 are nearly indistinguishable, 0.02-0.05 are subtly different, 0.05-0.15 are clearly different, and above 0.15 are very distinct.

The calculation uses Euclidean distance in the oklab color space (the Cartesian form of oklch), which is designed so that equal numeric distances correspond to equal perceived differences - unlike RGB or HSL, where the same numeric distance can look dramatically different depending on hue and lightness.

Typical uses include finding similar colors in a palette, detecting near-duplicates, and verifying that a color transformation produced a meaningful change. Returns null if either color is invalid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color1 | [String](#type-string)|[Color](#type-color) | false | — | first color |
| color2 | [String](#type-string)|[Color](#type-color) | false | — | second color |

### Returns

`[Double](../reference.md#type-double)` — perceptual distance (>= 0), or null if either input is invalid

### See Also

- [Colors.contrast](#classmethod-colorscontrast)
- [Colors.equals](#classmethod-colorsequals)

---
## ClassMethod: Colors.brighten

### Description
Returns a brighter, more vivid version of the given color by boosting both chroma (color intensity) and lightness together. This produces an "intensified" highlight rather than a washed-out tint (as [lighten()](#classmethod-colorslighten) alone would) or a hue shift without luminance change (as [saturate()](#classmethod-colorssaturate) alone would).

A typical use is hover highlighting in charts: the highlighted color should look like a more vibrant version of the base color rather than a lighter or pinker variant.

The `amount` controls both axes: lightness receives the full amount while chroma receives half, keeping the color recognizable at typical hover percentages (25–40). For independent control use [adjust()](#classmethod-colorsadjust) directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| amount | [double](../reference.md#type-double) | false | — | percentage to brighten, 0-100 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.dim](#classmethod-colorsdim)
- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.spin

### Description
Rotates the hue of a color by the given number of degrees (in oklch space). Positive values rotate clockwise, negative counter-clockwise. This is a convenience wrapper around [adjust(color, {hue: degrees](#classmethod-colorsadjust))}.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| degrees | [double](../reference.md#type-double) | false | — | signed rotation in degrees (e.g. 90, -45, 180) |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.adjust](#classmethod-colorsadjust)
- [Colors.complement](#classmethod-colorscomplement)

---
## ClassMethod: Colors.getString

### Description
Converts any valid CSS color to a string in the specified format. Accepts a CSS color string or a structured color object (as returned by [Colors.getColor](#classmethod-colorsgetcolor)). Returns null if the input is not a valid color or the format is unrecognized.

Supported target formats:

*   `"hex"` - "#RRGGBB" when opaque, "#RRGGBBAA" when semi-transparent
*   `"rgb"` - "rgb(R, G, B)" when opaque, "rgba(R, G, B, A)" when semi-transparent
*   `"hsl"` - "hsl(H, S%, L%)" when opaque, "hsla(H, S%, L%, A)" when semi-transparent
*   `"oklch"` - "oklch(L% C h)" when opaque, "oklch(L% C h / A)" when semi-transparent

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color)|[Object](../reference.md#type-object) | false | — | any valid CSS color string, or a structured color object with {r,g,b}, {h,s,l}, or {L,C,h} keys |
| format | [ColorFormat](../reference_2.md#type-colorformat) | false | — | target format: "hex", "rgb", "hsl", or "oklch" |

### Returns

`[String](#type-string)` — CSS color string in the target format, or null

---
## ClassMethod: Colors.darken

### Description
Returns a darker version of the given color. Equivalent to `adjust(color, {lightness: -amount})`.

The `amount` is a percentage (0-100) indicating how far to move toward black: 0 returns the original color, 100 returns black. Intermediate values move proportionally - `darken(color, 20)` always looks like "20% darker" regardless of the starting lightness.

For multi-axis adjustments, use [adjust()](#classmethod-colorsadjust) directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| amount | [double](../reference.md#type-double) | false | — | percentage to darken, 0-100 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.lighten](#classmethod-colorslighten)
- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.triad

### Description
Returns the three triadic colors (hues spaced 120 degrees apart). The first element is the original color, the second is +120 degrees, the third is +240 degrees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | base color |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to input format |

### Returns

`[Array of String](#type-array-of-string)` — three CSS color strings

---
## ClassMethod: Colors.splitComplement

### Description
Returns three colors: the original plus two split-complement accents (hue +150 and +210 degrees - flanking the complement rather than hitting it directly). Produces a more nuanced palette than a straight complementary pair.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | base color |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to input format |

### Returns

`[Array of String](#type-array-of-string)` — three CSS color strings

---
## ClassMethod: Colors.saturate

### Description
Returns a more vivid version of the given color by increasing its chroma (color intensity). Equivalent to `adjust(color, {saturation: amount})`.

The `amount` is a percentage (0-100) of additional chroma to add, scaled relative to a practical maximum. A gray color (chroma 0) saturated by 50 produces a clearly visible color; 100 gives full vivid saturation.

For multi-axis adjustments, use [adjust()](#classmethod-colorsadjust) directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| amount | [double](../reference.md#type-double) | false | — | percentage to saturate, 0-100 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.desaturate](#classmethod-colorsdesaturate)
- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.mostReadable

### Description
Returns the color from `candidates` that has the highest contrast against `background`. Useful for choosing a text color that will be readable on a given background - typically called with `["#ffffff", "#000000"]` as candidates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| background | [String](#type-string)|[Color](#type-color) | false | — | the background color to test against |
| candidates | [Array of String](#type-array-of-string) | false | — | list of candidate foreground colors |

### Returns

`[String](#type-string)` — the candidate with the highest contrast ratio, or null if inputs invalid

---
## ClassMethod: Colors.desaturate

### Description
Returns a more muted version of the given color by reducing its chroma (color intensity). Equivalent to `adjust(color, {saturation: -amount})`.

The `amount` is a percentage (0-100) of chroma to remove: 0 returns the original color, 100 returns a pure gray at the same lightness.

For multi-axis adjustments, use [adjust()](#classmethod-colorsadjust) directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| amount | [double](../reference.md#type-double) | false | — | percentage to desaturate, 0-100 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.saturate](#classmethod-colorssaturate)
- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.complement

### Description
Returns the complementary color - the hue on the opposite side of the color wheel (rotated by 180 degrees). Equivalent to `adjust(color, {h: 180})`.

Complementary pairs produce maximum hue contrast and are commonly used for accents, call-to-action elements, or alert states against a primary brand color. The oklch hue wheel: red ~30, yellow ~90, green ~145, cyan ~195, blue ~265, purple ~310. Other useful rotations via [adjust()](#classmethod-colorsadjust): +120/-120 for triadic accents, +90/-90 for square-scheme accents.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.flatten

### Description
Returns an opaque color that looks the same as the given semi-transparent color composited over a background. Solves the layering problem where translucent background colors look different depending on what is behind them - a button on a white panel looks different from the same button on a colored window header, and different again if either is disabled. Flattening removes the dependency on parent backgrounds entirely.

If the input color is already fully opaque (alpha = 1), it is returned unchanged. The optional `background` defaults to white; if it is itself semi-transparent, it is first flattened against white before compositing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | a semi-transparent color to flatten to opaque |
| background | [String](#type-string)|[Color](#type-color) | true | — | background to composite against; defaults to "#ffffff" |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — opaque CSS color string, or null if the input is not a valid color

---
## ClassMethod: Colors.getFormat

### Description
Returns the [ColorFormat](../reference_2.md#type-colorformat) of the given color string, or null if the value is not a valid color. For named colors (e.g. "red") and "transparent", the format is reported as `"hex"` since the canonical representation is hexadecimal.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string) | false | — | a CSS color string |

### Returns

`[ColorFormat](../reference_2.md#type-colorformat)` — the detected format, or null if invalid

---
## ClassMethod: Colors.isColor

### Description
Returns true if the given value is a valid CSS color specification. Accepts any format: hex (#RGB, #RRGGBB, #RRGGBBAA), rgb(), rgba(), hsl(), hsla(), oklch(), named colors, and "transparent".

If `format` is specified, the value must be parseable in that particular format (or be "transparent", which is always valid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color)|[Object](../reference.md#type-object) | false | — | value to test |
| format | [ColorFormat](../reference_2.md#type-colorformat) | true | — | if specified, require this format |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the value represents a valid color

---
## ClassMethod: Colors.getValues

### Description
Returns a plain object with color component values in the requested format. Unlike [Colors.getColor](#classmethod-colorsgetcolor), which returns a full [Color](../reference_2.md#object-color) object with methods and properties in all color spaces, this returns only the numeric components for the requested format - useful when you need raw values for computation without the overhead of a full Color, or when passing components to external APIs.

Supported formats and their returned keys:

*   `"rgb"` - `{r, g, b, alpha}` (0-255 integers, alpha 0-1)
*   `"hsl"` - `{h, s, l, alpha}` (h: 0-360 degrees, s/l: 0-100 percent, alpha 0-1)
*   `"oklch"` - `{L, C, h, alpha}` (L: 0-1 lightness, C: 0+ chroma, h: 0-360 degrees, alpha 0-1)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color)|[Object](../reference.md#type-object) | false | — | any valid CSS color string or [Color](../reference_2.md#object-color) |
| format | [ColorFormat](../reference_2.md#type-colorformat) | false | — | target format: "rgb", "hsl", or "oklch" |

### Returns

`[Object](../reference.md#type-object)` — plain object with numeric component keys, or null if invalid

### See Also

- [Colors.getColor](#classmethod-colorsgetcolor)
- [Colors.getString](#classmethod-colorsgetstring)

---
## ClassMethod: Colors.dim

### Description
Returns a dimmer, less vivid version of the given color — the inverse of [brighten()](#classmethod-colorsbrighten). Reduces both chroma and lightness together, producing a muted, subdued appearance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| amount | [double](../reference.md#type-double) | false | — | percentage to dim, 0-100 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.brighten](#classmethod-colorsbrighten)
- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.getColor

### Description
Parses any valid CSS color into a structured [Color](../reference_2.md#object-color) object with RGB, HSL, and oklch properties pre-computed, plus convenience methods for manipulation.

Accepts any CSS color string (`#hex`, `rgb()`, `hsl()`, `oklch()`, named colors) or a structured component object in any supported color space: `{r, g, b}`, `{h, s, l}`, or `{L, C, h}`.

Always returns a [Color](../reference_2.md#object-color) object. If the input cannot be parsed, the returned object will have [isValid()](Color.md#method-colorisvalid) returning false (properties default to black). If the input is already a [Color](../reference_2.md#object-color), a new Color with the same values is returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color)|[Object](../reference.md#type-object) | false | — | any valid CSS color string, an existing [Color](../reference_2.md#object-color) (copied), or a structured object with {r,g,b}, {h,s,l}, or {L,C,h} keys |

### Returns

`[Color](#type-color)` — a Color object - check [isValid()](Color.md#method-colorisvalid) for parse success

---
## ClassMethod: Colors.shades

### Description
Generates a lightness ramp from a single base color, producing an array of colors that range from near-white to near-black (or a custom range) while preserving the base color's hue and chroma. This is the core skin-generation operation: one brand color in, a full tint/shade palette out.

All interpolation is done in the oklch color space, so each step is perceptually equidistant - no uneven jumps or hue drift.

The `range` parameter controls the lightness endpoints as a two-element array `[startL, endL]` where L is 0 (black) to 1 (white). The default is `[0.95, 0.20]` (near-white to dark). To generate only tints (lighter shades), use e.g. `[0.97, 0.60]`; for only darks, `[0.50, 0.10]`.

Examples of common operations:

```
     var brand = "#3366CC";

     // Full palette: 7 shades from near-white to dark
     isc.Colors.shades(brand, 7)
     // => ["#E8EDF8", "#B6C4E6", "#6D8ACC", "#3D62B0",
     //     "#2A4580", "#1C2F56", "#0E182D"]

     // Tints only (backgrounds, hover fills)
     isc.Colors.shades(brand, 4, [0.95, 0.70])

     // Dark shades only (text, borders, shadows)
     isc.Colors.shades(brand, 4, [0.50, 0.10])

     // Dark-mode palette (dark to light)
     isc.Colors.shades(brand, 7, [0.15, 0.90])

     // Output as oklch for CSS custom properties
     isc.Colors.shades(brand, 5, null, "oklch")
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | base color - any valid CSS color string or structured object from [Colors.getColor](#classmethod-colorsgetcolor) |
| steps | [int](../reference.md#type-int) | false | — | number of colors to produce (minimum 2) |
| range | [Array of double](#type-array-of-double) | true | — | two-element array `[startL, endL]` defining the lightness range; defaults to `[0.95, 0.20]` |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | format for the returned strings; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[Array of String](#type-array-of-string)` — CSS color strings in the requested format, or null if the input is not a valid color

---
## ClassMethod: Colors.adjust

### Description
The general-purpose method for deriving a related color from a base color. Accepts any combination of adjustment keys in the `deltas` object and returns the result as a CSS color string. Single-axis convenience wrappers - [lighten()](#classmethod-colorslighten), [darken()](#classmethod-colorsdarken), [saturate()](#classmethod-colorssaturate), [desaturate()](#classmethod-colorsdesaturate), and [complement()](#classmethod-colorscomplement) - all delegate to this method.

**Friendly percentage keys** (recommended for most uses):

*   **lightness** (-100 to 100): positive values lighten (toward white), negative darken (toward black). See [Colors.lighten](#classmethod-colorslighten)/[darken](#classmethod-colorsdarken).
*   **saturation** (-100 to 100): positive values intensify color, negative desaturate toward gray. See [Colors.saturate](#classmethod-colorssaturate)/[desaturate](#classmethod-colorsdesaturate).
*   **hue** (degrees): signed rotation around the color wheel. See [complement()](#classmethod-colorscomplement) for the hue wheel reference.
*   **alpha**: signed delta to opacity (0 = transparent, 1 = opaque).

**Raw oklch keys** (for fine-grained control - see the [oklch color space](https://oklch.com/)):

*   **L**: signed delta to lightness (0-1). +0.1 is noticeably lighter.
*   **C**: signed delta to chroma (0 = gray, max ~0.4). -0.05 desaturates subtly.
*   **h** and **alpha** work the same as the friendly keys above.

Friendly and raw keys may be mixed freely; friendly keys are applied first. The output format defaults to the input format, so `rgb(...)` input returns `rgb(...)` output, etc.

Examples:

```
     var brand = "#3366CC";

     // Hover: 15% lighter; pressed: 20% darker
     isc.Colors.adjust(brand, {lightness: 15})
     isc.Colors.adjust(brand, {lightness: -20})

     // Disabled: lighter and desaturated
     isc.Colors.adjust(brand, {lightness: 25, saturation: -40})

     // Complementary accent, semi-transparent
     isc.Colors.adjust(brand, {hue: +180, alpha: -0.5})

     // Warm it up and lighten in one call
     isc.Colors.adjust(brand, {lightness: 10, hue: -15})

     // Non-hex input preserves format
     isc.Colors.adjust("hsl(220, 60%, 50%)", {lightness: 20})
     // => "hsl(220, 52%, 66%)"

     // Raw oklch: precise lightness + chroma control
     isc.Colors.adjust(brand, {L: +0.2, C: -0.08})
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | base color - any valid CSS color string or structured object from [Colors.getColor](#classmethod-colorsgetcolor) |
| deltas | [Object](../reference.md#type-object) | false | — | adjustment keys - any combination of friendly keys (`lightness` , `saturation`, `hue`, `alpha`) and/or raw oklch keys (`L`, `C`, `h`). See the key lists above. |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | format for the returned string; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string in the requested format, or null if the input is not a valid color

### See Also

- [Colors.lighten](#classmethod-colorslighten)
- [Colors.darken](#classmethod-colorsdarken)
- [Colors.saturate](#classmethod-colorssaturate)
- [Colors.desaturate](#classmethod-colorsdesaturate)
- [Colors.complement](#classmethod-colorscomplement)

---
## ClassMethod: Colors.analogous

### Description
Returns a set of analogous colors - hues near the original, evenly spaced within a segment of the color wheel. Defaults to 6 results spanning 30 degrees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | base color |
| results | [int](../reference.md#type-int) | true | — | number of colors to return (default 6) |
| slices | [int](../reference.md#type-int) | true | — | how many slices to divide the wheel into (default 30, meaning each step is 12 degrees) |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to input format |

### Returns

`[Array of String](#type-array-of-string)` — CSS color strings

---
## ClassMethod: Colors.mix

### Description
Blends two colors in the oklch color space, producing a single result color. Oklch mixing avoids the muddy midpoints of RGB blending and the hue drift of HSL blending.

The `ratio` controls the blend: 0 returns `color1`, 1 returns `color2`, and 0.5 (the default) returns an equal mix. Intermediate values weight toward the corresponding color.

Common uses include tinting a neutral toward a brand color (e.g. `mix(gray, brand, 0.15)`) and generating overlay effects.

Examples of common operations:

```
     var brand = "#3366CC";

     // Equal mix of two colors
     isc.Colors.mix("#0066FF", "#FFD500")

     // Brand-tinted neutral (for backgrounds, panels)
     isc.Colors.mix("#888888", brand, 0.15)

     // Warm up a gray toward a surface color
     isc.Colors.mix("#F5F5F5", "#FFF3E0", 0.3)

     // Blend brand toward white for a subtle highlight
     isc.Colors.mix(brand, "#FFFFFF", 0.8)

     // Blend brand toward black for a deep shadow
     isc.Colors.mix(brand, "#000000", 0.7)
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color1 | [String](#type-string)|[Color](#type-color) | false | — | first color - any valid CSS color string or structured object |
| color2 | [String](#type-string)|[Color](#type-color) | false | — | second color |
| ratio | [Double](../reference.md#type-double) | true | — | blend ratio from 0.0 (all color1) to 1.0 (all color2); defaults to 0.5 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | format for the returned string; defaults to the detected format of `color1` (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string in the requested format, or null if either input is not a valid color

---
## ClassMethod: Colors.tetrad

### Description
Returns four colors with hues spaced 90 degrees apart (square scheme). The first element is the original color, then +90, +180, +270 degrees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | base color |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to input format |

### Returns

`[Array of String](#type-array-of-string)` — four CSS color strings

---
## ClassMethod: Colors.contrast

### Description
Returns the approximate perceptual contrast ratio between two colors, based on oklch lightness. The result is a positive number where 1.0 means no contrast and higher values indicate greater contrast. A ratio of at least 4.5 is recommended for normal text readability (WCAG AA), and 7.0 for enhanced readability (WCAG AAA).

This method uses a simplified lightness-based approximation rather than the full WCAG relative-luminance formula, but oklch lightness correlates well with perceived contrast. Returns null if either color is invalid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color1 | [String](#type-string)|[Color](#type-color) | false | — | first color |
| color2 | [String](#type-string)|[Color](#type-color) | false | — | second color |

### Returns

`[Double](../reference.md#type-double)` — approximate contrast ratio (>= 1.0), or null

---
## ClassMethod: Colors.colorScale

### Description
Generates an array of evenly-spaced colors between two endpoints. The `space` parameter controls which color space is used for interpolation - different spaces produce visibly different ramps between the same endpoints. Oklch (the default) maintains perceptual uniformity, HSL preserves saturation but can introduce unexpected hue shifts, and RGB takes a straight-line path through the RGB cube.

The `format` parameter independently controls the output string format.

Useful for data-visualization ramps, theme generation, and palette tooling.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color1 | [String](#type-string)|[Color](#type-color) | false | — | start color (any valid CSS color string or structured object) |
| color2 | [String](#type-string)|[Color](#type-color) | false | — | end color |
| steps | [int](../reference.md#type-int) | false | — | number of colors to produce (minimum 2) |
| format | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format for the returned color strings; defaults to the detected format of `color1` (hex for named colors) |
| space | [ColorFormat](../reference_2.md#type-colorformat) | true | — | color space for interpolation: "oklch" (default), "hsl", or "rgb"/"hex" (both mean linear RGB) |

### Returns

`[Array of String](#type-array-of-string)` — CSS color strings in the requested format

---
## ClassMethod: Colors.lighten

### Description
Returns a lighter version of the given color. Equivalent to `adjust(color, {lightness: amount})`.

The `amount` is a percentage (0-100) indicating how far to move toward white: 0 returns the original color, 100 returns white. Intermediate values move proportionally - `lighten(color, 20)` on a dark color produces a bigger absolute lightness change than on an already-light color, but both look like "20% lighter" perceptually.

For multi-axis adjustments (e.g. lighten and desaturate together), use [adjust()](#classmethod-colorsadjust) directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| amount | [double](../reference.md#type-double) | false | — | percentage to lighten, 0-100 |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format; defaults to the detected format of the input color (hex for named colors) |

### Returns

`[String](#type-string)` — CSS color string, or null if the input is not a valid color

### See Also

- [Colors.darken](#classmethod-colorsdarken)
- [Colors.adjust](#classmethod-colorsadjust)

---
## ClassMethod: Colors.setAlpha

### Description
Returns a new color string with the alpha (opacity) component replaced. The output format matches the input format when possible; for named colors, hex is used.

Useful for deriving semi-transparent variants of a color without converting it to a different format.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | any valid CSS color string or structured color object |
| alpha | [double](../reference.md#type-double) | false | — | new alpha value, 0.0 (transparent) to 1.0 (opaque) |
| outputFormat | [ColorFormat](../reference_2.md#type-colorformat) | true | — | optional output format; defaults to the detected format of the input color |

### Returns

`[String](#type-string)` — CSS color string with the new alpha, or null if invalid

---
## ClassMethod: Colors.equals

### Description
Returns true if two color values represent the same color (same R, G, B, and alpha), regardless of input format. For example, `"red"`, `"#ff0000"`, and `"rgb(255, 0, 0)"` are all equal.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color1 | [String](#type-string)|[Color](#type-color) | false | — | first color |
| color2 | [String](#type-string)|[Color](#type-color) | false | — | second color |

### Returns

`[Boolean](#type-boolean)` — true if the colors are identical, false otherwise, null if either invalid

---
