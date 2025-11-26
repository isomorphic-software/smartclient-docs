# AsyncUtil Documentation

[← Back to API Index](../reference.md)

---

## Class: AsyncUtil

### Description
Contains utilities and constants to support asynchronous code.

---
## ClassAttr: AsyncUtil.asyncCanceledMessageGeneric

### Description
A message string to use when displaying an [AsyncOperationResult](../reference.md#object-asyncoperationresult) of [type](AsyncOperationResult.md#attr-asyncoperationresulttype) "canceled" to the user, and no [AsyncOperationResult.cancellationReason](AsyncOperationResult.md#attr-asyncoperationresultcancellationreason) is available.

[AsyncUtil.asyncCanceledMessage](#classattr-asyncutilasynccanceledmessage) is used when a cancellationReason is available.

### Groups

- i18nMessages

### See Also

- [AsyncUtil.getAsyncMessage](#classmethod-asyncutilgetasyncmessage)

**Flags**: RW

---
## ClassAttr: AsyncUtil.asyncCanceledMessage

### Description
A message string to use when displaying an [AsyncOperationResult](../reference.md#object-asyncoperationresult) of [type](AsyncOperationResult.md#attr-asyncoperationresulttype) "canceled" to the user, and a [AsyncOperationResult.cancellationReason](AsyncOperationResult.md#attr-asyncoperationresultcancellationreason) is available.

[AsyncUtil.asyncCanceledMessageGeneric](#classattr-asyncutilasynccanceledmessagegeneric) is used when no cancellationReason is available.

### Groups

- i18nMessages

### See Also

- [AsyncUtil.getAsyncMessage](#classmethod-asyncutilgetasyncmessage)

**Flags**: RW

---
## ClassAttr: AsyncUtil.asyncErrorMessageGeneric

### Description
A message string to use to when displaying an [AsyncOperationResult](../reference.md#object-asyncoperationresult) of [type](AsyncOperationResult.md#attr-asyncoperationresulttype) "error" to the user, and no [AsyncOperationResult.errorMessage](AsyncOperationResult.md#attr-asyncoperationresulterrormessage) is available.

### Groups

- i18nMessages

### See Also

- [AsyncUtil.getAsyncMessage](#classmethod-asyncutilgetasyncmessage)

**Flags**: RW

---
## ClassAttr: AsyncUtil.asyncNonSuccessMessage

### Description
A message string to use when displaying an [AsyncOperationResult](../reference.md#object-asyncoperationresult) to the user, when the provided [type](AsyncOperationResult.md#attr-asyncoperationresulttype) is neither "error" nor "canceled".

### Groups

- i18nMessages

### See Also

- [AsyncUtil.getAsyncMessage](#classmethod-asyncutilgetasyncmessage)
- [AsyncUtil.asyncNonSuccessMessageGeneric](#classattr-asyncutilasyncnonsuccessmessagegeneric)

**Flags**: RW

---
## ClassAttr: AsyncUtil.dataBeingFetchedMessage

### Description
A [disabledMessage](AsyncOperationResult.md#attr-asyncoperationresultdisabledmessage) to use when an operation was disabled because data were being fetched.

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AsyncUtil.asyncDisabledMessageGeneric

### Description
A message string to use when displaying an [AsyncOperationResult](../reference.md#object-asyncoperationresult) of [type](AsyncOperationResult.md#attr-asyncoperationresulttype) "disabled" to the user, and no [AsyncOperationResult.disabledMessage](AsyncOperationResult.md#attr-asyncoperationresultdisabledmessage) is available.

### Groups

- i18nMessages

### See Also

- [AsyncUtil.getAsyncMessage](#classmethod-asyncutilgetasyncmessage)

**Flags**: RW

---
## ClassAttr: AsyncUtil.asyncNonSuccessMessageGeneric

### Description
A message string to use when displaying an [AsyncOperationResult](../reference.md#object-asyncoperationresult) to the user, when the [type](AsyncOperationResult.md#attr-asyncoperationresulttype) is not provided.

### Groups

- i18nMessages

### See Also

- [AsyncUtil.getAsyncMessage](#classmethod-asyncutilgetasyncmessage)
- [AsyncUtil.asyncNonSuccessMessage](#classattr-asyncutilasyncnonsuccessmessage)

**Flags**: RW

---
## ClassAttr: AsyncUtil.missingRequiredParameterErrorMessage

### Description
An error message displayed when a required parameter to an API routine was not specified.

### Groups

- i18nMessages

**Flags**: RW

---
## ClassMethod: AsyncUtil.getAsyncMessage

### Description
Returns a user-displayable message for the given [AsyncOperationResult](../reference.md#object-asyncoperationresult) if its [type](AsyncOperationResult.md#attr-asyncoperationresulttype) is not "success".

[isc.getAsyncMessage()](isc.md#staticmethod-iscgetasyncmessage) and [AsyncUtil.getAsyncMessage()](#classmethod-asyncutilgetasyncmessage) are equivalent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [AsyncOperationResult](#type-asyncoperationresult) | false | — | the `AsyncOperationResult`. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — If the [type](AsyncOperationResult.md#attr-asyncoperationresulttype) is "success", then `null`; otherwise, a user-displayable message describing the non-successful result.

### See Also

- [AsyncUtil.asyncErrorMessageGeneric](#classattr-asyncutilasyncerrormessagegeneric)
- [AsyncUtil.asyncCanceledMessage](#classattr-asyncutilasynccanceledmessage)
- [AsyncUtil.asyncCanceledMessageGeneric](#classattr-asyncutilasynccanceledmessagegeneric)
- [AsyncUtil.asyncDisabledMessageGeneric](#classattr-asyncutilasyncdisabledmessagegeneric)
- [AsyncUtil.asyncNonSuccessMessage](#classattr-asyncutilasyncnonsuccessmessage)
- [AsyncUtil.asyncNonSuccessMessageGeneric](#classattr-asyncutilasyncnonsuccessmessagegeneric)

---
