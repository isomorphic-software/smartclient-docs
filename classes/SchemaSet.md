# SchemaSet Documentation

[← Back to API Index](../main.md)

---

## Class: SchemaSet

### Description
A set of schema derived from the <xsd:schema> element in a WSDL or XML schema file loaded by [XMLTools.loadWSDL](XMLTools.md#classmethod-xmltoolsloadwsdl) or [XMLTools.loadXMLSchema](XMLTools.md#classmethod-xmltoolsloadxmlschema).

---
## Attr: SchemaSet.schemaNamespace

### Description
Namespace of this SchemaSet, derived from the `targetNamespace` attribute of the ``<schema>`` element.

### Groups

- webService

**Flags**: R

---
## ClassMethod: SchemaSet.get

### Description
Retrieve a SchemaSet object by it's schemaNamespace.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| schemaNamespace | [String](#type-string) | false | — | uri from the "targetNamespace" attribute of the <xsd:schema> element from the XML Schema or WSDL file this SchemaSet was derived from. |

### Returns

`[SchemaSet](#type-schemaset)` — the requested SchemaSet, or null if not loaded

**Flags**: A

---
## Method: SchemaSet.getSchema

### Description
Get the schema definition of any complexType or element of complexType defined within the `<schema>` element this SchemaSet represents.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| schemaName | [String](#type-string) | false | — | name of the schema to retrieve |
| schemaType | [String](#type-string) | true | — | optional type of schema to return, either "element" for xs:element definitions only or "type" for xs:complexType definitions. If unspecified, either will be returned, with types preferred if names collide |

### Returns

`[DataSource](#type-datasource)` — the schema if found, or null

**Flags**: A

---
