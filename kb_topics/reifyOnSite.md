# Reify OnSite

[← Back to API Index](../main.md)

---

## KB Topic: Reify OnSite

### Description
**What is Reify OnSite?**

[Reify](reifyForDevelopers.md#kb-topic-reify-for-developers) is a cloud-based visual application builder in which users can build screens via drag-and-drop, create DataSources from sample data or using wizards, and visually define standard event handlers and multi-step workflows.

Reify OnSite is a special version of Reify that can be installed on your own network, behind your firewall, so that your data and intellectual property never leave your secure site. Applications are deployed to your private cloud, also behind your firewall. The tool itself can be configured for your specific requirements. DataSources that connect to internal enterprise data services are supported, [custom components](reify.md#kb-topic-reify-overview) can be added to the palette library, and the Reify design environment itself can even be customized on a per-user basis.

Reify OnSite is licensed separately from Reify.com accounts, and separately from SmartClient developer licenses, generally purchased as a either a fixed number of seats or unlimited within a group, site or company-wide. [Contact us here](https://www.reify.com/getStarted.jsp) to get started,

**Installation**

The OnSite package comes with an Embedded Tomcat server and pre-populated [HSQL database](http://hsqldb.org/) that's ready to be run with no additional setup required. If desired, it can be deployed to a separate servlet engine or run against a different database engine.

**Account Management**

Reify Designer Accounts are managed via a plain SQLDataSource, named "isc\_reifyUsers", which you can edit using the DataSources tab of the [Admin Console](adminConsole.md#kb-topic-admin-console) or [Developer Console](debugging.md#kb-topic-debugging). Within the DataSources tab, click on the "isc\_reifyUsers" DataSource record to open a section for editing user records, and click "add record" to add additional users. User records can be removed by clicking on the delete icon in the rightmost column of each record.

As shipped, a single user account, "admin" (password "reify"), is provided. To grant superuser privileges to additional accounts, just enter "superuser" for the "roles" field in the record.

**How Reify Stores your Designs and Data**

Reify uses [FileSource](fileSource.md#kb-topic-filesource-operations) DataSources to store your projects (`isc_hostedProjects` DS), screens (`isc_hostedScreens` DS), and DataSources (`isc_hostedDataSources` DS), rather than writing them to disk as files. These DataSources are shared for all users of your organization, so project and screen names must be unique.

**Deployment**

Reify OnSite runs your application in a dedicated sandbox (a separate database in HQL), with its own copy of each of your project [MockDataSources](../classes/MockDataSource.md#class-mockdatasource) instantiated as real SQL DataSources in the HSQL database. This process is called _deployment_. DataSources that are not MockDataSources are just deployed "as is" and will behave the same in all the different types of deployments.

During deployment, a unique database is created on the fly (one per deployment), named:

```
     sbx_<deploymentType>_deployment_<deploymentId>_org_1
```
where the deployment type is one of "test", "staging", or "production". The following DataSources are created in the deployment database during deployment, with records related to the project being deployed copied from the common database, in the case of the FileSource DataSources:

| DataSource Name | Contents | Is FileSource? |
|---|---|---|
| isc_hostedProjects | project definitions | Y |
| isc_hostedScreens | screen definitions | Y |
| isc_hostedDataSources | MockDataSource definitions | Y |
| isc_hostedSettings | project-specific settings | Y |
| isc_hostedUsers | users for deployment | N |
| isc_hostedRoles | user roles for deployment | N |
| isc_hostedSessions | tracks deployment sessions | N |
| isc_hostedSearches | saved searches | N |

Your application's deployment URL will target the current host with a path like:

```
     /<deploymentType>/reify/<deploymentName>/
```
where the deployment type is one of "app" (production), "test", or "staging", and the deployment name is one you choose during deployment, defaulting to the project name. For example, the complete URL might look like:
```
     https://server1.bigco.com/staging/reify/vendor_evaluation/
```
for a staging deployment of BigCo's "vendor evaluation" project to server1.

Future releases will support deployment to both private and public clouds, and multi-organization, allowing you to customize the middle path segment.

Note that using the "Export" option under the "Project" button, you can combine any created screen with a SmartClient SDK, and thus deploy to any platform that supports Java servlets and a database. For more details, refer to [Reify for Developers](reifyForDevelopers.md#kb-topic-reify-for-developers).

**Auditing**

Audit DataSources are automatically created during deployment for each DataSource in your deployment. You can open the [Deployment Management Console](deploymentManagement.md#kb-topic-deployment-management-console) to examine any DataSource in the deployment, view or edit users and roles, and analyze what sessions have hit the deployment, as well as what changes they've made to your DataSources.

**Custom Components**

Reify OnSite allows adding custom components to the palette, including components built on new classes and [component schema](componentSchema.md#kb-topic-component-schema). For an overview of the files required (e.g. `globalDependencies.xml`) and where to place them, see ["Adding Custom Components to Reify"](reifyCustomComponents.md#kb-topic-adding-custom-components-to-reify).

**Custom Workflow Tasks**

With Reify OnSite, custom workflow tasks and associated editors can be added to support your special project needs. See [reifyAddWorkflowTask](reifyAddWorkflowTask.md#kb-topic-reify-onsite-adding-custom-workflow-tasks) for details.

**Advanced Tasks**

Reify has various advanced tasks to be used in workflows, where [Send Email](../classes/SendEmailTask.md#class-sendemailtask) and [Send SMS](../classes/SendSMSTask.md#class-sendsmstask) are some of them. Take a look at the [reifyMessaging](reifyMessaging.md#kb-topic-reify-messaging) to know more about them.

**Default Skin for the initial project**

Any skin, standard or custom, can be configured as the default skin for Reify and it will be applied to the initial, default project created the first time each user logs in. New projects created thereafter use the currently selected skin.

Call `isc.Reify.setDefaultSkin(skinName [, skinURL])`, typically from the Runtime Customization detailed below, to set the default skin for this instance of Reify. If the default skin is a custom skin it will not show up in the Project->Skin menu automatically. See the Custom Skins section below for details on adding that selection.

When using the Runtime Customization to register the default skin, set the load timing to `afterVBCreate`.

**Custom Skins**

Custom skins that are not hosted by the Skin Editor can be registered with Reify by calling [Reify.registerSkin](#method-reifyregisterskin). The skin can then be selected from Project->Skin->Custom Skins menu. This skin registration is typically done via Runtime Customization detailed below. An optional URL can be provided if the skin is not located in the standard location (i.e. isomorphic/skins) or is served by a different server. Note that the URL must include the skin name as its last component (ex. /mySkins/MyCustomSkin).

When using the Runtime Customization to register the custom skin, set the load timing to `afterVBCreate`.

**Runtime Customization**

Reify OnSite provides a mechanism, the "isc\_reifyCustomizations" [DataSource](../classes/DataSource.md#class-datasource), whereby you can customize the project runtime environment with your own JavaScript snippets. Note that direct access to this dataSource [requies the _"superuser"_ role](../classes/DataSource.md#attr-datasourcerequiresrole).  
To add customizations, use the [DataSources tab](dataSourcesTab.md#kb-topic-datasources-tab) in the Admin or Developer Console. Select "isc\_reifyCustomizations" in the DataSource List, and then click "Add Record" at the bottom of the new section that appears to start editing a new record. The following fields should be populated:

*   Place the number 1 in the "Org Id" field, since Reify OnSite currently only supports a single organization. If in the future, full organization support is added, this field will allow different customizations to be added for each organization.
*   In the "Load Style" field, we recommend selecting "externalFile", as then the contents you enter can be the URL of a JavaScript file rather than actual JS. If you want to enter the JS directly in this table, select "inline" instead.
*   Enter the "Contents" that will be loaded, as either the URL of a JavaScript file (for "externalFile" mode), or the JS itself (for "inline" mode). When entering a URL, note that both relative (e.g. `/foo.js`) and absolute (e.g. `http://mysite.com/cool/custom.js`) URLs are supported.

**Resolving Errors**

Errors encountered by Reify OnSite, which may raise a dialog with a countdown timer reloading the page, are logged to the "isc\_hostedErrorReports" DataSource in the HSQL database `reifyNoSandbox`. Records here are detailed, containing the click stream of events leading up to the crash, as well as the stack trace. To help resolve any errors, VPN-based remote support can be purchased from Isomorphic.

**Switching Database Engines**

To switch Reify OnSite to use another database engine, such as MySQL, you can use the "Database Configuration" tab of the [Admin Console](adminConsole.md#kb-topic-admin-console) to change the default database, and then the "Import DataSources" tab to populate the required tables. You'll need to import the following DataSource definitions to populate the `reify` database::

*   isc\_hostedProjects
*   isc\_hostedScreens
*   isc\_hostedDataSources
*   isc\_hostedSettings
*   isc\_hostedUsers
*   isc\_hostedRoles
*   isc\_hostedSessions
*   isc\_hostedSearches
*   isc\_hostedDeployments
*   isc\_userSkin

**Switching Servlet Engines**

To switch to another servlet engine, such as Jetty, you just need to remove the `bin/` and `embeddedTomcat/` subdirectories from the `WEB-INF/` directory inside the zip, and then repackage it as a war with `WEB-INF/` underneath the root by running something such as:

```
     cd reifyOnSite && jar -cvf reifyOnSite.war *
```
in the directory where you originally expanded the Reify OnSite package. This will produce a standard Java war file that can be deployed to any servlet engine / application server that supports at least J2SE.

---
