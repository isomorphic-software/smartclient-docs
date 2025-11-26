# CalendarEvent Documentation

[← Back to API Index](../reference.md)

---

## Attr: CalendarEvent.styleName

### Description
CSS style series to use for [canvas instances](Calendar.md#attr-calendareventcanvas) that represent this event in the various [calendar views](CalendarView.md#class-calendarview). The basic series should include three classes - the base style and others suffixed "Header" and "Body".

If not specified on the event, the style can be specified on the [calendar](Calendar.md#attr-calendareventstylename), the [view](CalendarView.md#attr-calendarvieweventstylename) or individually on each [lane](Lane.md#attr-laneeventstylename) or [sublane](Lane.md#attr-lanesublanes).

The name of this field within the CalendarEvent can be changed via [Calendar.eventStyleNameField](Calendar.md#attr-calendareventstylenamefield)

**Flags**: IR

---
## Attr: CalendarEvent.headerBackgroundColor

### Description
An optional background color for the header portion of [canvases](EventCanvas.md#class-eventcanvas) representing this event in the various [calendar views](CalendarView.md#class-calendarview).

Note that the recommended approach for styling events is to set a [custom CSS style](#attr-calendareventstylename), which allows more complete customization of both header and body portions.

**Flags**: IRW

---
## Attr: CalendarEvent.headerBorderColor

### Description
An optional border color for the header portion of [canvases](EventCanvas.md#class-eventcanvas) representing this event in the various [calendar views](CalendarView.md#class-calendarview).

Note that the recommended approach for styling events is to set a [custom CSS style](#attr-calendareventstylename), which allows more complete customization of both header and body portions.

**Flags**: IRW

---
## Attr: CalendarEvent.canEdit

### Description
Optional boolean value controlling the editability of this particular calendarEvent. The name of this field within the CalendarEvent can be changed via [Calendar.canEditField](Calendar.md#attr-calendarcaneditfield).

**Flags**: IRW

---
## Attr: CalendarEvent.canDrag

### Description
Optional boolean value controlling whether this event can be dragged with the mouse. The name of this field within the CalendarEvent can be changed via [Calendar.canDragEventField](Calendar.md#attr-calendarcandrageventfield). Only has an effect when [editing](Calendar.md#attr-calendarcaneditevents) is enabled.

You can separately disallow drag-resize via [canResize](#attr-calendareventcanresize).

**Flags**: IRW

---
## Attr: CalendarEvent.canEditSublane

### Description
Boolean indicating whether this event can be moved between lanes. Can also be set at the [calendar level](Calendar.md#attr-calendarcaneditsublane).

The name of this field within the CalendarEvent can be changed via [Calendar.canEditSublaneField](Calendar.md#attr-calendarcaneditsublanefield).

**Flags**: IRW

---
## Attr: CalendarEvent.backgroundColor

### Description
An optional background color for the body portion of [canvases](EventCanvas.md#class-eventcanvas) representing this event in the various [calendar views](CalendarView.md#class-calendarview).

Note that the recommended approach for styling events is to set a [custom CSS style](#attr-calendareventstylename), which allows more complete customization of both header and body portions.

**Flags**: IRW

---
## Attr: CalendarEvent.lane

### Description
When in Timeline mode, or when [Calendar.showDayLanes](Calendar.md#attr-calendarshowdaylanes) is true, a string that represents the name of the [lane](Calendar.md#attr-calendarlanes) this [CalendarEvent](../reference.md#object-calendarevent) should sit in. The name of this field within the CalendarEvent can be changed via [Calendar.laneNameField](Calendar.md#attr-calendarlanenamefield).

**Flags**: IRW

---
## Attr: CalendarEvent.startDate

### Description
Date object which represents the start date of a [CalendarEvent](../reference.md#object-calendarevent). The name of this field within the CalendarEvent can be changed via [Calendar.startDateField](Calendar.md#attr-calendarstartdatefield)

**Flags**: IRW

---
## Attr: CalendarEvent.canEditLane

### Description
Boolean indicating whether this event can be moved between lanes. Can also be set at the [calendar level](Calendar.md#attr-calendarcaneditlane).

The name of this field within the CalendarEvent can be changed via [Calendar.canEditLaneField](Calendar.md#attr-calendarcaneditlanefield).

**Flags**: IRW

---
## Attr: CalendarEvent.textColor

### Description
An optional text color for the body portion of [canvases](EventCanvas.md#class-eventcanvas) representing this event in the various [calendar views](CalendarView.md#class-calendarview).

Note that the recommended approach for styling events is to set a [custom CSS style](#attr-calendareventstylename), which allows more complete customization of both header and body portions.

**Flags**: IRW

---
## Attr: CalendarEvent.disabled

### Description
For a CalendarEvent that represents a [styled zone](Calendar.md#attr-calendarzones), this attribute causes date-cells behind this zone to be disabled, meaning that events cannot be created or moved there with the mouse.

**Flags**: IRW

---
## Attr: CalendarEvent.borderColor

### Description
An optional border color for the body portion of [canvases](EventCanvas.md#class-eventcanvas) representing this event in the various [calendar views](CalendarView.md#class-calendarview).

Note that the recommended approach for styling events is to set a [custom CSS style](#attr-calendareventstylename), which allows more complete customization of both header and body portions.

**Flags**: IRW

---
## Attr: CalendarEvent.name

### Description
String which represents the name of a [CalendarEvent](../reference.md#object-calendarevent) The name of this field within the CalendarEvent can be changed via [Calendar.nameField](Calendar.md#attr-calendarnamefield)

**Flags**: IRW

---
## Attr: CalendarEvent.durationUnit

### Description
When a [duration](#attr-calendareventduration) is set for this event, this is the unit of that duration. The default is minutes.

**Flags**: IRW

---
## Attr: CalendarEvent.description

### Description
String which represents the description of a [CalendarEvent](../reference.md#object-calendarevent) The name of this field within the CalendarEvent can be changed via [Calendar.descriptionField](Calendar.md#attr-calendardescriptionfield)

**Flags**: IRW

---
## Attr: CalendarEvent.sublane

### Description
When in Timeline mode, or when [Calendar.showDayLanes](Calendar.md#attr-calendarshowdaylanes) is true, a string that represents the name of the [sublane](Lane.md#attr-lanesublanes) this [CalendarEvent](../reference.md#object-calendarevent) should sit in. The name of this field within the CalendarEvent can be changed via [Calendar.sublaneNameField](Calendar.md#attr-calendarsublanenamefield).

**Flags**: IRW

---
## Attr: CalendarEvent.headerTextColor

### Description
An optional text color for the header portion of [canvases](EventCanvas.md#class-eventcanvas) representing this event in the various [calendar views](CalendarView.md#class-calendarview).

Note that the recommended approach for styling events is to set a [custom CSS style](#attr-calendareventstylename), which allows more complete customization of both header and body portions.

**Flags**: IRW

---
## Attr: CalendarEvent.eventWindowStyle

### Description
CSS style series to use for the draggable event window that represents this event. If specified, overrides [Calendar.eventWindowStyle](Calendar.md#attr-calendareventwindowstyle) for this specific event.

The name of this field within the CalendarEvent can be changed via [Calendar.eventWindowStyleField](Calendar.md#attr-calendareventwindowstylefield)

**Deprecated**

**Flags**: IR

---
## Attr: CalendarEvent.duration

### Description
The duration of this event. May be specified instead of an [end date](#attr-calendareventenddate) and implies that this is a "Period" type event. If set to zero, implies an "Instant" type event - an event with a start date but no length.

**Flags**: IRW

---
## Attr: CalendarEvent.endDate

### Description
Date object which represents the end date of a [CalendarEvent](../reference.md#object-calendarevent) The name of this field within the CalendarEvent can be changed via [Calendar.endDateField](Calendar.md#attr-calendarenddatefield)

**Flags**: IRW

---
## Attr: CalendarEvent.canResize

### Description
Optional boolean value controlling whether this event can be drag-resized with the mouse. The name of this field within the CalendarEvent can be changed via [Calendar.canResizeEventField](Calendar.md#attr-calendarcanresizeeventfield).

Only has an effect if [editing](Calendar.md#attr-calendarcaneditevents) and [dragging](Calendar.md#attr-calendarcandragevents) are also enabled.

**Flags**: IRW

---
