# Colors Documentation

[← Back to API Index](../reference.md)

---

## Class: Colors

### Description
Utility class for color format conversion, validation, and manipulation. Accepts any valid CSS color specification (hex, rgb/rgba, hsl/hsla, oklch, named colors, "transparent") and converts between formats. See the [Color Overview](../kb_topics/colorOverview.md#kb-topic-color-overview) for a detailed guide to color spaces, formats, manipulation, CSS color relationships, and palettes.

The core entry points are [getColor()](#classmethod-colorsgetcolor) to parse any color into a [Color](../reference_2.md#object-color) object (with RGB, HSL, and oklch properties pre-computed), [getString()](#classmethod-colorsgetstring) to convert back to a CSS string, and [getValues()](#classmethod-colorsgetvalues) for raw numeric components in a single color space. [adjust()](#classmethod-colorsadjust) is the general-purpose manipulation method - all convenience methods like [lighten()](#classmethod-colorslighten), [saturate()](#classmethod-colorssaturate), etc. delegate to it.

See the [Color Overview](../kb_topics/colorOverview.md#kb-topic-color-overview) for a full guide organized by topic: [conversion](#classmethod-colorsgetcolor), [inspection](#classmethod-colorsisdark), [manipulation](#classmethod-colorsadjust) (including [alpha compositing](#classmethod-colorsflatten)), [palettes](#classmethod-colorscolorscale) and [harmony](#classmethod-colorstriad), [theme generation](#classmethod-colorspalette), and [CSS color relationships](#classmethod-colorsresolvecss).

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
## ClassMethod: Colors.resolveCSS

### Description
Resolves any CSS color expression to a flat [Color](../reference_2.md#object-color) by evaluating it through the browser's CSS engine. Handles `var()` references, `color-mix()`, and any other CSS color constructs supported by the current browser.

[Colors.getColor](#classmethod-colorsgetcolor) automatically delegates to this method for expressions containing `var()` or `color-mix()`, so most callers never need to call `resolveCSS()` directly. The main reason to use it explicitly is when you need to pass an `element` context for inherited CSS custom properties:

```
     // getColor() handles var() automatically:
     var c = isc.Colors.getColor("var(--isc-button-hover)");

     // Use resolveCSS() when you need element-scoped custom properties:
     var c = isc.Colors.resolveCSS("var(--panel-bg)", someElement);
 
```

Internally, a scratch DOM element's `color` style is set to the expression and `getComputedStyle()` reads back the browser-resolved value. If an `element` is provided, the scratch element is temporarily appended as its child, allowing inherited CSS custom properties to resolve correctly.

Returns an invalid Color (with [isValid()](Color.md#method-colorisvalid) false) if the expression is not a valid CSS color in the current browser, or if no DOM is available (e.g. server-side).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| expr | [String](#type-string) | false | — | any CSS color expression - hex, rgb(), hsl(), oklch(), color-mix(), var() references, RCS expressions, or any combination the browser supports |
| element | [Element](#type-element) | true | — | optional DOM element to use as the resolution context; if provided, CSS custom properties inherited by this element will be available for `var()` resolution |

### Returns

`[Color](#type-color)` — resolved Color object, or an invalid Color if the expression could not be resolved

### Groups

- colorOverview

### See Also

- [Colors.getColor](#classmethod-colorsgetcolor)
- [Colors.parseRelationship](#classmethod-colorsparserelationship)

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
## ClassMethod: Colors.parseRelationship

### Description
Extracts structural information from a CSS Relative Color Syntax (RCS) expression - the origin reference, color space, and per-channel modifications - without evaluating it. This is pure string parsing: no DOM access and no color resolution. It works with any origin, including `var()` references (which [Colors.getColor](#classmethod-colorsgetcolor) would resolve via the DOM - parseRelationship preserves the raw reference for structural inspection).

For example, a skin config stores `oklch(from var(--isc-accent) calc(l + 0.15) c h)` for a hover color. `parseRelationship()` extracts the structure so you can see what is being derived from what, without needing to resolve the colors:

```
     var rcs = "oklch(from var(--isc-accent) calc(l + 0.15) c h)";
     var info = isc.Colors.parseRelationship(rcs);
     info.origin      // "var(--isc-accent)" - the base color reference
     info.space        // "oklch"
     info.deltas       // { l: 0.15 } - 15% lighter, chroma and hue unchanged
     info.rawChannels  // ["calc(l + 0.15)", "c", "h"]

     // To actually see the resolved color, use resolveCSS() on the origin:
     var baseColor = isc.Colors.resolveCSS(info.origin);
 
```

The returned object describes the expression's structure:

*   **origin** - the raw origin string as it appears in the expression (e.g. `"var(--isc-accent)"`, `"#ff0000"`). If the origin is a `var()` reference, the caller must use [Colors.resolveCSS](#classmethod-colorsresolvecss) to resolve it to an actual color - [Colors.getColor](#classmethod-colorsgetcolor) cannot resolve `var()` references.
*   **space** - the color space: `"rgb"`, `"hsl"`, or `"oklch"`
*   **deltas** - an object mapping channel names to their additive delta (only channels that differ from identity). For example, `{l: 0.15}` means lightness is shifted by +0.15 while other channels pass through unchanged. Channels with complex expressions (multiplication, clamping via max/min) are omitted from deltas but present in rawChannels.
*   **rawChannels** - an array of three raw channel expression strings in CSS order, useful for complex expressions that cannot be reduced to a simple delta
*   **alpha** - the alpha value (1.0 if not specified)

Returns null if the expression is not valid RCS syntax (plain hex, rgb(), named colors, and `color-mix()` are not RCS and will return null).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rcsExpr | [String](#type-string) | false | — | a CSS RCS expression, e.g. `"oklch(from var(--x) calc(l + 0.15) c h)"` |

### Returns

`[Object](../reference.md#type-object)` — structured descriptor, or null if not valid RCS

### Groups

- colorOverview

### See Also

- [Colors.resolveCSS](#classmethod-colorsresolvecss)
- [Colors.generateCSS](#classmethod-colorsgeneratecss)

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
Returns true if the given value is a valid CSS color specification. Accepts any format: hex (#RGB, #RRGGBB, #RRGGBBAA), rgb(), rgba(), hsl(), hsla(), oklch(), named colors, "transparent", CSS Relative Color Syntax expressions, and `var()` or `color-mix()` expressions (resolved via the browser's CSS engine when a DOM is available; returns false server-side).

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
## ClassMethod: Colors.generateCSS

### Description
Converts an oklch relationship descriptor (as returned by [Colors.describeRelationship](#classmethod-colorsdescriberelationship) or [Colors.parseRelationship](#classmethod-colorsparserelationship)) into a CSS Relative Color Syntax expression. The generated expression uses oklch as the color space, ensuring perceptually uniform transforms.

For example, to define a hover color that is always 10% lighter than the theme's accent, regardless of what the accent color actually is:

```
     // "Make it 10% lighter" expressed as oklch RCS:
     var css = isc.Colors.generateCSS("var(--accent)", { L: 0.10 });
     // "oklch(from var(--accent) calc(l + 0.1) c h)"
     // This can go directly into a CSS stylesheet or skin config.

     // Analyze an existing pair of colors, then re-express the same
     // relationship against a different base:
     var rel = isc.Colors.describeRelationship("#3B82F6", "#6BA3F8");
     var css2 = isc.Colors.generateCSS("var(--new-accent)", rel);
 
```

The `origin` parameter is the CSS expression to use as the RCS origin - typically a `var()` reference like `"var(--isc-accent)"`, but can also be a literal color like `"#3B82F6"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| origin | [String](#type-string) | false | — | the CSS origin expression for the RCS - typically a `var()` reference or a literal color |
| relationship | [Object](../reference.md#type-object) | false | — | an object with oklch deltas: `L` (lightness), `C` (chroma), and/or `h` (hue). Properties that are zero, null, or omitted produce identity channel passes. Accepts the output of both [Colors.describeRelationship](#classmethod-colorsdescriberelationship) and [Colors.parseRelationship](#classmethod-colorsparserelationship) |

### Returns

`[String](#type-string)` — a CSS oklch RCS expression

### Groups

- colorOverview

### See Also

- [Colors.describeRelationship](#classmethod-colorsdescriberelationship)
- [Colors.parseRelationship](#classmethod-colorsparserelationship)
- [Colors.resolveCSS](#classmethod-colorsresolvecss)

---
## ClassMethod: Colors.getColor

### Description
Parses any valid CSS color into a structured [Color](../reference_2.md#object-color) object with RGB, HSL, and oklch properties pre-computed, plus convenience methods for manipulation.

Accepts any CSS color string (`#hex`, `rgb()`, `hsl()`, `oklch()`, named colors) or a structured component object in any supported color space: `{r, g, b}`, `{h, s, l}`, or `{L, C, h}`.

Also accepts CSS Relative Color Syntax (RCS) expressions with literal color origins, such as `rgb(from #3B82F6 calc(r - 0.1) g b)`, `hsl(from #47a7e3 h s calc(l + 20))`, or `oklch(from #3B82F6 calc(l + 0.15) c h)`. The origin can be any parseable color string - hex, named, or a nested function call. Channel keywords use CSS-native ranges: RGB channels are 0-1 sRGB fractions (not 0-255), HSL s/l are 0-100, oklch L is 0-1. The origin is resolved, the channel adjustments (bare keywords, `calc()`, `max()`, `min()`) are evaluated, and the result is returned as a fully resolved Color.

Also accepts manipulation function-strings such as `lighten(#3B82F6, 20)`, `darken(blue, 15%)`, `saturate(#abc, 30)`, or `complement(red)`. Supported function names: `lighten`, `darken`, `brighten`, `dim`, `saturate`, `desaturate`, `complement`, `spin`. The color argument can be any parseable color string; the amount is a number (optionally suffixed with "%"). `complement()` takes only a color argument. These are equivalent to calling the corresponding [Colors](#class-colors) class method, but expressed as a single string - useful when color expressions come from user input, configuration files, or declarative settings.

Expressions containing `var()` references or `color-mix()` are automatically resolved through the browser's CSS engine (via [Colors.resolveCSS](#classmethod-colorsresolvecss)). This requires DOM access - on the server, such expressions return an invalid Color.

Always returns a [Color](../reference_2.md#object-color) object. If the input cannot be parsed, the returned object will have [isValid()](Color.md#method-colorisvalid) returning false (properties default to black). If the input is already a [Color](../reference_2.md#object-color), a new Color with the same values is returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color)|[Object](../reference.md#type-object) | false | — | any valid CSS color string, an existing [Color](../reference_2.md#object-color) (copied), or a structured object with {r,g,b}, {h,s,l}, or {L,C,h} keys |

### Returns

`[Color](#type-color)` — a Color object - check [isValid()](Color.md#method-colorisvalid) for parse success

---
## ClassMethod: Colors.autoContrast

### Description
Returns a text color that meets a target contrast ratio against the given background. Useful for ensuring readability - given any background color, this method finds a foreground color that passes WCAG accessibility guidelines.

By default, tries white first (preferred for dark backgrounds) and falls back to black. When `tint` is true, the result is lightly tinted toward the background's hue for a more polished look, while still meeting the contrast target.

```
     // What text color is readable on this background?
     var textColor = isc.Colors.autoContrast("#3B82F6");
     // "#ffffff" (white has sufficient contrast against medium blue)

     var textColor2 = isc.Colors.autoContrast("#B0D4FF");
     // "#1a1a1a" or similar dark color (white lacks contrast on light blue)

     // Tinted: text picks up a hint of the background hue
     var tinted = isc.Colors.autoContrast("#3B82F6", { tint: true });
     // a very light blue-white instead of pure white
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| background | [String](#type-string)|[Color](#type-color) | false | — | the background color to find a readable text color for |
| options | [Object](../reference.md#type-object) | true | — | optional settings:

*   `target` - minimum contrast ratio (default 4.5 for WCAG AA; use 7.0 for WCAG AAA)
*   `prefer` - `"white"` (default) or `"black"`; which extreme to try first
*   `tint` - if true, lightly tint the result toward the background's hue (default false) |

### Returns

`[Color](#type-color)` — a Color meeting the contrast target, or the best available if the target cannot be met

### Groups

- colorOverview

### See Also

- [Colors.contrast](#classmethod-colorscontrast)
- [Colors.mostReadable](#classmethod-colorsmostreadable)

---
## ClassMethod: Colors.describeRelationship

### Description
Computes the perceptual relationship between two colors in oklch space and returns a structured description. This is the analytical inverse of color manipulation: given a base and a derived color, it tells you what oklch adjustments were applied.

For example, a skin has an accent color `#3B82F6` and a hand-picked hover color `#6BA3F8`. To find out what the relationship actually is (so it can be expressed as a formula rather than a second hard-coded hex value):

```
     var rel = isc.Colors.describeRelationship("#3B82F6", "#6BA3F8");
     rel.type  // "lighten" - the hover is essentially just lighter
     rel.L     // 0.07 (oklch lightness increased by ~7%)
     rel.C     // ~0 (chroma barely changed)
     rel.h     // ~0 (hue barely changed)

     // Now generate a CSS expression that captures this relationship:
     var css = isc.Colors.generateCSS("var(--accent)", rel);
     // "oklch(from var(--accent) calc(l + 0.07) c h)"
 
```

The returned object contains:

*   **type** - a simplified classification: `"lighten"`, `"darken"`, `"saturate"`, `"desaturate"`, `"spin"`, `"adjust"` (multiple significant changes), or `"identical"`
*   **L** - oklch lightness delta (positive = lighter, 0-1 scale)
*   **C** - oklch chroma delta (positive = more saturated)
*   **h** - oklch hue delta in degrees (shortest-arc rotation, -180 to +180)

The type classification uses perceptual thresholds: L changes > 0.01, C changes > 0.005, and hue changes > 2 degrees are considered significant. When exactly one dimension changes significantly, the type reflects that dimension. When multiple dimensions change, the type is `"adjust"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| baseColor | [String](#type-string)|[Color](#type-color) | false | — | the origin/base color |
| derivedColor | [String](#type-string)|[Color](#type-color) | false | — | the derived/transformed color |

### Returns

`[Object](../reference.md#type-object)` — relationship descriptor with type, L, C, h properties

### Groups

- colorOverview

### See Also

- [Colors.generateCSS](#classmethod-colorsgeneratecss)
- [Colors.parseRelationship](#classmethod-colorsparserelationship)

---
## ClassMethod: Colors.palette

### Description
Generates a tonal ramp - an ordered series of colors at different lightness levels sharing the same hue. In color theory, lighter variants of a color are called _tints_ (mixed toward white) and darker variants are called _shades_ (mixed toward black); this method produces both in a single ramp. This is the core operation for theme generation: one brand color in, a full light-to-dark palette out.

At its simplest, `palette("#3366CC", 7)` produces 7 stops from dark to light - usable directly as skin backgrounds, hover fills, text colors, and borders. With no options, it uses sensible defaults: a natural chroma curve (vivid in the mid-range, muted at extremes) and a subtle hue shift for a professional, non-flat appearance.

For a plain lightness scale with no chroma or hue variation, pass `{ chromaCurve: "constant", hueShift: 0 }`.

```
     // Simple: 7-stop ramp from a brand color (most common use)
     var ramp = isc.Colors.palette("#3366CC", 7);
     ramp[0].hex  // dark shade  - text, borders
     ramp[3].hex  // mid-tone    - near the seed color
     ramp[6].hex  // light tint  - backgrounds, hover fills

     // Plain lightness scale (no chroma curve or hue shift):
     var plain = isc.Colors.palette("#3366CC", 7, {
         chromaCurve: "constant", hueShift: 0
     });

     // Tints only (light backgrounds, subtle fills):
     var tints = isc.Colors.palette("#3366CC", 5, {
         lightnessRange: [0.70, 0.97]
     });

     // Shades only (text, borders, shadows):
     var shades = isc.Colors.palette("#3366CC", 5, {
         lightnessRange: [0.15, 0.45]
     });
 
```

All returned colors are guaranteed to be within the sRGB gamut (via automatic chroma reduction at the extremes). The seed color's own lightness determines where in the ramp it falls - it is not forced to a specific stop index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | the seed color whose hue and chroma define the palette |
| steps | [int](../reference.md#type-int) | true | — | number of stops to generate (default 11) |
| options | [Object](../reference.md#type-object) | true | — | optional settings:

*   `lightnessRange` - two-element array of oklch L values for the darkest and lightest stops (default `[0.15, 0.97]`)
*   `chromaCurve` - `"natural"` (default) tapers chroma toward extremes using a cosine curve; `"constant"` uses the seed's chroma for all stops; `"peaked"` pushes maximum chroma to a configurable lightness
*   `hueShift` - degrees of hue rotation across the full lightness range (default ~4; set to 0 to disable). Positive values shift lighter stops toward warmer hues. |

### Returns

`[Array of Color](#type-array-of-color)` — array of Color objects ordered from darkest to lightest

### Groups

- colorOverview

### See Also

- [Colors.scheme](#classmethod-colorsscheme)
- [Colors.colorScale](#classmethod-colorscolorscale)
- [Colors.autoContrast](#classmethod-colorsautocontrast)

---
## ClassMethod: Colors.adjust

### Description
The general-purpose method for deriving a related color from a base color. Accepts any combination of adjustment keys in the `deltas` object and returns the result as a CSS color string. Single-axis convenience wrappers - [lighten()](#classmethod-colorslighten), [darken()](#classmethod-colorsdarken), [saturate()](#classmethod-colorssaturate), [desaturate()](#classmethod-colorsdesaturate), and [complement()](#classmethod-colorscomplement) - all delegate to this method.

**Friendly percentage keys** (recommended for most uses):

*   **lightness** (-100 to 100): positive values lighten (toward white), negative darken (toward black). See [Colors.lighten](#classmethod-colorslighten)/[darken](#classmethod-colorsdarken).
*   **saturation** (-100 to 100): positive values intensify color, negative desaturate toward gray. See [Colors.saturate](#classmethod-colorssaturate)/[desaturate](#classmethod-colorsdesaturate).
*   **hue** (degrees): signed rotation around the color wheel. See [complement()](#classmethod-colorscomplement) for the hue wheel reference.
*   **alpha**: signed delta to opacity (0 = transparent, 1 = opaque).

**RGB delta keys** (for direct channel control):

*   **red**: signed delta to the red channel (0-255).
*   **green**: signed delta to the green channel (0-255).
*   **blue**: signed delta to the blue channel (0-255).

RGB deltas are applied first (in RGB space, clamped to 0-255), before any oklch adjustments. This allows combining RGB shifts with perceptual adjustments in a single call, e.g. `{red: 20, lightness: 10}`.

**Raw oklch keys** (for fine-grained control - see the [oklch color space](https://oklch.com/)):

*   **L**: signed delta to lightness (0-1). +0.1 is noticeably lighter.
*   **C**: signed delta to chroma (0 = gray, max ~0.4). -0.05 desaturates subtly.
*   **h** and **alpha** work the same as the friendly keys above.

All key groups may be mixed freely; RGB deltas are applied first, then friendly percentage keys, then raw oklch keys. The output format defaults to the input format, so `rgb(...)` input returns `rgb(...)` output, etc.

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
| deltas | [Object](../reference.md#type-object) | false | — | adjustment keys - any combination of RGB keys (`red`, `green`, `blue`), friendly keys (`lightness`, `saturation`, `hue`, `alpha`), and/or raw oklch keys (`L`, `C`, `h`). See the key lists above. |
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
## ClassMethod: Colors.scheme

### Description
Generates a set of harmonious seed colors from a single primary. Unlike the lower-level harmony methods ([Colors.triad](#classmethod-colorstriad), [Colors.tetrad](#classmethod-colorstetrad), etc.) which return raw CSS strings at fixed hue rotations, `scheme()` returns a structured object with semantic key names and applies chroma/lightness adjustments so that secondary and tertiary colors feel subordinate to the primary - a requirement for professional UI themes.

The returned object always contains a `primary` Color plus one or more supporting keys depending on the scheme type. It also includes auto-generated `neutral` (very low chroma at the primary's hue) and `error` (red variant) keys. Each seed can be passed to [Colors.palette](#classmethod-colorspalette) to generate a full tonal ramp.

```
     // Generate a split-complementary scheme from a brand blue:
     var s = isc.Colors.scheme("#3B82F6", "split-complementary");
     // s.primary   -> the original blue
     // s.secondary -> a warm orange-ish complement (subdued chroma)
     // s.tertiary  -> a cool red-violet complement (subdued chroma)
     // s.neutral   -> desaturated blue-gray
     // s.error     -> muted red

     // Generate a tonal ramp for each seed:
     var primaryRamp = isc.Colors.palette(s.primary, 11);
     var neutralRamp = isc.Colors.palette(s.neutral, 11);
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color) | false | — | the primary seed color |
| type | [String](#type-string) | true | — | scheme type: `"complementary"`, `"analogous"`, `"triadic"`, `"split-complementary"` (default), `"tetradic"`, or `"monochromatic"` |

### Returns

`[Object](../reference.md#type-object)` — a map with `primary`, `secondary`, `tertiary` (where applicable), `neutral`, and `error` keys, each a [Color](../reference_2.md#object-color) object

### Groups

- colorOverview

### See Also

- [Colors.palette](#classmethod-colorspalette)
- [Colors.autoContrast](#classmethod-colorsautocontrast)

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
