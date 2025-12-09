# EventCanvas Documentation

[← Back to API Index](../reference.md)

---

## Class: EventCanvas

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
The EventCanvas component is a lightweight [layout](../reference.md#class-vlayout) subclass for displaying a [CalendarEvent](../reference.md#object-calendarevent) in a [CalendarView](CalendarView.md#class-calendarview).

Each instance can be [styled](CalendarEvent.md#attr-calendareventstylename), and can render a single area, or separate [header](#attr-eventcanvasshowheader) and [body](#attr-eventcanvasshowbody) areas, for the look of a Window.

The component's close and context buttons, and any necessary resizers, are shown on [rollover](#attr-eventcanvasshowrollovercontrols).

---
## Attr: EventCanvas.headerStyle

### Description
CSS class for the [header area](#attr-eventcanvasshowheader) of the EventCanvas. If unset, defaults to the [base styleName](#attr-eventcanvasstylename) with the suffix "Header".

### Groups

- appearance

**Flags**: IRW

---
## Attr: EventCanvas.showContextButton

### Description
When set to true, shows a [small icon](Calendar.md#attr-calendareventcanvascontextbutton) in the top corner of an EventCanvas, beside the [close-icon](Calendar.md#attr-calendareventcanvascontextbutton). When clicked, shows a [context menu](Calendar.md#method-calendargeteventcanvasmenuitems) containing items applicable to this canvas.

**Flags**: IRW

---
## Attr: EventCanvas.showBody

### Description
Renders a body DIV that fills the main area of the canvas, or all of it if no [header](#attr-eventcanvasshowheader) is shown. This area typically displays an [event description](CalendarEvent.md#attr-calendareventdescription). This area can be styled via [EventCanvas.bodyStyle](#attr-eventcanvasbodystyle) and the HTML it shows is retrieved from a call to [getBodyHTML()](#method-eventcanvasgetbodyhtml). The default is taken from [Calendar.showEventDescriptions](Calendar.md#attr-calendarshoweventdescriptions).

**Flags**: IRW

---
## Attr: EventCanvas.bodyStyle

### Description
CSS class for the [body area](#attr-eventcanvasshowbody) of the EventCanvas. If unset, defaults to the [base styleName](#attr-eventcanvasstylename) with the suffix "Body".

### Groups

- appearance

**Flags**: IRW

---
## Attr: EventCanvas.showLabel

### Description
When set to true, the [header text](#method-eventcanvasgetheaderhtml) for the associated event is not rendered inside the eventCanvas itself.

Instead, it is rendered in it's own [label](#attr-eventcanvaslabel) and shown as a peer of this eventCanvas, immediately outside of it.

**Flags**: IRW

---
## Attr: EventCanvas.calendar

### Description
The [Calendar](Calendar.md#class-calendar) in which this EventCanvas is being rendered.

**Flags**: IR

---
## Attr: EventCanvas.gripper

### Description
When [showGripper](#attr-eventcanvasshowgripper) is true, this is the component that will be rendered adjacent to the canvas and allow the canvas to be moved with the mouse.

**Flags**: IRW

---
## Attr: EventCanvas.showHeader

### Description
Renders a header DIV above the main body of the event, an area of limited height, styled to stand out from the main [body](#attr-eventcanvasshowbody) of the event, and typically showing a [name](CalendarEvent.md#attr-calendareventname) or title - like a Window. This header area can be styled via [EventCanvas.headerStyle](#attr-eventcanvasheaderstyle) and the HTML it shows is retrieved from a call to [getHeaderHTML()](#method-eventcanvasgetheaderhtml). The default is taken from [Calendar.showEventHeaders](Calendar.md#attr-calendarshoweventheaders).

**Flags**: IRW

---
## Attr: EventCanvas.calendarView

### Description
The [CalendarView](CalendarView.md#class-calendarview) in which this EventCanvas is being rendered.

**Flags**: IR

---
## Attr: EventCanvas.verticalResize

### Description
Indicates the orientation of the event in its containing view. Affects drag and resize orientation and which edges of the canvas are available for resizing.

**Flags**: IRW

---
## Attr: EventCanvas.escapeHTML

### Description
When set to true, escapes the HTML displayed in this EventCanvas and it's hover.

**Flags**: IRW

---
## Attr: EventCanvas.gripperIcon

### Description
The source for the icon displayed as the "gripper" that snaps to the top of an event canvas and allows an event to be dragged with the mouse.

**Flags**: IRW

---
## Attr: EventCanvas.showGripper

### Description
When set to true, shows the [gripper](#attr-eventcanvasgripper) component, which snaps, centered, to the top edge of the eventCanvas and can be used to move it with the mouse.

**Flags**: IRW

---
## Attr: EventCanvas.label

### Description
When [showLabel](#attr-eventcanvasshowlabel) is true, this autoChild is used to display the [header text](#method-eventcanvasgetheaderhtml), adjacent to this eventCanvas.

**Flags**: IRW

---
## Attr: EventCanvas.isZoneCanvas

### Description
Readonly property indicating whether this is a special [ZoneCanvas](../reference.md#class-zonecanvas) subclass.

**Flags**: R

---
## Attr: EventCanvas.headerHeight

### Description
The height for the [header area](#attr-eventcanvasshowheader), when [headerWrap](#attr-eventcanvasheaderwrap) is false and [showBody](#attr-eventcanvasshowbody) is true. If `showBody` is false, the header area fills the canvas.

### Groups

- appearance

**Flags**: IRW

---
## Attr: EventCanvas.showRolloverControls

### Description
When set to the default value of true, this attribute causes a set of components to be shown when the mouse rolls over this EventCanvas. These components include the [close](Calendar.md#attr-calendareventcanvasclosebutton) and [context](Calendar.md#attr-calendareventcanvascontextbutton) buttons, the latter's [context menu](Calendar.md#attr-calendareventcanvascontextmenu) and the images used for drag-resizing.

Using rollover controls is more efficient that showing static buttons in each eventCanvas, so this is the default behavior. See [Calendar.useEventCanvasRolloverControls](Calendar.md#attr-calendaruseeventcanvasrollovercontrols) for the alternative.

**Flags**: IRW

---
## Attr: EventCanvas.headerWrap

### Description
Whether the [header area](#attr-eventcanvasshowheader) should autosize vertically to display all contents. If true, the header will wrap to multiple lines. If false, the header will be sized according to the specified [height](#attr-eventcanvasheaderheight), or to the full height of the canvas is [showBody](#attr-eventcanvasshowbody) is false.

### Groups

- appearance

**Flags**: IRW

---
## Attr: EventCanvas.isIndicatorCanvas

### Description
Readonly property dictating whether this is a special [IndicatorCanvas](../reference.md#class-indicatorcanvas) subclass.

**Flags**: R

---
## Attr: EventCanvas.styleName

### Description
The CSS class for this EventCanvas. Defaults to the style on [eventCanvas.event](CalendarEvent.md#attr-calendareventstylename), if specified, or on the [calendar](Calendar.md#attr-calendareventstylename) otherwise.

Also see [EventCanvas.headerStyle](#attr-eventcanvasheaderstyle) and [EventCanvas.bodyStyle](#attr-eventcanvasbodystyle).

### Groups

- appearance

**Flags**: IRW

---
## Attr: EventCanvas.event

### Description
The [event](../reference.md#object-calendarevent) associated with this EventCanvas.

**Flags**: IR

---
## Method: EventCanvas.getBodyHTML

### Description
Return the HTML to show in the body of this EventCanvas. The default implementation calls [Calendar.getEventBodyHTML](Calendar.md#method-calendargeteventbodyhtml), which returns the value of the [description field](Calendar.md#attr-calendardescriptionfield) for the current [event](../reference.md#object-calendarevent).

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to display in the body of the canvas

### Groups

- appearance

---
## Method: EventCanvas.setEvent

### Description
Assigns a new [event](../reference.md#object-calendarevent) to this EventCanvas, including updates to drag, style and [rollover](#attr-eventcanvasshowrollovercontrols) properties.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the new event to apply to this EventCanvas |
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | true | — | optional CSS class to apply to this EventCanvas |
| headerStyle | [CSSStyleName](../reference.md#type-cssstylename) | true | — | optional separate CSS class to apply to the [header](#attr-eventcanvasshowheader). |
| bodyStyle | [CSSStyleName](../reference.md#type-cssstylename) | true | — | optional separate CSS class to apply to the [body](#attr-eventcanvasshowbody). |

### Groups

- appearance

---
## Method: EventCanvas.getHeaderHTML

### Description
Returns the HTML to show in the header of this EventCanvas. The default implementation returns the [name](Calendar.md#attr-calendarnamefield) of the current [event](#attr-eventcanvasevent).

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to display in the header of the canvas

### Groups

- appearance

---
