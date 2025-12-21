# DatabaseBrowser Documentation

[← Back to API Index](../reference.md)

---

## Class: DatabaseBrowser

*Inherits from:* [Window](Window.md#class-window)

### Description
A component that connects to a database (and, depending on the RDBMS in use, optionally a particular schema) and displays the currently-defined tables, optionally filtered in a variety of ways. It also allows you to view the column details of a selected table, and optionally retrieves and displays the data currently in that table.

The DatabaseBrowser can also create a SmartClient DataSource from any existing SQL table.

Note, the DatabaseBrowser (and SmartClient's SQL features generally) does not support the SQL-92 concept of "catalog". Although JDBC defines catalogs as a containment level above schemas, in practice nearly all mainstream RDBMS either have no concept of catalog at all, or they equate "catalog" with "database" and bind a JDBC connection to a single one of them, making the catalog layer redundant. The JDBC `getCatalogs()` API typically returns either the current database, a list of databases that are not practically accessible within the same session, or nothing at all. As a result, real-world metadata navigation is almost always schema -> tables (or directly database -> tables in the case of MySQL/MariaDB), not catalog -> schema -> tables.

To make matters worse, some of the more long-established mainstream databases (Oracle, DB2, some less common ones) use the word "catalog" in their documentation to mean "system metadata", which is completely different from the SQL-92 definition. Since catalogs in the SQL-92 sense are nearly always either redundant or missing, and depending on the database in use there may also be a confusing collision of terminology, SmartClient does not provide explicit support for them.

---
## Attr: DatabaseBrowser.schemaCriteria

### Description
Optional criteria to pass to the [DatabaseBrowser.schemaDataSource](#attr-databasebrowserschemadatasource) when retrieving the list of schemas for a selected database. Note, this criteria is in addition to the criteria implied by the current [dbName](#attr-databasebrowserdbname)

**Flags**: IR

---
## Attr: DatabaseBrowser.schemaPickerForm

### Description
A form containing a single [SelectItem](SelectItem.md#class-selectitem) which lists all the schemas available in the current database (though see [schemaDataSource](#attr-databasebrowserschemadatasource) for details of how you can filter or otherwise modify this list)

Select a schema in the picklist to update the selected schema and display the table details in the [DatabaseBrowser.schemaTree](#attr-databasebrowserschematree). Set the selected schema to blank to show tables from all schemas.

Note, if the [schema](#attr-databasebrowserschema) property is set when the `DatabaseBrowser` is created, the schemaPicker shows the schema name, but is set read only so the user cannot change the selection.

**Flags**: IR

---
## Attr: DatabaseBrowser.schemaFetchOperation

### Description
Optional [OperationBinding.operationId](OperationBinding.md#attr-operationbindingoperationid) to pass to the [DatabaseBrowser.schemaDataSource](#attr-databasebrowserschemadatasource) when retrieving the list of schemas for a selected database.

**Flags**: IRA

---
## Attr: DatabaseBrowser.selectButton

### Description
Instance of Button used to continue once a table has been selected.

**Flags**: IR

---
## Attr: DatabaseBrowser.tableDataSource

### Description
DataSource to retrieve the list of tables and views from a database.

If not explicitly specified, a dataSource will be automatically created for you and will invoke a special BuiltInRPC method `getTables()` to retrieve the set defined set of tables and views for the selected database.

See [server_properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) for details on how to enable access to BuiltInRPC utility methods.

We ship a default dataSource implementation, and we recommend that you use it instead of the auto-created client-side dataSource, which is really intended as a fallback in case the DataSource is not specified or wasn't deployed with the application. This implementation gives the same results as the client-side version, but it works on the server-side, it supports filtering the results with regular `AdvancedCriteria`, and its functionality is implemented in Groovy script in the dataSource definition file, so it is easy to modify.

If you wish to use this DS implementation, set `tableDataSource` to "DBBrowser\_tables" (the DBBrowser\_\* dataSource definitions are shipped in the SmartClient SDK inside /shared/ds - you must ensure that these are deployed to the same location - or another valid dataSource location - in your deployed app)

If you do use the default "DBBrowser\_tables" dataSource, it provides a user hook where you can provide additional filtering logic without changing the base logic. To do this, create a new class that implements interface `com.isomorphic.tools.DiscoverableTableListFilter` and add a `server.properties` entry pointing to it, like this:

```
    discoverable.table.list.filter.impl:com.mycompany.MyTableFilterImpl
 
```
SmartClient will instantiate an instance of your class and call its `filter()` method, passing in the list of tables it derived, after fields have been renamed to suit suit the dataSource (eg, renaming "TABLE\_NAME" to "name"), and any criteria has been applied. You should return a list, filtered or otherwise modified however you like - the intention is that you make filtering changes, such as removing tables that are not applicable to the current department or user, but there is nothing to stop you from making any change you like, including adding or modifying entries.

Finally, to allow completely custom behavior retrieving the set of tables within a database, you can provide your own DataSource implementation to retrieve table names. At a minimum this DataSource must have fields for `name` (primary key) and `type` (one of "table" or "view"). The request to retrieve tables may be customized via [DatabaseBrowser.tableCriteria](#attr-databasebrowsertablecriteria), [DatabaseBrowser.tableFetchOperation](#attr-databasebrowsertablefetchoperation) and [DatabaseBrowser.tableFetchRequestProperties](#attr-databasebrowsertablefetchrequestproperties).

**Flags**: IR

---
## Attr: DatabaseBrowser.tableCriteria

### Description
Optional criteria to pass to the [DatabaseBrowser.tableDataSource](#attr-databasebrowsertabledatasource) when retrieving the set of tables and views for a selected database. Note, this criteria is in addition to the criteria implied by the current [dbName](#attr-databasebrowserdbname) and [schema](#attr-databasebrowserschema) (if any), and any criteria the user has entered into the table list widget's filterEditor

**Flags**: IR

---
## Attr: DatabaseBrowser.serverType

### Description
The type of database server this DatabaseBrowser should connect to. Valid values are "sql" (SmartClient's own built-in support for SQL databases) or "hibernate"

**Flags**: IR

---
## Attr: DatabaseBrowser.databaseList

### Description
List of database configurations derived from the [DatabaseBrowser.databaseDataSource](#attr-databasebrowserdatabasedatasource).

Select a database to update [DatabaseBrowser.dbName](#attr-databasebrowserdbname) and display the details in the [DatabaseBrowser.schemaTree](#attr-databasebrowserschematree).

**Flags**: IR

---
## Attr: DatabaseBrowser.schemaTree

### Description
Instance of ListGrid used to display the database schema (ie, the list of tables). This grid makes use of an +link{listGrid.canExpandRecords,expansion component) to show columns for each table.

**Flags**: IR

---
## Attr: DatabaseBrowser.tableFetchOperation

### Description
Optional [OperationBinding.operationId](OperationBinding.md#attr-operationbindingoperationid) to pass to the [DatabaseBrowser.tableDataSource](#attr-databasebrowsertabledatasource) when retrieving the set of tables and views for a selected database.

**Flags**: IRA

---
## Attr: DatabaseBrowser.databaseDataSource

### Description
DataSource to retrieve the list of database configurations.

If not explicitly specified, a dataSource will be automatically created for you and will invoke a special BuiltInRPC method `getDefinedDatabases()` to retrieve the set defined set of database connections for the deployment.

See [server_properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) for details on how to enable access to BuiltInRPC utility methods. Note that allowing full access to the database configurations in this way is typically not appropriate for production environments.

We ship a default dataSource implementation, and we recommend that you use it instead of the auto-created client-side dataSource, which is really intended as a fallback in case the DataSource is not specified or wasn't deployed with the application. This implementation gives the same results as the client-side version, but it works on the server-side, it supports filtering the results with regular `AdvancedCriteria`, and its functionality is implemented in Groovy script in the dataSource definition file, so it is easy to modify.

If you wish to use this DS implementation, set `databaseDataSource` to "DBBrowser\_databases" (the DBBrowser\_\* dataSource definitions are shipped in the SmartClient SDK inside /shared/ds - you must ensure that these are deployed to the same location - or another valid dataSouirce location - in your deployed app)

If you do use the default "DBBrowser\_databases" dataSource, it provides a user hook where you can provide additional filtering logic without changing the base logic. To do this, create a new class that implements interface `com.isomorphic.tools.DiscoverableDatabaseConnectionFilter` and add a `server.properties` entry pointing to it, like this:

```
    discoverable.database.connection.filter.impl:com.mycompany.MyDatabaseConnectionFilterImpl
 
```
SmartClient will instantiate an instance of your class and call its `filter()` method, passing in the list of database connections it derived, after any criteria has been applied. You should return a list, filtered or otherwise modified however you like - the intention is that you make filtering changes, such as removing database connections that the current user is not allowed to see, but there is nothing to stop you from making any change you like, including adding or modifying entries.

Finally, to allow completely custom behavior retrieving the set of database configs available within an application, you can provide your own DataSource implementation to retrieve configurations. At a minimum this DataSource must have fields for `dbName` (primary key) and `dbStatus`. The request to retrieve database connections may be customized via [DatabaseBrowser.dbCriteria](#attr-databasebrowserdbcriteria), [DatabaseBrowser.dbFetchOperation](#attr-databasebrowserdbfetchoperation) and [DatabaseBrowser.dbFetchRequestProperties](#attr-databasebrowserdbfetchrequestproperties).

**Flags**: IR

---
## Attr: DatabaseBrowser.schema

### Description
The name of the database schema to use. Leave this property unset to include all schemas by default, and allow the user to choose between available schemas with the [schema picklist](#attr-databasebrowserschemapickerform). Note that this property is not applicable to MySQL/MariaDB, which do not recognize the concept of multiple schemas within a database.

Note, it does not usually make sense to set this property unless you also set the [dbName](#attr-databasebrowserdbname) and switch off the ability to change the selected database by setting [showDatabaseList](#attr-databasebrowsershowdatabaselist) false, because it fixes the schema name while allowing the database to be chosen by the user. The only time it would make sense to do this would be when you have a series of databases and they all contain a schema with a given name (and you want to limit the user to just that schema)

Note that this property only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

**Flags**: IR

---
## Attr: DatabaseBrowser.dbName

### Description
The name of the database configuration currently being displayed. If [DatabaseBrowser.showDatabaseList](#attr-databasebrowsershowdatabaselist) is true, this property will be updated when the user selects a database configuration from the list. Otherwise, if `dbName` property is not explicitly set the default database will be displayed.

Note that this property only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

**Flags**: IR

---
## Attr: DatabaseBrowser.dataGrid

### Description
Instance of ListGrid used to display the actual data in the table selected in the [schemaTree](#attr-databasebrowserschematree).

**Flags**: IR

---
## Attr: DatabaseBrowser.showDatabaseList

### Description
Should the list of configured databases be shown to the user. If the database list is shown, the user can freely select between configured databases; if the list is not shown, the widget will only show schemas, tables and data from the database specified by [dbName](#attr-databasebrowserdbname)

Only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

**Flags**: IR

---
## Attr: DatabaseBrowser.excludeSubstring

### Description
If set, specifies a substring which must NOT exist in a table name for it to be included in this DatabaseBrowser. If this property is set to a List of strings, table names are excluded if they match any one of the strings. The comparison is case-insensitive.

For example, `excludeSubstring: ["E", "qry"]` would exclude all the following table names: "table", "QryTbl", "QRY", "ORDERS"

Note that if you specify both include and exclude criteria and they conflict (ie, according to the criteria you set, a table should be both included and excluded), exclude wins.

**Deprecated**

**Flags**: IR

---
## Attr: DatabaseBrowser.dbFetchOperation

### Description
Optional [OperationBinding.operationId](OperationBinding.md#attr-operationbindingoperationid) to pass to the [DatabaseBrowser.databaseDataSource](#attr-databasebrowserdatabasedatasource) when retrieving the set of databases to display in the [database list](#attr-databasebrowsershowdatabaselist).

**Flags**: IRA

---
## Attr: DatabaseBrowser.dbFetchRequestProperties

### Description
Optional dsRequest configuration for the fetch operation when retrieving the set of databases to display in the [database list](#attr-databasebrowsershowdatabaselist).

**Flags**: IR

---
## Attr: DatabaseBrowser.tableFetchRequestProperties

### Description
Optional dsRequest configuration for the fetch operation when retrieving the set of tables and views for a selected database.

**Flags**: IR

---
## Attr: DatabaseBrowser.schemaFetchRequestProperties

### Description
Optional dsRequest configuration for the fetch operation when retrieving the list of schemas for a selected database.

**Flags**: IR

---
## Attr: DatabaseBrowser.dbCriteria

### Description
Optional criteria to pass to the [DatabaseBrowser.databaseDataSource](#attr-databasebrowserdatabasedatasource) when retrieving the set of databases to display in the [database list](#attr-databasebrowsershowdatabaselist).

**Flags**: IR

---
## Attr: DatabaseBrowser.cancelButton

### Description
Instance of Button used to cancel this dialog.

**Flags**: IR

---
## Attr: DatabaseBrowser.title

### Description
A title to show in the header button of the DatabaseBrowser's schema tree. If not set, defaults to the name of the connected database

**Flags**: IR

---
## Attr: DatabaseBrowser.schemaDataSource

### Description
DataSource to retrieve the list of schemas from a database.

If not explicitly specified, a dataSource will be automatically created for you and will invoke the special BuiltInRPC method `getSchemas()` to retrieve the set defined set of tables and views for the selected database.

See [server_properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) for details on how to enable access to BuiltInRPC utility methods.

We ship a default dataSource implementation, and we recommend that you use it instead of the auto-created client-side dataSource, which is really intended as a fallback in case the DataSource is not specified or wasn't deployed with the application. This implementation gives the same results as the client-side version, but it works on the server-side, it supports filtering the results with regular `AdvancedCriteria`, and its functionality is implemented in Groovy script in the dataSource definition file, so it is easy to modify.

If you wish to use this DS implementation, set `schemaDataSource` to "DBBrowser\_schemas" (the DBBrowser\_\* dataSource definitions are shipped in the SmartClient SDK inside /shared/ds - you must ensure that these are deployed to the same location - or another valid dataSouirce location - in your deployed app)

Finally, to allow completely custom behavior retrieving the set of schemas within a database, you can provide your own DataSource implementation to retrieve schema names. At a minimum this DataSource have must have fields `dbName` and `schemaName`. The request to retrieve schemas may be customized via [DatabaseBrowser.schemaCriteria](#attr-databasebrowserschemacriteria), [DatabaseBrowser.schemaFetchOperation](#attr-databasebrowserschemafetchoperation) and [DatabaseBrowser.schemaFetchRequestProperties](#attr-databasebrowserschemafetchrequestproperties).

**Flags**: IR

---
## Attr: DatabaseBrowser.includeSubstring

### Description
If set, specifies a substring which must exist in a table name for it to be included in this DatabaseBrowser. If this property is set to a List of strings, table names are included if they match any one of the strings. The comparison is case-insensitive.

For example, `includeSubstring: ["E", "qry"]` would match all the following table names: "table", "QryTbl", "QRY", "ORDERS"

**Deprecated**

**Flags**: IR

---
## Method: DatabaseBrowser.getGeneratedDataSource

### Description
Returns the [DataSource](DataSource.md#class-datasource) most recently auto-derived by this DatabaseBrowser. This will correspond to the currently-selected table.

---
## Method: DatabaseBrowser.getResults

### Description
—

---
