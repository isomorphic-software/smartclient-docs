# OperationBinding Documentation

[← Back to API Index](../reference.md)

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

- [RPCTransport](../reference.md#type-rpctransport)
- [DataSource.callbackParam](DataSource.md#attr-datasourcecallbackparam)

**Flags**: IR

---
## Attr: OperationBinding.preventHTTPCaching

### Description
Configures [DataSource.preventHTTPCaching](DataSource.md#attr-datasourcepreventhttpcaching) on a per-operationType basis.

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
## Attr: OperationBinding.groupBy

### Description
Field or list of fields to group by when using [server-side summarization](../kb_topics/serverSummaries.md#kb-topic-server-summaries).

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for details and examples of usage.

### Groups

- serverSummaries

### See Also

- [OperationBinding.summaryFunctions](#attr-operationbindingsummaryfunctions)

**Flags**: IR

---
## Attr: OperationBinding.lineBreakStyle

### Description
The style of line-breaks to use in the exported output. See [LineBreakStyle](../reference.md#type-linebreakstyle) for more information.

**Flags**: IR

---
## Attr: OperationBinding.multiInsertNonMatchingStrategy

### Description
For "add" operations on dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, this property sets the multi-insert "non matching" strategy for this [operation](#class-operationbinding). Only has an effect if the [add request](DataSource.md#method-datasourceadddata) specifies a list of records as the data, and only if [multiInsertStrategy](#attr-operationbindingmultiinsertstrategy) is set to "multipleValues" either globally or at the [DSRequest](../reference_2.md#object-dsrequest), [OperationBinding](#class-operationbinding), or [DataSource](DataSource.md#class-datasource) level.

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

- [DSProtocol](../reference_2.md#type-dsprotocol)

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
*   expressions generated by `$sql.partialHaving(...)` and `$sql.havingWithout(...)` [Velocity context](#kb-topic-velocitysupport) variables used in [SQL Temlating](#kb-topic-customquerying)

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
## Attr: OperationBinding.criteria

### Description
**Elements of this feature are only available with Power or better licenses.** See [smartclient.com/product](http://smartclient.com/product) for details.

A list of [DSRequestModifier](../reference_2.md#object-dsrequestmodifier)s that will be used to modify the criteria of each [DSRequest](../reference_2.md#object-dsrequest) that uses this operationBinding. Note that the criteria elements are applied to DSRequest criteria as follows:

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
When set, causes the results of the DataSource Operation to be exported to a file, whose name and format are indicated by [OperationBinding.exportFilename](#attr-operationbindingexportfilename) and [OperationBinding.exportAs](#attr-operationbindingexportas) respectively. When no exportFilename is provided, the default is _Results_ and the default value of exportAs is _csv_. Once the Operation completes, [DSRequest.exportDisplay](DSRequest.md#attr-dsrequestexportdisplay) specifies whether the exported data will be downloaded to the file-system or displayed in a new window. The default value of exportDisplay is "download" which displays the Save As dialog. See [ExportDisplay](../reference_2.md#type-exportdisplay) for more information.

The export field-list can also be configured, see [DSRequest.exportFields](DSRequest.md#attr-dsrequestexportfields).

You can also configure the style of line-breaks to use when generating the output. See [LineBreakStyle](../reference.md#type-linebreakstyle) for more information.

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
## Attr: OperationBinding.requestProperties

### Description
Additional properties to pass through to the [DSRequest](../reference_2.md#object-dsrequest) created for this operation. Note that these will be cumulative with and will override on a per-property basis any properties set via [DataSource.requestProperties](DataSource.md#attr-datasourcerequestproperties).

These properties are applied before [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest) is called.

### Groups

- clientDataIntegration
- serverDataIntegration

### See Also

- [DSRequest](../reference_2.md#object-dsrequest)
- [DataSource.requestProperties](DataSource.md#attr-datasourcerequestproperties)

**Flags**: IR

---
## Attr: OperationBinding.summaryFunctions

### Description
A mapping from field names to [summary functions](../reference_2.md#type-summaryfunction) to be applied to each field.

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [OperationBinding.groupBy](#attr-operationbindinggroupby)

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
You can explicitly declare the arguments to be passed to [OperationBinding.serverMethod](#attr-operationbindingservermethod) using this attribute. This isn't required - in the absence of `methodArguments`, the DMI implementation will still automatically pass a stock set of arguments to your method (see the overview in [ServerObject](../reference_2.md#object-serverobject)), but specifying arguments gives you the ability to call pre-existing methods without adding SmartClient-specific code.

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

- [ServerObject](../reference_2.md#object-serverobject)

**Flags**: IR

---
## Attr: OperationBinding.requires

### Description
Indicates that the specified [VelocityExpression](../reference_2.md#type-velocityexpression) must be true for a user to access this operationBinding.

As with [OperationBinding.requiresRole](#attr-operationbindingrequiresrole), if there an operationBinding that is the default operationBinding for the operationType, its `requires` expression is assumed to apply to all other operationBindings of the same type unless they explicitly set `requires=""`

[DataSource.requires](DataSource.md#attr-datasourcerequires), if specified, applies before `operationBinding.requires` is evaluated. In this case, both `requires` expressions must be true for the request to be accepted.

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: OperationBinding.csvDelimiter

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.csvDelimiter](DataSource.md#attr-datasourcecsvdelimiter) - see that property's documentation for details

### Groups

- serverRestConnector

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
## Attr: OperationBinding.transformRequestScript

### Description
Scriptlet to be executed prior to the DataSource operation which is configured by this operationBinding. See [DataSource.transformRequestScript](DataSource.md#attr-datasourcetransformrequestscript) for further details.

Note, unlike many OperationBinding-level properties, a `transformRequestScript` at the OperationBinding level does not hide a `transformRequestScript` defined at the DataSource level. Instead, if you define `transformRequestScript` against both the DataSource and the OperationBinding, **both** are run - first the DataSource-level script, then the OperationBinding-level one.

### Groups

- serverScript

**Flags**: IR

---
## Attr: OperationBinding.suppressAutoMappings

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.suppressAutoMappings](DataSource.md#attr-datasourcesuppressautomappings) - see that property's documentation for details

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: OperationBinding.multiInsertBatchSize

### Description
For "add" operations on dataSources of [serverType](DataSource.md#attr-datasourceservertype) "sql" only, this property sets the multi-insert batch size for this [operation](#class-operationbinding). Only has an effect if the [add request](DataSource.md#method-datasourceadddata) specifies a list of records as the data, and only if [multiInsertStrategy](#attr-operationbindingmultiinsertstrategy) is set to "multipleValues" either globally or at the [DSRequest](../reference_2.md#object-dsrequest), [OperationBinding](#class-operationbinding), or [DataSource](DataSource.md#class-datasource) level.

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
## Attr: OperationBinding.xmlTag

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.xmlTag](DataSource.md#attr-datasourcexmltag) - see that property's documentation for details

### Groups

- serverRestConnector

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
*   _sqlConnection_: **SQLDataSource only**: the current SQLConnection object. If using [automatic transactions](#attr-datasourceautojointransactions) are enabled, this SQLConnection is in the context of the current transaction.
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
## Attr: OperationBinding.progressiveLoading

### Description
Sets [progressive loading mode](DataSource.md#attr-datasourceprogressiveloading) for this particular operation, overriding the DataSource-level setting. Note that this setting applies only to fetch operations - it has no effect if specified on any other kind of operation.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)

**Flags**: IRW

---
## Attr: OperationBinding.operationType

### Description
Which operationType this operationBinding is for. This property is only settable on an operationBinding, not a DataSource as a whole.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: OperationBinding.wrapInList

### Description
Applies to RestConnector dataSources ([serverType](DataSource.md#attr-datasourceservertype) "rest") only. This is an operationBinding-level override of [DataSource.wrapInList](DataSource.md#attr-datasourcewrapinlist) - see that property's documentation for details

### Groups

- serverRestConnector

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
The name of the method to invoke on the [ServerObject](../reference_2.md#object-serverobject) for this operationBinding.

**NOTE:** If you have a [DataSource-level ServerObject](DataSource.md#attr-datasourceserverobject) and wish to override this operation so that it simply calls a different method on the same server object, it is sufficient to specify just this property on the operationBinding: there is no need to redefine the serverObject at the operationBinding level.

**Flags**: IR

---
## Attr: OperationBinding.applyCriteriaBeforeAggregation

### Description
If set to "true", all criteria for the DSRequest using [serverSummaries](#serversummaries) are applied before aggregation, and the [afterWhereClause](#attr-operationbindingafterwhereclause) is not generated.

This property is only applicable if you are using the SQL DataSource, the other built-in types (Hibernate and JPA/JPA2) always perform filtering before summarization.

**NOTE** this property exists principally for backcompat, as the results of apply criteria before aggregation are usually senseless, and in this mode client-side filtering will not match server-side filtering (since client-side filtering is always post-aggregation), so the ability to filter on those fields would need to be disabled in the UI.

Still, if you have this flag was set to "true" and the "avg" function is being applied to a "price" field, criteria like "price < 5" will eliminate records where price is less than 5 _before_ the average price is calculated. Note that this means that client-side filtering may not work as expected with summarized results: client-side filter criteria are necessarily applied _after_ summary functions have been applied, so may not match the server's behavior. You can set [ResultSet.useClientFiltering](ResultSet.md#attr-resultsetuseclientfiltering) to disable client-side filtering on a grid via [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). Or individual fields can be marked [canFilter:false](ListGridField.md#attr-listgridfieldcanfilter).

Note that using [customQuerying](#kb-topic-customquerying) is an ultimate approach to make all kinds of modifications to the way SQL query is generated and with new _$sql.partialWhere(fieldNames)_, _$sql.whereWithout(fieldNames)_, _$sql.partialHaving(fieldNames)_ and _$sql.havingWithout(fieldNames)_ [Velocity context](#kb-topic-velocitysupport) APIs you have complete control over the automatically generated criteria.

To apply this setting to a specific DSRequest, use the [DSRequest.applyCriteriaBeforeAggregation](DSRequest.md#attr-dsrequestapplycriteriabeforeaggregation).

### See Also

- [OperationBinding.afterWhereClause](#attr-operationbindingafterwhereclause)
- [DSRequest.applyCriteriaBeforeAggregation](DSRequest.md#attr-dsrequestapplycriteriabeforeaggregation)

**Flags**: IR

---
## Attr: OperationBinding.exportAs

### Description
The format in which the data should be exported. Default is "csv". See [ExportFormat](../reference_2.md#type-exportformat) for more information.

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

A list of [DSRequestModifier](../reference_2.md#object-dsrequestmodifier)s that will be used to modify the values object of each [DSRequest](../reference_2.md#object-dsrequest) that uses this operationBinding. See this example: *queuedAdd example*.

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
