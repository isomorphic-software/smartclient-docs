# NotifySettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: NotifySettings.maxStackDismissMode

### Description
Specifies how to pick which message to dismiss when the [NotifySettings.maxStackSize](#attr-notifysettingsmaxstacksize) is reached, and the lowest priority value (highest numerical [messagePriority](#attr-notifysettingsmessagepriority)) is shared by more than one message.

We can simply dismiss the oldest message of that [messagePriority](#attr-notifysettingsmessagepriority), or we can pick the message with the least time left until it's auto-dismissed.

### See Also

- [NotifySettings.duration](#attr-notifysettingsduration)
- [Notify.dismissMessage](Notify.md#classmethod-notifydismissmessage)

**Flags**: IR

---
## Attr: NotifySettings.slideSpeed

### Description
Animation speed for [NotifyTransition](../reference.md#type-notifytransition): "slide", in pixels/second.

**Flags**: IR

---
## Attr: NotifySettings.multiMessageMode

### Description
Determines what happens if a message appears while there's still another one of the same [NotifyType](../reference_2.md#type-notifytype) being shown. Such messages are either stacked or replace one another,

**Flags**: IR

---
## Attr: NotifySettings.slideInOrigin

### Description
Determines where messages originate when they appear for [NotifySettings.appearMethod](#attr-notifysettingsappearmethod): "slide". Possible values are "L", "R", "T", and "B".

If not specified, the edge nearest the message's requested coordinates or position is used.

**Flags**: IR

---
## Attr: NotifySettings.labelProperties

### Description
Configures the properties, such as [Label.autoFit](Label.md#attr-labelautofit), [Label.align](Label.md#attr-labelalign), and [Label.width](Label.md#attr-labelwidth). of the [Label](Label.md#class-label) autochildren that will be used to draw messages, where not already determined by message layout or other `NotifySettings` properties such as [NotifySettings.styleName](#attr-notifysettingsstylename).

Not all label properties are guaranteed to work here, as the Notify system is assumed to layout message content and manage positioning messages. In particular, the following properties should be avoided:

| Property Name | Issue | Guidance |
|---|---|---|
| margin | Layout and positioning of the messages is handled by the Notify system. | Use [NotifySettings.stackSpacing](#attr-notifysettingsstackspacing) to configure the separation between messages, and [NotifySettings.leftOffset](#attr-notifysettingsleftoffset) and [NotifySettings.topOffset](#attr-notifysettingstopoffset) to fine-tine stack [positioning](#attr-notifysettingsposition). |
| padding | Padding is set by notification CSS so that children are positioned corrected relative to content. | You can apply your own [styling](#attr-notifysettingsstylename) to messages via CSS. Or you can use HTML as the message contents to create whatever sort of interior layout you like. |
| wrap | Autowrap behavior is managed by the Notify system. | To have [autofitted](#attr-notifysettingsautofitwidth) content not wrap, set [NotifySettings.autoFitMaxWidth](#attr-notifysettingsautofitmaxwidth) higher than your expected message widths. You can set it to "100%" if needed to allow the message to expand across the entire page. |

**Flags**: IR

---
## Attr: NotifySettings.messagePriority

### Description
Sets the priority of the message. Priority is used to determine which message to dismiss if [NotifySettings.maxStackSize](#attr-notifysettingsmaxstacksize) is hit. Lower numerical values have higher priority.

The default is:

*   [Notify.ERROR](Notify.md#classattr-notifyerror) for [NotifyType](../reference_2.md#type-notifytype): "error",
*   [Notify.WARN](Notify.md#classattr-notifywarn) for [NotifyType](../reference_2.md#type-notifytype): "warn", and
*   [Notify.MESSAGE](Notify.md#classattr-notifymessage) for all other [NotifyType](../reference_2.md#type-notifytype)s

**Impact on Appearance**

If you specify `messagePriority`, and [NotifySettings.applyPriorityToAppearance](#attr-notifysettingsapplyprioritytoappearance) is set, the properties:

*   [NotifySettings.messageIcon](#attr-notifysettingsmessageicon),
*   [NotifySettings.styleName](#attr-notifysettingsstylename), and
*   [NotifySettings.actionStyleName](#attr-notifysettingsactionstylename)

will be assigned, if not specified, to the default values from:

*   [NotifyType](../reference_2.md#type-notifytype): "error" for priority [Notify.ERROR](Notify.md#classattr-notifyerror),
*   [NotifyType](../reference_2.md#type-notifytype): "warn" for priority [Notify.WARN](Notify.md#classattr-notifywarn), or
*   [NotifyType](../reference_2.md#type-notifytype): "message" for priorities at or below [Notify.MESSAGE](Notify.md#classattr-notifymessage) (greater or equal numerically)

This allows you to automatically set "error" or "warn" styling, on a per-message basis, for any non-"error" or "warn" `NotifyType` by simply supplying a `messagePriority` for that message.

### See Also

- [Notify.addMessage](Notify.md#classmethod-notifyaddmessage)
- [NotifySettings.maxStackDismissMode](#attr-notifysettingsmaxstackdismissmode)

**Flags**: IRA

---
## Attr: NotifySettings.positionCanvas

### Description
Canvas over which to position the message, available as an alternative means of placement if viewport-relative [coordinates](#attr-notifysettingsx) aren't provided. Note that the canvas is only used to compute where to the place message, and will not be altered.

### See Also

- [NotifySettings.leftOffset](#attr-notifysettingsleftoffset)
- [NotifySettings.topOffset](#attr-notifysettingstopoffset)
- [NotifySettings.position](#attr-notifysettingsposition)

**Flags**: IR

---
## Attr: NotifySettings.applyPriorityToAppearance

### Description
Whether to default properties affecting the message appearance to those of the built-in [NotifyType](../reference_2.md#type-notifytype) corresponding to the [messagePriority](#attr-notifysettingsmessagepriority). Default is true except for [NotifyType](../reference_2.md#type-notifytype)s "error" and "warn", which default to false.

### See Also

- [NotifySettings.messagePriority](#attr-notifysettingsmessagepriority)

**Flags**: IRA

---
## Attr: NotifySettings.messageIconOrientation

### Description
If an icon is present, should it appear to the left or right of the title? valid options are `"left"` and `"right"`. If unset, default is "left" unless [RTL](Page.md#classmethod-pageisrtl) is active, in which case it's "right".

Note that the icon will automatically be given an alignment matching its orientation, so "left" for `messageIconOrientation` "left", and vice versa.

### See Also

- [Label.iconAlign](Label.md#attr-labeliconalign)
- [Label.iconOrientation](Label.md#attr-labeliconorientation)

**Flags**: IR

---
## Attr: NotifySettings.disappearMethod

### Description
Controls how messages disappear from or leave their requested location. The default of "fade" is recommended because a slide animation would draw too much attention to a notification that is no longer current, whereas a subtle fade should draw a minimum of attention (less even than instantaneously disappearing).

**Flags**: IR

---
## Attr: NotifySettings.fadeOutDuration

### Description
Time over which the fade-out effect runs for [NotifyTransition](../reference.md#type-notifytransition): "fade", in milliseconds.

**Flags**: IR

---
## Attr: NotifySettings.stackDirection

### Description
Determines how messages are stacked if [MultiMessageMode](../reference_2.md#type-multimessagemode) is "stack". For example, "down" means that older messages move down when a new message of the same [NotifyType](../reference_2.md#type-notifytype) appears.

**Flags**: IR

---
## Attr: NotifySettings.position

### Description
Where to show the message, specified as an edge ("T", "B", "R", "L"), a corner ("TL", "TR", "BL", "BR), or "C" for center, similar to [Canvas.snapTo](Canvas.md#attr-canvassnapto). If an edge is specified, the message will be shown at its center (or the very center for "C"). Only used if [coordinates](#attr-notifysettingsx) haven't been provided.

If a [NotifySettings.positionCanvas](#attr-notifysettingspositioncanvas) has been specified, the `position` is interpreted relative to it instead of the viewport, and this property defaults to "C". Otherwise, if no `positionCanvas` is present, the default is to use [NotifySettings.slideInOrigin](#attr-notifysettingsslideinorigin) or [NotifySettings.slideOutOrigin](#attr-notifysettingsslideoutorigin), or "L" if neither property is defined.

To place the message at an offset from the specified position, use [NotifySettings.leftOffset](#attr-notifysettingsleftoffset) or [NotifySettings.topOffset](#attr-notifysettingstopoffset).

### See Also

- [NotifySettings.x](#attr-notifysettingsx)
- [NotifySettings.y](#attr-notifysettingsy)
- [NotifySettings.positionCanvas](#attr-notifysettingspositioncanvas)

**Flags**: IR

---
## Attr: NotifySettings.messageIcon

### Description
Optional icon to be shown in the [Label](Label.md#class-label) drawn for this message. Default is

*   "\[SKIN\]/Notify/error.png" for [NotifyType](../reference_2.md#type-notifytype): "error",
*   "\[SKIN\]/Notify/warning.png" for [NotifyType](../reference_2.md#type-notifytype): "warn", and
*   "\[SKIN\]/Notify/checkmark.png" for all other [NotifyType](../reference_2.md#type-notifytype)s.

However, if you specify a [messagePriority](#attr-notifysettingsmessagepriority), it will determine the default rather than the actual `NotifyType`, if [NotifySettings.applyPriorityToAppearance](#attr-notifysettingsapplyprioritytoappearance) is true.

### See Also

- [NotifySettings.messagePriority](#attr-notifysettingsmessagepriority)

**Flags**: IR

---
## Attr: NotifySettings.topOffset

### Description
Specifies a top offset from the position specified by [NotifySettings.position](#attr-notifysettingsposition) or [NotifySettings.positionCanvas](#attr-notifysettingspositioncanvas) where the message should be shown. Ignored if [coordinates](#attr-notifysettingsy) are provided to position the message.

### See Also

- [NotifySettings.position](#attr-notifysettingsposition)
- [NotifySettings.leftOffset](#attr-notifysettingsleftoffset)

**Flags**: IR

---
## Attr: NotifySettings.stackPersistence

### Description
Controls how older messages' [NotifySettings.duration](#attr-notifysettingsduration) countdowns are affected when a new message of the same [NotifyType](../reference_2.md#type-notifytype) appears. We either continue the countdowns on the older messages as if they are unrelated, or we reset any countdowns that are less than the new message's `duration`.

Note that you can set this property in a call to [Notify.addMessage](Notify.md#classmethod-notifyaddmessage) even though it has "stack" in its name, since it governs the logic run on behalf of this message.

**Flags**: IRA

---
## Attr: NotifySettings.maxStackSize

### Description
Sets a limit on how many messages may be stacked if [MultiMessageMode](../reference_2.md#type-multimessagemode) is "stack". The oldest message of the affected [NotifyType](../reference_2.md#type-notifytype) will be dismissed to enforce this limit.

**Flags**: IR

---
## Attr: NotifySettings.repositionMethod

### Description
Controls how the stack or message is repositioned, if required, after [Notify.setMessageContents](Notify.md#classmethod-notifysetmessagecontents) has been called. Valid values are "slide" and "instant".

**Flags**: IR

---
## Attr: NotifySettings.y

### Description
Where to show the message, as a viewport-relative y coordinate offset to the top edge of the [Label](Label.md#class-label) rendering the message.

### See Also

- [NotifySettings.x](#attr-notifysettingsx)
- [NotifySettings.position](#attr-notifysettingsposition)

**Flags**: IR

---
## Attr: NotifySettings.canDismiss

### Description
Displays an icon to allow a message to be dismissed through the UI. Messages can always be dismissed programmatically by calling [Notify.dismissMessage](Notify.md#classmethod-notifydismissmessage).

**Flags**: IR

---
## Attr: NotifySettings.stackSpacing

### Description
Space between each message when [MultiMessageMode](../reference_2.md#type-multimessagemode) is "stack".

**Flags**: IR

---
## Attr: NotifySettings.duration

### Description
Length of time a message is shown before being auto-dismissed, in milliseconds. A value of 0 means that the message will not be dismissed automatically. Messages can always be dismissed by calling [Notify.dismissMessage](Notify.md#classmethod-notifydismissmessage) or, if [NotifySettings.canDismiss](#attr-notifysettingscandismiss) is set, by performing a "close click".

**Flags**: IR

---
## Attr: NotifySettings.slideOutOrigin

### Description
Determines where messages go when they disappear for [NotifySettings.disappearMethod](#attr-notifysettingsdisappearmethod): "slide". Possible values are "L", "R", "T", and "B".

If not specified, the edge nearest the message's requested coordinates or position is used.

**Flags**: IR

---
## Attr: NotifySettings.messageControlPadding

### Description
Optional specified padding to apply after the message content when showing a [dismiss button](#attr-notifysettingscandismiss) so that the button doesn't occlude any content. Only needed if the message [styling](#attr-notifysettingsstylename) doesn't already provide enough padding.

**Flags**: IR

---
## Attr: NotifySettings.actionSeparator

### Description
HTML to be added before each action to separate it from the previous action. For the first action, it will only be added if the message contents aren't empty.

You may override this on a per action basis using [NotifyAction.separator](../reference.md#attr-notifyactionseparator).

Besides the default, some other known useful values are "&emsp;" and "&nbsp;".

**Flags**: IR

---
## Attr: NotifySettings.x

### Description
Where to show the message, as a viewport-relative x coordinate offset to the left edge of the [Label](Label.md#class-label) rendering the message. Properties [NotifySettings.position](#attr-notifysettingsposition) and [NotifySettings.positionCanvas](#attr-notifysettingspositioncanvas) will only be used to place messages if coordinates aren't provided.

### See Also

- [NotifySettings.y](#attr-notifysettingsy)
- [NotifySettings.position](#attr-notifysettingsposition)

**Flags**: IR

---
## Attr: NotifySettings.messageIconHeight

### Description
Height in pixels of the icon image.

### See Also

- [Label.iconHeight](Label.md#attr-labeliconheight)

**Flags**: IR

---
## Attr: NotifySettings.autoFitMaxWidth

### Description
Maximum auto-fit width for a message if [NotifySettings.autoFitWidth](#attr-notifysettingsautofitwidth) is enabled. May be specified as a pixel value, or a percentage of page width.

### See Also

- [NotifySettings.autoFitWidth](#attr-notifysettingsautofitwidth)

**Flags**: IR

---
## Attr: NotifySettings.styleName

### Description
The CSS class to apply to the [Label](Label.md#class-label) drawn for this message. Default is:

*   "notifyError" for [NotifyType](../reference_2.md#type-notifytype): "error",
*   "notifyWarn" for [NotifyType](../reference_2.md#type-notifytype): "warn", and
*   "notifyMessage" for all other [NotifyType](../reference_2.md#type-notifytype)s.

However, if you specify a [messagePriority](#attr-notifysettingsmessagepriority), it will determine the default rather than the actual `NotifyType`, if [NotifySettings.applyPriorityToAppearance](#attr-notifysettingsapplyprioritytoappearance) is true.

Note that if [RTL](Page.md#classmethod-pageisrtl) is active, the default will be as above, but with an "RTL" suffix added.

### See Also

- [NotifySettings.messagePriority](#attr-notifysettingsmessagepriority)

**Flags**: IR

---
## Attr: NotifySettings.messageIconWidth

### Description
Width in pixels of the icon image.

### See Also

- [Label.iconWidth](Label.md#attr-labeliconwidth)

**Flags**: IR

---
## Attr: NotifySettings.appearMethod

### Description
Controls how messages appear at or reach their requested location. The default of "slide" is recommended because the motion will draw the user's attention to the notification.

**Flags**: IR

---
## Attr: NotifySettings.stayIfHovered

### Description
If true, pauses the auto-dismiss countdown timer when the mouse is over the messasge.

**Flags**: IR

---
## Attr: NotifySettings.fadeInDuration

### Description
Time over which the fade-in effect runs for [NotifyTransition](../reference.md#type-notifytransition): "fade", in milliseconds.

**Flags**: IR

---
## Attr: NotifySettings.actionStyleName

### Description
The CSS class to apply to action text in this message. default is:

*   "notifyErrorActionLink" for [NotifyType](../reference_2.md#type-notifytype): "error",
*   "notifyWarnActionLink" for [NotifyType](../reference_2.md#type-notifytype): "warn", and
*   "notifyMessageActionLink" for all other [NotifyType](../reference_2.md#type-notifytype)s.

However, if you specify a [messagePriority](#attr-notifysettingsmessagepriority), it will determine the default rather than the actual `NotifyType`, if [NotifySettings.applyPriorityToAppearance](#attr-notifysettingsapplyprioritytoappearance) is true.

### See Also

- [NotifySettings.messagePriority](#attr-notifysettingsmessagepriority)

**Flags**: IR

---
## Attr: NotifySettings.leftOffset

### Description
Specifies a left offset from the position specified by [NotifySettings.position](#attr-notifysettingsposition) or [NotifySettings.positionCanvas](#attr-notifysettingspositioncanvas) where the message should be shown. Ignored if [coordinates](#attr-notifysettingsx) are provided to position the message.

### See Also

- [NotifySettings.position](#attr-notifysettingsposition)
- [NotifySettings.topOffset](#attr-notifysettingstopoffset)

**Flags**: IR

---
## Attr: NotifySettings.messageIconSpacing

### Description
Pixels between icon and title text.

### See Also

- [Label.iconSpacing](Label.md#attr-labeliconspacing)

**Flags**: IR

---
## Attr: NotifySettings.autoFitWidth

### Description
If true, the specified width of the [Label](Label.md#class-label) drawn for this message will be treated as a minimum width. If the message content string exceeds this, the [Label](Label.md#class-label) will expand to accommodate it up to [NotifySettings.autoFitMaxWidth](#attr-notifysettingsautofitmaxwidth) (without the text wrapping).

Using this setting differs from simply disabling wrapping via [wrap:false](Label.md#attr-labelwrap) as the content will wrap if the [NotifySettings.autoFitMaxWidth](#attr-notifysettingsautofitmaxwidth) is exceeded.

**Flags**: IRA

---
