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
## Attr: Criterion.fieldName

### Description
Name of the field in each [Record](../reference.md#object-record) that this criterion applies to. Not applicable for a criterion with [sub-criteria](#attr-criterioncriteria). Can be specified as a dataPath to allow matching nested objects. Use '/' as delimiters for dataPath. See [dataPath](../reference_2.md#type-datapath) for more information.

#### [fieldQuery](#attr-criterionfieldquery) shortcuts
`fieldName` can also be used to express a compact form of related-field filtering. If you set this property to the qualified name of a field on a related DataSource, it will be transformed into a basic [AdvancedCriterionSubquery](../reference.md#object-advancedcriterionsubquery). For example, say you have an `Order` dataSource, which has a [foreign key relation](DataSourceField.md#attr-datasourcefieldforeignkey) to your `Customer` dataSource, and your `Customer` dataSource has a "region" field. If you wanted to fetch all Orders for Customers in the EMEA region, you could declare criteria like this:
```
    {fieldName: "Customer.region", operator: "equals", value: "EMEA"}
 
```
This would be transformed into a subquery filter that would select only the records you want:
```
 {
      fieldQuery: {
          dataSource: "Customer",
          queryOutput: "region"
      }, operator: "equals", value: "EMEA"
 }
 
```
This transformation takes place before the filtering subsystem even sees the criteria, so declaring the shortcut form via `fieldName` leads to **exactly** the same filtering behavior as if you specified the subquery directly as a `fieldQuery`

See the `AdvancedCriterionSubquery` overview linked above for more details of the extremely powerful subquery filtering options.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.valueQuery

### Description
A subquery to use instead of a [Criterion.value](#attr-criterionvalue). When you use a `valueQuery` instead of a `value`, you are comparing the values in the record field named in the criterion [Criterion.fieldName](#attr-criterionfieldname) to the result of running a per-record subquery, rather than a literal scalar value. . Note, it is also possible to specify both a `valueQuery` and a [fieldQuery](#attr-criterionfieldquery).

See the [subquery overview](../reference.md#object-advancedcriterionsubquery) for more details of the criteria subquery feature, and examples of use.

Note, if you specify both `valueQuery` and `value` in a criterion, we use the `value` and the `valueQuery` is ignored

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Criterion.fieldQuery

### Description
A subquery to use instead of a [Criterion.fieldName](#attr-criterionfieldname). When you use a `fieldQuery` instead of a `fieldName`, you are comparing the criterion [Criterion.value](#attr-criterionvalue) to the result of running a per-record subquery, rather than a field value found directly on the record. Note, it is also possible to specify both a `fieldQuery` and a [valueQuery](#attr-criterionvaluequery).

See the [subquery overview](../reference.md#object-advancedcriterionsubquery) for more details of the criteria subquery feature, and examples of use.

Note, if you specify both `fieldQuery` and `fieldName` in a criterion, we use the `fieldName` and the `fieldQuery` is ignored.

Note also that `fieldName` supports a special shortcut syntax for declaring a `fieldQuery` as a simple qualified reference to a related field. See the `fieldName` doc linked above for details

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

Value may be required or not required, or may be an Array, according to the [OperatorValueType](../reference_2.md#type-operatorvaluetype) of the operator.

### Groups

- advancedFilter

**Flags**: IR

---
