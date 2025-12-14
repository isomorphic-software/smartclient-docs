# Slider Documentation

[← Back to API Index](../reference.md)

---

## Class: Slider

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
The Slider class implements a GUI slider widget allowing the user to select a numeric value from within a range by dragging a visual indicator up and down a track.

The slider will generate events as the user interacts with it and changes its value. If slider.sliderTarget is specified, moving the slider thumb generates a custom event named 'sliderMove', sent to the sliderTarget. If a `sliderMove` handler stringMethod is defined on the target, it will be fired when the slider is moved. The second parameter (available via the variable name `eventInfo` if the handler is a string) is a pointer back to the slider.

The slider will also fire a `valueChanged()` method whenever its value is changed. This can be observed or overridden on the Slider instance to perform some action.

---
## Attr: Slider.flipValues

### Description
Specifies whether the value range of the slider should be flipped so that values increase as the thumb is moved down (for a [vertical](#attr-slidervertical) slider) or to the left (for a horizontal slider).

**Flags**: IRW

---
## Attr: Slider.valueStyle

### Description
CSS style for the floating [valueLabel](#attr-slidervaluelabel), visible when [Slider.showValue](#attr-slidershowvalue) is true.

**Flags**: IR

---
## Attr: Slider.minValue

### Description
The minimum slider value. The slider value is equal to minValue when the thumb is at the bottom or left of the slider (unless flipValues is true, in which case the minimum value is at the top/right of the slider)

### See Also

- [Slider.flipValues](#attr-sliderflipvalues)

**Flags**: IRW

---
## Attr: Slider.rangeFormat

### Description
[FormatString](../reference.md#type-formatstring) for numeric formatting of the range labels. If unset, defaults to [Slider.valueFormat](#attr-slidervalueformat)

### Groups

- appearance

**Flags**: IR

---
## Attr: Slider.labelWidth

### Description
The width of the labels used to display the minimum, maximum and current values of the slider.

**Flags**: IRW

---
## Attr: Slider.titleSpacing

### Description
The space between the [title](#attr-slidershowtitle) and the track.

**Flags**: IRW

---
## Attr: Slider.showTitle

### Description
Indicates whether the slider's [title](#attr-slidertitle) should be displayed. The default position for the title-label is to the left of a horizontal slider, or above a [vertical](#attr-slidervertical) slider.

### See Also

- [Slider.title](#attr-slidertitle)

**Flags**: IRW

---
## Attr: Slider.hTrackStyle

### Description
Optional CSS style for the track for a [horizontally oriented](#attr-slidervertical) slider.

Will have the suffix "Disabled" added when the slider is disabled.

**Flags**: IR

---
## Attr: Slider.vertical

### Description
Indicates whether this is a vertical or horizontal slider.

**Flags**: IRW

---
## Attr: Slider.valueTextStyle

### Description
CSS style for the text in the floating [valueLabel](#attr-slidervaluelabel), visible when [showValue](#attr-slidershowvalue) is true.

**Flags**: IR

---
## Attr: Slider.rangeStyle

### Description
CSS style for the [min and max](#attr-sliderrangelabel) range-labels, when [showRange](#attr-slidershowrange) is true.

**Flags**: IR

---
## Attr: Slider.vTrackStyle

### Description
Optional CSS style for the track for a [vertically oriented](#attr-slidervertical) slider.

Will have the suffix "Disabled" added when the slider is disabled.

**Flags**: IR

---
## Attr: Slider.activeTrackStyle

### Description
CSS style used to highlight the [active](#attr-slidershowactivetrack) part of the slider track.

Will have the suffix "Disabled" added when the slider is disabled.

**Flags**: IR

---
## Attr: Slider.vLabelSpacing

### Description
The space around the labels used to display the [minimum, maximum](#attr-sliderrangelabel) and [current](#attr-slidervaluelabel) values of the slider, when [vertical](#attr-slidervertical) is true. If unset, defaults to [Slider.labelSpacing](#attr-sliderlabelspacing).

**Flags**: IRW

---
## Attr: Slider.rangeLabel

### Description
Used to create both of the min and max range-labels, via the [AutoChild](../reference.md#type-autochild) pattern, hence `rangeLabelConstructor`, `rangeLabelDefaults` and `rangeLabelProperties` are valid.

**Flags**: IR

---
## Attr: Slider.animateThumbInit

### Description
If thumb animation is enabled, should the thumb be animated to its initial value?

### Groups

- animation

**Flags**: IRW

---
## Attr: Slider.length

### Description
Used to set slider height if vertical, slider width if horizontal. Applied to the slider track, not necessarily the entire widget. Overridden by an explicit width/height specification for the widget.

**Flags**: IRW

---
## Attr: Slider.activeTrack

### Description
A styled canvas used to highlight the [active](#attr-slidershowactivetrack) part of the slider track.

**Flags**: IR

---
## Attr: Slider.vValueStyle

### Description
Optional CSS style for the floating [valueLabel](#attr-slidervaluelabel), visible when [Slider.showValue](#attr-slidershowvalue) is true and [vertical](#attr-slidervertical) is true.

**Flags**: IR

---
## Attr: Slider.stepPercent

### Description
The percentage of the total slider that constitutes one discrete step. The slider will move one step when the appropriate arrow key is pressed.

**Flags**: IRW

---
## Attr: Slider.canFocus

### Description
Indicates whether keyboard manipulation of the slider is allowed.

**Flags**: IRW

---
## Attr: Slider.labelSpacing

### Description
The space around the labels used to display the [minimum, maximum](#attr-sliderrangelabel) and [current](#attr-slidervaluelabel) values of the slider.

**Flags**: IRW

---
## Attr: Slider.trackWidth

### Description
The thickness of the track. This is the width, for a [vertical](#attr-slidervertical) slider, or the height, for a horizontal slider.

**Flags**: IRW

---
## Attr: Slider.hThumbStyle

### Description
Optional CSS style for the thumb for a [horizontally oriented](#attr-slidervertical) slider.

Will have the suffix "down" added when the mouse is down on the thumb, and "Disabled" added when the slider is disabled.

**Flags**: IR

---
## Attr: Slider.showActiveTrack

### Description
Whether to show the [activeTrack](#attr-slideractivetrack), which highlights the 'active' portion of a slider, from its minimum to its current [value](#attr-slidervalue).

**Flags**: IR

---
## Attr: Slider.numValues

### Description
The number of discrete values represented by slider. If specified, the range of valid values (between `minValue` and `maxValue`) will be divided into this many steps. As the thumb is moved along the track it will only select these values and appear to jump between the steps.

**Flags**: IRW

---
## Attr: Slider.animateThumb

### Description
Should the thumb be animated to its new position when the value is changed programmatically, or by clicking in the slider track.

### Groups

- animation

**Flags**: IRW

---
## Attr: Slider.value

### Description
The slider value. This value should lie between the minValue and maxValue and increases as the thumb is moved up (for a vertical slider) or right (for a horizontal slider) unless flipValues is set to true.

### See Also

- [Slider.minValue](#attr-sliderminvalue)
- [Slider.maxValue](#attr-slidermaxvalue)
- [Slider.flipValues](#attr-sliderflipvalues)
- [Slider.showValue](#attr-slidershowvalue)

**Flags**: IRW

---
## Attr: Slider.trackImageType

### Description
The imageType setting for the slider track.

### See Also

- [ImageStyle](../reference.md#type-imagestyle)
- [StretchImg.imageType](StretchImg.md#attr-stretchimgimagetype)

**Flags**: IRW

---
## Attr: Slider.showValue

### Description
Indicates whether a [label](#attr-slidervaluelabel) for the value of the slider should be displayed. The default position for this label is to the right of a [vertical](#attr-slidervertical) slider, or below a horizontal slider.

### See Also

- [Slider.value](#attr-slidervalue)

**Flags**: IRW

---
## Attr: Slider.hValueStyle

### Description
Optional CSS style for the floating [valueLabel](#attr-slidervaluelabel), visible when [Slider.showValue](#attr-slidershowvalue) is true and [vertical](#attr-slidervertical) is false.

**Flags**: IR

---
## Attr: Slider.showRange

### Description
Indicates whether labels for the [min and max values](#attr-sliderrangelabel) of the slider should be displayed. The default positions for these labels are below the start/end of a horizontal slider, or to the right of the start/end of a [vertical](#attr-slidervertical) slider.

### See Also

- [Slider.minValueLabel](#attr-sliderminvaluelabel)
- [Slider.maxValueLabel](#attr-slidermaxvaluelabel)

**Flags**: IRW

---
## Attr: Slider.valueFormat

### Description
[FormatString](../reference.md#type-formatstring) for numeric formatting of the value and range labels.

### Groups

- appearance

**Flags**: IR

---
## Attr: Slider.maxValue

### Description
The maximum slider value. The slider value is equal to maxValue when the thumb is at the top or right of the slider (unless flipValues is true, in which case the maximum value is at the bottom/left of the slider)

### See Also

- [Slider.flipValues](#attr-sliderflipvalues)

**Flags**: IRW

---
## Attr: Slider.valueLabel

### Description
[AutoChild](../reference.md#type-autochild) displaying the current value as a floating label when [showValue](#attr-slidershowvalue) is true.

**Flags**: IR

---
## Attr: Slider.roundValues

### Description
Specifies whether the slider value should be rounded to the nearest integer. If set to false, values will be rounded to a fixed number of decimal places controlled by [Slider.roundPrecision](#attr-sliderroundprecision).

**Flags**: IRW

---
## Attr: Slider.thumbThickWidth

### Description
The dimension of the thumb perpendicular to the slider track.

**Flags**: IRW

---
## Attr: Slider.hLabelSpacing

### Description
The space around the labels used to display the [minimum, maximum](#attr-sliderrangelabel) and [current](#attr-slidervaluelabel) values of the slider, when [vertical](#attr-slidervertical) is false. If unset, defaults to [Slider.labelSpacing](#attr-sliderlabelspacing).

**Flags**: IRW

---
## Attr: Slider.sliderTarget

### Description
The target widget for the `sliderMove` event generated when the slider thumb is moved.

**Flags**: IRW

---
## Attr: Slider.roundPrecision

### Description
If [Slider.roundValues](#attr-sliderroundvalues) is false, the slider value will be rounded to this number of decimal places. If set to null the value will not be rounded

**Flags**: IRW

---
## Attr: Slider.minValueLabel

### Description
The text displayed in the label for the minimum value of the slider. If left as null, then slider.minValue will be displayed.

### See Also

- [Slider.showRange](#attr-slidershowrange)
- [Slider.minValue](#attr-sliderminvalue)

**Flags**: IRW

---
## Attr: Slider.animateThumbTime

### Description
Duration of thumb animation, in milliseconds.

### Groups

- animation

**Flags**: IRW

---
## Attr: Slider.labelHeight

### Description
The height of the labels used to display the [minimum, maximum](#attr-sliderrangelabel) and [current](#attr-slidervaluelabel) values of the slider.

**Flags**: IRW

---
## Attr: Slider.titleStyle

### Description
CSS style for the [title-text](#attr-slidertitle), when [showTitle](#attr-slidershowtitle) is true.

**Flags**: IR

---
## Attr: Slider.trackCapSize

### Description
The height of [vertical](#attr-slidervertical) slider start and end images, or width of horizontal slider start and end images.

**Flags**: IRW

---
## Attr: Slider.title

### Description
Optional display title for the slider.

### See Also

- [Slider.showTitle](#attr-slidershowtitle)

**Flags**: IRW

---
## Attr: Slider.maxValueLabel

### Description
The text displayed in the label for the maximum value of the slider. If left as null, then slider.maxValue will be displayed.

### See Also

- [Slider.showRange](#attr-slidershowrange)
- [Slider.maxValue](#attr-slidermaxvalue)

**Flags**: IRW

---
## Attr: Slider.thumbThinWidth

### Description
The dimension of the thumb parallel to the slider track.

**Flags**: IRW

---
## Attr: Slider.vThumbStyle

### Description
Optional CSS style for the thumb for a [vertically oriented](#attr-slidervertical) slider. See [Slider.hThumbStyle](#attr-sliderhthumbstyle) for state suffixes.

**Flags**: IR

---
## Attr: Slider.thumbSrc

### Description
The base filename for the slider thumb images. The filenames for the thumb icons are assembled from this base filename and the state of the thumb, as follows:  
Assume the thumbSrc is set to `{baseName}.{extension}`  
The full set of images to be displayed is:  
For horizontal sliders:

*   `h{baseName}.{extension}`: default enabled appearance.
*   `h{baseName}_down.{extension}`: appearance when the slider is enabled and the thumb is clicked.
*   `h{baseName}_Disabled.{extension}`: appearance when the slider is disabled.

For vertical sliders:

*   `v{baseName}.{extension}`: default enabled appearance.
*   `v{baseName}_down.{extension}`: appearance when the slider is enabled and the thumb is clicked.
*   `v{baseName}_Disabled.{extension}`: appearance when the slider is disabled.

**Flags**: IRW

---
## Attr: Slider.trackSrc

### Description
The base filename for the slider track images. The filenames for the track icons are assembled from this base filename and the state of the slider, as follows:  
Assume the trackSrc is set to `{baseName}.{extension}`  
The full set of images to be displayed is:  
For horizontal sliders:

*   `h{baseName}_start.{extension}`: start (left edge) of the track for a slider that is enabled.
*   `h{baseName}_stretch.{extension}`: the track for an enabled slider; this may be centered, tiled, or stretched.
*   `h{baseName}_end.{extension}`: end (right edge) of the track for a slider that is enabled.
*   `h{baseName}_Disabled_start.{extension}`: start (left edge) of the track for a slider that is disabled.
*   `h{baseName}_Disabled_stretch.{extension}`: the track for a disabled slider; this may be centered, tiled, or stretched.
*   `h{baseName}_Disabled_end.{extension}`: end (right edge) of the track for a slider that is disabled.

For vertical sliders:

*   `v{baseName}_start.{extension}`: start (bottom edge) of the track for a slider that is enabled.
*   `v{baseName}_stretch.{extension}`: the track for an enabled slider; this may be centered, tiled, or stretched.
*   `v{baseName}_end.{extension}`: end (top edge) of the track for a slider that is enabled.
*   `v{baseName}_Disabled_start.{extension}`: start (bottom edge) of the track for a slider that is disabled.
*   `v{baseName}_Disabled_stretch.{extension}`: the track for a disabled slider; this may be centered, tiled, or stretched.
*   `v{baseName}_end.{extension}`: end (top edge) of the track for a slider that is disabled.

### See Also

- [Slider.trackImageType](#attr-slidertrackimagetype)

**Flags**: IRW

---
## Method: Slider.setMaxValueLabel

### Description
Sets the [Slider.maxValueLabel](#attr-slidermaxvaluelabel) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelText | [String](#type-string) | false | — | new label text |

---
## Method: Slider.getValue

### Description
Returns the current slider value.

### Returns

`[float](../reference.md#type-float)` — current slider value

---
## Method: Slider.setMaxValue

### Description
Sets the [maximum value](#attr-slidermaxvalue) of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [float](../reference.md#type-float) | false | — | the new maximum value |

---
## Method: Slider.setRoundPrecision

### Description
Sets the [Slider.roundPrecision](#attr-sliderroundprecision) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| roundPrecision | [int](../reference.md#type-int) | false | — | new round precision |

---
## Method: Slider.setThumbThinWidth

### Description
Sets the [Slider.thumbThinWidth](#attr-sliderthumbthinwidth) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newWidth | [int](../reference.md#type-int) | false | — | new thumbThinWidth |

---
## Method: Slider.setFlipValues

### Description
Sets the [Slider.flipValues](#attr-sliderflipvalues) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| flipValues | [boolean](../reference.md#type-boolean) | false | — | flip slider values? |

---
## Method: Slider.setValue

### Description
Sets the slider value to newValue and moves the slider thumb to the appropriate position for this value. Sends the 'sliderMove' event to the sliderTarget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [float](../reference.md#type-float) | false | — | the new value |
| noAnimation | [boolean](../reference.md#type-boolean) | false | — | do not animate the slider thumb to the new value |

---
## Method: Slider.setLabelSpacing

### Description
Sets the [Slider.labelSpacing](#attr-sliderlabelspacing) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelWidth | [int](../reference.md#type-int) | false | — | new label spacing |

---
## Method: Slider.setTitle

### Description
Sets the [Slider.title](#attr-slidertitle) of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [String](#type-string) | false | — | new title for the slider |

---
## Method: Slider.setShowValue

### Description
Sets the [Slider.showValue](#attr-slidershowvalue) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showValue | [boolean](../reference.md#type-boolean) | false | — | show the slider value? |

---
## Method: Slider.setRoundValues

### Description
Sets the [Slider.roundValues](#attr-sliderroundvalues) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| roundValues | [boolean](../reference.md#type-boolean) | false | — | round slider values? |

---
## Method: Slider.setThumbThickWidth

### Description
Sets the [Slider.thumbThickWidth](#attr-sliderthumbthickwidth) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newWidth | [int](../reference.md#type-int) | false | — | new thumbThickWidth |

---
## Method: Slider.setShowTitle

### Description
Sets the [Slider.showTitle](#attr-slidershowtitle) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showTitle | [Boolean](#type-boolean) | false | — | show the slider title? |

---
## Method: Slider.setStepPercent

### Description
Sets the [Slider.stepPercent](#attr-slidersteppercent) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stepPercent | [float](../reference.md#type-float) | false | — | new slider step percent |

---
## Method: Slider.valueIsChanging

### Description
Call this method in your [Slider.valueChanged](#method-slidervaluechanged) handler to determine whether the value change is due to an ongoing drag interaction (true) or due to a thumb-release, mouse click, keypress, or programmatic event (false). You may choose to execute temporary or partial updates while the slider thumb is dragged, and final updates or persistence of the value in response to the other events.

### Returns

`[Boolean](#type-boolean)` — true if user is still dragging the slider thumb, false otherwise

**Flags**: A

---
## Method: Slider.setNumValues

### Description
Sets the [number of values](#attr-slidernumvalues) for the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newNumValues | [Integer](../reference_2.md#type-integer) | false | — | the new number of values |

---
## Method: Slider.setThumbSrc

### Description
Sets the [Slider.thumbSrc](#attr-sliderthumbsrc) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newSrc | [String](#type-string) | false | — | new thumbSrc |

---
## Method: Slider.setLabelHeight

### Description
Sets the [Slider.labelHeight](#attr-sliderlabelheight) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newHeight | [int](../reference.md#type-int) | false | — | new label height |

---
## Method: Slider.setTrackWidth

### Description
Sets the [Slider.trackWidth](#attr-slidertrackwidth) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newWidth | [int](../reference.md#type-int) | false | — | new trackWidth |

---
## Method: Slider.setTrackSrc

### Description
Sets the [Slider.trackSrc](#attr-slidertracksrc) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newSrc | [String](#type-string) | false | — | new trackSrc |

---
## Method: Slider.setShowRange

### Description
Sets the [Slider.showRange](#attr-slidershowrange) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showRange | [boolean](../reference.md#type-boolean) | false | — | show the slider range? |

---
## Method: Slider.setLabelWidth

### Description
Sets the [Slider.labelWidth](#attr-sliderlabelwidth) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelWidth | [int](../reference.md#type-int) | false | — | new label width |

---
## Method: Slider.setVertical

### Description
Sets the [Slider.vertical](#attr-slidervertical) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isVertical | [boolean](../reference.md#type-boolean) | false | — | is the slider vertical |

---
## Method: Slider.setTrackCapSize

### Description
Sets the [Slider.trackCapSize](#attr-slidertrackcapsize) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newSize | [int](../reference.md#type-int) | false | — | new trackCapSize |

---
## Method: Slider.valueChanged

### Description
This method is called when the slider value changes. This occurs when the [setValue()](#method-slidersetvalue) method is called, or when the slider is moved. Observe this method to be notified when the slider value changes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [double](../reference.md#type-double) | false | — | the new value. |

### See Also

- [Class.observe](Class.md#method-classobserve)

**Flags**: A

---
## Method: Slider.setMinValue

### Description
Sets the [minimum value](#attr-sliderminvalue) of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [float](../reference.md#type-float) | false | — | the new minimum value |

---
## Method: Slider.setTrackImageType

### Description
Sets the [Slider.trackImageType](#attr-slidertrackimagetype) property of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newType | [ImageStyle](../reference.md#type-imagestyle) | false | — | new trackImageType |

---
