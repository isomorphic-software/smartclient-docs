# Calendar Documentation

[← Back to API Index](../reference.md)

---

## Class: Calendar

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
The Calendar component provides several different ways for a user to view and edit a set of events. Note that the standard Calendar module must be loaded to make use of the Calendar class.

**CalendarEvents**

Events are represented as ordinary JavaScript Objects (see [CalendarEvent](../reference.md#object-calendarevent)). The Calendar expects to be able to read and write a basic set of properties on events: name, startDate, endDate, description, etc, which can be stored under configurable property names (see eg [Calendar.startDateField](#attr-calendarstartdatefield)).

Much like a [ListGrid](ListGrid_1.md#class-listgrid) manages it's ListGridRecords, the Calendar can either be passed an ordinary Array of CalendarEvents or can fetch data from a DataSource. When this is the case, if the DataSource does not contain fields with the configured property names, an attempt is made to auto-detect likely-looking fields from those that are present. To see logs indicating that this has happened, switch default logging preferences to INFO level in the Developer Console.

If the calendar is bound to a DataSource, event changes by user action or by calling methods will be saved to the DataSource.

**Navigation**

The calendar supports a number of views by default: [day](#attr-calendardayview), [week](#attr-calendarweekview), [month](#attr-calendarmonthview) and [timeline](#attr-calendartimelineview). The user can navigate using back and forward buttons or via an attached [DateChooser](#attr-calendardatechooser).

**Event Manipulation**

Events can be created by clicking directly onto one of the views, or via the [Add Event](#attr-calendaraddeventbutton) button. In the day, week and timeline views, the user may click and drag to create an event of a specific duration.

Creating an event via click or click and drag pops up the [EventDialog](#attr-calendareventdialog), which provides a simple form for quick event entry (for normal events, only the description is required by default - for events that are shown in a [lane](#attr-calendarlanes), that field is also required).

A separate editor called the [EventEditor](#attr-calendareventeditor) provides an interface for editing all possible properties of an event, including custom properties. The EventEditor is used whenever a pre-existing event is being edited, and can also be invoked by the user wherever the simpler EventDialog appears.

Events can also be programmatically [added](#method-calendaraddcalendarevent), [removed](#method-calendarremoveevent), or [updated](#method-calendarupdatecalendarevent).

---
## Attr: Calendar.baseStyle

### Description
The base name for the CSS class applied to the grid cells of the day and week views of the calendar. This style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.eventHeaderHeight

### Description
When [eventHeaderWrap](#attr-calendareventheaderwrap) is false and [showEventDescriptions](#attr-calendarshoweventdescriptions) is true, this is the fixed height for the [header area](EventCanvas.md#attr-eventcanvasshowheader) in event canvases.

**Flags**: IR

---
## Attr: Calendar.cancelButton

### Description
An [AutoChild](../reference.md#type-autochild) of type [IButton](../reference.md#class-ibutton), used to cancel editing of an event and close the [eventEditor](#attr-calendareventeditor).

**Flags**: R

---
## Attr: Calendar.dateEditingStyle

### Description
Indicates the type of controls to use in event-windows. Valid values are those in the [DateEditingStyle](../reference.md#type-dateeditingstyle) type.

If unset, the editing style will be set to the field-type on the DataSource, if there is one. If there's no DataSource, it will be set to "date" if the [granularity](#attr-calendartimelinegranularity) is "day" or larger and "time" if granularity is "minute" or smaller, otherwise "datetime".

**Flags**: IR

---
## Attr: Calendar.zoneTitleOrientation

### Description
The vertical alignment of the header-text in each [zone](#attr-calendarzones).

**Flags**: IR

---
## Attr: Calendar.otherDayBodyBaseStyle

### Description
The base name for the CSS class applied to the day body of the month view of the calendar. This style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.showDateChooser

### Description
Determines whether the [dateChooser](#attr-calendardatechooser) is displayed.

### Groups

- visibility

**Flags**: IR

---
## Attr: Calendar.indicatorCanvas

### Description
AutoChild component created for each [indicator](#attr-calendarindicators) entry.

**Flags**: A

---
## Attr: Calendar.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: Calendar.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference_2.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: Calendar.laneEventPadding

### Description
The pixel space to leave between events and the edges of the [lane](#attr-calendarlanes) or [sublane](Lane.md#attr-lanesublanes) they appear in. Only applicable to [timelines](#attr-calendartimelineview) and to [dayViews](#attr-calendardayview) showing [day lanes](#attr-calendarshowdaylanes).

**Flags**: IRW

---
## Attr: Calendar.canSelectEvents

### Description
When set to true, makes individual [event canvases](EventCanvas.md#class-eventcanvas) selectable. Events may be selected via a single click, as well as being included in the page's tab order. The current selected event is shown in a special style and pressing TAB or Shift-TAB will move the selection first among the events in the same lane, and then among those in the next or previous lane.

Pressing Enter while an editable event is selected will show either the event- [dialog](#attr-calendareventdialog) or [editor](#attr-calendareventeditor). Pressing Delete will remove the event.

Note that when this property is false, single clicking the event canvas for an editable event will bring up an editing interface for that event. When true this is no longer the case - a user can double click to bring up the editing interface instead (a single click will simply select the event canvas).

**Flags**: IR

---
## Attr: Calendar.eventEditor

### Description
An [AutoChild](../reference.md#type-autochild) of type [DynamicForm](DynamicForm.md#class-dynamicform) which displays [event data](../reference.md#object-calendarevent). This form is created within the [event editor layout](#attr-calendareventeditorlayout)

**Flags**: R

---
## Attr: Calendar.showEventHeaders

### Description
When rendering the [canvas](#attr-calendareventcanvas) for an event, whether to show the [header area](EventCanvas.md#attr-eventcanvasshowheader), typically containing suitable title text - [by default](#method-calendargeteventheaderhtml), the event's [name](#attr-calendarnamefield).

The default is true - if set to false, the event's [body area](EventCanvas.md#attr-eventcanvasshowbody) will fill the canvas.

**Flags**: IR

---
## Attr: Calendar.selectedCellStyle

### Description
The base name for the CSS class applied to a cell that is selected via a mouse drag.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.bringEventsToFront

### Description
If set to true, clicking an event will bring it to the front of the zorder.

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.zoneCanvas

### Description
AutoChild component created for each [zone](#attr-calendarzones) entry.

**Flags**: A

---
## Attr: Calendar.eventDragGap

### Description
The number of pixels to leave to the right of events so overlapping events can still be added using the mouse.

**Flags**: IRW

---
## Attr: Calendar.startDate

### Description
The start date of the calendar [timeline view](../reference.md#class-timeline). Has no effect in other views. If not specified, defaults to a timeline starting from the beginning of the current [timelineGranularity](#attr-calendartimelinegranularity) and spanning [a default of 20](#attr-calendardefaulttimelinecolumnspan) columns of that granularity.

To set different start and [end](#attr-calendarenddate) dates after initial draw, see [setTimelineRange](#method-calendarsettimelinerange).

Note that the value you provide may be automatically altered if showing [header-levels](#attr-calendarheaderlevels), to fit to header boundaries.

**Flags**: IR

---
## Attr: Calendar.allowLongEvents

### Description
When set to true, provides an intuitive way for users to view and interact with multi-day events, or events marked as lasting [all day](#attr-calendaralldayfield). If you've seen the calendars provided by Google, Apple or Microsoft, you'll already be familiar with the approach.

In vertical views, long-events are displayed in a [horizontal area](CalendarView.md#attr-calendarviewlongeventslayout) across the top of the main grid. In the [MonthView](#attr-calendarmonthview), each week of date-cells has its own area for displaying long-events, which may wrap from one week to the next. You can click or drag in this area to create new events, and click or drag existing events there to edit or move them, respectively. The style of this area may be [customized](#attr-calendarlongeventlayoutstylename).

Long events are rendered using a subclass of [EventCanvas](EventCanvas.md#class-eventcanvas), with custom [content](#method-calendargetlongeventhtml), [hover-content](#method-calendargetlongeventhoverhtml) and [styling](#attr-calendarlongeventstylename).

**Flags**: RWA

---
## Attr: Calendar.alternateLaneStyles

### Description
When showing a [Timeline](#attr-calendartimelineview), or a [day view](#attr-calendardayview) when [Calendar.showDayLanes](#attr-calendarshowdaylanes) is true, whether to make lane boundaries more obvious by showing alternate lanes in a different color.

**Flags**: IRW

---
## Attr: Calendar.hideUnusedLanes

### Description
When set to true, hides any [lane](#attr-calendarlanes) that doesn't have any active events in the current dataset.

**Flags**: IRW

---
## Attr: Calendar.canEditSublane

### Description
Can events be moved between sublanes?

If so, the event can be dragged to a different [sublane](Lane.md#attr-lanesublanes) within the same parent Lane and, when it's editor is shown, an additional drop-down widget is provided allowing the sublane to be altered.

If the sublane is locked, but the [parent lane](#attr-calendarcaneditlane) isn't, an update to the event's [lane name](#attr-calendarlanenamefield) will be allowed, assuming that the new Lane has an existing sublane with the same name.

In either case, the event's [sublane](#attr-calendarsublanenamefield) is updated automatically.

This setting can be overridden on each [event](CalendarEvent.md#attr-calendareventcaneditsublane).

**Flags**: IR

---
## Attr: Calendar.lanes

### Description
An array of [Lane](../reference.md#object-lane) definitions that represent the rows of the [Calendar.timelineView](#attr-calendartimelineview), or the columns of the [Calendar.dayView](#attr-calendardayview) if [showDayLanes](#attr-calendarshowdaylanes) is true.

**Flags**: IRW

---
## Attr: Calendar.showMonthButton

### Description
Set to false to prevent the [Month](#attr-calendarmonthbutton) button from displaying on Handset devices.

**Flags**: IRW

---
## Attr: Calendar.previousButtonHoverText

### Description
The text to be displayed when a user hovers over the [previous](#attr-calendarpreviousbutton) toolbar button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.selectionManager

### Description
The [Selection object](../kb_topics/selection.md#kb-topic-selection) associated with the `Calendar`.

### Groups

- selection

**Flags**: RA

---
## Attr: Calendar.eventDialogFields

### Description
The set of fields for the [event dialog](#attr-calendareventdialog).

The default set of fields are:

```
    {name: "name", title: "Event Name", type: nameType, width: 250 },
    {name: "save", title: "Save Event", editorType: "SubmitItem", endRow: false},
    {name: "details", title: "Edit Details", type: "button", startRow: false}
 
```
See the Customized Binding example below for more information on altering default datasource fields within forms.

### Groups

- editing

**Flags**: IR

---
## Attr: Calendar.eventEndDateFieldTitle

### Description
The title for the [Calendar.endDateField](#attr-calendarenddatefield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.minimalUI

### Description
A boolean value controlling whether the Calendar shows tabs for available calendar views. By default, this is true for handsets and false otherwise.

**Flags**: IRW

---
## Attr: Calendar.fixedEventHeight

### Description
When set, applies a fixed height to horizontal events in Timelines, rather than allowing them to share the whole height of their Lane. Overlapping behavior is unchanged, but all events are of the same fixed height and are stacked in the Lane, which may overflow to accommodate more events.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.otherDayBlankStyle

### Description
The CSS style applied to both the header and body of days from other months in the [month view](#attr-calendarmonthview), when [Calendar.showOtherDays](#attr-calendarshowotherdays) is false.

### Groups

- appearance

**Flags**: IR

---
## Attr: Calendar.weekendDays

### Description
An array of integer day-numbers that should be considered to be weekend days by this Calendar instance. If unset, defaults to the set of days indicated [globally](DateUtil.md#classattr-dateutilweekenddays).

### Groups

- visibility

**Flags**: IRW

---
## Attr: Calendar.saveButtonTitle

### Description
The title for the [Save button](#attr-calendarsavebutton) in the [quick event dialog](#attr-calendareventdialog) and the [event editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.timelineGranularity

### Description
The granularity in which the [timelineView](#attr-calendartimelineview) will display events. Possible values are those available in the built-in [TimeUnit](../reference_2.md#type-timeunit) type.

**Flags**: IR

---
## Attr: Calendar.laneFields

### Description
Field definitions for the frozen area of the [Calendar.timelineView](#attr-calendartimelineview), which shows data about the timeline [Calendar.lanes](#attr-calendarlanes). Each field shows one attribute of the objects provided as [Calendar.lanes](#attr-calendarlanes).

When [lane grouping](#attr-calendarcangrouplanes) is enabled, only fields that are specified as lane fields can be used as group fields.

**Flags**: IR

---
## Attr: Calendar.durationUnitField

### Description
The name of the [durationUnit](CalendarEvent.md#attr-calendareventdurationunit) field on a [CalendarEvent](../reference.md#object-calendarevent).

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.showCellHovers

### Description
When [showViewHovers](#attr-calendarshowviewhovers) is true, dictates whether to display hover prompts when the mouse rolls over the normal cells in the body of CalendarViews.

The content of the hover is determined by a call to [Calendar.getCellHoverHTML](#method-calendargetcellhoverhtml), which can be overridden to return custom results; by default, it returns the cell's date as a string.

**Flags**: IR

---
## Attr: Calendar.nextButton

### Description
An [ImgButton](ImgButton.md#class-imgbutton) that appears above the week/day/month views of the calendar and allows the user to move the calendar forwards in time.

**Flags**: IR

---
## Attr: Calendar.longEventStyleName

### Description
The base name for the CSS class applied to [events](#attr-calendareventcanvas) when they're rendered in a [long-events layout](CalendarView.md#attr-calendarviewlongeventslayout) in a view. This style will have "Header" and "Body" appended to it, according to which part of the event window is being styled. By default, only the Header.

When the start or end of a longEvent extends beyond the range of its containing-view, this style is appended with "LeftEnd", "RightEnd" or "BothEnds", which additions clip the ends of the canvas into arrows pointing toward the next range.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.data

### Description
A List of CalendarEvent objects, specifying the data to be used to populate the calendar.

This property will typically not be explicitly specified for databound Calendars, where the data is returned from the server via databound component methods such as [Calendar.fetchData](#method-calendarfetchdata). In this case the data objects will be set to a [resultSet](ResultSet.md#class-resultset) rather than a simple array.

### Groups

- data

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IRW

---
## Attr: Calendar.saveButton

### Description
An [AutoChild](../reference.md#type-autochild) of type [IButton](../reference.md#class-ibutton), used to save an event from the [eventEditor](#attr-calendareventeditor).

**Flags**: R

---
## Attr: Calendar.eventCanvasButtonLayout

### Description
HLayout that snaps to the top-right of an event canvas on rollover and contains the [close](#attr-calendareventcanvasclosebutton) and/or [context](#attr-calendareventcanvascontextbutton) buttons.

**Flags**: A

---
## Attr: Calendar.leadingDateField

### Description
The name of the leading date field for each event. When this attribute and [Calendar.trailingDateField](#attr-calendartrailingdatefield) are present in the data, a line extends out from the event showing the extent of the leading and trailing dates - useful for visualizing a pipeline of events where some can be moved a certain amount without affecting others.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.eventCanvasCloseButtonSize

### Description
The size of the [close-button](#attr-calendareventcanvasclosebutton) that snaps to the top-right of an event canvas on rollover and shows allows an event to be removed from a [CalendarView](CalendarView.md#class-calendarview).

**Flags**: IR

---
## Attr: Calendar.calMonthEventLinkStyle

### Description
The base name for the CSS class applied to the links rendered by [Calendar.getDayBodyHTML](#method-calendargetdaybodyhtml).

These links are rendered as plain HTML links using A elements, and the CSS style in the provided skins references the pseudo-classes :link, :visited, :active, :hover.  
Even though it goes against the general policy of not exposing the HTML structures SC writes out and not relying on them for styling, applying style to these particular selectors is acceptable, as we're unlikely to use any other kind of HTML structure than a link.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.canEditLane

### Description
Can events be moved between lanes? If so, the event can be dragged to a different [lane](#attr-calendarlanes), and the event [quick dialog](#attr-calendareventdialog) and [editor](#attr-calendareventeditor) allow a lane to be selected with a drop-down chooser.

In either case, the event's [laneNameField](#attr-calendarlanenamefield) is updated automatically.

If set to false, cross-lane dragging is disallowed and drop-down Lane-choosers are disabled when editing existng events. When creating [new events](#attr-calendarcancreateevents), the Lane-chooser remains enabled so an initial Lane can be selected.

This setting can be overridden on each [event](CalendarEvent.md#attr-calendareventcaneditlane).

**Flags**: IR

---
## Attr: Calendar.dayView

### Description
[CalendarView](CalendarView.md#class-calendarview) used to display events that pertain to a given day.

**Flags**: R

---
## Attr: Calendar.eventStartDateFieldTitle

### Description
The title for the [Calendar.startDateField](#attr-calendarstartdatefield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showNextButton

### Description
Set to false to hide the [Next](#attr-calendarnextbutton) button.

**Flags**: IRW

---
## Attr: Calendar.removeButton

### Description
An [AutoChild](../reference.md#type-autochild) of type [IButton](../reference.md#class-ibutton), used to permanently remove an event from the [eventEditor](#attr-calendareventeditor).

**Flags**: R

---
## Attr: Calendar.eventCanvasGripper

### Description
The "gripper" widget that snaps to the top of an event canvas and allows an event to be dragged with the mouse.

**Flags**: A

---
## Attr: Calendar.minimumDayHeight

### Description
In the [month view](#attr-calendarmonthview) when [Calendar.showDayHeaders](#attr-calendarshowdayheaders) is true, this is the minimum height applied to a day cell and its header combined.

If `showDayHeaders` is false, this attribute has no effect - the minimum height of day cells is either an equal share of the available height, or the rendered height of the cell's HTML content, whichever is greater. If the latter, a vertical scrollbar is shown.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.eventCanvasContextMenu

### Description
Context menu displayed when an [event canvas](EventCanvas.md#class-eventcanvas) is right-clicked, or when the rollover [context button](#attr-calendareventcanvascontextbutton) is clicked. The context button, and the menu itself, will only be displayed if [getEventCanvasMenuItems](#method-calendargeteventcanvasmenuitems) returns an array of appropriate items for the event.

**Flags**: R

---
## Attr: Calendar.showAddEventButton

### Description
Set to false to hide the [Add Event](#attr-calendaraddeventbutton) button.

**Flags**: IRW

---
## Attr: Calendar.addEventButton

### Description
An [ImgButton](ImgButton.md#class-imgbutton) that appears in a Calendar's week/day/month views and offers an alternative way to create a new [event](../reference.md#object-calendarevent).

**Flags**: IR

---
## Attr: Calendar.rowHeight

### Description
The height of time-slots in the calendar.

**Flags**: IRW

---
## Attr: Calendar.dayBodyBaseStyle

### Description
The base name for the CSS class applied to the day body of the month view of the calendar. This style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.todayBackgroundColor

### Description
The background color for cells that represent today in all [CalendarView](CalendarView.md#class-calendarview)s.

**Flags**: IR

---
## Attr: Calendar.showDayHeaders

### Description
If true, the default, show a header cell for each day cell in the [month view](#attr-calendarmonthview), with both cells having a minimum combined height of [Calendar.minimumDayHeight](#attr-calendarminimumdayheight). If false, the header cells will not be shown, and the value of [Calendar.minimumDayHeight](#attr-calendarminimumdayheight) is ignored. This causes the available vertical space in month views to be shared equally between day cells, such that no vertical scrollbar is required unless the HTML in the cells renders them taller than will fit.

### Groups

- visibility

**Flags**: IR

---
## Attr: Calendar.indicators

### Description
An array of CalendarEvent instances representing instants in time, to be highlighted in [timeline views](#attr-calendartimelineview). Each indicator renders out as an [indicator canvas](../reference.md#class-indicatorcanvas), a special, non-interactive subclass of [EventCanvas](EventCanvas.md#class-eventcanvas), which spans all lanes and draws behind any normal, interactive events in the zorder, but in front of any [zones](#attr-calendarzones). The default [style](#attr-calendarindicatorstylename) for these components renders them as thin vertical lines that span all lanes and have a hover but no title.

**Flags**: IRW

---
## Attr: Calendar.eventStyleNameField

### Description
The name of the field used to override [Calendar.eventStyleName](#attr-calendareventstylename) for an individual [CalendarEvent.styleName](CalendarEvent.md#attr-calendareventstylename).

### Groups

- calendarEvent
- appearance

**Flags**: IR

---
## Attr: Calendar.timelineView

### Description
[CalendarView](CalendarView.md#class-calendarview) used to display events in lanes in a horizontal [Timeline](../reference.md#class-timeline) view.

**Flags**: R

---
## Attr: Calendar.eventAllDayFieldTitle

### Description
The title for the [Calendar.allDayField](#attr-calendaralldayfield) in the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.detailsButtonTitle

### Description
The title for the edit button in the quick [quick event dialog](#attr-calendareventdialog).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.overlapSortSpecifiers

### Description
A set of [sort-specifiers](../reference_2.md#object-sortspecifier) for customizing the render order of events that overlap.

In [timelines](../reference.md#class-timeline), this dictates the vertical rendering order of overlapped events in each [lane](../reference.md#object-lane).

In [day](#attr-calendardayview) and [week](#attr-calendarweekview) views, it dictates the horizontal rendering order of overlapped events in each column or Lane.

By default, events that share space in a Lane or column are rendered from top to bottom, or left to right according to their [start-dates](#attr-calendarstartdatefield) - the earliest in a given lane appears top-most in that lane, or left-most in its column.

Providing `overlapSortSpecifiers` allows for the events to be ordered by one or more of the fields stored on the events, or in the underlying [data-source](DataSource.md#class-datasource), if the Calendar is databound.

**Flags**: IRW

---
## Attr: Calendar.useEventCanvasRolloverControls

### Description
By default, the [close buttons](#attr-calendareventcanvasclosebutton) and the [horizontal](#attr-calendareventcanvashresizer) and [vertical](#attr-calendareventcanvasvresizer) resizer widgets for event canvases are shown only when the mouse is over a given event. Set this attribute to false to have event canvases show these widgets permanently.

**Flags**: IR

---
## Attr: Calendar.currentViewName

### Description
The name of the view that should be visible initially by default.

**Flags**: IRW

---
## Attr: Calendar.canRemoveField

### Description
Name of the field on each [CalendarEvent](../reference.md#object-calendarevent) that determines whether an event shows a remove button.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.mainView

### Description
[TabSet](TabSet.md#class-tabset) for managing calendar views when multiple views are available (eg, [day](#attr-calendardayview) and [month](#attr-calendarmonthview)).

**Flags**: R

---
## Attr: Calendar.workdayBaseStyle

### Description
If [Calendar.showWorkday](#attr-calendarshowworkday) is set, this is the style used for cells that are within the workday, as defined by [Calendar.workdayStart](#attr-calendarworkdaystart) and [Calendar.workdayEnd](#attr-calendarworkdayend), or by a date-specific range provided in [Calendar.getWorkdayStart](#method-calendargetworkdaystart) and [Calendar.getWorkdayEnd](#method-calendargetworkdayend) implementations.

### Groups

- workday
- appearance

**Flags**: IR

---
## Attr: Calendar.canDragEvents

### Description
A boolean value controlling whether users can drag-reposition events. By default, this is false for Touch devices, where drag gestures scroll the view, and true otherwise.

Only has an effect when [canEditEvents](#attr-calendarcaneditevents) is true.

### Groups

- allowedOperations

**Flags**: IR

---
## Attr: Calendar.eventEditorLayout

### Description
An [AutoChild](../reference.md#type-autochild) of type [Window](Window.md#class-window) that displays the full [event editor](#attr-calendareventeditor)

**Flags**: R

---
## Attr: Calendar.eventOverlap

### Description
When [Calendar.eventAutoArrange](#attr-calendareventautoarrange) is true, setting eventOverlap to true causes events that share timeslots to overlap each other by a percentage of their width, specified by [Calendar.eventOverlapPercent](#attr-calendareventoverlappercent). The default is true for Calendars and false for [Timelines](../reference.md#class-timeline).

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.datePickerButton

### Description
An [ImgButton](ImgButton.md#class-imgbutton) that appears above the various views of the calendar and offers alternative access to a [DateChooser](DateChooser.md#class-datechooser) to pick the current day.

**Flags**: IR

---
## Attr: Calendar.canResizeEvents

### Description
Can [events](../reference.md#object-calendarevent) be resized by dragging appropriate edges of the [canvas](EventCanvas.md#attr-eventcanvasverticalresize)? Only has an effect when both [canEditEvents](#attr-calendarcaneditevents) and [canDragEvents](#attr-calendarcandragevents) are true. Set this attribute to false to disallow drag-resizing.

Always false when [showColumnLayouts](#attr-calendarshowcolumnlayouts) is true.

**Flags**: IR

---
## Attr: Calendar.showWorkday

### Description
When set to true, this setting enables various features related to cells that fall within the workday (as defined by [Calendar.workdayStart](#attr-calendarworkdaystart) and [Calendar.workdayEnd](#attr-calendarworkdayend)) in vertical calendar views ([day](#attr-calendardayview) and [week](#attr-calendarweekview)). Workday cells can be [styled separately](#attr-calendarworkdaybasestyle) and [sized automatically](#attr-calendarsizetoworkday), and users can be prevented from scrolling the calendar beyond the [workday hours](#attr-calendarlimittoworkday).

The hours of the workday can be customized for particular dates by providing implementations of [Calendar.getWorkdayStart](#method-calendargetworkdaystart) and [Calendar.getWorkdayEnd](#method-calendargetworkdayend).

### Groups

- workday

### See Also

- [Calendar.styleWorkday](#attr-calendarstyleworkday)
- [Calendar.scrollToWorkday](#attr-calendarscrolltoworkday)
- [Calendar.sizeToWorkday](#attr-calendarsizetoworkday)
- [Calendar.limitToWorkday](#attr-calendarlimittoworkday)

**Flags**: IRW

---
## Attr: Calendar.laneGroupStartOpen

### Description
Describes the default state of lane groups in timelines when [groupLanesBy](#method-calendargrouplanesby) is called. Possible values are:

*   "all": open all groups
*   "first": open the first group
*   "none": start with all groups closed
*   Array of values that should be opened

### Groups

- grouping

### See Also

- [Calendar.groupLanesBy](#method-calendargrouplanesby)

**Flags**: IRW

---
## Attr: Calendar.previousButton

### Description
An [ImgButton](ImgButton.md#class-imgbutton) that appears above the week/day/month views of the calendar and allows the user to move the calendar backwards in time.

**Flags**: IR

---
## Attr: Calendar.controlsBarHeight

### Description
Default height of the [Calendar.controlsBar](#attr-calendarcontrolsbar) shown above the main Calendar grid. When multiple views are available and tabs are visible, this value is modified to ensure that the content of the `controlsBar` is vertically-aligned with the text in the tabs.

**Flags**: IR

---
## Attr: Calendar.eventCanvasLabel

### Description
—

**Flags**: A

---
## Attr: Calendar.monthButton

### Description
A [NavigationButton](NavigationButton.md#class-navigationbutton) that appears to the left of other navigation controls in the [controls bar](#attr-calendarcontrolsbar) on Handset devices.

Used to show and hide the [month view](#attr-calendarmonthview) on devices with limited space.

**Flags**: IR

---
## Attr: Calendar.eventCanvas

### Description
To display events in [day](#attr-calendardayview), [week](#attr-calendarweekview) and [timeline](#attr-calendartimelineview) views, the Calendar creates instances of [EventCanvas](EventCanvas.md#class-eventcanvas) for each event. Use the [AutoChild](../reference.md#type-autochild) system to customize these canvases.

**Flags**: A

---
## Attr: Calendar.otherDayHeaderBaseStyle

### Description
The base name for the CSS class applied to the day headers of the month view. This style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.longEventHeight

### Description
The default height of the canvases for [long-events](#attr-calendarallowlongevents) which are displayed in the separate [CalendarView.longEventsLayout](CalendarView.md#attr-calendarviewlongeventslayout).

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.monthButtonTitle

### Description
The title of the [month button](#attr-calendarmonthbutton), used for showing and hiding the [month view](#attr-calendarmonthview) on Handsets.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, monthName, is available and represents the name of the month containing the currently selected date.

The default value is the Month-name of the selected date.

When the month view is already visible, the title for the month button is set according to the value of [Calendar.backButtonTitle](#attr-calendarbackbuttontitle).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.eventWindowStyle

### Description
The base name for the CSS class applied to event windows within calendars. This style will have "Header", "HeaderLabel", and "Body" appended to it, according to which part of the event window is being styled. For example, to style the header, define a CSS class called 'eventWindowHeader'.

### Groups

- appearance

**Deprecated**

**Flags**: IRW

---
## Attr: Calendar.eventEditorButtons

### Description
The list of buttons to include in the [Calendar.eventEditor](#attr-calendareventeditor). Entries can be the names of the builtin buttons, [saveButton](#attr-calendarsavebutton), [removeButton](#attr-calendarremovebutton) and [cancelButton](#attr-calendarcancelbutton), or the names of custom [autoChildren](../reference.md#type-autochild) that have been defined on the Calendar instance, or widget instances that already exist.

The default is to show the builtin buttons.

**Flags**: IR

---
## Attr: Calendar.eventDialog

### Description
An [AutoChild](../reference.md#type-autochild) of type [Window](Window.md#class-window) that displays a quick event entry form in a popup window.

**Flags**: R

---
## Attr: Calendar.weekView

### Description
[CalendarView](CalendarView.md#class-calendarview) used to display events that pertain to a given week.

**Flags**: R

---
## Attr: Calendar.alwaysShowEventHovers

### Description
By default, EventCanvases show their content in hovers. If you set this attribute to false, hovers will only be shown if the content of the event-canvas is visually clipped.

Note - if you have custom hover-content/handling, you should leave this property set to true.

**Flags**: IRW

---
## Attr: Calendar.eventOverlapPercent

### Description
The size of the overlap, presented as a percentage of the width of events sharing timeslots.

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.eventNameFieldTitle

### Description
The title for the [Calendar.nameField](#attr-calendarnamefield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showEventHovers

### Description
When [showViewHovers](#attr-calendarshowviewhovers) is true, dictates whether to display hover prompts when the mouse moves over an [event canvas](EventCanvas.md#class-eventcanvas) in a calendarView.

The content of the hover is determined by a call to [Calendar.getCellHoverHTML](#method-calendargetcellhoverhtml), which can be overridden to return custom results.

**Flags**: IRW

---
## Attr: Calendar.headerLevels

### Description
Configures the levels of [headers](../reference_2.md#object-headerlevel) shown above the event area, and their time units.

Header levels are provided from the top down, so the first header level should be the largest time unit and the last one the smallest. The smallest is then used for the actual field-headers.

**Flags**: IRW

---
## Attr: Calendar.styleWorkday

### Description
When [showWorkday](#attr-calendarshowworkday) is true, applies the [Calendar.workdayBaseStyle](#attr-calendarworkdaybasestyle) to cells that fall within the workday (as defined by [Calendar.workdayStart](#attr-calendarworkdaystart) and [Calendar.workdayEnd](#attr-calendarworkdayend)), in both the [Calendar.dayView](#attr-calendardayview) and [Calendar.weekView](#attr-calendarweekview).

The hours of the workday can be customized for particular dates by providing implementations of [Calendar.getWorkdayStart](#method-calendargetworkdaystart) and [Calendar.getWorkdayEnd](#method-calendargetworkdayend).

### Groups

- workday

### See Also

- [Calendar.scrollToWorkday](#attr-calendarscrolltoworkday)
- [Calendar.sizeToWorkday](#attr-calendarsizetoworkday)
- [Calendar.limitToWorkday](#attr-calendarlimittoworkday)

**Flags**: IRW

---
## Attr: Calendar.canEditField

### Description
Name of the field on each [CalendarEvent](../reference.md#object-calendarevent) that determines whether it can be edited in the [event editor](#attr-calendareventeditor). Note that an event with `canEdit` set to true can also have [canDrag](#attr-calendarcandrageventfield) or [canResize](#attr-calendarcanresizeeventfield) set to false, which would still allow editing, but not via drag operations.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.rowTitleFrequency

### Description
A minute value that indicates which rows should show times in vertical views, like [day](#attr-calendardayview) and [week](#attr-calendarweekview). The default of 60 minutes shows titles on the first row of each hour. The value provided must be a multiple of [minutesPerRow](#attr-calendarminutesperrow) and be no larger than 60.

**Flags**: IR

---
## Attr: Calendar.controlBarIconBaseStyle

### Description
A CSS style to apply to icons in the [Calendar.controlsBar](#attr-calendarcontrolsbar). This is a base style supporting suffixes for states, specifically "Over", "Down" and "Disabled", which are applied when [ImgButton](ImgButton.md#class-imgbutton) settings like [ImgButton.showRollOverIcon](ImgButton.md#attr-imgbuttonshowrollovericon) are applied to the icons.

**Flags**: IR

---
## Attr: Calendar.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [Calendar.initialCriteria](#attr-calendarinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle). Additional request properties may be specified using [fetchRequestProperties](#attr-databoundcomponentfetchrequestproperties).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_2.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [Calendar.initialCriteria](#attr-calendarinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_2.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: Calendar.showZoneHovers

### Description
When [showViewHovers](#attr-calendarshowviewhovers) is true, dictates whether to display hover prompts when the mouse moves over a [zone](#attr-calendarzones) in a calendarView.

When [showCellHovers](#attr-calendarshowcellhovers) is true, this attribute is ignored and zone hovers are not displayed.

The content of the hover is determined by a call to [Calendar.getZoneHoverHTML](#method-calendargetzonehoverhtml), which can be overridden to return custom results.

**Flags**: IRW

---
## Attr: Calendar.eventCanvasComponent

### Description
Multi-AutoChild component, created as a space-filling member in individual [event-canvases](EventCanvas.md#class-eventcanvas), when [Calendar.showEventCanvasComponents](#attr-calendarshoweventcanvascomponents) is true.

### See Also

- [Calendar.showEventCanvasComponents](#attr-calendarshoweventcanvascomponents)
- [Calendar.createEventCanvasComponent](#method-calendarcreateeventcanvascomponent)
- [Calendar.updateEventCanvasComponent](#method-calendarupdateeventcanvascomponent)

**Flags**: IR

---
## Attr: Calendar.laneGroupByField

### Description
For timelines with [canGroupLanes](#attr-calendarcangrouplanes) set to true, this is a field name or array of field names on which to group the lanes in a timeline.

**Flags**: IRW

---
## Attr: Calendar.eventDescriptionFieldTitle

### Description
The title for the [Calendar.descriptionField](#attr-calendardescriptionfield) field in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.canResizeEventField

### Description
Name of the field on each [CalendarEvent](../reference.md#object-calendarevent) that determines whether an event can be resized by dragging.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.eventOverlapIdenticalStartTimes

### Description
When set to true, events that start at the same time will not overlap each other to prevent events having their close button hidden.

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.dateChooser

### Description
[DateChooser](DateChooser.md#class-datechooser) used to select the date for which events will be displayed.

**Flags**: R

---
## Attr: Calendar.columnsPerPage

### Description
When using the Next and Previous arrows to scroll a Timeline, this is the number of columns of the [timelineGranularity](#attr-calendartimelinegranularity) to scroll by. With the default value of null, the Timeline will scroll by its current length.

**Flags**: IR

---
## Attr: Calendar.canGroupLanes

### Description
If true, allows the lanes in a Timeline to be grouped by providing a value for [laneGroupByField](#attr-calendarlanegroupbyfield). The fields available for grouping on are those defined as [lane fields](#attr-calendarlanefields). Since these are definitions for [normal fields](../reference_2.md#object-listgridfield), you can choose to [hide](ListGridField.md#method-listgridfieldshowif) the field in the timeline, but still have it available for grouping.

**Flags**: IRW

---
## Attr: Calendar.eventEditorFields

### Description
The set of fields for the [event editor](#attr-calendareventeditor).

The default set of fields are:

```
    {name: "startHours", title: "From",      editorType: "SelectItem", type: "integer", width: 60},
    {name: "startMinutes", showTitle: false, editorType: "SelectItem", type: "integer", width: 60},
    {name: "startAMPM", showTitle: false, type: "select", width: 60},
    {name: "invalidDate", type: "blurb", colSpan: 4, visible: false}
    {name: "endHours", title: "To",        editorType: "SelectItem", type: "integer", width: 60},
    {name: "endMinutes", showTitle: false, editorType: "SelectItem", type: "integer", width: 60},
    {name: "endAMPM", showTitle: false, type: "select", width: 60},
    {name: "name", title: "Name", type: "text", colSpan: 4},
    {name: "description", title: "Description", type: "textArea", colSpan: 4, height: 50}
 
```
See the Customized Binding example below for more information on altering default datasource fields within forms.

### Groups

- editing

**Flags**: IR

---
## Attr: Calendar.removeButtonTitle

### Description
The title for the [Remove button](#attr-calendarremovebutton) in the [event editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.firstDayOfWeek

### Description
The numeric day (0-6, Sunday-Saturday) which the calendar should consider as the first day of the week in multi-day views, and in the popup [DateChooser](#attr-calendardatechooser).

If unset, the default is taken from the current locale.

### Groups

- date

**Flags**: IRW

---
## Attr: Calendar.showColumnLayouts

### Description
When true, causes [layouts](#attr-calendarcolumnlayout) to be added to each column in vertical views. In this mode, eventCanvases are stacked in these layouts, filling width and auto-sizing vertically to content, rather than being placed, sized and overlapped according to their times.

Because times are ignored in this mode, various behaviors are switched off automatically; for example, the [time-column](#attr-calendarshowlabelcolumn) is hidden and event-canvases cannot be [resized](#attr-calendarcanresizeevents) or rendered [on-demand](#attr-calendarrendereventsondemand).

### Groups

- appearance

**Flags**: IR

---
## Attr: Calendar.minLaneHeight

### Description
The minimum height for Lanes in a Timeline. When events have a [fixed height](#attr-calendarfixedeventheight), Lanes will size just tall enough to accommodate their events but will not shrink below this minimum height.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.eventEditorButtonLayout

### Description
An [AutoChild](../reference.md#type-autochild) of type [HLayout](../reference.md#class-hlayout) which houses the [Save](#attr-calendarsavebutton), [Remove](#attr-calendarremovebutton) and [Cancel](#attr-calendarcancelbutton) buttons in the [eventEditor](#attr-calendareventeditor).

**Flags**: R

---
## Attr: Calendar.renderEventsOnDemand

### Description
When set to true, the default, each [event](EventCanvas.md#class-eventcanvas) is rendered as it appears in the viewport. If set to false, all events are rendered up-front, whenever the current range changes.

Has no effect when [showColumnLayouts](#attr-calendarshowcolumnlayouts) is true.

**Flags**: IR

---
## Attr: Calendar.weekPrefix

### Description
The text to appear before the week number in the title of [week-based](../reference_2.md#type-timeunit) [HeaderLevel](../reference_2.md#object-headerlevel)s when this calendar is showing a timeline.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.sizeToWorkday

### Description
When [showWorkday](#attr-calendarshowworkday) is true, attempt to resize rows in the day and week views so that the [workday hours](#attr-calendarworkdaystart) fill the visible viewport-height, and the whole workday is visible without scrolling. If the Calendar is resized, the row-size is recalculated to keep the workday hours visible.

Note that row-heights will not shrink below the [Calendar.minRowHeight](#attr-calendarminrowheight), so the entire workday may not be visible without scrolling if the workday is long or the viewport-height is insufficient.

### Groups

- workday

### See Also

- [Calendar.styleWorkday](#attr-calendarstyleworkday)
- [Calendar.scrollToWorkday](#attr-calendarscrolltoworkday)
- [Calendar.limitToWorkday](#attr-calendarlimittoworkday)
- [Calendar.minRowHeight](#attr-calendarminrowheight)

**Flags**: IRW

---
## Attr: Calendar.sublaneNameField

### Description
The name of the field which will determine the [sublane](Lane.md#attr-lanesublanes) in which this event will be displayed, within its parent Lane, in [Timeline](../reference.md#class-timeline)s and in the [day view](#attr-calendardayview), if [Calendar.showDayLanes](#attr-calendarshowdaylanes) is true.

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.chosenDate

### Description
The date for which events are displayed in the day, week, and month tabs of the calendar. Default is today.

### Groups

- date

**Flags**: IRW

---
## Attr: Calendar.monthMoreEventsMenu

### Description
AutoChild Menu, shown when a user clicks the [more events](#attr-calendarmonthmoreeventslinktitle) link in a cell of the [monthView](#attr-calendarmonthview). Items in this menu represent additional events, not already displayed in the cell, and clicking them fires the [eventClick](#method-calendareventclick) notification.

**Flags**: R

---
## Attr: Calendar.timeFormatter

### Description
Display format to use for the time portion of events' date information. By default, times are displayed in the global format, including the influence of the global [24-hour](Time.md#classattr-timeuse24hourtime) option, which is true by default. P> Note that this display setting does not affect the way in which time values are edited in the [eventEditor](#attr-calendareventeditor) - see [Calendar.twentyFourHourTime](#attr-calendartwentyfourhourtime) for more information.

**Flags**: IRW

---
## Attr: Calendar.monthView

### Description
[CalendarView](CalendarView.md#class-calendarview) used to display events that pertain to a given month.

**Flags**: R

---
## Attr: Calendar.showHeaderHovers

### Description
When [showViewHovers](#attr-calendarshowviewhovers) is true, dictates whether to display hover prompts when the mouse rolls over the [header levels](#attr-calendarheaderlevels) in a [CalendarView](CalendarView.md#class-calendarview).

The content of the hover is determined by a call to [Calendar.getHeaderHoverHTML](#method-calendargetheaderhoverhtml), which can be overridden to return custom results;

**Flags**: IR

---
## Attr: Calendar.eventSnapGap

### Description
The number of minutes that determines the positions to which events will snap when rendered, and when moved or resized with the mouse.

If unset (the default), all views will snap to each cell boundary; 30 minutes in a default vertical view, or one [column](#attr-calendartimelinegranularity) in a default Timeline.

If set to zero, views will snap to one of a set of known "sensible" defaults: for a default vertical, this will be 5 minutes. For timelines, the eventSnapGap is automatic depending on the current [Calendar.timelineGranularity](#attr-calendartimelinegranularity). If [Calendar.timelineUnitsPerColumn](#attr-calendartimelineunitspercolumn) is greater than 1, the snapGap is set to one unit of the current granularity. So, a cell-resolution of 15 minutes would snap to every minute, assuming there are at least 15 pixels per column. Otherwise, the snapGap is either 15 minutes, 1 hour, one day or one month, depending on granularity.

If any other value is specified, it is used where possible.

If the specified or calculated value is less than the time covered by a single pixel in the current view, then it can't be represented. In this case, it is rounded up to the lowest of a set of "sensible" time-spans that _can_ be represented: one of \[1, 5, 10, 15, 20, 30, 60, 120, 240, 360, 480, 720, 1440\].

For example - a Timeline showing "day" columns cannot support an eventSnapGap of 1 minute, unless each column is at least 1440 pixels wide - if the columns were only 150px wide, then each pixel would represent around 9.6 minutes, which would result in unpleasant and unexpected time-offsets when dragging events. So, the calculated eventSnapGap will be rounded up to the nearest "sensible" time-span - in this case, 10 minutes. If the columns were only 60px wide, it would be 30 minutes.

### Groups

- editing

**Flags**: IRW

---
## Attr: Calendar.newEventWindowTitle

### Description
The title-text displayed in the popup event dialog/editor for new events.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.addEventButtonHoverText

### Description
The text to be displayed when a user hovers over the [add event](#attr-calendaraddeventbutton) toolbar button

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.longEventLayoutStyleName

### Description
The base name for the CSS class applied to the layouts that show [long-events](CalendarView.md#attr-calendarviewlongeventslayout) in the various [CalendarViews](CalendarView.md#class-calendarview).

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.nameField

### Description
The name of the name field on a [CalendarEvent](../reference.md#object-calendarevent).

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.monthViewTitle

### Description
The title for the [month view](#attr-calendarmonthview).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.useSublanes

### Description
When set to true, causes [lanes](#attr-calendarlanes) to be sub-divided according to their set of [sublanes](Lane.md#attr-lanesublanes).

**Flags**: IR

---
## Attr: Calendar.allDayField

### Description
The name of the field on a [CalendarEvent](../reference.md#object-calendarevent) which indicates an event should fill the whole day. Such events are displayed in a separate [long-events layout](CalendarView.md#attr-calendarviewlongeventslayout), which appears beneath the headers in the [week](#attr-calendarweekview) and [day](#attr-calendardayview) views and does not scroll with the main body. In the [month](#attr-calendarmonthview) view, these layouts appear beneath the headers for each week, and very long events might wrap from one week to the next.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.eventSublaneFieldTitle

### Description
The title for the [sublaneNameField](#attr-calendarsublanenamefield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [event editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showLaneRollOver

### Description
When set to true, causes [Timelines](#attr-calendartimelineview) to highlight the Lane under the mouse with the "Over" style.

**Flags**: IRW

---
## Attr: Calendar.showEventDescriptions

### Description
When rendering the [canvas](#attr-calendareventcanvas) for an event, whether to show the [body area](EventCanvas.md#attr-eventcanvasshowbody), typically containing brief details of the event - [by default](#method-calendargeteventbodyhtml), [its description](#attr-calendardescriptionfield).

The default is true - if set to false, the event's [header](EventCanvas.md#attr-eventcanvasshowheader) will fill the canvas.

**Flags**: IR

---
## Attr: Calendar.weekViewTitle

### Description
The title for the [week view](#attr-calendarweekview).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showLaneFieldHovers

### Description
When [showViewHovers](#attr-calendarshowviewhovers) is true, dictates whether to display hover prompts when the mouse moves over the cells in a [laneField](#attr-calendarlanefields).

The content of the hover is determined by a call to [Calendar.getCellHoverHTML](#method-calendargetcellhoverhtml), which can be overridden to return custom results. Note that getCellHoverHTML() is also called when the mouse moves over cells if [showCellHovers](#attr-calendarshowcellhovers) is true - when called for a laneField, no "date" parameter is passed to that method.

**Flags**: IRW

---
## Attr: Calendar.canDragEventField

### Description
Name of the field on each [CalendarEvent](../reference.md#object-calendarevent) that determines whether an [EventCanvas](EventCanvas.md#class-eventcanvas) can be moved or resized by dragging with the mouse. Note that [canEditEvents](#attr-calendarcaneditevents) must be true for dragging to be allowed.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.weekEventBorderOverlap

### Description
Augments the width of week event windows slightly to avoid duplicate adjacent borders between events.

### Groups

- appearance

**Flags**: IR

---
## Attr: Calendar.includeRangeCriteria

### Description
When set to true, the default, the fetches issued by navigating around in the various views are limited to the accessible date-range in the current view - as you change the current date-range, a fetch is only issued if the new range is not entirely within the previous range.

For example, navigating in the [Calendar.monthView](#attr-calendarmonthview) will fetch all events in the range of 5 or 6 weeks that cover that month. If you then change to the [day](#attr-calendardayview) or [week](#attr-calendarweekview) views, no fetches will be issued until you navigate outside of the 5 or 6 weeks initially fetched by the Month view.

**Flags**: IR

---
## Attr: Calendar.defaultTimelineColumnSpan

### Description
The number of columns of the [timelineGranularity](#attr-calendartimelinegranularity) to give the timeline by default if no [endDate](#attr-calendarenddate) is provided. The default is 20.

**Flags**: IR

---
## Attr: Calendar.eventCanvasContextButton

### Description
The context button that snaps to the top-right of an event canvas on rollover and shows a custom [context menu](#method-calendargeteventcanvasmenuitems) when clicked.

**Flags**: A

---
## Attr: Calendar.eventEditorDateFieldTitle

### Description
The title for the Date-field in the [eventEditor](#method-calendarshoweventeditor) that allows for changing the logical start-date of an event, along with its start and end times, when editing events in the [day](#attr-calendardayview) and [week](#attr-calendarweekview) views.

### Groups

- editing
- i18nMessages

**Flags**: IR

---
## Attr: Calendar.startDateField

### Description
The name of the start date field on a [CalendarEvent](../reference.md#object-calendarevent).

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.durationField

### Description
The name of the [duration](CalendarEvent.md#attr-calendareventduration) field on a [CalendarEvent](../reference.md#object-calendarevent).

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.workdayEnd

### Description
When using [Calendar.showWorkday](#attr-calendarshowworkday):true, `workdayStart` and `workdayEnd` specify the time of day when the workday starts and ends, specified as a String acceptable to [Time.parseInput](Time.md#classmethod-timeparseinput).

Both start and end time must fall on a 30 minute increment (eg 9:30, but not 9:45).

The hours of the workday can be customized for particular dates by providing implementations of [Calendar.getWorkdayStart](#method-calendargetworkdaystart) and [Calendar.getWorkdayEnd](#method-calendargetworkdayend).

### Groups

- workday
- date

**Flags**: IR

---
## Attr: Calendar.eventScreen

### Description
Screen to create (via [createScreen()](RPCManager.md#classmethod-rpcmanagercreatescreen)) in lieu of calling [Calendar.createEventCanvasComponent](#method-calendarcreateeventcanvascomponent).

If this calendar has a [dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource), the created screen is provided with a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) that includes the event being shown. Be sure the event screen meets these [requirements](Canvas.md#attr-canvasautopopulatedata) to utilize the `dataContext`.

**Flags**: IR

---
## Attr: Calendar.canResizeTimelineEvents

### Description
Can [Timeline](../reference.md#class-timeline) events be stretched by their left and right edges?

**Deprecated**

**Flags**: IR

---
## Attr: Calendar.scrollToWorkday

### Description
If set, and [showWorkday](#attr-calendarshowworkday) is true, automatically scrolls the [day](#attr-calendardayview) and [week](#attr-calendarweekview) views to the start of the [workday](#attr-calendarworkdaystart) when the calendar is first displayed and whenever the user changes to a different day or week.

### Groups

- workday

### See Also

- [Calendar.styleWorkday](#attr-calendarstyleworkday)
- [Calendar.sizeToWorkday](#attr-calendarsizetoworkday)
- [Calendar.limitToWorkday](#attr-calendarlimittoworkday)

**Flags**: IRW

---
## Attr: Calendar.canEditSublaneField

### Description
Name of the field on each [CalendarEvent](../reference.md#object-calendarevent) that determines whether that event can be moved between individual [sublanes](Lane.md#attr-lanesublanes) in a [Lane](../reference.md#object-lane).

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.minLaneWidth

### Description
When showing [vertical lanes](#attr-calendarshowdaylanes) in the [Calendar.dayView](#attr-calendardayview), this attribute sets the minimum width of each column or field.

**Flags**: IR

---
## Attr: Calendar.selectChosenDate

### Description
When true, shows the current [chosenDate](#attr-calendarchosendate) in a selected style in the [month view](#attr-calendarmonthview). Has no effect in other views.

### Groups

- visibility

**Flags**: IRW

---
## Attr: Calendar.workdays

### Description
Array of days that are considered workdays when [Calendar.showWorkday](#attr-calendarshowworkday) is true. Has no effect if [Calendar.dateIsWorkday](#method-calendardateisworkday) is implemented.

### Groups

- workday

**Flags**: IR

---
## Attr: Calendar.cancelButtonTitle

### Description
The title for the [Cancel button](#attr-calendarcancelbutton) in the [event editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.indicatorStyleName

### Description
CSS style to apply to the [canvases](#attr-calendarindicatorcanvas) created for each specified [indicator](#attr-calendarindicators).

**Flags**: IRW

---
## Attr: Calendar.eventLaneFieldTitle

### Description
The title for the [laneNameField](#attr-calendarlanenamefield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showIndicatorsInFront

### Description
In [indicator lines](#attr-calendarindicators) are showing, this attribute affects where in the z-order their canvases will be rendered: either in front of, or behind normal calendar events.

**Flags**: IR

---
## Attr: Calendar.backButtonIconSrc

### Description
The icon to show in the [month-button](#attr-calendarmonthbutton) on Handsets when the [month view](#attr-calendarmonthview) is the current visible view.

**Flags**: IR

---
## Attr: Calendar.showViewHovers

### Description
When set to true, the default value, causes the Calendar to show customizable hovers when the mouse moves over various areas of a CalendarView.

See [showEventHovers](#attr-calendarshoweventhovers), [showZoneHovers](#attr-calendarshowzonehovers), [showHeaderHovers](#attr-calendarshowheaderhovers), [showCellHovers](#attr-calendarshowcellhovers), [showLaneFieldHovers](#attr-calendarshowlanefieldhovers), [showDragHovers](#attr-calendarshowdraghovers) for further configuration options.

**Flags**: IRW

---
## Attr: Calendar.monthMoreEventsLinkTitle

### Description
The title of the link shown in a cell of a [month view](#attr-calendarmonthview) when there are too many events to be displayed at once.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, eventCount, is available and represents the number of events that are not currently displayed and that will appear in the menu displayed when the More Events link is clicked.

The default value is a string like "+ 3 more...".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showWeekView

### Description
Whether to show the Week view.

### Groups

- appearance

**Flags**: IR

---
## Attr: Calendar.backButtonTitle

### Description
The title of the [month](#attr-calendarmonthbutton) on Handsets when the [month view](#attr-calendarmonthview) is the current visible view.

When the month view is not the current visible view, the title for the month button is set according to the value of [Calendar.monthButtonTitle](#attr-calendarmonthbuttontitle).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.controlBarIconSize

### Description
The size of the various icons displayed in the [controlsBar](#attr-calendarcontrolsbar) of this Calendar.

**Flags**: IR

---
## Attr: Calendar.canRemoveEvents

### Description
If true, users can remove existing events. Defaults to [Calendar.canEditEvents](#attr-calendarcaneditevents).

### Groups

- allowedOperations

**Flags**: IR

---
## Attr: Calendar.eventDurationUnitFieldTitle

### Description
The title for the [duration unit field](#attr-calendardurationunitfield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.canCreateOtherDayEvents

### Description
When [Calendar.showOtherDays](#attr-calendarshowotherdays) is true, determines whether clicking in a Month-view body-cell that represents a date outside the selected month will open the [event-editor window](#attr-calendareventeditor) at the cell's location.

Note that, when [Calendar.otherDayClickNavigation](#attr-calendarotherdayclicknavigation) is also true, the Month-view first switches to the month of the clicked date before displaying the event-editor. This causes the editor to open in a different cell than the one clicked and may be unexpected to users.

**Flags**: IRW

---
## Attr: Calendar.showZones

### Description
Set to true to render any defined [zones](#attr-calendarzones) into [timeline views](#attr-calendartimelineview).

**Flags**: IRW

---
## Attr: Calendar.showIndicators

### Description
Set to true to render any defined [indicators](#attr-calendarindicators) into [timeline views](#attr-calendartimelineview).

**Flags**: IRW

---
## Attr: Calendar.showOtherDays

### Description
If set to true, in the [month view](#attr-calendarmonthview), days that fall in an adjacent month are still shown with a header and body area, and are interactive. Otherwise days from other months are rendered in the [Calendar.otherDayBlankStyle](#attr-calendarotherdayblankstyle) and are non-interactive.

### Groups

- visibility

**Flags**: IR

---
## Attr: Calendar.eventCanvasVResizer

### Description
The resizer image that snaps to the bottom of event canvases in [day](#attr-calendardayview) and [week](#attr-calendarweekview) views, allowing them to be resized vertically by dragging with the mouse.

**Flags**: A

---
## Attr: Calendar.minutesPerRow

### Description
The number of minutes per row in [day](#attr-calendardayview) and [week](#attr-calendarweekview) views. The default of 30 minutes shows two rows per hour. Note that this value must divide into 60.

**Flags**: IR

---
## Attr: Calendar.sizeEventsToGrid

### Description
If true, events will be sized to the grid, even if they start and/or end at times between grid cells.

**Flags**: IR

---
## Attr: Calendar.showLabelColumn

### Description
When set to false, hides the frozen Label-Column in vertical [CalendarView](CalendarView.md#class-calendarview)s.

Always false when [showColumnLayouts](#attr-calendarshowcolumnlayouts) is true.

**Flags**: IR

---
## Attr: Calendar.showDayView

### Description
Whether to show the Day view.

### Groups

- appearance

**Flags**: IR

---
## Attr: Calendar.minRowHeight

### Description
The minimum height of time-rows in vertical calendar views. Rows will not shrink below this height when [Calendar.sizeToWorkday](#attr-calendarsizetoworkday) is true, meaning that a Calendar with a long workday may not be able to fit all workday rows in the viewport at once, and scrolling may be necessary.

To prevent users from scrolling beyond the workday hours, see [Calendar.limitToWorkday](#attr-calendarlimittoworkday).

**Flags**: IRW

---
## Attr: Calendar.canDeleteEvents

### Description
If true, users can delete existing events. Defaults to [Calendar.canEditEvents](#attr-calendarcaneditevents).

### Groups

- allowedOperations

**Deprecated**

**Flags**: IR

---
## Attr: Calendar.dayHeaderBaseStyle

### Description
The base name for the CSS class applied to the day headers of the month view. This style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.columnLayout

### Description
When [Calendar.showColumnLayouts](#attr-calendarshowcolumnlayouts) is true, the layouts added to each column to stack events.

**Flags**: A

---
## Attr: Calendar.monthButtonIconSrc

### Description
The icon to show next to the month-name in the [month button](#attr-calendarmonthbutton), used for showing and hiding the [month view](#attr-calendarmonthview) on Handsets.

**Flags**: IR

---
## Attr: Calendar.showEventCanvasComponents

### Description
Whether [event-canvases](#attr-calendareventcanvas) should show a custom widget as content, rather than the default [header](EventCanvas.md#attr-eventcanvasshowheader) and [body](EventCanvas.md#attr-eventcanvasshowbody) HTML.

### See Also

- [Calendar.createEventCanvasComponent](#method-calendarcreateeventcanvascomponent)
- [Calendar.updateEventCanvasComponent](#method-calendarupdateeventcanvascomponent)

**Flags**: IR

---
## Attr: Calendar.zoneStyleName

### Description
CSS style to apply to the [canvases](#attr-calendarzonecanvas) created for each specified [zone](#attr-calendarzones).

**Flags**: IRW

---
## Attr: Calendar.invalidDateMessage

### Description
The message to display in the [Calendar.eventEditor](#attr-calendareventeditor) when the 'To' date is greater than the 'From' date and a save is attempted.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.nextButtonHoverText

### Description
The text to be displayed when a user hovers over the [next](#attr-calendarnextbutton) toolbar button

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.longEventDragOpacity

### Description
The default [opacity percentage](Canvas.md#attr-canvasopacity) of [long-events](#attr-calendarallowlongevents) while being dragged.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.eventDurationFieldTitle

### Description
The title for the [duration field](#attr-calendardurationfield) in the quick [event dialog](#attr-calendareventdialog) and the detailed [editor](#attr-calendareventeditor).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.newLongEventName

### Description
The default name for new [long-events](#attr-calendarallowlongevents).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.eventWindowStyleField

### Description
The name of the field used to override [Calendar.eventWindowStyle](#attr-calendareventwindowstyle) for an individual [CalendarEvent](../reference.md#object-calendarevent). See [CalendarEvent.eventWindowStyle](CalendarEvent.md#attr-calendareventeventwindowstyle).

### Groups

- calendarEvent
- appearance

**Deprecated**

**Flags**: IR

---
## Attr: Calendar.showDatePickerButton

### Description
Set to false to hide the [Calendar.datePickerButton](#attr-calendardatepickerbutton) that allows selecting a new base date for this Calendar.

**Flags**: IRW

---
## Attr: Calendar.canEditLaneField

### Description
Name of the field on each [CalendarEvent](../reference.md#object-calendarevent) that determines whether that event can be moved between lanes.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.canReorderLanes

### Description
If true, lanes can be reordered by dragging their [laneFields](#attr-calendarlanefields) with the mouse.

**Flags**: IR

---
## Attr: Calendar.laneNameField

### Description
The name of the field which will determine the [lane](#attr-calendarlanes) in which a given event will be displayed in [Timeline](../reference.md#class-timeline)s and in the [day view](#attr-calendardayview), if [Calendar.showDayLanes](#attr-calendarshowdaylanes) is true.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.eventCanvasGripperIcon

### Description
Icon used as the default eveng gripper icon.

**Flags**: A

---
## Attr: Calendar.canEditEvents

### Description
If true, users can edit existing events.

### Groups

- allowedOperations

**Flags**: IR

---
## Attr: Calendar.trailingDateField

### Description
The name of the trailing date field for each event. When this attribute and [Calendar.leadingDateField](#attr-calendarleadingdatefield) are present in the data, a line extends out from the event showing the extent of the leading and trailing dates - useful for visualizing a pipeline of events where some can be moved a certain amount without affecting others.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.showDayLanes

### Description
If set to true, the [day view](#attr-calendardayview) uses [Calendar.lanes](#attr-calendarlanes) to render multiple vertical "lanes" within the day, very much like a vertical [Timeline](../reference.md#class-timeline).

Day lanes are useful for showing events for various entities on the same day - agendas for various staff members, for example, or delivery schedules for a fleet of trucks.

Each day lane is self-contained, showing in a column with a header and individual events are placed in [appropriate lanes](CalendarEvent.md#attr-calendareventlane), respecting padding and overlapping. If [Calendar.canEditEvents](#attr-calendarcaneditevents) is true, events can be drag-moved or drag-resized from their top and bottom edges, within the containing lane. To allow events to be dragged from one lane into another, see [Calendar.canEditLane](#attr-calendarcaneditlane).

**Flags**: IR

---
## Attr: Calendar.allowDurationEvents

### Description
When set to true, allows events to be managed by duration, as well as by end date. Values can be set for [duration](CalendarEvent.md#attr-calendareventduration) and [duration unit](CalendarEvent.md#attr-calendareventdurationunit) on each event, and are then maintained, instead of the end date, when alterations are made to the event via editors or dragging with the mouse.

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IRW

---
## Attr: Calendar.eventCanvasCloseButton

### Description
The close button that snaps to the top-right of an event canvas on rollover and allows an event to be removed from a [CalendarView](CalendarView.md#class-calendarview).

**Flags**: A

---
## Attr: Calendar.eventStyleName

### Description
The base name for the CSS class applied to [events](#attr-calendareventcanvas) when they're rendered in calendar views. This style will have "Header" and "Body" appended to it, according to which part of the event window is being styled. For example, to style the header, define a CSS class called 'eventWindowHeader'.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.eventCanvasCloseIconSize

### Description
The size of the icon in the [close-button](#attr-calendareventcanvasclosebutton) floated over events on rollover.

**Flags**: IR

---
## Attr: Calendar.workdayStart

### Description
When using [Calendar.showWorkday](#attr-calendarshowworkday):true, `workdayStart` and `workdayEnd` specify the time of day when the workday starts and ends, specified as a String acceptable to [Time.parseInput](Time.md#classmethod-timeparseinput).

Both start and end time must fall on a 30 minute increment (eg 9:30, but not 9:45).

The hours of the workday can be customized for particular dates by providing implementations of [Calendar.getWorkdayStart](#method-calendargetworkdaystart) and [Calendar.getWorkdayEnd](#method-calendargetworkdayend).

### Groups

- workday
- date

**Flags**: IR

---
## Attr: Calendar.canCreateEvents

### Description
If true, users can create new events.

### Groups

- allowedOperations

**Flags**: IR

---
## Attr: Calendar.canDragCreateEvents

### Description
A boolean value controlling whether new events of varying length can be created by dragging the cursor. By default, this is false for Touch devices and true otherwise.

**Flags**: IRW

---
## Attr: Calendar.showDragHovers

### Description
When [showViewHovers](#attr-calendarshowviewhovers) is true, dictates whether to display hover prompts when an event is being dragged with the mouse.

The content of the hover is determined by a call to [Calendar.getDragHoverHTML](#method-calendargetdraghoverhtml), which can be overridden to return custom results; by default, it returns the date range of the drag canvas as a string.

**Flags**: IRW

---
## Attr: Calendar.zones

### Description
An array of CalendarEvent instances representing pre-defined periods of time to be highlighted in [timeline views](#attr-calendartimelineview). Each zone renders out a [zone canvas](../reference.md#class-zonecanvas), a special, non-interactive subclass of [EventCanvas](EventCanvas.md#class-eventcanvas), which spans all lanes and draws behind any normal, interactive events in the zorder.

The default [style](#attr-calendarzonestylename) for these components renders them semi-transparent and with a bottom-aligned title label.

**Flags**: IRW

---
## Attr: Calendar.longEventLayoutSpace

### Description
The amount of space available in [long-event layouts](CalendarView.md#attr-calendarviewlongeventslayout) for drag-click and drag-creation of new events. Represents the default height of long-event layouts that have no events, and additional height in layouts with events.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Calendar.dateFormatter

### Description
Date formatter for displaying events. Default is to use the system-wide default short date format, configured via [DateUtil.setShortDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdisplayformat). Specify any valid [DateDisplayFormat](../reference.md#type-datedisplayformat).

**Flags**: IRW

---
## Attr: Calendar.showWeekends

### Description
Suppresses the display of weekend days in the [week](#attr-calendarweekview), [month](#attr-calendarmonthview) and [timeline](#attr-calendartimelineview) views, and disallows the creation of events on weekends. Which days are considered weekends is controlled by [Calendar.weekendDays](#attr-calendarweekenddays).

### Groups

- visibility

**Flags**: IRW

---
## Attr: Calendar.timelineUnitsPerColumn

### Description
How many units of [Calendar.timelineGranularity](#attr-calendartimelinegranularity) each cell represents.

**Flags**: IR

---
## Attr: Calendar.otherDayClickNavigation

### Description
When [Calendar.showOtherDays](#attr-calendarshowotherdays) is true, this attribute determines whether the month-view should change month when cells representing days in the previous or following month are clicked.

**Flags**: IRW

---
## Attr: Calendar.dateLabel

### Description
The [AutoChild](../reference.md#type-autochild) [Label](Label.md#class-label) used to display the current date or range above the selected calendar view.

**Flags**: IR

---
## Attr: Calendar.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_2.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

**Flags**: IRW

---
## Attr: Calendar.showPreviousButton

### Description
Set to false to hide the [Previous](#attr-calendarpreviousbutton) button.

**Flags**: IRW

---
## Attr: Calendar.dayViewTitle

### Description
The title for the [day view](#attr-calendardayview).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.descriptionField

### Description
The name of the description field on a [CalendarEvent](../reference.md#object-calendarevent).

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.showMonthView

### Description
Whether to show the Month view.

### Groups

- appearance

**Flags**: IR

---
## Attr: Calendar.timelineViewTitle

### Description
The title for the [timeline view](#attr-calendartimelineview).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.showQuickEventDialog

### Description
Determines whether the quick event dialog is displayed when a time is clicked. If this is false, the full event editor is displayed.

### Groups

- editing

**Flags**: IR

---
## Attr: Calendar.eventHeaderWrap

### Description
When rendering the [canvas](#attr-calendareventcanvas) for an event, whether to allow the content of the [header area](EventCanvas.md#attr-eventcanvasshowheader) to wrap to multiple lines.

The default is true - if set to false, the header area is [fixed](#attr-calendareventheaderheight), unless [Calendar.showEventDescriptions](#attr-calendarshoweventdescriptions) is false, in which case the header area fills the canvas.

**Flags**: IR

---
## Attr: Calendar.controlsBar

### Description
An [HLayout](../reference.md#class-hlayout) shown above the Calendar views and displaying a set of controls for interacting with the current view - namely, the [next](#attr-calendarnextbutton), [previous](#attr-calendarpreviousbutton) and [add](#attr-calendaraddeventbutton) buttons, the [date label](#attr-calendardatelabel) and the [date-picker](#attr-calendardatepickerbutton) icon.

**Flags**: IR

---
## Attr: Calendar.twentyFourHourTime

### Description
Dictates whether times throughout the widget are formatted and edited as 24-hour values. If unset, defaults to the [global 24-hour setting](Time.md#classattr-timeuse24hourtime). If set, and no [local formatter](#attr-calendartimeformatter) is installed, causes the Calendar to choose an appropriate builtin formatter.

**Flags**: IR

---
## Attr: Calendar.showDetailFields

### Description
Whether to show fields marked `detail:true` when a DataBoundComponent is given a DataSource but no `component.fields`.

The `detail` property is used on DataSource fields to mark fields that shouldn't appear by default in a view that tries to show many records in a small space.

### Groups

- databinding

**Flags**: IR

---
## Attr: Calendar.autoFetchTextMatchStyle

### Description
If [Calendar.autoFetchData](#attr-calendarautofetchdata) is `true`, this attribute allows the developer to specify a textMatchStyle for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

### Groups

- databinding

**Flags**: IR

---
## Attr: Calendar.datePickerHoverText

### Description
The text to be displayed when a user hovers over the [date picker](#attr-calendardatepickerbutton) toolbar button

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Calendar.initialCriteria

### Description
Criteria to be used when [Calendar.autoFetchData](#attr-calendarautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: Calendar.showControlsBar

### Description
If false the controls bar at the top of the calendar will not be displayed - this means that the [Calendar.controlsBar](#attr-calendarcontrolsbar) will be hidden, so the autoChildren ([Calendar.previousButton](#attr-calendarpreviousbutton), [Calendar.dateLabel](#attr-calendardatelabel), [Calendar.nextButton](#attr-calendarnextbutton), [Calendar.addEventButton](#attr-calendaraddeventbutton), and [Calendar.datePickerButton](#attr-calendardatepickerbutton)) will not be created or shown.

**Flags**: IR

---
## Attr: Calendar.showTimelineView

### Description
If set to true, show the [Timeline view](#attr-calendartimelineview).

**Flags**: IRW

---
## Attr: Calendar.endDate

### Description
The end date of the calendar timeline view. Has no effect in other views.

To set different [start](#attr-calendarstartdate) and end dates after initial draw, see [setTimelineRange](#method-calendarsettimelinerange).

Note that the value you provide may be automatically altered if showing [header-levels](#attr-calendarheaderlevels), to fit to header boundaries.

**Flags**: IR

---
## Attr: Calendar.eventAutoArrange

### Description
If set to true, enables the auto-arrangement of events that share time in the calendar. The default is true.

### Groups

- calendarEvent

**Flags**: IR

---
## Attr: Calendar.eventCanvasHResizer

### Description
The resizer image that snaps to the left and right edges of an editable event canvas in a [Timeline](../reference.md#class-timeline), allowing it to be resized horizontally by dragging with the mouse.

**Flags**: A

---
## Attr: Calendar.endDateField

### Description
The name of the end date field on a [CalendarEvent](../reference.md#object-calendarevent).

### Groups

- calendarEvent

### See Also

- [CalendarEvent](../reference.md#object-calendarevent)

**Flags**: IR

---
## Attr: Calendar.limitToWorkday

### Description
When [showWorkday](#attr-calendarshowworkday) is true, this attribute prevents the user from scrolling vertical views beyond the specified workday [start](#attr-calendarworkdaystart) and [end](#attr-calendarworkdayend) hours.

### Groups

- workday

### See Also

- [Calendar.styleWorkday](#attr-calendarstyleworkday)
- [Calendar.sizeToWorkday](#attr-calendarsizetoworkday)
- [Calendar.scrollToWorkday](#attr-calendarscrolltoworkday)
- [Calendar.minRowHeight](#attr-calendarminrowheight)

**Flags**: IR

---
## Attr: Calendar.disableWeekends

### Description
If true, weekend days appear in a disabled style and events cannot be created on weekends. Which days are considered weekends is controlled by [Calendar.weekendDays](#attr-calendarweekenddays).

### Groups

- visibility

**Flags**: IRW

---
## Method: Calendar.timelineEventMoved

### Description
Called when a Timeline event is moved via dragging by a user. Return false to disallow the move.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that was moved |
| startDate | [Date](#type-date) | false | — | new start date of the passed event |
| endDate | [Date](#type-date) | false | — | new end date of the passed event |
| lane | [Lane](#type-lane) | false | — | the Lane in which this event has been dropped |

### Returns

`[Boolean](#type-boolean)` — return false to disallow the move.

**Deprecated**

---
## Method: Calendar.eventRepositionStart

### Description
Notification fired when a user drags an EventCanvas. Return false to cancel the drag.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that's about to be moved |

### Returns

`[Boolean](#type-boolean)` — return false to cancel the default drag start behavior

---
## Method: Calendar.getWorkdayEnd

### Description
Returns the end of the working day on the passed date. By default, this method returns the value of [workdayEnd](#attr-calendarworkdayend).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance |
| laneName | [String](#type-string) | true | — | the name of the relevant lane - only passed for dayView with showDayLanes: true |

### Returns

`[String](#type-string)` — any parsable time-string

---
## Method: Calendar.setZones

### Description
Sets the [zones](#attr-calendarzones) used to highlight areas of this calendar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zones | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | array of zones to display |

---
## Method: Calendar.getMonthViewHoverHTML

### Description
This method returns the hover HTML to be displayed when the user hovers over a cell displayed in the calendar month view tab.

Default implementation will display a list of the events occurring on the date the user is hovering over. Override for custom behavior. Note that returning null will suppress the hover altogether.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | Date the user is hovering over |
| events | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | array of events occurring on the current date. May be empty. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML string to display

---
## Method: Calendar.updateEventCanvasComponent

### Description
Called from [EventCanvas.setEvent](EventCanvas.md#method-eventcanvassetevent) when [Calendar.showEventCanvasComponents](#attr-calendarshoweventcanvascomponents) is true and the eventCanvas already has a [component](#method-calendarcreateeventcanvascomponent). This method is expected to update the passed `component` as necessary, based on the [current event](EventCanvas.md#attr-eventcanvasevent).

By default, if the passed `component` has methods called `setEvent` or `setData`, those methods are called automatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [EventCanvas](#type-eventcanvas) | false | — | the eventCanvas to update the component for |
| component | [Canvas](#type-canvas) | false | — | the component to be updated the canvas in question |

### See Also

- [Calendar.createEventCanvasComponent](#method-calendarcreateeventcanvascomponent)

---
## Method: Calendar.adjustCriteria

### Description
Gets the criteria to use when the calendar date ranges shift. This would be called, for example, when the next button is clicked and new events may need to be fetched. Override this function to add any custom criteria to the default criteria constructed by the calendar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultCriteria | [Criterion](#type-criterion) | false | — | default criteria generated by the calendar |

### Returns

`[Criterion](#type-criterion)` — modified criteria

---
## Method: Calendar.getLongEventLayoutHoverHTML

### Description
Returns the text to be displayed in a [hover](Canvas.md#attr-canvasshowhover) when the mouse is held over the [separate layout](CalendarView.md#attr-calendarviewlongeventslayout) where [long-events](#method-calendarislongevent) are displayed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| layout | [Canvas](#type-canvas) | false | — | the longEventsLayout over which the mouse is hovered |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the event is being rendered |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to display in the hover for this longEventsLayout

---
## Method: Calendar.getSublaneEvents

### Description
For views that support [lanes](#attr-calendarlanes) and allow [sublanes](#attr-calendarusesublanes), returns the array of events in the current dataset that apply to the passed lane and sublane in the passed or current view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [Lane](#type-lane)|[String](#type-string) | false | — | lane object or name to get the events for |
| sublane | [Lane](#type-lane)|[String](#type-string) | false | — | sublane object or name to get the events for |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the passed sublane lives - uses the selected view if unset |

### Returns

`[Array of CalendarEvent](#type-array-of-calendarevent)` — the list of events that apply to the passed sublane and view

---
## Method: Calendar.dateChanged

### Description
Fires whenever the user changes the current date, including picking a specific date or navigating to a new week or month.

---
## Method: Calendar.getSublane

### Description
Returns the [sublane](Lane.md#attr-lanesublanes) with the passed name, from the [lane](../reference.md#object-lane) with the passed name, in the passed view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [String](#type-string) | false | — | the name of the lane containing the sublane to return |
| sublane | [String](#type-string) | false | — | the name of the sublane to return |
| view | [CalendarView](#type-calendarview) | true | — | the view to get the sublane object from |

### Returns

`[Lane](#type-lane)` — the sublane with the passed name, or null if not found

---
## Method: Calendar.setHideUnusedLanes

### Description
Setter for updating [Calendar.hideUnusedLanes](#attr-calendarhideunusedlanes) after creation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hideUnusedEvents | [boolean](../reference.md#type-boolean) | false | — | whether to hide unused lanes |

---
## Method: Calendar.selectSingleEvent

### Description
Selects a single event in the current view, showing it in a selected style and deselecting any other selected events.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to select |

### Returns

`[Boolean](#type-boolean)` — true if the selection was changed, false otherwise

---
## Method: Calendar.getEventLength

### Description
Returns the length of the passed [event](../reference.md#object-calendarevent) in the passed [unit](../reference_2.md#type-timeunit). If `unit` isn't passed, returns the length of the event in milliseconds.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the length of |
| unit | [TimeUnit](../reference_2.md#type-timeunit) | true | — | the time unit to return the length in, milliseconds if not passed |

---
## Method: Calendar.removeZone

### Description
Removes a [zone](#attr-calendarzones) from the calendar.

Accepts either a [zone object](../reference.md#object-calendarevent) or a string that represents the [name](CalendarEvent.md#attr-calendareventname) of a zone.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zone | [CalendarEvent](#type-calendarevent)|[String](#type-string) | false | — | either the actual CalendarEvent representing the zone, or the name of the zone to remove |

---
## Method: Calendar.setResolution

### Description
Reset the resolution, the header levels and scrollable range, of the timeline view.

`headerLevels` specifies the array of [headers](../reference_2.md#object-headerlevel) to show above the timeline, and the `unit` and `unitCount` parameters dictate the scrollable range (eg, passing "week" and 6 will create a timeline with a scrollable range of six weeks, irrespective of the number of columns that requires, according to the [granularity](#attr-calendartimelinegranularity)).

If the optional `granularityPerColumn` parameter is passed, each column will span that number of units of the granularity, which is determined from the unit of the innermost of the passed headerLevels. For example, to show a span of 12 hours with inner columns that each span 15 minutes, you could pass "hour" and "minute" -based headerLevels, unit and unitCount values of "hour" and 12 respectively, and granularityPerColumn of 15.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| headerLevels | [Array of HeaderLevel](#type-array-of-headerlevel) | false | — | the header levels to show in the timeline |
| unit | [TimeUnit](../reference_2.md#type-timeunit) | false | — | the time unit to use when calculating the range of the timeline |
| unitCount | [Integer](../reference_2.md#type-integer) | false | — | the count of the passed unit that the timeline should span |
| granularityPerColumn | [Integer](../reference_2.md#type-integer) | true | — | how many units of the granularity (the unit of the innermost headerLevel) should each column span? The default is 1. |

---
## Method: Calendar.getPeriodStartDate

### Description
Returns the start of the selected week or month depending on the current calendar view. For the month view, and for the week view when not showing weekends, this will often be a different date than that returned by [Calendar.getVisibleStartDate](#method-calendargetvisiblestartdate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to get the periodStartDate for, or current view if null |

### Returns

`[Date](#type-date)` — period start date

---
## Method: Calendar.showNewEventDialog

### Description
Open the Quick Event dialog to begin editing a new [event](../reference.md#object-calendarevent).

If passed, the event parameter is used as defaults for the new event - in addition, the event's [startDate](#attr-calendarstartdatefield), and its [lane](#attr-calendarlanenamefield), for timeline events, are used to calculate the display location for the dialog.

If this method is called when the Event Dialog is already showing another event, and if changes have been made, a confirmation dialog is displayed and editing of the new event is cancelled unless confirmed.

You can override this method to prevent the default action, perhaps instead showing a custom interface that performs validations or gathers custom data before making a call to [addCalendarEvent](#method-calendaraddcalendarevent) or [updateCalendarEvent](#method-calendarupdatecalendarevent) when the new data is available.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | true | — | defaults for the new event |

---
## Method: Calendar.deselectEvents

### Description
Removes one or more events from the list of selected events in the current view, clearing their selected styles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| events | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | the events to deselect |

### Returns

`[Boolean](#type-boolean)` — true if the selection was changed, false otherwise

---
## Method: Calendar.eventRemoveClick

### Description
Called whenever the close icon of an [event canvas](EventCanvas.md#class-eventcanvas) is clicked in the [day](#attr-calendardayview), [week](#attr-calendarweekview) and [timeline](#attr-calendartimelineview) views, or when the [remove button](#attr-calendarremovebutton) is pressed in the [event editor](#attr-calendareventeditor).

Implement this method to intercept the automatic removal of data. You can return false to prevent the default action (calling [removeEvent()](#method-calendarremoveevent)) and instead take action of your own. For example, returning false from this method and then showing a custom confirmation dialog - if the user cancels, do nothing, otherwise make a call to [removeEvent(event)](#method-calendarremoveevent), passing the event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | event that was clicked on |
| viewName | [String](#type-string) | false | — | view where the event was clicked on: "day", "week" or "month" |

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the removal

### Groups

- monthViewEvents

---
## Method: Calendar.eventResizeMove

### Description
Notification called on each resize during an event drag-resize operation.

The `newEvent` parameter represents the event as it will be after the resize.

Return false to prevent the default action, of resizing the drag canvas to the newEvent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that's being drag-resized |
| newEvent | [CalendarEvent](#type-calendarevent) | false | — | the event as it would be if dropped now |

### Returns

`[Boolean](#type-boolean)` — return false to cancel the default drag resize behavior

---
## Method: Calendar.getLongEventHoverHTML

### Description
Returns the text to be displayed in a [hover](Canvas.md#attr-canvasshowhover) when the mouse is held over a given [event](EventCanvas.md#class-eventcanvas) in the [separate layout](CalendarView.md#attr-calendarviewlongeventslayout) where [long-events](#method-calendarislongevent) are displayed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the description text for |
| layout | [Canvas](#type-canvas) | false | — | the longEventsLayout in which this event is displayed |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the event is being rendered |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to display in the header of an event canvas

---
## Method: Calendar.getEventCanvasMenuItems

### Description
If this method returns a value, it is expected to return an array of [items](../reference_2.md#object-menuitem) applicable to the passed canvas and its event. If an array with valid entries is returned, the rollover [context button](#attr-calendareventcanvascontextbutton) is shown for the passed canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [EventCanvas](#type-eventcanvas) | false | — | the canvas to get menu items for |

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — —

---
## Method: Calendar.showEventCanvasComponent

### Description
Should a component be applied to the passed [canvas](EventCanvas.md#class-eventcanvas) in the [view](EventCanvas.md#attr-eventcanvascalendarview) in which it appears? Return false from this method to override the global value of [showEventCanvasComponents](#attr-calendarshoweventcanvascomponents) for this canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [EventCanvas](#type-eventcanvas) | false | — | should this eventCanvas get a component component? |

### Returns

`[boolean](../reference.md#type-boolean)` — boolean

### See Also

- [Calendar.createEventCanvasComponent](#method-calendarcreateeventcanvascomponent)
- [Calendar.updateEventCanvasComponent](#method-calendarupdateeventcanvascomponent)

---
## Method: Calendar.eventChanged

### Description
Notification fired whenever a user changes an event, whether by dragging the event or by editing it in a dialog.

In a calendar with a DataSource, eventChanged() fires **after** the updated event has been successfully saved to the server

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that changed |

### Groups

- monthViewEvents

---
## Method: Calendar.selectEvents

### Description
Adds one or more events to the list of selected events in the current view, showing them in a selected style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| events | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | the events to add to the selection |

### Returns

`[Boolean](#type-boolean)` — true if the selection was changed, false otherwise

---
## Method: Calendar.eventMoved

### Description
Called when an event is moved via dragging by a user. Return false to disallow the move.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newDate | [Date](#type-date) | false | — | new start date and time that the event is being moved to |
| event | [CalendarEvent](#type-calendarevent) | false | — | the event as it will be after this movement |
| newLane | [String](#type-string) | false | — | the name of the lane into which the event was moved |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to disallow the move.

### Groups

- monthViewEvents

**Deprecated**

---
## Method: Calendar.getDateCellAlign

### Description
When [getDateHTML](#method-calendargetdatehtml) returns a value, this method returns the horizontal alignment for that value in its cell, in the passed view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to get the cell-alignment for |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | the row number containing the date to get the cell-alignment for |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the column number containing the date to get the cell-alignment for |
| view | [CalendarView](#type-calendarview) | false | — | the relevant CalendarView |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — cell-alignment for content in the cell with the passed date and rowNum/colNum

### See Also

- [Calendar.getDateHTML](#method-calendargetdatehtml)
- [Calendar.getDateCellVAlign](#method-calendargetdatecellvalign)
- [Calendar.getDateStyle](#method-calendargetdatestyle)
- [Calendar.getDateCSSText](#method-calendargetdatecsstext)

---
## Method: Calendar.getLane

### Description
Returns the [lane](../reference.md#object-lane) with the passed name, in the passed view

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [String](#type-string) | false | — | the name of the lane to return |
| view | [CalendarView](#type-calendarview) | true | — | the view to get the lane object from |

### Returns

`[Lane](#type-lane)` — the lane with the passed name, or null if not found

---
## Method: Calendar.getLaneFromPoint

### Description
Returns the [Lane](../reference.md#object-lane) at the passed co-ordinates. To get the lane under the mouse, pass null for both x and y.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../reference_2.md#type-integer) | true | — | the x offset into the body of the selected view |
| y | [Integer](../reference_2.md#type-integer) | true | — | the y offset into the body of the selected view. If this param and "x" are both unset, assumes both offsets from the last mouse event. |
| view | [CalendarView](#type-calendarview) | true | — | the view to get the lane from - selected view if not passed |

### Returns

`[Lane](#type-lane)` — the Lane at the passed co-ords in the passed or selected view

---
## Method: Calendar.dayBodyClick

### Description
Called when the body area of a day in the month view is clicked on, outside of any links to a particular event.

By default, if the user can add events, shows a dialog for adding a new event for that day. Return false to cancel this action.

Note that, when [Calendar.otherDayClickNavigation](#attr-calendarotherdayclicknavigation) is true, the calendar will first navigate the Month view to the selected month, before showing the Event Editor dialog at the proper location.

Not called if the day falls outside the current month and [Calendar.showOtherDays](#attr-calendarshowotherdays) is false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | JavaScript Date object representing this day |
| events | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | events that fall on this day |
| calendar | [Calendar](#type-calendar) | false | — | the calendar itself |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | the row number to which the parameter date belongs |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the column number to which the parameter date belongs |

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the default action

### Groups

- monthViewEvents

---
## Method: Calendar.getDayBodyHTML

### Description
Return the HTML to be shown in the body of a day in the month view.

Default is to render a series of links that call [Calendar.eventClick](#method-calendareventclick) to provide details and/or an editing interface for the events.

`getDayBodyHTML()` is not called for days outside of the current month if [Calendar.showOtherDays](#attr-calendarshowotherdays) is false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | JavaScript Date object representing this day |
| events | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | events that fall on this day |
| calendar | [Calendar](#type-calendar) | false | — | the calendar itself |
| rowNum | [int](../reference.md#type-int) | false | — | the row number to which the parameter date belongs |
| colNum | [int](../reference.md#type-int) | false | — | the column number to which the parameter date belongs |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to display

### Groups

- monthViewFormatting

---
## Method: Calendar.setLaneTitle

### Description
For views that support [lanes](#attr-calendarlanes), updates the title for the passed lane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [String](#type-string) | false | — | the name of the lane to change the title for |
| title | [String](#type-string) | false | — | the new title to apply |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the title was updated, false otherwise

---
## Method: Calendar.addZone

### Description
Adds a new [zone](#attr-calendarzones) to the calendar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zone | [CalendarEvent](#type-calendarevent) | false | — | a new zone to add to the calendar |

---
## Method: Calendar.deselectEvent

### Description
Removes an event from the list of selected events in the current view, clearing its selected style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to deselect |

### Returns

`[Boolean](#type-boolean)` — true if the selection was changed, false otherwise

---
## Method: Calendar.setHeaderLevels

### Description
For [Timeline](../reference.md#class-timeline)s, configures the levels of [headers](../reference_2.md#object-headerlevel) shown above the event area, and their time units, after initialization.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| headerLevels | [Array of HeaderLevel](#type-array-of-headerlevel) | false | — | the array of HeaderLevels to set |

---
## Method: Calendar.groupLanesBy

### Description
When [canGroupLanes](#attr-calendarcangrouplanes) is true, this method allows the grouping in [timeline](#attr-calendartimelineview)s to be altered at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupFieldName | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | one or more field names to group by |

### Groups

- grouping

---
## Method: Calendar.shouldDisableDate

### Description
Returns true if the passed date should be considered disabled. Disabled dates don't allow events to be created by clicking on them, and drag operations that would start or end on such dates are also disallowed.

The default implementation returns false only for dates that fall on a [weekend](DateUtil.md#classmethod-dateutilgetweekenddays).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance |
| view | [CalendarView](#type-calendarview) | true | — | the view the date appears in |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this date should be considered disabled

---
## Method: Calendar.backgroundClick

### Description
Callback fired when the mouse is clicked in a background-cell, ie, one without an event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startDate | [Date](#type-date) | false | — | start datetime of the selected slot |
| endDate | [Date](#type-date) | false | — | end datetime of the selected slot |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel the default behavior of creating a new event at the selected location and showing its editor.

---
## Method: Calendar.setIndicators

### Description
Sets the [indicators](#attr-calendarindicators) used to highlight instants in time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| indicators | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | array of indicators to display |

---
## Method: Calendar.getEventEndDate

### Description
Returns the [end date](#attr-calendarenddatefield) of the passed event. If the event is [duration-based](#attr-calendarallowdurationevents), the result is calculated from the [start date](CalendarEvent.md#attr-calendareventstartdate) and the specified [duration](CalendarEvent.md#attr-calendareventduration) and [unit](CalendarEvent.md#attr-calendareventdurationunit).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the start date of |

### Returns

`[Date](#type-date)` — the end date of the passed event

---
## Method: Calendar.setShowViewHovers

### Description
Switches the various levels of [hovers](#attr-calendarshowviewhovers) on or off at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showViewHovers | [boolean](../reference.md#type-boolean) | false | — | whether to allow CalendarViews to show hovers |

---
## Method: Calendar.dayHeaderClick

### Description
Called when the header area of a day in the month view is clicked on.

By default, moves to the day tab and shows the clicked days events. Return false to cancel this action.

Not called if the day falls outside the current month and [Calendar.showOtherDays](#attr-calendarshowotherdays) is false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | JavaScript Date object representing this day |
| events | [Array of CalendarEvent](#type-array-of-calendarevent) | false | — | events that fall on this day |
| calendar | [Calendar](#type-calendar) | false | — | the calendar itself |
| rowNum | [int](../reference.md#type-int) | false | — | the row number to which the parameter date belongs |
| colNum | [int](../reference.md#type-int) | false | — | the column number to which the parameter date belongs |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel the action

### Groups

- monthViewEvents

---
## Method: Calendar.getView

### Description
Returns the [view](CalendarView.md#class-calendarview) with the passed [name](../reference_2.md#type-viewname).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewName | [ViewName](../reference_2.md#type-viewname) | false | — | the name of the CalendarView to return |

### Returns

`[CalendarView](#type-calendarview)` — the currently selected view

---
## Method: Calendar.getDragHoverHTML

### Description
Returns the HTML to show in a hover when an existing event is dragged, or when a new event is being created by dragging with the mouse.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | false | — | the CalendarView the mouse is hovered over |
| event | [CalendarEvent](#type-calendarevent) | false | — | the CalendarEvent attached to the EventCanvas being dragged |
| defaultValue | [String](#type-string) | false | — | the default text for the passed values |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

---
## Method: Calendar.timelineEventResized

### Description
Called when a Timeline event is resized via dragging by a user. Return false to disallow the resize.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that was resized |
| startDate | [Date](#type-date) | false | — | new start date of the passed event, after the resize |
| endDate | [Date](#type-date) | false | — | new end date of the passed event, after the resize |

### Returns

`[Boolean](#type-boolean)` — return false to disallow the resize

**Deprecated**

---
## Method: Calendar.createEventCanvasComponent

### Description
Called from [EventCanvas.setEvent](EventCanvas.md#method-eventcanvassetevent) when [Calendar.showEventCanvasComponents](#attr-calendarshoweventcanvascomponents) is true and an eventCanvas needs a component. The method is expected to create and return a single component to apply as a space-filling member of the passed [EventCanvas](EventCanvas.md#class-eventcanvas) in the [view](EventCanvas.md#attr-eventcanvascalendarview) in which it appears.

By default, this method returns a [DetailViewer](DetailViewer.md#class-detailviewer) showing values from the associated event, according to the fields in the Calendar's [dataSource](#attr-calendardatasource), or the default event-fields if no dataSource is present.

However, the component can be any [canvas-based](Canvas.md#class-canvas) widget, including a Layout containing an arrangement of other widgets. When applied as a member of an eventCanvas, the component fills its container and limits its own content to that size, showing scrollbars as appropriate.

See [Calendar.updateEventCanvasComponent](#method-calendarupdateeventcanvascomponent) for details on updating components that have already been created and applied.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [EventCanvas](#type-eventcanvas) | false | — | the eventCanvas to get the component for |

### Returns

`[Canvas](#type-canvas)` — any Canvas

### See Also

- [Calendar.updateEventCanvasComponent](#method-calendarupdateeventcanvascomponent)
- [Calendar.eventScreen](#attr-calendareventscreen)

---
## Method: Calendar.getSelectedEvent

### Description
Returns the currently selected [event](../reference.md#object-calendarevent), or the first one if more than one is selected.

### Returns

`[CalendarEvent](#type-calendarevent)` — the selected event

---
## Method: Calendar.getIndicatorCanvasStyle

### Description
Returns the [styleName](../reference.md#type-cssstylename) to use for the passed [indicator](#attr-calendarindicators), in the passed [view](CalendarView.md#class-calendarview). By default, returns the style [on the indicator](#attr-calendareventstylenamefield), if one is specified, or the style specified on the [calendar](#attr-calendarindicatorstylename) otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| indicator | [CalendarEvent](#type-calendarevent) | false | — | the indicator to get the CSS style for |
| view | [CalendarView](#type-calendarview) | true | — | the CalendarView that contains the canvas being styled |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — —

---
## Method: Calendar.getEventLane

### Description
Returns the [lane](../reference.md#object-lane) associated with the passed event, in the passed view

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the lane for |
| view | [CalendarView](#type-calendarview) | true | — | the view to get the lane object from |

### Returns

`[Lane](#type-lane)` — the lane associated with the passed event

---
## Method: Calendar.setLanes

### Description
Sets the [lanes](#attr-calendarlanes) in the current calendar view. Only has an effect in [timeline views](#attr-calendartimelineview), and in [day views](#attr-calendardayview) when [Calendar.showDayLanes](#attr-calendarshowdaylanes) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lanes | [Array of Lane](#type-array-of-lane) | false | — | array of lanes to display |
| skipRefreshEvents | [boolean](../reference.md#type-boolean) | true | — | set to false to prevent events from being refreshed |

---
## Method: Calendar.getLaneEvents

### Description
For views that support [lanes](#attr-calendarlanes), returns the array of events in the current dataset that apply to the passed lane in the passed or current view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [Lane](#type-lane)|[String](#type-string) | false | — | lane object or name to get the events for |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the passed lane lives - uses the selected view if unset |

### Returns

`[Array of CalendarEvent](#type-array-of-calendarevent)` — the list of events that apply to the passed lane and view

---
## Method: Calendar.dateIsWorkday

### Description
Should the parameter date be considered a workday? By default this method tries to find the parameter date day in [Calendar.workdays](#attr-calendarworkdays), and returns true if found. Override this method to provide custom logic for determining workday, perhaps returning false on holidays.

Note that, when showing [vertical lanes](#attr-calendarshowdaylanes) in the [day view](#attr-calendardayview), this method is also passed the name of the associated lane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | date to check for being a workday |
| laneName | [String](#type-string) | false | — | the name of the lane if [Calendar.showDayLanes](#attr-calendarshowdaylanes) is true, null otherwise |

### Returns

`[boolean](../reference.md#type-boolean)` — true if date is a workday, false otherwise

---
## Method: Calendar.getEventStartDate

### Description
Returns the [start date](CalendarEvent.md#attr-calendareventstartdate) of the passed event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the start date of |

### Returns

`[Date](#type-date)` — the start date of the passed event

---
## Method: Calendar.getDateCSSText

### Description
Return CSS text for styling the cell associated with the passed date and/or rowNum & colNum, which will be applied in addition to the CSS class for the cell, as overrides.

"CSS text" means semicolon-separated style settings, suitable for inclusion in a CSS stylesheet or in a STYLE attribute of an HTML element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to return CSS text for |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | the row number containing the date to get the CSS for |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the column number containing the date to get the CSS for |
| view | [CalendarView](#type-calendarview) | false | — | the relevant CalendarView |

### Returns

`[String](#type-string)` — CSS text for the cell with the passed date and rowNum/colNum

### See Also

- [Calendar.getDateHTML](#method-calendargetdatehtml)
- [Calendar.getDateStyle](#method-calendargetdatestyle)

---
## Method: Calendar.addCalendarEvent

### Description
Create a new event in this calendar.

In all cases, the [event](../reference.md#object-calendarevent) passed as the first parameter must have at least a [start date](#attr-calendarstartdatefield) set. If the calendar is showing [lanes](#attr-calendarlanes), the name of the [lane](CalendarEvent.md#attr-calendareventlane) and, if applicable, the [sublane](CalendarEvent.md#attr-calendareventsublane), must also be set.

To deal with errors during saving, see [Calendar.eventSaveError](#method-calendareventsaveerror).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the new calendar event to add |
| customValues | [Object](../reference.md#type-object) | true | — | additional, custom values to be saved with the event |

---
## Method: Calendar.getVisibleStartDate

### Description
Returns the first visible date in the passed, or currently selected, calendar view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to get the startDate for, or current view if |

### Returns

`[Date](#type-date)` — first visible date

---
## Method: Calendar.setData

### Description
Initialize the data object with the given array. Observes methods of the data object so that when the data changes, the calendar will redraw automatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Array of CalendarEvent](#type-array-of-calendarevent)[] | false | — | data to show in the list |

### Groups

- data

---
## Method: Calendar.getActiveDay

### Description
Gets the day of the week (0-6) that the mouse is currently over.

### Returns

`[Integer](../reference_2.md#type-integer)` — the day that the mouse is currently over

### See Also

- [Calendar.getActiveTime](#method-calendargetactivetime)

---
## Method: Calendar.getEventHeaderHTML

### Description
Returns the title text for the passed event, which is displayed in the header area of an eventCanvas rendered in a vertical or horizontal view, or as a clickable link in a cell in a [Month view](#attr-calendarshowmonthview).

The default implementation returns the event's [name field](#attr-calendarnamefield) for timelines, and that same value pre-pended with the event's [start](#attr-calendarstartdatefield) for day, week and month views.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the description text for |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the event is being rendered |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to display in the header of an event canvas

---
## Method: Calendar.eventClick

### Description
Called whenever an event is clicked on in the day, week or month views.

By default, a dialog appears showing details for the event, and offering the ability to edit events that can be edited. Return false to cancel the default action. This is a good place to, for example, show a completely customized event dialog instead of the default one.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | event that was clicked on |
| viewName | [ViewName](../reference_2.md#type-viewname) | false | — | view where the event's canvas was clicked |

### Returns

`[Boolean](#type-boolean)` — false to cancel the default action

---
## Method: Calendar.showEventDialog

### Description
Open the Quick Event dialog showing minimal information about an existing [event](../reference.md#object-calendarevent).

The [startDate](#attr-calendarstartdatefield) field on the event is used to calculate the display location for the dialog.

If this method is called when the Event Dialog is already showing another event, and if changes have been made, a confirmation dialog is displayed and editing of the new event is cancelled unless confirmed.

You can override this method to prevent the default action, perhaps instead showing a custom interface that performs validations or gathers custom data before making a call to [addCalendarEvent](#method-calendaraddcalendarevent) or [updateCalendarEvent](#method-calendarupdatecalendarevent) when the new data is available.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | true | — | the event to show in the Editor |
| isNewEvent | [Boolean](#type-boolean) | true | — | optional boolean indicating that this is a new event, event if an event is passed - used to pass defaults for a new event |

---
## Method: Calendar.eventRepositionMove

### Description
Notification called whenever the drop position of an event being drag-moved changes.

The `newEvent` parameter represents the event as it will be after the move, including [start](CalendarEvent.md#attr-calendareventstartdate) and [end](CalendarEvent.md#attr-calendareventenddate) dates and [lane](CalendarEvent.md#attr-calendareventlane) and [sublane](CalendarEvent.md#attr-calendareventsublane) where applicable.

Return false to prevent the default action, of positioning the drag canvas to the newEvent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that's being moved |
| newEvent | [CalendarEvent](#type-calendarevent) | false | — | the event as it would be if dropped now |

### Returns

`[Boolean](#type-boolean)` — return false to cancel the default drag move behavior

---
## Method: Calendar.scrollToTime

### Description
Scrolls Calendar [day](#attr-calendardayview) or [week](#attr-calendarweekview) views to the time represented by the time parameter. This string parameter is expected to be an arbitrary logical time value in any parsable time format - no date portion is expected, but time formats like "13:31" or "1:20am" are supported.

Has no effect in [timelines](#attr-calendartimelineview), where an arbitrary time-value is inapplicable to any range or resolution greater than a day.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| time | [String](#type-string) | false | — | any parsable time-string |

---
## Method: Calendar.backgroundMouseDown

### Description
Callback fired when the mouse button is depressed over a background-cell, ie, one without an event. Return false to cancel the default behavior of allowing sweep selection via dragging.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startDate | [Date](#type-date) | false | — | start datetime of the selected slot |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to suppress default behavior of allowing sweep selection via dragging.

---
## Method: Calendar.indicatorClick

### Description
Called whenever an [IndicatorCanvas](../reference.md#class-indicatorcanvas) is clicked in the [timelineView](#attr-calendartimelineview). There is no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| indicatorEvent | [CalendarEvent](#type-calendarevent) | false | — | indicator that was clicked on |
| viewName | [ViewName](../reference_2.md#type-viewname) | false | — | view where the event's canvas was clicked |

### Returns

`[Boolean](#type-boolean)` — false to cancel the default action

---
## Method: Calendar.currentViewChanged

### Description
Notification that fires whenever the current view changes via the [mainView tabset](#attr-calendarmainview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewName | [ViewName](../reference_2.md#type-viewname) | false | — | the name of the current view after the change |

---
## Method: Calendar.selectTab

### Description
Selects the calendar view in the passed tab number.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabnum | [number](#type-number) | false | — | the index of the tab to select |

---
## Method: Calendar.setShowDayLanes

### Description
Changes the [view mode](#attr-calendarshowdaylanes) of the day view at runtime - whether to show a normal day column for the [Calendar.chosenDate](#attr-calendarchosendate), or the specified set of [vertical lanes](#attr-calendarlanes).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showDayLanes | [boolean](../reference.md#type-boolean) | false | — | whether or not to show lanes in the day view |

---
## Method: Calendar.getDateStyle

### Description
Return the CSS styleName for the associated date-cell in the passed view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to return the CSS styleName for |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | the row number containing the date to get the CSS styleName for |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the column number containing the date to get the CSS styleName for |
| view | [CalendarView](#type-calendarview) | false | — | the relevant CalendarView |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style for the cell with the passed date and rowNum/colNum

### See Also

- [Calendar.getDateHTML](#method-calendargetdatehtml)
- [Calendar.getDateCSSText](#method-calendargetdatecsstext)

---
## Method: Calendar.refreshEvent

### Description
Refreshes the passed event in the current view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | The event object to refresh in the current view |

---
## Method: Calendar.addEvent

### Description
Create a new event in this calendar instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startDate | [Date](#type-date)|[CalendarEvent](#type-calendarevent) | false | — | start date of event, or CalendarEvent Object |
| endDate | [Date](#type-date) | true | — | end date of event |
| name | [String](#type-string) | true | — | name of event |
| description | [String](#type-string) | true | — | description of event |
| otherFields | [Object](../reference.md#type-object) | true | — | new values of additional fields to be updated |

**Deprecated**

---
## Method: Calendar.getCellHoverHTML

### Description
Returns the hover HTML for the cell at the passed co-ordinates in the passed view. By default, the hover text is the snap date closest to the mouse, if the cell being hovered is a normal date cell - otherwise, it is the title of the [laneField](#attr-calendarlanefields) being hovered over.

Override here to return custom HTML for the passed cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | false | — | the CalendarView the mouse is hovered over |
| record | [Record](#type-record) | false | — | The record containing the cell being hovered |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | The rowNum of the cell being hovered |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the colNum of the cell being hovered |
| date | [Date](#type-date) | false | — | the snap-date at the mouse, which may be different from the result of a call to [getCellDate](#method-calendargetcelldate) |
| defaultValue | [String](#type-string) | false | — | the default hover text for the passed values |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

---
## Method: Calendar.shouldShowEvent

### Description
Indicates whether the passed [event](../reference.md#object-calendarevent) should be visible in the passed [CalendarView](CalendarView.md#class-calendarview).

The default implementation returns true - note that this method only runs for events that are known to be in the accessible range and is a mechanism for extended custom filtering.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to check |
| view | [CalendarView](#type-calendarview) | true | — | the view the event will be rendered in |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this event should be displayed in the passed view

---
## Method: Calendar.showNewEventEditor

### Description
Show an Event Editor for a new event. If an [event](../reference.md#object-calendarevent) is passed as the parameter, it is used as defaults for the new event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | true | — | defaults for the new event to show in the Editor |

---
## Method: Calendar.getVisibleEndDate

### Description
Returns the last visible date in the passed, or currently selected, calendar view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to get the endDate for, or current view if null |

### Returns

`[Date](#type-date)` — last visible date

---
## Method: Calendar.isLongEvent

### Description
Returns true if the passed event is marked as lasting [all day](#attr-calendaralldayfield), or it [starts](#attr-calendarstartdatefield) and [ends](#attr-calendarenddatefield) on different days in your current locale. These types of events are displayed horizontally in a [separate layout](CalendarView.md#attr-calendarviewlongeventslayout) placed above the date cells in CalendarViews.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event in question |
| multiDayOnly | [Boolean](#type-boolean) | true | — | when true, only matches events that span multiple days - otherwise, matches those events or [all-day events](#attr-calendaralldayfield). |

### Returns

`[Boolean](#type-boolean)` — true if the event lasts all day or starts and ends on different days

---
## Method: Calendar.setShowWeekends

### Description
Setter for updating [Calendar.showWeekends](#attr-calendarshowweekends) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showWeekends | [boolean](../reference.md#type-boolean) | false | — | whether or not to show weekends |

---
## Method: Calendar.eventSaveError

### Description
Notification method fired when an attempt to save [an event](../reference.md#object-calendarevent) following edits or drag-movements results in an error from the server. May be overridden to handle specific errors and provide feedback to the user or push a server-provided record to client caches with a call to [updateCaches()](DataSource.md#method-datasourceupdatecaches), for example.

The `scenarioCode` parameter may be used to determine [how the save was initiated](../reference.md#type-calendarsavescenario).

Return _false_ from this method to cancel builtin behavior, which is as follows:

If a save happened because an event-canvas was moved or sized with the mouse, and any kind of error occurs, the event is restored to it's pre-save position - if this method specifically returns _true_, the errors are also sent to [central error handling](../kb_topics/errorHandling.md#kb-topic-error-handling-overview), which will show them to the user in a simple error dialog.

If a save happened because an event was edited in the [Calendar.eventDialog](#attr-calendareventdialog) or [Calendar.eventEditor](#attr-calendareventeditor) windows and a validation error occurs, the window is re-opened for editing with the validation errors visible. If any other kind of error occurs, the window will not be re-opened and, if this method specifically returns _true_, the error will be sent to [central error handling](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) which will show a simple error dialog to the end user.

In all cases, if the server returned an updated record despite the save failing (eg, perhaps the server enforces optimistic locking and the underlying record has been changed by another user), it is assumed to be a latest-version of the record and is applied instead of the original record during those builtin UI processes. So, the [Calendar.eventEditor](#attr-calendareventeditor) and [Calendar.eventDialog](#attr-calendareventdialog) will show any changes from the latest-record. If the save was caused by dragging an event and the event's [start](#attr-calendarstartdatefield) or [end](#attr-calendarenddatefield) dates are different in the latest-record, the EventCanvas will be positioned using the latest values, instead of returning to it's pre-save position on-screen.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | DSResponse from the save-attempt |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | initiating DSRequest Properties |
| scenarioCode | [CalendarSaveScenario](../reference.md#type-calendarsavescenario) | false | — | scenario in which the save occurred |

### Returns

`[Boolean](#type-boolean)` — false to cancel builtin behavior - null to allow builtin behaviors, true to also allow central event-handling for unhandled errors

---
## Method: Calendar.cancelEditing

### Description
Cancels the current edit-session, closing the builtin event [dialog](#attr-calendareventdialog) or [editor](#attr-calendareventeditor) and clearing any visible edit-selection from the [current CalendarView](#method-calendargetselectedview).

---
## Method: Calendar.getIndicatorHoverHTML

### Description
Gets the hover HTML for an [indicator](#attr-calendarindicators) being hovered over. Override here to return custom HTML based upon the parameter indicator object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| indicator | [CalendarEvent](#type-calendarevent) | false | — | The indicator being hovered over |
| indicatorCanvas | [IndicatorCanvas](#type-indicatorcanvas) | false | — | the indicator canvas being hovered over |
| view | [CalendarView](#type-calendarview) | false | — | the CalendarView in which the indicatorCanvas is displayed |
| defaultValue | [String](#type-string) | false | — | the default HTML to show when hovering over the passed Indicator |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

---
## Method: Calendar.setCurrentViewName

### Description
Sets the currently visible view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewName | [ViewName](../reference_2.md#type-viewname) | false | — | The name of the view that should be made visible. |

### Returns

`[ViewName](../reference_2.md#type-viewname)` — The name of the visible view.

---
## Method: Calendar.backgroundMouseUp

### Description
Notification method fired when the mouse button is released over a background-cell, ie, one without an event. Return false to cancel the default behavior of showing a dialog to add a new event with the passed dates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startDate | [Date](#type-date) | false | — | the datetime of the slot where the mouse button was depressed |
| endDate | [Date](#type-date) | false | — | the datetime of the slot where the mouse button was released |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to suppress default behavior of showing a dialog to add a new event with the passed dates.

---
## Method: Calendar.next

### Description
Move to the next day, week, or month, depending on which tab is selected.

---
## Method: Calendar.getEventCanvasStyle

### Description
Returns the [styleName](../reference.md#type-cssstylename) to use for the passed [event](../reference.md#object-calendarevent), in the passed [view](CalendarView.md#class-calendarview). By default, returns the style [on the event](#attr-calendareventstylenamefield), if one is specified - otherwise, in [lane-based](#attr-calendarlanes) views, it returns the style specified on the [lane or sublane](Lane.md#attr-laneeventstylename), or the style specified on the [calendar](#attr-calendareventstylename).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the CSS style for |
| view | [CalendarView](#type-calendarview) | true | — | the CalendarView that contains the canvas being styled |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — the CSS style to apply to the passed event in the passed view

---
## Method: Calendar.getZoneCanvasStyle

### Description
Returns the [styleName](../reference.md#type-cssstylename) to use for the passed [zone](#attr-calendarzones), in the passed [view](CalendarView.md#class-calendarview). By default, returns the style [on the zone](#attr-calendareventstylenamefield), if one is specified, or the style specified on the [calendar](#attr-calendarzonestylename) otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zone | [CalendarEvent](#type-calendarevent) | false | — | the zone to get the CSS style for |
| view | [CalendarView](#type-calendarview) | true | — | the CalendarView that contains the canvas being styled |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — —

---
## Method: Calendar.getPeriodEndDate

### Description
Returns the end of the period selected in the passed, or current, calendar view. For the [month view](#attr-calendarmonthview), and for the [week view](#attr-calendarweekview) when not showing weekends, this will often be a different date than that returned by [Calendar.getVisibleEndDate](#method-calendargetvisibleenddate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to get the periodEndDate for, or current view if null |

### Returns

`[Date](#type-date)` — period end date

---
## Method: Calendar.removeLane

### Description
Removes a lane from the calendar in [Calendar.timelineView](#attr-calendartimelineview), or in [Calendar.dayView](#attr-calendardayview) if [Calendar.showDayLanes](#attr-calendarshowdaylanes) is true.

Accepts either a [Lane object](../reference.md#object-lane) or a string that represents the [name](Lane.md#attr-lanename) of a lane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [Lane](#type-lane)|[String](#type-string) | false | — | either the actual Lane object or the name of the lane to remove |

---
## Method: Calendar.setTimelineRange

### Description
Sets the range over which the timeline will display events.

If the `end` parameter is not passed, the end date of the range will default to [20](#attr-calendardefaulttimelinecolumnspan) columns of the current [granularity](#attr-calendartimelinegranularity) following the start date.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [Date](#type-date) | false | — | start of range |
| end | [Date](#type-date) | true | — | end of range |

---
## Method: Calendar.getCellDate

### Description
Return the Date instance associated with the passed co-ordinates in the passed or selected view. If the cell at the passed co-ordinates is not a date-cell, returns null. If rowNum and colNum are both unset, returns the date from the cell under the mouse.

To determine the date at a more specific point within a cell, see [Calendar.getDateFromPoint](#method-calendargetdatefrompoint).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | true | — | the row number to get the date for |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | the column number to get the date for |
| view | [CalendarView](#type-calendarview) | true | — | the view to use - uses the selected view if not passed |

### Returns

`[Date](#type-date)` — the date, if any, associated with the passed co-ords in the appropriate view

---
## Method: Calendar.getDateHeaderTitle

### Description
Return the title text to display in the header-button of the ListGridField showing the passed date, in the passed view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to return the header-title for - note that the [month view](#attr-calendarmonthview) does not pass this parameter because a single column represents multiple dates |
| dayOfWeek | [int](../reference.md#type-int) | false | — | the week-day number of the passed date, except for the [month view](#attr-calendarmonthview), where no date is passed, because the week-day number represents multiple dates. |
| defaultValue | [String](#type-string) | false | — | the default header-title for the passed date and view |
| view | [CalendarView](#type-calendarview) | false | — | the relevant CalendarView |

### Returns

`[String](#type-string)` — the text to show in the header-button for the passed date/field

---
## Method: Calendar.setEventStyle

### Description
Update the styleName for the passed event. Refreshes the event's canvas in the current view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | The event object to refresh in the current view |
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | false | — | The new CSS style to apply to the canvases showing this event |

---
## Method: Calendar.removeEvent

### Description
Remove an event from this calendar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | The event object to remove from the calendar |

---
## Method: Calendar.getEventCanvasGripperIcon

### Description
Returns the [source image](#attr-calendareventcanvasgrippericon) to use as the gripper for the passed event canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [EventCanvas](#type-eventcanvas) | false | — | the canvas that will show the gripper |

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — the URL for the image to load

---
## Method: Calendar.shouldShowLane

### Description
Indicates whether the passed [lane](#attr-calendarlanes) should be visible in the passed [CalendarView](CalendarView.md#class-calendarview).

The default implementation returns true, unless the lane has no events and [Calendar.hideUnusedLanes](#attr-calendarhideunusedlanes) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [Lane](#type-lane)|[String](#type-string) | false | — | the lane object or name |
| view | [CalendarView](#type-calendarview) | true | — | the view the lane appears in |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this lane should be displayed in the passed view

---
## Method: Calendar.getSublaneFromPoint

### Description
Returns the [sublane](Lane.md#attr-lanesublanes) at the passed co-ordinates. To get the sublane under the mouse, pass null for both x and y.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../reference_2.md#type-integer) | true | — | optional x offset into the body of the selected view |
| y | [Integer](../reference_2.md#type-integer) | true | — | optional y offset into the body of the selected view. If this param and "x" are both unset, assumes both offsets from the last mouse event. |
| view | [CalendarView](#type-calendarview) | true | — | the view to get the sublane from - selected view if not passed |

### Returns

`[Lane](#type-lane)` — the sublane at the passed co-ords in the selected view

---
## Method: Calendar.getZoneHoverHTML

### Description
Gets the hover HTML for a [zone](#attr-calendarzones) being hovered over. Override here to return custom HTML based upon the parameter zone object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zone | [CalendarEvent](#type-calendarevent) | false | — | The zone being hovered over |
| zoneCanvas | [ZoneCanvas](#type-zonecanvas) | false | — | the zone canvas being hovered over |
| view | [CalendarView](#type-calendarview) | false | — | the CalendarView in which the zoneCanvas is displayed |
| defaultValue | [String](#type-string) | false | — | the default HTML to show when hovering over the passed Zone |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

---
## Method: Calendar.getDateCellVAlign

### Description
When [getDateHTML](#method-calendargetdatehtml) returns a value, this method returns the vertical alignment for that value in its cell, in the passed view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to get the cell-alignment for |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | the row number containing the date to get the cell-alignment for |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the column number containing the date to get the cell-alignment for |
| view | [CalendarView](#type-calendarview) | false | — | the relevant CalendarView |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — vertical-alignment for content in the cell with the passed date and rowNum/colNum

### See Also

- [Calendar.getDateHTML](#method-calendargetdatehtml)
- [Calendar.getDateCellAlign](#method-calendargetdatecellalign)
- [Calendar.getDateStyle](#method-calendargetdatestyle)
- [Calendar.getDateCSSText](#method-calendargetdatecsstext)

---
## Method: Calendar.previous

### Description
Move to the previous day, week, month, or timeline range depending on which tab is selected.

---
## Method: Calendar.addIndicator

### Description
Adds a new [indicator](#attr-calendarindicators) to the calendar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| indicator | [CalendarEvent](#type-calendarevent) | false | — | a new indicator to add to the calendar |

---
## Method: Calendar.zoneClick

### Description
Called whenever a [ZoneCanvas](../reference.md#class-zonecanvas) is clicked in the [timelineView](#attr-calendartimelineview). There is no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zoneEvent | [CalendarEvent](#type-calendarevent) | false | — | zone that was clicked on |
| viewName | [ViewName](../reference_2.md#type-viewname) | false | — | view where the event's canvas was clicked |

### Returns

`[Boolean](#type-boolean)` — false to cancel the default action

---
## Method: Calendar.getSelectedEvents

### Description
Returns the currently selected list of [events](../reference.md#object-calendarevent).

### Returns

`[Array of CalendarEvent](#type-array-of-calendarevent)` — the list of selected events

---
## Method: Calendar.scrollToStart

### Description
Move the viewport of a CalendarView to the start of it's scrollable range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to affect, the current view if not specified |

---
## Method: Calendar.showEventEditor

### Description
Show an Event Editor for the passed event. Event Editor's fill the Calendar and allow for editing of the built-in Event fields, like [name](#attr-calendarnamefield) and [description](#attr-calendardescriptionfield), as well as any custom fields supplied via [Calendar.eventEditorFields](#attr-calendareventeditorfields).

If isNewEvent is true, a new event is created - in this case, if an event is passed, it represents default values to apply to the new event.

You can override this method to prevent the default action, perhaps instead showing a custom interface that performs validations or gathers custom data before making a call to [addCalendarEvent](#method-calendaraddcalendarevent) or [updateCalendarEvent](#method-calendarupdatecalendarevent) when the new data is available.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | true | — | an existing event to show in the Editor |
| isNewEvent | [Boolean](#type-boolean) | true | — | optional boolean indicating that this is a new event, even if an event is passed - used to pass defaults for a new event |

---
## Method: Calendar.getDateFromPoint

### Description
Returns a Date instance representing the point at the passed offsets into the body of the current view.

If snapOffsets is passed as false, returns the date representing the exact position of the passed offsets. If unset or passed as true, returns the date at the nearest eventSnapGap to the left, for [Timeline](../reference.md#class-timeline)s, or above for [day](#attr-calendardayview) and [week](#attr-calendarweekview) views.

If neither x nor y offsets are passed, assumes them from the last mouse event.

If the cell at the eventual offsets is not a date-cell, returns null.

Note that, for the [month view](#attr-calendarmonthview), this method is functionally equivalent to [Calendar.getCellDate](#method-calendargetcelldate), which determines the date associated with a cell, without the additional offset precision offered here.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../reference_2.md#type-integer) | true | — | the x offset into the body of the selected view - non-functional for the [day view](#attr-calendardayview). If this param and "y" are both unset, assumes both offsets from the last mouse event. |
| y | [Integer](../reference_2.md#type-integer) | true | — | the y offset into the body of the selected view - non-functional for the [timeline view](#attr-calendartimelineview). If this param and "x" are both unset, assumes both offsets from the last mouse event. |
| snapOffsets | [Boolean](#type-boolean) | true | — | whether to snap the offsets to the nearest eventSnapGap - if unset, the default is true |
| view | [CalendarView](#type-calendarview) | true | — | the view to use - or the selected view if not passed |

### Returns

`[Date](#type-date)` — the date, if any, associated with the passed co-ords in the current view

---
## Method: Calendar.updateEvent

### Description
Update an event in this calendar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | The event object to update |
| startDate | [Date](#type-date) | false | — | start date of event |
| endDate | [Date](#type-date) | false | — | end date of event |
| name | [String](#type-string) | false | — | name of event |
| description | [String](#type-string) | false | — | description of event |
| otherFields | [Object](../reference.md#type-object) | false | — | new values of additional fields to be updated |

**Deprecated**

---
## Method: Calendar.eventRepositionStop

### Description
Notification called when an event being drag-moved is dropped.

The `newEvent` parameter represents the event as it will be after the move, including [start](CalendarEvent.md#attr-calendareventstartdate) and [end](CalendarEvent.md#attr-calendareventenddate) dates and [lane](CalendarEvent.md#attr-calendareventlane) and [sublane](CalendarEvent.md#attr-calendareventsublane) where applicable.

Return false to prevent the default action, of actually [updating](#method-calendarupdatecalendarevent) the event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that's about to be moved |
| newEvent | [CalendarEvent](#type-calendarevent) | false | — | the event as it will be, unless this method returns false |
| customValues | [Object](../reference.md#type-object) | true | — | additional custom values associated with the event |

### Returns

`[Boolean](#type-boolean)` — return false to cancel the default drop behavior

---
## Method: Calendar.fetchData

### Description
Retrieves data from the DataSource that matches the specified criteria.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

When `fetchData()` is first called, if data has not already been provided via [setData()](ListGrid_2.md#method-listgridsetdata), this method will create a [ResultSet](ResultSet.md#class-resultset), which will be configured based on component settings such as [DataBoundComponent.fetchOperation](DataBoundComponent.md#attr-databoundcomponentfetchoperation) and [DataBoundComponent.dataPageSize](DataBoundComponent.md#attr-databoundcomponentdatapagesize), as well as the general purpose [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). The created ResultSet will automatically send a DSRequest to retrieve data from [listGrid.dataSource](ListGrid_1.md#attr-listgriddatasource), and from then on will automatically manage paging through large datasets, as well as performing filtering and sorting operations inside the browser when possible - see the [ResultSet](ResultSet.md#class-resultset) docs for details.

**NOTE:** do not use **both** [autoFetchData:true](DataBoundComponent.md#attr-databoundcomponentautofetchdata) **and** a call to `fetchData()` - this may result in two DSRequests to fetch data. Use either [autoFetchData](DataBoundComponent.md#attr-databoundcomponentautofetchdata) and [Criteria](../reference_2.md#type-criteria) **or** a manual call to fetchData() passing criteria.

Whether a ResultSet was automatically created or provided via [setData()](ListGrid_2.md#method-listgridsetdata), subsequent calls to fetchData() will simply call [ResultSet.setCriteria](ResultSet.md#method-resultsetsetcriteria).

Changes to criteria may or may not result in a DSRequest to the server due to [client-side filtering](ResultSet.md#attr-resultsetuseclientfiltering). You can call [willFetchData(criteria)](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine if new criteria will result in a server fetch.

If you need to force data to be re-fetched, you can call [invalidateCache()](ListGrid_2.md#method-listgridinvalidatecache) and new data will automatically be fetched from the server using the current criteria and sort direction. **NOTE:** when using `invalidateCache()` there is no need to **also** call `fetchData()` and in fact this could produce unexpected results.

This method takes an optional callback parameter (set to a [DSCallback](../reference_2.md#type-dscallback)) to fire when the fetch completes. Note that this callback will not fire if no server fetch is performed. In this case the data is updated synchronously, so as soon as this method completes you can interact with the new data. If necessary, you can use [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine whether or not a server fetch will occur when `fetchData()` is called with new criteria.

In addition to the callback parameter for this method, developers can use [dataArrived()](ListGrid_2.md#method-listgriddataarrived) to be notified every time data is loaded.

By default, this method assumes a [TextMatchStyle](../reference_2.md#type-textmatchstyle) of "exact"; that can be overridden by supplying a different value in the requestProperties parameter. See [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata);

**Changing the request properties**

Changes to [TextMatchStyle](../reference_2.md#type-textmatchstyle) made via `requestProperties` will be honored in combination with the fetch criteria, possibly invalidating cache and triggering a server request if needed, as documented for [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata). In contrast, changes to [operationId](DSRequest.md#attr-dsrequestoperationid) in the request properties will cause the [ResultSet](ResultSet.md#class-resultset) or [ResultTree](ResultTree.md#class-resulttree) to be rebuilt, always refetching from the server. However, changes to other request properties after the initial fetch won't be detected, and no fetch will get triggered based on that new request context.

To pick up such changes, we recommend that you call [setData(\[\])](#method-calendarsetdata) (passing an empty array to ensure the data model is cleared), and then call this method to fetch again. If you try to do it by calling [invalidateCache()](ListGrid_2.md#method-listgridinvalidatecache), you may see duplicate fetches if you haven't already updated the data context by calling this method with the new request properties, and fail to do so before the component is [redrawn](Canvas.md#method-canvasredraw).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](ListGrid_2.md#method-listgridrefreshdata)

---
## Method: Calendar.scrollToEvent

### Description
Scrolls the [current view](#method-calendargetcurrentviewname) so the passed event is visible. If the event is outside of the view's current date-range, the default behavior is to automatically reload the view with a date-range starting at the event's [startDate](#attr-calendarstartdatefield) and then scroll to the event vertically as necessary. Pass false as the `canReload` param to prevent that default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to move the calendar view to |
| canReload | [boolean](../reference.md#type-boolean) | true | — | set to false to prevent a view from automatically reloading with a new range if the passed event is not in its current scrollable range |

---
## Method: Calendar.moveToEvent

### Description
Resets the current visible range of a calendar view so that it shows the date on which the passed event occurs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to move the calendar view to |

**Deprecated**

---
## Method: Calendar.getEventSublane

### Description
Returns the [sublane](Lane.md#attr-lanesublanes) associated with the passed event, in the passed view

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the sublane for |
| view | [CalendarView](#type-calendarview) | true | — | the view to get the sublane object from |

### Returns

`[Lane](#type-lane)` — the sublane associated with the passed event

---
## Method: Calendar.getDateHTML

### Description
Return the HTML to be displayed in the associated date-cell in the passed view. Note that the [month view](#attr-calendarmonthview) has default cell HTML, controlled via [getDayBodyHTML()](#method-calendargetdaybodyhtml).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to get the HTML for |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | the row number containing the date to get the HTML for |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | the column number containing the date to get the HTML for |
| view | [CalendarView](#type-calendarview) | false | — | the relevant CalendarView |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to display in the cell with the passed date and rowNum/colNum

### See Also

- [Calendar.getDateCellAlign](#method-calendargetdatecellalign)
- [Calendar.getDateCellVAlign](#method-calendargetdatecellvalign)
- [Calendar.getDateStyle](#method-calendargetdatestyle)
- [Calendar.getDateCSSText](#method-calendargetdatecsstext)
- [Calendar.getDayBodyHTML](#method-calendargetdaybodyhtml)

---
## Method: Calendar.setChosenDate

### Description
Set the current date for which the calendar will display events.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newDate | [Date](#type-date) | false | — | the new date to set as the current date |

---
## Method: Calendar.eventResized

### Description
Called when an event is resized with the mouse. The passed date value is the new \*end\* date for the event, since resizing can only be performed on the bottom edge of an event in normal calendar views.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newDate | [Date](#type-date) | false | — | new end date and time that event is being resized to |
| event | [CalendarEvent](#type-calendarevent) | false | — | the event as it will be after this resize |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to disallow the resize

### Groups

- monthViewEvents

**Deprecated**

---
## Method: Calendar.eventResizeStop

### Description
Notification called when an event drag-resize operation completes.

The `newEvent` parameter represents the event as it will be after the move.

Return false to prevent the default action, of actually [updating](#method-calendarupdatecalendarevent) the event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that's about to be resized |
| newEvent | [CalendarEvent](#type-calendarevent) | false | — | the event as it will be, unless this method returns false |
| customValues | [Object](../reference.md#type-object) | true | — | additional custom values associated with the event |

### Returns

`[Boolean](#type-boolean)` — return false to cancel the default drag-resize stop behavior

---
## Method: Calendar.getDateLabelText

### Description
Returns the text to display between the navigation buttons above the Calendar - indicates the visible date range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewName | [String](#type-string) | false | — | one of "day", "week", "month" or "timeline" |
| startDate | [Date](#type-date) | false | — | the start of the visible date range |
| endDate | [Date](#type-date) | true | — | the optional end of the visible date range |

### Returns

`[String](#type-string)` — a formatted date or date-range string appropriate to the passed view

---
## Method: Calendar.eventAdded

### Description
Notification fired whenever a user adds an event.

In a calendar with a DataSource, eventAdded() fires **after** the event has been successfully added at the server

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that was added |

---
## Method: Calendar.getWorkdayStart

### Description
Returns the start of the working day on the passed date. By default, this method returns the value of [workdayStart](#attr-calendarworkdaystart).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance |
| laneName | [String](#type-string) | true | — | the name of the relevant lane - only passed for dayView with showDayLanes: true |

### Returns

`[String](#type-string)` — any parsable time-string

---
## Method: Calendar.getEventHoverHTML

### Description
Gets the hover HTML for an event being hovered over. Override here to return custom HTML based upon the parameter event object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | The event being hovered |
| eventCanvas | [EventCanvas](#type-eventcanvas) | false | — | the event canvas being hovered over |
| view | [CalendarView](#type-calendarview) | false | — | the CalendarView in which the eventCanvas lives |
| defaultValue | [String](#type-string) | true | — | the default HTML to show when hovering over the passed event |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

---
## Method: Calendar.selectEvent

### Description
Adds an event to the list of selected events in the current view, showing it in a selected style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to add to the selection |

### Returns

`[Boolean](#type-boolean)` — true if the selection was changed, false otherwise

---
## Method: Calendar.getActiveTime

### Description
Gets a date object representing the date over which the mouse is hovering for the current selected view. For month view, the time will be set to midnight of the active day. For day and week views, the time will be the rounded to the closest half hour relative to the mouse position.

### Returns

`[Date](#type-date)` — the date that the mouse is over

---
## Method: Calendar.getHeaderHoverHTML

### Description
Returns the hover HTML to show in a hover when the mouse moves over the header area.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | false | — | the CalendarView the mouse is hovered over |
| headerLevel | [HeaderLevel](#type-headerlevel) | false | — | the header level hovered over |
| startDate | [Date](#type-date) | false | — | the start date of the span being hovered over |
| endDate | [Date](#type-date) | false | — | the end date of the span being hovered over |
| defaultValue | [String](#type-string) | false | — | the default text for the passed header level and date range |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

---
## Method: Calendar.getCurrentViewName

### Description
Get the name of the visible view. Returns one of 'day', 'week', 'month' or 'timeline'.

### Returns

`[ViewName](../reference_2.md#type-viewname)` — The name of the currently visible view.

---
## Method: Calendar.eventsRendered

### Description
A notification method fired when the events in the current view have been refreshed.

---
## Method: Calendar.updateCalendarEvent

### Description
Save an event to this Calendar's ${isc.DocUtils.linkForRef('attr:Calendar.dataSource','dataSource) or \\n ${isc.DocUtils.linkForRef('attr:Calendar.data','data array\\')')}. To deal with errors while saving, see [Calendar.eventSaveError](#method-calendareventsaveerror)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | The event object that will be updated |
| newEvent | [CalendarEvent](#type-calendarevent) | false | — | The new attributes for the event |
| otherFields | [Object](../reference.md#type-object) | false | — | new values of additional fields to be updated |

---
## Method: Calendar.removeIndicator

### Description
Removes a [indicator](#attr-calendarindicators) from the calendar.

Accepts either a [indicator object](../reference.md#object-calendarevent) or a string that represents the [name](CalendarEvent.md#attr-calendareventname) of anindicator.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| indicator | [CalendarEvent](#type-calendarevent)|[String](#type-string) | false | — | either the actual CalendarEvent representing the indicator, or the name of the indicator to remove |

---
## Method: Calendar.addLane

### Description
Adds a new [Lane](../reference.md#object-lane) to the calendar, for display in the [timeline view](#attr-calendartimelineview), and in the [day view](#attr-calendardayview) if [showDayLanes](#attr-calendarshowdaylanes) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| lane | [Lane](#type-lane) | false | — | a new Lane object to add to the calendar |

---
## Method: Calendar.scrollToEnd

### Description
Move the viewport of a CalendarView to the end of its scrollable range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to affect, the current view if not specified |

---
## Method: Calendar.eventRemoved

### Description
Notification fired whenever a user removes an event.

In a calendar with a DataSource, eventRemoved() fires **after** the event has been successfully removed from the server

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event that was removed |

### Groups

- monthViewEvents

---
## Method: Calendar.shouldShowDate

### Description
Indicates whether the passed date should be visible in the passed [CalendarView](CalendarView.md#class-calendarview).

The default implementation returns true, unless the date falls on a [weekend](DateUtil.md#classmethod-dateutilgetweekenddays) and [showWeekends](#attr-calendarshowweekends) is false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance |
| view | [CalendarView](#type-calendarview) | true | — | the view the date appears in |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this date should be considered disabled

---
## Method: Calendar.filterData

### Description
Retrieves data that matches the provided criteria and displays the matching data in this component.

This method behaves exactly like [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) except that [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is automatically set to "substring" so that String-valued fields are matched by case-insensitive substring comparison.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required; see [fetchData()](ListGrid_2.md#method-listgridfetchdata) for details |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | for databound components only - optional additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata)

---
## Method: Calendar.getSelectedView

### Description
Returns the currently selected [view](CalendarView.md#class-calendarview).

### Returns

`[CalendarView](#type-calendarview)` — the currently selected view

---
## Method: Calendar.addLaneEvent

### Description
For [Timeline](../reference.md#class-timeline)s, and for [dayView](#attr-calendardayview) with [showDayLanes](#attr-calendarshowdaylanes) set, creates a new event and adds it to a particular [Lane](../reference.md#object-lane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| laneName | [Lane](#type-lane) | false | — | the Lane in which to add this event |
| startDate | [Date](#type-date)|[Object](../reference.md#type-object) | false | — | start date of event, or CalendarEvent Object |
| endDate | [Date](#type-date) | true | — | end date of event |
| name | [String](#type-string) | true | — | name of event |
| description | [String](#type-string) | true | — | description of event |
| otherFields | [Any](#type-any) | true | — | new values of additional fields to be updated |

**Deprecated**

---
## Method: Calendar.getEventBodyHTML

### Description
Returns the description text for the passed event, for display in the body area of an event canvas. The default implementation returns the event's [description field](#attr-calendardescriptionfield).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the description text for |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the event is being rendered |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to display in the body of the passed event's EventCanvas

---
## Method: Calendar.getLongEventHTML

### Description
Returns the text to be displayed in a [long-event](#attr-calendaralldayfield) displayed horizontally in the separate [long-events layout](CalendarView.md#attr-calendarviewlongeventslayout) above vertical Calendar views.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [CalendarEvent](#type-calendarevent) | false | — | the event to get the description text for |
| layout | [Canvas](#type-canvas) | false | — | the longEventsLayout in which this event is displayed |
| view | [CalendarView](#type-calendarview) | true | — | the view in which the event is being rendered |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to display in the header of an event canvas

---
## Method: Calendar.getLanePadding

### Description
For views that support [lanes](#attr-calendarlanes), returns the padding to apply to events rendered in lanes in the passed or current view. By default, returns [laneEventPadding](#attr-calendarlaneeventpadding).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [CalendarView](#type-calendarview) | true | — | the view to get the lane padding for |

### Returns

`[Integer](../reference_2.md#type-integer)` — the padding to apply to events in lanes in the passed or current view

---
