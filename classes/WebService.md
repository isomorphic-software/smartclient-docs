# WebService Documentation

[← Back to API Index](../reference.md)

---

## Class: WebService

### Description
Class representing a WebService definition derived from a WSDL file.

A Web Service object allows you to invoke operations (via [callOperation()](#method-webservicecalloperation)), inspect schema declared in the WSDL file ([getSchema()](#method-webservicegetschema)), and perform simple read-only databinding [WebService.getFetchDS](#method-webservicegetfetchds).

Once a WebService has been loaded, a DataSource can be declared with a [DataSource.serviceNamespace](DataSource.md#attr-datasourceservicenamespace) to connect it to the web service, allowing DataSource data to be loaded and saved to the web service using [operationBindings](OperationBinding.md#class-operationbinding).

### Groups

- webService

---
## Attr: WebService.serviceNamespace

### Description
Namespace of this WebService, derived from the `targetNamespace` attribute of the `<wsdl:definitions>` element.

### Groups

- webService

**Flags**: R

---
## Attr: WebService.globalNamespaces

### Description
Namespaces definitions to add to the root element of outbound XML messages sent to a web service, as a mapping from namespace prefix to namespace URI.

The default value is:

```
   globalNamespaces : {
      xsi: "http://www.w3.org/2001/XMLSchema-instance",
      xsd: "http://www.w3.org/2001/XMLSchema"
   },
 
```
This default value allows the use of the xsi:type and xsi:nil attributes without further declarations.

Note that some web services will only accept specific revisions of the XML Schema URI. If xsi-namespaced attributes seem to be ignored by an older webservice, try the URI "http://www.w3.org/1999/XMLSchema-instance" instead.

**Flags**: IRW

---
## ClassMethod: WebService.getByName

### Description
Retrieve a WebService object by the name attribute declared on the <wsdl:service> tag.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| serviceName | [String](#type-string) | false | — | name attribute from the <wsdl:service> tag |
| serviceNamespace | [String](#type-string) | true | — | optional serviceNamespace if needed to disambiguate |

### Returns

`[WebService](#type-webservice)` — the requested WebService, or null if not loaded

### Groups

- webService

---
## ClassMethod: WebService.get

### Description
Retrieve a WebService object by the targetNamespace declared on the <wsdl:definitions> element in the WSDL file from which the WebService was derived.

If you have more than one <wsdl:service> in the same target namespace, use [WebService.getByName](#classmethod-webservicegetbyname) to disambiguate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| serviceNamespace | [String](#type-string) | false | — | uri from the "targetNamespace" attribute of the <wsdl:definitions> element in the WSDL file |

### Returns

`[WebService](#type-webservice)` — the requested WebService, or null if not loaded

### Groups

- webService

---
## Method: WebService.getFetchDS

### Description
Retrieve a DataSource that provides read-only access to records returned by a web service operation.

[DataBound Components](../reference.md#interface-databoundcomponent) can be bound to the returned DataSource, and the [fetchData()](ListGrid_2.md#method-listgridfetchdata) method can be invoked to retrieve data from the web service.

The returned DataSource is only capable of the "fetch" [DataSource operation](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations), not "update", "add" or "remove". To create a DataSource capable of full read-write access, use [DataSource.operationBindings](DataSource.md#attr-datasourceoperationbindings) with the [wsOperation](OperationBinding.md#attr-operationbindingwsoperation) property set to associate each DataSource operation with a web service operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationName | [String](#type-string) | false | — | name of the web service operation to invoke to fetch records |
| resultType | [String](#type-string) | false | — | tag or type name of the XML element to be returned as DataSource records |
| operationBindingProperties | [OperationBinding Properties](#type-operationbinding-properties) | true | — | Optional additional properties for the operationType:"fetch" [operationBinding](OperationBinding.md#class-operationbinding) which this method automatically creates. This can be used to set properties such as [OperationBinding.useFlatFields](OperationBinding.md#attr-operationbindinguseflatfields) or [OperationBinding.recordXPath](OperationBinding.md#attr-operationbindingrecordxpath) |

### Groups

- webService

---
## Method: WebService.getOutputHeaderSchema

### Description
Get the schema for each part of the SOAP header for the output message of a given operation, as a mapping from part name to schema. For example, given WSDL like:
```
     <soap:header part="SessionHeader"/>
     <soap:header part="CallOptions"/>
 
```
The following schema would be returned:
```
     { SessionHeader : sessionHeaderPartSchema,
       CallOptions : callOptionsPartSchema }
 
```
The schema are instances of [DataSource](DataSource.md#class-datasource) that can be inspected to discover the elements and types that are legal in that header part, and can construct a valid SOAP header part if [DataSource.xmlSerialize](DataSource.md#method-datasourcexmlserialize) is invoked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationName | [String](#type-string) | false | — | name of an operation from this web service |

### Returns

`[Object](../reference.md#type-object)` — mapping from partName to schema

---
## Method: WebService.callOperation

### Description
Invoke a web service operation.

The `data` parameter will be serialized to XML to form the input message for the operation, as described by [DataSource.xmlSerialize](DataSource.md#method-datasourcexmlserialize). Namespacing, element ordering, and SOAP encoding rules are automatically followed. If the web service you are trying to contact requires a complicated nested structure, consider using [WSRequest.useFlatFields](WSRequest.md#attr-wsrequestuseflatfields) to simplify the required JavaScript input data.

The `resultType` selects what part of the message should be decoded to JavaScript and made available as the "data" variable in the callback. The `resultType` parameter can be either:

*   an XPath. "data" will be always be an Array, containing the selected elements as decoded by [XMLTools.toJS](XMLTools.md#classmethod-xmltoolstojs). All properties will have String value.
*   the name of an XML Schema type found somewhere in the response. You can use the WSDL tab of the Developer Console to analyze the WSDL file for an appropriate type name. "data" will be an Array, containing the decoded elements as decoded by [DataSource.recordsFromXML](#method-datasourcerecordsfromxml). In this case, since the XML Schema type of the selected data is known, properties will have correct type (eg "date" fields will have JavaScript Date objects)
*   null. "data" will an Object representing the entire <SOAP:Body> as decoded to JavaScript. As above, properties will have correct type.

In the callback, you also receive the XML document returned by the web service as "xmlDoc".

NOTE: `callOperation()` is appropriate for simple operations that do not involve DataBound Components, such as logging into a web service, or retrieving simple String data. `callOperation()` can also be used to retrieve small, read-only datasets such as the option list for a SelectItem, but only if the dataset is guaranteed to remain small enough for paging to be unnecessary. For any larger datasets or anything that will be edited, DataSource integration is more appropriate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationName | [String](#type-string) | false | — | Name of the operation to invoke |
| data | [Object](../reference.md#type-object) | false | — | data to serialize as XML to form the inbound message of the operation |
| resultType | [Type](#type-type)|[ElementName](#type-elementname)|[XPath](#type-xpath) | false | — | Type, Element name, or XPath that should be selected from the result. For XPaths, see [WSRequest.xmlNamespaces](WSRequest.md#attr-wsrequestxmlnamespaces) for available namespace prefixes and how to add more. |
| callback | [Callback](../reference.md#type-callback) | false | — | Callback to invoke on completion. Signature callback(data, xmlDoc, rpcResponse, wsRequest) |
| requestProperties | [WSRequest Properties](#type-wsrequest-properties) | false | — | Additional properties for the WSRequest, such as HTTPHeaders |

### Groups

- webService

---
## Method: WebService.getHeaderData

### Description
Override this method to return data that should be serialized as SOAP headers for the current operation, such as a sessionId.

Format of the returned data is the same as that documented for [DSRequest.headerData](DSRequest.md#attr-dsrequestheaderdata).

The object passed to this method will be a true DSRequest in the case of a DataSource operation, or just an Object with a "data" property for web service operations initiated by [WebService.callOperation](#method-webservicecalloperation).

If `headerData` is instead provided via either dsRequest.headerData or as part of the `requestProperties` parameter to [callOperation()](#method-webservicecalloperation), this method will never be called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | — |

### Returns

`[Object](../reference.md#type-object)` — data for SOAP headers

---
## Method: WebService.setLocation

### Description
Set location can be used when the actual URL where a service will be accessible isn't known until runtime, or changes at runtime, hence can't be embedded in the service definition.

With an operation parameter, `setLocation()` can be used to set a distinct URL for each web service operation. This is a development-time only feature that allows XML flat files to be placed at various URLs on a server, to serve as spoofed responses for each web service operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| location | [URL](../reference_2.md#type-url) | false | — | URL where web service can be contacted |
| operation | [String](#type-string) | true | — | optional operation name to set the location for, for debugging only |

### Groups

- webService

**Flags**: A

---
## Method: WebService.getSchema

### Description
Get the schema definition of any complexType or element of complexType defined in any `<schema>` blocks in the WSDL file this WebService represents.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| schemaName | [String](#type-string) | false | — | name of type or element |
| schemaType | [String](#type-string) | true | — | optional type of schema to return, either "element" for xs:element definitions only or "type" for xs:complexType definitions. If unspecified, either will be returned, with types preferred if names collide |

### Returns

`[DataSource](#type-datasource)` — requested schema

### Groups

- webService

---
## Method: WebService.getSoapMessage

### Description
Return the SOAP message that will be formed from this WSRequest.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| wsRequest | [WSRequest Properties](#type-wsrequest-properties) | false | — | web service request object |

### Returns

`[String](#type-string)` — SOAP message

**Flags**: A

---
## Method: WebService.getOperationNames

### Description
—

### Returns

`[Array](#type-array)` — names of the available operations supported by this service (array of strings)

### Groups

- webService

---
## Method: WebService.getInputDS

### Description
Get a DataSource representing the input message to a web service operation.

This DataSource is suitable for use as [form.dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource) for a form that the user fills out when providing inputs to call this web service operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationName | [String](#type-string) | false | — | name of the web service operation whose inputs the returned DataSource will represent |

### Returns

`[DataSource](#type-datasource)` — DataSource representing the input message of a web service operation

---
## Method: WebService.getInputHeaderSchema

### Description
Get the schema for each part of the SOAP header for the input message of a given operation, as a mapping from part name to schema. For example, given WSDL like:
```
     <soap:header part="SessionHeader" message="tns:HeaderMessage"/>
     <soap:header part="CallOptions" message="tns:HeaderMessage/>
 
```
The following schema would be returned:
```
     { SessionHeader : sessionHeaderPartSchema,
       CallOptions : callOptionsPartSchema }
 
```
The schema are instances of [DataSource](DataSource.md#class-datasource) that can be inspected to discover the elements and types that are legal in that header part, and can construct a valid SOAP header part if [DataSource.xmlSerialize](DataSource.md#method-datasourcexmlserialize) is invoked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationName | [String](#type-string) | false | — | name of an operation from this web service |

### Returns

`[Object](../reference.md#type-object)` — mapping from partName to schema

---
