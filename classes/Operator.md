# Operator Documentation

[← Back to API Index](../reference.md)

---

## Attr: Operator.hidden

### Description
Whether this operator should be offered to users by default in interfaces such as the [FilterBuilder](FilterBuilder.md#class-filterbuilder).

Setting hidden:true means the operator can be used in a programmatic search, for example, by calling [ResultSet.setCriteria](ResultSet.md#method-resultsetsetcriteria), but does not appear in the UI.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.fieldTypes

### Description
List of types that this Operator is valid for.

If omitted, the operator is assumed to be valid for all FieldTypes unless a list of FieldTypes is passed to [DataSource.addSearchOperator](DataSource.md#method-datasourceaddsearchoperator).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.titleProperty

### Description
Name of a property on the [Operators](Operators.md#class-operators) class that provides the title for this operator.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.ID

### Description
Unique id for an operator, which appears within [AdvancedCriteria](../reference.md#object-advancedcriteria) as the [Operator](../reference.md#object-operator) property.

A list of built-in identifiers is [here](../reference.md#type-operatorid).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.textTitle

### Description
User-visible title for this operator when used with text-based fields - eg, "equals (match case)" rather than just "equals".

To simplify internationalization by separating titles from operator code, you can use specify [Operator.textTitleProperty](#attr-operatortexttitleproperty) instead of this property.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.title

### Description
User-visible title for this operator, such as "doesn't contain".

To simplify internationalization by separating titles from operator code, you can use specify [Operator.titleProperty](#attr-operatortitleproperty) instead of this property.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.editorType

### Description
For an operator with [Operator.valueType](#attr-operatorvaluetype):"custom", indicates what kind of FormItem to use to provide a user interface for creating a valid [Criterion](../reference_2.md#object-criterion). The default of `null` means an ordinary TextItem is fine.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.symbol

### Description
The text use when using this operator as an [expression](FormItem.md#attr-formitemallowexpressions) in a FormItem.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.requiresServer

### Description
Whether this operator needs to be executed on the server side.

This implies that if a [Criterion](../reference_2.md#object-criterion) using this operator is either introduced into [criteria](../reference.md#object-advancedcriteria) or is changed, the server will need to be contacted to perform filtering.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.valueType

### Description
Indicates the kind of value expected in a [Criterion](../reference_2.md#object-criterion) that uses this operator. [OperatorValueType](../reference.md#type-operatorvaluetype) lists possibilities.

The default of `null` is equivalent to "fieldType", indicating that [Criterion.value](Criterion.md#attr-criterionvalue) is expected to contain a value of the same type as the field indicated by [Criterion.fieldName](Criterion.md#attr-criterionfieldname).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.usageHint

### Description
Usage hint text specific to this Operator and shown, for example, in the hover-text of [ListGrid](ListGrid_1.md#class-listgrid) [filterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) fields.

If unset, the default for all operators, this value is derived from an attribute on the [Operators](Operators.md#class-operators) class, in the format \[operator.valueType\]UsageHint - for example, the ["between"](Operators.md#classattr-operatorsbetweentitle) operator uses [Operators.valueRangeUsageHint](Operators.md#classattr-operatorsvaluerangeusagehint).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: Operator.textTitleProperty

### Description
Name of a property on the [Operators](Operators.md#class-operators) class that provides the title for this operator when used with text-based fields.

### Groups

- advancedFilter

**Flags**: IR

---
## Method: Operator.compareCriteria

### Description
Compare two criteria, both of which use this operator, and report whether the newCriteria is definitely more restrictive than the previous criteria.

This is used by the [ResultSet](ResultSet.md#class-resultset) to understand whether client-side filtering can continue using cached data, or whether server-side filtering must be used instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriterion | [Criterion](#type-criterion) | false | — | new criterion |
| oldCriterion | [Criterion](#type-criterion) | false | — | previous criterion |

### Returns

`[Number](#type-number)` — 0 if the criteria are equivalent, 1 if newCriterion is guaranteed more restrictive, and -1 if newCriterion is not guaranteed more restrictive

### Groups

- advancedFilter

---
## Method: Operator.getCriterion

### Description
In combination with [Operator.editorType](#attr-operatoreditortype), this override point allows you to define a client-side only Operator that simply provides a custom UI for creating a Criterion based on one of the built-in operators.

For example, the "between" operator allows AdvancedCriteria to be created that can select any date range, however in a given application certain specific date ranges might be more meaningful (eg "next week", "last quarter") and you might want to offer the user a picker for those date ranges. You could create an operator "presetDateRange" with an editorType indicating a custom SelectItem that shows available ranges, and then implement operation.getCriterion() to take the value from this SelectItem and produce a Criterion selecting the chosen date range.

Note that another approach, if it's not required that this custom interface appear in the FilterBuilder, is just to have a separate DynamicForm for picking special date ranges, and use [DataSource.combineCriteria](DataSource.md#classmethod-datasourcecombinecriteria) to merge the criteria with the FilterBuilder's criteria, as in *this sample*.

If not implemented, returns the result of calling [getCriterion()](FormItem.md#method-formitemgetcriterion) on the passed [item](FormItem.md#class-formitem).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | — |
| item | [FormItem](#type-formitem) | false | — | — |

### Returns

`[Criterion](#type-criterion)` — —

---
## Method: Operator.condition

### Description
Method which actually evaluates whether a given record meets a [Criterion](../reference_2.md#object-criterion).

For operators that act on [sub-criteria](Criterion.md#attr-criterioncriteria), call [DataSource.evaluateCriterion](DataSource.md#method-datasourceevaluatecriterion) to evaluate sub-criteria.

Because criteria are sometimes applied to user-entered data that has not been validated, a robust `condition()` function should expect that data found in a [Record](../reference.md#object-record) may be null, NaN, not the correct type (eg "NA" for a type:"date" field) or otherwise out of the expected range.

Note that `this` is the [Operator](../reference.md#object-operator) object, allowing a `condition()` function to be shared across a range of related operators with different [OperatorId](../reference.md#type-operatorid)s.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | the [Criterion.fieldName](Criterion.md#attr-criterionfieldname) |
| value | [Any](#type-any) | false | — | value of the record at [Criterion.fieldName](Criterion.md#attr-criterionfieldname), if applicable |
| criterionValues | [CriterionValues](#type-criterionvalues) | false | — | the [CriterionValues](../reference.md#object-criterionvalues) |
| dataSource | [DataSource](#type-datasource) | false | — | the [DataSource](DataSource.md#class-datasource) performing the evaluation |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the record passes the `Criterion`

### Groups

- advancedFilter

---
