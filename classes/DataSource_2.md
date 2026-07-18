# DataSource Documentation (Part 2 of 2)

[← Back to API Index](../reference.md)

---

## Method: DataSource.supportsDynamicTreeJoins

### Description
This method returns true for dataSources that support both self-joins and [additionalOutputs](DSRequest.md#attr-dsrequestadditionaloutputs). A "self-join" is a relation from a dataSource back to itself - for example a relation between a worker and his manager, both of whom are Employees. DataSources that can handle self-joins are able to create and navigate these relations, which are mostly useful for tree-type structures.

Out of the box, only the built-in [SQL DataSource](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) implementation supports self-joins, and thus dynamic tree joins; neither [clientOnly](DataSource_1.md#attr-datasourceclientonly) nor the other server-side built-in DataSource implementations support them. If you create a custom DataSource implementation that can handle both of these features, you can set the [allowDynamicTreeJoins](DataSource_1.md#attr-datasourceallowdynamictreejoins) flag to true, which will cause supportsDynamicTreeJoins() to return true (and equally, you can set that flag explicitly to false to prevent the system from using dynamic tree joins for a given dataSource, even if it is able to use them)

This method is called by the automatic [ResultTree.keepParentsOnFilter](ResultTree.md#attr-resulttreekeepparentsonfilter) algorithm to decide if it is possible to use self-referencing `additionalOutputs` to improve efficiency, and possibly performance.

### Returns

`[Boolean](#type-boolean)` — true if this dataSource supports both `additionalOutputs` and self-joins, otherwise false

---
## Method: DataSource.isDiscriminatedComplexField

### Description
Returns true if `field` is marked with [DataSourceField.typeDiscriminator](DataSourceField.md#attr-datasourcefieldtypediscriminator) and its resolved type is complex (a DataSource relationship) rather than atomic - the condition under which schema-rendering callers such as [DataSource.asJSONSchema](DataSource_1.md#method-datasourceasjsonschema) (via [JSONSchemaSettings.omitDiscriminatedFields](JSONSchemaSettings.md#attr-jsonschemasettingsomitdiscriminatedfields)) omit the field until the named discriminator field's value is known.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield) | false | — | field to test |

### Returns

`[Boolean](#type-boolean)` — true if the field should be omitted while discriminated-field omission is active

---
## Method: DataSource.getPrimaryKeyFields

### Description
Returns this DataSource's [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) fields as a map of fieldName to field.

### Returns

`[Record](#type-record)` — Javascript object containing all this datasource's primaryKey fields, as a map of field name to field

### See Also

- [DataSource.getPrimaryKeyField](DataSource_1.md#method-datasourcegetprimarykeyfield)
- [DataSource.getPrimaryKeyFieldNames](DataSource_1.md#method-datasourcegetprimarykeyfieldnames)

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
