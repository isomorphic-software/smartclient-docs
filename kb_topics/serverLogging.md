# Server logging

[← Back to API Index](../reference.md)

---

## KB Topic: Server logging

### Description
#### Default logging

SmartClient's server-side classes have extensive built-in diagnostics which are output via the [Apache Log4j 2 library](https://logging.apache.org/log4j/2.x/) (see below for other alternatives).

At startup, SmartClient will automatically load the file `log4j2.isc.config.xml` from the classpath and use it to configure Log4j 2. `log4j2.isc.config.xml` is in Log4j2's standard [XML configuration format](https://logging.apache.org/log4j/2.x/manual/configuration.html#XML), and sets default log threshold levels for various subsystems to produce output that is generally appropriate for both development and production systems. Various SmartClient documentation may encourage you to enable certain diagnostic logs using this file when troubleshooting specific problems.

There's a `iscLog4jConfiguration` JVM argument, which if explicitly set will be used instead of the default `log4j2.isc.config.xml` configuration file. It should point to an alternative configuration file using the same Log4j2's standard [XML configuration format](https://logging.apache.org/log4j/2.x/manual/configuration.html#XML):

```
 -DiscLog4jConfiguration=log4j2.custom.config.xml
 
```
Note if the `iscLog4jConfiguration` is present, but the configuration file could not be loaded, Smartclient will fallback to default `log4j2.isc.config.xml` configuration.

#### Server Logs tab (SmartClient Developer Console)

The Server Logs tab of the [SmartClient Developer Console](debugging.md#kb-topic-debugging) provides the ability to view the most recent 10000 log entries, and change log threshold levels dynamically at runtime.

Note that the features of the "Server Logs" tab will **only** be available if using Log4j 2 API with the default Log4j 2 implementation.

#### Configure custom log4j loggers

If Log4j2 is used and custom loggers are configured in `log4j2.isc.config.xml` file, use `DataTools.getLoggerContext()` method to access them on server side, like this:

```
 DataTools.getLoggerContext().getLogger(CustomClass.class.getName());
 
```
#### Redirecting logging to Slf4j framework

_**Deprecated.** Slf4j is intended to be a generic API that you can log to, which can be configured to talk to various logging frameworks. However, Log4j 2 now offers the same capability of plugging in alternate logging frameworks, and the generic logging API is better than Slf4j, making Slf4j support obsolete and deprecated._

SmartClient server logging can alternatively use the Simple Logging Facade for Java (slf4j), which allows logs to be sent to a variety of different logging frameworks that support Slf4j.

To send all logging to slf4j, the `iscUseSlf4j` VM argument must be set to true on the command line, like this:

```
 -DiscUseSlf4j=true
 
```
#### Legacy: using Sfl4j to continue to use Log4j 1.x

It is still possible to use Log4j 1.x via the Slf4j. And even when the Slf4j will not be directly supported by the Smartclient there will be an option to redirect Log4j 2 API to the Slf4j + Log4j 1.x combo by using the [Log4j 2.x to Slf4j binding](https://logging.apache.org/log4j/2.x/log4j-to-slf4j/index.html).

Note that the only reason to do this is that you've got heavy logging customizations that depend on Log4j 1.x, so you can't migrate to another logging system yet. However, if you use this setup, you should plan migration as soon as possible.

_See our [Logging migration](loggingMigration.md#kb-topic-logging-migration) recommendations on how to move to Log4j 2.x._

#### Third-party libraries depending on Slf4j

Smartclient uses Quartz Scheduler 2.3.1 and also continues to support Hibernate 3, both of which depend on Slf4j for their internal logging. So, we are shipping with the set of dependencies redirecting Hibernate and Quartz logging to the Log4j 2 using the [Log4j 2.x Slf4j binding](https://logging.apache.org/log4j/2.x/log4j-slf4j-impl/index.html) approach, so that the internal logging goes: _Hibernate -> Slf4j -> Slf4j to Log4j 2.x binding -> Log4j 2.x_.

#### Special logging category: com.isomorphic.SLOW\_SQL

Used to log slow SQL queries. SQL query is considered "slow" if its execution time exceeds configured threshold, see the global _sql.log.queriesSlowerThan_ [server.properties SQL setting](sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties) and more specific [DataSource.logSlowSQL](../classes/DataSource.md#attr-datasourcelogslowsql) setting for more details.

Set category logging level to "DEBUG" to log all slow queries:

```
 <Logger name="com.isomorphic.SLOW_SQL" level="DEBUG" />
 
```
or enable logging for specific [operation types](../reference.md#type-dsoperationtype):
```
 <Logger name="com.isomorphic.SLOW_SQL.fetch" level="DEBUG" />
 <Logger name="com.isomorphic.SLOW_SQL.add" level="DEBUG" />
 <Logger name="com.isomorphic.SLOW_SQL.update" level="DEBUG" />
 <Logger name="com.isomorphic.SLOW_SQL.remove" level="DEBUG" />
 <Logger name="com.isomorphic.SLOW_SQL.custom" level="DEBUG" />
 
```
#### Special logging category: com.isomorphic.SQL

Used to log all SQL queries even if other `com.isomorphic.sql.*` loggers are disabled. Set category logging level to "INFO" to log all queries or to "DEBUG" to get additional details. For example:

```
 <Logger name="com.isomorphic.SQL" level="INFO" />
 
```
#### Special logging category: com.isomorphic.SQL\_ERROR

This category is used to log SQL errors, including the full SQL statement that caused the error, regardless of other logging settings. It must be set to "DEBUG":

```
 <Logger name="com.isomorphic.SQL_ERROR" level="DEBUG" />
 
```

---
