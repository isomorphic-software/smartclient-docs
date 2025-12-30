# EventHandler Documentation

[← Back to API Index](../reference.md)

---

## Class: EventHandler

### Description
The ISC system provides a predictable cross-browser event-handling mechanism for ISC widgets. Events can be handled both at the page level (i.e., globally), and at the level of individual widgets.

With the exception of a few page-specific events ('load', 'unload', 'idle' and 'resize'), events are processed in the following sequence:

1\. The event is sent to any global (page-level) event handlers. These handlers can cancel further propagation of the event by returning false. You can register to listen for any of the events linked in the seeAlso section (below) by calling [Page.setEvent](Page.md#classmethod-pagesetevent) method.

2\. If the event occurred on a form element or a link, it is passed on to the browser so that the element will perform its default action. No widget receives the event.

3\. If the event occurred on an enabled widget (but not on a form element or link inside the widget), it is sent to that widget's event handler, if any. This handler can cancel further propagation of the event by returning false. An "enabled" widget is any widget that defines an event handler for one of the supported events. Interceptable events are defined in the ["widgetEvents" section of Canvas](#class-canvas-methods-events).

4\. The event is "bubbled" up to the widget's parent in the containment hierarchy, if any. Again, the parent's handler for the event can cancel further propagation by returning false. This step is repeated, with the event "bubbling" up through the containment hierarchy, until a top-level widget is reached or the event is explicitly canceled. In brief, the ISC event model offers the best features of browser event models:

*   Page-first event handling allows you to reliably process or cancel any event before it affects the objects on the page.
*   Event "bubbling" ensures that parent widgets receive events sent to their children, and allows you to create generalized parent-level handlers rather than duplicating code in each child.

Note: Canceling propagation of an event may cancel its side effects as well, including the generation of other (synthetic) events. For example, if a global mouseDown handler returns false, drag-and-drop events will not be generated. Specific effects are discussed in the descriptions of the various events in the following sections.

SmartClient libraries will not interfere with native event handling when events occur outside of a target widget. You can therefore have HTML that is not ISC-based on the same page as widget objects that will react to native events as you would expect.

You can use isc.Event as an alias for isc.EventHandler.

### Groups

- eventHandling

### See Also

- [PageEvent](../reference.md#type-pageevent)
- [Page.setEvent](Page.md#classmethod-pagesetevent)
- [Page.clearEvent](Page.md#classmethod-pageclearevent)
- [Canvas#methods#widgetEvents](#class-canvas-methods-widgetevents)

---
## ClassAttr: EventHandler.STOP_BUBBLING

### Description
Return this constant from a child event to stop the event propagating to its parent, without suppressing any native browser handling associated with the event. Developers should not need to modify this value - it should be treated as read-only in most circumstances.

**Flags**: IRA

---
## ClassAttr: EventHandler.synchronousFocusNotifications

### Description
Advanced property governing whether focus and blur notifications throughout the SmartClient system should be fired synchronously in Internet Explorer and Microsoft Edge, as they are in other browsers.

Internet Explorer differs from other supported browsers in that the native `onfocus` and `onblur` browser events are fired asynchronously. In all other browsers these handlers are fired synchronously.  
Historically, SmartClient focus change event notifications such as [Canvas.focusChanged](Canvas.md#method-canvasfocuschanged) and [FormItem.focus](FormItem.md#method-formitemfocus) / [FormItem.blur](FormItem.md#method-formitemblur) were fired from these native event handlers, meaning that they would also be asynchronous in Internet Explorer and synchronous in all other browsers.  
Internet Explorer does provide developers with a separate focus-change notification which fires synchronously in the form of the `focusin` and `focusout` events (documented [here](http://www.w3schools.com/jsref/event_onfocusin.asp)).  
When synchronousFocusNotifications is set to `true` the SmartClient system will leverage these events to provide synchronous notifications in Internet Explorer.

For example, consider a Canvas with a 'focusChanged' handler, as follows:

```
 // ... Canvas definition
 isc.Canvas.create({
     ID:"testCanvas", backgroundColor:"lightblue",
     contents:"testCanvas",
     canFocus:true,
     focusChanged:function (hasFocus) {
         this.logWarn('focusChanged:' + hasFocus);
     },
     autoDraw:true
 });
 
```
...along with the following code to put focus into that canvas:
```
 // ... Code to execute in the flow of the application
 isc.logWarn("Before calling focus");
 testCanvas.focus();
 isc.logWarn("After calling focus");
 
```
If `synchronousFocusNotifications` is false, the focus changed notification will be fired asynchronously in Internet Explorer, meaning the order of events logged in the developer console would be:
```
 WARN:Log:Before calling focus
 WARN:Log:After calling focus
 WARN:Canvas:testCanvas:focusChanged:true
 
```
In all other browsers, the focus changed notification is synchronous:
```
 WARN:Log:Before calling focus
 WARN:Canvas:testCanvas:focusChanged:true
 WARN:Log:After calling focus
 
```
Setting `synchronousFocusNotifications` to true makes event notifications synchronous in Internet Explorer as well.

As of SmartClient version 11.1 (SmartGWT version 6.1), this property is `true` by default. For backwards compatibility purposes, it may be explicitly set to `false` to reinstate the previous asynchronous focus notification behavior in Internet Explorer, should application code depend on this behavior.

**Flags**: IRWA

---
## ClassAttr: EventHandler.ALL_EDGES

### Description
Constant containing the full set of edges a component may be resized from. When a component is marked as canDragResize, this will be the default set of edges from which it may be resized.

**Flags**: IR

---
## ClassAttr: EventHandler.showNoDropIndicator

### Description
If set to true, when the user drags a [canDrop:true](Canvas.md#attr-canvascandrop) canvas over any component with [Canvas.canAcceptDrop](Canvas.md#attr-canvascanacceptdrop) set to false or where [Canvas.willAcceptDrop](Canvas.md#method-canvaswillacceptdrop) returns false, the [no-drop cursor](Canvas.md#attr-canvasnodropcursor) will be shown automatically to indicate this is not a valid drop point.

This property can be modified at runtime, meaning a developer could choose to show the no drop indicator for specific drag/drop interactions by changing the value from a dragStart handler or similar.

Note that when this property is false, developers may still use the [Canvas.dropMove](Canvas.md#method-canvasdropmove) handler for potential drop targets and use [Canvas.setCursor](Canvas.md#method-canvassetcursor) to explicitly indicate invalid drop areas within a widget. This is the approach used by default for [TreeGrid](TreeGrid.md#class-treegrid) drag/drop interactions, for example.

**Flags**: IRW

---
## ClassAttr: EventHandler.IDLE_DELAY

### Description
amount of time between idle messages (msec)

**Flags**: IRWA

---
## ClassMethod: EventHandler.setDragOffset

### Description
Sets the initial coordinate offset of the last event, typically a mouseDown or touchStart, from the drag target. For example, when grabbing and dragging a [Scrollbar](Scrollbar.md#class-scrollbar) thumb with the mouse, you'd expect positive coordinates that reflect your position relative to the top, left corner of the thumb. If a drag tracker will be used, call [EventHandler.setDragTracker](#classmethod-eventhandlersetdragtracker) instead, which takes optional arguments `offsetX` and `offsetY` that act similarly to those passed to this method.

Your canvas can call this method to set the initial drag offset to whatever you want like so:

```
    dragStart : function () {
        isc.EventHandler.setDragOffset(5, 20);
    }
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| offsetX | [int](../reference.md#type-int) | false | — | initial x-offset for the drag |
| offsetY | [int](../reference.md#type-int) | false | — | initial y-offset for the drag |

### Groups

- dragdrop

### See Also

- [Canvas.dragStart](Canvas.md#method-canvasdragstart)

---
## ClassMethod: EventHandler.getX

### Description
Return the page-relative X (horizontal) coordinate of an event.

### Returns

`[int](../reference.md#type-int)` — x-coordinate in page coordinate space

### Groups

- mouseEvents

---
## ClassMethod: EventHandler.rightButtonDown

### Description
Returns true if the right mouse button is being pressed.

### Returns

`[Boolean](#type-boolean)` — true == right button is down, false == up

### Groups

- mouseEvents

### See Also

- [EventHandler.leftButtonDown](#classmethod-eventhandlerleftbuttondown)
- [EventHandler.middleButtonDown](#classmethod-eventhandlermiddlebuttondown)

---
## ClassMethod: EventHandler.middleButtonDown

### Description
Returns true if the middle mouse button is being pressed.

Checking whether the middle mouse button is pressed can be used to implement power user shortcuts; however, note that many pointing devices do not have a middle button. Thus, the application should **not** require the user to press a middle button in order to perform some action.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the middle mouse button is pressed; false otherwise.

### Groups

- mouseEvents

### See Also

- [EventHandler.leftButtonDown](#classmethod-eventhandlerleftbuttondown)
- [EventHandler.rightButtonDown](#classmethod-eventhandlerrightbuttondown)

**Flags**: A

---
## ClassMethod: EventHandler.leftButtonDown

### Description
Returns true if the left mouse button is being pressed.

### Returns

`[Boolean](#type-boolean)` — true == left button is down, false == up

### Groups

- mouseEvents

### See Also

- [EventHandler.middleButtonDown](#classmethod-eventhandlermiddlebuttondown)
- [EventHandler.rightButtonDown](#classmethod-eventhandlerrightbuttondown)

---
## ClassMethod: EventHandler.getDragTarget

### Description
Returns the current dragTarget. This is the component on which the drag and drop interaction was initiated. This only returns something meaningful during a drag and drop interaction.

### Returns

`[Canvas](#type-canvas)` — The dragTarget.

### Groups

- mouseEvents

### See Also

- [Canvas.dragTarget](Canvas.md#attr-canvasdragtarget)

**Flags**: A

---
## ClassMethod: EventHandler.getWheelDeltaX

### Description
Horizontal scroll delta reported by a [mouseWheel](Canvas.md#method-canvasmousewheel) event (such as a horizontal swipe on a track-pad).

Returns a numeric value indicating how far the mouse wheel was rotated / the magnitude of the scroll gesture. This value will be positive if the user scrolled the mousewheel to the right, negative if scrolled in the other direction.

### Returns

`[float](../reference.md#type-float)` — numeric value indicating how far the mouse wheel was rotated.

### See Also

- [EventHandler.getWheelDeltaY](#classmethod-eventhandlergetwheeldeltay)

---
## ClassMethod: EventHandler.getKeyEventCharacter

### Description
Return the character for the current key being pressed. Note that this is only set reliably for keyPress events on character keys.

### Returns

`[String](#type-string)` — Character the user entered. May be null for non-character keys.

### Groups

- keyboardEvents

---
## ClassMethod: EventHandler.getTarget

### Description
Return the canvas that is the target of the mouse event. Returns null if no canvas found.

### Returns

`[Canvas](#type-canvas)` — event target canvas

### Groups

- mouseEvents

---
## ClassMethod: EventHandler.getNativeDragData

### Description
For a cross-frame drag, retrieves the data made available when the drag was initiated in the foreign frame via [EventHandler.setNativeDragData](#classmethod-eventhandlersetnativedragdata).

Can only be called during the [Canvas.drop](Canvas.md#method-canvasdrop) event (or methods called during the handling of that event, such as [ListGrid.recordDrop](ListGrid_2.md#method-listgridrecorddrop)); will return null if called at any other time, or if called during a non-HTML5 drag and drop.

### Returns

`[Object](../reference_2.md#type-object)` — data made available in the foreign frame

---
## ClassMethod: EventHandler.getKey

### Description
Return the name of the key for the event passed in. Note that this is only set reliably for keyboard events.

### Returns

`[KeyName](../reference.md#type-keyname)` — Key Name

### Groups

- keyboardEvents

---
## ClassMethod: EventHandler.targetIsMasked

### Description
Return whether this Canvas is masked by a clickMask (see [Canvas.showClickMask](Canvas.md#method-canvasshowclickmask)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | widget to check |

### Returns

`[Boolean](#type-boolean)` — true if masked, false if not masked.

### Groups

- clickMask

**Flags**: A

---
## ClassMethod: EventHandler.getDragRect

### Description
During a drag with [dragAppearance](Canvas.md#attr-canvasdragappearance) of either "target" or "outline", returns the page-relative coordinates of whatever element is being dragged.

Calling this method allows you to write drag and drop logic that works identically even if `dragAppearance` is subsequently changed.

### Returns

`[Rect](#type-rect)` — global (page-relative) coordinates and size of the dragged element, as a 4-element array \[left,top,width,height\], or null if not dragging

### Groups

- dragdrop

---
## ClassMethod: EventHandler.setDragTrackerImage

### Description
This API may be called to set the native HTML5 drag tracker image. The `x` and `y` parameters may be specified to affect the placement of the drag tracker image relative to the mouse cursor. The size of the drag tracker image is the intrinsic size of the image. Browsers may apply certain visual effects (such as a slight transparency) to this image.

Can only be called during the [Canvas.dragStart](Canvas.md#method-canvasdragstart) event (or methods called during the handling of that event).

**NOTES:**

*   Not supported in Opera 12.x or Safari.
*   For best results, this image should be preloaded. Otherwise, the image might not appear for the first drag using this image.
*   This API does not work in Chrome or Firefox on Windows 7 if the "Use visual styles on windows and buttons" setting is turned off.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [SCImgURL](../reference_2.md#type-scimgurl) | false | — | image source |
| x | [int](../reference.md#type-int) | true | — | offset-x from the mouse cursor |
| y | [int](../reference.md#type-int) | true | — | offset-y from the mouse cursor |

### Groups

- dragdrop

---
## ClassMethod: EventHandler.setNativeDragData

### Description
Sets the data available in a cross-frame HTML5 drag (see [Canvas.useNativeDrag](Canvas.md#attr-canvasusenativedrag)).

Data provided to this method must be valid for serialization to JSON via the [JSONEncoder](JSONEncoder.md#class-jsonencoder), or can simply be a String.

Can only be called during the [Canvas.dragStart](Canvas.md#method-canvasdragstart) event (or methods called during the handling of that event).

Do not pass in sensitive data (e.g. passwords, auth/session tokens, credit card numbers, SSNs, etc.).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Object](../reference_2.md#type-object)|[String](#type-string) | false | — | data to make available to foreign frames |
| strData | [String](#type-string) | true | — | text data to set. This is the text that users may see if the drag is dropped into an external application such as Notepad or a non-SmartClient/Smart GWT web application. |

---
## ClassMethod: EventHandler.altKeyDown

### Description
Return true if the alt (option) key is being held down. Note that this is only set reliably for keyboard events.

### Returns

`[Boolean](#type-boolean)` — true == alt key is down

### Groups

- keyboardEvents

---
## ClassMethod: EventHandler.getKeyEventCharacterValue

### Description
Returns the numeric characterValue reported by the browser. Only available on keyPress events, and only for character (or ascii control) keys

### Returns

`[int](../reference.md#type-int)` — Numeric character value reported by the browser (ASCII value of the key pressed)

### Groups

- keyboardEvents

---
## ClassMethod: EventHandler.shiftKeyDown

### Description
Return true if the shift key is being held down. Note that this is only set reliably for keyboard events.

### Returns

`[Boolean](#type-boolean)` — true == shift key is down

### Groups

- keyboardEvents

---
## ClassMethod: EventHandler.getY

### Description
Return the page-relative Y (vertical) coordinate of an event.

### Returns

`[int](../reference.md#type-int)` — y-coordinate in page coordinate space

### Groups

- mouseEvents

---
## ClassMethod: EventHandler.setDragTracker

### Description
Set the HTML for the drag tracker that follows the mouse during a drag and drop interaction.

Your canvas can use this routine to set the drag tracker to whatever HTML you want like so:

```
    dragStart : function () {
        isc.EventHandler.setDragTracker('Your contents here');
    }
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| html | [String](#type-string) | false | — | HTML for the tracker |
| newWidth | [int](../reference.md#type-int) | true | — | new width for the tracker. Default value: 10 |
| newHeight | [int](../reference.md#type-int) | true | — | new height for the tracker. Default value: 10 |
| offsetX | [int](../reference.md#type-int) | true | — | x-offset for the tracker |
| offsetY | [int](../reference.md#type-int) | true | — | y-offset for the tracker |
| properties | [Canvas Properties](#type-canvas-properties) | true | — | properties to configure the dragTracker |

### Groups

- dragdrop
- dragTracker

---
## ClassMethod: EventHandler.getFocusCanvas

### Description
Method to return the [canvasFocus:true](Canvas.md#attr-canvascanfocus) canvas with current keyboard focus.

### Returns

`[Canvas](#type-canvas)` — Current focus canvas

---
## ClassMethod: EventHandler.getWheelDelta

### Description
Applies to [mouseWheel](Canvas.md#method-canvasmousewheel) events only. Returns a numeric value indicating how far the mouse wheel was rotated. This value will be positive if the user scrolled the mousewheel forward or up, or negative if scrolled in the other direction. For a standard wheel-mouse, an increment of 1 relates to the smallest possible rotation of the mouse wheel. For other scrolling devices, such as scroll gestures on a track pad, wheel delta may be reported in finer grained increments (causing this method to return a fractional value).

Note that behavior for trackpad scroll-gestures may differ by browser, but where separate vertical and horizontal scroll information is available, this method refers to a vertical scroll gesture.

Developers should also be aware that some browsers and operating systems allow the user to configure the sensitivity of the mouse wheel or trackpad, which may change this value.

### Returns

`[float](../reference.md#type-float)` — numeric value indicating how far the mouse wheel was rotated.

**Deprecated**

---
## ClassMethod: EventHandler.getNativeMouseTarget

### Description
Returns the natively reported target (or source) DOM element for the current mouse event. **NOTE:** SmartClient cannot guarantee that the same element will be reported in all browser/platform configurations for all event types. If you wish to make use of this value, we recommend testing your use case in all target browser configurations.

### Returns

`[DOMElement](#type-domelement)` — native DOM element over which the mouse event occurred

**Flags**: A

---
## ClassMethod: EventHandler.ctrlKeyDown

### Description
Return true if the control key is being held down. Note that this is only set reliably for keyboard events.

### Returns

`[Boolean](#type-boolean)` — true == control key is down

### Groups

- keyboardEvents

---
## ClassMethod: EventHandler.getWheelDeltaY

### Description
Applies to [mouseWheel](Canvas.md#method-canvasmousewheel) events only. Returns a numeric value indicating how far the mouse wheel was rotated. This value will be positive if the user scrolled the mousewheel forward or up, or negative if scrolled in the other direction. For a standard wheel-mouse, an increment of 1 relates to the smallest possible rotation of the mouse wheel. For other scrolling devices, such as scroll gestures on a track pad, wheel delta may be reported in finer grained increments (causing this method to return a fractional value).

Note that behavior for trackpad scroll-gestures may differ by browser, but where separate vertical and horizontal scroll information is available, this method refers to a vertical scroll gesture.

Developers should also be aware that some browsers and operating systems allow the user to configure the sensitivity of the mouse wheel or trackpad, which may change this value.

### Returns

`[float](../reference.md#type-float)` — numeric value indicating how far the mouse wheel was rotated.

### See Also

- [EventHandler.getWheelDeltaX](#classmethod-eventhandlergetwheeldeltax)

---
