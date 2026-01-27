# SQL Connection Pooling

[← Back to API Index](../reference.md)

---

## KB Topic: SQL Connection Pooling

### Description
**This discussion applies primarily to the built-in SQL DataSource provided in Pro and better editions of SmartClient, though elements of it also apply to the built-in Hibernate and JPA DataSources**

SQLDataSource communicates with database products using [JDBC Connection objects](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html). These Connections are provided by the individual database products' JDBC drivers; they either wrap the database's native mechanism for a client-server connection, or they implement a pure Java equivalent of the same thing. All read and update operations performed by SQL DataSource take place via one of these connections. Also, [SQL transactions](#attr-datasourceautojointransactions) are implemented by having the queue of related updates take place through the same connection, with a single commit (or rollback) at the end of the queue.

Database connections are a limited resource, and they can also be expensive to acquire. For both of these reasons, SmartClient by default uses the Apache DBCP pooling library to maintain a pool of resuable connections. Connections are borrowed from the pool as required, and returned to the pool when they are no longer needed, and the pooling library ensures that connections are only lent out to one borrowing process at any given time. This arrangement is efficient in terms of both connection acquisition speed and the number of connections required

*   Reusing an existing connection is typically faster than asking the database for a new one; depending on the database, it can be much faster
*   Reusing the same connections over and over means that applications require fewer connections to handle the same workload. Even busy applications handling hundreds of concurrent users typically require a much smaller number of pooled connections than might be thought at first glance

For these reasons, we ship SmartClient with connection pooling switched on, and we recommend you leave it that way.
#### Connection pool settings
You configure the behavior of SQL connection pooling with the following `server.properties` settings (note, many of these settings map directly to settings in the underlying DBCP library; you can find out more about their effects in the [DBCP docs](http://commons.apache.org/proper/commons-dbcp/configuration.html)):

| sql.pool.enabled | Set true/false to enable or disable the entire SQL connection pooling feature. Defaults to true |
|---|---|
| sql.pool.maxActive | Maximum number of "active" (ie, currently lent out) connections. Defaults to -1, which means "no limit" |
| sql.pool.maxIdle | Maximum number of "idle" (ie, currently sitting in the pool, not lent out) connections. Defaults to -1, which means "no limit" |
| sql.pool.minIdle | Minimum number of "idle" (ie, currently sitting in the pool, not lent out) connections. If the pool drops below this number of idle connections, new ones will be created. Defaults to -1, which means "no minimum" |
| sql.pool.whenExhaustedAction | Specifies what the pool should do if the system attempts to borrow a connection and there are no idle connections to lend."fail" will throw an Exception and the SQL operation will fail"block" will cause the borrowing thread to block until a connection becomes available"grow" will create a new connection, add it to the pool, and then return it to the borrowing thread. Note, if you use this strategy, the "maxActive" setting has no effectThe default value is "grow" |
| sql.pool.testOnBorrow | If true, we attempt to validate the connection before lending it out. This validation involves checking if the connection is marked as closed, and also running a "pingTest" query if one is defined (see the section on per-database configuration, below). If validation fails, the connection is discarded and another one selected from the pool. Defaults to true |
| sql.pool.testOnReturn | The same as testOnBorrow, but the checking occurs when the connection is returned to the pool rather than when we are about to lend it out. Defaults to false |
| sql.pool.testWhileIdle | The same as testOnBorrow, but the checking is done by the idle connection evictor (see below) during its periodic inspection of the idle objects in the pool. Defaults to false |
| sql.pool.timeBetweenEvictionRunsMillis | DBCP can optionally run an "idle connection evictor" thread, which periodically checks the pool for connections that have been idle for more than a threshold time, and "evicts" them from the pool (ie, closes and then discards them). The purpose of this is to keep the connection pool at the intended size, instead of allowing it to remain at whatever size it reached during the system's busiest time. Without an evictor, it would not be unusual to see the number of connections in the pool grow towards maxActive over time, or even beyond it if the pool is configured to grow when exhausted. If this is not what you want, configure an eviction thread. However, note that the eviction thread contends with the main pooling code for access to the idle connections; if you set the evictor to run very frequently, it can introduce performance issues.This property specifies the number of milliseconds to sleep between runs of the idle connection evictor. If set to a negative value, no evictor will be run. Defaults to -1 (ie, no eviction thread) |
| sql.pool.minEvictableIdleTimeMillis | The minimum time a connection may sit idle in the pool before it is eligible for eviction. If set to a negative value, connections will never be evicted due to the length of time they have sat idle (a connection will only be evicted if testWhileIdle is true and it fails validation). Defaults to -1 |
| sql.pool.numTestsPerEvictionRun | The number of connections to check during each eviction run. Defaults to -1, which means check all objects in the pool (this is not documented by Apache, but negative values are treated as the denominator in determining a fraction of the pool size, so -2 means check half the connections, -3 means check a third, etc) |

In addition to the `sql.pool` configuration subtree, you can specify per-database configuration by adding the [dbName](../classes/DataSource.md#attr-datasourcedbname) to the property, like so:

```
     sql.mydatabase.pool.enabled: true
     sql.mydatabase.pool.numTestsPerEvictionRun: 10
     # etc...
 
```
There is also a configuration property outside the `sql.pool` and `sql.{DBNAME}.pool` trees that is nevertheless part of SQL connection pooling configuration. This property, `sql.{DBNAME}.pingTest`, should be a small SQL fetch query, ideally a dummy fetch that runs very quickly and returns a single row. As discussed above, this "pingTest", if configured, is used to determine if a connection is valid before lending it out. Most databases have a traditional, proprietary query that fits the bill, but it varies by database. Some example pingTest queries:
```
     # Oracle
     sql.OracleDatabase.pingTest: select 1 from dual
     # SQL Server
     sql.mssqlserverdb.pingTest: select 'x'
     # DB2
     sql.db2database.pingTest: select 'x' from SYSIBM.SYSDUMMY1
 
```
#### Troubleshooting issues related to connection pooling
Many databases will automatically close inactive connections, which can interfere with connection pooling: if an application is not constantly using all of the connections in its pool, it may retrieve a closed connection from the pool.

In some cases you can disable the behavior of closing inactive connections. For MySQL it's controlled by the [wait\_timeout](http://dev.mysql.com/doc/refman/5.0/en/server-system-variables.html#sysvar_wait_timeout) setting in your my.cnf file). However, this could potentially cause leaked connections if applications terminate without cleaning up their database connections.

Intelligent connection pools compensate for unexpectedly closed connections automatically:

*   J2EE containers generally implement internal keepalives or staleness checks - this is the preferred solution if available. If using SQLDataSource, use JNDI-based configuration as described [here](dbConfigTool.md#kb-topic-database-configuration).
*   SQLDataSource uses DBCP (Apache Commons) pooling, which also compensates for connection closure automatically. This is enabled by default with appropriate settings, but can be disabled system wide via setting **sql.pool.enabled** to false in [server.properties](server_properties.md#kb-topic-serverproperties-file), or disabled for a specific database configuration via **sql._dbName_.pool.enabled**. The following properties can also be set on sql.pool / sql._dbName_.pool and control same-named DBCP properties, however, it is not recommended to set these properties unless you have experience with DBCP and are troubleshooting a specific pool-related performance problem: testOnBorrow, testOnReturn, testWhileIdle, timeBetweenEvictionRunsMillis, minEvictableIdleTimeMillis, numTestsPerEvictionRun.
    
    When the pool is configured for connection validation, as it is by default, a SQL statement is run to verify the condition of its connection. To control the timeout value on this statement, set the sql.validationQueryTimeout / sql.dbName.validationQueryTimeout property (in seconds, default value is 10).
    
    If you are trying to diagnose an issue related to SQL connection pooling, you can enable DEBUG logging for the following classes in `log4j.isc.config.xml` (see installation instructions for details about this file). All of these classes are in package `com.isomorphic.sql`:
    
    *   PoolableSQLConnectionFactory: logs connection creation, and whether or not the connections are pooled
    *   SQLConnectionManager: logs when connections are borrowed
    *   SQLDriver: logs the hashCode of the connection when SQL statements are executed
    *   SQLTransaction: logs transactional open, commit, rollback and close.
*   JPA/Hibernate: Hibernate's built-in connection pool is **not** intended for production use according to Hibernate's own documentation. This includes using JPA with Hibernate as the provider. If you get dead connections during development you can disable Hibernate's built-in connection pool by setting "hibernate.connection.pool\_size" to 0. For production use you must use production-ready connection pool libraries for example C3P0. Here are recommended settings for C3P0 properties:
    *   c3p0.acquireRetryDelay=1000
    *   c3p0.acquireRetryAttempts=60
    *   c3p0.breakAfterAcquireFailure=false

---
