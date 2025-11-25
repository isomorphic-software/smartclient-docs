# Database Configuration

[← Back to API Index](../main.md)

---

## KB Topic: Database Configuration

### Description
DataSources that use SmartClient's built-in [SQL engine](sqlDataSource.md#kb-topic-sql-datasources) refer to configuration settings from the [server.properties](server_properties.md#kb-topic-serverproperties-file) file for database access.

Developers may make use of the [Admin Console tool](adminConsole.md#kb-topic-admin-console) to set up database configuration blocks, or they may add configuration settings to `server.properties` by hand. Note that you should restart your servlet engine after changing this file.

**Manually specifying database connection settings**

Within an application deployment, the [server.properties](server_properties.md#kb-topic-serverproperties-file) file resides in the `WEB-INF/classes` directory.

For each database, configuration settings within this file are prefixed with `"sql._`<dbName>`_"`.  
For example, the following settings are the defaults in a new SmartClient installation for a MySQL server; they are approximately correct for a MySQL server running on the same machine as the servlet engine and listening on the default MySQL port. For details of what each of these properties means, check [this page](sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties).

```
   sql.Mysql.database.type: mysql
   sql.Mysql.database.ansiMode: false
   sql.Mysql.interface.type: dataSource
   sql.Mysql.driver: com.mysql.jdbc.jdbc2.optional.MysqlDataSource
   # name of the database to use
   sql.Mysql.driver.databaseName: isomorphic
   # hostname and port where the database server is installed
   sql.Mysql.driver.serverName: localhost
   sql.Mysql.driver.portNumber: 3306
   # username and password that can create and modify tables in that database
   # this user must have the following privileges for the system to function
   # properly: create/alter/drop table; insert/update/replace/delete rows.
   sql.Mysql.driver.user: root
   sql.Mysql.driver.password:
 
```
Note the distinction here between database _type_ and database _name_. Database type refers to the actual product - Oracle, DB2 or whatever. In the above example, database type is "mysql" (all lowercase) - the value of property `sql.Mysql.database.type`. Database type is very important. The type of a given database connection dictates whether features like SQL paging and transactions are supported; it even dictates the syntax of the SQL we generate.

Database name is just an arbitrary name for a particular database connection, and it is embedded in the property names immediately after the `sql` prefix. In this example it happens to be very similar to the database type - "Mysql" as opposed to "mysql" - but in fact the name has no significance and could be any string. When referring to specific database connections in your [DataSources](../classes/DataSource.md#class-datasource) with the [dbName](../classes/DataSource.md#attr-datasourcedbname) property, it is the database _name_ you use.

NOTE: It is common for DataSources to not specify `dbName`. In this case, the default database is used. To specify the default database manually in [server.properties](server_properties.md#kb-topic-serverproperties-file), set `sql.defaultDatabase`, using database name. So, to set our example connection from above as the default:

```
   sql.defaultDatabase: Mysql
 
```

**Manually specifying JNDI settings**

Instead of specifying database connection parameters directly in [server.properties](server_properties.md#kb-topic-serverproperties-file), it is possible to connect to a database that is configured as a JNDI resource in your application server. Assume you have an Oracle JNDI resource with the name "jndiTest", configured similar to this in Tomcat:

```
   <Resource name="jdbc/jndiTest"
                    auth="Container"
                    type="javax.sql.DataSource"
                    driverClassName="oracle.jdbc.driver.OracleDriver"
                    url="jdbc:oracle:thin:@192.168.132.152:1521:xe"
                    username="system"
                    password="manager"
                    initialSize="5"
                    maxActive="50" />
 
```
The minimal set of properties required to create a SmartClient database connection that attaches to this resource is as follows (Note that the `java:comp/env/` prelude in the first line is optional - the server will automatically look there if it can't find the resource in the absolute location)
```
   sql.myOracleConnection.driver.name: java:comp/env/jdbc/jndiTest
   sql.myOracleConnection.database.type: oracle
   sql.myOracleConnection.interface.type: jndi
 
```

### See Also

- [adminConsole](adminConsole.md#kb-topic-admin-console)
- [server_properties](server_properties.md#kb-topic-serverproperties-file)
- [sqlConnectionPooling](sqlConnectionPooling.md#kb-topic-sql-connection-pooling)
- [testData](testData.md#kb-topic-test-data)

---
