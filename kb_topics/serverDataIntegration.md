# Server DataSource Integration

[← Back to API Index](../reference.md)

---

## KB Topic: Server DataSource Integration

### Description
Server Data Integration means:

*   You [install](iscInstall.md#kb-topic-installing-the-smartclient-runtime) the [SmartClient Java Server Framework](iscServer.md#kb-topic-smartclient-server-summary) into any J2SE/J2EE environment, including any existing web application
*   You [create DataSources](dataSourceDeclaration.md#kb-topic-creating-datasources) via an XML declaration, possibly on-the-fly from [existing metadata](metadataImport.md#kb-topic-metadata-import).
*   Server communication for components bound to these DataSources is handled automatically with a highly efficient, compressed protocol. You work with clean Java APIs instead of dealing with the details of XML or JSON over HTTP.
*   You can use built-in connectors for SQL, Hibernate and other common data providers without writing any code, or you can easily build your own connectors in Java.
*   Whether using the built-in connectors or custom connectors, declarations in your DataSource control a large set of server features that can make common types of business logic entirely declarative

This approach is in contrast to [Client-side Data Integration](clientDataIntegration.md#kb-topic-client-side-data-integration) in which client-side DataSources are configured to send and receive HTTP messages containing XML, JSON or other content.

**Server-side Request Processing**

Client-side [DataBoundComponents](../reference.md#interface-databoundcomponent) will send [DSRequests](../reference.md#object-dsrequest) to the SmartClient Server as background communications transparent to the user. Integrating SmartClient's DataSource layer with your data model is a matter of handling these DSRequests and sending back DSResponses, in order to fulfill the 4 basic operations of the [DataSource Protocol](dataSourceOperations.md#kb-topic-datasource-operations).

Out of the box, SmartClient is set up to route all DSRequests through a special servlet called `IDACall`.

Note that the SmartClient SDK includes detailed Javadoc reference for this servlet and all shipped SmartClient Java server classes.

Requests that go through `IDACall` have the following lifecycle:

*   The overall HTTP request is received by the IDACall servlet. SmartClient supports queuing of transactions, so each HTTP request might contain multiple DSRequests.
*   IDACall sets up an instance of `RPCManager` to manage the processing of the entire queue of transactions. For every DSRequest in the queue, this RPCManager:

*   Validates the DSRequest
*   Checks the DataSource configuration for customizations implemented via [server scripting](serverScript.md#kb-topic-server-scripting) or [DMI](dmiOverview.md#kb-topic-direct-method-invocation) - in other words, your code - and passes the request to this logic.
    
    As described later in this section, your code can perform some custom logic here: either completely fulfilling the request, or alternatively modifying the request and causing the default processing of the request to continue
    
*   Calls the DataSource's `execute` method to obtain a DSResponse.

*   Having processed all requests, the RPCManager now serializes all the DSResponses and sends them back to the browser as a single HTTP response

This basic request handling flow can be customized at a number of points:

*   If you need an overarching authentication service, this is best implemented using [servlet Filters](http://java.sun.com/products/servlet/Filters.html) to intercept unauthenticated requests before they reach the `IDACall` servlet
*   The [DataSource.serverType](../classes/DataSource.md#attr-datasourceservertype) specification within your `.ds.xml` configuration file is used to specify a standard server-side connector to service your requests.
*   General custom business logic can be added in a number of ways, both declaratively and programmatically:

*   The `<criteria>` and `<values>` properties of an [OperationBinding](../classes/OperationBinding.md#class-operationbinding) allow you to modify the dataSource request dynamically at transaction-processing time, using built-in [Velocity support](#kb-topic-velocitysupport).  
    Note this feature also allows developers to use [Transaction Chaining](transactionChaining.md#kb-topic-transaction-chaining) to dynamically set data values according to the results of earlier transactions.
*   For editing, standard [DataSourceField.validators](../classes/DataSourceField.md#attr-datasourcefieldvalidators) defined in the `.ds.xml` file will be processed on both the client and the server. In addition to the built-in validator types, entirely custom server validation logic may be implemented using ["serverCustom" type validators](../reference.md#type-validatortype).
*   For SQL DataSources, use [SQL Templating](#kb-topic-customquerying) to change, add to or even completely replace the SQL sent to the database, including calling stored procedures
*   The [DataSource.serverConstructor](../classes/DataSource.md#attr-datasourceserverconstructor) allows you to specify an explicit custom DataSource subclass to create as your DataSource instance. This must be a subclass of `BasicDataSource`.  
    When requests are recieved by the `IDACall` servlet, they will be passed to standard methods on this DataSource, which can be overridden for custom behavior.  
    Validation is performed via a call to the `validate()` method.  
    The request is processed by the `execute()`, method which can be overridden directly, or developers may override the operation-specific methods `executeFetch()`, `executeAdd()`, `executeUpdate`, or `executeRemove()` called from the standard `execute()` implementation.  
    This approach allows you to either extend one of the built-in persistence mechanisms by subclassing a shipped class such as `SQLDataSource`, or create an entirely custom implementation from scratch.  
    A custom dataSource will still take full advantage of DataSource-agnostic features of the SmartClient Server, like validation, queuing, transaction chaining, support for Velocity templating, and so on.  
    For more information see the [custom server dataSource overview](writeCustomDataSource.md#kb-topic-custom-server-datasources)
*   Use [Direct Method Invocation](dmiOverview.md#kb-topic-direct-method-invocation) to call directly into your own Java classes. An operation configured to use DMI will invoke the specified method instead of running through the standard DataSource `execute()` method directly - the DMI implementation can then use `dsRequest.execute()` to call the default behavior. This means DMIs allow you to modify the `DSRequest` before it executes, modify the `DSResponse` before it returns, or replace the default behavior with unrelated actions. Note that DMI can be applied [to all operations](../classes/DataSource.md#attr-datasourceserverobject), or to [individual operation bindings](../classes/OperationBinding.md#attr-operationbindingserverobject), and can be used in conjunction with a [custom dataSource](../classes/DataSource.md#attr-datasourceserverobject).
*   Use [server scripting](serverScript.md#kb-topic-server-scripting) to add small amounts of business logic right in your `.ds.xml` file (either [per operation](../classes/OperationBinding.md#attr-operationbindingscript), or as standard handling for [all operations](../classes/DataSource.md#attr-datasourcescript)). DMI scripts allow you to add business logic just like normal DMIs, but don't require the logic to be in a separate .java file.

  
*   If you need to use a Front Controller servlet for some other reason than authentication - for example, you are using Spring some other similar system which requires that all requests go through some particular servlet - just call `RPCManager.processRequest()` within your Spring Controller or whatever the equivalent is in the framework in use.
    
    However, note carefully that taking this approach is often a sign that the SmartClient architecture has not been correctly understood. SmartClient is architected for _client-server_ data communication, as opposed to early web MVC frameworks which do everything on the server. In particular, it is absolutely incorrect to represent every individual DataSource operation - or even every DataSource - as a separate Spring Controller because this implies different URLs for different operations. All DataSource operations should go through a single URL in order to allow [transaction queuing](../classes/RPCManager.md#class-rpcmanager) - see these *Queuing examples*.
    

For more information on the DMI subsystem, see the [DMI overview](dmiOverview.md#kb-topic-direct-method-invocation), [DMI class](../classes/DMI.md#class-dmi) and the *DMI example* in the Feature Explorer.

Note that, as you continue to integrate your prototype with your backend, you can use a mixture of DataSources that have been fully integrated with your backend and DataSources that are running in "client-only" mode (see [clientOnlyDataSources](clientOnlyDataSources.md#kb-topic-client-only-datasources)).

**Important methods for handling DataSource requests**

The basic flow of logic for handling DataSource requests is:

| 1. Determine operation type (Fetch, Add, Update, Remove) for a single request. Not necessary if you follow the recommendations for [writing a custom DataSource](writeCustomDataSource.md#kb-topic-custom-server-datasources) and provide your implementation via executeFetch(), executeAdd(), et al. | dsRequest.getOperationType() |
|---|---|
| 2. Get inbound values (Add, Update) and/or criteria (Fetch, Update, Remove) for this request. | dsRequest.getFieldValue()dsRequest.getValues()dsRequest.getCriteria() |
| 3. Business logic, validation, calls to data and service tiers... anything you can code. | execute custom logic |
| 4. Set status and data for the response. | dsResponse.setStatus()dsResponse.setData() |

For more information, see the [RPCManager documentation](../classes/RPCManager.md#class-rpcmanager), and the *Custom ORM DataSource example*.

### Related

- [DSDataFormat](../reference.md#type-dsdataformat)
- [DSServerType](../reference_2.md#type-dsservertype)
- [DataSource.dataFormat](../classes/DataSource.md#attr-datasourcedataformat)
- [DataSource.dataProtocol](../classes/DataSource.md#attr-datasourcedataprotocol)
- [DataSource.requestProperties](../classes/DataSource.md#attr-datasourcerequestproperties)
- [DataSource.serverType](../classes/DataSource.md#attr-datasourceservertype)
- [DataSource.tableName](../classes/DataSource.md#attr-datasourcetablename)
- [DataSource.quoteTableName](../classes/DataSource.md#attr-datasourcequotetablename)
- [DataSource.dbName](../classes/DataSource.md#attr-datasourcedbname)
- [DataSource.configBean](../classes/DataSource.md#attr-datasourceconfigbean)
- [DataSource.forceSort](../classes/DataSource.md#attr-datasourceforcesort)
- [OperationBinding.forceSort](../classes/OperationBinding.md#attr-operationbindingforcesort)
- [DataSource.defaultSortField](../classes/DataSource.md#attr-datasourcedefaultsortfield)
- [DataSource.defaultTextMatchStyle](../classes/DataSource.md#attr-datasourcedefaulttextmatchstyle)
- [DataSource.defaultBooleanStorageStrategy](../classes/DataSource.md#attr-datasourcedefaultbooleanstoragestrategy)
- [DataSource.useAnsiJoins](../classes/DataSource.md#attr-datasourceuseansijoins)
- [DataSource.audit](../classes/DataSource.md#attr-datasourceaudit)
- [DataSource.serverObject](../classes/DataSource.md#attr-datasourceserverobject)
- [OperationBinding.requestProperties](../classes/OperationBinding.md#attr-operationbindingrequestproperties)
- [RestDataSource.dataProtocol](../classes/RestDataSource.md#attr-restdatasourcedataprotocol)

---
