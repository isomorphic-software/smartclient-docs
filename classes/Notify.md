# Notify Documentation

[← Back to API Index](../main.md)

---

## Class: Notify

### Description
Notify provides a means to display on-screen messages that are automatically dismissed after a configurable amount of time, as an alternative to [modal notification](isc.md#staticmethod-iscconfirm) dialogs that can lower end user productivity. Messages may be shown at a particular location, specified either with viewport-relative coordinates, or as an edge or center location relative to the viewport or a canvas. Messages can be configured to appear and disappear instantly, by sliding into (or out of) view, or by fading in (or out).

One or more [actions](../main.md#object-notifyaction) can be provided when [addMessage()](#classmethod-notifyaddmessage) is called to display a message. They will be rendered as links on which to click to execute the action.

The behavior and appearance of messages are configured per [NotifyType](../main_2.md#type-notifytype), which is simply a string that identifies that message group, similar to [log category](Class.md#method-classlogwarn). By calling [configureMessages()](#classmethod-notifyconfiguremessages) with the `NotifyType`, it can be assigned a [NotifySettings](../main.md#object-notifysettings) configuration to control message animation, placement, and the the [Label](Label.md#class-label) used to render each message, allowing styling and autofit behavior to be configured.

Messages of the same `NotifyType` may be stacked to provide a visible history, with a configurable stacking direction and maximum stacking depth. Details on how to configure messages are provided in the documentation for [NotifySettings](../main.md#object-notifysettings).

Messages for different `NotifyType`s are stacked separately and animated by independent Framework pipelines. It's up to you to configure the placement of supported `NotifyType`s in your app so that they don't overlap, as the Framework doesn't manage it. For example, separate `NotifyType`s could be assigned separate screen edges, or assigned a different [NotifySettings.positionCanvas](NotifySettings.md#attr-notifysettingspositioncanvas).

To dismiss a message manually before its scheduled duration expires, you may call [dismissMessage()](#classmethod-notifydismissmessage) with a `NotifyType` (to dismiss all such messages) or an ID previously returned by [addMessage()](#classmethod-notifyaddmessage) (to dismiss that single message).

**Warnings and Errors**

Each notification may be assigned a [messagePriority](NotifySettings.md#attr-notifysettingsmessagepriority) in the settings passed to [addMessage()](#classmethod-notifyaddmessage). By default, all `NotifyType`s are configured to have priority [Notify.MESSAGE](#classattr-notifymessage), except for "error" and "warn" `NotifyType`s, which are configured with priority [Notify.ERROR](#classattr-notifyerror) and [Notify.WARN](#classattr-notifywarn), respectively.

The [messagePriority](NotifySettings.md#attr-notifysettingsmessagepriority) determines the default styling of a message, and which message to remove if a new message is sent while the message stack is already at its limit. We recommended applying a [messagePriority](NotifySettings.md#attr-notifysettingsmessagepriority) as the best approach for showing pre-styled warnings and errors, since that allows you to interleave them with ordinary messages in a single `NotifyType`.

Alternatively, you can display pre-styled warnings and errors by calling [addMessage()](#classmethod-notifyaddmessage) with the separate `NotifyType`s "warning" and "error", respectively, but then you must take care to [assign each NotifyType](#classmethod-notifyconfiguremessages) used to a separate screen location to avoid one rendering on top of the other.

**Viewport Considerations**

Messages are edge or corner-aligned based on the [viewport width](Page.md#classmethod-pagegetscrollwidth) and [viewport height](Page.md#classmethod-pagegetscrollheight) of the current page rather than screen, so you may need to scroll to see the targeted corner or edge. Note that widgets placed offscreen below or to the right of a page may cause the browser to report a larger viewport, and prevent messages from being visible, even if no scrollbars are present. If you need to stage widgets offscreen for measurement or other reasons, place them above or to the left.

**Modal Windows and Click Masks**

Messages are always shown above all other widgets, including [modal windows](Window.md#attr-windowismodal) and [click masks](Canvas.md#method-canvasshowclickmask). This is because it's expected that messages are "out of band" and logically indepedent of the widget hierarchy being shown. We apply this layering policy even for windows and widgets created by [NotifyAction](../main.md#object-notifyaction)s. If there may a scenario where a message can block a window created by an action, set [NotifySettings.canDismiss](NotifySettings.md#attr-notifysettingscandismiss) to true so that an unobstructed view of the underlying widgets can be restored.

In the linked sample, note how we take care to reuse the existing modal window, if any, if the "Launch..." link is clicked, so that repeated clicks never stack windows over each other.

### See Also

- [isc.say](isc.md#staticmethod-iscsay)
- [isc.confirm](isc.md#staticmethod-iscconfirm)

---
## ClassAttr: Notify.MESSAGE

### Description
Third-highest priority. Default priority for all [NotifyType](../main_2.md#type-notifytype)s other than "error" and "warn".

### See Also

- [Notify.ERROR](#classattr-notifyerror)
- [Notify.WARN](#classattr-notifywarn)

**Flags**: R

---
## ClassAttr: Notify.WARN

### Description
Second-highest priority. Default priority of [NotifyType](../main_2.md#type-notifytype): "warn".

### See Also

- [Notify.ERROR](#classattr-notifyerror)
- [Notify.MESSAGE](#classattr-notifymessage)

**Flags**: R

---
## ClassAttr: Notify.ERROR

### Description
Highest priority. Default priority of [NotifyType](../main_2.md#type-notifytype): "error".

### See Also

- [Notify.WARN](#classattr-notifywarn)
- [Notify.MESSAGE](#classattr-notifymessage)

**Flags**: R

---
## ClassMethod: Notify.addMessage

### Description
Displays a new message, subject to the [stored configuration](#classmethod-notifyconfiguremessages) for the passed `notifyType`, overridden by any passed `settings`. Returns an opaque `MessageID` that can be passed to [Notify.dismissMessage](#classmethod-notifydismissmessage) to clear it.

Note that an empty string may be passed for `contents` if `actions` have been provided, so you may have the message consist only of your specified actions.

Most users should do all configuration up front via a call to [Notify.configureMessages](#classmethod-notifyconfiguremessages). The `settings` argument in this method is provided to allow adjustment of properties that affect only one message, such as [autoFitWidth](NotifySettings.md#attr-notifysettingsautofitwidth), [styleName](NotifySettings.md#attr-notifysettingsstylename), or [labelProperties](NotifySettings.md#attr-notifysettingslabelproperties). Making changes to [stacking](../main_2.md#type-multimessagemode)-related properties via this argument isn't supported, unless specifically documented on the property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| contents | [HTMLString](../main.md#type-htmlstring) | false | — | message to be displayed |
| actions | [Array of NotifyAction](#type-array-of-notifyaction) | true | — | actions (if any) for this message |
| notifyType | [NotifyType](../main_2.md#type-notifytype) | true | — | category of message; default "message" |
| settings | [NotifySettings](#type-notifysettings) | true | — | display and behavior settings for this message that override the [configured](#classmethod-notifyconfiguremessages) settings for the `notifyType` |

### Returns

`[MessageID](#type-messageid)` — opaque identifier for message

### See Also

- [isc.say](isc.md#staticmethod-iscsay)
- [isc.confirm](isc.md#staticmethod-iscconfirm)
- [isc.notify](isc.md#staticmethod-iscnotify)

---
## ClassMethod: Notify.setMessageContents

### Description
Updates the contents of the message from what was passed originally to [Notify.addMessage](#classmethod-notifyaddmessage), while preserving any existing [actions](../main.md#object-notifyaction).

The purpose of this method is to support messages that contain timer countdowns or other data that perhaps need refreshing during display. If you find yourself replacing the entire content with something new, you should probably just add it as a new message.

Note that this method has minimal animation support. The change in message content and corresponding resizing are instant, but the repositioning of the message or stack (if stacked) to keep your requested [alignment](NotifySettings.md#attr-notifysettingsposition) is controlled by [NotifySettings.repositionMethod](NotifySettings.md#attr-notifysettingsrepositionmethod), allowing slide animation. However, that setting is ignored and the repositioning is instant if you've chosen [viewport alignment](NotifySettings.md#attr-notifysettingspositioncanvas) to a border or corner along the [bottom or right](NotifySettings.md#attr-notifysettingsposition) viewport edge, or if an animation is already in progress, in which case the instant repositioning will happen after it completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messageID | [MessageID](#type-messageid) | false | — | message identifier from [Notify.addMessage](#classmethod-notifyaddmessage) |
| contents | [HTMLString](../main.md#type-htmlstring) | false | — | updated message |

**Flags**: A

---
## ClassMethod: Notify.configureMessages

### Description
Sets the default [NotifySettings](../main.md#object-notifysettings) for the specified [NotifyType](../main_2.md#type-notifytype). This may be overridden by passing settings to [Notify.addMessage](#classmethod-notifyaddmessage) when the message is shown, but changing [stacking](../main_2.md#type-multimessagemode)-related properties via [Notify.addMessage](#classmethod-notifyaddmessage) isn't supported,

By default, the [NotifyType](../main_2.md#type-notifytype)s "message", "warn", and "error" are predefined, each with their own [NotifySettings](../main.md#object-notifysettings) with different [styleName](NotifySettings.md#attr-notifysettingsstylename)s. When configuring a new (non-predefined) NotifyType with this method, any [NotifySettings](../main.md#object-notifysettings) left unset will default to those for NotifyType "message".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| notifyType | [NotifyType](../main_2.md#type-notifytype) | false | — | category of message; null defaults to "message" |
| settings | [NotifySettings](#type-notifysettings) | false | — | settings to store for the `notifyType` |

### See Also

- [Notify.configureDefaultSettings](#classmethod-notifyconfiguredefaultsettings)

---
## ClassMethod: Notify.setMessageActions

### Description
Updates the actions of the message from those, if any, passed originally to [Notify.addMessage](#classmethod-notifyaddmessage), while preserving any existing [contents](#classmethod-notifyaddmessage).

See [Notify.setMessageContents](#classmethod-notifysetmessagecontents) for further guidance and animation details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messageID | [MessageID](#type-messageid) | false | — | message identifier from [Notify.addMessage](#classmethod-notifyaddmessage) |
| actions | [Array of NotifyAction](#type-array-of-notifyaction) | false | — | updated actions for this message |

---
## ClassMethod: Notify.canDismissMessage

### Description
Can the message corresponding to the `messageID` be dismissed? Returns false if the message is no longer being shown. The `messageID` must have been previously returned by [Notify.addMessage](#classmethod-notifyaddmessage).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messageID | [MessageID](#type-messageid) | false | — | message identifier to dismiss |

### Returns

`[boolean](../main.md#type-boolean)` — whether message can be dismissed

### See Also

- [Notify.dismissMessage](#classmethod-notifydismissmessage)

---
## ClassMethod: Notify.configureDefaultSettings

### Description
Changes the default settings that are applied when you create a new [NotifyType](../main_2.md#type-notifytype) with [Notify.configureMessages](#classmethod-notifyconfiguremessages). If you want to change the defaults for the built-in NotifyTypes "message", "warn", and "error", with this method, it must be called before the first call to [Notify.configureMessages](#classmethod-notifyconfiguremessages) or [Notify.addMessage](#classmethod-notifyaddmessage). Once a NotifyType has been created, you must use [Notify.configureMessages](#classmethod-notifyconfiguremessages) to change its settings.

Note that for defaults that depend on priority (and thus differ between the built-in NotifyTypes), this method only sets the defaults for the "message" NotifyType.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [NotifySettings](#type-notifysettings) | false | — | changes to NotifyType defaults |

### See Also

- [Notify.configureMessages](#classmethod-notifyconfiguremessages)

---
## ClassMethod: Notify.dismissMessage

### Description
Dismisses one or more messages currently being shown, subject to the existing settings for their [NotifyType](../main_2.md#type-notifytype). You may either pass the opaque message identifier returned from the call to [Notify.addMessage](#classmethod-notifyaddmessage) to dismiss a single message, or a `NotifyType` to dismiss all such messages.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messageID | [MessageID](#type-messageid)|[NotifyType](../main_2.md#type-notifytype) | false | — | message identifier or category to dismiss |

### See Also

- [NotifySettings.duration](NotifySettings.md#attr-notifysettingsduration)
- [NotifyAction.wholeMessage](../main.md#attr-notifyactionwholemessage)

---
## ClassMethod: Notify.messageHasActions

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messageID | [MessageID](#type-messageid) | false | — | message identifier to check |

### Returns

`[boolean](../main.md#type-boolean)` — whether message has any actions

### See Also

- [Notify.addMessage](#classmethod-notifyaddmessage)
- [Notify.setMessageActions](#classmethod-notifysetmessageactions)

---
