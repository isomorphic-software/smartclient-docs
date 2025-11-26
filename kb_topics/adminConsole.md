# Admin Console

[← Back to API Index](../reference.md)

---

## KB Topic: Admin Console

### Description
The Admin Console is a tool for configuring database access, importing and exporting server-backed SmartClient DataSources, and performing other tasks.

It can be found at _tools/adminConsole.jsp_ within the SmartClient SDKPackage, so if you're running your servlet engine on localhost:8080, it can be reached at  
[http://localhost:8080/tools/adminConsole.jsp](http://localhost:8080/tools/adminConsole.jsp)

_Features:_

**Database Configuration**

This tab allows you to configure SQL database connetions. This is an alternative to adding SQL configuration blocks directly to [server.properties](server_properties.md#kb-topic-serverproperties-file) by hand. See the [database configuration](dbConfigTool.md#kb-topic-database-configuration) documentation for more details.

**View DataSources**

The [DataSource Navigator](dataSourcesTab.md#kb-topic-datasources-tab) lets you view the available DataSources in dedicated sections, where you can also edit and export records.

**Import DataSources**

This tab allows you to generate and populate database tables from DataSource definitions.

All DataSources defined in XML (as described [here](dataSourceDeclaration.md#kb-topic-creating-datasources)) are displayed in a list. Developers may select any dataSource to see details of the dataSource and preview its data if any exists.

For DataSources of [type](../reference_2.md#type-dsservertype) `"sql"` or `"hibernate"`, the buttons at the bottom of this tab allow users to create a new database table for the DataSources. Test data may be imported test data, either from an existing [test data file](../classes/DataSource.md#attr-datasourcetestdata) or by uploading [CSV, JSON or XML formatted data](testData.md#kb-topic-test-data).

**Server Logs**

Just like in the [Developer Console](debugging.md#kb-topic-debugging) this will allow you to see the 500 most recent server side log entries.

**SQL Browser**

On this tab you will be able to browse your SQL databases and see the data in their tables. You may also create DataSources from those tables and save them to disk, at the location specified by a `project.datasources.generated` [config property](server_properties.md#kb-topic-serverproperties-file) (by default the same as the `project.datasources` property).

**Scheduler**

With the [scheduler tool](quartzAdapters.md#kb-topic-quartz-datasources) you can view, schedule, trigger and pause arbitrary [Quartz](http://www.quartz-scheduler.org) jobs. Requires the Isomorphic Scheduler server library and an [initialized](https://www.quartz-scheduler.org/documentation/2.4.0-SNAPSHOT/cookbook/ServletInitScheduler.html) / [configured](https://www.quartz-scheduler.org/documentation/2.4.0-SNAPSHOT/configuration.html) Quartz Scheduler.

**Other Tools**

Here you will find links to some other standalone development tools.

### See Also

- [toolsDeployment](toolsDeployment.md#kb-topic-tools-deployment)

---
