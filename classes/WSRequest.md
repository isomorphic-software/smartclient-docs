# WSRequest Documentation

[← Back to API Index](../main.md)

---

## Attr: WSRequest.xmlNamespaces

### Description
Optional object declaring namespace prefixes for use in evaluating the `resultType` parameter of [WebService.callOperation](WebService.md#method-webservicecalloperation), if resultType is an XPath.

Format is identical to [OperationBinding.xmlNamespaces](OperationBinding.md#attr-operationbindingxmlnamespaces), and default namespaces bindings are also identical.

**Flags**: IR

---
## Attr: WSRequest.wsOperation

### Description
Name of the web service operation to invoke.

**Flags**: IR

---
## Attr: WSRequest.data

### Description
Data to be serialized to XML to form the SOAP body.

**Flags**: IR

---
## Attr: WSRequest.useFlatFields

### Description
When `useFlatFields` is set for a request to be sent to a WSDL web service, when creating the input XML message to send to the web service, properties in [request.data](#attr-wsrequestdata) will be used as the values for XML elements of the same name, at any level of nesting.

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

For [DataBoundComponents](../main.md#interface-databoundcomponent), [component.useFlatFields](DataBoundComponent.md#attr-databoundcomponentuseflatfields) can be set use "flattened" binding to fields of a WSDL message or XML Schema.

Note that `useFlatFields` is not generally recommended for use with XML input messages where multiple simple type fields exist with the same name, however if used in this way, the first field to use a given name wins. "first" means the first field encountered in a depth first search. "wins" means only the first field will be populated in the generated XML message.

### Groups

- flatFields

**Flags**: IR

---
## Attr: WSRequest.headerData

### Description
Data to be serialized to form the SOAP headers, as a map from the header part name to the data. For example, given WSDL like this:
```
     <soap:header part="SessionHeader" message="tns:HeaderMessage"/>
     <soap:header part="CallOptions" message="tns:HeaderMessage/>
 
```
`headerData` like this might be provided:
```
     dsRequest.headerData = 
         { SessionHeader : data
           CallOptions : data };
 
```
The provided data will be serialized to XML by the [SOAP header schema](WebService.md#method-webservicegetinputheaderschema) via [DataSource.xmlSerialize](DataSource.md#method-datasourcexmlserialize)

**Flags**: IR

---
## Attr: WSRequest.xmlResult

### Description
Valid only with [WebService.callOperation](WebService.md#method-webservicecalloperation). If set, do not transform XML results to JavaScript. Instead just return the XML nodes selected by the passed XPath or recordName, or all nodes within the SOAP body if no XPath was passed.

**Flags**: IR

---
