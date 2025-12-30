# WSDL Binding

[← Back to API Index](../reference.md)

---

## KB Topic: WSDL Binding

### Description
SmartClient supports automated integration with WSDL-described web services. This support consists of:

*   creation of SOAP XML messages from JavaScript application data, with automatic namespacing, and support for both "literal" and "encoded" SOAP messaging, and "document" and "rpc" WSDL-SOAP bindings
*   automatic decode of SOAP XML messages to JavaScript objects, with strong typing (eg an XML schema "date" type becomes a JavaScript Date object)
*   [import of XML Schema](../classes/XMLTools.md#classmethod-xmltoolsloadxmlschema) (contained in WSDL, or external), including translating XML Schema "restrictions" to ISC [Validators](../classes/Validator.md#class-validator)

WSDL services can be contacted by using [XMLTools.loadWSDL](../classes/XMLTools.md#classmethod-xmltoolsloadwsdl) or the [<isc:loadWSDL> JSP tag](loadWSDLTag.md#kb-topic-isomorphicloadwsdl) to load the service definition, then invoking methods on the resulting [WebService](../classes/WebService.md#class-webservice) object.

[WebService.callOperation](../classes/WebService.md#method-webservicecalloperation) can be used to manually invoke operations for custom processing (example using *public zipcode service*, examples using .NET at [/examples/databinding/dotNET/temperatureConvert.jsp](/examples/databinding/dotNET/temperatureConvert.jsp)).

**Fetch-only DataSource binding**

To bind a component to a web service operation, call

  [WebService.getFetchDS(_operationName,elementName_)](../classes/WebService.md#method-webservicegetfetchds)

to obtain a DataSource which describes the structure of an XML element or XML Schema type named _elementName_, which appears in the response message for the operation named _operationName_. A component bound to this DataSource will show fields corresponding to the structure of the chosen XML element or type, that is, one field per subelement or attribute. [fetchData()](../classes/ListGrid_1.md#method-listgridfetchdata) called on this DataSource (or on a component bound to it) will invoke the specified web service operation, using the [Criteria](../reference.md#type-criteria) passed to fetchData() to fill out the input message via [DataSource.xmlSerialize](../classes/DataSource.md#method-datasourcexmlserialize), and using the specified XML element from the response message as data.

Similarly, [WebService.getInputDS(_operationName_)](../classes/WebService.md#method-webservicegetinputds) returns a DataSource suitable for binding to a form that a user will fill out to provide inputs to the specified web service operation. Typical use is to let the user fill in the form, then pass the results of [form.getValues()](../classes/DynamicForm.md#method-dynamicformgetvalues) to [fetchData()](../classes/ListGrid_1.md#method-listgridfetchdata) as criteria.

If the input message to the web service has extra nesting, consider using the [useFlatFields](../classes/OperationBinding.md#attr-operationbindinguseflatfields) property to simplify the inputs required for `fetchData()`, and/or to simplify form databinding via [component.useFlatFields](../classes/DataBoundComponent.md#attr-databoundcomponentuseflatfields).

Note that the WSDL tab in the Developer Console can provide a clean, simplified view of any WSDL file, making it easier to pick out the appropriate `operationName` and `elementName` parameters to pass to `getFetchDS()` and other [WebService](../classes/WebService.md#class-webservice) methods.

Take a look at the *Google SOAP Search example* and the [.NET example](/examples/databinding/dotNET/customerSearch.jsp) (/examples/databinding/dotNET/customerSearch.jsp).

**Binding with Customized Presentation**

Because XML Schema lacks key presentation metadata such as user-viewable titles, typically you cannot directly use the DataSources derived from XML Schema embedded in a WSDL file to drive visual component DataBinding in your final application.

You can create a DataSource that has custom fields **and** invokes a web service operation by setting [DataSource.serviceNamespace](../classes/DataSource.md#attr-datasourceservicenamespace) to match the targetNamespace of the [WebService](../classes/WebService.md#class-webservice) (found on the ``<definitions>`` element from the WSDL file), and setting [wsOperation](../classes/OperationBinding.md#attr-operationbindingwsoperation) to the name of the web service operation to invoke. `fetchData()` called on such a DataSource will invoke the web service operation named by [wsOperation](../classes/OperationBinding.md#attr-operationbindingwsoperation), just like a DataSource returned by [WebService.getFetchDS](../classes/WebService.md#method-webservicegetfetchds).

In contrast to `getFetchDS()`, creating a DataSource in this way gives you the opportunity to:

*   declare arbitrary fields, with SmartClient presentation attributes such as titles and formatters
*   extract any data from the response message, via [operationBinding.recordXPath](../classes/OperationBinding.md#attr-operationbindingrecordxpath) and [field.valueXPath](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath), and transform it with [transformResponse()](../classes/DataSource.md#method-datasourcetransformresponse)
*   transform the inbound data, if necessary, in order to add metadata such as [DSRequest.startRow](../classes/DSRequest.md#attr-dsrequeststartrow) for paging, or a sessionId for a service requiring authentication

These techniques are shown in the *Google SOAP Search example*.

**XML Schema Reuse**

Having loaded a WSDL file, all of the XML Schema definitions within the service definition get translated to SmartClient [DataSources](../classes/DataSource.md#class-datasource) and [SimpleTypes](../classes/SimpleType.md#class-simpletype) via the rules described by [XMLTools.loadXMLSchema](../classes/XMLTools.md#classmethod-xmltoolsloadxmlschema), and are available to you via [WebService.getSchema](../classes/WebService.md#method-webservicegetschema) and [DataSourceField.type](../classes/DataSourceField.md#attr-datasourcefieldtype).

You can use the [DataSource.inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom) property to create DataSources that extend from XML schema definitions, then add presentation metadata not found in XML schema.

Even if you choose to declare all fields manually, you can leverage XML Schema `<simpleType>` definitions by setting [field.type](../classes/DataSourceField.md#attr-datasourcefieldtype) to the name of an XML Schema simple type embedded in the WSDL file.

**Round Trip Binding \[fetch -> edit -> save\]**

For full read-write integration with a service that supports the basic [DataSource operations](dataSourceOperations.md#kb-topic-datasource-operations) on persistent data, [OperationBindings](../classes/OperationBinding.md#class-operationbinding) can be declared for each DataSource operation, and the [wsOperation](../classes/OperationBinding.md#attr-operationbindingwsoperation) property can be used to to bind each [DataSource operation](dataSourceOperations.md#kb-topic-datasource-operations) (fetch, update, add, remove) to a corresponding web service operation.

For example, this code accomplishes part of the binding to the [SalesForce partner web services](http://www.google.com/search?q=sforce+partner+wsdl) (additional code is required to handle authentication and other details):

```
 isc.DataSource.create({
    serviceNamespace : "urn:partner.soap.sforce.com",
    operationBindings : [
        { operationType:"fetch", wsOperation:"query", recordName: "sObject" },
        { operationType:"update", wsOperation:"update", recordName: "SaveResult" },
        { operationType:"add", wsOperation:"create", recordName: "SaveResult" },
        { operationType:"remove", wsOperation:"delete", recordName: "DeleteResult" }
    ],
    ...
 }); 
 
```
NOTE: additional code is required to handle authentication and other details, see the complete code in smartclientSDK/examples/databinding/SalesForce.

In this usage, any DSRequest performed on this DataSource invokes the web service operation named by the `wsOperation` property on the corresponding operationBinding, and [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata) is serialized via [DataSource.xmlSerialize](../classes/DataSource.md#method-datasourcexmlserialize) to form the input message to send to the web service. For example, if a [DynamicForm.saveData](../classes/DynamicForm.md#method-dynamicformsavedata) is invoked and triggers a DSRequest with operationType:"add", the DataSource above will invoke the "create" operation, and [form.values](../classes/DynamicForm.md#method-dynamicformgetvalues) will become [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata) and be serialized to form the input message of the "create" web service operation.

Typical usage is:

1.  declare a DataSource that represents the fields of the object as you want them represented in the UI. This DataSource is considered the "entity DataSource". It may extend from an XML Schema complex type via [DataSource.inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom).
2.  use [operationBindings](../classes/OperationBinding.md#class-operationbinding) to configure the entity DataSource to call the appropriate web service operations for each DataSource operation, and extract results via [recordXPath](../classes/OperationBinding.md#attr-operationbindingrecordxpath)/[recordName](../classes/OperationBinding.md#attr-operationbindingrecordname)
3.  bind components as follows:
    *   bind [grids](../classes/ListGrid_1.md#class-listgrid) to the entity DataSource
    *   bind [SearchForms](../classes/SearchForm.md#class-searchform) to the input message of the fetch operation (obtained via [webService.getInputDS("operationName")](../classes/WebService.md#method-webservicegetinputds). This is done because search inputs are frequently unrelated to the structure of the objects being searched for
    *   bind forms use for editing ("add" and "update" operations) to the entity DataSource
4.  use [transformRequest](../classes/DataSource.md#method-datasourcetransformrequest)/[transformResponse](../classes/DataSource.md#method-datasourcetransformresponse), [OperationBinding.useFlatFields](../classes/OperationBinding.md#attr-operationbindinguseflatfields) and [OperationBinding.responseDataSchema](../classes/OperationBinding.md#attr-operationbindingresponsedataschema) to handle inconsistencies between the WSDL operations and the data you want in the presentation layer.

A complete example of binding to the SalesForce "partner" web service, including authentication via SOAP headers, saving data and cache sync, inline editing, validation error handling and data paging, can be found in \[webroot\]/examples/databinding/SalesForce.

This requires a SalesForce account. SalesForce currently offers [free developer accounts](http://www.google.com/search?hl=en&q=salesforce+developer+account). Please note: this application deals with **live data** and if you using inline editing **it will save to SalesForce**.

**Deployment**

For best performance, using the [<isc:loadWSDL> JSP tag](loadWSDLTag.md#kb-topic-isomorphicloadwsdl) is recommended, as it automatically caches a translated form of the WSDL file. If you are not using the SmartClient server, the WSDL tab in the Developer Console allows you to save a .js file representing a WebService object, which can then be loaded and cached like a normal JavaScript file.

**Creating New WSDL Services**

If you have no existing WSDL web service but would like to use web services for integration, you can implement the "SmartClientOperations" web service described by the ${isc.DocUtils.externalLink(isc.Page.getIsomorphicDir()+"system/schema/SmartClientOperations.wsdl","WSDL file")} included in the SDK. This simple, 4 operation web service can support any number of DataSources. In this case, you create your DataSources as client-side instances of [WSDataSource](../reference.md#class-wsdatasource) (general client-side DataSource creation is described under [Creating DataSources](dataSourceDeclaration.md#kb-topic-creating-datasources)). To change the URL where ISC expects to find the SmartClientOperations web service, use [WebService.setLocation](../classes/WebService.md#method-webservicesetlocation) like so:

```
      var service = isc.WebService.get("urn:operations.smartclient.com");
      service.setLocation("myURL");
 
```

To implement a web service **starting from a WSDL file**:

*   In the .NET framework, you will use the Web Services Description Language Tool [(wsdl.exe)](http://www.google.com/search?q=wsdl.exe) to generate C# stubs that you will add business logic to
*   In Java, [Apache Axis](http://ws.apache.org/axis/) can be used to generate Java stubs for implementing a web service
*   In Perl, the [SOAP:Lite](http://soaplite.com) module can be used to implement web services without code generation
*   for PHP, the NuSoap module can likewise be used to implement web services without code generation

### Related

- [DataSource.serviceNamespace](../classes/DataSource.md#attr-datasourceservicenamespace)
- [DataSource.schemaNamespace](../classes/DataSource.md#attr-datasourceschemanamespace)

---
