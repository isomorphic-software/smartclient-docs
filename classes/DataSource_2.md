# DataSource Documentation (Part 2 of 2)

[← Back to API Index](../reference.md)

---

## Method: DataSource.invalidateCache

### Description
Drop the current dataSource cache. This has two effects:

*   For DataSources [DataSource.cacheAllData](DataSource_1.md#attr-datasourcecachealldata) or [clientOnly](DataSource_1.md#attr-datasourceclientonly), discard the current client-side cache data.
*   If `notify` is passed, cause all [data objects](ResultSet.md#class-resultset) associated with this dataSource to drop their caches. This occurs regardless of the dataSource type - and can be thought of as equivalent to processing a response with [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache) set.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| notify | [boolean](../reference.md#type-boolean) | true | — | Should data objects associated with this dataSource have their cache invalidated? |

### Groups

- clientData

---
## Method: DataSource.downloadFile

### Description
Download a file stored in a field of type:"binary" in a DataSource record.

This will trigger the browser's "Save As" dialog and allow the user to save the file associated with some record.

Note that if this method is called for a record with no associated file, the download URL may not be functional. By default when dataSources encounter a [binary type fields](../reference_2.md#type-fieldtype), an additional field, ``<fieldName>`_filename`, is generated to store the filename for the binary field value. If this field is present in the data source but has no value for this record, developers can assume they're working with a record with no stored file. If this field is not present in some custom dataSource configuration, or the record is not loaded on the client, an additional server transaction may be required to determine whether the record has an associated file before calling this method to download a file.

See the overview of [Binary Fields](../kb_topics/binaryFields.md#kb-topic-binary-fields) for more details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record) | false | — | Record to download. Only required to have a value for the primary key field. |
| fieldName | [FieldName](../reference.md#type-fieldname) | true | — | Optional name of the binary field containing the file. If not provided, the first binary field is used. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Additional properties to set on the DSRequest that will be issued. |

---
## Method: DataSource.getClientOnlyDataSource

### Description
Produces a clientOnly "copy" of a particular subset of data from a normal DataSource, via calling fetchData() to fetch matching rows, and constructing a clientOnly DataSource that [DataSource.inheritsFrom](DataSource_1.md#attr-datasourceinheritsfrom) the original DataSource.

This clientOnly "copy" can be useful in situations where you want to allow a series of local changes without immediately committing to the server. See also [ListGrid.autoSaveEdits](ListGrid_1.md#attr-listgridautosaveedits) for more fine-grained tracking of edits (eg, special styling for uncommitted changes).

The new DataSource is returned via the "callback" argument. If [DataSource.cacheAllData](DataSource_1.md#attr-datasourcecachealldata) is enabled and [DataSource.hasAllData](DataSource_1.md#method-datasourcehasalldata) returns true, the new DataSource is synchronously returned as the result of the method. In this case, if a callback was passed, it also is executed synchronously.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | The criteria for the clientOnly DS |
| callback | [ClientOnlyDataSourceCallback](#type-clientonlydatasourcecallback) | false | — | The callback to fire passing the clientOnly DS |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | optional properties to pass through to the DSRequest |
| dataSourceProperties | [DataSource Properties](#type-datasource-properties) | true | — | optional properties to pass through to the clientOnly DS |

---
## Method: DataSource.supportsDynamicTreeJoins

### Description
This method returns true for dataSources that support both self-joins and [additionalOutputs](DSRequest.md#attr-dsrequestadditionaloutputs). A "self-join" is a relation from a dataSource back to itself - for example a relation between a worker and his manager, both of whom are Employees. DataSources that can handle self-joins are able to create and navigate these relations, which are mostly useful for tree-type structures.

Out of the box, only the built-in [SQL DataSource](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) implementation supports self-joins, and thus dynamic tree joins; neither [clientOnly](DataSource_1.md#attr-datasourceclientonly) nor the other server-side built-in DataSource implementations support them. If you create a custom DataSource implementation that can handle both of these features, you can set the [allowDynamicTreeJoins](DataSource_1.md#attr-datasourceallowdynamictreejoins) flag to true, which will cause supportsDynamicTreeJoins() to return true (and equally, you can set that flag explicitly to false to prevent the system from using dynamic tree joins for a given dataSource, even if it is able to use them)

This method is called by the automatic [ResultTree.keepParentsOnFilter](ResultTree.md#attr-resulttreekeepparentsonfilter) algorithm to decide if it is possible to use self-referencing `additionalOutputs` to improve efficiency, and possibly performance.

### Returns

`[Boolean](#type-boolean)` — true if this dataSource supports both `additionalOutputs` and self-joins, otherwise false

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
Get the list of [Operator](../reference.md#object-operator)s available for this [FieldType](../reference_2.md#type-fieldtype), as a [ValueMap](../reference_2.md#type-valuemap) from [OperatorId](../reference.md#type-operatorid) to the [Operator.title](Operator.md#attr-operatortitle) specified for the [Operator](../reference.md#object-operator), or the corresponding property in [Operators](Operators.md#class-operators) if [Operator.titleProperty](Operator.md#attr-operatortitleproperty) is set.

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

Typically called by the [condition](Operator.md#method-operatorcondition) function of a custom [Operator](../reference.md#object-operator) to evaluate [sub-criteria](Criterion.md#attr-criterioncriteria).

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
