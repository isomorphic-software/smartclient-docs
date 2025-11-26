# CancellationController Documentation

[← Back to API Index](../reference.md)

---

## Class: CancellationController

### Description
Provides a mechanism for canceling asynchronous operations.

---
## ClassAttr: CancellationController.componentFieldsWereChangedReason

### Description
Cancellation reason string that is used when the set of fields for a [DataBoundComponent](../reference.md#interface-databoundcomponent) are changed while an asynchronous operation that depends on the component's old set of fields was in progress.

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: CancellationController.ancestorCanceledReason

### Description
Cancellation reason that is used when a `CancellationController` created by [CancellationController.createSubController](#method-cancellationcontrollercreatesubcontroller) is canceled by its parent, grandparent, great-grandparent, etc. `CancellationController` being canceled, and a reason for the ancestor `CancellationController` being canceled is provided.  
For example: "The great-grandparent operation was canceled: The user requested cancellation."

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: CancellationController.componentDataSourceWasChangedReason

### Description
Cancellation reason string that is used when the [dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource) for a [DataBoundComponent](../reference.md#interface-databoundcomponent) is changed while an asynchronous operation that depends on the component's old `dataSource` was in progress.

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: CancellationController.ancestorCanceledReasonGeneric

### Description
Cancellation reason that is used when a `CancellationController` created by [CancellationController.createSubController](#method-cancellationcontrollercreatesubcontroller) is canceled by its parent, grandparent, great-grandparent, etc. `CancellationController` being canceled, and no specific reason was provided for why the ancestor `CancellationController` was canceled.  
For example: "The great-grandparent operation was canceled."

### Groups

- i18nMessages

**Flags**: RW

---
## Attr: CancellationController.canceled

### Description
Whether [CancellationController.cancel](#method-cancellationcontrollercancel) has been called.

**Flags**: R

---
## Attr: CancellationController.cancellationReason

### Description
The reason, if any, passed to the first call to [CancellationController.cancel](#method-cancellationcontrollercancel).

**Flags**: R

---
## Method: CancellationController.createSubController

### Description
Creates a new [CancellationController](#class-cancellationcontroller) which is canceled whenever this `CancellationController` is canceled.

Note that the sub-`CancellationController` may be independently canceled before this parent `CancellationController` is canceled.

### Returns

`[CancellationController](#type-cancellationcontroller)` — a new [CancellationController](#class-cancellationcontroller) that is canceled whenever this `CancellationController` is canceled.

---
## Method: CancellationController.cancel

### Description
Requests cancellation of all asynchronous operations that are polling [CancellationController.canceled](#attr-cancellationcontrollercanceled) or [observing](Class.md#method-classobserve) this method. Also cancels any [sub-`CancellationController`](#method-cancellationcontrollercreatesubcontroller)s of this `CancellationController` that are not already canceled.

[this.cancellationReason](#attr-cancellationcontrollercancellationreason) is set to the provided `reason` only on the first call to cancel().

For observers of this method, the recommended practice is to capture the `returnVal` and only perform the cancellation steps if the `returnVal` was `true`. This is because it could happen that cancel() is called a second time before the observers finish.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [HTMLString](../reference.md#type-htmlstring) | true | — | A reason for cancellation. |

### Returns

`[Boolean](#type-boolean)` — `true` if this was the first call to cancel(); `false` otherwise.

---
