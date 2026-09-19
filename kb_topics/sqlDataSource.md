# SQL DataSources

[← Back to API Index](../reference.md)

---

## KB Topic: SQL DataSources

### Description
The SmartClient Server supports comprehensive, codeless SQL connectivity for DataSources defined in XML. Our SQL connectivity is mature, feature-rich, protected against injection attacks and easily customizable to support user-written SQL and additional business logic of any complexity. [This article](sqlVsJPA.md#kb-topic-sql-datasource-vs-jpa-ejb-mybatis-and-other-technologies) compares the built-in SQL DataSource to other persistence approaches based on Javabeans.

To use the built-in SQL engine, declare a [DataSource](../classes/DataSource.md#class-datasource) in XML format with [DataSource.serverType](../classes/DataSource.md#attr-datasourceservertype) set to "sql", and place it in the shared dataSources directory (\[webroot\]/shared/ds by default) in a file called "\[dataSourceId\].ds.xml".

You can then use the [Admin Console](adminConsole.md#kb-topic-admin-console) to configure database access, as well as to automatically create and populate a database table based on your DataSource. By default, DataSources will use the "default database" from the admin console, however you can set [DataSource.dbName](../classes/DataSource.md#attr-datasourcedbname) to the name of a specific database configuration you have configured via the Admin Console.

The list of databases known to work with the built-in SQL logic is as follows:

|  | HSQLDB ${HSQLDB_versions} |  |
|---|---|---|
|  | IBM DB2 ${IBM_DB2_versions} |  |
|  | IBM DB2 for i (formerly known as DB2 for i5/OS) ${IBM_DB2_for_i_versions} |  |
|  | Firebird ${Firebird_versions} |  |
|  | Informix ${Informix_versions} |  |
|  | MS SQL Server ${MS_SQL_Server_versions} |  |
|  | MySQL ${MySQL_versions} |  |
|  | MariaDB ${MariaDB_versions} |  |
|  | Oracle ${Oracle_versions} |  |
|  | PostgreSQL ${PostgreSQL_versions} |  |
|  | Progress OpenEdge ${OpenEdge_versions} (Note, DDL via JDBC operations are restricted by the product itself) |  |
|  | Snowflake ${Snowflake_versions} |  |

We also support a generic SQL92 database connection which works for basic CRUD operations with any database product that supports standard SQL92 syntax and data types, plus a couple of widely-implemented features that are not actually part of the standard. Specifically, this means we do not support:

*   Sequences
*   Paging via SQL limit queries
*   [Automatic transaction management](../classes/DataSource.md#attr-datasourceautojointransactions)
*   Long text values (there is no real definition of "long" here - we try to use a standard VARCHAR, but different databases will support different maximum values for this)
*   Databases that do not implement the widely-supported LOWER() function
*   Databases that do not support the ability to perform string-type operations on numeric columns - for example, `myNumericColumn LIKE '%5%'`

You will also need a JDBC driver for your specific database. Licensing restrictions prevent us including any JDBC driver other than the one for HSQLDB. However, you can download these drivers for free from the vendors' websites. If your specific database server or version is not listed above, please go to the [SmartClient forums](http://forums.smartclient.com) for assistance.

You can connect to an existing database table by providing a [DataSource.tableName](../classes/DataSource.md#attr-datasourcetablename) attribute value. Field-level details can be provided explicitly, if you choose, or these can be automatically inferred from your schema via [DataSource.autoDeriveSchema](../classes/DataSource.md#attr-datasourceautoderiveschema). **With autoDeriveSchema, you get full SQL connectivity / generation from a one-line .ds.xml file!.** You can of course customize these automatically derived field definitions without having to reiterate the properties discovered by auto-derivation. For example, the following field definition overrides an automatically [derived title](../classes/DataSource.md#attr-datasourceautoderivetitles) while preserving metadata obtained from the table, such as type & length:

```
   <field name="information" title="Interesting Facts" />
 
```

Once you have your SQL DataSource connected to a table, in a default SDK installation, DSRequests for your DataSource will be sent to the default [actionURL](../classes/RPCManager.md#classattr-rpcmanageractionurl), and hence handled automatically, without you having to write any Java code, by the [IDACall servlet registered in web.xml](servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets). IDACall is a very simple servlet that just calls the server-side method dsRequest.execute() for all inbound requests. For more details on how DataSource requests are processed by SmartClient Server, and how you can alter and add to this processing, see this description of [server data integration](serverDataIntegration.md#kb-topic-server-datasource-integration).

### Related

- [DataSourceField.sequenceName](../classes/DataSourceField.md#attr-datasourcefieldsequencename)
- [DataSourceField.implicitSequence](../classes/DataSourceField.md#attr-datasourcefieldimplicitsequence)

---
