# <isomorphic:loadDS>

[← Back to API Index](../reference.md)

---

## KB Topic: <isomorphic:loadDS>

### Description
See [jspTags](../reference.md#kb-topic-smartclient-jsp-tags)

_produces:_ JavaScript

This tag converts a SmartClient DataSource or SimpleType defined in XML to JavaScript for use in databinding on the client (browser).

Note that this JSP tag must be surrounded by `<SCRIPT>` tags in the JSP because it generates JavaScript code. Like other tags that generate JavaScript code, this tag can be used in a JSP that is included from your main page in order to create separate cacheability. For example:

```
 <SCRIPT SRC="myDataSources.jsp"></SCRIPT>
 
```

**Tag Attributes:**

**ID**  
_value format_: String - ID of datasource or simpleType to load  
_default value_: NONE

This attribute specifies the name of the dataSource or simpleType that you wish to load. DataSources are located in `[webroot]/shared/ds` or `[webroot]/WEB-INF/ds` by default. This location is changeable in `[webroot]/WEB-INF/classes/server.properties` by setting the config parameter `project.datasources` to the directory where your dataSources are located.  
We recommend that for prototyping, at least, you use the default directory.  

For example:

```
 <isomorphic:loadDS ID="supplyItem"/>
 
```
Would load the `supplyItem` DataSource.

You can also load multiple dataSources in one go by specifying a comma-separated list of dataSource names as the ID. For example:

```
 <isomorphic:loadDS ID="supplyItem, employees, worldDS"/>
 
```
See [dataSourceDeclaration](dataSourceDeclaration.md#kb-topic-creating-datasources) for more details on creating DataSources and an example.

See [SimpleType](../classes/SimpleType.md#class-simpletype) for more details on how to define server-side SimpleType in xml format.

**name**  
_value format_: String - ID of datasource to load  
_default value_: NONE

This is a synonym for the `ID` attribute.

**locale**  
_value format_: valid locale string - see [dataSourceLocalization](dataSourceLocalization.md#kb-topic-datasource-and-component-xml-localization) for more details and examples.  
_default value_: as set by the OS/JVM defaults

**mockMode**  
_value format_: boolean - acceptable values: "true" or "false"  
_default value_: "false"

This attribute determines if the DataSource(s) is loaded in [DataSource.mockMode](../classes/DataSource.md#attr-datasourcemockmode).

### See Also

- [dataSourceDeclaration](dataSourceDeclaration.md#kb-topic-creating-datasources)

---
