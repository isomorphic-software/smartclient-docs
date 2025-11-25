# Transparent Multi-Tenancy

[← Back to API Index](../main.md)

---

## KB Topic: Transparent Multi-Tenancy

### Description
A multi-tenant application is one where multiple customers experience the same application but with their data segregated - the different customers are not aware of each other.

SmartClient provides a "transparent" multi-tenant system, in which a SmartClient application can be quickly converted to support multi-tenancy, with only a handful of very simple changes required.

In short, you designate a set of DataSources as multi-tenant, and those DataSources are then available to you in tenant-specific forms, which can store data in different databases, automatically.

Specifically:

1.  database configurations become a template where _tenantId_ can appear in the settings
    
    You can use `$tenantId` in your DB settings so that you can put different tenants in different schemas or even entirely different DB hosts.
    
    There are also APIs for providing entirely different database settings on a per-tenant basis, or for specific tenants that are special.
    
2.  when loading DataSources into the browser, you pass a _tenantId_ (to DataSourceLoader, or in JSP tags)
    
    This means that tenant-specific DataSources are returned, with a naming convention that defaults to `mt__tenantId___originalDataSourceID_`.
    
    However, for client-side logic, the DataSources are still available under the original name. So, your ListGrid that is bound to the "orders" DataSource still works as expected, and code such as `DataSource.get("orders").fetchData(...)` also works, unchanged.
    
3.  for server-side logic, you just tell us the authenticated _tenantId_, and server-side APIs transparently work without code changes
    
    You provide the authenticated _tenantId_ to the server-side RPCManager object via the `setTenantId()` API. From then on, if you ask the RPCManager for a DataSource (`getDataSource()` API), you get tenant-specific DataSources.
    
    Likewise, if you create a `new DSRequest(...)` and pass the RPCManager into the constructor, the operation is scoped to the current tenant.
    

---

Taken together, these features mean that a typical SmartClient app can be converted to multi-tenancy by just:

1.  moving multi-tenant DataSources to the designated directory, by default `$webRoot/shared/ds`
2.  adding the _tenantId_ to the DataSourceLoader `<script>` tag in your bootstrap .html file
3.  securely providing the authenticated _tenantId_ to SmartClient: a call to `RPCManager.setTenantId()`, or setting the servlet attribute `isc_tenantId`
4.  adding `$tenantId` in your database config (and of course provisioning the databases!)

All the rest is handled for you, by SmartClient.

## SmartClient multi-tenancy

