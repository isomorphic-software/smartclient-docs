# AsyncOperationResult Documentation

[← Back to API Index](../reference.md)

---

## Attr: AsyncOperationResult.cancellationReason

### Description
If this is a "canceled"-[AsyncOperationResult.type](#attr-asyncoperationresulttype) result, an optional statement to be displayed to the user of the reason for cancellation.

### See Also

- [CancellationController.cancel](CancellationController.md#method-cancellationcontrollercancel)

**Flags**: IR

---
## Attr: AsyncOperationResult.errorMessage

### Description
If this is an "error"-[AsyncOperationResult.type](#attr-asyncoperationresulttype) result, an optional statement to be displayed to the user of the error that occurred.

**Flags**: IR

---
## Attr: AsyncOperationResult.disabledMessage

### Description
If this is a "disabled"-[AsyncOperationResult.type](#attr-asyncoperationresulttype) result, an optional statement to be displayed to the user that the operation was disabled. This may include information about the reason why the operation was disabled.

It is recommended to use the past tense, because this message may continue to be displayed to the user when the conditions for the operation being disabled are no longer the case.

**Flags**: IR

---
## Attr: AsyncOperationResult.type

### Description
The result type.

`null` is interpreted as a non-successful result type.

**Flags**: IR

---
