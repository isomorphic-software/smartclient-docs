# Server logging

[← Back to API Index](../reference.md)

---

## KB Topic: Server logging

### Description
#### Default logging

SmartClient's server-side classes have extensive built-in diagnostics which are output via the [Apache Log4j library](http://logging.apache.org/log4j/1.2/) (see below for other alternatives).

At startup, SmartClient will automatically load the file `log4j.isc.config.xml` from the classpath and use it to configure Log4j. `log4j.isc.config.xml` is in Log4j's standard [XML configuration format](http://wiki.apache.org/logging-log4j/Log4jXmlFormat), and sets default log threshold levels for various subsystems to produce output that is generally appropriate for both development and production systems. Various SmartClient documentation may encourage you to enable certain diagnostic logs using this file when troubleshooting specific problems.

There's a `iscLog4jConfiguration` JVM argument, which if explicitly set will be used instead of the default `log4j.isc.config.xml` configuration file. It should point to an alternative configuration file using the same Log4j's standard [XML configuration format](http://wiki.apache.org/logging-log4j/Log4jXmlFormat):

```
 -DiscLog4jConfiguration=log4j.custom.config.xml
 
```
Note if the `iscLog4jConfiguration` is present, but the configuration file could not be loaded, Smartclient will fallback to default `log4j.isc.config.xml` configuration.

#### Server Logs tab (SmartClient Developer Console)

The Server Logs tab of the [SmartClient Developer Console](debugging.md#kb-topic-debugging) provides the ability to view the most recent 500 log entries, and change log threshold levels dynamically at runtime.

#### Redirecting logging to other frameworks

SmartClient server logging can alternatively use the Simple Logging Facade for Java (slf4j), which allows logs to be sent to a variety of different logging frameworks that support slf4j.

To send all logging to slf4j, the `iscUseSlf4j` VM argument must be set to true on the command line, like this:

```
 -DiscUseSlf4j=true
 
```
If slf4j is used and the underlying log system is still Log4j, SmartClient will still configure Log4j using `log4j.isc.config.xml` as describe above _unless_ you pass an additional command line argument to prevent this:
```
 -DiscUseLog4jConfig=false
 
```
If slf4j is used with any other logging system, SmartClient will not attempt to apply configuration - see the [SLF4J user manual](http://www.slf4j.org/manual.html) for details on how to configure slf4j.

Note that the features of the "Server Logs" tab will **not** be available if using slf4j, even if Log4j is also used.

#### Configure custom log4j loggers

If log4j is used and custom loggers are configured in `log4j.isc.config.xml` file, use `DataTools.getLoggerRespository()` method to access them on server side, like this:

```
 DataTools.getLoggerRepository().getLogger(CustomClass.class.getName());
 
```

#### Special logging category: com.isomorphic.SLOW\_SQL

Used to log slow SQL queries. SQL query is condidered "slow" if its execution time exceeds configured threshold, see the global _sql.log.queriesSlowerThan_ [server.properties SQL setting](sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties) and more specific [DataSource.logSlowSQL](../classes/DataSource.md#attr-datasourcelogslowsql) setting for more details.

Set category logging level to "DEBUG" to log all slow queries:

```
 <category name="com.isomorphic.SLOW_SQL">
    <priority value="DEBUG" />
 </category>
 
```
or enable logging for specific [operation types](../reference.md#type-dsoperationtype):
```
 <category name="com.isomorphic.SLOW_SQL.fetch">
    <priority value="DEBUG" />
 </category>
 <category name="com.isomorphic.SLOW_SQL.update">
    <priority value="DEBUG" />
 </category>
 
```

---
