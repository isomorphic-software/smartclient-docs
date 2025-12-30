# RestDataSource Documentation

[← Back to API Index](../reference.md)

---

## Class: RestDataSource

*Inherits from:* [DataSource](DataSource.md#class-datasource)

### Description
The RestDataSource implements the 4 core DataSource operations using a simple protocol of XML or JSON requests and responses sent over HTTP, which can be easily fulfilled by any HTTP server technology.

RestDataSource is named for the [REST](http://www.google.com/search?hl=en&q=REST+HTTP) (REpresentational State Transfer) pattern, which in brief says that simple messages passed over HTTP is a sufficient protocol for many web applications, without the need for further protocols such as WSDL or SOAP.

A RestDataSource is used just like a normal DataSource. RestDataSources are pre-configured, using the general-purpose databinding facilities of DataSources, to expect a particular format for responses and to send requests in a specific format. These request and response formats represent Isomorphic's recommended best practices for binding SmartClient to backends which do not already support a similar, pre-existing request and response format and where the SmartClient Java Server cannot be used.

If you have a pre-existing REST or WSDL service which is difficult to change, consider adapting SmartClient to the existing service instead, by starting with a normal [DataSource](DataSource.md#class-datasource) and using the [client-side data integration](../kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration) facilities to create a mapping between SmartClient's [DSRequest](../reference.md#object-dsrequest) and [DSResponse](DSResponse.md#class-dsresponse) objects and the message formats of your existing services. **NOTE**: do **not** begin this process by creating or subclassing RestDataSource; for a **pre-existing** service which is unrelated to the protocol documented for RestDataSource, start by configuring or subclassing [DataSource](DataSource.md#class-datasource) instead.

RestDataSource is typically used with PHP, Ruby, Python, Perl or custom server technologies, and represents an alternative to installing the SmartClient Server in a Java technology stack, or using [WSDL-based binding](../kb_topics/wsdlBinding.md#kb-topic-wsdl-binding) with .NET or other WSDL-capable technologies. Note that SmartClient Server also provides built-in support for the REST protocol via its RESTHandler servlet; this is primarily to allow non-SmartClient clients to make use of DataSource operations. If you particularly wished to do so, you could use RestDataSource to make a SmartClient app talk to the SmartClient Server using REST rather than the proprietary wire format normally used when communicating with SmartClient Server (this is how we are able to write automated tests for the RESTHandler servlet). However, doing this provides no benefit, imposes a number of inconveniences, and makes a handful of server-based features less useful ([field-level declarative security](DataSourceField.md#attr-datasourcefieldviewrequiresauthentication), for example), so we strongly recommend that you do _not_ do this; it is only mentioned here for completeness while we are discussing REST.

The request and response formats used by the RestDataSource allow for many of the available features of SmartClient's databinding system to be used, including data paging, searching & sorting, [long transactions](DSRequest.md#attr-dsrequestoldvalues), [automatic cache sync](ResultSet.md#class-resultset), [relogin](../kb_topics/relogin.md#kb-topic-relogin) and [queuing](RPCManager.md#classmethod-rpcmanagerstartqueue). However, advanced features such as [uploading / binary fields](../kb_topics/upload.md#kb-topic-uploading-files) and [export](ListGrid_2.md#method-listgridexportdata) aren't available with RestDataSource and need to be re-implemented as needed. Most, though not all, [server-based features](../kb_topics/iscServer.md#kb-topic-smartclient-server-summary) are still available when using RestDataSource, as long as you are also using the RESTHandler servlet that is part of SmartClient Server. However, as noted above, this approach is not recommended; if you are using Isomorphic technology both client- and server-side, it makes more sense to use the proprietary wire format.

**RestDataSource and binary data**

Binary data in a response provided to a RestDataSource must be delivered as valid XML or JSON Strings. Once delivered to the browser as Strings, there is no way to trigger the browser's "Save As" dialog to download the data, and in most cases no way to trigger other helper applications that might be launched to handle binary data (such as Excel or a PDF viewer). Hence for binary it usually makes sense to make a direct request via RPCManager.sendRequest() with downloadResult:true, separate from RestDataSource.

If you are using the SmartClient Server included in Pro, Power end Enterprise to handle your REST requests server-side, there is transparent support for conversion between Java `InputStream`s representing binary data, and Strings containing that binary data encoded using the [Base64 algorithm](http://en.wikipedia.org/wiki/Base64). Thus, on the server, the binary data is in its raw binary form, with transparent conversion to or from Base64 for messages to or from the REST client.

Examples

**XML formatted responses:**

RestDataSource expects a response like the following in response to a "fetch" request:

```
 <response>
    <status>0</status>
    <startRow>0</startRow>
    <endRow>76</endRow>
    <totalRows>546</totalRows>
    <data>
      <record>
          <field1>value</field1>
          <field2>value</field2>
      </record>
      <record>
          <field1>value</field1>
          <field2>value</field2>
      </record>
      ... 76 total records ... 
    </data>
 </response>
 
```
The `<status>` element indicates whether the fetch operation was successful (see [statusCodes](../kb_topics/statusCodes.md#kb-topic-statuscodes)).

The `<data>` element contains a list of record nodes, each of which represents a record returned by the server. The optional `<startRow>`, `<endRow>` and `<totalRows>` elements are needed only if data paging is in use, and populate the [startRow](DSResponse.md#attr-dsresponsestartrow), [endRow](DSResponse.md#attr-dsresponseendrow) and [totalRows](DSResponse.md#attr-dsresponsetotalrows) properties of the [DSResponse](DSResponse.md#class-dsresponse).

Note: for a more compact format, simple field values may be specified on record nodes directly as attributes - in this case a record element might be structured like this:

```
     <record field1="value" field2="value" />
 
```

Note that a RestDataSource will bypass browser caching of all responses by default. See [DataSource.preventHTTPCaching](DataSource.md#attr-datasourcepreventhttpcaching).

Successful "add" or "update" request responses are similar in format - in this case the data element would be expected to contain a single record object containing the details of the record, as saved on the server.

The response from a "remove" operation would again include status and data elements, but in this case, only the primary key field value(s) of the removed record would be expected to be present under the data element.

If a validation failure occurred on the server, the response would have status set to [RPCResponse.STATUS_VALIDATION_ERROR](RPCResponse.md#classattr-rpcresponsestatus_validation_error) \[`-4`\], and any validation errors could be included as per-field sub-elements of an "errors" element. For a validation error, the response is not expected to contain any `<data>` element.

A response showing a validation error might look like this:

```
 <response>
    <status>-4</status>
    <errors>
      <field1>
          <errorMessage>A validation error occurred for this field</errorMessage>
      </field1>
    </errors>
 </response>
 
```

An unrecoverable error, such as an unexpected server failure, can be flagged by setting `<status>` to -1 and setting `<data>` to an error message. In this case the `<errors>` element is not used (it's specific to validation errors). An unrecoverable error causes all response processing to be skipped and [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror) to be invoked, which by default will show the provided error message as an alert using [isc.warn](isc.md#staticmethod-iscwarn).

**JSON formatted responses:**

JSON format responses are expected to contain the same data / meta-data as XMLresponses, encapsulated in a simple object with a `"response"` attribute.  
The response to a "fetch" request would therefore have this format:  

```
 {
    "response": {
       "status": 0,
       "startRow": 0,
       "endRow": 76,
       "totalRows": 546,
       "data": [
           {"field1": "value", "field2": "value"},
           {"field1": "value", "field2": "value"},
           ... 76 total records ...
       ]
    }
 }
 
```
The structure successful for "add", "update" and "remove" responses would be similar, though the data array would be expected to contain only a single object, representing the values as saved. This allows the server to return values such as an auto-generated sequence primaryKey, a last modified timestamp, or similar server-generated field values.

For a remove, only the value for the primaryKey field\[s\] would be required.

For a validation error, the `status` attribute would be set to [RPCResponse.STATUS_VALIDATION_ERROR](RPCResponse.md#classattr-rpcresponsestatus_validation_error) \[`-4`\], and errors would be specified in the `errors` attribute of the response. For example:

```
 {    "response":
      {   "status": -4,
          "errors":
              {   "field1": {"errorMessage": "A validation error on field1"},
                  "field2": {"errorMessage": "A validation error on field2"}
              }
      }
 }
 
```
An array of errors may also be returned for a single field, like this:
```
 {    "response":
      {   "status": -4,
          "errors":
              {   "field1": [
                      {"errorMessage": "First error on field1"},
                      {"errorMessage": "Second error on field1"}
                  ]
              }
      }
 }
 
```

As with the XML format above, an unrecoverable error is indicated by setting the `status` attribute to -1 and the `data` property to the error message.

**Responses with related updates**

Related updates is a way to communicate additional changes that occur as a consequence of the current DSResponse succeeding, such as changes to other records in the same DataSource or to records from unrelated DataSources. Related updates can be attached to main response via `DSResponse.addRelatedUpdate(dsResponse)` server-side API, see its docs for more details. RestDataSource supports this on the client, [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches) will be called for all related updates found in response. Here's schematic example of how they look like:

```
 <response>
     ... normal response ...
     <relatedUpdates>
         <response>
              ... normal response ...
         </response>
         <response>
              ... normal response ...
         </response>
     </relatedUpdates>
 </response>
 
```
same in JSON format
```
 {
   ... normal response ...,
   relatedUpdates: [
     {
       ... normal response ...
     },
     {
       ... normal response ...
     }
   ]
 }
 
```

**Server inbound data formats**

The format of data sent to the server is determined by the [OperationBinding.dataProtocol](OperationBinding.md#attr-operationbindingdataprotocol) specified for the operation. Request data is sent as parameters if the format is specified as `"getParams"` or `"postParams"`.

In this case, the parameters sent to the server will consist of the DSRequest's data, and any parameters explicitly specified on the DSRequest object (as [RPCRequest.params](RPCRequest.md#attr-rpcrequestparams).  
If [RestDataSource.sendMetaData](#attr-restdatasourcesendmetadata) is true, the DSRequest meta data properties will also be present as parameters, prefixed with [RestDataSource.metaDataPrefix](#attr-restdatasourcemetadataprefix).

Example URL constructed with the metaDataPrefix set to `"_"` (the default):

   `_[dataURL]_?field1=value1&_operationType=fetch&_startRow=0&_endRow=50&_sortBy=-field2&_dataSource=dsName`

In this case the server would be able to separate the request's data from the meta data via the `"_"` prefix.

If data is sent to the server via the `"postMessage"` dataProtocol, the data will be serialized as an XML or JSON message according to the `dataFormat` setting. Both XML and JSON messages will contain request metadata such as startRow and endRow, and will appear exactly as though the subset of the [DSRequest](../reference.md#object-dsrequest) that is meaningful to the server had been passed to [DataSource.xmlSerialize](DataSource.md#method-datasourcexmlserialize) or [JSON.encode](JSON.md#classmethod-jsonencode) respectively.

An example of an XML message might look like this:

```
    <request>
        <data>
            <countryCode>US</countryCode>
            <countryName>Edited Value</countryName>
            <capital>Edited Value</capital>
            <continent>Edited Value</continent>
        </data>
        <dataSource>countryDS</dataSource>
        <operationType>update</operationType>
    </request>
 
```
An example of an XML message for a fetch operation passing simple criteria:
```
    <request>
        <data>
            <continent>North America</continent>
        </data>
        <dataSource>countryDS</dataSource>
        <operationType>fetch</operationType>
        <startRow>0</startRow>
        <endRow>75</endRow>
        <componentId>worldGrid</componentId>
        <textMatchStyle>exact</textMatchStyle>
    </request>
 
```
And an example of an XML message for a fetch operation passing AdvancedCriteria:
```
    <request>
        <data>
            <_constructor>AdvancedCriteria</_constructor>
            <operator>or</operator>
            <criteria>
                <criterion>
                    <fieldName>continent</fieldName>
                    <operator>equals</operator>
                    <value>North America</value>
                </criterion>
                <criterion>
                    <operator>and</operator>
                    <criteria>
                        <criterion>
                            <fieldName>continent</fieldName>
                            <operator>equals</operator>
                            <value>Europe</value>
                        </criterion>
                        <criterion>
                            <fieldName>population</fieldName>
                            <operator>greaterThan</operator>
                            <value>50000000</value>
                        </criterion>
                    </criteria>
                </criterion>
            </criteria>
        </data>
        <dataSource>countryDS</dataSource>
        <operationType>fetch</operationType>
        <startRow>0</startRow>
        <endRow>75</endRow>
        <componentId>worldGrid</componentId>
    </request>
 
```
An example of an XML message for a fetch operation when using [server-side summaries](../kb_topics/serverSummaries.md#kb-topic-server-summaries):
```
    <request>
        <data></data>
        <dataSource>countryDS</dataSource>
        <operationType>fetch</operationType>
        <summaryFunctions>
            <pk>count</pk>
        </summaryFunctions>
        <groupBy>member_g8</groupBy>
    </request>
 
```
JSON messages are just the plain JSON form of the structures shown in the above XML examples. The advanced criteria XML example above but in JSON form:
```
 {
     data: {
         _constructor: "AdvancedCriteria",
         operator: "or",
         criteria: [
             {
                 fieldName: "continent",
                 operator: "equals",
                 value: "North America
             },
             {
                 operator: "and", criteria: [
                     {
                         fieldName: "continent",
                         operator: "equals",
                         value: "Europe"
                     },
                     {
                         fieldName: "population",
                         operator: "greaterThan",
                         value: 50000000
                     }
                 ]
             }
         ]
     }
     dataSource: "countryDS",
     operationType: "fetch",
     startRow: 0,
     endRow: 75,
     componentId: "worldGrid"
 }
 
```
The [default OperationBindings](#attr-restdatasourceoperationbindings) for a RestDataSource specify dataProtocol as "getParams" for the fetch operation, and "postParams" for update, add and remove operations. Note that most webservers impose a limit on the maximum size of GET requests (specifically, on the size of the request URL + HTTP headers). Using dataProtocol:"getParams" for "fetch" operations that involve complex AdvancedCriteria will result in a JSON serialization of the AdvancedCriteria in the request URL, and when combined with large cookies this can easily overflow the default limits on certain webservers (see [http://stackoverflow.com/questions/686217/maximum-on-http-header-values](http://stackoverflow.com/questions/686217/maximum-on-http-header-values)). For this reason, we recommend that you use the "postMessage" protocol whenever you are intending to use AdvancedCriteria with RestDataSource.

**Date, time and datetime values**

Date, time and datetime values must be communicated using XML Schema format, as in the following examples:

```
   <dateField>2007-04-22</dateField>
   <timeField>11:07:13</timeField>
   <dateTimeField>2007-04-22T11:07:13</dateTimeField>
   <dateTimeField>2007-04-22T11:07:13.582</dateTimeField>
 
```

And the equivalent in JSON:

```
   dateField: "2007-04-22"
   timeField: "11:07:13"
   dateTimeField: "2007-04-22T11:07:13"
   dateTimeField: "2007-04-22T11:07:13.582"
 
```

Both RestDataSource on the client-side and the RESTHandler servlet on the server side automatically handle encoding and decoding temporal values using these formats. Both also handle datetime formats including or excluding milliseconds automatically. When encoding, both honor the [DataSource.trimMilliseconds](DataSource.md#attr-datasourcetrimmilliseconds) setting on the DataSource, falling back to the `server.properties` setting `rest.trimMilliseconds`; when decoding, both detect whether or not to try to parse milliseconds based on the string they receive.

Fields of type "date" and "time" are considered to hold logical date and time values, as discussed in the [date and time handling article](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage), and are not affected by timezones. Fields of type "datetime" will be converted to UTC on the client side by RestDataSource, and will be sent back down to the client as UTC by the server-side RESTHandler. We recommend that your own REST client and/or server code do the same thing (ie, transmit all datetime values in both directions as UTC). Note that the examples given above give no timezone information, and will be treated by the SmartClient Server as UTC values. If you wish to work with datetime values in a particular timezone, use a format like this:

```
   <dateField>2007-04-22T11:07:13-0800</dateField>
   <dateField>2012-11-19T22:12:04+0100</dateField>
 
```

And the equivalent in JSON:

```
   dateTimeField: "2007-04-22T11:07:13-0800"
   dateTimeField: "2012-11-19T22:12:04+0100"
 
```

**NOTE:** Although we refer above to XML Schema format, the format used for specifying timezone offset is slightly different from XML Schema - as shown in the above examples, you specify "+HHMM" or "-HHMM", as opposed to the XML Schema format which requires a ":" character between the hours and minutes. The reason for this difference is simply that the Java SimpleDateFormat class imposes it.

**RestDataSource queuing support**

RestDataSource supports [queuing](RPCManager.md#classmethod-rpcmanagerstartqueue) of DSRequests. This allows you to send multiple requests to the server in a single HTTP turnaround, thus minimizing network traffic and allowing the server to treat multiple requests as a single transaction, if the server is able to do so (in Power Edition and above, the SmartClient Server transparently supports grouping multiple REST requests in a queue into a single database transaction when using one of the built-in DataSource types). Note that you can disable queuing support with the [RestDataSource.disableQueuing](#attr-restdatasourcedisablequeuing) flag.

If you want to use queuing with RestDataSource, you must use the "postMessage" dataProtocol with either XML or JSON dataFormat. Message format is similar to the non-queued examples shown earlier: it is simply extended to cope with the idea of multiple DSRequests encapsulated in the message.

An example of the XML message sent from RestDataSource to the server for two update requests combined into a queue, using XML dataFormat:

```
 <transaction>
     <operations>
         <request>
             <data>
                 <pk>1</pk>
                 <countryName>Edited Value</countryName>
                 <capital>Edited Value</capital>
                 <continent>Edited Value</continent>
             </data>
             <dataSource>countryDS</dataSource>
             <operationType>update</operationType>
         </request>
         <request>
             <data>
                 <pk>2</pk>
                 <capital>Edited Value</capital>
                 <population>123456</population>
             </data>
             <dataSource>countryDS</dataSource>
             <operationType>update</operationType>
         </request>
     </operations>
 <transaction>
 
```
And the same message in JSON format:
```
 { 
     transaction: { 
         operations: [{
             dataSource:"countryDS", 
             operationType:"update", 
             data: {
                 pk: 1
                 countryName: "Edited Value",
                 capital: "Edited Value",
                 continent: "Edited Value"
             }
         }, {
             dataSource:"countryDS", 
             operationType:"update", 
             data: {
                 pk: 2,
                 capital: "Edited Value",
                 popuilation: 123456
             }
         }]
     }
 }
 
```
RestDataSource expects the response to a queue of requests to be a queue of responses in the same order as the original requests. Again, the message format is very similar to the unqueued REST format, it just has an outer container construct. Note also that the individual DSResponses in a queued response have an extra property, [`queueStatus`](DSResponse.md#attr-dsresponsequeuestatus). This allows each individual response to determine whether the queue as a whole succeeded. For example, if the first update succeeded but the second failed validation, the first response would have a `status` of 0, but a `queueStatus` of -1, while the second response would have both properties set to -1.

The update queue example given above would expect a response like this (in XML):

```
 <responses>
     <response>
         <status>0</status>
         <queueStatus>0</queueStatus>
         <data>
             <record>
                 <countryName>Edited Value</countryName>
                 <gdp>1700.0</gdp>
                 <continent>Edited Value</continent>
                 <capital>Edited Value</capital>
                 <pk>1</pk>
             </record>
         </data>
     </response>
     <response>
         <status>0</status>
         <queueStatus>0</queueStatus>
         <data>
             <record>
                 <countryName>United States</countryName>
                 <gdp>7247700.0</gdp>
                 <continent>North America</continent>
                 <independence>1776-07-04</independence>
                 <capital>Washington DC</capital>
                 <pk>2</pk>
                 <population>123456</population>
             </record>
         </data>
     </response>
 </responses>
 
```
And in JSON:
```
 [
 {
     "response": {
         "queueStatus": 0,
         "status": 0, 
         "data": [{
             "countryName": "Edited Value",
             "gdp": 1700.0,
             "continent": "Edited Value",
             "capital": "Edited Value",
             "pk": 1
         }]
     }
 },
 {
     "response": {
         "queueStatus": 0,
         "status": 0,
         "data": [{
             "countryName": "United States",
             "gdp": 7247700.0,
             "continent": "North America",
             "independence": "1776-07-04",
             "capital": "Washington DC",
             "pk": 2,
             "population": 123456
         }]
     }
 }
 ]
 
```
**Hierarchical (Tree) data:**

To create a hierarchical DataSource, in the DataSource's `fields` array, a field must be specified as the parent id field - the field which will contain a pointer to the id of each node's parent. This can be achieved by setting the [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) and the [DataSourceField.rootValue](DataSourceField.md#attr-datasourcefieldrootvalue) attributes on the field definition. For example:

```
 RestDataSource.create({
    ID:"supplyItem",
    fields : [
        {name:"itemId", type:"sequence", primaryKey:true},
        {name:"parentId", type:"integer", foreignKey:"supplyItem.itemId", rootValue:0},
        ...
    ]
 });
 
```
Tree Data is then treated on the server as a flat list of records linked by parent id.

Tree data is typically displayed using a dataBound [TreeGrid](TreeGrid.md#class-treegrid) component. TreeGrids automatically create a [ResultTree](ResultTree.md#class-resulttree) data object, which requests data directly from the DataSource. ResultTrees load data on demand, only requesting currently visible (open) nodes from the server. This is handled by including a specified value for the parent id field in the request criteria.  
To implement a standard load-on-demand tree RestDataSource back end, you should therefore simply return the set of nodes that match the criteria passed in. For example, if your DataSource was defined as the "supplyItem" code snippet above, a fetch request for all children of a node with `itemId` set to `12` would have `"parentId"` set to `12` in the request criteria. A valid response would then contain all the records that matched this criteria. For example:

```
 <response>
    <status>0</status>
    <data>
      <record>
          <itemId>15</itemId>
          <parentId>12</parentId>
      </record>
      <record>
          <itemId>16</itemId>
          <parentId>12</parentId>
      </record>
    </data>
 </response>
 
```
The structure of responses for Add, Update and Delete type requests will be the same regardless of whether the data is hierarchical. However you should be aware that the underlying data storage may need to be managed slightly differently in some cases.

Specifically, Add and Update operations may change the structure of the tree by returning a new parent id field value for the modified node. Depending on how your data is stored you may need to include special back-end logic to handle this.

Also, if a user deletes a folder within a databound tree, any children of that folder will also be dropped from the tree, and can be removed from the back-end data storage.

Note: For a general overview of binding components to Tree structured data, see [Tree Databinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding).

---
## Attr: RestDataSource.dataURL

### Description
Default URL to contact to fulfill all DSRequests. RestDataSources also allow per-operationType dataURLs to be set via

*   [RestDataSource.fetchDataURL](#attr-restdatasourcefetchdataurl)
*   [RestDataSource.addDataURL](#attr-restdatasourceadddataurl)
*   [RestDataSource.updateDataURL](#attr-restdatasourceupdatedataurl)
*   [RestDataSource.removeDataURL](#attr-restdatasourceremovedataurl)

**NOTE:**: when using [queuing](RPCManager.md#classmethod-rpcmanagerstartqueue) with RestDataSource, an HTTP request containing mixed [operationTypes](DSRequest.md#attr-dsrequestoperationtype) (such as a mixture of "add", "update" and "remove" operations resulting from [Grid Mass Editing](ListGrid_1.md#attr-listgridautosaveedits)) can only go to one URL, so you should not set distinct URLs for each `operationType`; doing so will break queuing of mixed operationTypes: multiple requests will be sent to distinct URLs, and a warning logged.

**Flags**: IR

---
## Attr: RestDataSource.dataProtocol

### Description
Rather than setting [DataSource.dataProtocol](DataSource.md#attr-datasourcedataprotocol), to control the format in which inputs are sent to the dataURL, you must specify a replacement [OperationBinding](OperationBinding.md#class-operationbinding) and specify [OperationBinding.dataProtocol](OperationBinding.md#attr-operationbindingdataprotocol) on that `operationBinding`.

This is because `RestDataSource` specifies default `operationBindings` for all operationTypes - see [RestDataSource.operationBindings](#attr-restdatasourceoperationbindings).

### Groups

- clientDataIntegration
- serverDataIntegration

**Flags**: IR

---
## Attr: RestDataSource.removeDataURL

### Description
Custom [dataURL](DataSource.md#attr-datasourcedataurl) for [DSRequests](../reference.md#object-dsrequest) with [operationType](DSRequest.md#attr-dsrequestoperationtype) "remove".

See [RestDataSource.dataURL](#attr-restdatasourcedataurl) to configure a single URL for all requests, which is required to support [RPCManager.startQueue](RPCManager.md#classmethod-rpcmanagerstartqueue).

**Flags**: IR

---
## Attr: RestDataSource.fetchDataURL

### Description
Custom [dataURL](DataSource.md#attr-datasourcedataurl) for [DSRequests](../reference.md#object-dsrequest) with [operationType](DSRequest.md#attr-dsrequestoperationtype) "fetch".

Use [RestDataSource.dataURL](#attr-restdatasourcedataurl) to configure a single URL for all requests, which is required to support [RPCManager.startQueue](RPCManager.md#classmethod-rpcmanagerstartqueue).

**Flags**: IR

---
## Attr: RestDataSource.updateDataURL

### Description
Custom [dataURL](DataSource.md#attr-datasourcedataurl) for [DSRequests](../reference.md#object-dsrequest) with [operationType](DSRequest.md#attr-dsrequestoperationtype) "update".

See [RestDataSource.dataURL](#attr-restdatasourcedataurl) to configure a single URL for all requests, which is required to support [RPCManager.startQueue](RPCManager.md#classmethod-rpcmanagerstartqueue).

**Flags**: IR

---
## Attr: RestDataSource.metaDataPrefix

### Description
If [RestDataSource.sendMetaData](#attr-restdatasourcesendmetadata) is true, this attribute is used to specify the prefix to apply to 'meta data' properties when assembling parameters to send to the server. Applies to operations where OperationBinding.dataProtocol is set to `"getParams"` or `"postParams"` only.

**Flags**: IR

---
## Attr: RestDataSource.jsonSuffix

### Description
Allows you to specify an arbitrary suffix string to apply to all json format responses sent from the server to this application. The client will expect to find this suffix on any JSON response received for this DataSource, and will strip it off before evaluating the response text.

The default suffix is "//isc\_JSONResponseEnd".

### See Also

- [RestDataSource.jsonPrefix](#attr-restdatasourcejsonprefix)

**Flags**: IRW

---
## Attr: RestDataSource.sendMetaData

### Description
Should operation meta data be included when assembling parameters to send to the server? If true, meta data parameters will be prefixed with the [RestDataSource.metaDataPrefix](#attr-restdatasourcemetadataprefix).  
Applies to operations where OperationBinding.dataProtocol is set to `"getParams"` or `"postParams"` only.

**Flags**: IR

---
## Attr: RestDataSource.addDataURL

### Description
Custom [dataURL](DataSource.md#attr-datasourcedataurl) for [DSRequests](../reference.md#object-dsrequest) with [operationType](DSRequest.md#attr-dsrequestoperationtype) "add".

See [RestDataSource.dataURL](#attr-restdatasourcedataurl) to configure a single URL for all requests, which is required to support [RPCManager.startQueue](RPCManager.md#classmethod-rpcmanagerstartqueue).

**Flags**: IR

---
## Attr: RestDataSource.recordXPath

### Description
For RestDataSources, by default, either the [RestDataSource.xmlRecordXPath](#attr-restdatasourcexmlrecordxpath) or [RestDataSource.jsonRecordXPath](#attr-restdatasourcejsonrecordxpath) is used based on the [RestDataSource.dataFormat](#attr-restdatasourcedataformat) setting.

Note that you can also apply record xpath binding via [OperationBinding.recordXPath](OperationBinding.md#attr-operationbindingrecordxpath).

**Flags**: IRW

---
## Attr: RestDataSource.operationBindings

### Description
RestDataSource OperationBindings set to specify default dataProtocol per operationType. Default databindings are:
```
   operationBindings : [
     {operationType:"fetch", dataProtocol:"getParams"},
     {operationType:"add", dataProtocol:"postParams"},
     {operationType:"remove", dataProtocol:"postParams"},
     {operationType:"update", dataProtocol:"postParams"} 
   ],
 
```
If you are integrating with a [REST](#class-restdatasource) server that requires the more obscure [RPCRequest.httpMethod](RPCRequest.md#attr-rpcrequesthttpmethod)s of "PUT", "DELETE" or "HEAD", you can specify these httpMethod settings via [OperationBinding.requestProperties](OperationBinding.md#attr-operationbindingrequestproperties). dataProtocol settings that mention "GET" or "POST" are compatible with these additional HTTP methods as well. Typical [operationBindings](DataSource.md#attr-datasourceoperationbindings) for a REST server that uses "PUT" and "DELETE" are as follows:
```
   operationBindings:[
     {operationType:"fetch", dataProtocol:"getParams"},
     {operationType:"add", dataProtocol:"postParams"},
     {operationType:"remove", dataProtocol:"getParams", requestProperties:{httpMethod:"DELETE"}},
     {operationType:"update", dataProtocol:"postParams", requestProperties:{httpMethod:"PUT"}}
   ],
 
```

Note that dataProtocol:"postMessage" is always used when [queuing](RPCManager.md#classmethod-rpcmanagerstartqueue) is used to send multiple DSRequests to the server as a single HttpRequest. See [RestDataSource](#class-restdatasource) docs, "queuing support". We also recommend that you use the "postMessage" protocol whenever you are intending to use AdvancedCriteria with RestDataSource - this is discussed in the section "Server inbound data format" in the [RestDataSource overview](#class-restdatasource).

**Flags**: IR

---
## Attr: RestDataSource.prettyPrintJSON

### Description
When using dataFormat:"json" and dataProtocol:"postMessage" should we use the [JSONEncoder.prettyPrint](JSONEncoder.md#attr-jsonencoderprettyprint) feature to enable indented, highly readable JSON messages.

True by default because the bandwidth involved is generally negligible and the benefits for troubleshooting are key.

**Flags**: IR

---
## Attr: RestDataSource.disableQueuing

### Description
If set, disables [request queuing](RPCManager.md#classmethod-rpcmanagerstartqueue) for this RestDataSource.

**Flags**: IRW

---
## Attr: RestDataSource.xmlNamespaces

### Description
When [RestDataSource.dataFormat](#attr-restdatasourcedataformat) is "xml", `xmlNamespaces` configures the set of namespace prefixes that are added to the document element of the XML message sent to the server. Format is the same as [DataSource.xmlNamespaces](DataSource.md#attr-datasourcexmlnamespaces).

By default, the "xsi" prefix is bound to "http://www.w3.org/2001/XMLSchema-instance" in order to allow explicit null values in Records to be sent for [fields declared nillable](DataSourceField.md#attr-datasourcefieldnillable). Set to null to avoid any prefixes being added.

### See Also

- [DataSourceField.nillable](DataSourceField.md#attr-datasourcefieldnillable)

**Flags**: IR

---
## Attr: RestDataSource.jsonPrefix

### Description
Allows you to specify an arbitrary prefix string to apply to all json format responses sent from the server to this application. The client will expect to find this prefix on any JSON response received for this DataSource, and will strip it off before evaluating the response text.

The default prefix is "`<SCRIPT>`//'\\"\]\]>>isc\_JSONResponseStart>>".

The inclusion of such a prefix ensures your code is not directly executable outside of your application, as a preventative measure against [javascript hijacking](http://www.google.com/search?q=javascript+hijacking).

You can switch off JSON wrapping altogether by setting both this and [RestDataSource.jsonSuffix](#attr-restdatasourcejsonsuffix) to empty strings.

If you are using SmartClient Server's RESTHandler servlet, see the server-side Javadocs for details of how to change the way JSON wrapping works on the server side.

### See Also

- [RestDataSource.jsonSuffix](#attr-restdatasourcejsonsuffix)

**Flags**: IRW

---
## Attr: RestDataSource.xmlRecordXPath

### Description
`recordXPath` mapping to the data node of XML returned by the server. Applies if this.dataFormat is set to `"xml"`.  
The default value will pick up data from a response structured as follows:  
```
 <response>
    <status>0</status>
    <data>
      <record>
          <field1>value</field1>
          <field2>value</field2>
      </record>
      <record>
          <field1>value</field1>
          <field2>value</field2>
      </record>
    </data>
 </response>
 
```

**Flags**: IR

---
## Attr: RestDataSource.dataFormat

### Description
Expected format for server responses. RestDataSources handle `"json"` and `"xml"` format responses by default. See class overview documentation for examples of responses in each format.

**Flags**: IR

---
## Attr: RestDataSource.jsonRecordXPath

### Description
`recordXPath` mapping to the data node of json returned by the server. Applies if this.dataFormat is set to `"json"`  
The default value will pick up data from a response structured as follows:  
```
 {response:
  {status:0,
   data:[
      {field1:"value", field2:"value"},
      {field1:"value", field2:"value"}
   ]
 }
 
```

**Flags**: IR

---
## Method: RestDataSource.transformRequest

### Description
RestDataSource overrides transformRequest and handles serializing the request in the appropriate format (determined by the specified [dataProtocol](OperationBinding.md#attr-operationbindingdataprotocol)), including the submitted [data](DSRequest.md#attr-dsrequestdata) as well as the meta data parameters, which may include -  
[dataSource](DSRequest.md#attr-dsrequestdatasource), [operationType](DSRequest.md#attr-dsrequestoperationtype), [operationId](DSRequest.md#attr-dsrequestoperationid);  
[startRow](DSRequest.md#attr-dsrequeststartrow) and [endRow](DSRequest.md#attr-dsrequestendrow) (for fetches);  
[sortBy](DSRequest.md#attr-dsrequestsortby) and [textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) (for fetches);  
[oldValues](DSRequest.md#attr-dsrequestoldvalues) (for update and remove operations);  
and possibly [componentId](DSRequest.md#attr-dsrequestcomponentid).

If you override this method in order to add additional data to the DSRequest, you must call [Super()](Class.md#method-classsuper) or you will remove the functionality provided by RestDataSource. For example:

```
    transformRequest : function (dsRequest) {
        // modify dsRequest.data here, for example, add fixed criteria
        dsRequest.data.userId = myApplication.getCurrentUserId();
  
        return this.Super("transformRequest", arguments);
    }
 
```

See [RestDataSource overview](#class-restdatasource) for a description of the standard formatting applied to requests.

---
## Method: RestDataSource.transformResponse

### Description
RestDataSource implements transformResponse in order to extract data and meta-data properties from server responses, as described in the [RestDataSource overview](#class-restdatasource).

You can override `transformResponse()` in order to further modify the response, but if you do so, call [Super()](Class.md#method-classsuper) as shown below or you will wipe out the built-in response processing behavior of RestDataSource.

```
 transformResponse : function (dsResponse, dsRequest, data) {        
     var dsResponse = this.Super("transformResponse", arguments);
     // ... do something to dsResponse ...
     return dsResponse;
 }
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | default DSResponse derived from the response data |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | DSRequest object that initiated this request |
| data | [XMLDocument](../reference.md#type-xmldocument)|[JSON](#type-json) | false | — | XML document or JSON objects returned by the web service |

### Returns

`[DSResponse](#type-dsresponse)` — response derived

---
