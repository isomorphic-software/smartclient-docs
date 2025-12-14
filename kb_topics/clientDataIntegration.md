# Client-side Data Integration

[← Back to API Index](../reference.md)

---

## KB Topic: Client-side Data Integration

### Description
SmartClient supports declarative, XPath-based binding of visual components to any server capable of returning XML or JSON responses over HTTP, without the need for the [SmartClient server](serverDataIntegration.md#kb-topic-server-datasource-integration).

This approach is called Client-Side Data Integration, which means:

*   You [create DataSources](dataSourceDeclaration.md#kb-topic-creating-datasources) in JavaScript which describe the data to be loaded and manipulated in the user interface. The JavaScript that creates these DataSources may be dynamically generated and/or existing metadata may be [imported](metadataImport.md#kb-topic-metadata-import).
*   You configure DataSources, via property and method overrides, to send appropriate HTTP requests to your server, and to parse HTTP responses from your server, in order to fulfill the 4 core operations of the [DataSource Protocol](dataSourceOperations.md#kb-topic-datasource-operations).
*   These DataSources are then bound to [databinding-capable UI components](../reference.md#interface-databoundcomponent), which can provide a variety of complete user interactions (form-based editing, grid-based editing, load on demand, ..) based on these 4 core operations

#### Approaches and platforms

**REST integration with RestDataSource (preferred)**

The [RestDataSource](../classes/RestDataSource.md#class-restdatasource) provides a complete XML or JSON-based protocol that supports all of the features of SmartClient's databinding layer (data paging, queuing/batching of requests for transactions, nested AdvancedCriteria, server-side validation errors, automatic cache synchronization, etc). To use the RestDataSource, simply write server code that can parse RestDataSource requests and produce the required responses; example requests and responses are [provided](../classes/RestDataSource.md#class-restdatasource).

The SmartClient public wiki contains examples of integration with [.NET's ASP.NET MVC](http://wiki.smartclient.com/display/Main/Integrating+with+ASP.Net+MVC) as well as [PHP with Doctrine](https://isomorphic.atlassian.net/wiki/spaces/Main/pages/524974/Integrating+with+PHP+Doctrine).

#### Consuming Existing XML and JSON formats

If you have pre-existing XML or JSON formats, SmartClient DataSources can be configured to work with them. However, **only use this approach if you are unable to modify a pre-existing protocol**. If you have a choice, use RestDataSource.

In particular, if you are choosing between tools that can automatically generate a REST service from an API vs using the pre-built RestDataSource protocol, **definitely use RestDataSource**. Automatically generated REST interfaces will not handle the needs of a modern GUI, such as transactional/batched saves and user-ready validation error messages. For a deeper discussion, see [this FAQ](http://forums.smartclient.com/showthread.php?t=8159#aExistingRest).

Specifically for pre-existing WSDL web services, see the discussion of WSDL Integration below instead.

To display XML or JSON from a pre-existing service in a visual component such as a ListGrid, you bind the component to a [DataSource](../classes/DataSource.md#class-datasource) which provides the [URL](../classes/DataSource.md#attr-datasourcedataurl) of the service, as well as a declaration of how to form inputs to the service and how to interpret service responses as DataSource records.

An XPath expression, the [recordXPath](../classes/OperationBinding.md#attr-operationbindingrecordxpath), is applied to the service response to select the XML elements or JSON objects that should be interpreted as DataSource records. Then, for each field of the DataSource, an optional [DataSourceField.valueXPath](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath) can be declared which selects the value for the field from within each of the XML elements or JSON objects selected by the recordXPath. If no valueXPath is specified, the field name itself is taken as an XPath, which will select the same-named subelement or property from the record element or object.

For example, the following code defines a DataSource that a ListGrid could bind to in order to display an RSS 2.0 feed.

```
    isc.DataSource.create({
        dataURL:feedURL,
        recordXPath:"//item",
        fields:[
            { name:"title" },
            { name:"link" },
            { name:"description" }
        ]
    });
 
```
A representative slice of an RSS 2.0 feed follows:
```
     <?xml version="1.0" encoding="iso-8859-1" ?> 
     <rss version="2.0">
     <channel>
       <title>feed title</title> 
       ...
       <item>
         <title>article title</title> 
         <link>url of article</link> 
         <description>
            article description
         </description> 
       </item>
       <item>
          ...
 
```
Here, the recordXPath selects a list of `<item>` elements. Since the intended values for each DataSource field appear as simple subelements of each `<item>` element (eg `<description>`), the field name is sufficient to select the correct values, and no explicit valueXPath needs to be specified.

A running version of this example is available here: *rssFeed example*. Further examples of simple XML or JSON data loading using files stored on disk as the "service" to contact: the *Simple JSON* example shows loading data from a JSON file into a databound grid, and the *XPath Binding example* shows loading XML and processing it with XPaths.

**WSDL integration**

If you have a choice between WSDL and REST integration, we recommend REST integration - it's simpler, requires less specialized knowledge, is easier to troubleshoot and is faster. If you need to use WSDL, see the [WSDL Binding Overview](wsdlBinding.md#kb-topic-wsdl-binding).

#### Round Tripping: Loading, Editing and Saving

For WSDL web services, see the [WSDL binding topic](wsdlBinding.md#kb-topic-wsdl-binding) first.

When using RestDataSource, see the [RestDataSource](../classes/RestDataSource.md#class-restdatasource) docs for message formats for saving, as well as expected responses.

When a user triggers a DSRequest (eg, completes an inline edit in a grid), the request data will be sent to the dataURL. The [DataSource protocol](dataSourceOperations.md#kb-topic-datasource-operations) describes request and response data expected for each operation type.

By using settings such as [OperationBinding.dataProtocol](../classes/OperationBinding.md#attr-operationbindingdataprotocol), you can control how DSRequests are sent to your backend so that you can handle them most easily. By using the same properties used to initially load data (eg [recordXPath](../classes/OperationBinding.md#attr-operationbindingrecordxpath)), you can control how SmartClient forms the DSResponses that are then interpreted by [databound components](../reference.md#interface-databoundcomponent).

**Controlling how DSRequests are sent**

According to the [protocol](../classes/OperationBinding.md#attr-operationbindingdataprotocol) being used, the [DataSource request data](dataSourceOperations.md#kb-topic-datasource-operations), if any, either becomes HTTP params (sent by GET or POST), or an XML message as put together by [DataSource.xmlSerialize](../classes/DataSource.md#method-datasourcexmlserialize). For a DataSource invoking a WSDL-described web service, XML serialization automatically handles namespacing and SOAP encoding.

Note that, by default, just [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata) is sent, not any of the metadata such as [DSRequest.startRow](../classes/DSRequest.md#attr-dsrequeststartrow). This can be customized via [DataSource.transformRequest](../classes/DataSource.md#method-datasourcetransformrequest).

The URL to contact is set via the [dataURL](../classes/OperationBinding.md#attr-operationbindingdataurl) property. If using a Web Service, the `dataURL` defaults to the service location URL embedded in the WSDL file.

For example, in the default configuration for non-WSDL binding, since [dataProtocol](../classes/OperationBinding.md#attr-operationbindingdataprotocol) is "getParams", [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata) is sent as HTTP params in an HTTP "GET" operation. Given:

*   changes to an existing record, hence an "update" request
*   a [primaryKey](../classes/DataSourceField.md#attr-datasourcefieldprimarykey) field of "id" with value "5" on the record to be updated
*   a field "age" being changed to "32"
*   "dataURL" of "save.php"

You will see an HTTP GET to the URL `save.php?id=5&age=32`.

**Forming a DSResponse from the response data**

A [DSResponse](../classes/DSResponse.md#class-dsresponse) is created from the response data by using XPath expressions declared in the schema ([recordXPath](../classes/OperationBinding.md#attr-operationbindingrecordxpath) and [valueXPath](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath)) to extract DataSource record and field values.

See the *"Edit and Save"* example for sample XML responses for all four operationTypes.

Similar to input processing, by default DataSource layer metadata, such as [DSResponse.startRow](../classes/DSResponse.md#attr-dsresponsestartrow), is not extracted from the response data. You can implement [DataSource.transformResponse](../classes/DataSource.md#method-datasourcetransformresponse) to fill out the metadata fields of the [DSResponse](../classes/DSResponse.md#class-dsresponse), in order to allow more DataSource features, such as paging and validation errors, to be used with a web service that supports such features.

See the *XML* and *JSON* versions of the transformResponse() example for an example of providing validation errors in XML or JSON responses.

### Related

- [DSDataFormat](../reference.md#type-dsdataformat)
- [DSProtocol](../reference_2.md#type-dsprotocol)
- [Callbacks.GetFieldValueCallback](../classes/Callbacks.md#method-callbacksgetfieldvaluecallback)
- [DataSource.dataFormat](../classes/DataSource.md#attr-datasourcedataformat)
- [DataSource.dataProtocol](../classes/DataSource.md#attr-datasourcedataprotocol)
- [DataSource.useHttpProxy](../classes/DataSource.md#attr-datasourceusehttpproxy)
- [DataSource.callbackParam](../classes/DataSource.md#attr-datasourcecallbackparam)
- [DataSource.requestProperties](../classes/DataSource.md#attr-datasourcerequestproperties)
- [DataSource.dataTransport](../classes/DataSource.md#attr-datasourcedatatransport)
- [DataSource.dropExtraFields](../classes/DataSource.md#attr-datasourcedropextrafields)
- [DataSource.sendExtraFields](../classes/DataSource.md#attr-datasourcesendextrafields)
- [DataSource.xmlNamespaces](../classes/DataSource.md#attr-datasourcexmlnamespaces)
- [DataSource.serviceNamespace](../classes/DataSource.md#attr-datasourceservicenamespace)
- [DataSource.schemaNamespace](../classes/DataSource.md#attr-datasourceschemanamespace)
- [DataSource.recordXPath](../classes/DataSource.md#attr-datasourcerecordxpath)
- [DataSource.dataURL](../classes/DataSource.md#attr-datasourcedataurl)
- [DataSource.tagName](../classes/DataSource.md#attr-datasourcetagname)
- [DataSource.defaultTextMatchStyle](../classes/DataSource.md#attr-datasourcedefaulttextmatchstyle)
- [DataSourceField.valueXPath](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath)
- [DataSourceField.valueWriteXPath](../classes/DataSourceField.md#attr-datasourcefieldvaluewritexpath)
- [DataSourceField.getFieldValue](../classes/DataSourceField.md#attr-datasourcefieldgetfieldvalue)
- [OperationBinding.beanClassName](../classes/OperationBinding.md#attr-operationbindingbeanclassname)
- [OperationBinding.operationType](../classes/OperationBinding.md#attr-operationbindingoperationtype)
- [OperationBinding.operationId](../classes/OperationBinding.md#attr-operationbindingoperationid)
- [OperationBinding.requiredCriterion](../classes/OperationBinding.md#attr-operationbindingrequiredcriterion)
- [OperationBinding.wsOperation](../classes/OperationBinding.md#attr-operationbindingwsoperation)
- [OperationBinding.dataURL](../classes/OperationBinding.md#attr-operationbindingdataurl)
- [OperationBinding.dataProtocol](../classes/OperationBinding.md#attr-operationbindingdataprotocol)
- [OperationBinding.dataFormat](../classes/OperationBinding.md#attr-operationbindingdataformat)
- [OperationBinding.dataTransport](../classes/OperationBinding.md#attr-operationbindingdatatransport)
- [OperationBinding.useHttpProxy](../classes/OperationBinding.md#attr-operationbindingusehttpproxy)
- [OperationBinding.callbackParam](../classes/OperationBinding.md#attr-operationbindingcallbackparam)
- [OperationBinding.requestProperties](../classes/OperationBinding.md#attr-operationbindingrequestproperties)
- [OperationBinding.defaultParams](../classes/OperationBinding.md#attr-operationbindingdefaultparams)
- [OperationBinding.useFlatFields](../classes/OperationBinding.md#attr-operationbindinguseflatfields)
- [OperationBinding.recordXPath](../classes/OperationBinding.md#attr-operationbindingrecordxpath)
- [OperationBinding.recordName](../classes/OperationBinding.md#attr-operationbindingrecordname)
- [DataSource.recordName](../classes/DataSource.md#attr-datasourcerecordname)
- [OperationBinding.spoofResponses](../classes/OperationBinding.md#attr-operationbindingspoofresponses)
- [OperationBinding.xmlNamespaces](../classes/OperationBinding.md#attr-operationbindingxmlnamespaces)
- [OperationBinding.responseDataSchema](../classes/OperationBinding.md#attr-operationbindingresponsedataschema)
- [RestDataSource.dataProtocol](../classes/RestDataSource.md#attr-restdatasourcedataprotocol)

---
