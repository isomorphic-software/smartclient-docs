# DecisionGateway Documentation

[← Back to API Index](../reference.md)

---

## Class: DecisionGateway

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Chooses a next element in a [Process](Process.md#class-process) by evaluating a series of criteria against the [Process.state](Process.md#attr-processstate) and choosing the element associated with the criteria that matched, or a [defaultElement](#attr-decisiongatewaydefaultelement) if none of the criteria match.

---
## Attr: DecisionGateway.nextElement

### Description
Not applicable to a DecisionGateway.

### See Also

- [DecisionGateway.defaultElement](#attr-decisiongatewaydefaultelement)

**Flags**: IR

---
## Attr: DecisionGateway.decisionList

### Description
List of [TaskDecisions](../reference_2.md#object-taskdecision) to be processed to find the first with matching criteria. The specified [TaskDecision.targetTask](TaskDecision.md#attr-taskdecisiontargettask) is then used to identify the the next element.

If no criteria is matched the next element is [DecisionGateway.defaultElement](#attr-decisiongatewaydefaultelement) or the workflow is finished.

When providing a DecisionGateway in XML, the `decisionList` is expressed as:

```
     <DecisionGateway ID="continentDecision" description="Which continent?" defaultElement="summary">
         <decisionList>
             <taskDecision targetTask="europeVATTask">
                 <criteria fieldName="order.continent" operator="equals" value="Europe" />
             </taskDecision>
             ...
         </decisionList>
     <DecisionGateway>
 
```

**Flags**: IR

---
## Attr: DecisionGateway.defaultElement

### Description
Next element to pick if no criteria match. If this gateway is part of a [sequence](Process.md#attr-processsequences) and has a next element in the sequence, the `defaultElement` is assumed to be the next element and does not need to be specified.

**Flags**: IR

---
## Attr: DecisionGateway.criteriaMap

### Description
A Map from [ProcessElement.ID](ProcessElement.md#attr-processelementid) to Criteria that will cause this ProcessElement to be chosen as the next element if the criteria matches.

If no criteria is matched the next element is [DecisionGateway.defaultElement](#attr-decisiongatewaydefaultelement) or the workflow is finished.

Data values in this criteria prefixed with "$" will be treated as dynamic expressions as detailed in [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

Note that dynamic expressions starting with "$input" are not applicable for an DecisionGateway but "$inputRecord" can be used for direct reference to [Process.state](Process.md#attr-processstate).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

**Deprecated**

**Flags**: IR

---
