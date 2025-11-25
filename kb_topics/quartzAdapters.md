# Quartz DataSources

[← Back to API Index](../main.md)

---

## KB Topic: Quartz DataSources

### Description
Occasionally, it can be useful to provide a user interface to facilitate the management of background jobs. [Quartz](http://www.quartz-scheduler.org) is a very capable job scheduling library but does not bundle any user interface.

The Scheduler tab of the [Admin Console](adminConsole.md#kb-topic-admin-console) provides such a [user interface](../main.md#class-quartzmanager) by way of [server-side integration](serverDataIntegration.md#kb-topic-server-datasource-integration) that accepts standard fetch, add, update, and remove requests and translates them into the appropriate Quartz API calls.

Note that only cron schedules are supported at this time.

The Quartz\*.ds.xml DataSources found in the system/datasources directory use a [declarative security](declarativeSecurity.md#kb-topic-declarative-security) feature to limit access based on the presence of a special request attribute, and could be be used in your own application if desired by controlling how that attribute is set. Refer to the adminConsoleOperations JSP documented at [toolsDeployment](toolsDeployment.md#kb-topic-tools-deployment) for detail.

---
