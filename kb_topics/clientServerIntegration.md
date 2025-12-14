# Client-Server Integration

[← Back to API Index](../reference.md)

---

## KB Topic: Client-Server Integration

### Description
Like client-server desktop applications, SmartClient browser-based applications interact with remote data and services via background communication channels. Background requests retrieve chunks of data rather than new HTML pages, and update your visual components in place rather than rebuilding the entire user interface.

**DataSources**

First you must create [DataSources](../classes/DataSource.md#class-datasource) that describe the objects from your object model that will be loaded or manipulated within your application. All of SmartClient's most powerful functionality builds on the concept of a DataSource, and because of SmartClient's databinding framework (see [DataBoundComponent](../reference.md#interface-databoundcomponent)), it's as easy to create a DataSource that can configure an unlimited number of components as it is to configure a single component.

For background information on how to create DataSources, [bind](../reference.md#interface-databoundcomponent) components to DataSources and initiate [DSRequest](../reference.md#object-dsrequest)s, please see the _Data Binding_ chapter of the _SmartClient Quickstart Guide_.

**Data Integration**

DataSources provide a data-provider agnostic API to SmartClient Visual Components that allow them to perform the 4 CRUD operations (**C**reate, **R**etrieve, **U**pdate, **D**elete). By "agnostic" we mean that the implementation details - the nuts and bolts of how a given DataSource actually retrieves or updates data - are unknown to bound SmartClient components. One effect of this is that DataSources are "pluggable": they can be replaced without affecting the User Interface.

When a visual component, or your own custom code, performs a CRUD operation on a DataSource, the DataSource creates a [DSRequest](../reference.md#object-dsrequest) (DataSource Request) representing the operation. "Data Integration" is the process of fulfilling that DSRequest by creating a corresponding [DSResponse](../classes/DSResponse.md#class-dsresponse) (DataSource Response), by using a variety of possible approaches to connect to the ultimate data provider.

There are two main approaches to integrating DataSources with your server technology:

*   [Server-side integration](serverDataIntegration.md#kb-topic-server-datasource-integration): DataSource requests from the browser arrive as Java Objects on the server. You deliver responses to the browser by returning Java Objects. The various server-side integration possibilities are discussed later in this article.
*   [Client-side integration](clientDataIntegration.md#kb-topic-client-side-data-integration): DataSource requests arrive as simple HTTP requests which your server code receives directly (in Java, you use the Servlet API or .jsps to handle the requests). Responses are sent as XML or JSON which you directly generate.

The possible approaches are summarized in the diagram below. Paths 2, 3 and 4 are client-side integration approaches, and path 1 includes all server-side integration approaches.

![](skin/ClientServerIntegration.png)

SmartClient supports, out of the box, codeless connectivity to various kinds of common data providers, including SQL and Hibernate. SmartClient also provides functionality and tools for accelerated integration with broad categories of data providers, such as Java Object-based persistence mechanisms (JPA, EJB, MyBatis, in-house written systems), and REST and WSDL web services in XML or JSON formats. Ultimately, a DataSource can be connected to anything that is accessible via HTTP or HTTPS, and also to in-browser persistence engines such as [Google Gears](http://gears.google.com).

**Choosing a Data Integration Approach**

This section aims to help you decide which of the many possible data integration approaches is best for your particular circumstances. The recommendations given here will guide you to the approach that involves the least effort.

![](skin/dataIntegrationFlowchart.png)

*   If you have a Java server:

*   If your ultimate storage is a SQL database:

*   Use the SQLDataSource unless you have a very large amount of pre-existing JPA or Hibernate code - small amounts of business logic can be easily migrated. Be sure to read the overview of [SQLDataSource vs JPA/Hibernate](sqlVsJPA.md#kb-topic-sql-datasource-vs-jpa-ejb-mybatis-and-other-technologies) in order to understand the large benefits the SQLDataSource provides
*   Derive DataSource definitions from existing tables or Hibernate mappings using the [autoDeriveSchema](../classes/DataSource.md#attr-datasourceautoderiveschema) feature, or from Java Beans via the [schemaBean](../classes/DataSource.md#attr-datasourceschemabean) feature. Or, use the [Admin Console](adminConsole.md#kb-topic-admin-console) to generate tables from DataSource definitions you create by hand

*   If your ultimate storage is not a SQL database:

*   If your persistence is based on Java Beans, use the [schemaBean](../classes/DataSource.md#attr-datasourceschemabean) feature to derive DataSource definitions from any Java bean
*   write a [custom DataSource](writeCustomDataSource.md#kb-topic-custom-server-datasources) that provides the CRUD operations you want to support.

*   Whether or not your storage is SQL, add business logic either declaratively in the DataSource definition, via [DMI](dmiOverview.md#kb-topic-direct-method-invocation), or any combination of the two:
    *   The `<criteria>` and `<values>` properties of an [OperationBinding](../classes/OperationBinding.md#class-operationbinding) allow you to dynamically set data values at transaction-processing time, using built-in [Velocity support](velocitySupport.md#kb-topic-velocity-context-variables)
    *   Override the `validate()` method of the DataSource to provide extra custom validations - just call `super` to obtain the list of errors derived from SmartClient validations, then add to that list as required with your own custom code
    *   Override the `execute()` method of the DataSource to add extra processing either before or after the SmartClient processing
    *   Use [Transaction Chaining](transactionChaining.md#kb-topic-transaction-chaining) to dynamically set data values according to the results of earlier transactions
    *   For SQL DataSources, use [SQL Templating](customQuerying.md#kb-topic-custom-querying-overview) to change, add to or even completely replace the SQL sent to the database, and to implement special query requirements
    *   For JPA DataSources, use [custom JQL queries](../classes/OperationBinding.md#attr-operationbindingcustomjql) to implement special query requirements
    *   For Hibernate DataSources, use [custom HQL queries](../classes/OperationBinding.md#attr-operationbindingcustomhql) to implement special query requirementsRead more about the server-side request processing flow and how to customize it in [the server integration overview](serverDataIntegration.md#kb-topic-server-datasource-integration).

*   If you do not have a Java server:

*   If you are not obliged to use a pre-existing network protocol, use the [RestDataSource](../classes/RestDataSource.md#class-restdatasource)
*   Otherwise, use [client-side data integration](clientDataIntegration.md#kb-topic-client-side-data-integration) features to create a custom client-side DataSource that adapts the DataSource protocol to your existing services

  
**RPCs: Unstructured Server Communication**

SmartClient also supports "unstructured" client-server operations. These [RPCRequest](../reference.md#object-rpcrequest)s (Remote Procedure Call Requests) are a low-level, very flexible mechanism for custom client-server communications. In an nutshell, RPCRequests:

*   may contain arbitrary data
*   are always initiated by custom code (a call to [RPCManager.send](../classes/RPCManager.md#classmethod-rpcmanagersend)), and have their responses handled by custom code (the callback passed to `send()`)

RPCRequests are relatively rare. Most client-server communications are better done in a structured fashion using a [DSRequest](../reference.md#object-dsrequest) (DataSource Request). Note that _any_ RPCRequest can alternatively be framed as a [DataSource fetch](../classes/DataSource.md#method-datasourcefetchdata); depending on the circumstances, this may be more convenient.

See the [RPCManager](../classes/RPCManager.md#class-rpcmanager) documentation for further information on RPCRequests.

---
