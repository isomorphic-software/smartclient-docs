# DecisionGateway Documentation

[← Back to API Index](../reference.md)

---

## Class: DecisionGateway

*Inherits from:* [MultiDecisionTask](MultiDecisionTask.md#class-multidecisiontask)

### Description
Chooses a next element in a [Process](Process.md#class-process) by evaluating a series of criteria against the [Process.state](Process.md#attr-processstate) and choosing the element associated with the criteria that matched, or a [defaultElement](MultiDecisionTask.md#attr-multidecisiontaskdefaultelement) if none of the criteria match.

**Deprecated**

---
## Attr: DecisionGateway.criteriaMap

### Description
A Map from [ProcessElement.ID](ProcessElement.md#attr-processelementid) to Criteria that will cause this ProcessElement to be chosen as the next element if the criteria matches.

If no criteria is matched the next element is [defaultElement](MultiDecisionTask.md#attr-multidecisiontaskdefaultelement) or the workflow is finished.

Data values in this criteria prefixed with "$" will be treated as dynamic expressions as detailed in [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

Note that dynamic expressions starting with "$input" are not applicable for an decisionGateway but "$inputRecord" can be used for direct reference to [Process.state](Process.md#attr-processstate).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

**Deprecated**

**Flags**: IR

---
