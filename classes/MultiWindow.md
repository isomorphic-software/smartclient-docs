# MultiWindow Documentation

[← Back to API Index](../main.md)

---

## Class: MultiWindow

### Description
Provides tracking of other SmartClient browser windows opened by the original window, as [RemoteWindows](RemoteWindow.md#class-remotewindow).

Includes APIs for:

*   Registering event listeners for events on other windows
*   Opening a new window and finding a window by name
*   Moving, activating, or deactiving a window by name
*   Sharing DataSources and their caches between SmartClient windows
*   Sharing [messaging](../kb_topics/messaging.md#kb-topic-real-time-messaging) channels between SmartClient windows

Within the [OpenFin](https://developers.openfin.co/of-docs/docs) environment, the underlying implementation is actually via the [OpenFin](../main.md#class-openfin) class.

Reloading of child windows is in general supported (but see [MultiWindow.autoCopyDataSources](#classattr-multiwindowautocopydatasources)), while reloading the [main window](#classmethod-multiwindowismainwindow) currently is not.

### Groups

- experimental

---
## ClassAttr: MultiWindow.autoCopyDataSources

### Description
Should [DataSources](DataSource.md#class-datasource) from other OpenFin windows with SmartClient loaded be copied by reference into this window? Such DataSources will be copied:

*   when a page in another window is loaded (potentially several DataSources at once)
*   at the moment DataSources are created in a page loaded in another window (just that DataSource)

This property will default to true if OpenFin is present; otherwise, false.

Note that reloading a page that created DataSources copied by reference into other windows (via this property) is not supported.

**Flags**: IRW

---
## ClassAttr: MultiWindow.shareMessageChannels

### Description
Should this window share [Realtime Messaging](../kb_topics/messaging.md#kb-topic-real-time-messaging) channels with other windows?

This property will default to true if OpenFin is present; otherwise, false.

**Flags**: IRW

---
## ClassMethod: MultiWindow.resize

### Description
Resizes e existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| width | [number](#type-number) | false | — | desired new width |
| height | [number](#type-number) | false | — | desired new height |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) moved |

---
## ClassMethod: MultiWindow.minimize

### Description
Minimizes the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) minimized |

---
## ClassMethod: MultiWindow.getDataContext

### Description
Returns the [DataContext](../main.md#object-datacontext) provided by the [MultiWindow.open](#classmethod-multiwindowopen) call that opened this window, or a newly created (on demand) [DataContext](../main.md#object-datacontext) if this is the main application window, or no DataContext was provided.

### Returns

`[DataContext](#type-datacontext)` — [DataContext](../main.md#object-datacontext) for this window

---
## ClassMethod: MultiWindow.restore

### Description
Restores the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) restored |

---
## ClassMethod: MultiWindow.getLocalWindow

### Description
Returns the [RemoteWindow](RemoteWindow.md#class-remotewindow) instance for the current window (where the method was called).

### Returns

`[RemoteWindow](#type-remotewindow)` — instance wrapping the current window

---
## ClassMethod: MultiWindow.show

### Description
Shows the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) shown |

---
## ClassMethod: MultiWindow.otherWindowsChanged

### Description
Notification fired when the set of other [RemoteWindows](RemoteWindow.md#class-remotewindow) changes or requires re-synchronization due a call to [create()](Class.md#classmethod-classcreate), [close()](RemoteWindow.md#method-remotewindowclose), or a page reload in a different RemoteWindow.

This method has no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| otherWindows | [Array of RemoteWindow](#type-array-of-remotewindow) | false | — | current set of other RemoteWindows. |

---
## ClassMethod: MultiWindow.getParentWindow

### Description
Returns the parent [RemoteWindow](RemoteWindow.md#class-remotewindow) instance that opened this window.

### Returns

`[RemoteWindow](#type-remotewindow)` — instance wrapping the parent window or null

---
## ClassMethod: MultiWindow.clearEvent

### Description
Unregisters a previously registered window event listener. The event type and ID returned by the original [MultiWindow.setEvent](#classmethod-multiwindowsetevent) call should be passed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| eventType | [MultiWindowEvent](../main_2.md#type-multiwindowevent) | false | — | event type to register |
| ID | [number](#type-number) | true | — | ID of the event to clear. If not specified, all events of eventType will be cleared. |

### See Also

- [MultiWindow.setEvent](#classmethod-multiwindowsetevent)

---
## ClassMethod: MultiWindow.bringToFront

### Description
Brings the existing window with the specified name to the top of the window stack.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) is brought to the front |

---
## ClassMethod: MultiWindow.deactivate

### Description
Deactivates (blurs) the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) deactivated |

---
## ClassMethod: MultiWindow.open

### Description
Opens a new window with the specified URL, name, and [DataContext](../main.md#object-datacontext).

Note that if the provided window name already exists, that window will just be [activated](#classmethod-multiwindowactivate), and though the callback will be run, the supplied url, dataContext, windowSettings, and classSettings will be ignored.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| url | [URL](../main_2.md#type-url) | false | — | url to open in the window or null to reuse the current url |
| name | [String](#type-string) | false | — | unique window name to open as a new window |
| dataContext | [DataContext](#type-datacontext) | true | — | dataContext to apply to window |
| callback | [RemoteWindowBooleanCallback](#type-remotewindowbooleancallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) created or activated (parameter true if created) |
| windowSettings | [BrowserWindowSettings](#type-browserwindowsettings) | true | — | settings applied to child browser window |
| classSettings | [MultiWindowSettings](#type-multiwindowsettings) | true | — | settings for child [MultiWindow](#class-multiwindow) class |

---
## ClassMethod: MultiWindow.move

### Description
Moves the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| x | [number](#type-number) | false | — | desired x-offset of left edge |
| y | [number](#type-number) | false | — | desired y-offset of top edge |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) moved |

---
## ClassMethod: MultiWindow.close

### Description
Closes the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| force | [boolean](../main.md#type-boolean) | true | — | whether to force it closed |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) closed |

---
## ClassMethod: MultiWindow.isMainWindow

### Description
Returns whether this [RemoteWindow](RemoteWindow.md#class-remotewindow) wraps the main application window.

### Returns

`[boolean](../main.md#type-boolean)` — whether this instance wraps the main application window

---
## ClassMethod: MultiWindow.getOtherWindows

### Description
Returns a list of [RemoteWindow](RemoteWindow.md#class-remotewindow) for the other currently known windows (excluding the [local window](#classmethod-multiwindowgetlocalwindow)). This would typically only be used to initialize logic dependent on other windows. You'd want to observe [MultiWindow.otherWindowsChanged](#classmethod-multiwindowotherwindowschanged) to ensure you keep things updated as windows are opened or closed.

### Returns

`[Array of RemoteWindow](#type-array-of-remotewindow)` — current set of other RemoteWindows.

---
## ClassMethod: MultiWindow.maximize

### Description
Maximizes the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) maximized |

---
## ClassMethod: MultiWindow.setEvent

### Description
Registers a window event listener to be called whenever the event type occurs for any window in the application.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| eventType | [MultiWindowEvent](../main_2.md#type-multiwindowevent) | false | — | event type to register |
| listener | [MultiWindowEventCallback](#type-multiwindoweventcallback) | false | — | function to be called when event fires |

### Returns

`[number](#type-number)` — ID number of this event, may be used to remove the event

### See Also

- [MultiWindow.clearEvent](#classmethod-multiwindowclearevent)

---
## ClassMethod: MultiWindow.activate

### Description
Activates (focuses) the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) activated |

---
## ClassMethod: MultiWindow.isShowing

### Description
Checks whether a window with the specified name is showing. Callback returns null if the window cannot be found; otherwise returns true or false according as it's showing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowBooleanCallback](#type-remotewindowbooleancallback) | false | — | callback to receive output |

---
## ClassMethod: MultiWindow.hide

### Description
Hides the existing window with the specified name,

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after [RemoteWindow](RemoteWindow.md#class-remotewindow) hidden |

---
## ClassMethod: MultiWindow.find

### Description
Returns window with the specified name, if it exists in the application. Note that, without OpenFin, only windows created with [MultiWindow.open](#classmethod-multiwindowopen) (and the base window) can be found with this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | unique window name |

### Returns

`[RemoteWindow](#type-remotewindow)` — requested window

---
