# CalendarView Documentation

[← Back to API Index](../reference.md)

---

## Class: CalendarView

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
CalendarView is a base class, extended by the various views available in a [Calendar](Calendar.md#class-calendar).

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
## Attr: CalendarView.longEventsLayout

### Description
A separate container that provides an intuitive way for users to view and interact with multi-day events, or events marked as lasting [all day](Calendar.md#attr-calendaralldayfield). If you've seen the calendars provided by Google, Apple or Microsoft, you'll already be familiar with the approach.

In the [day](Calendar.md#attr-calendardayview) and [week](Calendar.md#attr-calendarweekview) views, this component appears beneath the headers and does not scroll with the main body. In the [month](Calendar.md#attr-calendarmonthview) view, multiple instances of this component are created and shown beneath the headers for each week.

Users may click in this component to create an _all-day_ event on the clicked date, or drag to create an event that spans multiple days, and weeks in the [month view](Calendar.md#attr-calendarmonthview). Either shows the new event for editing in the usual [Calendar.eventEditor](Calendar.md#attr-calendareventeditor).

When an event spans multiple days, or is marked as an all-day event, its associated [eventCanvas](Calendar.md#attr-calendareventcanvas) is displayed in this component instead of in the main body of a given [CalendarView](#class-calendarview). Each such event appears as a narrow horizontal bar spanning the full width of the columns its [start](Calendar.md#attr-calendarstartdatefield) and [end](Calendar.md#attr-calendarenddatefield) dates involve. In the _Month-view_, if an event spans multiple weeks, the longEvents component in each week will show parts of this event.

If a multi-day event spans beyond the current view's date-range at one or both ends, those ends are styled to indicate the event continues in that direction. Otherwise, if an event can be edited, users may drag -move or -resize it, or click it to show the _eventEditor_ window.

If multiple long-events occupy the same date-range, they are stacked vertically and this component will resize to accommodate them.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `calendarView.longEventsLayoutProperties` and `calendarView.longEventsLayoutDefaults`.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

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
## Method: CalendarView.refreshEvents

### Description
Clear, recalculate and redraw the events for the current range, without causing a fetch.

---
## Method: CalendarView.isWeekView

### Description
Returns true if this is the [week view](Calendar.md#attr-calendarweekview), false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a Week view

---
## Method: CalendarView.isTimelineView

### Description
Returns true if this is the [timeline view](Calendar.md#attr-calendartimelineview), false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a Timeline view

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
