# MultiDecisionTask Documentation

[← Back to API Index](../reference.md)

---

## Class: MultiDecisionTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
Chooses a next element in a [Process](Process.md#class-process) by evaluating a series of criteria against the [Process.state](Process.md#attr-processstate) and choosing the element associated with the criteria that matched, or a [defaultElement](#attr-multidecisiontaskdefaultelement) if none of the criteria match.

---
## Attr: MultiDecisionTask.decisionList

### Description
List of [DecisionBranchs](../reference.md#object-decisionbranch) to be processed to find the first with matching criteria. The specified [DecisionBranch.targetTask](DecisionBranch.md#attr-decisionbranchtargettask) is then used to identify the the next element.

If no criteria is matched the next element is [MultiDecisionTask.defaultElement](#attr-multidecisiontaskdefaultelement) or the workflow is finished.

When providing a MultiDecisionTask in XML, the `decisionList` is expressed as:

```
     <MultiDecisionTask ID="continentDecision" description="Which continent?" defaultElement="summary">
         <decisionList>
             <decisionBranch targetTask="europeVATTask">
                 <criteria fieldName="order.continent" operator="equals" value="Europe" />
             </decisionBranch>
             ...
         </decisionList>
     <MultiDecisionTask>
 
```

**Flags**: IR

---
## Attr: MultiDecisionTask.defaultElement

### Description
Next element to pick if no criteria match. If this decision is part of a [sequence](Process.md#attr-processsequences) and has a next element in the sequence, the `defaultElement` is assumed to be the next element and does not need to be specified.

**Flags**: IR

---
## Attr: MultiDecisionTask.nextElement

### Description
Not applicable to a MultiDecisionTask.

### See Also

- [MultiDecisionTask.defaultElement](#attr-multidecisiontaskdefaultelement)

**Flags**: IR

---
