# Lane Documentation

[← Back to API Index](../reference.md)

---

## Attr: Lane.sublanes

### Description
Array of [Lane](../reference.md#object-lane) objects that will share the available space in the parent Lane, vertically in [timelines](Calendar.md#attr-calendartimelineview) and horizontally in [day views](Calendar.md#attr-calendardayview).

Only one level of sublanes is supported, so this attribute only has an effect on [top-level lanes](Calendar.md#attr-calendarlanes).

Note that this feature is mutually exclusive with the [auto arrangement](Calendar.md#attr-calendareventautoarrange) of events that share time.

**Flags**: IR

---
## Attr: Lane.styleName

### Description
The base style-name for normal cells in this Lane.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Lane.height

### Description
In [Timeline](../reference.md#class-timeline)s, the height of this Lane's row. Has no effect when set on a Lane being displayed in a [day view](Calendar.md#attr-calendardayview) as a result of [Calendar.showDayLanes](Calendar.md#attr-calendarshowdaylanes) being true.

If set directly on a [sublane](#attr-lanesublanes), overrides the default behavior of dividing the height equally among the lane's sublanes. Each sublane is still initially assigned an equal slice of the parent height, and the value for this sublane is then updated. So the overall height of the parent lane will change by the delta between the initial slice and the specified one.

**Flags**: IR

---
## Attr: Lane.title

### Description
Title to show for this lane. Has no effect if set directly on [sublanes](#attr-lanesublanes).

**Flags**: IR

---
## Attr: Lane.eventStyleName

### Description
The base name for the CSS class applied to [events](Calendar.md#attr-calendareventcanvas) when they're rendered in this lane. See [Calendar.eventStyleName](Calendar.md#attr-calendareventstylename).

If set directly on a [sublane](#attr-lanesublanes), overrides the corresponding value on the parent [lane](Calendar.md#attr-calendarlanes). See [getEventCanvasStyle()](Calendar.md#method-calendargeteventcanvasstyle) for more information.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Lane.name

### Description
To determine whether a CalendarEvent should be placed in this lane, the value of this attribute is compared with the [Calendar.laneNameField](Calendar.md#attr-calendarlanenamefield) property on the CalendarEvent.

**Flags**: IR

---
## Attr: Lane.width

### Description
When set on a Lane being displayed in a [day view](Calendar.md#attr-calendardayview) as a result of [Calendar.showDayLanes](Calendar.md#attr-calendarshowdaylanes) being set, dictates the width of the Lane's column. Has no effect in [Timeline](../reference.md#class-timeline)s.

If set directly on a [sublane](#attr-lanesublanes), overrides the default behavior of dividing the width equally among the lane's sublanes. Each sublane is still initially assigned an equal slice of the original parent width, and the value for this sublane is then updated. So the overall width of the parent lane will change by the delta between the initial slice and the specified one.

**Flags**: IR

---
## Attr: Lane.fieldStyleName

### Description
The base style-name for [lane-fields](Calendar.md#attr-calendarlanefields) displayed in this Lane.

### Groups

- appearance

**Flags**: IRW

---
