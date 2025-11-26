# Including custom elements in the tab order

[← Back to API Index](../reference.md)

---

## KB Topic: Including custom elements in the tab order

### Description
Non-SmartClient user interface components which can receive focus, such as native HTML elements or third party widgets may be included the tab order of a SmartClient page.  
For example, if a native HTML ``<input>`` element is written into some Canvas as part of its contents, a developer would likely want this element to be included in the tab sequence for the page in its intuitive spot (between the canvas it is embedded in and any subsequent canvases on the page).

To achieve this a developer needs to take several steps:

*   A new (unique) entry for the focusable component should be added to the TabIndexManager, at the desired location in the tab sequence tree. In the case of an ``<input>`` element written into a Canvas, the developer would choose an arbitrary identifying string for the input element, and call the [TabIndexManager.addTarget](../classes/TabIndexManager.md#classmethod-tabindexmanageraddtarget) API, passing in the [ID of the canvas in which it is embedded](../classes/Canvas.md#method-canvasgetid) as the parentID parameter.
*   Once the entry has been registered, the developer may call [TabIndexManager.getTabIndex](../classes/TabIndexManager.md#classmethod-tabindexmanagergettabindex) to retrieve a a numeric tabIndex to apply to the element. This can be used when generating the HTML to write out for the element.
*   The generated numeric tabIndex for this entry will not be static. Various actions, such as [moving the canvas containing the item to a new parent](../classes/Canvas.md#method-canvasaddchild) would cause this value to change. The `tabIndexUpdated` callback parameter of the [TabIndexManager.addTarget](../classes/TabIndexManager.md#classmethod-tabindexmanageraddtarget) method is a notification which will be called when this occurs, and may be used to update the element's tab index if it has already been written into the DOM when the value changes.

In some situations, the SmartClient framework will intercept Tab keystroke events and explicitly manage focus navigation between elements. Cases where this occurs include moving between unmasked components when a [click mask](../classes/Canvas.md#method-canvasshowclickmask) is up, using the Tab key to navigate between editors embedded in a ListGrid during [grid editing](editing.md#kb-topic-grid-editing), and for any focusable UI embedded in a canvas where [Canvas.alwaysManageFocusNavigation](../classes/Canvas.md#attr-canvasalwaysmanagefocusnavigation) has been explicitly set to true.  
To have focusable, non-SmartClient elements participate in this explicit tab navigation, a couple of additional steps are required:

*   The `shiftFocusCallback` parameter should be passed to [TabIndexManager.addTarget](../classes/TabIndexManager.md#classmethod-tabindexmanageraddtarget) when registering an ID for the custom element. This is a callback developers should implement to put native focus into the target (or return false if this is not currently possible for some reason). It will be invoked automatically by the system when focus is being shifted programmatically
*   Developers should also explicitly intercept the keydown event on the element they write out, and for Tab (or Shift+Tab) keystrokes, check whether explicit focus navigation is currently required (by calling [TabIndexManager.useExplicitFocusNavigation](../classes/TabIndexManager.md#classmethod-tabindexmanageruseexplicitfocusnavigation), passing in the ID that was registered via [TabIndexManager.addTarget](../classes/TabIndexManager.md#classmethod-tabindexmanageraddtarget)), and if that returns true explicitly calling [TabIndexManager.shiftFocus](../classes/TabIndexManager.md#classmethod-tabindexmanagershiftfocus), and preventing default native behavior by invoking [preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) on the native event object.

---
