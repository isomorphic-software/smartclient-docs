# DecisionBranch Documentation

[← Back to API Index](../reference.md)

---

## Attr: DecisionBranch.targetTask

### Description
[ProcessElement.ID](ProcessElement.md#attr-processelementid) of element to be used as next element if [criteria](#attr-decisionbranchcriteria) matches.

**Flags**: IR

---
## Attr: DecisionBranch.criteria

### Description
Criteria identifying when the [DecisionBranch.targetTask](#attr-decisionbranchtargettask) should be chosen within a [MultiDecisionTask.decisionList](MultiDecisionTask.md#attr-multidecisiontaskdecisionlist).

Data values in this criteria prefixed with "$" will be treated as dynamic expressions as detailed in [TaskInputExpression](../reference_2.md#type-taskinputexpression). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

Note that dynamic expressions starting with "$input" are not applicable in this context but "$inputRecord" can be used for direct reference to [Process.state](Process.md#attr-processstate).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

**Flags**: IR

---
