# Color Overview

[← Back to API Index](../reference.md)

---

## KB Topic: Color Overview

### Description
#### Color Spaces
SmartClient's [Colors](../classes/Colors.md#class-colors) class works in three color spaces, each with different strengths. All three are always available on every [Color](../reference_2.md#object-color) object - conversion is automatic.

*   **RGB** ([Color.r](../classes/Color.md#attr-colorr), [Color.g](../classes/Color.md#attr-colorg), [Color.b](../classes/Color.md#attr-colorb)) - the hardware color space. Each channel is 0-255. Best for: direct pixel-level work, matching exact hex values, and interop with legacy APIs. Poor for manipulation - "add 20 to green" is not a meaningful perceptual operation.
*   **HSL** ([Color.h](../classes/Color.md#attr-colorh), [Color.s](../classes/Color.md#attr-colors), [Color.l](../classes/Color.md#attr-colorl)) - separates hue (color), saturation (intensity), and lightness. Hue is 0-360 degrees, s and l are 0-100. Intuitive for humans but _not_ perceptually uniform - 50% lightness in yellow looks far brighter than 50% lightness in blue.
*   **oklch** ([Color.ok_L](../classes/Color.md#attr-colorok_l), [Color.ok_C](../classes/Color.md#attr-colorok_c), [Color.ok_h](../classes/Color.md#attr-colorok_h)) - a perceptually uniform color space where equal numeric steps produce equal perceived visual differences. L is 0-1 (lightness), C is ~0-0.4 (chroma/saturation), h is 0-360 (hue). Best for: color manipulation, palette generation, accessibility contrast checking. All [adjust()](../classes/Colors.md#classmethod-colorsadjust) operations work in oklch. Note that oklch hue angles differ from HSL hue angles (red is ~30 in oklch vs 0 in HSL) because oklch redistributes hues for perceptual uniformity.

#### Color Formats and Conversion
The [ColorFormat](../reference_2.md#type-colorformat) type covers four CSS string representations: `"hex"`, `"rgb"`, `"hsl"`, and `"oklch"`. Key conversion methods:

*   [Colors.getColor](../classes/Colors.md#classmethod-colorsgetcolor) - parse any color string or object into a full [Color](../reference_2.md#object-color) with all three color spaces pre-computed
*   [Colors.getString](../classes/Colors.md#classmethod-colorsgetstring) - convert to a CSS string in any format
*   [Colors.getValues](../classes/Colors.md#classmethod-colorsgetvalues) - extract raw numeric components in one color space
*   [Colors.isColor](../classes/Colors.md#classmethod-colorsiscolor) - validate without conversion
*   [Colors.getFormat](../classes/Colors.md#classmethod-colorsgetformat) - detect the format of a color string

[Colors.getColor](../classes/Colors.md#classmethod-colorsgetcolor) always returns a Color object (never null). If the input cannot be parsed, [isValid()](../classes/Color.md#method-colorisvalid) returns false and properties default to black.
#### Color Manipulation
All manipulation methods operate in oklch for perceptual uniformity and return new Color objects or CSS strings.

*   [Colors.adjust](../classes/Colors.md#classmethod-colorsadjust) - general-purpose multi-axis adjustment (lightness, saturation, hue, alpha); the foundation for all other manipulation methods
*   [Colors.lighten](../classes/Colors.md#classmethod-colorslighten) / [Colors.darken](../classes/Colors.md#classmethod-colorsdarken) - perceptual lightness (oklch L)
*   [Colors.brighten](../classes/Colors.md#classmethod-colorsbrighten) / [Colors.dim](../classes/Colors.md#classmethod-colorsdim) - combined lightness + chroma boost/cut
*   [Colors.saturate](../classes/Colors.md#classmethod-colorssaturate) / [Colors.desaturate](../classes/Colors.md#classmethod-colorsdesaturate) - chroma (oklch C)
*   [Colors.complement](../classes/Colors.md#classmethod-colorscomplement) / [Colors.spin](../classes/Colors.md#classmethod-colorsspin) - hue rotation
*   [Colors.flatten](../classes/Colors.md#classmethod-colorsflatten) - composite semi-transparent color to opaque over a background
*   [Colors.getAlpha](../classes/Colors.md#classmethod-colorsgetalpha) / [Colors.setAlpha](../classes/Colors.md#classmethod-colorssetalpha) - read or change the alpha channel

#### Inspection

*   [Colors.isDark](../classes/Colors.md#classmethod-colorsisdark) - perceptual light-vs-dark test (oklch L < 0.6)
*   [Colors.contrast](../classes/Colors.md#classmethod-colorscontrast) - approximate perceptual contrast ratio between two colors
*   [Colors.distance](../classes/Colors.md#classmethod-colorsdistance) - perceptual color difference in oklab space
*   [Colors.equals](../classes/Colors.md#classmethod-colorsequals) - same-color comparison across formats

#### CSS Color Relationships
Modern CSS supports _derived colors_ - colors defined as transformations of a base color using CSS Relative Color Syntax (RCS). For example, a skin might define a "hover highlight" as "10% lighter than the accent color": `oklch(from var(--accent) calc(l + 0.10) c h)`. When the user changes the accent color, the hover highlight updates automatically because it is defined as a _relationship_ rather than a fixed hex value.

Four methods form a pipeline for working with these color relationships:

*   [Colors.resolveCSS](../classes/Colors.md#classmethod-colorsresolvecss) - resolve any CSS color expression (including `var()` references) to a flat Color via the browser's CSS engine
*   [Colors.parseRelationship](../classes/Colors.md#classmethod-colorsparserelationship) - extract the structure of an RCS expression (origin, color space, channel deltas) without evaluating it
*   [Colors.describeRelationship](../classes/Colors.md#classmethod-colorsdescriberelationship) - given a base and derived color, compute what changed (e.g. "lightened by 0.15 in oklch")
*   [Colors.generateCSS](../classes/Colors.md#classmethod-colorsgeneratecss) - produce an oklch RCS expression from a relationship descriptor, ready for CSS output

**Typical round-trip**: a skin config stores `oklch(from var(--accent) calc(l + 0.15) c h)`. On load, `parseRelationship()` extracts the origin and deltas. The Skin Editor resolves `var(--accent)` via `resolveCSS()` to show a color swatch. If the user changes the accent, `generateCSS()` rebuilds the RCS expression with the same relationship but the new origin.

[Colors.getColor](../classes/Colors.md#classmethod-colorsgetcolor) can also resolve RCS expressions with literal color origins (hex, named colors, rgb()/hsl()/oklch() calls) in pure JavaScript - no DOM required. For expressions that reference CSS custom properties via `var()`, [Colors.resolveCSS](../classes/Colors.md#classmethod-colorsresolvecss) is needed to resolve them through the browser's CSS engine.

Channel ranges in RCS follow the native CSS scale for each color space: r/g/b are 0-255, h is degrees, s/l are 0-100 (HSL), and oklch L is 0-1, C is ~0-0.4, h is 0-360. Each channel position in the RCS expression can be a bare keyword (`r`), a `calc()` expression (`calc(r - 50)`), or a `max()`/`min()` wrapper for clamping (`max(calc(s - 80), 0)`).

#### Palette and Harmony
Methods for generating sets of related colors:

*   [Colors.colorScale](../classes/Colors.md#classmethod-colorscolorscale) - multi-step gradient between two endpoints
*   [Colors.mix](../classes/Colors.md#classmethod-colorsmix) - blend two colors at a given ratio
*   [Colors.mostReadable](../classes/Colors.md#classmethod-colorsmostreadable) - pick the highest-contrast candidate against a background
*   [Colors.triad](../classes/Colors.md#classmethod-colorstriad) / [Colors.tetrad](../classes/Colors.md#classmethod-colorstetrad) - evenly-spaced hues around the color wheel
*   [Colors.splitComplement](../classes/Colors.md#classmethod-colorssplitcomplement) - flanking the complementary hue
*   [Colors.analogous](../classes/Colors.md#classmethod-colorsanalogous) - nearby hues for harmonious palettes

All interpolation and palette methods default to oklch for perceptual uniformity.
#### Theme Generation
Higher-level methods for generating color themes from one or a few seed colors. These handle sRGB gamut mapping automatically - oklch can represent colors outside the displayable range, but all returned colors are gamut-safe.

*   [Colors.palette](../classes/Colors.md#classmethod-colorspalette) - generate a tonal ramp (dark-to-light series) from a seed color, with professional chroma curves, hue shift, and automatic gamut mapping
*   [Colors.scheme](../classes/Colors.md#classmethod-colorsscheme) - generate harmonious seed colors from one primary (e.g. split-complementary, triadic), with chroma subordination for visual hierarchy
*   [Colors.autoContrast](../classes/Colors.md#classmethod-colorsautocontrast) - find a WCAG-compliant text color for any background, with optional hue tinting for a polished look

Typical workflow: `scheme()` picks harmonious seed colors, then `palette()` generates a tonal ramp for each seed.

### Related

- [Colors.autoContrast](../classes/Colors.md#classmethod-colorsautocontrast)
- [Colors.palette](../classes/Colors.md#classmethod-colorspalette)
- [Colors.scheme](../classes/Colors.md#classmethod-colorsscheme)
- [Colors.resolveCSS](../classes/Colors.md#classmethod-colorsresolvecss)
- [Colors.parseRelationship](../classes/Colors.md#classmethod-colorsparserelationship)
- [Colors.describeRelationship](../classes/Colors.md#classmethod-colorsdescriberelationship)
- [Colors.generateCSS](../classes/Colors.md#classmethod-colorsgeneratecss)

---
