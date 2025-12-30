# Admin Console

[← Back to API Index](../reference.md)

---

## KB Topic: Admin Console

### Description
The admin console groups together heap of other tools into one user interface in order to make it easier to find and work with these tools. It also provides you with links to some tools which do not fit into the admin console but are standalone tools.

NOTE: To use the Admin Console, you must have the Isomorphic SmartClient package installed and your servlet engine started. Direct your browser to the following URL to access the Admin Console:

  [http://localhost:8080/tools/adminConsole.jsp](http://localhost:8080/tools/adminConsole.jsp)

The common default servlet engine port 8080 is used in the URL given above. Adjust your URL as necessary if you are using a different port and replace localhost with the machine name running the servlet engine if you are accessing it from a remote machine.

The Admin Console UI comes with a number of tabs at the top, each representing a different tool, below you will find a description of what each tab/tool offers.

**Database Configuration**

On this tab you will be able to see any available JNDI connections. If you aren't using JNDI, you can use the GUI to enter and test JDBC settings. Both ConnectionManager and JDBC DataSource settings are supported. Once you've got a working connection, set it as the default connection using the "Set as Default" button.

**Import DataSources**

The database configuration tool allows you to configure database access for DataSources that use SmartClient's built-in [SQL engine](sqlDataSource.md#kb-topic-sql-datasources). See [database configuration tool](dbConfigTool.md#kb-topic-database-configuration-tools) for a more in depth explaination of this tool.

**Server Logs**

Just like in the [Developer Console](debugging.md#kb-topic-debugging) this will allow you to see the 500 most recent server side log entries.

**SQL Browser**

On this tab you will be able to browse your SQL databases and see the data in their tables.

**Scheduler**

With the scheduler tool you can view, trigger and paus any of your Quartz jobs.

**Other Tools**

Here you will find links to other useful tools which are not appropriate to put into a tab in the Admin Console.

### See Also

- [toolsDeployment](toolsDeployment.md#kb-topic-tools-deployment)

---
