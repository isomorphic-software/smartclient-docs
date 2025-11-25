# OperationBinding Documentation

[← Back to API Index](../main.md)

---

## Class: OperationBinding

### Description
An operationBinding tells a DataSource how to execute one of the basic DS operations: fetch, add, update, remove. See [DataSource.operationBindings](DataSource.md#attr-datasourceoperationbindings).

---
## Attr: OperationBinding.requiredCriterion

### Description
A comma-separated list of field names that must be present in criteria / advancedCriteria provided by the caller. Failure to provide any one of these will yield a [RPCResponse.STATUS_CRITERIA_REQUIRED_ERROR](RPCResponse.md#classattr-rpcresponsestatus_criteria_required_error) from the server.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.headers

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.headers](DataSource.md#attr-datasourceheaders) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.recordName

### Description
For an XML DataSource, tagName of the elements to be used as records.

This is a simple alternative to [OperationBinding.recordXPath](#attr-operationbindingrecordxpath) when the elements to be used as records all share a tagName.

When a DataSource has a WebService, `recordName` can also be set to the name of any `complexType` declared within the WebService's WSDL file.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.transformRawResponseScript

### Description
**Applicable to [server-side REST DataSources](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector) only**

A scriptlet to be executed on the server after data has been fetched from the REST service by this operation, but before it is processed through templating. See [DataSource.transformRawResponseScript](DataSource.md#attr-datasourcetransformrawresponsescript) for further details.

Note, unlike many OperationBinding-level properties, a `transformRawResponseScript` at the OperationBinding level does not hide a `transformRawResponseScript` defined at the DataSource level. Instead, if you define `transformRawResponseScript` against both the DataSource and the OperationBinding, **both** are run - first the DataSource-level script, then the OperationBinding-level one.

### Groups

- serverScript

**Flags**: IR

---
## Attr: OperationBinding.outputs

### Description
Specifies, for this operationBinding only, the list of field names that should be returned to the client. Typically this will be a subset of the [DataSource.fields](DataSource.md#attr-datasourcefields), but note that this is not a requirement; `outputs` can include fields that are not defined in the DataSource's field list. In this case, the server will return extra fields even if [DataSource.dropExtraFields](DataSource.md#attr-datasourcedropextrafields) is true.

You specify this property as a string containing a comma-separated list of field names (eg, "foo, bar, baz")

Note that this setting overrides [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs) and [DataSourceField.outputWhen](DataSourceField.md#attr-datasourcefieldoutputwhen) setting, meaning fields listed in operationBinding.outputs will be returned to the client regardless of those settings.

### See Also

- [DataSourceField.outputWhen](DataSourceField.md#attr-datasourcefieldoutputwhen)
- [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs)

**Flags**: IR

---
## Attr: OperationBinding.dataTransport

### Description
Transport to use for this operation. Defaults to [DataSource.dataTransport](DataSource.md#attr-datasourcedatatransport), which in turn defaults to [RPCManager.defaultTransport](RPCManager.md#classattr-rpcmanagerdefaulttransport). This would typically only be set to enable "scriptInclude" transport for contacting [JSON](DataSource.md#attr-datasourcedataformat) web services hosted on servers other than the origin server.

When using the "scriptInclude" transport, be sure to set [DataSource.callbackParam](DataSource.md#attr-datasourcecallbackparam) or [OperationBinding.callbackParam](#attr-operationbindingcallbackparam) to match the name of the query parameter name expected by your JSON service provider.

### Groups

- clientDataIntegration

### See Also

- [RPCTransport](../main.md#type-rpctransport)
- [DataSource.callbackParam](DataSource.md#attr-datasourcecallbackparam)

**Flags**: IR

---
## Attr: OperationBinding.preventHTTPCaching

### Description
Configures [DataSource.preventHTTPCaching](DataSource.md#attr-datasourcepreventhttpcaching) on a per-operationType basis.

**Flags**: IR

---
## Attr: OperationBinding.ansiJoinClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke ANSI-style joins clause to use when constructing the SQL query to perform this operation. The property should be a set of joins implemented with JOIN directives (as opposed to additional join expressions in the where clause), joining related tables to the main table or view defined in [tableClause](#attr-operationbindingtableclause). The server will insert the text of this property immediately after the [tableClause](#attr-operationbindingtableclause).

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [DataSource.useAnsiJoins](DataSource.md#attr-datasourceuseansijoins)
- [OperationBinding.includeAnsiJoinsInTableClause](#attr-operationbindingincludeansijoinsintableclause)

**Flags**: IR

---
## Attr: OperationBinding.transformResponseScript

### Description
Scriptlet to be executed after the DataSource operation which is configured by this operationBinding. See [DataSource.transformResponseScript](DataSource.md#attr-datasourcetransformresponsescript) for further details.

Note, unlike many OperationBinding-level properties, a `transformResponseScript` at the OperationBinding level does not hide a `transformResponseScript` defined at the DataSource level. Instead, if you define `transformResponseScript` against both the DataSource and the OperationBinding, **both** are run - first the DataSource-level script, then the OperationBinding-level one.

### Groups

- serverScript

**Flags**: IR

---
## Attr: OperationBinding.qualifyColumnNames

### Description
Specifies, for this specific operationBinding, whether to qualify column names with table names in any SQL we generate. Overrides the [DataSource.qualifyColumnNames](DataSource.md#attr-datasourcequalifycolumnnames) property. Only applicable to dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql".

**Flags**: IR

---
## Attr: OperationBinding.description

### Description
An optional description of the operationBinding's behavior. Not automatically exposed on any component, but useful for developer documentation, and as such is included on any [OpenAPI specification](../kb_topics/openapiSupport.md#kb-topic-openapi-specification-oas-support) generated by the framework. Markdown is a commonly used syntax, but you may also embed HTML content in a CDATA tag.

**Flags**: IR

---
## Attr: OperationBinding.customValueFields

### Description
Indicates that the listed fields should be included in the default [selectClause](#attr-operationbindingselectclause) and [valuesClause](#attr-operationbindingvaluesclause) generated for this operationBinding, even if they are marked [customSQL](DataSourceField.md#attr-datasourcefieldcustomsql)="true".

You can specify this property as a comma-separated list (eg, "foo, bar, baz") or by just repeating the `<customValueFields>` tag multiple times with one field each.

This property is only applicable to DataSources of ["sql"](DataSource.md#attr-datasourceservertype).

### Groups

- customQuerying

### See Also

- [OperationBinding.customFields](#attr-operationbindingcustomfields)
- [OperationBinding.customCriteriaFields](#attr-operationbindingcustomcriteriafields)

**Flags**: IR

---
## Attr: OperationBinding.groupBy

### Description
List of fields to group by when using [server-side summarization](../kb_topics/serverSummaries.md#kb-topic-server-summaries).

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for details and examples of usage.

### Groups

- serverSummaries

### See Also

- [OperationBinding.summaryFunctions](#attr-operationbindingsummaryfunctions)

**Flags**: IR

---
## Attr: OperationBinding.lineBreakStyle

### Description
The style of line-breaks to use in the exported output. See [LineBreakStyle](../main.md#type-linebreakstyle) for more information.

**Flags**: IR

---
## Attr: OperationBinding.multiInsertNonMatchingStrategy

### Description
For "add" operations on dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, this property sets the multi-insert "non matching" strategy for this [operation](#class-operationbinding). Only has an effect if the [add request](DataSource.md#method-datasourceadddata) specifies a list of records as the data, and only if [multiInsertStrategy](#attr-operationbindingmultiinsertstrategy) is set to "multipleValues" either globally or at the [DSRequest](../main_2.md#object-dsrequest), [OperationBinding](#class-operationbinding), or [DataSource](DataSource.md#class-datasource) level.

Note that this setting overrides the equivalent [dataSource setting](DataSource.md#attr-datasourcemultiinsertnonmatchingstrategy), and can in turn be overridden at the [DSRequest level](DSRequest.md#attr-dsrequestmultiinsertnonmatchingstrategy)

### See Also

- [OperationBinding.multiInsertStrategy](#attr-operationbindingmultiinsertstrategy)
- [OperationBinding.multiInsertBatchSize](#attr-operationbindingmultiinsertbatchsize)

**Flags**: IRW

---
## Attr: OperationBinding.mail

### Description
Definition of an email message that will be sent as an after-effect of selecting or updating data.

Note that if a fixed number of different messages need to be sent, multiple ``<mail>`` tags may be specified. For example, one mail could be sent to an admin address, and a different message to every member of a user group.

### Groups

- mail

**Flags**: IR

---
## Attr: OperationBinding.dataProtocol

### Description
Controls the format in which inputs are sent to the dataURL.

When a DataSource operation such as fetchData() is invoked on this DataSource or a component bound to this DataSource, the data passed to the operation, if any, will be sent to the `dataURL`. The `dataProtocol` property controls the format in which the data is sent: SOAP message, HTTP GET or POST of parameters, etc.

The `dataProtocol` property need not be set for a DataSource with a WebService ( [DataSource.serviceNamespace](DataSource.md#attr-datasourceservicenamespace) is set), in this case, SOAP messaging is used by default.

Developers may completely bypass the SmartClient comm system by setting dataProtocol to `"clientCustom"`. In this case SmartClient will not attempt to send any data to the server after calling [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest). Instead the developer is expected to implement `transformRequest()` such that it performs the necessary data action outside of SmartClient, and then calls [DataSource.processResponse](DataSource.md#method-datasourceprocessresponse), passing in the [DSRequest.requestId](DSRequest.md#attr-dsrequestrequestid) and an appropriate set of DSResponse properties to indicate the result of the action.

NOTE: when [OperationBinding.dataFormat](#attr-operationbindingdataformat) is "iscServer", `dataProtocol` is not consulted. Instead, SmartClient uses a proprietary wire format to communicate with the SmartClient server, and the server-side DSRequest and DSResponse objects should be used to access request data and form responses.

### Groups

- clientDataIntegration

### See Also

- [DSProtocol](../main_2.md#type-dsprotocol)

**Flags**: IR

---
## Attr: OperationBinding.groupWhereClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

Alias for [OperationBinding.afterWhereClause](#attr-operationbindingafterwhereclause). Kept for backward compatibility. Same semantics and SQL insertion point. See the new attribute for full docs and examples.

If both `groupWhereClause` and `afterWhereClause` are set, `afterWhereClause` is used.

### See Also

- [OperationBinding.afterWhereClause](#attr-operationbindingafterwhereclause)
- [OperationBinding.useHavingClause](#attr-operationbindingusehavingclause)
- [OperationBinding.customSQL](#attr-operationbindingcustomsql)

**Deprecated**

**Flags**: IR

---
## Attr: OperationBinding.responseTemplate

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of the [DataSource.responseTemplate](DataSource.md#attr-datasourceresponsetemplate) - see that property's documentation for details

### Groups

- serverRestConnector

### See Also

- [DataSource.responseTemplate](DataSource.md#attr-datasourceresponsetemplate)
- [OperationBinding.transformResponseScript](#attr-operationbindingtransformresponsescript)
- [OperationBinding.requestTemplate](#attr-operationbindingrequesttemplate)

**Flags**: IR

---
## Attr: OperationBinding.requiresAuthentication

### Description
Whether a user must be authenticated in order to access this operation. For details of what is meant by "authenticated", see [DataSource.requiresAuthentication](DataSource.md#attr-datasourcerequiresauthentication).

To protect access to an entire operationType (eg, all "fetch" operations), declare an operationBinding with `requiresAuthentication="true"`, [OperationBinding.operationType](#attr-operationbindingoperationtype) set to the operationType to be protected, but no [OperationBinding.operationId](#attr-operationbindingoperationid). This will then prevent access to the "fetch" operationType unless another [OperationBinding](#class-operationbinding) declares requiresAuthentication="false" with a specific [operationId](#attr-operationbindingoperationid).

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: OperationBinding.useHavingClause

### Description
This setting switches between "having" clause and sub-select approaches when generating aggregated SQL queries. It also affects how aggregated fields are referred in:

*   generated [afterWhereClause](#attr-operationbindingafterwhereclause)
*   expressions generated by `SQLDataSource.getPartialHaving(...)` and `SQLDataSource.getHavingWithout(...)` server-side API
*   expressions generated by `$sql.partialHaving(...)` and `$sql.havingWithout(...)` [Velocity context](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables) variables used in [SQL Temlating](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview)

#### useHavingClause=true (default)
SQL query is generated using traditional "having" clause approach:
```
   select <selectClause>
     from ...
    where ...
 group by <groupClause>
   having <afterWhereClause>
 
```
Aggregated fields are referred by SQL expressions:
```
   select customer, sum(quantity * price) as amount
     from ...
    where ...
 group by customer
   having sum(quantity * price) > 10
 
```
#### useHavingClause=false
SQL query is generated using sub-select approach when main query becomes sub-select and then it is filtered in outer "where" clause:
```
 select *
 from (select <selectClause> from ... where ... group by <groupClause>) work
 where <afterWhereClause>
 
```
Aggregated fields are referred by aliases they are selected by:
```
   select *
     from (select customer, sum(quantity * price) as amount
             from ...
            where ...
         group by customer) work
    where amount > 10
 
```
If `operationBinding.useHavingClause` is omitted this may be controlled by `sql.MyDatabase.useHavingClause` setting in [server.properties](../kb_topics/sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties) on a per-database basis.

### See Also

- [OperationBinding.afterWhereClause](#attr-operationbindingafterwhereclause)

**Flags**: IR

---
## Attr: OperationBinding.customHQL

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "hibernate", this property can be specified on an operationBinding to indicate that the server should run user-specified HQL (Hibernate Query Language), rather than the Hibernate criteria query or `saveOrUpdate` call it would normally generate to satisfy a dataSource operation via Hibernate.

Note that inserting new records via HQL is often impractical, due to intentional restrictions in the language (it is only possible to perform an insert expressed in terms of a SELECT; the "VALUES" construct commonly used when inserting new rows singly is not supported). If you are intending to use customHQL, we recommend that you avoid doing so for [OperationBinding](#class-operationbinding)s with [operationType](#attr-operationbindingoperationtype) "add", unless you have a special requirement such as a bulk insert; if you need custom queries to perform inserts on "hibernate" dataSources, we recommend you use [customSQL](#attr-operationbindingcustomsql), which is valid for "hibernate" DataSources as well as "sql" dataSources.

For other operations on "hibernate" dataSources, however, HQL has the advantage of being more portable across different database engines than is plain SQL.

Note that using customHQL affects paging implementation. If you use it, full data set is fetched from Hibernate and records that aren't in the requested range are dropped at the server side.

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [OperationBinding.namedQuery](#attr-operationbindingnamedquery)
- [DataSourceField.customSQL](DataSourceField.md#attr-datasourcefieldcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.criteria

### Description
**Elements of this feature are only available with Power or better licenses.** See [smartclient.com/product](http://smartclient.com/product) for details.

A list of [DSRequestModifier](../main_2.md#object-dsrequestmodifier)s that will be used to modify the criteria of each [DSRequest](../main_2.md#object-dsrequest) that uses this operationBinding. Note that the criteria elements are applied to DSRequest criteria as follows:

*   **Simple criteria:** The field and value are just applied as an extra key/value pair in the criteria map, as long as the [operator](DSRequestModifier.md#attr-dsrequestmodifieroperator) attribute is left unset, or is set to "equals". For any other setting of `operator`, the criteria is first converted to the equivalent AdvancedCriteria and then processed as described below
*   **AdvancedCriteria:** If the topmost operator is "and", we add the new criterion as an additional criterion directly in the existing list. Otherwise, we create a new top-level AdvancedCriteria with an operator of "and". This is then set to have two elements in its criteria: the previous top-level criteria and the new criterion.

The effect of this is to apply any criteria specifed here as additional constraints on top of what the user has specified, and of course, the user is unable to affect this. Thus, this is a suitable and convenient place to enforce rules such as "Users can only ever see their own records".

Below is an example of the XML as it should be defined in your ds.xml, datasource definitions.

```
 <operationBindings>
   <operationBinding operationType="fetch" operationId="...">
     <criteria fieldName="USER_ROLE" value="ADMIN" operator="equals" />
   </operationBinding>
 </operationBindings>
 
```

### Groups

- transactionChaining

### See Also

- [OperationBinding.values](#attr-operationbindingvalues)

**Flags**: IR

---
## Attr: OperationBinding.useHttpProxy

### Description
Whether to use the [HttpProxy](RPCManager.md#classmethod-rpcmanagersendproxied) servlet to send requests described by this operationBinding. If unset, automatically detects whether using the HttpProxy is necessary based on the same-origin policy.

Valid only with [OperationBinding.dataProtocol](#attr-operationbindingdataprotocol) settings other than ISCServer.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.wsOperation

### Description
Name of the web service operation that will be invoked in order to execute this DataSource operation.

Valid only for a DataSource that has a WebService ([DataSource.serviceNamespace](DataSource.md#attr-datasourceservicenamespace) is set). Otherwise, use [OperationBinding.dataURL](#attr-operationbindingdataurl).

Setting `wsOperation` means that [DSRequest.data](DSRequest.md#attr-dsrequestdata) will be serialized as the request message for the specified web service operation, with namespacing and soap encoding handled automatically. See [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest) for how to customize what data is sent to the server.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.callbackParam

### Description
Applies only to dataFormat: "json". Specifies the name of the query parameter that tells your JSON service what function to call as part of the response for this operation.

Typically set once for the DataSource as a whole via [DataSource.callbackParam](DataSource.md#attr-datasourcecallbackparam).

### Groups

- clientDataIntegration

### See Also

- [DataSource.callbackParam](DataSource.md#attr-datasourcecallbackparam)

**Flags**: IR

---
## Attr: OperationBinding.responseFormat

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), the response format to use for this specific operationBinding. Overriddes any [DataSource-level setting](DataSource.md#attr-datasourceresponseformat). Note, if `responseFormat` is not specified at either the DataSource or OperationBinding level, response processing will throw an exception.

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.exportResults

### Description
When set, causes the results of the DataSource Operation to be exported to a file, whose name and format are indicated by [OperationBinding.exportFilename](#attr-operationbindingexportfilename) and [OperationBinding.exportAs](#attr-operationbindingexportas) respectively. When no exportFilename is provided, the default is _Results_ and the default value of exportAs is _csv_. Once the Operation completes, [DSRequest.exportDisplay](DSRequest.md#attr-dsrequestexportdisplay) specifies whether the exported data will be downloaded to the file-system or displayed in a new window. The default value of exportDisplay is "download" which displays the Save As dialog. See [ExportDisplay](../main_2.md#type-exportdisplay) for more information.

The export field-list can also be configured, see [DSRequest.exportFields](DSRequest.md#attr-dsrequestexportfields).

You can also configure the style of line-breaks to use when generating the output. See [LineBreakStyle](../main.md#type-linebreakstyle) for more information.

As well as setting this and other properties on the [OperationBinding](#class-operationbinding), Exports can be initiated in two other ways. You can set properties on the dsRequest by passing _requestProperties_ into [DataSource.exportData](DataSource.md#method-datasourceexportdata). Note that this method does not support exporting to JSON format (see [this post](http://forums.smartclient.com/showthread.php?t=235) for more detail). Additionally, custom server code may set export-related properties on the [DSResponse](DSResponse.md#class-dsresponse).

**Format Examples**

XML format

```
     <List>
         <Object>
             <id>10101</id>
             <displayName>Record 10101</displayName>
         </Object>
    </List>
 
```
JSON Format
```
     [
         { id: 10101, displayName: "Record 10101" }
     ]
 
```
CSV Format
```
     id,displayName
     10101,"Record 10101"
 
```

**Flags**: IR

---
## Attr: OperationBinding.serverObject

### Description
Optional ServerObject declaration that specifies the ServerObject configuration for this operationBinding. In the absence of a serverObject specification here, the one specified on the DataSource itself is used by default, if present ([DataSource.serverObject](DataSource.md#attr-datasourceserverobject)). If neither is present, then Direct Method Invocation will not be enabled for this operationBinding.

_Note that if a dataSource configuration has both a [`<script>`](#attr-operationbindingscript) block and a specified `serverObject` for some operation, the script block will be executed, and the serverObject ignored._

### See Also

- [DataSource.serverObject](DataSource.md#attr-datasourceserverobject)

**Flags**: IR

---
## Attr: OperationBinding.customJQL

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "jpa", this property can be specified on an operationBinding to indicate that the server should run user-specified JQL (Java Persistence Query Language).

Note that inserting new records via JQL is often impractical, due to intentional restrictions in the language (it is only possible to perform an insert expressed in terms of a SELECT; the "VALUES" construct commonly used when inserting new rows singly is not supported). If you are intending to use customJQL, we recommend that you avoid doing so for [OperationBinding](#class-operationbinding)s with [operationType](#attr-operationbindingoperationtype) "add", unless you have a special requirement such as a bulk insert; if you need custom queries to perform inserts on "jpa" dataSources, we recommend you use [customSQL](#attr-operationbindingcustomsql), which is valid for "jpa" DataSources as well as "sql" dataSources.

For other operations on "jpa" dataSources, however, JQL has the advantage of being more portable across different database engines than is plain SQL.

Note that using customJQL affects paging implementation. If you use it, full data set is fetched from JPA and records that aren't in the requested range are dropped at the server side.

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [OperationBinding.namedQuery](#attr-operationbindingnamedquery)
- [DataSourceField.customSQL](DataSourceField.md#attr-datasourcefieldcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.requestProperties

### Description
Additional properties to pass through to the [DSRequest](../main_2.md#object-dsrequest) created for this operation. Note that these will be cumulative with and will override on a per-property basis any properties set via [DataSource.requestProperties](DataSource.md#attr-datasourcerequestproperties).

These properties are applied before [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest) is called.

### Groups

- clientDataIntegration
- serverDataIntegration

### See Also

- [DSRequest](../main_2.md#object-dsrequest)
- [DataSource.requestProperties](DataSource.md#attr-datasourcerequestproperties)

**Flags**: IR

---
## Attr: OperationBinding.selectClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke SELECT clause to use when constructing the SQL query to perform this operation. The property should be a comma-separated list of column names and/or expressions, and you can refer to any scalar function supported by the underlying database. The server will insert the text of this property immediately after the "SELECT" token.

Note that if you also specify a [groupClause](#attr-operationbindinggroupclause), you can use aggregate functions such as SUM and COUNT in the selectClause.

This property is only applicable to operationBindings of [operationType](#attr-operationbindingoperationtype) "fetch".

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.summaryFunctions

### Description
A mapping from field names to [summary functions](../main_2.md#type-summaryfunction) to be applied to each field.

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [OperationBinding.groupBy](#attr-operationbindinggroupby)

**Flags**: IR

---
## Attr: OperationBinding.applySqlSuffixToRowCount

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For operations on DataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, if [OperationBinding.sqlSuffix](#attr-operationbindingsqlsuffix) is specified at either operation or DataSource level, should that prefix also be applied to the rowcount query, if one is run? This property is true by default, meaning we will apply the suffix to both rowcount and main queries

This property is ignored for non-SQL dataSources

This property can also be specified at the [DataSource level](DataSource.md#attr-datasourceapplysqlsuffixtorowcount); any such value acts as a default for the dataSource, and will be overridden by an operationBinding-level setting

### Groups

- customQuerying

### See Also

- [OperationBinding.applySqlPrefixToRowCount](#attr-operationbindingapplysqlprefixtorowcount)

**Flags**: IR

---
## Attr: OperationBinding.cacheSyncTiming

### Description
The [cacheSyncTiming](../main_2.md#type-cachesyncstrategy) to use for this operation. Overrides any [dataSource-level cacheSyncTiming](DataSource.md#attr-datasourcecachesynctiming)

### Groups

- cacheSynchronization

### See Also

- [OperationBinding.cacheSyncStrategy](#attr-operationbindingcachesyncstrategy)
- [DataSource.cacheSyncTiming](DataSource.md#attr-datasourcecachesynctiming)
- [DSRequest.cacheSyncTiming](DSRequest.md#attr-dsrequestcachesynctiming)

**Flags**: IR

---
## Attr: OperationBinding.requiresCompleteRESTResponse

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.requiresCompleteRESTResponse](DataSource.md#attr-datasourcerequirescompleterestresponse) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.methodArguments

### Description
You can explicitly declare the arguments to be passed to [OperationBinding.serverMethod](#attr-operationbindingservermethod) using this attribute. This isn't required - in the absence of `methodArguments`, the DMI implementation will still automatically pass a stock set of arguments to your method (see the overview in [ServerObject](../main_2.md#object-serverobject)), but specifying arguments gives you the ability to call pre-existing methods without adding SmartClient-specific code.

The format for specifying `methodArguments` is as a comma separated list of VTL (Velocity Template Language) expressions. See the [VTL Reference](https://velocity.apache.org/engine/devel/vtl-reference.html) and [Velocity User Guide](https://velocity.apache.org/engine/2.3/user-guide.html) for an overview of how to use VTL.

The Velocity context is pre-populated with the following variables - you can pass these verbatim as arguments, or call methods on these objects and pass the resulting values:

*   dsRequest: instance of the current DSRequest
*   request: the current HttpServletRequest
*   response: the current HttpServletResponse
*   rpcManager: the instance of RPCManager for this request
*   dataSource: a DataSource instance for this request

So, for example, if you had a method signature like the following:

`public DSResponse fetch(SupplyItem criteria, long startRow, long endRow)`

You can invoke it by specifying `methodArguments` as follows:

`methodArguments="$dsRequest.criteria, $dsRequest.startRow, $dsRequest.endRow"`

Without `methodArguments`, there would be no way for you to specify `startRow/endRow` as arguments. You could, of course, simply declare the method to take a `DSRequest` object and call `getStartRow()/getEndRow()` in the body of the method.

### See Also

- [ServerObject](../main_2.md#object-serverobject)

**Flags**: IR

---
## Attr: OperationBinding.requires

### Description
Indicates that the specified [VelocityExpression](../main_2.md#type-velocityexpression) must be true for a user to access this operationBinding.

As with [OperationBinding.requiresRole](#attr-operationbindingrequiresrole), if there an operationBinding that is the default operationBinding for the operationType, its `requires` expression is assumed to apply to all other operationBindings of the same type unless they explicitly set `requires=""`

[DataSource.requires](DataSource.md#attr-datasourcerequires), if specified, applies before `operationBinding.requires` is evaluated. In this case, both `requires` expressions must be true for the request to be accepted.

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: OperationBinding.customCriteriaFields

### Description
Indicates that the listed fields should be included in the default [whereClause](#attr-operationbindingwhereclause) generated for this operationBinding, even if they are marked [customSQL="true"](DataSourceField.md#attr-datasourcefieldcustomsql).

You can specify this property as a comma-separated list (eg, "foo, bar, baz") or by just repeating the `<customCriteriaFields>` tag multiple times with one field each.

This property is only applicable to DataSources of ["sql"](DataSource.md#attr-datasourceservertype).

### Groups

- customQuerying

### See Also

- [OperationBinding.customFields](#attr-operationbindingcustomfields)
- [OperationBinding.customValueFields](#attr-operationbindingcustomvaluefields)
- [OperationBinding.excludeCriteriaFields](#attr-operationbindingexcludecriteriafields)

**Flags**: IR

---
## Attr: OperationBinding.csvDelimiter

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.csvDelimiter](DataSource.md#attr-datasourcecsvdelimiter) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.excludeCriteriaFields

### Description
Indicates that the listed fields should be excluded from the default [whereClause](#attr-operationbindingwhereclause) generated for this operationBinding.

This enables you to use these fields in a [custom query](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview) while still allowing the $defaultWhereClause to be generated for all other fields. For example, you might take a particular field and apply it in the WHERE clause of a subquery.

You can specify this property as a comma-separated list (eg, "foo, bar, baz") or by just repeating the `<customCriteriaFields>` tag multiple times with one field each. Note that if a field is included in both excludeCriteriaFields and [customCriteriaFields](#attr-operationbindingcustomcriteriafields), customCriteriaFields wins.

This property is only applicable to DataSources of ["sql"](DataSource.md#attr-datasourceservertype).

### Groups

- customQuerying

### See Also

- [OperationBinding.customCriteriaFields](#attr-operationbindingcustomcriteriafields)

**Flags**: IR

---
## Attr: OperationBinding.xmlNamespaces

### Description
Optional object declaring namespace prefixes for use in [OperationBinding.recordXPath](#attr-operationbindingrecordxpath) and [DataSourceField.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) XPath expressions.

`xmlNamespaces` should be specified as a mapping from namespace prefix to namespace URI, for example:

```
    xmlNamespaces : {
        az : "http://webservices.amazon.com/AWSECommerceService/2005-03-23"
    }
 
```
By default, all namespaces declared on the document element (outermost element of the response) are made available with the prefix used in the document itself.

Then, for non-WSDL-described XML results, if there is a default namespace on the document element, it is made available with the special prefix "default".

For results of WSDL-described operations, the prefix "service" means the service namespace, that is, the "targetNamespace" on the `<definitions>` element from the WSDL file. The prefix "schema" means the namespace of the outermost element in the output message for the current operation. "default" will be the schema namespace if there is one, otherwise the service namespace.

For basic information on XML Namespaces and their use in XPath, try the following search: [http://www.google.com/search?q=XPath+xml+namespaces](http://www.google.com/search?q=XPath+xml+namespaces)

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.httpMethod

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.httpMethod](DataSource.md#attr-datasourcehttpmethod) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.useForCacheSync

### Description
For an operationBinding of [operationType](#attr-operationbindingoperationtype) "fetch" which specifies no [operationId](#attr-operationbindingoperationid), this property determines whether the operationBinding should be used for cache synchronization purposes (ie, to retrieve the record most recently added or changed). This property has no effect on an operationBinding that specifies an operationId - see [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation).

In order to work correctly with SmartClient's cache synchronization system, an operationBinding marked useForCacheSync should have the following properties:

*   Able to complete its retrieval using no context other than the values of the primary key fields declared in the dataSource (these will be provided in the $criteria object passed to the operation)
*   Returns the entire record, including any values that may require joins to other tables or other complexities

This property is not applicable to the built-in [Hibernate](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) and [JPA](../kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa) DataSources.

Please also read the overview article on [cacheSynchronization](../kb_topics/cacheSynchronization.md#kb-topic-automatic-cache-synchronization) for full details of all the cache sync options

### Groups

- cacheSynchronization

### See Also

- [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation)

**Flags**: IR

---
## Attr: OperationBinding.creatorOverrides

### Description
Indicates that field-level declarative security rules are waived for rows that were created by the current user, as described in the discussion of [dataSource.creatorOverrides](DataSource.md#attr-datasourcecreatoroverrides). This setting overrides `dataSource.creatorOverrides`, for this operation only.

### Groups

- fieldLevelAuth
- declarativeSecurity

### See Also

- [DataSourceField.editRequires](DataSourceField.md#attr-datasourcefieldeditrequires)
- [DataSourceField.viewRequires](DataSourceField.md#attr-datasourcefieldviewrequires)
- [DataSource.creatorOverrides](DataSource.md#attr-datasourcecreatoroverrides)

**Flags**: IR

---
## Attr: OperationBinding.sqlSuffix

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For operations on DataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, some text to add right at the end of the query generated for this specific operation, after all other text. This can be plain text or a [Velocity template](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables). Like [OperationBinding.sqlPrefix](#attr-operationbindingsqlprefix), this property allows for non-standard SQL extensions that may be required to obtain some special, database-specific behavior. For example, Progress OpenEdge database can be given hints like `"WITH (NOLOCK)"`, that must appear after all other text.

This property is ignored for non-SQL dataSources

`sqlSuffix` can also be specified at the [DataSource level](DataSource.md#attr-datasourcesqlprefix); any such value acts as a default for the dataSource, and will be overridden by an operationBinding-level setting

You can alternatively provide SQL suffix text programmatically, by overriding `getSQLSuffix()` in a [custom DataSource implementation](DataSource.md#attr-datasourceserverconstructor)

### Groups

- customQuerying

**Flags**: IR

---
## Attr: OperationBinding.transformRequestScript

### Description
Scriptlet to be executed prior to the DataSource operation which is configured by this operationBinding. See [DataSource.transformRequestScript](DataSource.md#attr-datasourcetransformrequestscript) for further details.

Note, unlike many OperationBinding-level properties, a `transformRequestScript` at the OperationBinding level does not hide a `transformRequestScript` defined at the DataSource level. Instead, if you define `transformRequestScript` against both the DataSource and the OperationBinding, **both** are run - first the DataSource-level script, then the OperationBinding-level one.

### Groups

- serverScript

**Flags**: IR

---
## Attr: OperationBinding.afterWhereClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke HAVING clause to use when constructing the SQL query to perform this operation. The property should be a valid expression in the syntax of the underlying database. The server will insert the text of this property immediately after the outer "HAVING" token:

```
   select <selectClause>
     from ...
    where ...
 group by <groupClause>
   having <afterWhereClause>
 
```
or after outer "WHERE" token if [OperationBinding.useHavingClause](#attr-operationbindingusehavingclause) was set to `false`:
```
 select *
 from (select <selectClause> from ... where ... group by <groupClause>) work
 where <afterWhereClause>
 
```
Note that care is required when using afterWhereClause to ensure that the selectClause contains all the fields you are filtering by. Failure to do this correctly will result in a runtime SQL error.

This property is only applicable to operationBindings of [operationType](#attr-operationbindingoperationtype) "fetch".

It fully supports [SQL Templating](#attr-operationbindingcustomsql) feature, for example:

```
 <afterWhereClause>$defaultAfterWhereClause AND field_name = value </afterWhereClause>
 
```
See the documentation for [SQL Templating](#attr-operationbindingcustomsql) for more details and [Server Summaries](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for how criteria is applied to aggregated fields. Also, see "Filtered summaries", "Aggregation & Custom SQL" and "Custom Aggregation Query" [Server Summaries samples](https://www.smartclient.com/smartclient-latest/showcase/?id=serverSummariesFolder) in Smartclient Showcase.

#### "Standalone" afterWhereClause usage

Normally afterWhereClause is used in the context of the Server Summaries feature, but it is possible to use it in non aggregated fetches as well. For example:

```
 <DataSource ID="order" serverType="sql" tableName="order">
     <fields>
         <field name="orderID" primaryKey="true" ... />
         ...
     </fields>
     <operationBinding operationType="fetch">
         <tableClause>$defaultTableClause JOIN orderItem oi on order.orderID = oi.orderID</tableClause>
         <groupClause>$defaultSelectClause</groupClause>
         <afterWhereClause>count(oi.orderID) > 1 AND sum(oi.unitPrice * oi.quantity) > 100</afterWhereClause>
     <operationBinding>
 </DataSource>
 
```
There's no builtin aggregation used in `operationBinding` above, but the regular "fetch" is limited by requiring every order to have multiple order items with amount greater than 100.

### Groups

- customQuerying
- serverSummaries

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [OperationBinding.selectClause](#attr-operationbindingselectclause)
- [OperationBinding.useHavingClause](#attr-operationbindingusehavingclause)
- [OperationBinding.applyCriteriaBeforeAggregation](#attr-operationbindingapplycriteriabeforeaggregation)
- [DSRequest.afterCriteria](DSRequest.md#attr-dsrequestaftercriteria)

**Flags**: IR

---
## Attr: OperationBinding.suppressAutoMappings

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.suppressAutoMappings](DataSource.md#attr-datasourcesuppressautomappings) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.customFields

### Description
Indicates that the listed fields should be included in the default [selectClause](#attr-operationbindingselectclause) and [whereClause](#attr-operationbindingwhereclause) generated for this operationBinding, even if they are marked [customSQL](DataSourceField.md#attr-datasourcefieldcustomsql)="true".

If you need to apply different sets of overrides for the `selectClause` and the `whereClause`, use [customValueFields](#attr-operationbindingcustomvaluefields) and/or [customCriteriaFields](#attr-operationbindingcustomcriteriafields) instead. If you specify both `customFields` and `customCriteriaFields` or `customValueFields`, the more specific variant wins. If you specify both `customFields` and [excludeCriteriaFields](#attr-operationbindingexcludecriteriafields), `customFields` wins (this is another use case when you may wish to use `customValueFields` instead)

You can specify this property as a comma-separated list (eg, "foo, bar, baz") or by just repeating the `<customFields>` tag multiple times with one field each.

This property is only applicable to DataSources of ["sql"](DataSource.md#attr-datasourceservertype).

### Groups

- customQuerying

### See Also

- [OperationBinding.customValueFields](#attr-operationbindingcustomvaluefields)
- [OperationBinding.customCriteriaFields](#attr-operationbindingcustomcriteriafields)
- [OperationBinding.excludeCriteriaFields](#attr-operationbindingexcludecriteriafields)

**Flags**: IR

---
## Attr: OperationBinding.multiInsertBatchSize

### Description
For "add" operations on dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, this property sets the multi-insert batch size for this [operation](#class-operationbinding). Only has an effect if the [add request](DataSource.md#method-datasourceadddata) specifies a list of records as the data, and only if [multiInsertStrategy](#attr-operationbindingmultiinsertstrategy) is set to "multipleValues" either globally or at the [DSRequest](../main_2.md#object-dsrequest), [OperationBinding](#class-operationbinding), or [DataSource](DataSource.md#class-datasource) level.

Note that this setting overrides the equivalent [dataSource setting](DataSource.md#attr-datasourcemultiinsertbatchsize), and can in turn be overridden at the [DSRequest level](DSRequest.md#attr-dsrequestmultiinsertbatchsize)

### See Also

- [OperationBinding.multiInsertStrategy](#attr-operationbindingmultiinsertstrategy)
- [OperationBinding.multiInsertNonMatchingStrategy](#attr-operationbindingmultiinsertnonmatchingstrategy)

**Flags**: IRW

---
## Attr: OperationBinding.params

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.params](DataSource.md#attr-datasourceparams) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.exportFields

### Description
The list of field-names to export. If provided, the field-list in the exported output is limited and sorted as per the list.

If exportFields is not provided, the exported output includes all visible fields from the DataSource (field.hidden=false), sorted in the order they're defined.

**Flags**: IR

---
## Attr: OperationBinding.responseDataSchema

### Description
Optional schema describing how to extract DataSource records from the XML elements selected.

Once a set of XML elements have been selected via `recordXPath` or `recordName`, those elements are normally transformed to JavaScript objects using the `fields` of the DataSource that owns the operationBinding. A `responseDataSchema` can be specified instead if the XML differs in some way between different DataSource operations, such that different values for [field.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) may be necessary to extract the same DataSource record from slightly different XML structures.

### Groups

- clientDataIntegration

**Flags**: IRA

---
## Attr: OperationBinding.forceSort

### Description
For DataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, indicates whether we should automatically add a sort field for [paged fetches](ResultSet.md#attr-resultsetfetchmode). Only applies to ["fetch" operations](#attr-operationbindingoperationtype). If left unset, this property defaults first to the [dataSource-level setting](DataSource.md#attr-datasourceforcesort), and then to one of the global values described in the [defaultSortField](DataSource.md#attr-datasourcedefaultsortfield) documentation.

Note, the ability to set this property per-operation is only provided to allow for complete configurability in unusual cases. See the `defaultSortField` docs for details of why use of this property should be considered a red flag.

### Groups

- serverDataIntegration

**Flags**: IRA

---
## Attr: OperationBinding.allowAdvancedCriteria

### Description
This property indicates whether this operation supports AdvancedCriteria. This setting overrides [DataSource.allowAdvancedCriteria](DataSource.md#attr-datasourceallowadvancedcriteria) for this operation only. See [DataSource.supportsAdvancedCriteria](DataSource.md#method-datasourcesupportsadvancedcriteria) for further information.

**NOTE:** If you specify this property in a DataSource descriptor (`.ds.xml` file), it is enforced on the server. This means that if you run a request containing AdvancedCriteria against an OperationBinding that advertises itself as `allowAdvancedCriteria:false`, it will be rejected.

### See Also

- [DataSource.allowAdvancedCriteria](DataSource.md#attr-datasourceallowadvancedcriteria)

**Flags**: IRWA

---
## Attr: OperationBinding.invalidateCache

### Description
If set, every invocation of this operationBinding will invalidate the local cache, forcing a server visit to refresh the data.

**Flags**: IR

---
## Attr: OperationBinding.cacheSyncOperation

### Description
For an operationBinding of [operationType](#attr-operationbindingoperationtype) "add" or "update", this property is the [operationId](#attr-operationbindingoperationid) of a "fetch" operationBinding to use for cache synchronization purposes (ie, to fetch the row most recently added or changed). This property, along with [useForCacheSync](#attr-operationbindinguseforcachesync) and [canSyncCache](#attr-operationbindingcansynccache) is provided so that you can use custom database operations without sacrificing the benefits of SmartClient's automatic cache synchronization.

This property is not applicable to the built-in [Hibernate](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) and [JPA](../kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa) DataSources.

Please also read the overview article on [cacheSynchronization](../kb_topics/cacheSynchronization.md#kb-topic-automatic-cache-synchronization) for full details of all the cache sync options

### Groups

- cacheSynchronization

### See Also

- [OperationBinding.useForCacheSync](#attr-operationbindinguseforcachesync)
- [OperationBinding.canSyncCache](#attr-operationbindingcansynccache)

**Flags**: IR

---
## Attr: OperationBinding.requiresRole

### Description
Comma-separated list of user roles that are allowed to invoke the operation described by this operationBinding. If the current user has any of the roles listed, they can invoke the operation. Also note that `authentication.superuserRole` can be specified in the [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) file. If set this denotes a "super user" role - any user with that role will have access to all operations, regardless of the "requiresRole" settings for the operation.

Whether the current user has a given role is determined by calling the standard Java servlets method `httpServletRequest.isUserInRole()`, hence works with both simple J2EE security (realms and form-based authentication) and JAAS (Java Authentication & Authorization Service).

If you wish to use a role-based security scheme that does not make use of the servlet API's standards, SmartClient Server also implements the `setAuthenticated` and `setUserRoles` methods on `RPCManager`. You can use this API to tell SmartClient that all the requests in the queue currently being processed are associated with a user who has the roles you supply; in this case, SmartClient will not attempt to resolve the user's roles via `httpServletRequest.isUserInRole()`. When taking this approach, the `rpcManager.setUserRoles()` method should be called on the server for each transaction received from the client. We recommend doing this by overriding the special IDACall servlet and checking server side state to determine the current user's roles, calling the API, and then calling `handleDSRequest()` or `handleRPCRequest()` directly to handle the request(s) passed in.  
Here's an example of this approach which assumes the current user's roles has been set directly on the HttpSession object as a comma-separated-string attribute "roles":

```
  public class SecureIDACall extends IDACall {
		
      public void processRequest(HttpServletRequest request,
              HttpServletResponse response)
       throws ServletException, IOException
      {
          HttpSession session = request.getSession();
          Object roles = session == null ? null : session.getAttribute("roles");
 
          if (roles != null) {
              try {
                  RequestContext context = RequestContext.instance(this, request, response);   
                  RPCManager rpc = new RPCManager(request, response);
                  rpc.setAuthenticated(true);
                  rpc.setUserRoles((String) roles); 
                  
                  // call processRPCTransaction() to iterate through all RPCRequests and
                  // DSRequests and execute them
                  processRPCTransaction(rpc, context);
 
              } catch (Throwable e) {
                  handleError(response, e);
              }
          } else {
              super.processRequest(request, response);
          } 
      }
  }
 
```

If there is an operationBinding declared for a given operationType which does not have an [OperationBinding.operationId](#attr-operationbindingoperationid), that is, it is the default operationBinding for the type, then any other operationBinding of the same type is assumed to have the same setting for `requiresRole` as the default operationBinding for the operationType. For example, given these declarations:

```
     <operationBinding operationType="fetch" requiresRole="manager">
           ... settings ...
      </operationBinding>
     <operationBinding operationType="fetch" operationId="fetchWithExtraFields">
           ... settings ...
      </operationBinding>
 
```
The second operationBinding requires the "manager" role even though there is no explicit `requiresRole` declaration. To prevent the "manager" role being required by the second operationBinding, add `requireRole=""`.

Note that if [DataSource.requiresRole](DataSource.md#attr-datasourcerequiresrole) is set, all operations on the DataSource require the roles set for the DataSource as a whole, even if they declare individual `requiresRole` attributes.

This property is valid only for a server-side DataSource when using the SmartClient Server.

#### Special rules for cache sync

After successfull "add" or "update" operation cache sync request is performed, which is using "fetch" operation of the same datasource. It may happen that user is allowed to add records, but is not allowed to fetch them, for example:

```
     <operationBinding operationType="fetch" requiresRole="admin">
           ... settings ...
     </operationBinding>
     <operationBinding operationType="add">
           ... settings ...
     </operationBinding>
 
```
User without "admin" role will be able to successfully add record, but the cache sync operation will fail due to security violation. In this case the record will be saved to database, but the added record will not be fetched from database, instead just [old values](DSRequest.md#attr-dsrequestoldvalues) overlaid with submitted values will be returned. So, any changes made to the new record during request execution, including generated values for primary key fields of "sequence" type, will not be returned to the client.

However, if "add" or "update" operation explicitly declares [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation), cache sync request will be executed even if the user does not meet the security checks for the operationBinding. Note that field-level security still will be respected and disallowed fields will be excluded from returned data.

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: OperationBinding.requestTemplate

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of the [DataSource.requestTemplate](DataSource.md#attr-datasourcerequesttemplate) - see that property's documentation for details

### Groups

- serverRestConnector

### See Also

- [DataSource.requestTemplate](DataSource.md#attr-datasourcerequesttemplate)
- [OperationBinding.transformRequestScript](#attr-operationbindingtransformrequestscript)
- [OperationBinding.responseTemplate](#attr-operationbindingresponsetemplate)

**Flags**: IR

---
## Attr: OperationBinding.exportFilename

### Description
The name of the file to save the exported data into.

**Flags**: IR

---
## Attr: OperationBinding.useFlatFields

### Description
Setting `useFlatFields` on an operationBinding is equivalent to setting [DSRequest.useFlatFields](DSRequest.md#attr-dsrequestuseflatfields) on all DataSource requests with the same [OperationBinding.operationType](#attr-operationbindingoperationtype) as this `operationBinding`.

Typical usage is to combine operationBinding.useFlatFields with [searchForm.useFlatFields](DataBoundComponent.md#attr-databoundcomponentuseflatfields), with the [SearchForm](SearchForm.md#class-searchform) bound to the [input message](WebService.md#method-webservicegetinputds) of the web service operation set as [OperationBinding.wsOperation](#attr-operationbindingwsoperation). This allows gratuitous nesting to be consistently bypassed in both the user presentation and in the actual XML messaging.

Note that `useFlatFields` is not generally recommended for use with input messages where multiple simple type fields exist with the same name, however if used in this way, the first field to use a given name wins. "first" means the first field encountered in a depth first search. "wins" means only the first field will be available in data binding, and only the first field will be populated in the generated XML message.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.cacheSyncStrategy

### Description
The [cacheSyncStrategy](../main_2.md#type-cachesyncstrategy) to use for this operation. Overrides any [dataSource-level cacheSyncStrategy](DataSource.md#attr-datasourcecachesyncstrategy)

### Groups

- cacheSynchronization

### See Also

- [DataSource.cacheSyncStrategy](DataSource.md#attr-datasourcecachesyncstrategy)
- [DSRequest.cacheSyncStrategy](DSRequest.md#attr-dsrequestcachesyncstrategy)

**Flags**: IR

---
## Attr: OperationBinding.xmlTag

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.xmlTag](DataSource.md#attr-datasourcexmltag) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.canSyncCache

### Description
For an operation of type "add" or "update", a SQLDataSource will normally obtain data to return to the client by performing the "cacheSyncOperation": a SELECT statement that retrieves the modified record by primary key. This accommodates sequence columns, columns with default values, database triggers and other database features that may modify data after insertion or update.

Certain major SQL customizations can prevent the SQLDataSource from authoritatively determining the primary key used in the SQL statement, such that re-selecting the saved record may fail. By default, when `canSyncCache` has not been explicitly set, in the following cases it is assumed that the normal cacheSyncOperation cannot be used:

*   `<customSQL>` has been used to define an entirely custom query
*   a custom `<whereClause>` has been defined for an "update" or "remove" operation
*   a custom `<valuesClause>` has been defined for an "add" operation

If any of these cases apply or if `canSyncCache` has been set false, the server will skip the cacheSyncOperation and return a DSResponse where [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache) has been set to true to notify client-side components that they may need to refresh their entire cache.

Alternatively, if the default re-selection behavior will not work but a customized SQL query would work, you can define that SQL operation as another operationBinding and use [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation) to declare that it should be used. Setting `cacheSyncOperation` implicitly sets `canCacheSync` to true.

Note, setting this property to false inhibits cache synchronization for most DataSource types - it is not specific to SQL DataSources. However, it is not applicable to the built-in [Hibernate](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) and [JPA](../kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa) DataSources. See the [cache sync overview](../kb_topics/cacheSynchronization.md#kb-topic-automatic-cache-synchronization) for further details.

### Groups

- cacheSynchronization

### See Also

- [OperationBinding.useForCacheSync](#attr-operationbindinguseforcachesync)
- [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation)

**Flags**: IR

---
## Attr: OperationBinding.script

### Description
Scriptlet to be executed prior to the DataSource operation which is configured by this operationBinding. This setting overrides any [script specified at the DataSource level](DataSource.md#attr-datasourcescript) for this operation.

Scriptlets are used similarly to DMIs configured via [OperationBinding.serverObject](#attr-operationbindingserverobject) - they can add business logic by modifying the DSRequest before it's executed, modifying the default DSResponse, or taking other, unrelated actions.

Scriptlets are used similarly to DMIs configured via [DataSource.serverObject](DataSource.md#attr-datasourceserverobject) or [OperationBinding.serverObject](#attr-operationbindingserverobject) - they can add business logic by modifying the DSRequest before it's executed, modifying the default DSResponse, or taking other, unrelated actions.

For example:

```
    <operationBindings>
       <operationBinding operationType="add">
           <script language="groovy">
              ... Groovy code ...
           </script>
       </operationBinding>
    </operationBindings>
 
```

Scriptlets can be written in any language supported by the "JSR 223" standard, including Java itself. See the [DMI Script Overview](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) for rules on how to return data, add additional imports, and other settings.

The following variables are available for DMI scriptlets:

*   _dataSource_: the current DataSource
*   _dsRequest_: the current DSRequest
*   _criteria_: shortcut to DSRequest.getCriteria() (a Map)
*   _values_: shortcut to DSRequest.getValues() (a Map)
*   _oldValues_: shortcut to DSRequest.getOldValues() (a Map)
*   _sqlConnection_: **SQLDataSource only**: the current SQLConnection object. If using [automatic transactions](DataSource.md#attr-datasourceautojointransactions) are enabled, this SQLConnection is in the context of the current transaction.
*   _beanFactory_: the spring BeanFactory (when applicable)
*   _cdiBeanManager_: the CDI BeanManager (when applicable)

Scriptlets also have access to a set of contextual variables related to the Servlets API, as follows:

*   _servletRequest_: the current ServletRequest
*   _session_: the current HttpSession
*   _rpcManager_: the current RPCManager
*   _servletResponse_: the current ServletResponse **(advanced use only)**
*   _servletContext_: the current ServletContext**(advanced use only)**

As with DMI in general, be aware that if you write scriptlets that depend upon these variables, you preclude your DataSource from being used in the widest possible variety of circumstances. For example, adding a scriptlet that relies on the `HttpSession` prevents your DataSource from being used in a command-line process.

_Note that if a dataSource configuration has both a ``<script>`` block and a specified [serverObject](#attr-operationbindingserverobject) for some operation, the script block will be executed, and the serverObject ignored._

**Flags**: IR

---
## Attr: OperationBinding.autoJoinTransactions

### Description
If true, causes requests against this operation to automatically start or join a transaction. if false, causes requests against this operation to be committed individually. If null, falls back to [DataSource.autoJoinTransactions](DataSource.md#attr-datasourceautojointransactions).

See [DataSource.autoJoinTransactions](DataSource.md#attr-datasourceautojointransactions) for further details of SmartClient's automatic transaction control.

**Flags**: IR

---
## Attr: OperationBinding.progressiveLoading

### Description
Sets [progressive loading mode](DataSource.md#attr-datasourceprogressiveloading) for this particular operation, overriding the DataSource-level setting. Note that this setting applies only to fetch operations - it has no effect if specified on any other kind of operation.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)

**Flags**: IRW

---
## Attr: OperationBinding.useSpringTransaction

### Description
Sets or clears the `useSpringTransaction` flag for this specific operation.

See [DataSource.useSpringTransaction](DataSource.md#attr-datasourceusespringtransaction) for details of the Spring transaction integration feature

**Flags**: IR

---
## Attr: OperationBinding.valuesClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke set of values to add or update, for use when constructing the SQL query to perform this operation. The property should be one of the following, depending on the [operationType](#attr-operationbindingoperationtype):

For "add" operations, the syntax that would be valid for an INSERT INTO query: a comma-separated list of column names enclosed in parentheses, followed by a comma-separated list of new values, enclosed in parentheses and preceded by the token "VALUES". For example:

``<valuesClause>`(name, age) VALUES("Jane Doe", 48)`</valuesClause>``

For "update" operations, the syntax that would be valid for an UPDATE query: a comma-separated list of expressions equating a column name to its new value. For example:

``<valuesClause>`name="Jane Doe", age=48`</valuesClause>``

You may find the SmartClient-provided **$values** variable of particular use with this property.

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.applySqlPrefixToRowCount

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For operations on DataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, if [OperationBinding.sqlPrefix](#attr-operationbindingsqlprefix) is specified at either operation or DataSource level, should that prefix also be applied to the rowcount query, if one is run? This property is true by default, meaning we will apply the prefix to both rowcount and main queries

This property is ignored for non-SQL dataSources

This property can also be specified at the [DataSource level](DataSource.md#attr-datasourceapplysqlprefixtorowcount); any such value acts as a default for the dataSource, and will be overridden by an operationBinding-level setting

### Groups

- customQuerying

### See Also

- [OperationBinding.applySqlSuffixToRowCount](#attr-operationbindingapplysqlsuffixtorowcount)

**Flags**: IR

---
## Attr: OperationBinding.skipRowCount

### Description
A SQLDataSource will normally issue two queries for a "fetch" operation when paging is enabled: one to determine the total rows available (the "row count query"), and one to fetch the specific range of rows requested.

Setting skipRowCount="true" will avoid the "row count query", but as a consequence [DSResponse.totalRows](DSResponse.md#attr-dsresponsetotalrows) will be set to match the requested [DSRequest.endRow](DSRequest.md#attr-dsrequestendrow) since the totalRows is unknown. You can avoid this by using a [paging strategy](#attr-operationbindingsqlpaging) of "jdbcScroll" or "dropAtServer", but be aware that these paging strategies can introduce significant delays when used with potentially large datasets (in fact, "dropAtServer" is almost guaranteed to do so if used with datasets of more than 1000 or so rows)

As an alternative, consider enabling [progressive loading](DataSource.md#attr-datasourceprogressiveloading), which avoids doing a query for row counts, but will still allow the user to load more results using the scrollbar if viewing results in a ListGrid.

**Flags**: IR

---
## Attr: OperationBinding.whereClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke WHERE clause to use when constructing the SQL query to perform this operation. The property should be a valid expression in the syntax of the underlying database. The server will insert the text of this property immediately after the "WHERE" token.

You may find the SmartClient-provided **$criteria** variable of particular use with this property.

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.operationType

### Description
Which operationType this operationBinding is for. This property is only settable on an operationBinding, not a DataSource as a whole.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.orderClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke ORDER BY clause to use when constructing the SQL query to perform this operation. The property should be a comma-separated list of column names and/or expressions, forming a valid ORDER BY clause in the syntax of the underlying database. The server will insert the text of this property immediately after the "ORDER BY" token.

This property is only applicable to operationBindings of [operationType](#attr-operationbindingoperationtype) "fetch".

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.wrapInList

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.wrapInList](DataSource.md#attr-datasourcewrapinlist) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.unionFields

### Description
Only applicable to "union" dataSources, this is a comma-separated list of the names of the dataSource fields that make up the union. This property overrides the DataSource-level setting of the same name.

Note, this property can only be used to narrow the list of fields in the union, not to widen it. In other words, only fields that are included at the dataSource level - either by specifying an explicit [unionFields](DataSource.md#attr-datasourceunionfields) property or by automatically deriving a list of fields according to the [DataSource.defaultUnionFieldsStrategy](DataSource.md#attr-datasourcedefaultunionfieldsstrategy) - can be named in the operationBinding-level `unionFields` declaration.

### Groups

- unionDataSource

### See Also

- [DataSource.unionFields](DataSource.md#attr-datasourceunionfields)

**Flags**: IR

---
## Attr: OperationBinding.useSubselectForRowCount

### Description
Whether to use the subselect technique (see [DataSource.useSubselectForRowCount](DataSource.md#attr-datasourceusesubselectforrowcount) for details) to derive a rowcount query for this operation. If this property is not set, we fall back to the `useSubselectForRowCount` setting on the DataSource, and the defaults described in the documentation for that property.

### See Also

- [DataSource.useSubselectForRowCount](DataSource.md#attr-datasourceusesubselectforrowcount)
- [OperationBinding.customSQL](#attr-operationbindingcustomsql)

**Flags**: IRW

---
## Attr: OperationBinding.includeAnsiJoinsInTableClause

### Description
This setting makes difference if [ANSI-style joins](DataSource.md#attr-datasourceuseansijoins) are in use. If true, causes ansi joins to be included in [$defaultTableClause](../main.md#type-defaultqueryclause), otherwise ansi joins will be put into separate [$defaultAnsiJoinClause](../main.md#type-defaultqueryclause).

If omitted, system-wide `sql.includeAnsiJoinsInTableClause` setting from `server.properties` will be used. If it is missing as well, `false` is the default.

### See Also

- [DataSource.useAnsiJoins](DataSource.md#attr-datasourceuseansijoins)
- [OperationBinding.ansiJoinClause](#attr-operationbindingansijoinclause)

**Flags**: IR

---
## Attr: OperationBinding.sqlType

### Description
For dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" and "hibernate" only, this property determines whether "custom" operations have their custom SQL or HQL sent to the underlying database via a JDBC `executeQuery()` or a JDBC `executeUpdate()`. The default value of null means the same as "query", so you only need to use this property when your custom SQL or HQL updates data.

### Groups

- customQuerying

**Flags**: IR

---
## Attr: OperationBinding.multiInsertStrategy

### Description
For "add" operations on dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, this property sets the multi-insert strategy for this [operation](#class-operationbinding). Only has an effect if the [add request](DataSource.md#method-datasourceadddata) specifies a list of records as the data.

Note that this setting overrides the equivalent [dataSource setting](DataSource.md#attr-datasourcemultiinsertstrategy), and can in turn be overridden at the [DSRequest level](DSRequest.md#attr-dsrequestmultiinsertstrategy)

### See Also

- [OperationBinding.multiInsertBatchSize](#attr-operationbindingmultiinsertbatchsize)
- [OperationBinding.multiInsertNonMatchingStrategy](#attr-operationbindingmultiinsertnonmatchingstrategy)

**Flags**: IRW

---
## Attr: OperationBinding.csvQuoteCharacter

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.csvQuoteCharacter](DataSource.md#attr-datasourcecsvquotecharacter) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.isDDL

### Description
Only applicable to "sql" dataSources. This property should be set to `true` if your operation runs _Data Definition Language_ (DDL) statements rather than _Data Manipulation Language_ (DML) statements. DDL statements are concerned with creating, altering and dropping database objects, rather than fetching and updating data. Some examples of DDL statements:
```
    CREATE VIEW myView ...
    ALTER TABLE myTable DROP CONSTRAINT PK_myTable
    DROP DATABASE xyz
    TRUNCATE TABLE myTable
 
```
When `isDDL` is true, we switch off certain JDBC flags to inhibit the return of generated key information. This generated key information is very important in supporting SmartClient's automatic cache-synchronization features, but it is never needed for DDL statements. In fact, the concept of generated keys makes no sense in the context of DDL, and asking for this information anyway causes broken behavior in some cases, with some databases (PostgreSQL and Microsoft SQL Server are the two products known to exhibit problems at the time of writing, but there may be others)

The default value of `null` is equivalent to `false`, and means that this is an ordinary DML (data fetch or update) operation.

**Flags**: IR

---
## Attr: OperationBinding.transformMultipleFields

### Description
If set to "false", transformation of values for [multiple:true](DataSourceField.md#attr-datasourcefieldmultiple) fields, normally controlled by [DataSourceField.multipleStorage](DataSourceField.md#attr-datasourcefieldmultiplestorage), is instead disabled for this OperationBinding.

### Groups

- multipleField

**Flags**: IR

---
## Attr: OperationBinding.skipAudit

### Description
Setting `skipAudit` to `true` indicates that [auditing](DataSource.md#attr-datasourceaudit) must be skipped for this operationBinding.

Note, that this setting can be overridden by server-side API `DSRequest.setSkipAudit()`.

**Flags**: IR

---
## Attr: OperationBinding.beanClassName

### Description
A per-operationBinding setting for beanClassName, otherwise also settable at the top-level DataSource configuration.

### Groups

- clientDataIntegration

### See Also

- [DataSource.beanClassName](DataSource.md#attr-datasourcebeanclassname)

**Flags**: IR

---
## Attr: OperationBinding.serverMethod

### Description
The name of the method to invoke on the [ServerObject](../main_2.md#object-serverobject) for this operationBinding.

**NOTE:** If you have a [DataSource-level ServerObject](DataSource.md#attr-datasourceserverobject) and wish to override this operation so that it simply calls a different method on the same server object, it is sufficient to specify just this property on the operationBinding: there is no need to redefine the serverObject at the operationBinding level.

**Flags**: IR

---
## Attr: OperationBinding.namedQuery

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "jpa" or "hibernate", this property can be specified on an operationBinding to indicate that the server should execute a named query which has already been defined on an entity.

```
    @Entity
    @Table (name="Countries")
    @NamedQuery(name = "Country.withPopulationLessThan", query = "SELECT country FROM Country country WHERE country.population < :population")
    public class Country { ... }
 
```
```
    <operationBindings>
        <operationBinding operationType="custom" operationId="withPopulationLessThan" namedQuery="Country.withPopulationLessThan"/>
    </operationBindings>
```

Substitution values can be used in order to build more dynamic named queries. When calling [DataSource.performCustomOperation](DataSource.md#method-datasourceperformcustomoperation) the values are passed in using the data argument.

**Note** that value substitution for named queries is slightly different to other custom queries. Because of the way the persistence API works the JQL query written in the @NamedQuery annotation can only contain basic parameter names such as "population". Therefore the value substitution becomes a simple name based mapping.

#### Examples
**Using Simple Criteria**  
  
An example using a simple criteria for the above defined Country entity. In this case the named query parameter ":population" will be swapped out for the value of the criteria objects "population" field.
```
    var criteria = {
        population: 596000
    };

    countryDataSource.performCustomOperation("withPopulationLessThan", criteria);
 
```

**Using Advanced Criteria**  
  
If an advanced criteria is detected, access to all "fieldName" variables and their values will be provided but still using simple name based mapping. In the below case only the deep-first occurrence of the "population" fieldName will available. The operator is effectively ignored.

```
    var criteria = {
        _constructor: "AdvancedCriteria",
        operator:"or",
        criteria:[
            {
                fieldName:"population",
                operator:"lessThan",
                value: 12000
            },
            {
                fieldName:"name",
                operator:"equals",
                value: "Sweden"
            },
            {
                _constructor: "AdvancedCriteria",
                operator:"and",
                criteria:[
                    {
                        fieldName:"population",
                        operator:"lessThan",
                        value: 0
                    }
                ]
            }
        ]
    };

    countryDataSource.performCustomOperation("withPopulationLessThan", criteria);
 
```

**Note**  
Using namedQuery affects paging implementation. If you use it, full data set is fetched from JPA and records that aren't in the requested range are dropped at the server side.

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [DataSourceField.customSQL](DataSourceField.md#attr-datasourcefieldcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.applyCriteriaBeforeAggregation

### Description
If set to "true", all criteria for the DSRequest using [serverSummaries](#serversummaries) are applied before aggregation, and the [afterWhereClause](#attr-operationbindingafterwhereclause) is not generated.

This property is only applicable if you are using the SQL DataSource, the other built-in types (Hibernate and JPA/JPA2) always perform filtering before summarization.

**NOTE** this property exists principally for backcompat, as the results of apply criteria before aggregation are usually senseless, and in this mode client-side filtering will not match server-side filtering (since client-side filtering is always post-aggregation), so the ability to filter on those fields would need to be disabled in the UI.

Still, if you have this flag was set to "true" and the "avg" function is being applied to a "price" field, criteria like "price < 5" will eliminate records where price is less than 5 _before_ the average price is calculated. Note that this means that client-side filtering may not work as expected with summarized results: client-side filter criteria are necessarily applied _after_ summary functions have been applied, so may not match the server's behavior. You can set [ResultSet.useClientFiltering](ResultSet.md#attr-resultsetuseclientfiltering) to disable client-side filtering on a grid via [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). Or individual fields can be marked [canFilter:false](ListGridField.md#attr-listgridfieldcanfilter).

Note that using [customQuerying](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview) is an ultimate approach to make all kinds of modifications to the way SQL query is generated and with new _$sql.partialWhere(fieldNames)_, _$sql.whereWithout(fieldNames)_, _$sql.partialHaving(fieldNames)_ and _$sql.havingWithout(fieldNames)_ [Velocity context](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables) APIs you have complete control over the automatically generated criteria.

To apply this setting to a specific DSRequest, use the [DSRequest.applyCriteriaBeforeAggregation](DSRequest.md#attr-dsrequestapplycriteriabeforeaggregation).

### See Also

- [OperationBinding.afterWhereClause](#attr-operationbindingafterwhereclause)
- [DSRequest.applyCriteriaBeforeAggregation](DSRequest.md#attr-dsrequestapplycriteriabeforeaggregation)

**Flags**: IR

---
## Attr: OperationBinding.tableClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke table clause to use when constructing the SQL query to perform this operation. The property should be a comma-separated list of tables and views, and you can use any special language constructs supported by the underlying database. The server will insert the text of this property immediately after the "FROM" token.

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [OperationBinding.includeAnsiJoinsInTableClause](#attr-operationbindingincludeansijoinsintableclause)

**Flags**: IR

---
## Attr: OperationBinding.exportAs

### Description
The format in which the data should be exported. Default is "csv". See [ExportFormat](../main_2.md#type-exportformat) for more information.

**Flags**: IR

---
## Attr: OperationBinding.defaultParams

### Description
HTTP parameters that should be submitted with every DSRequest.

Useful for authenticated services that require a sessionId with every request.

Can be set for all operations of a given DataSource as DataSource.defaultParams.

### Groups

- clientDataIntegration

**Flags**: IRA

---
## Attr: OperationBinding.values

### Description
**Elements of this feature are only available with Power or better licenses.** See [smartclient.com/product](http://smartclient.com/product) for details.

A list of [DSRequestModifier](../main_2.md#object-dsrequestmodifier)s that will be used to modify the values object of each [DSRequest](../main_2.md#object-dsrequest) that uses this operationBinding. See this example: *queuedAdd example*.

Below example of the xml as it should be defined in ds.xml: ``<operationBinding operationType="add">` `<values fieldName="orderID" value="$responseData.last('queuedAdd_order','add').orderID" />` `</operationBinding>``

### Groups

- transactionChaining

### See Also

- [OperationBinding.criteria](#attr-operationbindingcriteria)

**Flags**: IR

---
## Attr: OperationBinding.requestFormat

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), the request format to use for this specific operationBinding. Overriddes any [DataSource-level setting](DataSource.md#attr-datasourcerequestformat). Note, if `requestFormat` is not specified at either the DataSource or OperationBinding level, the request will be rejected.

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.makeKeysAvailable

### Description
For an operation of type "add" or "update", a SQLDataSource will normally obtain data to return to the client by performing the [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation). In certain edge cases this is either not possible or causes problems (such as record locks); in this case, you mark the operation with [OperationBinding.canSyncCache](#attr-operationbindingcansynccache): false to inhibit this automatic behavior. However, this gives you an operation that does not properly cooperate with the client in keeping client-side caches fresh, which in turn leads to an application that must perform more server turnarounds and explicit database fetches.

It is possible that the data needed for cache synchronization could be obtained by application code running in a [DMI](DMI.md#class-dmi) or [server script](../kb_topics/serverScript.md#kb-topic-server-scripting), even if the normal automatic cache synchronization will not work. However, such application code is almost certainly going to need to know the primary key(s) of any newly added record(s).

When `makeKeysAvailable` is true, SmartClient Server will go through the process of obtaining generated keys in accordance with the [SequenceMode](../main.md#type-sequencemode), even if `canSyncCache` is false (note, "in accordance with the `sequenceMode`" implies that we do not attempt to get keys if the `sequenceMode` is "none"). The keys used in the operation (both generated keys, if any, and any keys provided in the operation's criteria or values) will be stored on the `DSResponse` and your server-side DMI or script will have access to them via the server API `dsResponse.getKeys()`. Please see the server-side documentation for that method for further details.

Note, if you are using [SequenceMode](../main.md#type-sequencemode) "jdbcDriver", the keys are available to SmartClient Server at no cost, so `makeKeysAvailable` is always true. If you are using `sequenceMode` "native", a separate native query must be run to obtain the keys. The overhead of this native query is likely to be insignificant, but because it is an extra step that you may not want or need, `makeKeysAvailable` defaults to false in this case. You can override this by adding setting `sql.always.makeKeysAvailable:true` to your `server.properties` file.

This property is only applicable to DataSources of type "sql".

### Groups

- customQuerying

### See Also

- [OperationBinding.canSyncCache](#attr-operationbindingcansynccache)
- [OperationBinding.cacheSyncOperation](#attr-operationbindingcachesyncoperation)

**Flags**: IR

---
## Attr: OperationBinding.guestUserId

### Description
Value to use for the [ownerIdField](#attr-operationbindingowneridfield) if no one has authenticated.

Overrides the same setting at the [DataSource](DataSource.md#attr-datasourceguestuserid) level.

### See Also

- [OperationBinding.ownerIdField](#attr-operationbindingowneridfield)
- [DataSource.guestUserId](DataSource.md#attr-datasourceguestuserid)

**Flags**: IR

---
## Attr: OperationBinding.recordXPath

### Description
For an XML or JSON, JSON or [RestConnector](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector) DataSource, an XPath expression used to retrieve the objects that will become DataSource records.

For example, an "ItemSearch" web service might return a "Results" structure containing metadata along with the set of Items that one might want to display in a grid. An XPath expression like "/Results/Items" could be used to retrieve just the Items, which would then become DataSource records.

For a JSON web service, the `recordXPath` is applied to the returned JSON data via [XMLTools.selectObjects](XMLTools.md#classmethod-xmltoolsselectobjects). Only limited XPath syntax is allowed; see [selectObjects()](XMLTools.md#classmethod-xmltoolsselectobjects) for details.

For processing XML results, see [OperationBinding.xmlNamespaces](#attr-operationbindingxmlnamespaces) for information on the namespaces that are available in this XPath expression. If you are contacting a WSDL web service, note that [OperationBinding.recordName](#attr-operationbindingrecordname) is an alternative way to specify which records should be selected by their tagName or type, and this is usually simpler.

To learn about XPath, try the following search: [http://www.google.com/search?q=xpath+tutorial](http://www.google.com/search?q=xpath+tutorial)

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.allowMultiUpdate

### Description
Ordinarily, "update" and "remove" operations are only allowed for [DataSource](DataSource.md#class-datasource)s that have a [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey), and all primary key values are present in the request. This is because an update of a DataSource with no primary key, or an update request that has missing primary key values, cannot be guaranteed to affect only one record.

Setting this property on an operationBinding circumvents this restriction for that operation only.

**Warning:** Be aware that this is a potentially dangerous setting and should be used with care. With this flag set, you have no guarantee that an update will not change or remove every row in a table.

Note, in the case of doing an update or delete operation with a primary key **_and additional criteria_**, allowMultiUpdate must be set or additional criteria will be dropped and just the primary key fields will be used in criteria.

Also, running `allowMultiUpdate` operations directly from the client is not straightforward because it requires the ability to specify criteria and values separately in the request, which is not currently supported. This can be worked around in various ways, but really `allowMultiUpdate` is primarily intended for server-side operations. Therefore, the recommended pattern is to use a [custom operation](DataSource.md#method-datasourceperformcustomoperation) from the client to invoke a DMI on the server which performs the multi-update operation via a second, server-side DSRequest.

In any case, it's normally a good idea to set [requiredCriterion](#attr-operationbindingrequiredcriterion) on the multi-update operation to ensure that the alternative criteria is present as expected.

### See Also

- [OperationBinding.providesMissingKeys](#attr-operationbindingprovidesmissingkeys)
- [DataSource.defaultMultiUpdatePolicy](DataSource.md#attr-datasourcedefaultmultiupdatepolicy)

**Flags**: IR

---
## Attr: OperationBinding.spoofResponses

### Description
For a DataSource contacting a [WSDL web service](DataSource.md#attr-datasourceservicenamespace), setting this flag means the DataSource doesn't actually attempt to contact the server but generates a sample response instead, based on the XML Schema of the response message embedded in the WSDL.

The spoofed response will include all complexType elements and will fill in appropriate values by type for all simpleType elements, although the spoofed data will not conform to all xs:restriction declarations (eg xs:pattern).

Note that if your WSDL does not fully describe the response format (some WSDL services just have a placeholder <xs:any> element), SmartClient can only produce a partial response. To use a hand-generated sample response, just save an XML file to disk and use the [OperationBinding.dataURL](#attr-operationbindingdataurl) setting to point to it.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.sqlUsePagingHint

### Description
If explicitly set true or false, forces the use of a "hint" in the SQL we generate for paged queries on or off as appropriate. If not set, defaults to the [DataSource.sqlUsePagingHint](DataSource.md#attr-datasourcesqlusepaginghint) value. Note this property is only applicable to [SQL](DataSource.md#attr-datasourceservertype) DataSources, only when a [paging strategy](DataSource.md#attr-datasourcesqlpaging) of "sqlLimit" is in force, and it only has an effect for those specific database products where we employ a native hint in the generated SQL in an attempt to improve performance.

### Groups

- sqlPaging

### See Also

- [DataSource.sqlUsePagingHint](DataSource.md#attr-datasourcesqlusepaginghint)

**Flags**: IR

---
## Attr: OperationBinding.dataURL

### Description
URL to contact to fulfill DSRequests for this operationBinding.

`dataURL` is typically set as `DataSource.dataURL` rather than on each individual operationBinding. However, when using `dataURL` to configure the server side of a [RestConnector](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), it is common to set `dataURL` at the operationBinding level, as described in the [DataSource-level dataURL](DataSource.md#attr-datasourcedataurl) documentation.

`dataURL` can be omitted for a DataSource using a Web Service ([DataSource.serviceNamespace](DataSource.md#attr-datasourceservicenamespace) is set).

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.sqlPrefix

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For operations on DataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, some text to add right at the beginning of the query generated for this specific operation, before all other text. This can be plain text or a [Velocity template](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables). Like [DataSource.sqlSuffix](DataSource.md#attr-datasourcesqlsuffix), this property allows for non-standard SQL extensions that may be required to obtain some special, database-specific behavior. For example, Oracle database supports hints specified in comments that appear before the main query text, like this:

```
    /* ALL_ROWS */  SELECT * FROM MyTable
 
```
This property is ignored for non-SQL dataSources

`sqlPrefix` can also be specified at the [DataSource level](DataSource.md#attr-datasourcesqlprefix); any such value acts as a default for the dataSource, and will be overridden by an operationBinding-level setting

You can alternatively provide SQL prefix text programmatically, by overriding `getSQLPrefix()` in a [custom DataSource implementation](DataSource.md#attr-datasourceserverconstructor)

### Groups

- customQuerying

**Flags**: IR

---
## Attr: OperationBinding.operationId

### Description
Optional operationId if this DataSource supports two or more variants of one of the basic DataSource operations, for instance, a "fetch" that uses full text search and a "fetch" that accepts per-field search criteria. See [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) for usage.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.dataFormat

### Description
Format for response data for this operation.

Typically set once for the DataSource as a whole via [DataSource.dataFormat](DataSource.md#attr-datasourcedataformat).

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.ownerIdField

### Description
Overrides the same setting at the [DataSource](DataSource.md#attr-datasourceowneridfield) level, for this operation only. See the dataSource-level documentation for details.

### See Also

- [DataSource.ownerIdField](DataSource.md#attr-datasourceowneridfield)
- [OperationBinding.guestUserId](#attr-operationbindingguestuserid)

**Flags**: IR

---
## Attr: OperationBinding.providesMissingKeys

### Description
Ordinarily, "update" and "remove" operations are only allowed if all primary key values are present in the request. This is because an update request that has missing primary key values cannot be guaranteed to affect only one record.

Setting this property on an operationBinding circumvents this restriction for that operation only. Note, this property differs from [allowMultiUpdate](#attr-operationbindingallowmultiupdate) in its intent: `allowMultiUpdate` tells the framework that this operation deliberately affects multiple records; `providesMissingKeys` tells the framework that this operation will only affect one record, and will ensure this by providing values for missing keys during its operation. Unlike `allowMultiUpdate`, setting this flag does not cause component caches to be [invalidated](ListGrid_2.md#method-listgridinvalidatecache)

Providing values for missing keys can be done in various ways:

*   Operations that specify `<[customSQL](#attr-operationbindingcustomsql)>` or `<[whereClause](#attr-operationbindingwhereclause)>` can provide missing key values from session storage or elsewhere in the provided record
*   Operations that specify `<[script](../kb_topics/serverScript.md#kb-topic-server-scripting)>` can provide arbitrary code to manipulate the record in whatever way they like before executing the underlying built-in functionality
*   Operations can specify `<[criteria](#attr-operationbindingcriteria)>` to provide missing keys
*   A request can contain [fieldValueExpressions](DSRequest.md#attr-dsrequestfieldvalueexpressions), which can be used to provide values for missing keys

Note, you can also use a regular [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) to arbitrarily manipulate the record sent from the client, including providing values for any missing keys. If you do this, you do not need to specify `providesMissingKeys` because the request is not validated for the presence of key values until after the DMI has run.

**Warning:** Be aware that this is a potentially dangerous setting and should be used with care. With this flag set, the framework cannot guarantee that an update will not change or remove every row in a table: it becomes your code's responsibility to ensure that all PK values are provided to the operation by the time it actually needs them.

### See Also

- [OperationBinding.allowMultiUpdate](#attr-operationbindingallowmultiupdate)
- [DataSourceField.autoGenerated](DataSourceField.md#attr-datasourcefieldautogenerated)

**Flags**: IR

---
## Attr: OperationBinding.groupClause

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", this property can be specified on an operationBinding to provide the server with a bespoke GROUP BY clause to use when constructing the SQL query to perform this operation. The property should be a comma-separated list of column names and/or expressions, forming a valid GROUP BY clause in the syntax of the underlying database. The server will insert the text of this property immediately after the "GROUP BY" token.

Note that specifying this property enables you to use aggregate functions (such as COUNT and SUM) in your [selectClause](#attr-operationbindingselectclause). Also note that care is required when using groupClause to ensure that the selectClause contains the fields you are grouping by. Failure to do this correctly will result in a runtime SQL error.

This property is only applicable to operationBindings of [operationType](#attr-operationbindingoperationtype) "fetch".

See the documentation for [OperationBinding.customSQL](#attr-operationbindingcustomsql) for usage examples

### Groups

- customQuerying

### See Also

- [OperationBinding.customSQL](#attr-operationbindingcustomsql)
- [OperationBinding.selectClause](#attr-operationbindingselectclause)

**Flags**: IR

---
## Attr: OperationBinding.customSQL

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For a dataSource of [serverType](DataSource.md#attr-datasourceservertype) "sql", "hibernate" or "jpa", this property can be specified on an operationBinding to indicate that the server should run user-specified SQL, rather than the query it would normally generate to satisfy a dataSource operation. This property allows you to provide a fully-customized query.

Hibernate and JPA dataSources also support customizing the query via [OperationBinding.customHQL](#attr-operationbindingcustomhql) or [OperationBinding.customJQL](#attr-operationbindingcustomjql) respectively.

For SQL dataSources, as an alternative to `customSQL` you can provide custom "pieces" to the query generator, via properties such [whereClause](#attr-operationbindingwhereclause) and [valuesClause](#attr-operationbindingvaluesclause).  
This feature is not available for Hibernate or JPA DataSources.  
See the [customQuerying](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview) for more details.

For a dataSource of type "sql", the SmartClient server generates a number of useful [query "pieces"](../main.md#type-defaultqueryclause), and makes them available to your custom SQL code via the Velocity templating language (note that this is not available for "hibernate" dataSources).

We also make the template variables **$criteria** and **$values** available, to give you direct access to the supplied criteria, and to the new field values for update and add operations. These variables are available to both "sql" and "hibernate" dataSources.

Note that you should use this feature with care. In particular, writing customSQL code that makes use of a particular database engine's features or syntax will make your application less portable.

See [customQuerying](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview) for an overview of writing custom queries and clauses.

#### Examples
An example using the SmartClient-supplied query pieces. This custom query will give exactly the same result as the SmartClient-generated query:

``<operationBinding operationId="customFetch" operationType="fetch">`     `<customSQL>`       SELECT $defaultSelectClause FROM $defaultTableClause WHERE $defaultWhereClause ORDER BY $defaultOrderClause     `</customSQL>`   `</operationBinding>`   `

An example using the SmartClient-supplied **$criteria** template variable:

``<operationBinding operationId="customFetch" operationType="fetch">`     `<customSQL>`       SELECT foo, bar, baz FROM MyTable WHERE bar > $criteria.someValue     `</customSQL>`   `</operationBinding>`   `

An update example:

``<operationBinding operationId="myUpdateOp" operationType="update">`     `<customSQL>`       UPDATE $defaultTableClause SET $defaultValuesClause WHERE bar <= $criteria.someValue     `</customSQL>`   `</operationBinding>`   `

### Groups

- customQuerying

### See Also

- [OperationBinding.customHQL](#attr-operationbindingcustomhql)
- [OperationBinding.namedQuery](#attr-operationbindingnamedquery)
- [DataSourceField.customSQL](DataSourceField.md#attr-datasourcefieldcustomsql)

**Flags**: IR

---
## Attr: OperationBinding.arrayCriteriaForceExact

### Description
Operation-level override for the DataSource-level [arrayCriteriaForceExact](DataSource.md#attr-datasourcearraycriteriaforceexact) flag. See the documentation for that flag for details.

### Groups

- clientDataIntegration
- serverDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.sqlPaging

### Description
The paging strategy to use for this specific OperationBinding. If this property is not set, we fall back to the [DataSource.sqlPaging](DataSource.md#attr-datasourcesqlpaging) value, and the defaults described in the documentation for that property.

### See Also

- [DataSource.sqlPaging](DataSource.md#attr-datasourcesqlpaging)

**Flags**: IRW

---
