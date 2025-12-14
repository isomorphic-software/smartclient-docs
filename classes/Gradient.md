# Gradient Documentation

[← Back to API Index](../reference.md)

---

## Attr: Gradient.colorStops

### Description
An array of color stops for this gradient.

**Flags**: IR

---
## Attr: Gradient.startColor

### Description
A start color for the gradient. If both startColor and [endColor](#attr-gradientendcolor) are set then [colorStops](#attr-gradientcolorstops) is ignored.

**Flags**: IR

---
## Attr: Gradient.id

### Description
Identifier which can be used by one or more DrawItems when gradient is assigned to [DrawPane.gradients](DrawPane.md#attr-drawpanegradients). The ID property is optional when gradient is assigned directly to a DrawItem.

The ID must be unique within DrawPane.gradients if defined.

**Flags**: IR

---
## Attr: Gradient.endColor

### Description
An end color for the gradient. If both [startColor](#attr-gradientstartcolor) and endColor are set then [colorStops](#attr-gradientcolorstops) is ignored.

**Flags**: IR

---
## Attr: Gradient.direction

### Description
For a [SimpleGradient](../reference.md#object-simplegradient), the angle of the direction vector in degrees. The default of 0.0 causes the gradient to sweep from the start color on the left to the end color on the right. Positive direction angles correspond to clockwise rotations of the default gradient.

This property is only applicable when using [Gradient.startColor](#attr-gradientstartcolor) and [Gradient.endColor](#attr-gradientendcolor) (not [Gradient.colorStops](#attr-gradientcolorstops)).

**Flags**: IR

---
