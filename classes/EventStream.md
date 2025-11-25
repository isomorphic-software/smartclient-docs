# EventStream Documentation

[← Back to API Index](../main.md)

---

## Class: EventStream

### Description
A `EventStream` captures event details as JavaScript objects as they are handled by the [EventHandler](EventHandler.md#class-eventhandler). The event target [canvas](Canvas.md#class-canvas) ID and [class name](Class.md#method-classgetclassname) as well the [locator](../main_2.md#type-autotestlocator) are included, as available. Event-specific data (for example, the [KeyName](../main_2.md#type-keyname) for keyboard events) are also included where appropriate. See [EventStreamEvent](../main.md#object-eventstreamevent) for more information.

You can configure the stream to capture most DOM event types and other useful events, such as [relogins](../kb_topics/relogin.md#kb-topic-relogin) and JavaScript errors that are triggered by events:

| Event Category | Includes (source DOM eventType(s) or description) | Controlling Attribute | From DOM Event? |
|---|---|---|---|
| click events | mouseDown, mouseUp, click, dblClick | [captureClickEvents](#attr-eventstreamcaptureclickevents) | Y |
| move events | mouseMove, mouseOut | [captureMoveEvents](#attr-eventstreamcapturemoveevents) | Y |
| key events | keyDown, keyPress, keyUp | [captureKeyEvents](#attr-eventstreamcapturekeyevents) | Y |
| drag events | dragStart, dragMove, dragStop | [captureDragEvents](#attr-eventstreamcapturedragevents) | Y |
| context menu events | contextMenu | [captureMenuEvents](#attr-eventstreamcapturemenuevents) | Y |
| mouse wheel events | mouseWheel | [captureWheelEvents](#attr-eventstreamcapturewheelevents) | Y |
| page events | load, unload, resize | [capturePageEvents](#attr-eventstreamcapturepageevents) | Y |
| login events | Successful [relogin](../kb_topics/relogin.md#kb-topic-relogin) via the [RPCManager](RPCManager.md#class-rpcmanager) | [captureLoginEvents](#attr-eventstreamcaptureloginevents) | N |
| [Reify](../kb_topics/reify.md#kb-topic-reify-overview) file events | Project and screen (auto)saves and loads | [captureDSFileEvents](#attr-eventstreamcapturedsfileevents) | N |
| event errors | JavaScript exceptions | [captureEventErrors](#attr-eventstreamcaptureeventerrors) | N |

(Pointer and touch equivalents to mouse events have not been listed above. See the associated attribute for a more inclusive list.)

Note that several types of DOM events can be collapsed so that one event is reported instead of many if they occur over the same target. You can enable collapsing for [move and drag events](#attr-eventstreamcollapsemoveevents), [key events](#attr-eventstreamcollapsekeyevents), [wheel events](#attr-eventstreamcollapsewheelevents), and [page events](#attr-eventstreamcollapsepageevents). A [stream capture limit](#attr-eventstreammaxsize) is also supported via circular buffering, so that only the most recent events are preserved. All available events can be returned as an array of [EventStreamEvent](../main.md#object-eventstreamevent) via [getEvents()](#method-eventstreamgetevents).

A `EventStream` will start capturing events as soon as it's created by default, but if you set [autoStart](#attr-eventstreamautostart): false, you can start capturing manually by calling [start()](#method-eventstreamstart). Calling [end()](#method-eventstreamend) will end capturing and return the [EventStreamData](../main.md#object-eventstreamdata).

### Groups

- reify
- experimental

### See Also

- [EventHandler](EventHandler.md#class-eventhandler)
- [RPCManager](RPCManager.md#class-rpcmanager)

---
## ClassAttr: EventStream.skipVerifyEvents

### Description
When true, "verify" events will be skipped during event execution via [EventStream.runEvents](#classmethod-eventstreamrunevents). This allows running event streams for their side effects without failing on verification failures.

### Groups

- autoTest

**Flags**: IRW

---
## Attr: EventStream.collapseMoveEvents

### Description
Whether mouse or touch-motion related events (including dragging) with the same [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) and [targetID](EventStreamEvent.md#attr-eventstreameventtargetid) should be collapsed into a single event.

Note that if an error is thrown while handling an event, it won't be collapsed, but see [EventStream.minErrorReportingInterval](#attr-eventstreamminerrorreportinginterval).

### See Also

- [EventStream.captureMoveEvents](#attr-eventstreamcapturemoveevents)

**Flags**: IR

---
## Attr: EventStream.capturePageEvents

### Description
Whether page-level events such as a page load or resize should be captured by the stream. Multple adjacent page events having the same eventType will be collapsed into one if [EventStream.collapsePageEvents](#attr-eventstreamcollapsepageevents) is true.

Includes such [eventType](EventStreamEvent.md#attr-eventstreameventeventtype)s as `load`, `unload`, and `resize`.

**Flags**: IR

---
## Attr: EventStream.collapseWheelEvents

### Description
Whether mouse wheel events with the same [targetID](EventStreamEvent.md#attr-eventstreameventtargetid) and scroll directions should be collapsed into a single event, containing a sum of the [delta offsets](EventStreamEvent.md#attr-eventstreameventdeltax) from the original events.

Note that if an error is thrown while handling an event, it won't be collapsed, but see [EventStream.minErrorReportingInterval](#attr-eventstreamminerrorreportinginterval).

### See Also

- [EventStream.captureWheelEvents](#attr-eventstreamcapturewheelevents)

**Flags**: IR

---
## Attr: EventStream.collapseKeyEvents

### Description
Whether to collapse adjacent `keyPress` events into one event where possible. Self-inserting keys will generally be collapsed by concatenating them into a single string, [EventStreamEvent.keyNames](EventStreamEvent.md#attr-eventstreameventkeynames). On the other hand, special keys such as "Esc" and "Backspace" will only be collapsed for repeating sequences of the same key, which will be reported as [EventStreamEvent.count](EventStreamEvent.md#attr-eventstreameventcount).

Note that if an error is thrown while handling an event, it won't be collapsed, but see [EventStream.minErrorReportingInterval](#attr-eventstreamminerrorreportinginterval).

### See Also

- [EventStream.captureKeyEvents](#attr-eventstreamcapturekeyevents)

**Flags**: IR

---
## Attr: EventStream.captureMenuEvents

### Description
Whether opening a context menu should be captured by the stream. This may occur due to mouse or keyboard interaction.

Includes the [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) `contextMenu`.

**Flags**: IR

---
## Attr: EventStream.autoStart

### Description
Whether the stream should automatically begin capturing events. If false, the steam won't start capturing events until [EventStream.start](#method-eventstreamstart) is called.

**Flags**: IR

---
## Attr: EventStream.minErrorReportingInterval

### Description
Number of seconds that must elapse before another event error will be reported. This allows you to avoid the stream getting flooded with likely duplicate errors that may be rapidly and repeatedly reported, due to mouseMove or repeatedly executing code. Setting the property to zero disables it (avoiding any timestamp checking).

Note that when an error is reported by the Framework, this property will be ignored if the last captured event triggered the error and has no [errorTrace](EventStreamEvent.md#attr-eventstreameventerrortrace), so that it effectively only prevents adding new events to the stream specifically to report errors. However, an [errorTrace](EventStreamEvent.md#attr-eventstreameventerrortrace) attached to an event within the reporting interval of the previous error won't prevent that event from being [collapsed](#attr-eventstreamcollapsemoveevents).

### See Also

- [EventStream.collapseMoveEvents](#attr-eventstreamcollapsemoveevents)
- [EventStream.collapseKeyEvents](#attr-eventstreamcollapsekeyevents)
- [EventStream.collapseWheelEvents](#attr-eventstreamcollapsewheelevents)
- [EventStream.collapsePageEvents](#attr-eventstreamcollapsepageevents)

**Flags**: IR

---
## Attr: EventStream.collapsePageEvents

### Description
Whether adjacgent page events with the same [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) should be collapsed into a single event.

Note that if an error is thrown while handling an event, it won't be collapsed, but see [EventStream.minErrorReportingInterval](#attr-eventstreamminerrorreportinginterval).

### See Also

- [EventStream.capturePageEvents](#attr-eventstreamcapturepageevents)

**Flags**: IR

---
## Attr: EventStream.captureWheelEvents

### Description
Whether mouse wheel events should be captured by the stream. If the preceding "wheel event" has the same [targetID](EventStreamEvent.md#attr-eventstreameventtargetid) and scroll directions, it will be replaced by the current one, subject to [EventStream.collapseWheelEvents](#attr-eventstreamcollapsewheelevents), with the [delta offsets](EventStreamEvent.md#attr-eventstreameventdeltax) in the "collapsed" event getting adjusted to be the sum of those from all the original events.

Includes the [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) `mouseWheel`.

**Flags**: IR

---
## Attr: EventStream.captureEventErrors

### Description
Whether to capture JavaScript errors. If an already-captured event triggered the error, the details will attached to that event. Otherwise, a separate event will be created, with the [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) of the last dispatched DOM event (i.e., there is no special "error" [eventType](EventStreamEvent.md#attr-eventstreameventeventtype).)

[EventStreamEvent](../main.md#object-eventstreamevent) records annotated or specially-reported with error details will contain an [errorTrace](EventStreamEvent.md#attr-eventstreameventerrortrace) with the error stack trace, and a [threadCode](EventStreamEvent.md#attr-eventstreameventthreadcode) reporting the thread ID from the [EventHandler](EventHandler.md#class-eventhandler) responsible for the error.

**Flags**: IR

---
## Attr: EventStream.captureClickEvents

### Description
Whether mouse button-driven events (or their touch equivalents) should be captured by the stream.

Includes such [eventType](EventStreamEvent.md#attr-eventstreameventeventtype)s as `mouseDown`, `mouseUp`, `click`, `doubleClk`, `pointerDown`, `pointerUp`, `pointerCancel`, `touchStart`, `touchEnd`, and `touchCancel`.

**Flags**: IR

---
## Attr: EventStream.captureKeyEvents

### Description
Whether keyboard input events should be captured by the stream. For non-modifier keys, which includes all the self-inserting visible keyboard characters, we capture only the `keyPress`, as `keyDown`/`keyUp` are generally not useful. Conversely, for modifier keys (e.g. Shift), we capture _only_ the `keyDown` and `keyUp`. events, and not the `keyPress`.

If [EventStream.collapseKeyEvents](#attr-eventstreamcollapsekeyevents) is true, multiple adjacent keyPress events may be collapsed into a single event for greater readability and a more compact event trace.

Note that if an error is thrown while handling an event, it will get reported regardless of this setting and the above capturing rules, but see [EventStream.minErrorReportingInterval](#attr-eventstreamminerrorreportinginterval). So for example an error handling a `keyDown` would still generally end up in the event trace, even for a self-inserting key such as "A".

**Flags**: IR

---
## Attr: EventStream.captureMoveEvents

### Description
Whether mouse or touch motion-related events (other than dragging) should be captured by the stream. Multple adjacent "move events" having the same [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) and [targetID](EventStreamEvent.md#attr-eventstreameventtargetid) will be collapsed into one if [EventStream.collapseMoveEvents](#attr-eventstreamcollapsemoveevents) is true.

Includes such [eventType](EventStreamEvent.md#attr-eventstreameventeventtype)s as `mouseMove`, `pointerMove`, `touchMove`, and `mouseOut`.

**Flags**: IR

---
## Attr: EventStream.captureLoginEvents

### Description
Whether [relogin](../kb_topics/relogin.md#kb-topic-relogin)s are captured by the stream. Login events are non-DOM events originating from the [RPCManager](RPCManager.md#class-rpcmanager) rather than the [EventHandler](EventHandler.md#class-eventhandler). Login events have a [transaction URL](EventStreamEvent.md#attr-eventstreameventurl).

Includes the [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) `relogin`.

**Flags**: IR

---
## Attr: EventStream.captureDragEvents

### Description
Whether dragging-related events should be captured by the stream. Multiple "drag move" type events that have the same [eventType](EventStreamEvent.md#attr-eventstreameventeventtype) and [targetID](EventStreamEvent.md#attr-eventstreameventtargetid) will be collapsed into one if [EventStream.collapseMoveEvents](#attr-eventstreamcollapsemoveevents) is true.

Includes such [eventType](EventStreamEvent.md#attr-eventstreameventeventtype)s as:

*   `dragStart`, `dragRepositionStart`, `dragResizeStart`, `dragSelectStart`,
*   `dragMove`, `dragRepositionMove`, `dragResizeMove`, `dragSelectMove`,
*   `dragStop`, `dragRepositionStop`, `dragResizeStop`, `dragSelectStop`,
*   `drop`, `dropOver`, and `dragLeave`.

**Flags**: IR

---
## Attr: EventStream.maxSize

### Description
Maximum number of events that will be stored by this `EventStream`. After `maxSize` events are captured, the oldest events will be overwritten. Set this property to `null` to capture events without ever overwriting.

**Flags**: IR

---
## ClassMethod: EventStream.getCypressEventScript

### Description
Generates a Cypress command snippet for a single event using our custom SC commands.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [EventStreamEvent](#type-eventstreamevent) | false | — | The event to translate into a Cypress command. |

### Returns

`[String](#type-string)` — A snippet like 'cy.getSC(locator).click()' or '.dblclick()', assuming our custom commands are loaded.

### Groups

- smartClientCypress
- autoTest

### See Also

- [EventStream.getCypressScriptFromData](#classmethod-eventstreamgetcypressscriptfromdata)

---
## ClassMethod: EventStream.evaluateVerifyEvent

### Description
Evaluates a "verify" event to check if the specified condition is met. A verify event can check component existence, data criteria, formulas, or custom scripts.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [EventStreamEvent](#type-eventstreamevent) | false | — | The verify event to evaluate with structure: - eventType: "verify" (required) - locator: AutoTest locator for target component (required) - description: Human-readable description (optional) - dataTarget: "data" | "selection" | "properties" (defaults to "data" for DBCs, "properties" otherwise) - criteria: AdvancedCriteria to match against dataTarget - matchType: "any" | "all" | "none" | "exact" | "one" (default "any") - matchCount: Expected count for matchType:"exact" (default 1) - formula: {text: "formula expression"} to evaluate - value: Expected value for formula/script comparison - operator: "equals" | "notEquals" | "greaterThan" | "lessThan" | "between" (default "equals") - script: Arbitrary script to run for verification - timeout: Max time to wait for verification (milliseconds, default 5000) |
| ruleScope | [Object](../main.md#type-object) | true | — | Optional ruleScope for formula/criteria evaluation |

### Returns

`[Object](../main.md#type-object)` — Result object with structure: - success: (Boolean) True if verification passed - error: (String) Error message if verification failed - actual: (Any) Actual value that was checked - expected: (Any) Expected value for comparison

### Groups

- autoTest

---
## ClassMethod: EventStream.getPlaywrightScriptFromData

### Description
Translates an array of EventStreamEvent objects into an array of Playwright command strings. Each command is formatted with 'await' for async execution.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| events | [Array of EventStreamEvent](#type-array-of-eventstreamevent) | false | — | Array of events to convert. |

### Returns

`[Array of String](#type-array-of-string)` — List of Playwright command snippets.

### Groups

- smartClientPlaywright
- autoTest

### See Also

- [EventStream.getPlaywrightEventScript](#classmethod-eventstreamgetplaywrighteventscript)
- [EventStream.getPlaywrightScript](#classmethod-eventstreamgetplaywrightscript)

---
## ClassMethod: EventStream.runEvents

### Description
Replays a sequence of recorded events in the live UI and logs each step.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| events | [Array of EventStreamEvent](#type-array-of-eventstreamevent) | false | — | Events to replay one by one. |
| speed | [Number](#type-number) | false | — | Milliseconds delay between each event. |
| textAreaLog | [TextAreaItem](#type-textareaitem) | false | — | Component where outcomes will be logged. |
| callback | [Function](#type-function) | false | — | Invoked once all events have been processed. |

### Groups

- smartClientCypress
- autoTest

### See Also

- [EventStream.getCypressScript](#method-eventstreamgetcypressscript)

---
## ClassMethod: EventStream.getPlaywrightScript

### Description
Builds a full Playwright test file by framing event commands in test.describe/test blocks. It adds a beforeEach with page.goto, viewport setup, optional waits, and then the test steps. All commands are properly async/await formatted for Playwright's asynchronous API.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| eventStream | [Array of EventStreamEvent](#type-array-of-eventstreamevent) | false | — | Array of events to convert. |
| targetUrl | [String](#type-string) | true | — | URL to visit in beforeEach; defaults to current page. |
| testName | [String](#type-string) | true | — | Name of the test() block; defaults to "Test". |
| testDescription | [String](#type-string) | true | — | Description of the test.describe() block; defaults to "Testing". |

### Returns

`[String](#type-string)` — Complete Playwright spec code ready to paste into a \`.spec.js\`.

### Groups

- smartClientPlaywright
- autoTest

### See Also

- [EventStream.getPlaywrightEventScript](#classmethod-eventstreamgetplaywrighteventscript)
- [EventStream.getPlaywrightScriptFromData](#classmethod-eventstreamgetplaywrightscriptfromdata)

---
## ClassMethod: EventStream.getPlaywrightEventScript

### Description
Generates a Playwright command snippet for a single event using our custom SC commands. Playwright commands are async, so all commands include 'await' and use page.\* methods.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [EventStreamEvent](#type-eventstreamevent) | false | — | The event to translate into a Playwright command. |

### Returns

`[String](#type-string)` — A snippet like 'await page.clickSC(locator)' or 'await page.dblclickSC(locator)', assuming our custom commands are loaded.

### Groups

- smartClientPlaywright
- autoTest

### See Also

- [EventStream.getPlaywrightScriptFromData](#classmethod-eventstreamgetplaywrightscriptfromdata)

---
## ClassMethod: EventStream.getCypressScriptFromData

### Description
Translates an array of EventStreamEvent objects into an array of Cypress command strings.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| events | [Array of EventStreamEvent](#type-array-of-eventstreamevent) | false | — | Array of events to convert. |

### Returns

`[Array of String](#type-array-of-string)` — List of Cypress command snippets.

### Groups

- smartClientCypress
- autoTest

### See Also

- [EventStream.getCypressEventScript](#classmethod-eventstreamgetcypresseventscript)
- [EventStream.getCypressScript](#method-eventstreamgetcypressscript)

---
## ClassMethod: EventStream.getEventDescription

### Description
Returns a human-readable description of an event action for logging purposes. Used during Mock Mode test generation to show what action is being taken.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| event | [EventStreamEvent](#type-eventstreamevent) | false | — | The event to describe. |

### Returns

`[String](#type-string)` — A description like "Taking action 'click' on component" or "Taking action 'keyPress' (Enter) on component"

### Groups

- autoTest

---
## Method: EventStream.end

### Description
Ends event capturing and returns the [EventStreamData](../main.md#object-eventstreamdata). Once ended, capturing cannot be restarted without losing all stored events.

### Returns

`[EventStreamData](#type-eventstreamdata)` — —

### See Also

- [EventStream.autoStart](#attr-eventstreamautostart)
- [EventStream.start](#method-eventstreamstart)

---
## Method: EventStream.getAsSeleneseCommands

### Description
Creates and returns Selenese that represents the events captured by the stream as an array of [Selenium commands](../main.md#object-seleniumcommand). Compare with [EventStream.getAsSeleneseHTML](#method-eventstreamgetasselenesehtml), where you'll also find more common details.

Just as when retrieving the Selenese as HTML, if a [EventStream.transformSelenese](#method-eventstreamtransformselenese) function has been defined, it's called before returning the Selenese.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [SeleneseSettings](#type-selenesesettings) | true | — | — |

### Returns

`[Array of SeleniumCommand](#type-array-of-seleniumcommand)` — —

### Groups

- automatedTesting
- experimental

---
## Method: EventStream.getCypressScript

### Description
Builds a full Cypress test file by framing event commands in describe/it blocks. It adds a beforeEach with cy.visit, viewport setup, optional waits, and then the test steps.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| eventStream | [EventStream](#type-eventstream) | false | — | Stream of events to convert. |
| targetUrl | [String](#type-string) | true | — | URL to visit in beforeEach; defaults to current page. |
| testName | [String](#type-string) | true | — | Name of the it() block; defaults to "Test". |
| testDescription | [String](#type-string) | true | — | Description of the describe() block; defaults to "Testing". |

### Returns

`[String](#type-string)` — Complete Cypress spec code ready to paste into a \`.spec.js\`.

### Groups

- smartClientCypress
- autoTest

### See Also

- [EventStream.getCypressEventScript](#classmethod-eventstreamgetcypresseventscript)
- [EventStream.getCypressScriptFromData](#classmethod-eventstreamgetcypressscriptfromdata)

---
## Method: EventStream.start

### Description
Starts capturing all enabled events. See the overview of [EventStream](#class-eventstream) for a list of filter properties you can configure to control which events are captured.

If called after [EventStream.end](#method-eventstreamend), capturing will restart, but all previously stored events will be lost.

### See Also

- [EventStream.autoStart](#attr-eventstreamautostart)
- [EventStream.end](#method-eventstreamend)

---
## Method: EventStream.getAsSeleneseHTML

### Description
Creates and returns Selenese that represents the events captured by the stream. This Selenese contains SmartClient-specific locators (scLocators), and SmartClient command extensions (e.g. "waitForElementClickable") that are discussed in our [Selenium](../kb_topics/usingSelenium.md#kb-topic-using-selenium-scripts-selenese) overview.

This method returns the Selenese as a string of HTML table rows, just as in an rctest.html file that you can directly execute with Selenium. Does not include the leading or trailing HTML, such as the `<BODY>` and `<TBODY>` tags; you'll need to wrap what's returned with the appropriate outer HTML tags to properly embed the table. If you'd rather have the Selenese returned as an array of [Selenium commands](../main.md#object-seleniumcommand), call [EventStream.getAsSeleneseCommands](#method-eventstreamgetasselenesecommands) instead.

To customize the returned Selenese, see [EventStream.transformSelenese](#method-eventstreamtransformselenese). Note that if the stream has [rolled over](#attr-eventstreammaxsize), the Selenese for the lost events will not be returned.

For example, in your application instance init code, you can create a stream like so:

```
     this.eventStream = isc.EventStream.create();
 
```
_... time passes where end user is interacting with your app ...._ Then to retrieve the Selenese you can call something like:
```
     var rcTestHTML = "<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">" +
                      "<body><table><tbody>" +
                      myApp.eventStream.getAsSeleneseHTML(true) +
                      "</tbody></table></body></html>";
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [SeleneseSettings](#type-selenesesettings) | true | — | — |

### Returns

`[HTML](../main.md#type-html)` — —

### Groups

- automatedTesting
- experimental

---
## Method: EventStream.setEventErrorListener

### Description
Installs a callback that will be called when the EventStream reports an [event error](#attr-eventstreamcaptureeventerrors), subject to the [error reporting interval](#attr-eventstreamminerrorreportinginterval). The callback will be passed all retained [EventStreamEvent](../main.md#object-eventstreamevent)s captured by the stream since the last time it was called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [EventErrorCallback](#type-eventerrorcallback) | false | — | Callback to fire when the stream encounters an event error, subject to the reporting interval |

### Groups

- prodErrorReport

### See Also

- [EventStream.maxSize](#attr-eventstreammaxsize)
- [EventStream.minErrorReportingInterval](#attr-eventstreamminerrorreportinginterval)

---
## Method: EventStream.getEvents

### Description
Returns all available captured events, oldest first. At most [EventStream.maxSize](#attr-eventstreammaxsize) events will be returned.

### Returns

`[Array of EventStreamEvent](#type-array-of-eventstreamevent)` — —

### See Also

- [EventStream.end](#method-eventstreamend)

---
## Method: EventStream.getStartTime

### Description
Returns when this stream started capturing events (i.e. when [EventStream.start](#method-eventstreamstart) got called).

### Returns

`[Date](#type-date)` — —

### See Also

- [EventStream.start](#method-eventstreamstart)
- [EventStream.autoStart](#attr-eventstreamautostart)

---
