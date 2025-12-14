# server.properties file

[← Back to API Index](../reference.md)

---

## KB Topic: server.properties file

### Description
The `server.properties` file is a configuration file read by the SmartClient server - see the file itself for more information and default or sample settings.

Note that this is a standard Java Properties file, except it allows variable substitution from other properties defined earlier in the file.

It's loaded from the `CLASSPATH`, so it can be anywhere in the `CLASSPATH`, but is typically either in the projects java "src" directory or in `WEB-INF/classes`.

Server side code can access and modify the properties specified in this file via the `com.isomorphic.base.Config` class.

When modifying `server.properties` developers should restart the servlet engine after changing this file to pick up changes.

The following settings are used by SmartClient server features.  
_Note that this is not intended to be an exhaustive list_:

*   `project.datasources` specifies the location for [server-backed DataSource configuration files _(\*.ds.xml files)_](dataSourceDeclaration.md#kb-topic-creating-datasources) as well as [server-backed SimpleType declarations _(\*.type.xml files)_](../classes/SimpleType.md#class-simpletype)
*   `project.ui` specifies the location for [XML Screen definitions _(\*.ui.xml files)_](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen)
*   `project.project` specifies the location for [XML Project definitions _(\*.project.xml files)_](../classes/RPCManager.md#classmethod-rpcmanagerloadproject)
*   `project.apps` specifies the location for [Application declarations _(\*.app.xml files)_](applicationDeclaration.md#kb-topic-application-declaration-files)
*   `modulesDir` specifies the location for modules files if using the [loadISC](loadISCTag.md#kb-topic-isomorphicloadisc) or [loadModules](../reference.md#kb-topic-isomorphicloadmodules) jsp tags.
*   `isc.addVersionToLoadTags` (boolean) May be set to false to disable the automatic versioning applied to URLs written out by [loadISC](loadISCTag.md#kb-topic-isomorphicloadisc) or [loadModules](../reference.md#kb-topic-isomorphicloadmodules) jsp tags.
*   `isc.defaultVersionStyle` specifies the default `versionStyle` for [loadISC](loadISCTag.md#kb-topic-isomorphicloadisc) or [loadModules](../reference.md#kb-topic-isomorphicloadmodules) jsp tags. Default value is "params".
*   `isc.versionPathSegmentPrefix` Specifies a standard path segment prefix written out by [loadISC](loadISCTag.md#kb-topic-isomorphicloadisc) or [loadModules](../reference.md#kb-topic-isomorphicloadmodules) jsp tags with `versionStyle` set to "pathSegment". The generated path segment will consist of this prefix combined with the current SmartClient version. The default value is `"isc_version."`.
*   `isc.stripVersionPathSegments` (boolean) When set to true, any URL containing a path segment that starts with the `isc.pathSegmentPrefix` will be automatically stripped by the SmartClient FileDownloadServlet, or the dedicated VersionedURLFilter when resolving the URL to a resource on the filesystem.  
    This may be disabled if you want to use a different strategy such as using Apache mod\_rewrite on a dedicated web server to resolve URLs including versioned path segments.
*   `authentication.defaultRequired` can be used to require [authentication](../classes/DataSource.md#attr-datasourcerequiresauthentication) for all dataSources by default
*   `authentication.superuserRole` can be used to identify a [user role](../classes/OperationBinding.md#attr-operationbindingrequiresrole) as the super user role.
*   This file can contain [DataBase configuration settings for SQL DataSources](dbConfigTool.md#kb-topic-database-configuration). Note that the [Admin Console tool](adminConsole.md#kb-topic-admin-console) provides an interface for adding database configuration blocks to server.properties without the need to edit the file by hand.
*   This file can contain [SQL Connection pooling](sqlConnectionPooling.md#kb-topic-sql-connection-pooling) settings for SQL DataSources.
*   This file can contain various configuration properties used for [jpaIntegration](jpaIntegration.md#kb-topic-integration-with-jpa)
*   This file can contain SMTP configuration settings for the [OperationBinding.mail](../classes/Mail.md#class-mail) feature.
*   This file can contain configuration settings for the [optional RealTimeMessaging module](messaging.md#kb-topic-real-time-messaging).
*   `enabledBuiltins` can be used to configure access to methods provided by the server side `BuiltInRPC` class. (See server side JavaDoc for that class as well as the [tools deployment overview](toolsDeployment.md#kb-topic-tools-deployment) for more information).
*   `domainSync.disabled` and `domainSync.baseDomains` can be used to [configure domain synching behavior](xssAndCSRFSecurity.md#kb-topic-xss-and-csrf-security).
*   `import.consume.bom` can be set to false to switch off automatic consumption of Byte Order Markers when importing UTF data (see the server Javadocs for the DataImport class for more details)
*   `datasources.autoConvertRelativeDates` can be used to change when relative dates are converted or to entirely disable the automatic conversion (see [DataSource.autoConvertRelativeDates](../classes/DataSource.md#attr-datasourceautoconvertrelativedates) for more details)
*   `reflection.classCache` specifies how (if enabled) Smartclient Reflection library caches loaded classes, availables values are "global", "classloader" (default), "jdk" and "off". See comment in server.properties for more details.
*   `sql.log.formatQueries` can be set to `true` to enable the SQL queries formatting in [server logs](serverLogging.md#kb-topic-server-logging) under `com.isomorphic.sql.SQLDriver` category
*   `sql.log.compactFormatting` can be set to `true` to make formatted SQL queries more compact
*   `sql.log.maxLength` can be set to an integer controlling the maximum length of formatted SQL queries
*   `sql.log.queriesSlowerThan` can be set to an integer controlling SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category. See [DataSource.logSlowSQL](../classes/DataSource.md#attr-datasourcelogslowsql) for more details.
*   `sql_comment_mdc_key` if specified is used as a logging MDC key to get the configurable "log\_correlation\_id" third party tools, like Dynatrace, Graylog etc., use for the context. Smartclient picks that from the logging MDC and adds as a comment to the end of generated SQL queries, so those can be connected to the context.

---
