# XORGateway Documentation

[← Back to API Index](../reference.md)

---

## Class: XORGateway

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Chooses one or another next process element based on AdvancedCriteria applied to [Process.state](Process.md#attr-processstate).

If the AdvancedCriteria evaluate to true, the [nextElement](#attr-xorgatewaynextelement) is chosen, otherwise the [failureElement](#attr-xorgatewayfailureelement).

Note that "XOR" in `XORGateway` means "exclusive or" - only one next element is chosen.

---
## Attr: XORGateway.failureElement

### Description
ID of the next sequence or element to proceed to if the criteria do not match.

**Flags**: IR

---
## Attr: XORGateway.nextElement

### Description
Next [sequence](Process.md#attr-processsequences) or [element](Process.md#attr-processelements) to execute if the criteria match the process state.

`nextElement` does not need to be specified if this gateway is part of a [sequence](Process.md#attr-processsequences) and has a next element in the sequence.

Note that if there is both a `sequence` and a normal `element` with the same name in the current `Process`, the `sequence` will be used.

**Flags**: IR

---
## Attr: XORGateway.criteria

### Description
Simple or [AdvancedCriteria](../reference.md#object-advancedcriteria) to be applied against the [Process.state](Process.md#attr-processstate).

Data values in this criteria prefixed with "$" will be treated as dynamic expressions as detailed in [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

Note that dynamic expressions starting with "$input" are not applicable for an XORGateway but "$inputRecord" can be used for direct reference to [Process.state](Process.md#attr-processstate).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

**Flags**: IR

---
