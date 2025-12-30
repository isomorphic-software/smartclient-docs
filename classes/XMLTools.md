# XMLTools Documentation

[← Back to API Index](../reference.md)

---

## Class: XMLTools

### Description
Utility methods for dealing with XML elements, XML Schema, WSDL files, XSLT, and other XML-related functionality.

---
## ClassMethod: XMLTools.toJS

### Description
Translates an XML fragment to JavaScript collections. This method works just like the server-side method XML.toJS(Element, Writer):

*   Elements become JavaScript Objects with each attribute becoming a property
*   Subelements with just text (no child elements or attributes) become properties
*   Subelements with child elements or attributes become sub objects

For example, if you pass the following fragment to this method:
```
 <foo bar="zoo">
       <x>y</x>
 </foo>
 
```
You will get back the following JS structure:
```
 { bar:"zoo", x:"y"}
 
```
All atomic property values will be of String type. Use [DataSource.recordsFromXML](DataSource.md#method-datasourcerecordsfromxml) to do schema-driven XML to JS transform, which can produce correctly typed values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [XMLElement](../reference.md#type-xmlelement)|[XMLDocument](../reference.md#type-xmldocument) | false | — | The element to transform to JS |

### Returns

`[Object](../reference_2.md#type-object)` — The resulting JavaScript collection.

---
## ClassMethod: XMLTools.selectNodes

### Description
Retrieve a set of nodes from an XML element or document based on an XPath expression.

If the target document is namespaced, namespace prefixes declared in the document element of the target document will be available, as well as the default namespace, if declared, under the prefix "default".

To declare your own namespace prefixes, provide a prefix to URI mapping as a simple JS Object, for example:

```
   {
      az : "http://webservices.amazon.com/AWSECommerceService/2005-03-23",
      xsd : "http://www.w3.org/2001/XMLSchema"
   }
 
```

**NOTE:** this API cannot be supported on the Safari web browser for versions earlier than 3.0.3.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [XMLElement](../reference.md#type-xmlelement)|[XMLDocument](../reference.md#type-xmldocument)|[String](#type-string) | false | — | Native XMLElement,document, or xml string to select from |
| expression | [XPath](#type-xpath) | false | — | XPath expression to use to select nodes |
| namespaces | [Map](#type-map)<[Prefix,URI](#type-prefix-uri)> | true | — | namespace mapping used by the expression |

### Returns

`[Array](#type-array)` — list of nodes matching XPath

### Groups

- xmlTransform

---
## ClassMethod: XMLTools.nativeXMLAvailable

### Description
Returns true if the current browser exposes an XML parser that can be used for SmartClient XML operations like web service bindings and XML processing. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information on when the XML parser may not available and what features are impacted as a result.

### Returns

`[boolean](../reference.md#type-boolean)` — true if native XML processing is available, false otherwise.

---
## ClassMethod: XMLTools.selectObjects

### Description
Applies an XPath expression to JavaScript objects, returning matching objects.

Both child and attribute names are interpreted as property names, and array access notation can be used to select elements from Arrays. For example:

```
     var results = {
        searchResults:[
            { title:"Page One", relevance:6.3 },
            { title:"Page Two", relevance:5.2, 
              summary: "Summary of Page One" }
        ]
     };

     // returns the "searchResults" two-item Array
     isc.XMLTools.selectObjects(results, "/searchResults");

     // returns the first item under "searchResults", in an Array (NOTE: in XPath, Array
     // index starts at 1, not 0)
     isc.XMLTools.selectObjects(results, "/searchResults[1]");

     // returns ["Page One"]
     isc.XMLTools.selectObjects(results, "/searchResults[1]/title");

     // also returns ["Page One"]
     isc.XMLTools.selectObjects(results, "/searchResults[1]@title");
 
```
A limited form of XPath "predicates", that is, expressions with brackets that filter returned objects, is allowed. A predicate can be either:

*   a number only, eg \[5\], for Array access
*   the XPath function call "last()", eg \[last()\], to retrieve the last item
*   a property name (\*without\* any leading "@"), meaning that the property contains a value that is considered "true" in JavaScript. For example: \[summary\]
*   a property name, comparison operator, and either a number or String literal, for example, \[name = "bob"\]. In this case the property can also be the XPath function position(), for example, \[position() > 5\]

Some examples of using simple predicates with the sample data above:
```
     // returns an Array with only the first result
     isc.XMLTools.selectObjects(results, "/searchResults[relevance > 5.5]");
 
     // return an Array with only the second result, since the first has no summary
     isc.XMLTools.selectObjects(results, "/searchResults[summary]");
 
```
Details of the XPath -> Objects mapping:

*   JavaScript Object properties are considered element children, and text children do not exist (in the XML model, text children exist \*between\* element children, but nothing exists between JavaScript properties)
*   The contents of Array-valued properties are considered immediate element children (this is consistent with the predicate "\[5\]" acting like Array access)
*   "\*" in XML selects all element children, so "\*" in Object XPath selects the values of all properties, that is, [isc.getValues(object)](isc.md#staticmethod-iscgetvalues), except that Array-valued properties are "flattened" into the returned list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference_2.md#type-object) | false | — | Object to select results from |
| xPath | [String](#type-string) | false | — | XPath expression |

### Returns

`[Array](#type-array)` — Array of matching objects, or null for no match

**Flags**: A

---
## ClassMethod: XMLTools.loadXML

### Description
Load an XML document from the origin server or from a foreign server by relaying through the origin server. An asynchronous callback provides both the XML document and raw text of the response.

Relaying through the origin server requires that the ISC HttpProxyServlet be installed and accessible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [URL](../reference.md#type-url) | false | — | URL to load the schema from |
| callback | [Callback](../reference.md#type-callback) | false | — | callback to fire when the XML is loaded. Signature is callback(xmlDoc, xmlText) |
| requestProperties | [RPCRequest](#type-rpcrequest) | true | — | additional properties to set on the RPCRequest that will be issued |

---
## ClassMethod: XMLTools.disableIEXMLHackaround

### Description
Disables an Internet Explorer-specific work around for the MSXML bug that the 'xml' namespace prefix cannot be explicitly declared.

Though redundant, the [Namespaces in XML spec allows](http://www.w3.org/TR/REC-xml-names/#xmlReserved) XML documents to explicitly declare namespace prefix 'xml' bound to namespace name `http://www.w3.org/XML/1998/namespace`; e.g.

```
xmlns:xml="http://www.w3.org/XML/1998/namespace"
```
MSXML does not allow the 'xml' namespace prefix to be declared, and will raise the XML parse error: The namespace prefix is not allowed to start with the reserved string "xml". Microsoft has disclosed this bug as a Normative Variation in MSXML: [http://msdn.microsoft.com/en-us/library/ff460535(v=vs.85).aspx](http://msdn.microsoft.com/en-us/library/ff460535\(v=vs.85\).aspx). A framework-level work around is used by default in [XMLTools.parseXML](#classmethod-xmltoolsparsexml) where if the string `xmlns:xml="http://www.w3.org/XML/1998/namespace"` or `xmlns:xml='http://www.w3.org/XML/1998/namespace'` is found in the first 1000 characters of the `xmlText` parameter to parseXML(), then these two strings are removed from `xmlText` wherever they appear. This work around may be disabled by calling disableIEXMLHackaround() at any time before parseXML() is called.

---
## ClassMethod: XMLTools.serializeToString

### Description
Takes an XMLDocument and returns it as a String.

This method is not supported on the Safari web browser versions prior to 3.0.3.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| inputDocument | [XMLDocument](../reference.md#type-xmldocument) | false | — | XML document to apply the transform to |

### Returns

`[String](#type-string)` — XML document as a String

### Groups

- xmlTransform

---
## ClassMethod: XMLTools.loadXMLSchema

### Description
Load an XML file containing XML schema definitions and create DataSource and SimpleType objects to represent the schema. You can use to loaded schema to bind ISC components, perform validation, create editing interfaces, and build other metadata-driven interfaces. You can also use [schema inheritance](DataSource.md#attr-datasourceinheritsfrom) to overlay presentation-specific data (such as user-visible titles) on top of XML Schema.

In the loaded XML Schema, all <xsd:complexType> declarations become SmartClient DataSources, and all <xsd:simpleType> definitions become SmartClient [atomic type definitions](SimpleType.md#class-simpletype).

By default, named complexType definitions and named element definitions containing complexTypes become global DataSources, that is, they can be fetched with [DataSource.getDataSource](DataSource.md#classmethod-datasourcegetdatasource). Inline complexType definitions get automatically generated names.

Named simpleType declarations become global [atomic types](SimpleType.md#class-simpletype), that is, subsequently defined DataSources can use them for [DataSourceField.type](DataSourceField.md#attr-datasourcefieldtype). XML schema "restrictions" for simple types are automatically translated to [DataSourceField.valueMap](DataSourceField.md#attr-datasourcefieldvaluemap) or [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators) as appropriate.

The created SchemaSet object is available in the callback as the single parameter "schemaSet", or can retrieved via `SchemaSet.get(schemaNamespace)`.

NOTE: unless you are building an application that dynamically loads XML Schema without prior knowledge, instead of calling loadXMLSchema(), you should either:

*   use the [loadXMLSchemaTag](../kb_topics/loadXMLSchemaTag.md#kb-topic-isomorphicloadxmlschema) tag to eliminate the need for an asynchronous download of an XML Schema file as part of application startup, **OR**
*   use the "WSDL" tab in the Developer Console to obtain the XML Schema definition as a JavaScript file that can be loaded via a normal HTML `<SCRIPT SRC=>` tag and/or combined with other JavaScript files.

NOTE: required fields: the XML Schema concept of "required" for an attribute or subelement, expressed via use="required" (for an attribute) or minOccurs > 0 (for a subelement), is that the attribute or element must be present in the XML document _but can have any value_, including being empty or null. The SmartClient notion of required means non-null. You can express the SmartClient notion of required in XML Schema with the combination of minOccurs>0 and a minLength or length "restriction", and SmartClient will recognize the field as SmartClient-required, with all of the behaviors that implies (eg, specially styled form titles, automatic validation, etc).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| schemaURL | [URL](../reference.md#type-url) | false | — | URL to load the schema from |
| callback | [Callback](../reference.md#type-callback) | false | — | signature is callback(schemaSet) |
| requestProperties | [RPCRequest](#type-rpcrequest) | false | — | additional properties to set on the RPCRequest that will be issued |
| autoLoadImports | [boolean](../reference.md#type-boolean) | false | — | if set, xsd:import statements will be processed automatically to load dependent XSD files where a "location" is specified. The callback will not fire until all dependencies have been loaded |

### Groups

- xmlSchema

**Flags**: A

---
## ClassMethod: XMLTools.transformNodes

### Description
Apply an XSLT Stylesheet to an XML Document.

This method cannot currently be supported on the Safari web browser versions prior to 3.0.3.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| inputDocument | [XMLDocument](../reference.md#type-xmldocument) | false | — | XML document to apply the transform to |
| styleSheet | [XMLDocument](../reference.md#type-xmldocument) | false | — | XSLT stylesheet to use for transform |

### Returns

`[String](#type-string)` — stylesheet output

### Groups

- xmlTransform

---
## ClassMethod: XMLTools.selectNumber

### Description
Retrieve a numeric value from an XML element or document based on an XPath expression.

If more than one node matches, only the first node's value will be returned.

Namespacing works as described under [XMLTools.selectNodes](#classmethod-xmltoolsselectnodes)

**NOTE:** this API cannot be supported on the Safari web browser for versions prior to 3.0.3.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [XMLElement](../reference.md#type-xmlelement)|[XMLDocument](../reference.md#type-xmldocument)|[String](#type-string) | false | — | Native XMLElement,document, or xml string to select from |
| expression | [XPath](#type-xpath) | false | — | XPath expression to use to select nodes |
| namespaces | [Map](#type-map)<[Prefix,URI](#type-prefix-uri)> | true | — | namespace mapping used by the expression |

### Returns

`[Number](#type-number)` — result of the XPath, in Number form

### Groups

- xmlTransform

**Flags**: A

---
## ClassMethod: XMLTools.selectString

### Description
Retrieve a string value from an XML element or document based on an XPath expression.

If more than one node matches, only the first node's value will be returned.

Namespacing works as described under [XMLTools.selectNodes](#classmethod-xmltoolsselectnodes)

**NOTE:** this API cannot be supported on the Safari web browser for versions prior to 3.0.3.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [XMLElement](../reference.md#type-xmlelement)|[XMLDocument](../reference.md#type-xmldocument)|[String](#type-string) | false | — | Native XMLElement,document, or xml string to select from |
| expression | [XPath](#type-xpath) | false | — | XPath expression to use to select nodes |
| namespaces | [Map](#type-map)<[Prefix,URI](#type-prefix-uri)> | true | — | namespace mapping used by the expression |

### Returns

`[String](#type-string)` — result of the XPath, in String form

### Groups

- xmlTransform

**Flags**: A

---
## ClassMethod: XMLTools.parseXML

### Description
Parse XML text into an [XMLDocument](../reference.md#type-xmldocument). Parse errors, if any, are reported to the log.

**NOTE:** Internet Explorer's XML parser implementation, MSXML, has a bug in its handling of namespace name `http://www.w3.org/XML/1998/namespace`. Though redundant, the [Namespaces in XML spec allows](http://www.w3.org/TR/REC-xml-names/#xmlReserved) XML documents to explicitly declare namespace prefix 'xml' bound to namespace name `http://www.w3.org/XML/1998/namespace`; e.g.

```
xmlns:xml="http://www.w3.org/XML/1998/namespace"
```
MSXML does not allow the 'xml' namespace prefix to be declared, and will raise the XML parse error: The namespace prefix is not allowed to start with the reserved string "xml". Microsoft has disclosed this bug as a Normative Variation in MSXML: [http://msdn.microsoft.com/en-us/library/ff460535(v=vs.85).aspx](http://msdn.microsoft.com/en-us/library/ff460535\(v=vs.85\).aspx). A framework-level work around is used by default where if the string `xmlns:xml="http://www.w3.org/XML/1998/namespace"` or `xmlns:xml='http://www.w3.org/XML/1998/namespace'` is found in the first 1000 characters of `xmlText`, then these two strings are removed from `xmlText` wherever they appear. This work around may be disabled by calling [XMLTools.disableIEXMLHackaround](#classmethod-xmltoolsdisableiexmlhackaround) at any time before parseXML() is called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| xmlText | [String](#type-string) | false | — | XML text to be parsed |

### Returns

`[XMLDocument](../reference.md#type-xmldocument)` — resulting XMLDocument

---
## ClassMethod: XMLTools.loadWSDL

### Description
Load a WSDL file and create an instance of WebService that allows invoking operations and binding DataSources to web service operations.

The created WebService object is available in the callback as the single parameter "service", or can be retrieved via `WebService.get(serviceNamespace)`.

XML Schema present in the WSDL file will also be processed as described in [XMLTools.loadXMLSchema](#classmethod-xmltoolsloadxmlschema). However note that **imported** XML Schema (<xs:import> tag) will not be automatically loaded and must be loaded manually using [XMLTools.loadXMLSchema](#classmethod-xmltoolsloadxmlschema) before the loaded service will be usable. This is because the WSDL spec allows but does not require a valid URL to be provided for loading imported XML Schema.

NOTE: unless you are building an application that dynamically contacts WSDL web services without prior knowledge, instead of calling loadWSDL(), you should either:

*   use the [loadWSDLTag](../kb_topics/loadWSDLTag.md#kb-topic-isomorphicloadwsdl) tag to eliminate the need for an asynchronous download of a WSDL file as part of application startup, **OR**
*   use the "WSDL" tab in the Developer Console to obtain the WebService definition as a JavaScript file that can be loaded via a normal HTML `<SCRIPT SRC=>` tag and/or combined with other JavaScript files.

Platform notes:

*   loadWSDL() is not supported in Safari 2.0 (but is supported in Safari 3.0.3 and greater) However, you can use either approach mentioned above (loadWSDLTag or JavaScript file) with Safari pre 3.0.3.
*   if you are using a non-Java server, in order to obtain a JavaScript file representing a web service, you must run the Developer Console in the Java-based SmartClient SDK

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| wsdlURL | [URL](../reference.md#type-url) | false | — | URL to load the WSDL file from |
| callback | [Callback](../reference.md#type-callback) | false | — | signature is callback(service) |
| requestProperties | [RPCRequest](#type-rpcrequest) | false | — | additional properties to set on the RPCRequest that will be issued |
| autoLoadImports | [boolean](../reference.md#type-boolean) | false | — | if set, xsd:import statements will be processed automatically to load dependent XSD files where a "location" is specified. The callback will not fire until all dependencies have been loaded |

### Groups

- xmlSchema

**Flags**: A

---
