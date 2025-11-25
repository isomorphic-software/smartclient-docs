# DatabaseBrowser Documentation

[← Back to API Index](../main.md)

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
## Attr: DatabaseBrowser.serverType

### Description
The type of database server this DatabaseBrowser should connect to. Valid values are "sql" (SmartClient's own built-in support for SQL databases) or "hibernate"

**Flags**: IR

---
## Attr: DatabaseBrowser.databaseList

### Description
Instance of DynamicForm used to select a database from the list for display in the [schemaTree](#attr-databasebrowserschematree).

**Flags**: IR

---
## Attr: DatabaseBrowser.schemaTree

### Description
Instance of TreeGrid used to display the database schema (tables and columns)

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
The name of the database configuration to use. Database configurations are set up through the "Databases" tab of the Developer Console. If not set, defaults to the current default database configuration.

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
## Attr: DatabaseBrowser.includeSubstring

### Description
If set, specifies a substring which must exist in a table name for it to be included in this DatabaseBrowser. If this property is set to a List of strings, table names are included if they match any one of the strings. The comparison is case-insensitive.

For example, `includeSubstring: ["E", "qry"]` would match all the following table names: "table", "QryTbl", "QRY", "ORDERS"

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
