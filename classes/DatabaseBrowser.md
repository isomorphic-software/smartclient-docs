# DatabaseBrowser Documentation

[← Back to API Index](../reference.md)

---

## Class: DatabaseBrowser

*Inherits from:* [Window](Window.md#class-window)

### Description
A component that connects to a database (and, depending on the RDBMS in use, optionally a particular catalog and/or schema) and displays the currently-defined tables, optionally filtered in a variety of ways. It also allows you to view the column details of a selected table, and optionally retrieves and displays the data currently in that table.

The DatabaseBrowser can also create a SmartClient DataSource from any existing SQL table.

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

To allow custom behavior retrieving the set of tables and views within a database, you can provide your own explicitly specified DataSource to retrieve connections. At a minimum this DataSource have fields for `name` (primary key) and `type` (one of "table" or "view"). The request to retrieve database connections may be customized via [DatabaseBrowser.tableCriteria](#attr-databasebrowsertablecriteria), [DatabaseBrowser.tableFetchOperation](#attr-databasebrowsertablefetchoperation) and [DatabaseBrowser.tableFetchRequestProperties](#attr-databasebrowsertablefetchrequestproperties).

**Flags**: IR

---
## Attr: DatabaseBrowser.tableCriteria

### Description
Optional criteria to pass to the [DatabaseBrowser.tableDataSource](#attr-databasebrowsertabledatasource) when retrieving the set of tables and views for a selected database.

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

To allow customized access to the configured database connections, you can provide your own explicitly specified DataSource to retrieve connections. At a minimum this DataSource have fields for `dbName` (primary key) and `dbStatus`. The request to retrieve database connections may be customized via [DatabaseBrowser.dbCriteria](#attr-databasebrowserdbcriteria), [DatabaseBrowser.dbFetchOperation](#attr-databasebrowserdbfetchoperation) and [DatabaseBrowser.dbFetchRequestProperties](#attr-databasebrowserdbfetchrequestproperties).

**Flags**: IR

---
## Attr: DatabaseBrowser.schema

### Description
The name of the database schema to use. Leave this property unset to include all schemata. Note that this property is not applicable to the MySQL database, which does not recognize the concept of multiple schemata within a database.

Note that this property only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

**Flags**: IR

---
## Attr: DatabaseBrowser.dbName

### Description
The name of the database configuration currently being displayed. If [showDatabaseList](#showdatabaselist) is true, this property will be updated when the user selects a database configuration from the list. Otherwise, if `dbName` property is not explicitly set the default database will be displayed.

Note that this property only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

**Flags**: IR

---
## Attr: DatabaseBrowser.dataGrid

### Description
Instance of ListGrid used to display the actual data in the table selected in the [schemaTree](#attr-databasebrowserschematree).

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
Optional [OperationBinding.operationId](OperationBinding.md#attr-operationbindingoperationid) to pass to the [DatabaseBrowser.databaseDataSource](#attr-databasebrowserdatabasedatasource) when retrieving the set of databases to display in the [database list](#showdatabaselist).

**Flags**: IRA

---
## Attr: DatabaseBrowser.showDataseList

### Description
Should the list of configured databases be shown to the user.

Only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

**Flags**: IR

---
## Attr: DatabaseBrowser.dbFetchRequestProperties

### Description
Optional dsRequest configuration for the fetch operation when retrieving the set of databases to display in the [database list](#showdatabaselist).

**Flags**: IR

---
## Attr: DatabaseBrowser.tableFetchRequestProperties

### Description
Optional dsRequest configuration for the fetch operation when retrieving the set of tables and views for a selected database.

**Flags**: IR

---
## Attr: DatabaseBrowser.dbCriteria

### Description
Optional criteria to pass to the [DatabaseBrowser.databaseDataSource](#attr-databasebrowserdatabasedatasource) when retrieving the set of databases to display in the [database list](#showdatabaselist).

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

To allow custom behavior retrieving the set of schemas within a database, you can provide your own explicitly specified DataSource to retrieve connections. At a minimum this DataSource have must have field `schemaName`

**Flags**: IR

---
## Attr: DatabaseBrowser.includeSubstring

### Description
If set, specifies a substring which must exist in a table name for it to be included in this DatabaseBrowser. If this property is set to a List of strings, table names are included if they match any one of the strings. The comparison is case-insensitive.

For example, `includeSubstring: ["E", "qry"]` would match all the following table names: "table", "QryTbl", "QRY", "ORDERS"

**Deprecated**

**Flags**: IR

---
## Attr: DatabaseBrowser.catalog

### Description
The name of the database catalog to use, if the RDBMS in use recognizes the concept of multiple catalogs. Leave this property unset to include all catalogs.

Note that this property only applies where [DatabaseBrowser.serverType](#attr-databasebrowserservertype) is "sql"

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
