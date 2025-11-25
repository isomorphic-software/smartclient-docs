# Metadata Import

[← Back to API Index](../main.md)

---

## KB Topic: Metadata Import

### Description
In SmartClient, metadata is expressed through [DataSources](../classes/DataSource.md#class-datasource), which in turn drive [DataBoundComponents](../main.md#interface-databoundcomponent). If you have existing metadata, there are several possible approaches to transforming it to SmartClient DataSources, either one time or on the fly.

There are two possible targets for metadata import: XML format or JavaScript format. The XML format is more general purpose, since the ISC server can transform it to JavaScript via the [loadDS tag](loadDSTag.md#kb-topic-isomorphicloadds), and DataSources in XML format can be used by the ISC server for server-side validation (this split is covered in more detail under [Data Source Declaration](dataSourceDeclaration.md#kb-topic-creating-datasources)).

You may also transform your metadata dynamically (while the application is running in production) or statically (one time ever or at packaging time). Generally for a static or dynamic transform targetting JavaScript format you will want to produce one .js file containing all your DataSource definitions, to be loaded by your application via a normal `<SCRIPT SRC>` tag. For a static transform targetting XML format, you will want to produce a series of .ds.xml files and place them in the directories expected by the ISC server (see [DataSource Declaration](dataSourceDeclaration.md#kb-topic-creating-datasources)). Statically generated XML DataSources can be delivered to the browser as a single .js file via a .jsp containing several [`loadDS` tags](loadDSTag.md#kb-topic-isomorphicloadds).

If you want to do dynamic transform targetting XML format and use ISC server-side validation, the server-side API DataSource.fromXML() can be used to create a DataSource dynamically from XML, so that you can then call DataSource.validate(). Either the XML DataSource definition or the live DataSource itself can be passed to the server-side API XML.toJS() to produce JavaScript.

How to actually produce JavaScript or XML DataSource definitions from your existing metadata depends on the format of your metadata.

**XML Schema**

The method [XMLTools.loadXMLSchema](../classes/XMLTools.md#classmethod-xmltoolsloadxmlschema) and the [loadXMLSchema JSP tag](loadXMLSchemaTag.md#kb-topic-isomorphicloadxmlschema) provide dynamic transform of XML Schema to JavaScript. This is essentially accomplished by running `isomorphic/system/schema/schemaTranslator.xsl` on the XML schema file to produce XML DataSource definitions, and then translating those to JavaScript. You can run the `schemaTranslator` stylesheet using any standard XSLT processor and capture the XML output.

**Java Beans**

Metadata available via Java's "reflection" APIs allows a basic DataSource to be generated from Java beans. Sample Java code can be found in `examples/server_integration/DataSourceGenerator.java`. See also the last section on this page for an automatic option for generating DataSource definitions via Reflection.

**Other XML formats**

If you are familiar with XSLT or other XML transform languages, you could use it to do an XML to XML transform, and then use XML.toJS() to get to JavaScript.

**Schema represented as Java Objects**

If you are targetting XML, hand-coded generation of DataSource XML is straightforward, and from XML you can use XML.toJS() to get to JavaScript.

**Database Schema, Hibernate mappings or Java class definitions**

_**Note: This is an Enterprise feature.** It is not available to users of the LGPL, Pro or Power Editions of SmartClient. Please see the [licensing page](http://smartclient.com/licensing) for details._

If you have existing database tables, Hibernate classes or Java POJOs that follow the Javabean semantics, you can use these to automatically produce basic XML DataSource definitions. We provide the Batch DataSource Generator, a supported tool that makes use of SmartClient Server APIs to generate XML DataSource definitions and save them as `.ds.xml` files in your `shared/ds` folder. The source for the tool is provided in `tools/batchDSGenerator.jsp`.

If your metadata source is existing database tables, the Batch DS Generator can also extract data from those tables and save it as test data in your `shared/ds/test_data` folder. With this option, you have a complete round-trip facility from a populated database table to a client-side DataSource that does not require a server. The database table can be recreated and repopulated from the XML files using the SmartClient Admin Console, giving you a portable schema and dataset that can be used to initialize any database.

The tool is also able to output the DataSource definitions and test data in Javascript format rather than XML, for direct inclusion in client-side programs. In this mode, it will create `.ds.js` and `.data.js` files, rather than files with a `.xml` extension.

To use the tool, direct your web browser to the `tools/batchDSGenerator.jsp` resource of your SmartClient server. If you pass no parameters to the JSP, a SmartClient window will be shown, prompting you for the various generation parameters. Alternatively, you can effect a true batch operation by passing these parameters in directly. The source code is extensively commented and explains the meanings of all the parameters should you wish to take this latter approach.

Example simple usage (via the UI):  
`http://localhost:8080/tools/batchDSGenerator.jsp`

Example batch usage (providing the parameters by hand):  
`http://localhost:8080/tools/batchDSGenerator.jsp?dbName=Mysql&tableName=foo&tableName=bar&className=com.bar.foo.SomeClass&overwrite=true`

---
