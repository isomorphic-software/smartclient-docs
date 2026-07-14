# DataSource Documentation (Part 2 of 2)

[← Back to API Index](../reference.md)

---

## Method: DataSource.getTypeOperatorMap

### Description
Get the list of [Operator](../reference_2.md#object-operator)s available for this [FieldType](../reference_2.md#type-fieldtype), as a [ValueMap](../reference_2.md#type-valuemap) from [OperatorId](../reference.md#type-operatorid) to the [Operator.title](Operator.md#attr-operatortitle) specified for the [Operator](../reference_2.md#object-operator), or the corresponding property in [Operators](Operators.md#class-operators) if [Operator.titleProperty](Operator.md#attr-operatortitleproperty) is set.

This valueMap is suitable for use in a UI for building queries, similar to the [FilterBuilder](FilterBuilder.md#class-filterbuilder), and optionally omits operators marked [Operator.hidden](Operator.md#attr-operatorhidden) : true.

It is also possible to have this function return only operators of a given [OperatorValueType](../reference_2.md#type-operatorvaluetype), or everything except operators of that type. This is useful, for example, if you want to return all the logical operators (like "and"), or everything except the logical operators.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [FieldType](../reference_2.md#type-fieldtype) | true | — | Type to obtain operator map for. Defaults to "text" if not passed. |
| includeHidden | [boolean](../reference.md#type-boolean) | true | — | whether to include Operators marked hidden:true |
| valueType | [OperatorValueType](../reference_2.md#type-operatorvaluetype) | true | — | If passed, returns only operators of this [OperatorValueType](../reference_2.md#type-operatorvaluetype) |
| omitValueType | [boolean](../reference.md#type-boolean) | true | — | If set, reverses the meaning of the `valueType` parameter, so operators of that [OperatorValueType](../reference_2.md#type-operatorvaluetype) are the only ones omitted |

### Returns

`[ValueMap](../reference_2.md#type-valuemap)` — mapping from [OperatorId](../reference.md#type-operatorid) to title, as described above

### Groups

- advancedFilter

### See Also

- [DataSource.getFieldOperatorMap](DataSource_1.md#method-datasourcegetfieldoperatormap)

---
## Method: DataSource.getLegalChildTags

### Description
For a DataSource that describes a DOM structure, the list of legal child elements that can be contained by the element described by this DataSource.

For a DataSource described by XML schema, this is the list of legal subelements **of complexType** (elements of simpleType become DataSourceFields with atomic type).

Note that currently, if an XML schema file contains ordering constraints, DataSources derived from XML Schema do not capture these constraints.

### Groups

- xmlSchema

---
## Method: DataSource.evaluateCriterion

### Description
Evaluate the given criterion with respect to the passed record.

Typically called by the [condition](Operator.md#method-operatorcondition) function of a custom [Operator](../reference_2.md#object-operator) to evaluate [sub-criteria](Criterion.md#attr-criterioncriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record to evaluate |
| criterion | [Criterion](#type-criterion) | false | — | criterion to use |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the record meets the supplied [Criterion](../reference_2.md#object-criterion)

### Groups

- advancedFilter

---
