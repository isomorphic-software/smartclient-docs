# CriterionValues Documentation

[← Back to API Index](../reference.md)

---

## Attr: CriterionValues.otherValue

### Description
If the operator's [valueType](Operator.md#attr-operatorvaluetype) is "fieldName", then this is the value of the field named by [Criterion.value](Criterion.md#attr-criterionvalue). In the case of date fields, a relative date `otherValue` is converted to an absolute date.

**Flags**: R

---
## Attr: CriterionValues.end

### Description
[Criterion.end](Criterion.md#attr-criterionend). In the case of date fields, a relative date `end` is converted to an absolute date.

**Flags**: R

---
## Attr: CriterionValues.value

### Description
[Criterion.value](Criterion.md#attr-criterionvalue). In the case of date fields, a relative date `value` is converted to an absolute date.

**Flags**: R

---
## Attr: CriterionValues.start

### Description
[Criterion.start](Criterion.md#attr-criterionstart). In the case of date fields, a relative date `start` is converted to an absolute date.

**Flags**: R

---
## Attr: CriterionValues.criterion

### Description
If the operator's [valueType](Operator.md#attr-operatorvaluetype) is "criteria" or "custom", then the [Criterion](../reference_2.md#object-criterion) itself.

**Flags**: R

---
## Attr: CriterionValues.record

### Description
If the operator's [valueType](Operator.md#attr-operatorvaluetype) is "criteria" or "custom", then the record being evaluated.

**Flags**: R

---
