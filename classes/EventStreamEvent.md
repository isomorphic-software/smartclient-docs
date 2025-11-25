# EventStreamEvent Documentation

[← Back to API Index](../main.md)

---

## Attr: EventStreamEvent.deltaX

### Description
The [horizontal scroll delta](EventHandler.md#classmethod-eventhandlergetwheeldeltax), present for [wheel events](EventStream.md#attr-eventstreamcapturewheelevents).

### See Also

- [EventStreamEvent.deltaY](#attr-eventstreameventdeltay)

**Flags**: R

---
## Attr: EventStreamEvent.threadCode

### Description
A symbolic thead ID useful for debugging, present when a JavaScript error is hit processing an event.

### See Also

- [EventStreamEvent.errorTrace](#attr-eventstreameventerrortrace)
- [EventStreamEvent.errorEvent](#attr-eventstreameventerrorevent)

**Flags**: R

---
## Attr: EventStreamEvent.dragTargetID

### Description
The [widget ID](Canvas.md#attr-canvasid) of the [drag target](EventHandler.md#classmethod-eventhandlergetdragtarget), present for most [drag events](EventStream.md#attr-eventstreamcapturedragevents).

Note that if drag events are not being captured, it will be populated for the `mouseUp` event terminating the drag.

### See Also

- [EventStreamEvent.dropTargetID](#attr-eventstreameventdroptargetid)
- [EventStreamEvent.dropTargetClass](#attr-eventstreameventdroptargetclass)
- [EventStreamEvent.dragTargetClass](#attr-eventstreameventdragtargetclass)

**Flags**: R

---
## Attr: EventStreamEvent.metaKey

### Description
Present for [key events](EventStream.md#attr-eventstreamcapturekeyevents) if the meta key was down when the event got triggered. Otherwise, not present.

### See Also

- [EventStreamEvent.keyName](#attr-eventstreameventkeyname)
- [EventStreamEvent.shiftKey](#attr-eventstreameventshiftkey)
- [EventStreamEvent.ctrlKey](#attr-eventstreameventctrlkey)

**Flags**: R

---
## Attr: EventStreamEvent.width

### Description
The [page width](Page.md#classmethod-pagegetwidth), present for page-level [resize events](EventStream.md#attr-eventstreamcapturepageevents).

### See Also

- [EventStreamEvent.height](#attr-eventstreameventheight)

**Flags**: R

---
## Attr: EventStreamEvent.keyName

### Description
The name of the key that triggered this event, present for [key events](EventStream.md#attr-eventstreamcapturekeyevents). For flexibility and ease of conversion to formats such as Selenese, the `keyName` for self-inserting keys (e.g. alphanumerics, "!", "@", etc.) reflects the actual character typed, factoring in the shift key. This aligns with [EventHandler.getKeyEventKey](EventHandler.md#classmethod-eventhandlergetkeyeventkey) rather than [EventHandler.getKey](EventHandler.md#classmethod-eventhandlergetkey), but refer to [KeyName](../main_2.md#type-keyname) for special keys.

Note that the `keyName` for special keys may be more than one character, such as "Enter", or "Down". For improved [collapsing](EventStream.md#attr-eventstreamcollapsekeyevents), the space key is always reported as the self-inserting key " ", rather than the special key "Space", since we can't collapse special and self-inserting keys into one event.

### See Also

- [EventStreamEvent.shiftKey](#attr-eventstreameventshiftkey)
- [EventStreamEvent.ctrlKey](#attr-eventstreameventctrlkey)
- [EventStreamEvent.metaKey](#attr-eventstreameventmetakey)
- [EventStreamEvent.keyNames](#attr-eventstreameventkeynames)

**Flags**: R

---
## Attr: EventStreamEvent.synthetic

### Description
True For synthetic events. Otherwise, not present at all. When true, [EventStreamEvent.originalType](#attr-eventstreameventoriginaltype) should be set indicating the original `eventType`.

### See Also

- [EventStreamEvent.originalType](#attr-eventstreameventoriginaltype)

**Flags**: R

---
## Attr: EventStreamEvent.dropTargetClass

### Description
The [class name](Class.md#method-classgetclassname) of the [drop target](Canvas.md#method-canvasdrop), present for some [drag events](EventStream.md#attr-eventstreamcapturedragevents).

Note that if drag events are not being captured, it will be populated for the `mouseUp` event terminating the drag.

### See Also

- [EventStreamEvent.dropTargetID](#attr-eventstreameventdroptargetid)
- [EventStreamEvent.dragTargetID](#attr-eventstreameventdragtargetid)
- [EventStreamEvent.dragTargetClass](#attr-eventstreameventdragtargetclass)

**Flags**: R

---
## Attr: EventStreamEvent.targetY

### Description
The vertical offset of the event from the [top edge](Canvas.md#attr-canvastop) of the event target, if one exists. Keyboard, page-level, and non-DOM events may not have any target.

### See Also

- [EventStreamEvent.targetID](#attr-eventstreameventtargetid)
- [EventStreamEvent.targetClass](#attr-eventstreameventtargetclass)
- [EventStreamEvent.targetY](#attr-eventstreameventtargety)

**Flags**: R

---
## Attr: EventStreamEvent.deltaY

### Description
The [vertiacl scroll delta](EventHandler.md#classmethod-eventhandlergetwheeldeltax), present for [wheel events](EventStream.md#attr-eventstreamcapturewheelevents).

### See Also

- [EventStreamEvent.deltaX](#attr-eventstreameventdeltax)

**Flags**: R

---
## Attr: EventStreamEvent.errorTrace

### Description
The stack reported when a JavaScript error is hit processing an event. The `errorTrace` contains an initial description of the error, and formatting whitespace and newlines to make the trace readable.

### See Also

- [EventStreamEvent.threadCode](#attr-eventstreameventthreadcode)
- [EventStreamEvent.errorEvent](#attr-eventstreameventerrorevent)

**Flags**: R

---
## Attr: EventStreamEvent.originalType

### Description
For synthetic events (where the [EventHandler](EventHandler.md#class-eventhandler) has (re)dispatched a DOM event as a new type), the original `eventType`.

### See Also

- [EventStreamEvent.synthetic](#attr-eventstreameventsynthetic)

**Flags**: R

---
## Attr: EventStreamEvent.targetID

### Description
The [widget ID](Canvas.md#attr-canvasid) of the event target, if one exists. Page-level and non-DOM events may not have any target.

### See Also

- [EventStreamEvent.targetClass](#attr-eventstreameventtargetclass)
- [EventStreamEvent.targetX](#attr-eventstreameventtargetx)
- [EventStreamEvent.targetY](#attr-eventstreameventtargety)

**Flags**: R

---
## Attr: EventStreamEvent.Y

### Description
The top offset of the event on the page. This property typically won't be set unless no [target](#attr-eventstreameventtargetid) is present and the event has an [EventStreamEvent.errorTrace](#attr-eventstreameventerrortrace).

### See Also

- [EventStreamEvent.X](#attr-eventstreameventx)

**Flags**: R

---
## Attr: EventStreamEvent.URL

### Description
The transaction `URL` associated wtih the successful [relogin](../kb_topics/relogin.md#kb-topic-relogin). Only present for [login events](EventStream.md#attr-eventstreamcaptureloginevents).

**Flags**: R

---
## Attr: EventStreamEvent.timeOffset

### Description
The time offset of this event from [EventStreamData.startTime](EventStreamData.md#attr-eventstreamdatastarttime), when capturing started, in milliseconds.

**Flags**: R

---
## Attr: EventStreamEvent.targetClass

### Description
The [class name](Class.md#method-classgetclassname) of the event target, if one exists. Page-level and non-DOM events may not have any target.

### See Also

- [EventStreamEvent.targetID](#attr-eventstreameventtargetid)
- [EventStreamEvent.targetX](#attr-eventstreameventtargetx)
- [EventStreamEvent.targetY](#attr-eventstreameventtargety)

**Flags**: R

---
## Attr: EventStreamEvent.targetX

### Description
The horizontal offset of the event from the [left edge](Canvas.md#attr-canvasleft) of the event target, if one exists. Keyboard, page-level, and non-DOM events may not have any target.

### See Also

- [EventStreamEvent.targetID](#attr-eventstreameventtargetid)
- [EventStreamEvent.targetClass](#attr-eventstreameventtargetclass)
- [EventStreamEvent.targetY](#attr-eventstreameventtargety)

**Flags**: R

---
## Attr: EventStreamEvent.keyNames

### Description
When [key event collapsing](EventStream.md#attr-eventstreamcollapsekeyevents) is active and other events have been collapsed into this one, contains a string representing the concatenated [keyNames](#attr-eventstreameventkeyname) from the collapsed events. The length of this string should match [EventStreamEvent.count](#attr-eventstreameventcount), and the first character in the string should be [EventStreamEvent.keyName](#attr-eventstreameventkeyname).

Note that only self-inserting keys can be concentated by collapsing, not special keys.

### See Also

- [EventStreamEvent.keyName](#attr-eventstreameventkeyname)

**Flags**: R

---
## Attr: EventStreamEvent.locator

### Description
The locator representing the event target, if one exists. Designed to be robust, the the locator provides a future-proof way to specify a [Canvas](Canvas.md#class-canvas), [FormItem](FormItem.md#class-formitem), or widget part such as a row of a [ListGrid](ListGrid_1.md#class-listgrid).

### See Also

- [usingSelenium](../kb_topics/usingSelenium.md#kb-topic-using-selenium-scripts-selenese)
- [AutoTest.getObject](AutoTest.md#classmethod-autotestgetobject)

**Flags**: R

---
## Attr: EventStreamEvent.height

### Description
The [page height](Page.md#classmethod-pagegetheight), present for page-level [resize events](EventStream.md#attr-eventstreamcapturepageevents).

### See Also

- [EventStreamEvent.width](#attr-eventstreameventwidth)

**Flags**: R

---
## Attr: EventStreamEvent.dragTargetClass

### Description
The [class name](Class.md#method-classgetclassname) of the [drag target](EventHandler.md#classmethod-eventhandlergetdragtarget), present for most [drag events](EventStream.md#attr-eventstreamcapturedragevents).

Note that if drag events are not being captured, it will be populated for the `mouseUp` event terminating the drag.

### See Also

- [EventStreamEvent.dragTargetID](#attr-eventstreameventdragtargetid)
- [EventStreamEvent.dropTargetID](#attr-eventstreameventdroptargetid)
- [EventStreamEvent.dropTargetClass](#attr-eventstreameventdroptargetclass)

**Flags**: R

---
## Attr: EventStreamEvent.X

### Description
The left offset of the event on the page. This property typically won't be set unless no [target](#attr-eventstreameventtargetid) is present and the event has an [EventStreamEvent.errorTrace](#attr-eventstreameventerrortrace).

### See Also

- [EventStreamEvent.Y](#attr-eventstreameventy)

**Flags**: R

---
## Attr: EventStreamEvent.count

### Description
Contains a count of the number of events (if any) collapsed into this event if collapsing is active, which includes:

*   [move events](EventStream.md#attr-eventstreamcollapsemoveevents)
*   [key events](EventStream.md#attr-eventstreamcollapsekeyevents)
*   [wheel events](EventStream.md#attr-eventstreamcollapsewheelevents)
*   [page events](EventStream.md#attr-eventstreamcollapsepageevents)

The count, if present, includes the event itself so it will always be a number greater than or equal to two.

**Flags**: R

---
## Attr: EventStreamEvent.dropTargetID

### Description
The [widget ID](Canvas.md#attr-canvasid) of the [drop target](Canvas.md#method-canvasdrop), present for some [drag events](EventStream.md#attr-eventstreamcapturedragevents).

Note that if drag events are not being captured, it will be populated for the `mouseUp` event terminating the drag.

### See Also

- [EventStreamEvent.dragTargetID](#attr-eventstreameventdragtargetid)
- [EventStreamEvent.dragTargetClass](#attr-eventstreameventdragtargetclass)
- [EventStreamEvent.dropTargetClass](#attr-eventstreameventdroptargetclass)

**Flags**: R

---
## Attr: EventStreamEvent.eventType

### Description
The type of the [EventStreamEvent](../main.md#object-eventstreamevent). For DOM events, this is just the official [EventHandler](EventHandler.md#class-eventhandler) name for the event, such as `mouseDown`. Otherwise, it's unique to [EventStream](EventStream.md#class-eventstream), but should reflect what event was captured, such as `fileLoad` or `relogin`.

**Flags**: R

---
## Attr: EventStreamEvent.ctrlKey

### Description
Present for [key events](EventStream.md#attr-eventstreamcapturekeyevents) if the control key was down when the event got triggered. Otherwise, not present.

### See Also

- [EventStreamEvent.keyName](#attr-eventstreameventkeyname)
- [EventStreamEvent.shiftKey](#attr-eventstreameventshiftkey)
- [EventStreamEvent.metaKey](#attr-eventstreameventmetakey)

**Flags**: R

---
## Attr: EventStreamEvent.dragCanceled

### Description
Set on the event captured at the end of a drag if the drag is canceled. This is normally an event such as `dragStop`, `dragRepositionStop`, `dragResizeStop`, or `dragSelectStop`, but if [drag events](EventStream.md#attr-eventstreamcapturedragevents) aren't being captured, this property may be set on the `mouseUp` ending the drag.

**Flags**: R

---
## Attr: EventStreamEvent.errorEvent

### Description
Present along with [EventStreamEvent.errorTrace](#attr-eventstreameventerrortrace) and [EventStreamEvent.threadCode](#attr-eventstreameventthreadcode) if the event triggering the error wasn't already captured, and required adding a new event. If a stream is configured to [capture event errors](EventStream.md#attr-eventstreamcaptureeventerrors), then through error reporting it may capture [EventStreamEvent.eventType](#attr-eventstreameventeventtype)s not specified by the filters.

### See Also

- [EventStreamEvent.eventType](#attr-eventstreameventeventtype)
- [EventStreamEvent.errorTrace](#attr-eventstreameventerrortrace)

**Flags**: R

---
## Attr: EventStreamEvent.shiftKey

### Description
Present for [key events](EventStream.md#attr-eventstreamcapturekeyevents) if the shift key was down when the event got triggered. Otherwise, not present.

### See Also

- [EventStreamEvent.keyName](#attr-eventstreameventkeyname)
- [EventStreamEvent.ctrlKey](#attr-eventstreameventctrlkey)
- [EventStreamEvent.metaKey](#attr-eventstreameventmetakey)

**Flags**: R

---
