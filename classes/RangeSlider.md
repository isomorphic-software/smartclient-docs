# RangeSlider Documentation

[← Back to API Index](../reference.md)

---

## Class: RangeSlider

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
A "double slider" allowing the user to select a range via two draggable thumbs.

---
## Attr: RangeSlider.vertical

### Description
Whether the rangeSlider should be vertical or horizontal. Default is horizontal.

**Flags**: IR

---
## Attr: RangeSlider.minValue

### Description
Set the minimum value (left/top of slider).

**Flags**: IRW

---
## Attr: RangeSlider.track

### Description
Optional track of the RangeSlider. Set `showTrack` false to avoid showing a track so the RangeSlider can be superimposed over something else.

**Flags**: IR

---
## Attr: RangeSlider.baseStyle

### Description
Base style name for CSS styles applied to the background of the rangeSlider. The following suffixes are applied for different areas of the slider:

*   "Start": area of the slider before the startThumb
*   "Selected": area of the slider between the thumbs (the selected range)
*   "End": area of the slider after the endThumb

.. and the following suffixes are applied in addition according to the slider's dynamic state:

*   "Over": if the mouse is over the segment
*   "Down": if the mouse is down on the segment

For example, if the mouse is down in the area before the start thumb, that area will have the CSS style "rangeSliderStartDown".

**Flags**: IR

---
## Attr: RangeSlider.startValue

### Description
The beginning of the selected range.

**Flags**: IRW

---
## Attr: RangeSlider.endThumb

### Description
Thumb for the end of the range

**Flags**: IR

---
## Attr: RangeSlider.startThumb

### Description
Thumb for the start of the range.

**Flags**: IR

---
## Attr: RangeSlider.scrollbar

### Description
Optional Scrollbar shown as a second way of adjusting the range.

**Flags**: IR

---
## Attr: RangeSlider.endValue

### Description
The end of the selected range.

**Flags**: IRW

---
## Attr: RangeSlider.maxValue

### Description
Set the maximum value (right/bottom of slider).

**Flags**: IRW

---
## Method: RangeSlider.changed

### Description
Notification fired when the selected range is changed by the end user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startValue | [float](../reference.md#type-float) | false | — | new start value |
| endValue | [float](../reference.md#type-float) | false | — | new end value |
| isDragging | [boolean](../reference.md#type-boolean) | false | — | whether the user is still in the middle of a drag, so that expensive operations can be avoided if needed |

---
