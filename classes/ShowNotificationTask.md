# ShowNotificationTask Documentation

[← Back to API Index](../main.md)

---

## Class: ShowNotificationTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Show a message which fades out automatically using [Notify](Notify.md#class-notify).

---
## Attr: ShowNotificationTask.notifyType

### Description
NotifyType for message.

**Flags**: IR

---
## Attr: ShowNotificationTask.textFormula

### Description
Formula to be used to calculate the message contents. Use [ShowNotificationTask.message](#attr-shownotificationtaskmessage) property to assign a static message instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: ShowNotificationTask.message

### Description
Message to display. To display a dynamic message see [ShowNotificationTask.textFormula](#attr-shownotificationtasktextformula).

**Flags**: IR

---
## Attr: ShowNotificationTask.autoDismiss

### Description
Auto-dismiss message after a short duration.

**Flags**: IR

---
## Attr: ShowNotificationTask.position

### Description
Where to show the message, specified as an edge ("T", "B", "R", "L") similar to [Canvas.snapTo](Canvas.md#attr-canvassnapto), or "C" for center. The message will be shown at the center of the edge specified (or the very center for "C").

**Flags**: IR

---