[DataSources](../classes/DataSource.md#class-datasource) in SmartClient support the Bridge model and Silo model for multi-tenancy. as described in the section below titled, "Multi-tenancy models."
#### Multi-tenant DataSource loading
By default multi-tenant DataSources in SmartClient are named `mt_`<tenantId>`_`<baseId>``, where `baseId` is the filename prefix of the XML DS definition file (e.g. `supplyItem` for `supplyItem.ds.xml`), but when loaded by the client an alias is automatically created so that it's accessible simply as `baseId` via [DataSource.get](../classes/DataSource.md#classmethod-datasourceget). The server looks for the definitions under the `tenants` subdirectory of each of your `project.datasources` paths, so if that property is just the directory `$webRoot/shared/ds`, for example, then we'll look in `$webRoot/shared/ds/tenants`.

When loading a DataSource via the [DataSourceLoader](server/javadoc/com/isomorphic/servlet/DataSourceLoader.html) servlet, you should supply the baseId(s) of any multi-tenant DataSources. If a `tenantId` parameter is included in the request, and is authorized, the multi-tenant directories are searched first, falling back to the normal DataSource filesystem location(s) if the DS isn't found. Conversely, if no `tenantId` parameter is included, the server will search the normal DS location(s) first, and then fall back to the multi-tenant directories (assuming authorization is present).

You can designate specific multi-tenant DataSources as "test" DataSources that should be loaded from the normal DS filesystem location(s) by declaring them in the config property `tenant.testDataSources`, and you can limit the allowed tenants by listing them in the config property `mt.tenants`.

**Note:** See the server.properties table at the end of this topic for how to customize the attribute name and other multi-tenant configuration.

#### Converting app to use multi-tenancy
To convert an existing SmartClient app to use multi-tenancy you just need to make a few changes outlined as follows. There's no need to rewrite the client app since an alias is created for the multi-tenant DataSource under its "base" ID.
#### Define a database template in your [server.properties](server_properties.md#kb-topic-serverproperties-file) file
When encountering a new tenant for the first time, the SmartClient server will automatically add a database definition for the tenant to the global config, using the database template. The template consists of a number of separate config properties that are each Velocity templates, so they can reference `tenandId` and standard Velocity variables, but also existing server.properties variables.

For example, the template used by the multi-tenant sample in the SDK is:

```
 tenant.dbTemplate.driver: $sql.HSQLDB.driver
 tenant.dbTemplate.driver.databaseName: mt_\$tenantId
 tenant.dbTemplate.driver.url: jdbc:hsqldb:file:$sql.HSQLDB.database.baseDir/mt_\$tenantId
 tenant.dbTemplate.database.type: $sql.HSQLDB.database.type
 tenant.dbTemplate.interface.type: $sql.HSQLDB.interface.type
 tenant.dbTemplate.driver.user: SA
 tenant.dbTemplate.driver.password:
```
Note that references to Velocity variables must be escaped by putting a backslash before the `$` symbol; otherwise it will be interpreted as a reference to another config property.
#### Add an authorization mechanism
In a multi-tenant system, one tenant's data should not be accessible by other tenants, so you will need to add a means of authenticating the current tenant. There are several ways to do this securely in a production system. We support two approaches:

*   **By Servlet Request.** Set an attribute on the servlet request via a web.xml filter or other server code.
*   **By RPCManager.** Call [RPCManager.setTenantId()](server/javadoc/com/isomorphic/rpc/RPCManager.html#setTenantId) from a user override of [IDACall.prepareRPCTransaction()](server/javadoc/com/isomorphic/servlet/IDACall.html#prepareRPCTransaction)

In the first approach, your filter will need to intercept servlet traffic to the IDACall and DataSourceLoader servlets, adding authorization by setting the `isc_tenantId` attribute on the servlet request. For proper security, your solution should avoid just checking for certain query params, at least if their values can be easily guessed, since that would allow any client to gain access.

Under this approach, when loading DataSources with a `<isomorphic:loadDS>` tag, there's no need to set the `tenantId` attribute as it's assumed to be whatever your servlet filter authorizes, though you can set the attribute to `"none"` to avoid unintentionally picking up a multi-tenant DS if you have one by the same name that's both multi-tenant and a normal DataSource.

As an alternate approach, you can subclass the [IDACall](server/javadoc/com/isomorphic/servlet/IDACall.html) servlet, and override [IDACall.prepareRPCTransaction()](server/javadoc/com/isomorphic/servlet/IDACall.html#prepareRPCTransaction) like so:

```
 public void prepareRPCTransaction (RPCManager rpc, RequestContext context) {
     String tenantId = null;
     // ... code here that analyzes context and sets (authorizes) tenantid ...
     rpc.setTenantId(tenantId);
 }
```
which also requires setting [RPCManager.actionURL](../classes/RPCManager.md#classattr-rpcmanageractionurl) to "\[ISOMORPHIC\]/AuthedIDACall", assuming your subclass is named `AuthedIDACall`.

Under this approach, you can load the DataSource either by providing a servlet filter to auth DataSourceLoader, or by launching your app with a JSP so that the JSP sets the authorized tenant into the `tenantId` attribute of the `<isomorphic:loadDS>` tag.

#### Multi-tenant demo app
The Order Management App has been included in the SmartClient SDK as a demo of multi-tenancy. A few shortcuts have been taken adding multi-tenancy to this app, leveraging the fact that we are not worried about a client gaining unauthorized access to the demo tenant data:

*   To enable tenant authorization for the `<isomorphic:loadDS>` JSP tag, we've just added the built-in [ParamMapperFilter](server/javadoc/com/isomorphic/servlet/ParamMapperFilter.html) filter to the SDK's web.xml to apply the `isc_tenantId` servlet request parameter to the `isc_tenantId` servlet request attribute.
*   To support multi-tenant IDACall requests, we've added the config property `tenant.testOnlyURLParam` to [server.properties](server_properties.md#kb-topic-serverproperties-file). This causes any `isc_tenantId` query param in the page URL to be sent to the server as a request parameter for IDACall requests, and ultimately set into the `isc_tenantId` servlet request attribute, authorizing the tenant

The end result is that for the demo, you can choose (authorize) one of the two supported tenants, "biginc" and "worldship," by simply setting the tenant's ID as the value of the `isc_tenantId` query param in the demo URL.

So, for example, you can hit

[/examples/multi\_tenant/orderManagementJS.jsp?isc\_tenantId=biginc](/examples/multi_tenant/orderManagementJS.jsp?isc_tenantId=biginc)

to use the app as tenant "biginc", and

[/examples/multi\_tenant/orderManagementJS.jsp?isc\_tenantId=worldship](/examples/multi_tenant/orderManagementJS.jsp?isc_tenantId=worldship)

to use it as "worldship." Obviously, having the tenant ID query param on the client authorize access is only suitable for a demo, and not a real production setup.

#### Custom configuration
Much of SmartClient's multi-tenant behavior can be customized via server.properties configuration:

| Property Name | Default value | Description |
|---|---|---|
| datasources.poolTenantDataSources | true | Whether to pool multi-tenant DataSources |
| mt.tenants | empty list | If defined, limits tenants to those listed. Other tenants will be treated as unauthorized even if the normal auth process has been followed. |
| tenant.datasources | list of directories formed from project.datasources by adding the subdirectory /tenants to each directory entry | List of directories in which to look for the multi-tenant DS XML definition files (files of the form `<baseId>`.ds.xml). |
| tenant.datasources.nameTemplate | mt_${tenantId}_$baseId | The multi-tenant name for the DataSource with the base DS ID baseId and tenant tenantId. This property is used by the DataSourceLoader servlet to generate a multi-tenant DataSource ID |
| tenant.datasources.namingPattern | mt_([A-Za-z0-9]+)_([A-Za-z0-9_$]+) | Pattern used by the Multi-tenant Dynamic DataSource Generator to recognize the name of a valid multi-tenant DataSource. The first regex group will be assumed to be the tenant ID and the second to be the base DS ID. |
| tenant.dbNameTemplate | mt_$tenantId | Database name for tenant tenantId |
| tenant.servletReqAttribute | isc_tenantId | Attribute to look for on the servlet request that holds the authorized tenant ID. Note that currently, the URL query param name read by the client framework and sent to the server as the request param when tenant.testOnlyURLParam is true is hardcoded to isc_tenantId, and is thus unaffected by this config setting. |
| tenant.testDataSources | empty list | List of DataSource base IDs that should be picked up from the normal DS filesystem location(s) (typically defined by project.datasources) instead of from the multi-tenant directories defined by tenant.datasources. |
| tenant.testOnlyURLParam | false | If true, when the client URL query parameter isc_tenantId is present and forwarded to the server as a servlet request parameter, it will be set into the servlet request attribute defined by tenant.servletReqAttribute, thus authorizing the tenant specified on the client. This is insecure, and so for testing or demo purposes only. |

## Multi-tenancy models

Multi-tenancy refers to the ability of a single database system to serve multiple tenants, where each tenant represents a distinct entity, such as a customer, user, or organization. These tenants share the same underlying database infrastructure, but their data is logically isolated and segregated to ensure privacy, security, and performance.

For consistency, we define the following terms before continuing:

*   **Database Process:** means a separate OS-level database process - what results when you run the mariaDB binary, for example
*   **Database Server:** means a distinct OS install that is dedicated to one database process, with no other database processes running on that OS. Does not necessarily mean separate physical hardware. Does not necessarily mean that the database server is running only a database process and nothing else (there could also be an application server, for example)
*   **Database (without other qualifiers):** a container for tables, views, etc, where there might be many "databases" within a given database process . This is what you get when you run "create database" in MariaDB, for example. Sometimes also called a "schema" but we won't use that term, because in SmartClient we have Component Schema et al and a set of DataSource fields is also commonly referred to as a "schema".

Given these terms, we can describe three different approaches to multi-tenancy.
#### Pool Model
In the pool model, tenants share and their data coexists within a single database and database process. This is cost efficient, as resources are shared among multiple tenants, and easily scalable to provision for a larger or smaller number of tenants. it's also easily managed, as only a single database process is required.

However, sharing resources with other tenants can raise security risks if not properly managed, and there can be performance issues from resource contention among multiple tenants.

#### Silo Model
In the silo model, each tenant's data is stored within a dedicated database process, completely isolated from other tenants. In this model, isolating resources for each tenant reduces the risk of security vulnerabilities. Moreover, tenants have more control over their individual resource allocations and configurations. Resource contention between the separate database processes of different tenants may be eliminated, as there's no requirement that the separate processes even be on the same physical hardware.

However, these advantages come with higher costs due to maintaining per-tenant resources. Also, managing the separate database processes or servers can require more effort, and more expertise if different database server products are used. If the separate database processes must run on a single machine, scalability may be an issue as each process may require significant resources.

#### Bridge Model
The bridge model is a compromise in which data for separate tenants is stored in separate databases within the same database process. This offers better cross-tenant data security than the pool model, while not consuming as many machine resources as having separate database processes per tenant. It can be more easily scaled to a larger number of tenants than a silo implementation, but the separate tenant databases may make management more challenging than a pool implementation.

---
