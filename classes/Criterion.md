# Criterion Documentation

[← Back to API Index](../reference.md)

---

## Attr: Criterion.operator

### Description
Operator this criterion applies.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.valuePath

### Description
Wherever [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) are supported, `valuePath` can be specified as a path in the current [Canvas.ruleScope](Canvas.md#attr-canvasrulescope) as an alternative to setting a fixed [Criterion.value](#attr-criterionvalue).

Note: `valuePath` vs setting a path for [Criterion.fieldName](#attr-criterionfieldname):

*   use a path for `criterion.fieldName` when criteria will be matched against a nested data structure.
*   use `criterion.valuePath` when the values used in filtering should be dynamically derived based on the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope). This does not imply that the criteria will be matched against a nested structure.

**Flags**: IR

---
## Attr: Criterion.end

### Description
End value of a criterion with an operator of type `"valueRange"`.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.start

### Description
Start value of a criterion with an operator of type `"valueRange"`.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.fieldName

### Description
Name of the field in each [Record](../reference.md#object-record) that this criterion applies to. Not applicable for a criterion with [sub-criteria](#attr-criterioncriteria). Can be specified as a dataPath to allow matching nested objects. Use '/' as delimiters for dataPath. See [dataPath](../reference.md#type-datapath) for more information.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.criteria

### Description
For a criterion with an operator that acts on other criteria (eg "and", "or"), a list of sub-criteria that are grouped together by the operator.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.value

### Description
Value to be used in the application of this criterion.

Value may be required or not required, or may be an Array, according to the [OperatorValueType](../reference.md#type-operatorvaluetype) of the operator.

### Groups

- advancedFilter

**Flags**: IR

---
