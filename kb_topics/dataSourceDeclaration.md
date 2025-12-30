# Creating DataSources

[← Back to API Index](../reference.md)

---

## KB Topic: Creating DataSources

### Description
DataSources can be specified in XML format, in which case the SmartClient server is used to load the DataSource, or DataSources can be programmatically created on the client.

Whether a DataSource is loaded via the SmartClient server or programmatically created client-side, identical requests will ultimately be submitted to the server. However, DataSources defined in XML are loaded and used by the SmartClient Server, enabling many features including synchronized client-server validation, request bundling, file upload, and optional automatic SQL/JPA/Hibernate connectivity (see the [Server Summary](iscServer.md#kb-topic-smartclient-server-summary) for details).

DataSources created on the client use the same style of creation as DataBound components:

```
    isc.DataSource.create({
        ID:"supplyItem",
        fields:[
            {name:"itemName", ... }
            ...
        ]
    });
 
```
Reference for all properties that can be set for DataSources, their fields and validators is given in the [DataSource](../classes/DataSource.md#class-datasource) class reference.

DataSources defined in XML declare fields, validators and other settings using XML tags:

```
     <DataSource ID="supplyItem">
         <fields>
             <field name="itemName" type="text" title="Item"/>
             <field name="SKU"      type="text" title="SKU">
                 <validators>
                     <validator type="integerRange" ... />
                 </validators>
             </field>
         </fields>
     </DataSource>
 
```
DataSources defined in XML are loaded by using the `DataSourceLoader` servlet provided by the SmartClient Server. This can be done as an ordinary HTML `<script>` tag as you application first loads:
```
     <SCRIPT SRC=isomorphic/DataSourceLoader?dataSource=supplyItem,employees,worldDS></SCRIPT>
 
```
.. or can be done on the fly via [DataSource.load](../classes/DataSource.md#classmethod-datasourceload).

Alternatively, in JSP environments, XML DataSources can be loaded via a special JSP tag supported by the SmartClient Server:

```
     <%@ taglib uri="/WEB-INF/iscTaglib.xml" prefix="isomorphic" %>
     ...
     <SCRIPT>
     <isomorphic:loadDS ID="supplyItem"/>
     </SCRIPT>
 
```

When loading an XML DataSource, by default, the ISC Server will look for a file named ``<dataSourceId>`.ds.xml` in the `/shared/ds` subdirectory under webroot. The location of this directory can be changed, or individual DataSources can be placed in arbitrary locations. For more information, see [\[webroot\]/WEB-INF/classes/server.properties](../reference.md#kb-topic-serverproperties-file).

XML DataSources can also be generated on the fly in case the entire DataSource or portions of it are based on dynamic data. See the server API com.isomorphic.DataSource.addDynamicDSGenerator().

### See Also

- [DataSource](../classes/DataSource.md#class-datasource)
- [loadDSTag](loadDSTag.md#kb-topic-isomorphicloadds)

---
