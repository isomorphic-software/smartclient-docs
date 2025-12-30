# CalendarView Documentation

[← Back to API Index](../reference.md)

---

## Class: CalendarView

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
CalendarView is a base class, extended by the various views available in a [Calendar](Calendar.md#class-calendar).

---
## Attr: CalendarView.calendar

### Description
The [calendar](Calendar.md#class-calendar) this view is in.

**Flags**: R

---
## Attr: CalendarView.useEventCanvasPool

### Description
Should [event canvas](EventCanvas.md#class-eventcanvas) instances be reused when visible events change?

**Flags**: IRW

---
## Attr: CalendarView.eventDragCanvasStyleName

### Description
CSS class applied to the [eventDragCanvas](#attr-calendarvieweventdragcanvas).

**Flags**: IR

---
## Attr: CalendarView.viewName

### Description
The name of this view, used to identify it in the [calendar](#attr-calendarviewcalendar).

**Flags**: R

---
## Attr: CalendarView.eventStyleName

### Description
If specified, overrides [Calendar.eventStyleName](Calendar.md#attr-calendareventstylename) and dictates the CSS style to use for events rendered in this view. Has no effect on events that already have a [style specified](CalendarEvent.md#attr-calendareventstylename).

### Groups

- appearance

**Flags**: IRW

---
## Attr: CalendarView.eventDragCanvas

### Description
[Canvas](Canvas.md#class-canvas) displayed while dragging or resizing an event in this view and styled according to [eventDragCanvasStyleName](#attr-calendarvieweventdragcanvasstylename).

**Flags**: IR

---
## Method: CalendarView.rebuild

### Description
Rebuild this CalendarView, including re-fetching its data as necessary. To avoid re-fetching the data, pass 'false' to this method, or call [refreshEvents()](#method-calendarviewrefreshevents) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| refreshData | [Boolean](#type-boolean) | true | — | If false, prevents data from bing refreshed. |

---
## Method: CalendarView.isTimelineView

### Description
Returns true if this is the [timeline view](Calendar.md#attr-calendartimelineview), false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a Timeline view

---
## Method: CalendarView.refreshEvents

### Description
Clear, recalculate and redraw the events for the current range, without causing a fetch.

---
## Method: CalendarView.isDayView

### Description
Returns true if this is the [day view](Calendar.md#attr-calendardayview), false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a Day view

---
## Method: CalendarView.isMonthView

### Description
Returns true if this is the [month view](Calendar.md#attr-calendarmonthview), false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a Month view

---
## Method: CalendarView.scrollToStart

### Description
Move the viewport of this CalendarView to the start of its scrollable range.

---
## Method: CalendarView.isWeekView

### Description
Returns true if this is the [week view](Calendar.md#attr-calendarweekview), false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a Week view

---
## Method: CalendarView.isSelectedView

### Description
Returns true if this view is the currently selected view in the parent calendar.

### Returns

`[Boolean](#type-boolean)` — true if the view is selected in the parent calendar, false otherwise

---
## Method: CalendarView.scrollToEnd

### Description
Move the viewport of this CalendarView to the end of its scrollable range.

---
