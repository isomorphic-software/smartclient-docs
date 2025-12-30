# Operations Overview

[← Back to API Index](../reference.md)

---

## KB Topic: Operations Overview

### Description
SmartClient Operations are dynamic, transparent communications made from the client-side SmartClient system running in the browser, to the server-side SmartClient system running in a servlet engine, or to other non-SmartClient servers available via HTTP. Operations are used to load new data or new behavior into a running SmartClient application. Operations are also used to save data entered by users, and in general, to get the result of any process which must be run on the server for security reasons.  
  
**RPC Operations**  
  
RPC Operations are low-level communications that send and retrieve arbitrary data. RPC Operations are supported by the [RPCManager](../classes/RPCManager.md#class-rpcmanager) class, which when used with the SmartClient server, provides Java to JavaScript [2-way translation](../classes/RPCRequest.md#attr-rpcrequestdata) of basic data structures. The RPCManager also provides a mechanism for client-side code to be invoked when an operation completes (called a "callback"). RPC Operations are intended for unstructured data; data that is ultimately destined for display in SmartClient components will generally come from DataSource operations.  
  
**DataSource Operations and DataBound Components**  
  
A [DataSource Operation](dataSourceOperations.md#kb-topic-datasource-operations) is an operation that acts on a DataSource, performing one of the basic actions that makes sense on a set of similar records: "fetch", "add", "update" or "remove". Unlike RPC operations, DataSource operations have specific request data and response data, for example, in the "fetch" DataSource operation, the request data is expected to be search criteria, and the response data is expected to be a list of matching DataSource records. Although DataSource operations can be invoked manually from the client, they are generally automatically invoked by DataBound components.  
  
DataBound Components are components that understand DataSources. Databound components configured with a DataSource are able to offer complete user interactions without further configuration (extensive customization is also supported).  
  
For example, given a DataSource, the ListGrid component supports a sophisticated inline editing interaction, complete with automatically chosen editors like date pickers for dates, type-aware validation, saving, and error reporting.  
  
A DataBound component supporting an interaction such as inline editing will automatically submit DataSource operations to the server at appropriate times.  
  
**DataSource Operation Integration**  
  
Integrating DataSource operations with an existing system is best approached by implementing the the 4 basic DataSource operations in terms of your existing object model or data store. With these 4 operations implemented, the entire range of user interactions supported by SmartClient [databinding-capable components](../reference.md#interface-databoundcomponent) becomes applicable to your server. At that point authentication, authorization and other business rules can be layered on top.  
  
**Built-in SQL Connectivity**  
  
The SmartClient Server comes with a built-in [SQLDataSource](sqlDataSource.md#kb-topic-sql-datasources) which can be used without any server-side code needing to be written. In contrast, any operation which uses custom server-side code is called a "Custom Operation".  
  
Generally it makes sense to prototype an application using Built-in DataSource Operations, then on the backend, create Custom DataSource Operations to retrieve data from the data store you will use in production (though don't rule out using the SQL DataSource in production - see [this discussion](sqlVsJPA.md#kb-topic-sql-datasource-vs-jpa-ejb-ibatis-and-other-technologies) of the advantages of doing so}. As you switch from using Built-in DataSources to Custom Operations, no client-side code changes will be required, because the client cares only about the DataSource definition, not the data store which the data is ultimately retrieved from.  
  
**Data Managers: ResultSet and ResultTree**  
  
Data Managers manage datasets retrieved from DataSources. Data Managers are automatically created by DataBound components, but can be created directly when more control is needed.  
  
Data Managers provide load-on-demand for datasets too large to be loaded on the client, automatically invoking DataSource operations as necessary to retrieve data as it is requested, and optionally fetching ahead to anticipate further requests. Data Managers will automatically perform actions locally when it is possible, for example, a sort action can be performed locally with a complete cache. Data Managers also automatically manage the consistency of the client-side cache, observing update operations performed against DataSources and integrating updated rows automatically.

### Related

- [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror)
- [RPCManager.runDefaultErrorHandling](../classes/RPCManager.md#classmethod-rpcmanagerrundefaulterrorhandling)
- [DataSource.fetchData](../classes/DataSource.md#method-datasourcefetchdata)
- [DataSource.filterData](../classes/DataSource.md#method-datasourcefilterdata)
- [DataSource.exportData](../classes/DataSource.md#method-datasourceexportdata)
- [DataSource.addData](../classes/DataSource.md#method-datasourceadddata)
- [DataSource.updateData](../classes/DataSource.md#method-datasourceupdatedata)
- [DataSource.removeData](../classes/DataSource.md#method-datasourceremovedata)
- [DataSource.validateData](../classes/DataSource.md#method-datasourcevalidatedata)
- [DataSource.performCustomOperation](../classes/DataSource.md#method-datasourceperformcustomoperation)
- [DataBoundComponent.fetchOperation](../classes/DataBoundComponent.md#attr-databoundcomponentfetchoperation)
- [DataBoundComponent.updateOperation](../classes/DataBoundComponent.md#attr-databoundcomponentupdateoperation)
- [DataBoundComponent.addOperation](../classes/DataBoundComponent.md#attr-databoundcomponentaddoperation)
- [DataBoundComponent.removeOperation](../classes/DataBoundComponent.md#attr-databoundcomponentremoveoperation)
- [DataBoundComponent.exportOperation](../classes/DataBoundComponent.md#attr-databoundcomponentexportoperation)
- [DSRequest.operationId](../classes/DSRequest.md#attr-dsrequestoperationid)
- [ValuesManager.addOperation](../classes/ValuesManager.md#attr-valuesmanageraddoperation)
- [ValuesManager.updateOperation](../classes/ValuesManager.md#attr-valuesmanagerupdateoperation)
- [ValuesManager.removeOperation](../classes/ValuesManager.md#attr-valuesmanagerremoveoperation)
- [ValuesManager.fetchOperation](../classes/ValuesManager.md#attr-valuesmanagerfetchoperation)

### See Also

- [RPCManager](../classes/RPCManager.md#class-rpcmanager)
- [DataBoundComponent](../reference.md#interface-databoundcomponent)
- [dataSourceOperations](dataSourceOperations.md#kb-topic-datasource-operations)
- [clientServerIntegration](clientServerIntegration.md#kb-topic-client-server-integration)
- [DataSource.fetchData](../classes/DataSource.md#method-datasourcefetchdata)
- [ResultSet](../classes/ResultSet.md#class-resultset)
- [ResultTree](../classes/ResultTree.md#class-resulttree)

---
