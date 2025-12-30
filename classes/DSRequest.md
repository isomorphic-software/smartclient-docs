# DSRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: DSRequest.exportToClient

### Description
If set to true (the default), SmartClient Server will export data back to the client, either as a file download or as content in a new browser window, depending on the setting of [exportDisplay](#attr-dsrequestexportdisplay).

Setting this property to false disables this. This may be useful when developers wish to [export the data to a file on the server fileSystem](#attr-dsrequestexporttofilesystem), but do not need to display it in the browser in response to the export request.

Note that it is perfectly valid to have both this property and [exportToFilesystem](#attr-dsrequestexporttofilesystem) set to true; in this case the data is both exported to a file on the server filesystem, and downloaded to the client. If you specify _neither_ property, the export no-ops.

**Flags**: IR

---
## Attr: DSRequest.endRow

### Description
End row of requested results, used only with fetch operations.

Note that startRow and endRow are zero-based, inclusive at the beginning and exclusive at the end (like substring), so startRow: 0, endRow: 1 is a request for the first record.

### Groups

- paging

**Flags**: IR

---
## Attr: DSRequest.startRow

### Description
Starting row of requested results, used only with fetch operations. If unset, 0 is assumed.

Note that startRow and endRow are zero-based, inclusive at the beginning and exclusive at the end (like substring), so startRow: 0, endRow: 1 is a request for the first record.

### Groups

- paging

**Flags**: IR

---
## Attr: DSRequest.additionalOutputs

### Description
For fetch, add or update operation, an optional comma separated list of fields to fetch from another, related DataSource.

Fields should be specified in the format `"localFieldName!relatedDataSourceID.relatedDataSourceFieldName"`. where `_relatedDataSourceID_` is the ID of the related dataSource, and `_relatedDataSourceFieldName_` is the field for which you want to fetch related values. The returned field values will be stored on the data returned to the client under the specified `_localFieldName_`. Note that this will be applied in addition to any specified [DSRequest.outputs](#attr-dsrequestoutputs).

Note that as with [DataSourceField.includeFrom](DataSourceField.md#attr-datasourcefieldincludefrom), the related dataSource must be linked to the primary datasource via a foreignKey relationship.

Note additionalOutputs sent in request from the browser can be completely disabled in [server.properties](../reference.md#kb-topic-serverproperties-file) by setting `datasource.allowClientAdditionalOutputs`:

```
     datasource.allowClientAdditionalOutputs: false
 
```
In this case [DSRequest.additionalOutputs](#attr-dsrequestadditionaloutputs) sent from the browser will be cleared before executing request. Note that programatically configured additionalOutputs are always allowed, but you can't modify them from within a DMI method, so the only way to execute a request with additionalOutputs that differ from what was sent by the client is to create a new DSRequest

**Flags**: IRA

---
## Attr: DSRequest.sortBy

### Description
Field name to sortBy, prefixed with optional "-" indicating descending sort. For example, to sort by the field "userName" in ascending order, set `sortBy` to just "userName". For descending sort on "userName", set `sortBy` to "-userName".

To sort by multiple fields, an array of field names is also supported. For example, to sort by the field "department" in ascending order, followed by the field "userName" in descending order, set `sortBy` to:

`[ "department", "-userName" ]`

Additionally, this property supports an array of [SortSpecifier](../reference.md#object-sortspecifier) objects. Setting `sortBy` to the following SortSpecifier array results in the same multi-level sort mentioned above:

`[     { property: "department", direction: "ascending" },     { property: "userName", direction: "descending" }   ]`

**Flags**: IR

---
## Attr: DSRequest.linkDataFetchOperation

### Description
For a databound [multi-link tree](Tree.md#method-treeismultilinktree), this is the `operationId` to use for the separate fetch on the [ResultTree.linkDataSource](ResultTree.md#attr-resulttreelinkdatasource) that will be generated if [LinkDataFetchMode](../reference.md#type-linkdatafetchmode) is "separate". This property overrides the [linkDataFetchOperation](ResultTree.md#attr-resulttreelinkdatafetchoperation) property on [ResultTree](ResultTree.md#class-resulttree), for this fetch only.

Ignored if this DSRequest is not a fetch against a multi-link tree.

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: DSRequest.textMatchStyle

### Description
For "fetch" operations, how search criteria should be interpreted for text fields: one of "exact" for exact match, "exactCase" for case-sensitive exact match, "startsWith" for matching at the beginning only, or "substring" for substring match. All `textMatchStyle` settings except "exactCase" are case-insensitive; use [AdvancedCriteria](../reference.md#object-advancedcriteria) for greater control over matching.

This property defaults to the value of [DataSource.defaultTextMatchStyle](DataSource.md#attr-datasourcedefaulttextmatchstyle) if it is not explicitly provided on the `DSRequest`. Note, however, that DSRequests issued by [ListGrid](ListGrid_1.md#class-listgrid)s and other [components](../reference.md#interface-databoundcomponent) will generally have a setting for textMatchStyle on the component itself (see [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle), for example).

This setting is respected by the built-in server-side connectors for SQL, JPA and Hibernate. A custom server-side DataSource implementation should generally respect this flag as well, or server-side filtering will not match client-side filtering, which will require [disabling client-side filtering](ResultSet.md#attr-resultsetuseclientfiltering), a huge performance loss.

**Flags**: IR

---
## Attr: DSRequest.pendingAdd

### Description
Indicates that a validation request is being made for a record that will ultimately be saved with an "add" request, as opposed to an "update" request. This context is necessary for some validators because the nature of the validation depends on whether we are adding or updating a record. The system sets this flag when processing interim validations, such as those fired when [DynamicForm.validateOnChange](DynamicForm.md#attr-dynamicformvalidateonchange) is in force.

**Flags**: IR

---
## Attr: DSRequest.exportShowHeaderSpanTitles

### Description
When you erxport a [ListGrid](ListGrid_1.md#class-listgrid) that has [headerSpans](ListGrid_1.md#attr-listgridheaderspans), should headerSpans also be exported. See [DSRequest.exportSpanTitleSeparator](#attr-dsrequestexportspantitleseparator) for details of of what it means to export headerSpans to different export targets.

Note that [DSRequest.exportPropertyIdentifier](#attr-dsrequestexportpropertyidentifier) controls whether field names or titles are appended to the headerSpan titles (and used for fields without headerSpans).

**Flags**: IR

---
## Attr: DSRequest.oldValues

### Description
For an `update` or `remove` operation, the original values from the record that is being updated or removed. `oldValues` is automatically added to DSRequests submitted by DataBound Components. Available on the server via `DSRequest.getOldValues()`.

The server can compare the `oldValues` to the most recent stored values in order to detect that the user was looking at stale values when the user submitted changes (NOTE: this means of detecting concurrent edit is sometimes called "optimistic concurrency" or "long transactions").

In applications where a policy of "last update wins" is not appropriate when updating certain fields, special UI can be shown for this case. For example, on detecting concurrent edit, the server may send back a special `dsResponse.status` code that the client application detects, offering the user a choice of proceeding with the operation, discarding edits, or reconciling new and old values in a special interface.

**Flags**: IR

---
## Attr: DSRequest.resultTree

### Description
For advanced use in integrating trees that [load data on demand](ResultTree.md#attr-resulttreeloaddataondemand) with web services, the ResultTree that issued this "fetch" DSRequest is automatically made available as the `resultTree` property.

This property can only be read. There is no meaning to setting this property yourself.

**Flags**: R

---
## Attr: DSRequest.summaryFunctions

### Description
A mapping from field names to [summary functions](../reference.md#type-summaryfunction) to be applied to each field.

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [DSRequest.groupBy](#attr-dsrequestgroupby)

**Flags**: IR

---
## Attr: DSRequest.exportImageFormat

### Description
The image format in which the SVG graphic should be exported.

**Flags**: IR

---
## Attr: DSRequest.exportFooter

### Description
Optional text to appear at the end of the file.

**Flags**: IR

---
## Attr: DSRequest.exportFilename

### Description
The name of the file to save the exported data into. If [exportToFilesystem](#attr-dsrequestexporttofilesystem) is set, this is the name of the file the server creates on its filesystem. If [exportToClient](#attr-dsrequestexporttoclient) is set, this is the filename that will appear to the browser.

If the exportFilename that you specify does not include an extension, one will be added to it based on the [ExportFormat](../reference.md#type-exportformat) specified by [DSRequest.exportAs](#attr-dsrequestexportas). Filename is forced to have the correct extension to work around bugs in IE, but if you don't want the filename to be manipulated, use "custom" [exportFormat](../reference.md#type-exportformat), see example.

### See Also

- [DSRequest.exportPath](#attr-dsrequestexportpath)

**Flags**: IR

---
## Attr: DSRequest.exportCSS

### Description
When using [RPCManager.exportContent](RPCManager.md#classmethod-rpcmanagerexportcontent) to produce a .pdf from a SmartClient UI, this property allows dynamic CSS to be passed to the server. Since the `exportContent()` system already provides a way to specify a custom skin or additional stylesheet for export, `exportCSS` should only be used for small bits of CSS that are necessarily dynamic.

For example, when printing a very wide page, such as a grid with many columns or a very wide chart, you could send the string "@page {size: A4 landscape; }" as `exportCSS` to cause the generated PDF to use landscape mode, so that all content fits without clipping.

**Flags**: IR

---
## Attr: DSRequest.groupBy

### Description
List of fields to group by when using [server-side summarization](../kb_topics/serverSummaries.md#kb-topic-server-summaries).

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for details and examples of usage.

### Groups

- serverSummaries

### See Also

- [DSRequest.summaryFunctions](#attr-dsrequestsummaryfunctions)

**Flags**: IR

---
## Attr: DSRequest.streamResults

### Description
If true, results will be streamed on the server, rather than all records being read into server memory at once; this approach is appropriate for retrieving or exporting large datasets without swamping the server.

Although this property can be set without any particular concerns (small datasets can be streamed just as readily as large ones), bear in mind that although streaming enables the processing of very large datasets, processing and downloading very large datasets in a normal client/server flow will very rarely give an acceptable user experience. Streaming is of more practical use in a batch setting - for example, a disconnected [export](#attr-dsrequestexporttofilesystem).

Note that streaming requires specific server support; of SmartClient's built-in DataSource types, only `SQLDataSource` is able to stream results. This property is ignored by other DataSource types. If you wish to implement the necessary server-side behavior to support streaming with a custom DataSource, see the the server-side Javadocs for `DSResponse.hasNextRecord()` and `DSResponse.nextRecordAsObject()`.

See also the server-side documentation for `DSResponse`, `SQLDataSource` and `StreamingResponseIterator`.

Note, that streaming results does not support fields with ["concat" summary function](../reference.md#type-summaryfunction) on non-Oracle databases. Such fields will be skipped.

**Flags**: IR

---
## Attr: DSRequest.lineBreakStyle

### Description
The style of line-breaks to use in the exported output. See [LineBreakStyle](../reference_2.md#type-linebreakstyle) for more information.

**Flags**: IR

---
## Attr: DSRequest.exportHeader

### Description
Optional text to appear at the beginning of the file.

**Flags**: IR

---
## Attr: DSRequest.keepParentsOnFilter

### Description
This property is for advanced use in integrating trees that [load data on demand](TreeGrid.md#attr-treegridloaddataondemand) using data paging. When this flag is set, a server fetch operation is expected to return all of the tree nodes that either match the provided criteria **or** have one or more children that match the criteria.

A ResultTree with [fetchMode:"paged"](ResultTree.md#attr-resulttreefetchmode) and with [keepParentsOnFilter](ResultTree.md#attr-resulttreekeepparentsonfilter) enabled will automatically set this property to `true` on all DSRequests that it sends to the server.

Currently, no built-in server-side connectors (SQL, JPA, Hibernate) implement support for the keepParentsOnFilter flag.

### Groups

- treeDataBinding

**Flags**: IRW

---
## Attr: DSRequest.exportTitleSeparatorChar

### Description
The character with which to replace spaces in field-titles when exporting to XML. If not specified in the request, the server uses "".

**Flags**: IR

---
## Attr: DSRequest.clientContext

### Description
An object to be held onto for the duration of the DSRequest turnaround to track application-specific context.

When a DataSource request completes, the `clientContext` is available in the [DSCallback](../reference.md#type-dscallback) as `dsResponse.clientContext`. The `clientContext` is never sent to the server.  
The `clientContext` is useful for holding onto state that will be used when the [DSCallback](../reference.md#type-dscallback) fires, such as the name of a component that will receive the returned data.

### See Also

- [DSResponse.clientContext](DSResponse.md#attr-dsresponseclientcontext)
- [RPCRequest.clientContext](RPCRequest.md#attr-rpcrequestclientcontext)

**Flags**: IRW

---
## Attr: DSRequest.exportTZ

### Description
For server-side export with [ExportFormat](../reference.md#type-exportformat) "xls" or "ooxml" only, timezone to use when saving values from [FieldType](../reference.md#type-fieldtype) "datetime" to the spreadsheet.

This setting exists because MS Excel™ has no concept of providing a true datetime value that is timezone-independent and will display in the local timezone where the Excel program is launched. This setting sets the timezone of the Excel workbook, so that it will display dates in the same timezone regardless of the local timezone where the Excel program is launched. Alternative approach is to set [exportDatesAsFormattedString=true](#attr-dsrequestexportdatesasformattedstring) telling datetime values must be provided as a rendered string, which implies rendering in a particular timezone when the spreadsheet is generated.

`exportTZ` can either be specified as a timezone offset in the same format expected by [Time.setDefaultDisplayTimezone](Time.md#classmethod-timesetdefaultdisplaytimezone) (for example, "+01:00" for one hour after GMT) or as the special constants "client" (meaning the current client display timezone) or "server" (meaning the timezone of the server).

Default if unspecified is "server".

This setting does not affect fields of type "date" or "time", which are timezone-independent values. See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on how SmartClient handles date, time and datetime values.

All non-spreadsheet export formats always use UTC. This setting also does not affect client-driven exports ([DataSource.exportClientData](DataSource.md#method-datasourceexportclientdata)), which always use client-side time.

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: DSRequest.exportNumbersAsFormattedString

### Description
When exporting via [ListGrid.exportClientData](ListGrid_1.md#method-listgridexportclientdata) to an `XLS` or `OOXML` spreadsheet, forces numbers to export as a string rather than a true numerical value.

If a number is provided to a spreadsheet as a string, Excel or other spreadsheet applications may not recognize them as being numbers that are valid for use in numerical formulas, filters, etc.

For this reason, the default behavior of `exportClientData` is to provide numerical values to the spreadsheet as true numbers. If [Format Strings](../reference.md#type-formatstring) are provided via properties like [dataSourceField.format](DataSourceField.md#attr-datasourcefieldformat) these will be translated to Excel / OpenOffice format strings and used when generating spreadsheets. Other formatting logic, such as [cell formatters](ListGridField.md#method-listgridfieldformatcellvalue), will not be used since they cannot be automatically translated to an Excel format string. If no translatable format string is available, numbers will be provided to the spreadsheet with no formatter and the spreadsheet program's default formatting for numerical values will be used.

If `exportNumbersAsFormattedString` is set to true, numbers will appear as strings that exactly match the formatting shown in the [DataBoundComponent](../reference.md#interface-databoundcomponent). As noted above, this means the spreadsheet program will not recognize the value as a number.

### Groups

- exportFormatting

### See Also

- [DataSourceField.exportFormat](DataSourceField.md#attr-datasourcefieldexportformat)

**Flags**: IR

---
## Attr: DSRequest.operationType

### Description
Type of operation being performed: "fetch", "add", "remove", "update" or "custom".

This property is generally automatically populated, for example when calling `fetchData()` on a DataSource or DataBound component the operationType is automatically set to "fetch". Note that "custom" operations are never generated automatically, they are always fired by your code.

**Flags**: IR

---
## Attr: DSRequest.data

### Description
Data, such as search criteria or an updated record, to be acted upon. Contents differ by `operationType`, see [DataSource Operations](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) for details.

This field is generally filled in by passing the "data" argument to methods such as [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata).

**Flags**: IR

---
## Attr: DSRequest.requestId

### Description
Automatically generated unique ID for this request. This ID will be required by developers making use of the ["clientCustom" dataProtocol](../reference.md#type-dsprotocol).

**Flags**: RA

---
## Attr: DSRequest.operationId

### Description
When a [DataBoundComponent](../reference.md#interface-databoundcomponent) sends a DSRequest, the `dsRequest.operationId` will be automatically picked up from the `fetchOperation`, `addOperation`, etc properties of the DataBoundComponent.

The `operationId` serves as an identifier that you can use to create variations on the 4 basic DataSource operations that are used by different components in different parts of your application. For example, you may be using a standard `fetch` operation in one part of your application, however on another screen you want to perform a `fetch` operation on the same DataSource but interpret search criteria differently (eg full text search).

If you declare more than one [OperationBinding](OperationBinding.md#class-operationbinding) for the same [OperationBinding.operationType](OperationBinding.md#attr-operationbindingoperationtype), you can specify an `operationId` [on the operationBinding](OperationBinding.md#attr-operationbindingoperationid) which will cause that operationBinding to be used for dsRequests containing a matching `operationId`. This allows all the possible settings of an `operationBinding`, including [wsOperation](OperationBinding.md#attr-operationbindingwsoperation) or [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) settings, to be switched on a per-component or per-request basis.

For example, by setting the `fetchOperation` on a particular ListGrid, you could cause it to invoke a different server method via DMI, different [dataURL](OperationBinding.md#attr-operationbindingdataurl) or different [web service operation](OperationBinding.md#attr-operationbindingwsoperation).

The `operationId` can also be directly received by the server in order to affect behavior. When using the SmartClient Server, `operationId` can be accessed via dsRequest.getOperationId(). The [RestDataSource](RestDataSource.md#class-restdatasource) will also send the `operationId` to the server as part of the [request metadata](RestDataSource.md#attr-restdatasourcemetadataprefix).

Note that if you [manually invoke](DataSource.md#method-datasourcefetchdata) a DataSource operation, you can also specify operationId via the `requestProperties` parameter.

Note that the `operationId` has special significance in terms of whether two DSRequests are considered equivalent for caching and synchronization purposes - see [dsRequestEquivalence](../kb_topics/dsRequestEquivalence.md#kb-topic-dsrequestequivalence).

### Groups

- operations

**Flags**: IR

---
## Attr: DSRequest.exportSpanTitleSeparator

### Description
When you export a [ListGrid](ListGrid_1.md#class-listgrid) that has [headerSpans](ListGrid_1.md#attr-listgridheaderspans) defined and [DSRequest.exportShowHeaderSpanTitles](#attr-dsrequestexportshowheaderspantitles) is true, the behavior is dependent on the export type. Direct exports to Excel formats (both XLS and OOXML) place the headerSpans in merged cells in the spreadsheet, giving the same visual effect as the original ListGrid. This is not possible with exports to CSV format; instead, we alter the exported headers so that they contain the titles of the ancestor headerSpan(s).

For example, if you had a field titled "Population" inside a headerSpan titled "National", nested inside another headerSpan titled "Demographics", that would result in the exported field being titled "Demographics - National - Population".

The `exportSpanTitleSeparator` property allows you to override the separator string used when constructing these amalgamated headers.

**Flags**: IR

---
## Attr: DSRequest.exportDatesAsFormattedString

### Description
When exporting via [ListGrid.exportClientData](ListGrid_1.md#method-listgridexportclientdata) to an `XLS` or `OOXML` spreadsheet, forces dates to export as a string rather than a true date value.

If a date value is provided to a spreadsheet as a string, Excel or other spreadsheet applications may not recognize them as being date values that are valid for use in date-specific functions in formulas, filters, etc.

For this reason, the default behavior of `exportClientData` is to provide date values to the spreadsheet as true date values. If [Format Strings](../reference.md#type-formatstring) are provided via properties like [dataSourceField.format](DataSourceField.md#attr-datasourcefieldformat) these will be translated to Excel / OpenOffice format strings and used when generating spreadsheets. Other formatting logic, such as [cell formatters](ListGridField.md#method-listgridfieldformatcellvalue), will not be used since they cannot be automatically translated to an Excel format string. If no translatable format string is available, date values will be provided to the spreadsheet with no formatter and the spreadsheet program's default formatting for date values will be used.

If `exportDatesAsFormattedString` is set to true, date fields will appear as strings that exactly match the formatting shown in the [DataBoundComponent](../reference.md#interface-databoundcomponent). As noted above, this means the spreadsheet program will not recognize the value as a date.

### Groups

- exportFormatting

### See Also

- [DataSourceField.exportFormat](DataSourceField.md#attr-datasourcefieldexportformat)

**Flags**: IR

---
## Attr: DSRequest.exportResults

### Description
When set, causes the results of the DSRequest to be exported to a file, whose name and format are indicated by [DSRequest.exportFilename](#attr-dsrequestexportfilename) and [DSRequest.exportAs](#attr-dsrequestexportas) respectively. When no exportFilename is provided, the default is _Results.csv_ and the default value of exportAs is _csv_.

The export field-list can also be configured, see [DSRequest.exportFields](#attr-dsrequestexportfields). Formats for exported date and numeric are controlled by several settings - see [exportFormatting](../kb_topics/exportFormatting.md#kb-topic-exports--formatting) for an overview.

Once the operation completes, [DSRequest.exportDisplay](#attr-dsrequestexportdisplay) specifies whether the exported data should be downloaded to the file-system or displayed in a new window. The default value of exportDisplay is "download" which displays the Save As dialog. See [ExportDisplay](../reference.md#type-exportdisplay) for more information.

You can configure the style of [line-breaks](../reference_2.md#type-linebreakstyle) to use when generating the output, the [delimiter](#attr-dsrequestexportdelimiter) to use when exporting to CSV and the [separator-character](#attr-dsrequestexporttitleseparatorchar) to use in field-titles when exporting to XML.

Additionally, you can output arbitrary text before and after the exported data by setting [exportHeader](#attr-dsrequestexportheader) and [exportFooter](#attr-dsrequestexportfooter).

Note that for security reasons, an export initiated using dsRequest properties does not provide support for JSON format (see [this post](http://forums.smartclient.com/showthread.php?t=235) for more detail). However, you can use operationBinding.exportAs:"json" in a server-side .ds.xml file to force JSON export to be allowed.

As well as setting dsRequest.exportResults and related properties, exports can be initiated in two other ways, via [OperationBinding](OperationBinding.md#class-operationbinding)s and via custom server code which sets export-related properties on the [DSResponse](DSResponse.md#class-dsresponse). Both of those methods support exporting to JSON format.

**Format Examples** XML format

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
## Attr: DSRequest.useFlatFields

### Description
When `useFlatFields` is set for a request to be sent to a WSDL web service, when creating the input XML message to send to the web service, properties in [request.data](#attr-dsrequestdata) will be used as the values for XML elements of the same name, at any level of nesting.

`useFlatFields` allows you to ignore gratuitous XML message structure, such as extra levels of nested elements, and provides some insulation against changes in the required structure of the input message.

For example, given this input message:

```
 <FindServices>
     <searchFor>search text</searchFor>
     <Options>
         <caseSensitive>false</caseSensitive>
     </Options>
     <IncludeInSearch>
         <serviceName>true</serviceName>
         <documentation>true</documentation>
         <keywords>true</keywords>
     </IncludeInSearch>
 </FindServices>
 
```
If `useFlatFields` were **not** set, in order to fill out this message correctly, `request.data` would need to be:
```
{
    searchFor: "search text",
    Options : {
        caseSensitive: false,
    },
    IncludeInSearch : {
        serviceName: true,
        documentation : true,
        keywords : true
    }
 }
```
However if useFlatFields were set, `request.data` could be just:
```
{
    searchFor: "search text",
    caseSensitive: false,
    serviceName: true,
    documentation : true,
    keywords : true
 }
```
`useFlatFields` is often set when the input data comes from a [DynamicForm](DynamicForm.md#class-dynamicform) to avoid the cumbersome and fragile process of mapping input fields to an XML structure.

[OperationBinding.useFlatFields](OperationBinding.md#attr-operationbindinguseflatfields) can also be set to cause **all** dsRequests of a particular type to `useFlatFields` automatically.

For [DataBoundComponents](../reference.md#interface-databoundcomponent), [component.useFlatFields](DataBoundComponent.md#attr-databoundcomponentuseflatfields) can be set use "flattened" binding to fields of a WSDL message or XML Schema.

Note that `useFlatFields` is not generally recommended for use with XML input messages where multiple simple type fields exist with the same name, however if used in this way, the first field to use a given name wins. "first" means the first field encountered in a depth first search. "wins" means only the first field will be populated in the generated XML message.

### Groups

- flatFields

**Flags**: IR

---
## Attr: DSRequest.exportData

### Description
Only applies to request properties passed to [ListGrid.exportClientData](ListGrid_1.md#method-listgridexportclientdata). If specified this property contains an arbitrary set of data to be exported.

**Flags**: IR

---
## Attr: DSRequest.generateRelatedUpdates

### Description
Specifies should related updates have to be generated. If not set (or set to `null`) then related updates will be generated only for "add" and "update" operations. This property has to be explicitly set to `true` to generate related updates for "remove" operation.

This functionality loads related objects from database thus affecting operation performance. For "add" and "update" operations related objects are loaded anyway and performance impact is minimal. Simple "remove" operation does not need to load related objects. Depending on database structure performance impact can be significant if this property is set to `true`.

Note this feature works only with Hibernate/JPA data sources, see [JPA & Hibernate Relations](../kb_topics/jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations) for instructions how to set up relations. Table below uses "country -> cities" sample data model.

| Relation and Operation type | Loading complete related objects | Loading related IDs |
|---|---|---|
| Many-to-one (cities -> country): ADD/UPDATE | If operation affected country, for example new city added with existing countryId, then relatedUpdate is generated. Otherwise if city is added or updated without countryId set, relatedUpdate is not generated.Note that if provided countryId does not exist, it is created. | Same as with complete related objects, except if provided countryId does not exist, then it is not created, but reset to NULL. |
| Many-to-one (cities -> country): REMOVE | Removes record, depending on setting generates or not relatedUpdate for parent record. For example if city record is removed and countryId is sent to the server in remove request, then country record will be generated in relatedUpdates. |
| One-to-many (country -> cities): ADD/UPDATE | If add or update operation provides value sets for cities as well as for country, then cities are created/updated if necessary and relatedUpdates are generated.Note that all fields in cities value sets can be sent to server. | Same as with complete related objects, except you can only sent primary key values for cities. |
| One-to-many (country -> cities): REMOVE | Removes country, depending on setting returns or not relatedUpdates for the cities of removed country, which can be either REMOVE operations of all cities if cascade enabled, or UPDATE operations setting countryId=null to all cities if cascade is disabled |

Note that Many-to-Many works the same way as One-to-Many.

**Flags**: IRW

---
## Attr: DSRequest.shouldUseCache

### Description
This is a per-request flag for explicitly controlling whether the cache is used (bypassing it when not wanted, or using it when settings would indicate otherwise). See [DataSource.cacheAllData](DataSource.md#attr-datasourcecachealldata), [DataSource.cacheAllOperationId](DataSource.md#attr-datasourcecachealloperationid) and [DataSource.cacheAcrossOperationIds](DataSource.md#attr-datasourcecacheacrossoperationids) for caching management for all requests of a dataSource.

**Flags**: IRW

---
## Attr: DSRequest.outputs

### Description
The list of fields to return in the response, specified as a comma-separated string (eg, `"foo, bar, baz"`). You can use this property to indicate to the server that you are only interested in a subset of the fields that would normally be returned.

Note that you cannot use this property to request a _superset_ of the fields that would normally be returned, because that would be a security hole. It is possible to configure individual [OperationBinding](OperationBinding.md#class-operationbinding)s to return extra fields, but this must be done in the server's [DataSource](DataSource.md#class-datasource) descriptor; it cannot be altered on the fly from the client side.

### See Also

- [OperationBinding.outputs](OperationBinding.md#attr-operationbindingoutputs)
- [DSRequest.additionalOutputs](#attr-dsrequestadditionaloutputs)

**Flags**: IR

---
## Attr: DSRequest.exportDisplay

### Description
Specifies whether the exported data will be downloaded as an attachment or displayed in a new browser window. See [ExportDisplay](../reference.md#type-exportdisplay) for more information.

**Flags**: IR

---
## Attr: DSRequest.exportImageQuality

### Description
If exporting in [JPEG format](../reference.md#type-exportimageformat), the output JPEG quality level. This is a number from 0 to 1, with 1 representing the best quality and 0 representing the least quality but smallest file size.

**Flags**: IR

---
## Attr: DSRequest.exportRawValues

### Description
Whether formatting settings should be applied to data being exported. Default behavior and the effect of setting of `exportRawValues` is described in the [Export Formatting overview](../kb_topics/exportFormatting.md#kb-topic-exports--formatting).

### Groups

- exportFormatting

**Flags**: IRW

---
## Attr: DSRequest.exportDelimiter

### Description
The character to use as a field-separator in CSV exports. The default delimiter is comma.

**Flags**: IR

---
## Attr: DSRequest.exportAs

### Description
The format in which the data should be exported. Note that 'JSON' is not allowed as a client-side option. See [ExportFormat](../reference.md#type-exportformat) for more information.

**Flags**: IR

---
## Attr: DSRequest.useStrictJSON

### Description
Should the HTTP response to this request be formatted using the strict JSON subset of the javascript language? If set to true, responses returned by the server should match the format described [here](http://www.json.org/js.html).

Only applies to requests sent a server with [DataSource.dataFormat](DataSource.md#attr-datasourcedataformat) set to "json" or "iscServer".

**Flags**: IR

---
## Attr: DSRequest.exportPath

### Description
If [exportToFilesystem](#attr-dsrequestexporttofilesystem) is set, optionally specifies a path to use when saving the file. This path is relative to the default export path, which is set using the [server.properties](../reference.md#kb-topic-serverproperties-file) setting `export.location`; this is the project webRoot by default. For example, with the default setting of `export.location`, an `exportPath` of `"shared/ds"` and an [exportFilename](#attr-dsrequestexportfilename) of `"exportedData.csv"`, SmartClient Server would export to file `$webRoot/shared/ds/exportedData.csv`.

If you do not specify this property, SmartClient Server will export to the file indicated by `exportFilename` directly in the default export location.

This property is only applicable when [exportToFilesystem](#attr-dsrequestexporttofilesystem) is set.

### See Also

- [DSRequest.exportFilename](#attr-dsrequestexportfilename)

**Flags**: IR

---
## Attr: DSRequest.resultSet

### Description
For advanced use in integrating dataset paging with web services, the ResultSet that issued this "fetch" DSRequest is automatically made available as the `resultSet` property.

This property can only be read. There is no meaning to setting this property yourself.

**Flags**: R

---
## Attr: DSRequest.exportHeaderless

### Description
This property allows omitting column names from CSV and Excel exports (no effect on JSON or XML exports).

**Flags**: IRW

---
## Attr: DSRequest.exportPropertyIdentifier

### Description
Determines the [PropertyIdentifier](../reference.md#type-propertyidentifier) to be used in the exported data. This essentially means, should we export internal field names like "countryCode" or "EMPLOYEE\_NO", or localized descriptive field titles like "code du pays" or "Employee Number". This setting has a lot in common with [DSRequest.exportRawValues](#attr-dsrequestexportrawvalues); both are largely dependent on whether the exported data is intended for direct consumption by an end user (in which case it is appropriate to export formatted values and localized field titles), or for interface to some downstream computer system (in which case you probably want raw, unformatted values and internal field names).

If this property is not set, the following defaults apply:

*   If the export format is a native spreadsheet format (XLS or OOXML), localized field titles are used
*   If the export format is CSV, XML or JSON and this is a client-driven export (ie it was initiated by a call to [exportClientData()](ListGrid_1.md#method-listgridexportclientdata)), localized field titles are used
*   If the export format is CSV, XML or JSON and this is **not** a client-driven export, internal field names are used

### Groups

- exportFormatting

**Flags**: IRW

---
## Attr: DSRequest.callback

### Description
A callback method that will be called with an instance of DSResponse, as sent by the server. Queuing does not affect callbacks in any way - your specified callback will be invoked for each DSRequest that contained a callback regardless of whether the request was sent as part of a queue or not.

Note that if the request encounters an error (such as 500 server error), by default the callback will **not** be fired. Instead, [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror) is called to invoke the default system-wide error handling. Set [willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror):true to have your callback invoked regardless of whether there are errors; however, make sure your callback properly handles malformed responses when [RPCResponse.status](RPCResponse.md#attr-rpcresponsestatus) is non-zero. See the [error handling overview](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) below for more details.

### Groups

- errorHandling

**Flags**: IR

---
## Attr: DSRequest.componentId

### Description
For requests submitted by a [DataBoundComponent](../reference.md#interface-databoundcomponent), the [Canvas.ID](Canvas.md#attr-canvasid) of the submitting component.

This ID will be present for operations including automatic saves by a ListGrid [during editing](../kb_topics/editing.md#kb-topic-grid-editing), or calls to [form.saveData()](DynamicForm.md#method-dynamicformsavedata). It will not be present for a direct call to a DataSource method such as [DataSource.fetchData](DataSource.md#method-datasourcefetchdata).

Note this is the component's **String** ID - you can retrieve the component itself via [Canvas.getById](Canvas.md#classmethod-canvasgetbyid).

This property should be used for debugging purposes only - do not use it to trigger differences in server-side behavior, instead, use [DSRequest.operationId](#attr-dsrequestoperationid) because only `operationId` is considered when assessing [request equivalence](../kb_topics/dsRequestEquivalence.md#kb-topic-dsrequestequivalence).

**Flags**: IR

---
## Attr: DSRequest.validationMode

### Description
Mode of validation for entered data.

**Flags**: IR

---
## Attr: DSRequest.exportToFilesystem

### Description
If set, SmartClient Server will export data to a file on the **server** filesystem. The file we export to is determined by the [exportFilename](#attr-dsrequestexportfilename) and [exportPath](#attr-dsrequestexportpath). Note that filesystem exports are disabled by default, for security reasons. To enable them, set `export.allow.filesystem` to true in your `server.properties` file. If you enable filesystem exports, you should also consider setting a default export path, as described in the [exportPath](#attr-dsrequestexportpath) documentation.

Note that it is perfectly valid to specify both this property and [exportToClient](#attr-dsrequestexporttoclient); in this case the data is both exported to a file on the server filesystem _and_ downloaded to the client. If you specify _neither_ property, the export no-ops.

It is possible to redirect the filesystem export to make use of an `OutputStream` you provide. You use this when you want to make some use of the export document other than writing it to a disk file - for example, attaching it to an email or writing it to a database table. See the server-side Javadocs for `DSRequest.setExportTo()`.

**Flags**: IR

---
## Attr: DSRequest.exportFields

### Description
The list of field names to export. If provided, the field list in the exported output is limited and sorted as per the list.

If exportFields is not provided:

*   If we are exporting via [exportData()](#attr-dsrequestexportdata), the field list in the exported output is every non-hidden field defined in the DataSource, in DataSource definition order
*   If we are exporting via [exportClientData()](ListGrid_1.md#method-listgridexportclientdata) and we are not exporting to OOXML, or we are exporting to OOXML but we are not [streaming](#attr-dsrequestexportstreaming), the field list in the exported output is based on the client data sent up, taking every row into account (so if there is a value for field "foo" only in row 57, we will output a column "foo", the cells of which are empty except for row 57)
*   If we are exporting via [exportClientData()](ListGrid_1.md#method-listgridexportclientdata) and we are exporting to OOXML and streaming is in force (the default for OOXML), the field list in the exported output is based on the client data sent up, taking just the first row into account (so if there is a value for field "foo" only in row 57, we will not output a column "foo" at all)

**Flags**: IR

---
## Attr: DSRequest.exportValueFields

### Description
This flag has a different meaning depending on whether you are doing a client-driven or server-driven export.

For [exportClientData()](ListGrid_1.md#method-listgridexportclientdata) calls (client-driven), ordinarily any fields that have a [displayField](ListGridField.md#attr-listgridfielddisplayfield) defined have the value of that displayField exported, rather than the underlying value in the [valueField](ListGridField.md#attr-listgridfieldvaluefield). If you set the `exportValueFields` property, we export both the underlying value and the displayField value.

Again for `exportClientData()` calls, any fields that have a [valueMap](ListGridField.md#attr-listgridfieldvaluemap) defined ordinarily have the mapped value of the field exported, rather than the underlying data value. If you set the `exportValueFields` property, we instead export the underlying data value. Note, there is only one field in this scenario, not a `valueField` and a separate `displayField`, so we export **either** the underlying data value or the mapped value, not both as in the `displayField`/`valueField` case described above.

For [exportData()](DataBoundComponent.md#method-databoundcomponentexportdata) calls (server-driven), we ordinarily export the underlying data value of all fields. However, if you set the `exportValueFields` property explicitly to `false`, any fields that have a DataSource-defined [valueMap](DataSourceField.md#attr-datasourcefieldvaluemap) will have the mapped value exported instead. This is similar to the client-side treatment of valueMaps, except that the defaults are reversed.

For `exportData()` calls, if we encounter a field that has an in-record [displayField](DataSourceField.md#attr-datasourcefielddisplayfield) declared _in the DataSource_, by default we export both the underlying value and the display value, so you end up with two columns in the exported data for that field. You can influence this by setting `exportValueFields` explicitly: if set `true` we export only the value field, and if set `false` we export only the display field. Note, the reason for the similar but not identical behavior of this flag between `exportData()` and `exportClientData()` is backwards compatibility.

**Flags**: IR

---
## Attr: DSRequest.parentNode

### Description
For advanced use in integrating trees that [load data on demand](TreeGrid.md#attr-treegridloaddataondemand) with web services, `parentNode` is automatically set in "fetch" DSRequests issued by a databound TreeGrid that is loading children for that `parentNode`.

This is sometimes needed if a web service requires that additional properties beyond the ID of the parentNode must be passed in order to accomplished level-by-level loading. A custom implementation of [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest) can access dsRequest.parentNode and add any such properties to [DSRequest.data](#attr-dsrequestdata).

`parentNode` will also be automatically set by a TreeGrid performing databound reparenting of nodes, as implemented by [TreeGrid.folderDrop](TreeGrid.md#method-treegridfolderdrop).

This property can only be read. There is no meaning to setting this property yourself.

**Flags**: R

---
## Attr: DSRequest.progressiveLoading

### Description
Sets [progressive loading mode](DataSource.md#attr-datasourceprogressiveloading) for this particular request, overriding the OperationBinding- and DataSource-level settings. This setting overrides the [progressiveLoadingThreshold](DataSource.md#attr-datasourceprogressiveloadingthreshold) setting as well, meaning that if `DSRequest.progressiveLoading` is explicitly set to `false` SmartClient won't automatically switch to loading data progressively even if `DataSource.progressiveLoadingThreshold` is exceeded.

Note that this setting applies only to fetch requests - it has no effect if specified on any other kind of request.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)
- [DataSource.progressiveLoadingThreshold](DataSource.md#attr-datasourceprogressiveloadingthreshold)
- [OperationBinding.progressiveLoading](OperationBinding.md#attr-operationbindingprogressiveloading)

**Flags**: IRW

---
## Attr: DSRequest.dataSource

### Description
DataSource this DSRequest will act on.

This property is generally automatically populated, for example when calling [DataSource.fetchData](DataSource.md#method-datasourcefetchdata) the dataSource property is set to the target DataSource.

**Flags**: IR

---
## Attr: DSRequest.useFlatHeaderFields

### Description
Cause the [useFlatFields](#attr-dsrequestuseflatfields) XML serialization behavior to be used for **all** soap headers in the request. See also [DSRequest.headerData](#attr-dsrequestheaderdata).

### Groups

- flatFields

**Flags**: IRW

---
## Attr: DSRequest.exportStreaming

### Description
When exporting to OOXML format (this is the standard file format used by Excel 2007 and later), we default to using streaming mode, for memory efficiency. You can override this for individual exports by setting this flag false. You may wish to do this if you need to grab the spreadsheet object in a DMI and do something with it. The underlying object in use - POI's `SXSSFWorkbook` - is intended for write only and cannot usefully be read.

You can switch off Excel streaming altogether by setting "excel.useStreaming" false in `server.properties`.

Note, OOXML is the only native Excel format that supports streaming: when exporting to the older XLS format, we build the spreadsheet in its entirety in server-side memory before writing it to disk or returning it to the client. This is unlikely to change: streaming the XLS format is impractical bcause it is a self-referential binary format, and in any case the problem of huge exports overflowing JVM memory is less likely to arise with XLS, because it is innately limited to 65535 rows.

**Flags**: IR

---
## Attr: DSRequest.fieldValueExpressions

### Description
A set of key:value pairs, mapping field names to expressions that will be evaluated server-side to derive a value for that field. This property allows for client-driven [Transaction Chaining](../kb_topics/transactionChaining.md#kb-topic-transaction-chaining), with some restrictions for security reasons:

*   Normal [server-side Transaction Chaining settings](OperationBinding.md#attr-operationbindingvalues) for a field take precedence over this property, so server-defined rules cannot be overridden from the client
*   Arbitrary Velocity expressions are not allowed in DSRequests sent from the client (`fieldValueExpressions` is also a valid property on a server-side DSRequest, and normal Velocity expressions _are_ allowed in that case - see the server-side Javadoc for `DSRequest.setFieldValueExpressions()`). For client-originated requests, only the following bindings are allowed - see the [Velocity overview](#kb-topic-velocitysupport) for details of what these values mean:
    *   $currentDate
    *   $currentDateUTC
    *   $transactionDate
    *   $transactionDateUTC
    *   $userId
    *   $masterId - see [DSRequestModifier.value](DSRequestModifier.md#attr-dsrequestmodifiervalue) for details
    *   References to specific fields in prior responses, via $responseData.first and $responseData.last, with or without parameters. For example, **$responseData.first("myDataSource", "fetch")\[0\].myField**. See the [Velocity overview](#kb-topic-velocitysupport) for details of $responseData
    *   References to certain metadata properties of prior responses, via $responses.first and $responses.last, with or without parameters. For example, **$responses.last("myDataSource", "fetch").totalRows**. Note that the only properties allowed in a client-driven `fieldValueExpression` are: "startRow", "endRow", "totalRows" and "status"; this restriction does not apply to server-driven `fieldValueExpressions`. See the Velocity overview for details of $responses
*   Normal [declarative security rules](DataSourceField.md#attr-datasourcefieldeditrequiresrole) apply: if a field is not valid for writing, its `fieldValueExpression` will be ignored. Again, this only applies to client-originated requests.

Note, it is possible to globally disable `fieldValueExpression` in client-originated requests by setting a flag in your `server.properties` file:
```
   dataSource.allowClientFieldValueExpressions: false
```

### Groups

- transactionChaining

**Flags**: IRW

---
## Attr: DSRequest.headerData

### Description
For DataSources using SOAP messaging with a WSDL web service, data to be serialized to form SOAP headers, as a map from the header part name to the data. See [WSRequest.headerData](WSRequest.md#attr-wsrequestheaderdata) for more information.

SOAP headers typically contain request metadata such as a session id for authentication, and so `dsRequest.headerData` is typically populated by [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest), or, for data that applies to every request sent to the server, by [WebService.getHeaderData](WebService.md#method-webservicegetheaderdata).

Note that this only applies to SOAP headers. General HTTP headers for requests may be modified using [RPCRequest.httpHeaders](RPCRequest.md#attr-rpcrequesthttpheaders).

**Flags**: IRW

---
## Attr: DSRequest.dataProtocol

### Description
[DataProtocol](DataSource.md#attr-datasourcedataprotocol) for this particular request.

**Note:** Typically developers should use [operation bindings](DataSource.md#attr-datasourceoperationbindings) to specify an explicit data protocol for a request.

One exception: advanced developers may wish to have a custom [request transformer](DataSource.md#method-datasourcetransformrequest) with entirely client-side handling for some requests. This may be achieved by setting the request's `dataProtocol` to ["clientCustom"](../reference.md#type-dsprotocol) within transformRequest, and also triggering application code which will fire [DataSource.processResponse](DataSource.md#method-datasourceprocessresponse) when complete.

The [DataSource.getDataProtocol](DataSource.md#method-datasourcegetdataprotocol) method may be used to determine what data protocol will be used to handle a specific request based on this property (if set), otherwise the settings at the [operationBinding](OperationBinding.md#attr-operationbindingdataprotocol) or [dataSource](DataSource.md#attr-datasourcedataprotocol) levels.

**Flags**: IRW

---
