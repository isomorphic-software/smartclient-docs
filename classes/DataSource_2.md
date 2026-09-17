# DataSource Documentation (Part 2 of 2)

[← Back to API Index](../reference.md)

---

## Method: DataSource.getFetchDataURL

### Description
Returns a URL to DataSource fetch operation. This API is intended to return media such as images or videos to the browser.

Note that because the entirety of the request is encoded in the URL, there is an inherent limitation on the amount of data that you can send viat he criteria argument to the server. The actual length depends on your server configuration and other factors such as the size of cookies (if any) being sent to the server and other HTTP headers in use. Conservatively, assume that you have about 2 kilobytes to work with.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | Criteria to be sent to server. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Returns

`[String](#type-string)` — a URL that targets the specified fetch operation.

---
## Method: DataSource.getTextMatchStyleJSONSchema

### Description
Returns a JSON Schema for a DSRequest `textMatchStyle` value. This is a fixed enum and does not depend on DataSource shape, but is exposed as an instance method for uniform access alongside the other DSRequest sub-schemas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [JSONSchemaSettings](#type-jsonschemasettings) | true | — | Optional settings. |

### Returns

`[Object](../reference.md#type-object)|[String](#type-string)` — JSON Schema.

---
## Method: DataSource.getAllPathsToRelation

### Description
Returns all known paths between this and the given targetDS.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetDS | [String](#type-string)|[DataSource](#type-datasource) | false | — | The DataSource at the relationship's other end. |

### Returns

`[RelationPath](#type-relationpath)` — Array ofAll known paths between this and the given targetDS.

---
## Method: DataSource.getFileURL

### Description
Returns a direct URL to access a file stored in a field of type:"binary".

This URL can be used as the "src" attribute of an Img widget or `<img>` tag (if the file is an image), or can be used in an ordinary HTML link (`<a>` tag) to download the file. However, for the latter use case, see also [DataSource.downloadFile](#method-datasourcedownloadfile) and [DataSource.viewFile](DataSource_1.md#method-datasourceviewfile).

The URL returned is not to a static file on disk, rather, the returned URL essentially encodes a DSRequest as URL parameters, in a format understood by the IDACall servlet that comes with the Server Framework.

Hence, this URL will dynamically retrieve whatever file is currently stored in the binary field via executing a normal DSRequest server side. The request will run through normal security checks, so if your application requires authentication, the user must have a valid session and be authorized to access the binary field.

Note that if this method is called for a record with no associated file, the returned URL may not be functional. By default when dataSources encounter a [binary type fields](../reference_2.md#type-fieldtype), an additional field, ``<fieldName>`_filename`, is generated to store the filename for the binary field value. If this field is present in the data source but has no value for this record, developers can assume they're working with a record with no stored file. If this field is not present in some custom dataSource configuration, or the record is not loaded on the client, an additional server transaction may be required to determine whether the record has an associated file before calling this method to retrieve a download URL.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record)|[PKValue](#type-pkvalue) | false | — | Record containing at least the primary key field, or just the value of the primary key field. |
| fieldName | [FieldName](../reference.md#type-fieldname) | true | — | Optional name of the binary field containing the file. If not provided, the first binary field is used. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Additional properties to set on the DSRequest that will be issued. |

### Returns

`[String](#type-string)` — a URL to directly access the stored file

---
## Method: DataSource.recordsAsText

### Description
Converts a list of Records to simple text formats with a Record per line and values separated by a configurable separator, including both tab-separated-values and comma-separated-values (aka CSV).

In addition to the `settings` parameter for this method, [DataSourceField.exportForceText](DataSourceField.md#attr-datasourcefieldexportforcetext) can be set.

If two or more different text exports are needed for the same DataSource creating a conflict for any DataSourceField setting, [DataSource.inheritsFrom](DataSource_1.md#attr-datasourceinheritsfrom) can be used to create a child DataSource where these settings can be changed without recapitulating all field definitions.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record) | false | — | records to convert |
| settings | [TextExportSettings Properties](#type-textexportsettings-properties) | true | — | settings for the export |

### Returns

`[String](#type-string)` — records as CSV/TSV (separator can be specified)

---
## Method: DataSource.fetchRecord

### Description
Fetch a single record from the DataSource by [primary key](DataSourceField.md#attr-datasourcefieldprimarykey). This simply calls [DataSource.fetchData](DataSource_1.md#method-datasourcefetchdata) after creating [Criteria](../reference_2.md#type-criteria) that contain the primary key field and value.

If you call this method on a DataSource with a composite primary key - ie, one with multiple primaryKey fields - this method returns the first record where the first defined primary field matches the supplied pkValue; this may or may not be meaningful, depending on your use case. Generally, for DataSources with composite keys, it makes more sense to use `fetchData()` directly, rather than this convenience method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pkValue | [Any](#type-any) | false | — | value for the field marked [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey):true in this DataSource (or the first field so marked if there is more than one) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

---
## Method: DataSource.discardQueuedChanges

### Description
Removes queued requests from [DataSource.pendingChanges](DataSource_1.md#attr-datasourcependingchanges) without sending them to the server.

Accepts standard [Criteria](../reference_2.md#type-criteria) or [AdvancedCriteria](../reference.md#object-advancedcriteria) to filter which requests to discard, matched against DSRequest fields. Common filters:

```
 // Discard all
 ds.discardQueuedChanges();

 // Discard by operation type
 ds.discardQueuedChanges({ operationType: "add" });

 // Discard specific request
 ds.discardQueuedChanges({ requestId: "employees_request47" });

 // Discard requests older than a date
 ds.discardQueuedChanges({
     _constructor: "AdvancedCriteria",
     fieldName: "clientTimestamp",
     operator: "lessThan",
     value: cutoffDate
 });
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria) | true | — | Optional filter for which requests to discard |

### Returns

`[int](../reference.md#type-int)` — Number of requests discarded

### See Also

- [DataSource.pendingChanges](DataSource_1.md#attr-datasourcependingchanges)

---
## Method: DataSource.getSortByJSONSchema

### Description
Returns a JSON Schema for a DSRequest `sortBy` value against this DataSource. The schema allows any of the three documented forms: a single field-path string, an array of field-path strings, or an array of [SortSpecifier](../reference_2.md#object-sortspecifier) objects.

Field references include dotted FK-graph paths out to [jSONSchemaSettings.fkDepth](#jsonschemasettingsfkdepth) (default 2), so an Order DataSource with a `customerId` foreign key will accept `"customerId.name"` as a sort property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [JSONSchemaSettings](#type-jsonschemasettings) | true | — | Optional settings. |

### Returns

`[Object](../reference.md#type-object)|[String](#type-string)` — JSON Schema object (or string if [JSONSchemaSettings.asString](JSONSchemaSettings.md#attr-jsonschemasettingsasstring)).

---
## Method: DataSource.supportsAdvancedCriteria

### Description
Do fetch and filter operations on this dataSource support being passed [AdvancedCriteria](../reference.md#object-advancedcriteria)?

For a DataSource to support being passed AdvancedCriteria, it must be [clientOnly:true](DataSource_1.md#attr-datasourceclientonly) or [cacheAllData:true](DataSource_1.md#attr-datasourcecachealldata), or have server side logic which can process AdvancedCriteria objects passed from the client.

AdvancedCriteria are supported on the server for standard [SQL](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources), [Hibernate](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) and [JPA](../kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa) DataSources in SmartClient Enterprise or Power editions (not supported in SmartClient Pro).

The framework assumes that custom dataSources support AdvancedCriteria; if you have a a custom DataSource implementation that does not support AdvancedCriteria, you can set the [DataSource.allowAdvancedCriteria](DataSource_1.md#attr-datasourceallowadvancedcriteria) property to false.

### Returns

`[Boolean](#type-boolean)` — true if this dataSource supports being passed AdvancedCriteria in fetch and filter type operations, false otherwise.

---
## Method: DataSource.getDisplayValue

### Description
Given a fieldName and a dataValue, apply any [DataSourceField.valueMap](DataSourceField.md#attr-datasourcefieldvaluemap) for the field and return the display value for the field

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | name of the field to retrieve a value for |
| value | [Any](#type-any) | false | — | data value for the field |

### Returns

`[Any](#type-any)` — display value for the field

---
## Method: DataSource.isCalculated

### Description
Does the specified field have its value dynamically calculated via [DataSourceField.formula](DataSourceField.md#attr-datasourcefieldformula) or other similar attributes?

This method will return true for fields with the following attributes:

*   [DataSourceField.formula](DataSourceField.md#attr-datasourcefieldformula)
*   [DataSourceField.template](DataSourceField.md#attr-datasourcefieldtemplate)
*   [DataSourceField.customSelectExpression](DataSourceField.md#attr-datasourcefieldcustomselectexpression)

Or if the field has explicitly been marked as [calculated:true](DataSourceField.md#attr-datasourcefieldcalculated).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield)|[String](#type-string) | false | — | Field or fieldName |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a field with dynamically calculated values

---
## Method: DataSource.handleError

### Description
If you define this method on a DataSource, it will be called whenever the server returns a DSResponse with a status other than [RPCResponse.STATUS_SUCCESS](RPCResponse.md#classattr-rpcresponsestatus_success). You can use this hook to do DataSource-specific error handling. Unless you return `false` from this method, [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror) will be called by SmartClient right after this method completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [DSResponse](#type-dsresponse) | false | — | the DSResponse or DSResponse object returned from the server |
| request | [DSRequest](#type-dsrequest) | false | — | the DSRequest or DSRequest that was sent to the server |

### Returns

`[Boolean](#type-boolean)` — false to suppress [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror)

### Groups

- errorHandling

### See Also

- [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror)

**Flags**: A

---
## Method: DataSource.hasFile

### Description
Indicates whether a file exists in this DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType or fileFormat are not provided, will indicate whether any file with the provided fileName exists. |
| callback | [HasFileCallback](#type-hasfilecallback) | false | — | [Callback](Callbacks.md#method-callbackshasfilecallback) executed with the results. The `data` parameter is a boolean indicating whether the file is present. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.convertRelativeDates

### Description
Takes all relative date values found anywhere within a Criteria / AdvancedCriteria object and converts them to concrete date values, returning the new criteria object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | criteria to convert |
| timezoneOffset | [String](#type-string) | true | — | optional timezone offset. Defaults to the current timezone |
| firstDayOfWeek | [Integer](../reference_2.md#type-integer) | true | — | first day of the week (zero is Sunday). Defaults to [DateChooser.firstDayOfWeek](DateChooser.md#attr-datechooserfirstdayofweek) |
| baseDate | [Date](#type-date) | true | — | base value for relative conversion - defaults to now |

### Returns

`[Criteria](../reference_2.md#type-criteria)` — new copy of the criteria with all relative dates converted

---
## Method: DataSource.addSearchOperator

### Description
Add a new search operator, only to this DataSource.

If an existing [Operator](../reference_2.md#object-operator) is passed, restricts the set of FieldTypes to which that operator can be applied in this DataSource.

See also [DataSource.addSearchOperator](DataSource.md#classmethod-datasourceaddsearchoperator) for adding operators to all DataSources.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operator | [Operator](#type-operator) | false | — | definition of the operator to add |
| types | [Array of FieldType](#type-array-of-fieldtype) | true | — | types to which this operator applies |

### Groups

- advancedFilter

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
