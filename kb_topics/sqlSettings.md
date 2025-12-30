# SQL Database Settings in server.properties

[← Back to API Index](../reference.md)

---

## KB Topic: SQL Database Settings in server.properties

### Description
Although the Admin Console provides a UI to let you to configure database access for DataSources that use SmartClient's built-in [SQL engine](sqlDataSource.md#kb-topic-sql-datasources), it is also possible to configure these DataSources with manual entries in your [server.properties](../reference.md#kb-topic-serverproperties-file) file.

When you manually configure a DataSource like this, you do so by maintaining a set of properties with names structured like this:

```
   sql.{dbName}.x.y
 
```
where `{dbName}` is the name of the database configuration you are providing. Note that this database name is just an arbitrary name for a particular database configuration; many of the default ones provided with SmartClient are named after a database _type_, in order to make their intended use more immediately obvious, but this is not by any means a requirement.

For the remainder of this discussion, we will assume we are configuring a database with a name of "MyDatabase".

#### SQL configuration properties

**`sql.MyDatabase.database.type`**  
This should be set to one of the supported database types. These are:

| hsqldb | HSQLDB 1.7.x and greater |
|---|---|
| db2 | IBM DB2 8.x and greater |
| db2iSeries | IBM DB2 for iSeries/i5, V5R4 and greater |
| firebirdsql | Firebird 2.5 and greater |
| informix | Informix 11.5 and greater |
| sqlserver | Microsoft SQL Server 2000 and greater |
| mysql | MySQL 3.2.x and greater |
| mariadb | MariaDB 5.1 and greater |
| oracle | Oracle 8.0.5, 8i and greater |
| postgresql | PostgreSQL 7.x and greater |
| generic | A generic SQL92 database, with limitations described in [this article](sqlDataSource.md#kb-topic-sql-datasources) |

`**sql.MyDatabase.driver**`  
The name of the JDBC driver implementation. This depends upon your database product and version, and the specific JDBC driver you are using (JDBC drivers can usually be downloaded from your database vendor's website). Bearing in mind the caveat that this information can vary by release and JDBC implementation, here are some suggested values for our supported databases:

| hsqldb | org.hsqldb.jdbcDriver |
|---|---|
| db2 | com.ibm.db2.jcc.DB2DataSource |
| db2iSeries | com.ibm.as400.access.AS400JDBCDriver |
| firebirdsql | org.firebirdsql.jdbc.FBDriver |
| informix | com.informix.jdbc.IfxDriver |
| sqlserver | com.microsoft.jdbc.sqlserver.SQLServerDriver or com.microsoft.sqlserver.jdbc.SQLServerDriver (Microsoft changed the order of "jdbc" and "sqlserver" between the 2000 and 2005 editions of the product) |
| mysql | com.mysql.jdbc.jdbc2.optional.MysqlDataSource |
| mariadb | org.mariadb.jdbc.MariaDbDataSource |
| oracle | oracle.jdbc.driver.OracleDriver |
| postgresql | org.postgresql.Driver |

`**sql.MyDatabase.driver.serverName**`  
The name or IP address of the database server

`**sql.MyDatabase.driver.portNumber**`  
The port on which the database server is listening

`**sql.MyDatabase.driver.user**`  
The user to connect as

`**sql.MyDatabase.driver.password**`  
The user's password

`**sql.MyDatabase.driver.databaseName**`  
The database to connect to. A "database" in this context is a named collection of tables and other database resources that are somehow grouped together by the database product. The specifics of how this is implemented vary by database. Note that some database products use the terms "catalog" or "schema" to refer to the same concept, and Oracle - although it does also have a concept of catalog - uses the term "SID" for this concept.

`**sql.MyDatabase.interface.type**`  
Indicates how the JDBC connection will be created or looked up; the value of this setting depends on the capabilities of the particular JDBC driver you are using, and is inherently connected to the value of `sql.MyDatabase.driver`. The following settings are supported:

**dataSource** - the driver is an instance of `javax.sql.DataSource` and should be instantiated by SmartClient Server  
**driverManager** - the driver is an instance of `java.sql.DriverManager`  
**jndi** - the driver is an instance of `javax.sql.DataSource` and should be looked up using JNDI

`**sql.MyDatabase.driver.url**`  
For configurations where `sql.MyDatabase.interface.type` is "driverManager", this property allows you to manually enter the URL we use to connect to the database. If this property is not provided, we build the URL from other settings such as `sql.MyDatabase.driver.serverName` and `sql.MyDatabase.driver.databaseName`.

**Other properties**  
Different JDBC drivers support different properties to support product-specific quirks and features. You can often specify these properties by embedding them as parameters in the URL used to connect to the database.

Alternatively, any subproperty you set on the "driver" in server.properties is applied to the JDBC driver object via Reflection. For example, the MySQL JDBC driver supports a property "useUnicode", which forces the database to use Unicode character encoding. If `sql.MyDatabase.driver` is `com.mysql.jdbc.jdbc2.optional.MysqlDataSource`, setting `sql.MyDatabase.driver.useUnicode` to true means we'll attempt to call `setUseUnicode(true)` on this class. This would have exactly the same effect as defining the connection URL manually and specifying the parameter `useUnicode=true` Mysql vs MariaDB: there is broad compatibility between these two databases as described in [https://mariadb.com/kb/en/library/mariadb-vs-mysql-compatibility/](https://mariadb.com/kb/en/library/mariadb-vs-mysql-compatibility/). Within the bounds of that compatibility matrix, you can use database.type 'mysql' and 'mariadb' interchangeably, and likewise with the drivers that you use. However for future compatibility it is recommended that you use `database.type: mariadb` for MariaDB. This will ensure that as MariaDB implements new features and backompat breaking changes, your application won't run into any gotchas because the SmartClient server logic will automatically use the right feature set to accomplish documented behavior.

#### Smartclient properties

**`sql.mysql.optimizeCaseSensitiveCriteria`**  
_This setting affects all **MySQL** connectors and it is set to **true** by default._ Depending on [textMatchStyle](../reference.md#type-textmatchstyle) case sensitivity in text criteria is achieved by using LIKE BINARY sql comparison operator, which does not use indexed search. Indexes are used with regular "=" comparison operator, which does not ensure case sensitivity. With big amounts of data indexes are critical, so in order to use them and still have case sensitivity supported this setting must be set to `true` (default). This way we would generate comparison expression like:  
``<field>` = `<value>` AND `<field>` LIKE BINARY `<value>``  
where first part ensures efficient indexed search and second part adds case sensitivity to significantly reduced amounts of data. This would be more efficient without indexes as well, cause LIKE BINARY conversion would be performed on less rows anyway.  
Setting this property to `false` would bring back the old behavior, when only LIKE BINARY comparison would be used, which would return same results, but much slower.

**`sql.aliasLengthLimit` and `sql.MyDatabase.aliasLengthLimit`**  
These properties override the default table alias length limit when using features like [DataSourceField.includeVia](../classes/DataSourceField.md#attr-datasourcefieldincludevia). Default alias length limit is set accordingly to the documentation for supported databases and defaults to 128 characters, except these databases:

| firebirdsql | 63 |
|---|---|
| mysql | 256 |
| mariadb | 256 |
| oracle | automatically set to 128 since DB version 12.2 and to 30 for older versions |
| postgresql | 63 |

In order to support portability across databases it is advised to keep alias length limit at the lowest supported value. Use global setting `sql.aliasLengthLimit` to apply limit across all DB drivers, or use DB specific setting `sql.MyDatabase.aliasLengthLimit` (overrides the global one).

**`sql.postgresql.useILike`**  
Starting with version 12.0, SmartClient Server supports the use of a Postgres-specific comparison keyword, ILIKE. This keyword natively does a case-insensitive LIKE, so the SmartClient driver does not have to do what it normally does to enable this kind of comparison, which is to convert the filter value to lower case and then generate SQL like:

```
WHERE LOWER(someField) LIKE 'united%'
```
When ILIKE is in use, Postgres is able to make use of indexes, which it does not do when we use the "lowercase both sides" strategy, so this is a potentially significant performance enhancer, depending on your application:
```
 WHERE someField ILIKE 'United%'
```

---
