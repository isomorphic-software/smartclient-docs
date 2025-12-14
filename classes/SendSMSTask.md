# SendSMSTask Documentation

[← Back to API Index](../reference.md)

---

## Class: SendSMSTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Sends an SMS message using the [reifyMessaging](../kb_topics/reifyMessaging.md#kb-topic-reify-messaging) `isc_sendSMS` DataSource.

There is a matching Reify Workflow Editor task editor, [SendSMSTaskEditor](#class-sendsmstaskeditor), that can be enabled by [Reify.enableSendSMSTaskEditor](#attr-reifyenablesendsmstaskeditor).

If [mock mode](Process.md#attr-processmockmode) is enabled, instead of sending an SMS message a [notification message](#attr-sendsmstaskmockmodenotifymessage) is shown instead.

---
## Attr: SendSMSTask.requestProperties

### Description
Additional properties to set on the DSRequest that will be issued to perform send.

Note that `operationId` will always be set `sms` and `willHandleError` will always be set `true`.

**Flags**: IR

---
## Attr: SendSMSTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises from operation.

**Flags**: IR

---
## Attr: SendSMSTask.mockModeNotifyMessage

### Description
Message displayed by [Notify](Notify.md#class-notify) in lieu of sending an actual email when the workflow is in [mock mode](Process.md#attr-processmockmode).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

The following dynamic variables are available:

*   to
*   message

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SendSMSTask.message

### Description
Message to be sent to recipients.

**Flags**: IR

---
## Attr: SendSMSTask.to

### Description
SMS recipient phone number(s) separated by commas.

**Flags**: IR

---
