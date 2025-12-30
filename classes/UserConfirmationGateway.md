# UserConfirmationGateway Documentation

[← Back to API Index](../reference.md)

---

## Class: UserConfirmationGateway

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Chooses one or another next process element based on confirmation of a message shown to user.

If the user clicks OK, the [nextElement](XORGateway.md#attr-xorgatewaynextelement) is chosen, otherwise the choice is [failureElement](XORGateway.md#attr-xorgatewayfailureelement).

---
## Attr: UserConfirmationGateway.failureElement

### Description
ID of the next sequence or element to proceed to if the criteria do not match.

**Flags**: IR

---
## Attr: UserConfirmationGateway.textFormula

### Description
Formula to be used to calculate the message contents. Use [UserConfirmationGateway.message](#attr-userconfirmationgatewaymessage) property to assign a static message instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: UserConfirmationGateway.nextElement

### Description
Next [sequence](Process.md#attr-processsequences) or [element](Process.md#attr-processelements) to execute if the criteria match the process state.

`nextElement` does not need to be specified if this gateway is part of a [sequence](Process.md#attr-processsequences) and has a next element in the sequence.

Note that if there is both a `sequence` and a normal `element` with the same name in the current `Process`, the `sequence` will be used.

**Flags**: IR

---
## Attr: UserConfirmationGateway.message

### Description
Message to display to the user for confirmation. To display a dynamic message see [UserConfirmationGateway.textFormula](#attr-userconfirmationgatewaytextformula).

**Flags**: IR

---
