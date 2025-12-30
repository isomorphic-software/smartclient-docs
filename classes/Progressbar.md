# Progressbar Documentation

[← Back to API Index](../reference.md)

---

## Class: Progressbar

*Inherits from:* [StretchImg](StretchImg.md#class-stretchimg)

### Description
The Progressbar widget class extends the StretchImg class to implement image-based progress bars (graphical bars whose lengths represent percentages, typically of task completion).

---
## Attr: Progressbar.percentDone

### Description
Number from 0 to 100, inclusive, for the percentage to be displayed graphically in this progressbar.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Progressbar.useCssStyles

### Description
When set to true, styles the Progressbar via the [base](#attr-progressbarbasestyle) and [progress](#attr-progressbarprogressstyle) CSS styles.

**Flags**: IR

---
## Attr: Progressbar.src

### Description
The base file name for the progressbar image.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Progressbar.vertical

### Description
Indicates whether this is a vertical or horizontal progressbar.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Progressbar.breadth

### Description
Thickness of the progressbar in pixels. This is effectively width for a vertical progressbar, or height for a horizontal progressbar.

This property must be set instead of setting `width` or `height`.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Progressbar.progressStyle

### Description
[Base style](StatefulCanvas.md#attr-statefulcanvasbasestyle) used to style the percentage-done portion of this Progressbar. Only used when [useCssStyles](#attr-progressbarusecssstyles) is true.

**Flags**: IR

---
## Attr: Progressbar.length

### Description
Length of the progressbar in pixels. This is effectively height for a vertical progressbar, or width for a horizontal progressbar.

This property must be set instead of setting `width` or `height`.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Progressbar.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Progressbar.baseStyle

### Description
[Base style](StatefulCanvas.md#attr-statefulcanvasbasestyle) for this Progressbar. Only used when [useCssStyles](#attr-progressbarusecssstyles) is true.

**Flags**: IR

---
## Method: Progressbar.percentChanged

### Description
This method is called when the percentDone value changes. Observe this method to be notified upon a change to the percentDone value.

### See Also

- [Class.observe](Class.md#method-classobserve)

**Flags**: A

---
## Method: Progressbar.getLength

### Description
Returns the current width of a horizontal progressbar, or height of a vertical progressbar.

### Returns

`[Number](#type-number)` — the length of the progressbar

---
## Method: Progressbar.setBreadth

### Description
Sets the breadth of the progressbar to newLength. This is the height of a horizontal progressbar, or the width of a vertical progressbar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newBreadth | [number](#type-number) | false | — | the new breadth of the progressbar |

---
## Method: Progressbar.setLength

### Description
Sets the length of the progressbar to newLength. This is the width of a horizontal progressbar, or the height of a vertical progressbar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newLength | [Number](#type-number) | false | — | the new length of the progressbar |

---
## Method: Progressbar.getBreadth

### Description
Returns the current height of a horizontal progressbar, or width of a vertical progressbar.

### Returns

`[number](#type-number)` — the breadth of the progressbar

---
## Method: Progressbar.setPercentDone

### Description
Sets percentDone to newPercent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPercent | [number](#type-number) | false | — | percent to show as done (0-100) |

---
