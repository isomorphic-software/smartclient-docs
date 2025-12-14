# SendEmailTask Documentation

[← Back to API Index](../reference.md)

---

## Class: SendEmailTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Sends an email using the [reifyMessaging](../kb_topics/reifyMessaging.md#kb-topic-reify-messaging) `isc_sendEmail` DataSource. Refer to [Mail overview](Mail.md#class-mail) to know how to set up access to an SMTP server.

There is a matching Reify Workflow Editor task editor, [SendEmailTaskEditor](#class-sendemailtaskeditor), that can be enabled by [Reify.enableSendEmailTaskEditor](#attr-reifyenablesendemailtaskeditor).

If [mock mode](Process.md#attr-processmockmode) is enabled, instead of sending an email a [notification message](#attr-sendemailtaskmockmodenotifymessage) is shown instead.

---
## Attr: SendEmailTask.mockModeNotifyMessage

### Description
Message displayed by [Notify](Notify.md#class-notify) in lieu of sending an actual email when the workflow is in [mock mode](Process.md#attr-processmockmode).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

The following dynamic variables are available:

*   to
*   subject
*   message

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SendEmailTask.subject

### Description
Email subject. To assign a dynamic subject see [SendEmailTask.subjectFormula](#attr-sendemailtasksubjectformula).

**Flags**: IR

---
## Attr: SendEmailTask.subjectFormula

### Description
Formula to be used to calculate the subject contents. Use [SendEmailTask.subject](#attr-sendemailtasksubject) property to assign a static subject instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: SendEmailTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises from operation.

**Flags**: IR

---
## Attr: SendEmailTask.to

### Description
Email recipient address(es) separated by commas.

**Flags**: IR

---
## Attr: SendEmailTask.requestProperties

### Description
Additional properties to set on the DSRequest that will be issued to perform send.

Note that `operationId` will always be set `email` and `willHandleError` will always be set `true`.

**Flags**: IR

---
## Attr: SendEmailTask.message

### Description
Message to be sent to recipients.

**Flags**: IR

---
