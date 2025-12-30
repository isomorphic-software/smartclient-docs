# Keyboard Events

[← Back to API Index](../reference.md)

---

## KB Topic: Keyboard Events

### Description
SmartClient allows keyboard events to be captured at the page level via [Page.registerKey](../classes/Page.md#classmethod-pageregisterkey) or [Page.setEvent](../classes/Page.md#classmethod-pagesetevent) or at the widget level via [Canvas.keyDown](../classes/Canvas.md#method-canvaskeydown), [Canvas.keyPress](../classes/Canvas.md#method-canvaskeypress), and [Canvas.keyUp](../classes/Canvas.md#method-canvaskeyup).

Details about the key events can be retrieved via static methods on the EventHandler class including [EventHandler.getKey](../classes/EventHandler.md#classmethod-eventhandlergetkey), [EventHandler.getKeyEventCharacter](../classes/EventHandler.md#classmethod-eventhandlergetkeyeventcharacter) and [EventHandler.getKeyEventCharacterValue](../classes/EventHandler.md#classmethod-eventhandlergetkeyeventcharactervalue).

As with other SmartClient event handling code, returning `false` will suppress the default native browser behavior.  
**Note:** browsers do not allow cancellation of some keys' default behaviors. These cases vary by browser, and wherever native cancellation is supported, returning false from your event handler should be sufficient to suppress the behavior.  
Some specific cases where default behavior cancellation is not always possible include:

*   Some function keys (`f1, f3, f5,` etc) which trigger native browser behavior. \[These can be suppressed in Internet Explorer and Mozilla Firefox but not in some other browsers such as Safari / Chrome, etc\]
*   Some accelerator key combos such as `Alt+f3`
*   The "Meta" key (the `Windows` / `Apple` key to show OS level menu)

If you do want to include functionality for these keys in your application, we'd recommend testing against your expected users' browser types. It is also worth considering whether by changing the functionality of these standard browser keys you may provide an unexpected user experience (for example a user may press "f5" in an attempt to reload the application and be surprised by this triggering some alternative functionality in your application).

### Related

- [EventHandler.getKeyEventCharacterValue](../classes/EventHandler.md#classmethod-eventhandlergetkeyeventcharactervalue)
- [EventHandler.getKeyEventCharacter](../classes/EventHandler.md#classmethod-eventhandlergetkeyeventcharacter)
- [EventHandler.getKey](../classes/EventHandler.md#classmethod-eventhandlergetkey)
- [EventHandler.shiftKeyDown](../classes/EventHandler.md#classmethod-eventhandlershiftkeydown)
- [EventHandler.ctrlKeyDown](../classes/EventHandler.md#classmethod-eventhandlerctrlkeydown)
- [EventHandler.altKeyDown](../classes/EventHandler.md#classmethod-eventhandleraltkeydown)

---
