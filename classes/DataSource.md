# DataSource Documentation

[← Back to API Index](../reference.md)

---

## Class: DataSource

### Description
A DataSource is data-provider-independent description of a set of objects that will be loaded, edited and saved within the user interface of your application.

Each DataSource consists of a list of [fields](#attr-datasourcefields) that make up a DataSource `record`, along with [field types](DataSourceField.md#attr-datasourcefieldtype), [validation rules](DataSourceField.md#attr-datasourcefieldvalidators), [relationships](DataSourceField.md#attr-datasourcefieldforeignkey) to other DataSources, and other metadata.

The abstract object description provided by a DataSource is easily mapped to a variety of backend object models and storage schemes. The following table shows analogous terminology across systems.

| Isomorphic SmartClient | Relational Database | Enterprise Java Beans (EJB) | Entity/Relationship Modeling | OO/UML | XML Schema/WSDL | LDAP |
|---|---|---|---|---|---|---|
| DataSource | Table | EJB class | Entity | Class | Element Schema (ComplexType) | Objectclass |
| Record | Row | EJB instance | Entity instance | Class instance/Object | Element instance (ComplexType) | Entry |
| Field | Column | Property | Attribute | Property/Attribute | Attribute or Element (SimpleType) | Attribute |

DataSources can be [declared](../kb_topics/dataSourceDeclaration.md#kb-topic-creating-datasources) in either JavaScript or XML format, and can also be [imported](../kb_topics/metadataImport.md#kb-topic-metadata-import) from existing metadata formats, including XML Schema.

_Data Binding_ is the process by which [Data Binding-capable UI components](../reference.md#interface-databoundcomponent) can automatically configure themselves for viewing, editing and saving data described by DataSources. DataBinding is covered in the *QuickStart Guide*, Chapter 6, _Data Binding_.

[Data Integration](../kb_topics/clientServerIntegration.md#kb-topic-client-server-integration) is the process by which a DataSource can be connected to server systems such as SQL DataBases, Java Object models, WSDL web services and other data providers. Data Integration comes in two variants: client-side and server-side. [Server-side integration](../kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration) uses the SmartClient Java-based server to connect to data represented by Java Objects or JDBC-accessible databases. [Client-side integration](../kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration) connects SmartClient DataSources to XML, JSON or other formats accessible via HTTP.

DataSources have a concept of [4 core operations](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) ("fetch", "add", "update" and "remove") that can be performed on the set of objects represented by a DataSource. Once a DataSource has been integrated with your data store, databinding-capable UI components can leverage the 4 core DataSource operations to provide many complete user interactions without the need to configure how each individual component loads and saves data.

These interactions include [grid views](ListGrid_1.md#class-listgrid), [tree views](TreeGrid.md#class-treegrid), [detail views](DetailViewer.md#class-detailviewer), [form](DynamicForm.md#class-dynamicform)-based [editing](DynamicForm.md#method-dynamicformeditrecord) and [saving](DynamicForm.md#method-dynamicformsavedata), grid-based [editing](ListGrid_1.md#attr-listgridcanedit) and [saving](ListGrid_1.md#attr-listgridsavebycell), and custom interactions provided by *patternReuse example* custom databinding-capable components.

### See Also

- [DataBoundComponent](../reference.md#interface-databoundcomponent)
- [dataSourceDeclaration](../kb_topics/dataSourceDeclaration.md#kb-topic-creating-datasources)

---
## ClassAttr: DataSource.requiredCriterionMessage

### Description
A message returned by a `DataSource` when an operation requires criteria, but none was provided.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: DataSource.deepCloneNonFieldValuesOnEdit

### Description
Provides the global default setting for deep or shallow cloning of non-field attributes of value objects prior to edit. See [DataSource.deepCloneNonFieldValuesOnEdit](#attr-datasourcedeepclonenonfieldvaluesonedit) for details of what this means.

The default setting of null is the same as false; with this default in place, `deepCloneNonFieldValuesOnEdit` must be set explicitly set at dataSource or component level if you require deep cloning.

### See Also

- [DataSource.deepCloneNonFieldValuesOnEdit](#attr-datasourcedeepclonenonfieldvaluesonedit)
- [DataBoundComponent.deepCloneNonFieldValuesOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepclonenonfieldvaluesonedit)

**Flags**: IRWA

---
## ClassAttr: DataSource.deepCloneOnEdit

### Description
Provides the global default setting for deep or shallow cloning of objects prior to edit. See [DataSource.deepCloneOnEdit](#attr-datasourcedeepcloneonedit) for details of what this means.

The default setting of null is the same as false; with this default in place, `deepCloneOnEdit` must be set explicitly set at dataSource, component or field level if you require deep cloning.

### See Also

- [DataSource.deepCloneOnEdit](#attr-datasourcedeepcloneonedit)
- [DataBoundComponent.deepCloneOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepcloneonedit)
- [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit)

**Flags**: IRWA

---
## ClassAttr: DataSource.maxFileSizeExceededMessage

### Description
A message returned by a `DataSource` when an uploaded file's size exceeded [DataSourceField.maxFileSize](DataSourceField.md#attr-datasourcefieldmaxfilesize).

If this is not set, then [Validator.maxFileSizeExceeded](Validator.md#classattr-validatormaxfilesizeexceeded) value will be used.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: DataSource.requiredFileMessage

### Description
A message returned by a `DataSource` when an uploaded file was empty, but the field is [required](DataSourceField.md#attr-datasourcefieldrequired).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: DataSource.serializeTimeAsDatetime

### Description
Specifies how time field values should be serialized when being sent to the server for dataSources with dataFormat `"xml"` or `"json"`. If `false` the time field will be serialized as a logical time object in UTC, using the standard truncated XML Schema format: `"HH:MM:SS"`. If `true` the time field will be serialized as a complete dateTime object matching the value of the underlying JavaScript date object representing this time on the client.

**Flags**: IRA

---
## ClassAttr: DataSource.defaultStringInBrowser

### Description
Default value if [DataSourceField.stringInBrowser](DataSourceField.md#attr-datasourcefieldstringinbrowser) is not defined. See `stringInBrowser` docs for details.  
Note this setting should be used only if you are \*not\* using the SmartClient Server.

### See Also

- [DataSourceField.stringInBrowser](DataSourceField.md#attr-datasourcefieldstringinbrowser)

**Flags**: RW

---
## ClassAttr: DataSource.offlineMessage

### Description
A message returned by a DataSource when it is returning an empty dataset for a fetch because the browser is currently offline and there is no suitable cached offline response.

### Groups

- i18nMessages
- offlineGroup

**Flags**: IRW

---
## ClassAttr: DataSource.loaderURL

### Description
The URL where the DataSourceLoader servlet has been installed. Defaults to the [isomorphicDir](Page.md#classmethod-pagesetisomorphicdir) plus "/DataSourceLoader". Change by calling calling [DataSource.setLoaderURL](#classmethod-datasourcesetloaderurl)

**Flags**: RW

---
## Attr: DataSource.sqlUsePagingHint

### Description
If explicitly set true or left null, causes the server to use a "hint" in the SQL we generate for paged queries. If explicitly set false, forces off the use of hints. This property can be overridden per operationBinding - see [OperationBinding.sqlUsePagingHint](OperationBinding.md#attr-operationbindingsqlusepaginghint).

Note this property is only applicable to [SQL](#attr-datasourceservertype) DataSources, only when a [paging strategy](#attr-datasourcesqlpaging) of "sqlLimit" is in force, and it only has an effect for those specific database products where we employ a native hint in the generated SQL in an attempt to improve performance.

### Groups

- sqlPaging

### See Also

- [OperationBinding.sqlUsePagingHint](OperationBinding.md#attr-operationbindingsqlusepaginghint)

**Flags**: IR

---
## Attr: DataSource.autoDiscoverTree

### Description
Causes [Tree.discoverTree](Tree.md#classmethod-treediscovertree) to be called on dsResponse.data in order to automatically discover tree structures in the response data.

If autoDiscoverTree is set, discoverTree() is called after the default dsResponse.data has been derived ([recordXPath](OperationBinding.md#attr-operationbindingrecordxpath) and [valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) have been applied) and after [DataSource.transformResponse](#method-datasourcetransformresponse) has been called.

If a DataSourceField is declared with [childrenProperty:true](DataSourceField.md#attr-datasourcefieldchildrenproperty), discoverTree() will be invoked with [settings.newChildrenProperty](DiscoverTreeSettings.md#attr-discovertreesettingsnewchildrenproperty) set to the name of the field marked as the childrenField. Similarly, if the DataSource has a [DataSource.titleField](#attr-datasourcetitlefield) it will be used as the [settings.nameProperty](DiscoverTreeSettings.md#attr-discovertreesettingsnameproperty).

**Flags**: IR

---
## Attr: DataSource.resultBatchSize

### Description
Very advanced: for servers that do not support paging, and must return large numbers of XML records in one HTTP response, SmartClient breaks up the processing of the response in order to avoid the "script running slowly" dialog appearing for an end user.

If you have a relatively small number of records with a great deal of properties or subobjects on each record, and you have not set [DataSource.dropExtraFields](#attr-datasourcedropextrafields) to eliminate unused data, and you see the "script running slowly" dialog, you may need to set this number lower.

**Flags**: IRWA

---
## Attr: DataSource.beanClassName

### Description
This property has different meanings depending on the [serverType](#attr-datasourceservertype):

**For SQL DataSources (DataSources with serverType "sql")**  
If set, results from the database will be used to create one instance of the indicated Java bean per database row. Otherwise a Map is used to represent each row retrieved from SQL.

With this feature active, a DSResponse from this DataSource will contain a Collection of instances of the indicated `beanClassName`, available via DSResponse.getData(). This creates a couple of possibilities:

Add business logic for derived properties, such as computed formulas

For example, declare a DataSourceField named "revenueProjection". By default this field will call getRevenueProjection() on your bean to retrieve the value to send to the client. Your implementation of getRevenueProjection() could apply some kind of formula to other values loaded from the database.

Call business logic on retrieved beans via DMI

By adding a [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) method that calls DSRequest.execute() to retrieve a DSResponse, you have an opportunity to call business logic methods on the beans representing each row affected by the DSRequest. For example, notify a related BPEL process of changes to certain fields.

By using `beanClassName` on a specific [OperationBinding](OperationBinding.md#class-operationbinding), you can:

*   Use a bean to represent your data only when it matters; for example, avoid the overhead of using a bean for "fetch" operations, but do use a bean for "update" operations so that you can execute relevant business logic after the update completes.
*   Skip the use of beans for complex reporting queries that produce results unrelated to your persistent object model. Set beanClassName to blank ("") on a specific operationBinding to override DataSource.beanClassName for that specific operation.
*   For SQL joins that produce additional data fields, use a special, operation-specific bean that represents a join of multiple entities and contains business logic specific to that joined dataset

Note that `beanClassName` affects what numeric field types will be used for inbound DSRequest data. For fields with numeric types, the [record data](DSRequest.md#attr-dsrequestdata) in DSRequests will automatically be converted to the type of the target field, before the request is received in a [DMI](DMI.md#class-dmi). For details, see [dsRequestBeanTypes](../kb_topics/dsRequestBeanTypes.md#kb-topic-dsrequest-data-auto-converted-to-bean-types).

Note that [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) also has a built-in facility for populating a bean with the inbound [DSRequest.data](DSRequest.md#attr-dsrequestdata) - just declare the bean as a method argument.

**For generic DataSources (DataSources with serverType "generic")**  
[Reify](../kb_topics/reify.md#kb-topic-reify-overview) sets this property when it creates a generic DataSource using the Javabean Wizard. It has no built-in server-side effects.

**For Hibernate DataSources (DataSources with serverType "hibernate")**  
The name of the Java bean or POJO class that is mapped in Hibernate. This will typically be the fully-qualified class name - eg `com.foo.MyClass` - but it may be the simple class name - just `MyClass` - or it may be some other value. It all depends on how your classes have been mapped in Hibernate.

The declared Java bean will affect how its properties will be mapped to built-in numeric types, see [Hibernate Integration overview](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) for details.

Note: If you are intending to use Hibernate as a data-access layer only, you do not need to create Hibernate mappings or Java objects: SmartClient will generate everything it needs on the fly.

**For JPA DataSources (DataSources with serverType "jpa" or "jpa1")**  
The fully qualified class name of the JPA annotated entity.

**NOTE for Hibernate and JPA users:** When you use JPA, or use Hibernate as a full ORM system (ie, not just allowing SmartClient Server to drive Hibernate as a data access layer), the beans returned on the server-side are **live**. This means that if you make any changes to them, the ORM system will persist those changes. This is true even if the beans were created as part of a fetch operation.

This causes a problem in the common case where you want to use a DMI or custom DataSource implementation to apply some post-processing to the beans fetched from the persistent store. If you change the values in the beans directly, those changes will be persisted.

If you want to alter the data returned from a JPA or Hibernate persistent store as part of a fetch request just so you can alter what gets sent to the client, you can use the server-side `DSResponse`'s `getRecords()` method. This will return your bean data in "record" format - ie, as a List of Maps. You can alter these records without affecting your persistent store, and then call `setData()` on the `DSResponse`), passing the altered list of records. See the server-side Javadocs for `DSResponse` for details of these two methods.

### See Also

- [OperationBinding.beanClassName](OperationBinding.md#attr-operationbindingbeanclassname)

**Flags**: IR

---
## Attr: DataSource.auditDataSourceID

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), optionally specifies the ID of the audit DataSource. If this property is not specified, the ID of the audit DataSource will be `audit_[OriginalDSID]`

**Flags**: IR

---
## Attr: DataSource.serverConstructor

### Description
This property allows you to write and use custom DataSource subclasses on the server, by specifying either

*   the fully-qualified name of the DataSource subclass that should be instantiated server-side for this dataSource, or
*   the token "spring:" followed by a valid Spring bean ID, if you wish to instantiate your custom dataSource object using Spring dependency injection. For example, `"spring:MyDataSourceBean"`. See also [serverInit](../kb_topics/serverInit.md#kb-topic-server-framework-initialization) for special concerns with framework initialization when using Spring. It is also particularly important that you read the discussion of caching and thread-safety linked to below, as there are special considerations in this area when using Spring.
*   the token "cdi:" followed by a valid CDI bean name, if you wish to instantiate your custom dataSource object using CDI dependency injection. For example, `"cdi:MyDataSourceBean"`.

One reason you might wish to do this would be to override the validate() method to provide some arbitrary custom validation (such as complex database lookups, validation embedded in legacy applications, etc). It is also possible - though obviously a more substantial task - to override the execute() method in your custom DataSource. This is one way of creating a completely customized DataSource implementation.

**Note:** If you use this property, you are responsible for making sure that it refers to a valid server-side class that extends `com.isomorphic.datasource.BasicDataSource`, or to a Spring bean of the same description. If your implementation relies on methods or state only present in certain specialized subclasses of DataSource (for example, you want the normal behavior and features of a HibernateDataSource, but with a specialized validate() method), then you should extend the subclass rather than the base class.

NOTE: Please take note of the points made in [this discussion](../kb_topics/serverDataSourceImplementation.md#kb-topic-notes-on-server-side-datasource-implementations) of caching and thread-safety issues in server-side DataSources.

**Flags**: IR

---
## Attr: DataSource.dataFormat

### Description
Indicates the format to be used for HTTP requests and responses when fulfilling DSRequests (eg, when [DataSource.fetchData](#method-datasourcefetchdata) is called).

### Groups

- clientDataIntegration
- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.autoCacheAllData

### Description
When a DataSource is not [DataSource.cacheAllData](#attr-datasourcecachealldata):true and a fetch results in the entire dataset being retrieved, this attribute being set to true causes the DataSource to automatically switch to `cacheAllData:true` and prevent further server-trips for fetch requests.

[cacheAllData](#attr-datasourcecachealldata) is automatically enabled in either of these conditions:

*   The request has no criteria and no startRow/endRow request properties. The latter can be accomplished by disabling paging with a [dataFetchMode](DataBoundComponent.md#attr-databoundcomponentdatafetchmode) setting of "basic" or "local" or by an explicit fetchData request with those request properties excluded.
*   The request has no criteria but has startRow/endRow specified and the response received has all data available (`startRow:0` and `endRow:totalRows`).

### Groups

- clientData

**Flags**: IR

---
## Attr: DataSource.jsonSuffix

### Description
Allows you to specify an arbitrary suffix string to apply to all json format responses sent from the server to this application.

The inclusion of such a suffix ensures your code is not directly executable outside of your application, as a preventative measure against [javascript hijacking](http://www.google.com/search?q=javascript+hijacking).

Only applies to responses formatted as json objects. Does not apply to responses returned via scriptInclude type transport.

### See Also

- [OperationBinding.dataFormat](OperationBinding.md#attr-operationbindingdataformat)
- [OperationBinding.dataTransport](OperationBinding.md#attr-operationbindingdatatransport)

**Flags**: IRA

---
## Attr: DataSource.sequenceMode

### Description
For fields of [type](DataSourceField.md#attr-datasourcefieldtype) "sequence" in a dataSource of [serverType](#attr-datasourceservertype) "sql", indicates the [SequenceMode](../reference.md#type-sequencemode) to use. This property has no effect for fields or dataSources of other types.

You can set a default sequenceMode for all DataSources of a given database type by setting property "sql.{database\_type}.default.sequence.mode" in `server.properties`. You set a global default sequenceMode that applies to all database types by setting property "sql.default.sequence.mode". For example:

```
   sql.mysql.default.sequence.mode: jdbcDriver
 
```

**Flags**: IR

---
## Attr: DataSource.sqlPaging

### Description
The paging strategy to use for this DataSource. If this property is not set, the default paging strategy, specified with the [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) setting `sql.defaultPaging`, is used.

This setting can be overridden with the [OperationBinding.sqlPaging](OperationBinding.md#attr-operationbindingsqlpaging) property.

**NOTE:** Operations that involve a [customSQL](OperationBinding.md#attr-operationbindingcustomsql) clause ignore this property, because customSQL operations usually need to be treated as special cases. For these operations, the paging strategy comes from the [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) setting `sql.defaultCustomSQLPaging` or `sql.defaultCustomSQLProgressivePaging`, depending on whether or not [progressiveLoading](#attr-datasourceprogressiveloading) is in force. Note that these can always be overridden by a `sqlPaging` setting on the OperationBinding.

### See Also

- [OperationBinding.sqlPaging](OperationBinding.md#attr-operationbindingsqlpaging)

**Flags**: IRW

---
## Attr: DataSource.script

### Description
Default scriptlet to be executed on the server for each operation. If [OperationBinding.script](OperationBinding.md#attr-operationbindingscript) is specified, it will be executed for the operation binding in question instead of running this scriptlet.

Scriptlets are used similarly to DMIs configured via [DataSource.serverObject](#attr-datasourceserverobject) or [OperationBinding.serverObject](OperationBinding.md#attr-operationbindingserverobject) - they can add business logic by modifying the DSRequest before it's executed, modifying the default DSResponse, or taking other, unrelated actions.

For example:

```
    <DataSource>
       <script language="groovy">
          ... Groovy code ...
       </script>
      ... other DataSource properties
    </DataSource>
 
```

Scriptlets can be written in any language supported by the "JSR 223" standard, including Java itself. See the [DMI Script Overview](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) for rules on how to return data, add additional imports, and other settings.

The following variables are available for DMI scriptlets:

*   _requestContext_: RequestContext (from com.isomorphic.servlet)
*   _dataSource_: the current DataSource (same as DSRequest.getDataSource())
*   _dsRequest_: the current DSRequest
*   _criteria_: shortcut to DSRequest.getCriteria() (a Map)
*   _values_: shortcut to DSRequest.getValues() (a Map)
*   _oldValues_: shortcut to DSRequest.getOldValues() (a Map)
*   _log_: an instance of `com.isomorphic.log.Logger`, so your scripts can log in the same manner as regular Java code
*   _config_: an instance of `com.isomorphic.base.Config`, so your scripts have access to your `server.properties` settings
*   _sqlConnection_: **SQLDataSource only**: the current SQLConnection object. If using [automatic transactions](#attr-datasourceautojointransactions) are enabled, this SQLConnection is in the context of the current transaction
*   _rpcManager_: the current RPCManager
*   _applicationContext_: the Spring ApplicationContext (when applicable)
*   _beanFactory_: the Spring BeanFactory (when applicable)

Scriptlets also have access to a set of contextual variables related to the Servlets API, as follows:

*   _servletRequest_: the current ServletRequest
*   _session_: the current HttpSession
*   _servletResponse_: the current ServletResponse **(advanced use only)**
*   _servletContext_: the current ServletContext**(advanced use only)**

As with DMI in general, be aware that if you write scriptlets that depend upon these variables, you preclude your DataSource from being used in the widest possible variety of circumstances. For example, adding a scriptlet that relies on the `HttpSession` prevents your DataSource from being used in a command-line process.

_Note that if a dataSource configuration has both a ``<script>`` block and a specified [serverObject](OperationBinding.md#attr-operationbindingserverobject) for some operation, the script block will be executed, and the serverObject ignored._

**Flags**: IR

---
## Attr: DataSource.fileNameField

### Description
The native field name used by this DataSource on the server to represent the `fileName` for [FileSource Operations](../kb_topics/fileSource.md#kb-topic-filesource-operations) operations. Any extensions to the fileName to indicate type or format (e.g. ".ds.xml") are stored in the [fileTypeField](#attr-datasourcefiletypefield) and [fileFormatField](#attr-datasourcefileformatfield), if specified for this DataSource.

If not specified for a DataSource, the fileNameField will be inferred on the server as follows:

*   If there is a field named "fileName", "name", or "title", then that field is used.
*   Otherwise, if there is a single primary key, and it has the type "text", then that field is used.
*   Otherwise, an error is logged

### Groups

- fileSource

**Flags**: IR

---
## Attr: DataSource.autoJoinTransactions

### Description
If true, causes all operations on this DataSource to automatically start or join a transaction associated with the current HttpServletRequest. This means that multiple operations sent to the server in a [request queue](RPCManager.md#classmethod-rpcmanagerstartqueue) will be committed in a single transaction.

Note that this includes fetch operations - setting this property to true has the same effect as a transaction policy of ALL for just this DataSource's operations - see the server-side `RPCManager.setTransactionPolicy()` for details of the different TransactionPolicy settings.

If this property is explicitly false, this causes all operations on this DataSource to be committed individually - the same as a transaction policy of NONE, just for this DataSource's operations.

In either case, you can override the setting for individual operations - see [OperationBinding.autoJoinTransactions](OperationBinding.md#attr-operationbindingautojointransactions).

If this property if null or not defined, we fall back to the default setting for this type of DataSource. These are defined in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) as follows:

*   **Hibernate:** `hibernate.autoJoinTransactions`
*   **JPA/JPA2:** `jpa.autoJoinTransactions`
*   **SQL:** There is one setting per configured database connection ([dbName](#attr-datasourcedbname)). For example, the setting for the default MySQL connection is `sql.Mysql.autoJoinTransactions`

If the setting is not defined at the DataSource-type level, we use the system global default, which is defined in `server.properties` as `autoJoinTransactions`.

At the dbName and global system levels, you can set the autoJoinTransactions attribute to a valid Transaction Policy, rather than a simple true or false (although these values work too - true is the same as ALL, false is the same as NONE). For valid TransactionPolicy values and their meanings, see the server-side Javadoc for `RPCManager.setTransactionPolicy()`

Note that the configuration settings discussed here can be overridden for a particular queue of requests by setting the server-side RPCManager's transaction policy. Look in the server-side Javadoc for `RPCManager.getTransactionPolicy()`.

Transactions can also be initiated manually, separate from the RPCManager/HttpServletRequest lifecycle, useful for both multi-threaded web applications, and standalone applications that don't use a servlet container - see [standaloneDataSourceUsage](../kb_topics/standaloneDataSourceUsage.md#kb-topic-standalone-datasource-usage).

NOTE: Setting this property to true does not cause a transactional persistence mechanism to automatically appear - you have to ensure that your DataSource supports transactions. The SmartClient built-in SQL, Hibernate and JPA DataSources support transactions, but note that they do so **at the provider level**. This means that you can combine updates to, say, an Oracle database and a MySQL database in the same queue, but they will be committed in _two_ transactions - one per database. The SmartClient server will commit or rollback these two transactions as if they were one, so a failure in some Oracle update would cause all the updates to both databases to be rolled back. However, this is not a true atomic transaction; it is possible for one transaction to be committed whilst the other is not - in the case of hardware failure, for example.

NOTE: Not all the supported SQL databases are supported for transactions. Databases supported in this release are:

*   DB2
*   HSQLDB
*   Firebird
*   Informix
*   Microsoft SQL Server
*   MySQL (you must use InnoDB tables; the default MyISAM storage engine does not support transactions)
*   MariaDB
*   Oracle
*   PostgreSQL

### See Also

- [OperationBinding.autoJoinTransactions](OperationBinding.md#attr-operationbindingautojointransactions)

**Flags**: IR

---
## Attr: DataSource.auditUserFieldName

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), specifies the field name used to store the user who performed the operation. If empty string is specified as the field name, the audit DataSource will not store this field.

**Flags**: IR

---
## Attr: DataSource.operationBindings

### Description
Optional array of OperationBindings, which provide instructions to the DataSource about how each DSOperation is to be performed.

When using the SmartClient Server, OperationBindings are specified in your DataSource descriptor (.ds.xml file) and control server-side behavior such as what Java object to route DSRequest to ([OperationBinding.serverObject](OperationBinding.md#attr-operationbindingserverobject)) or customizations to SQL, JQL and HQL queries ([OperationBinding.customSQL](OperationBinding.md#attr-operationbindingcustomsql), [OperationBinding.customJQL](OperationBinding.md#attr-operationbindingcustomjql) and [OperationBinding.customHQL](OperationBinding.md#attr-operationbindingcustomhql)). See the *Java Integration samples*.

For DataSources bound to WSDL-described web services using [DataSource.serviceNamespace](#attr-datasourceservicenamespace), OperationBindings are used to bind each DataSource [operationType](OperationBinding.md#attr-operationbindingoperationtype) to an [operation](OperationBinding.md#attr-operationbindingwsoperation) of a WSDL-described [web service](WebService.md#class-webservice), so that a DataSource can both fetch and save data to a web service.

For example, this code accomplishes part of the binding to the [SalesForce partner web services](http://www.google.com/search?q=sforce+partner+wsdl)

```
 isc.DataSource.create({
    serviceNamespace : "urn:partner.soap.sforce.com",
    operationBindings : [
        { operationType:"fetch", wsOperation:"query", recordName: "sObject" },
        { operationType:"update", wsOperation:"update", recordName: "SaveResult" },
        { operationType:"add", wsOperation:"create", recordName: "SaveResult" },
        { operationType:"remove", wsOperation:"delete", recordName: "DeleteResult" }
    ],
    ...
 }); 
 
```
NOTE: additional code is required to handle authentication and other details, see the complete code in smartclientSDK/examples/databinding/SalesForce.

For DataSources that contact non-WSDL-described XML or JSON services, OperationBindings can be used to separately configure the URL, HTTP method, input and output processing for each operationType. This makes it possible to fetch JSON data from one URL for the "fetch" operationType and save to a web service for the "update" operationType, while appearing as a single integrated DataSource to a [DataBoundComponent](../reference.md#interface-databoundcomponent) such as an [editable ListGrid](ListGrid_1.md#attr-listgridcanedit).

If no operationBinding is defined for a given DataSource operation, all of the properties which are valid on the operationBinding are checked for on the DataSource itself.

This also means that for a read-only DataSource, that is, a DataSource only capable of fetch operations, operationBindings need not be specified, and instead all operationBinding properties can be set on the DataSource itself. In the *RSS Feed* sample, you can see an example of using OperationBinding properties directly on the DataSource in order to read an RSS feed.

### See Also

- [OperationBinding](OperationBinding.md#class-operationbinding)

**Flags**: IR

---
## Attr: DataSource.logSlowRemove

### Description
Allows you to specify ["remove" operation](../reference.md#type-dsoperationtype) SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category.

See [DataSource.logSlowSQL](#attr-datasourcelogslowsql) for more details.

**Flags**: IR

---
## Attr: DataSource.fileTypeField

### Description
The native field name used by this DataSource on the server to represent the `fileType` for [FileSource Operations](../kb_topics/fileSource.md#kb-topic-filesource-operations).

If the fileTypeField is not configured, then a field named "fileType" will be used, if it exists. Otherwise, the DataSource will not track fileTypes -- this may be acceptable if, for instance, you use a separate DataSource for each fileType.

The fileType is specified according to the extension that would have been used in the filesystem -- for instance, the fileType for employees.ds.xml would be "ds".

### Groups

- fileSource

**Flags**: IR

---
## Attr: DataSource.useFlatFields

### Description
Like [DataBoundComponent.useFlatFields](DataBoundComponent.md#attr-databoundcomponentuseflatfields), but applies to all DataBound components that bind to this DataSource.

### Groups

- fields

**Flags**: IR

---
## Attr: DataSource.infoField

### Description
Name of the field that has the second most pertinent piece of textual information in the record, for use when a [DataBoundComponent](../reference.md#interface-databoundcomponent) needs to show a short summary of a record.

For example, for a DataSource of employees, a "job title" field would probably be the second most pertinent text field aside from the employee's "full name".

Unlike [DataSource.titleField](#attr-datasourcetitlefield), infoField is not automatically determined in the absence of an explicit setting.

### Groups

- dsSpecialFields

**Flags**: IR

---
## Attr: DataSource.xmlNamespaces

### Description
Sets the XML namespace prefixes available for XPaths on a DataSource-wide basied. See [OperationBinding.xmlNamespaces](OperationBinding.md#attr-operationbindingxmlnamespaces) for details.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.multiInsertNonMatchingStrategy

### Description
For dataSources of [serverType](#attr-datasourceservertype) "sql" only, this property sets the multi-insert "non matching" strategy for add requests on this [dataSource](#class-datasource). Only has an effect if the [add request](#method-datasourceadddata) specifies a list of records as the data, and only if [multiInsertStrategy](#attr-datasourcemultiinsertstrategy) is set to "multipleValues" either globally or at the [DSRequest](../reference.md#object-dsrequest), [OperationBinding](OperationBinding.md#class-operationbinding), or [DataSource](#class-datasource) level. See the docs for [MultiInsertNonMatchingStrategy](../reference_2.md#type-multiinsertnonmatchingstrategy) for more information.

Note that this setting (along with the other multi-insert properties, [multiInsertStrategy](#attr-datasourcemultiinsertstrategy) and [multiInsertBatchSize](#attr-datasourcemultiinsertbatchsize)) can be overridden at the [operationBinding level](OperationBinding.md#attr-operationbindingmultiinsertnonmatchingstrategy) and the [dsRequest level](DSRequest.md#attr-dsrequestmultiinsertnonmatchingstrategy). If you wish to configure multi-insert setting globally, see the documentation for [multiInsertStrategy](#attr-datasourcemultiinsertstrategy).

### See Also

- [DataSource.multiInsertStrategy](#attr-datasourcemultiinsertstrategy)
- [DataSource.multiInsertBatchSize](#attr-datasourcemultiinsertbatchsize)

**Flags**: IRW

---
## Attr: DataSource.requires

### Description
Indicates that the specified [VelocityExpression](../reference_2.md#type-velocityexpression) must evaluate to true for a user to access this DataSource.

See also [OperationBinding.requires](OperationBinding.md#attr-operationbindingrequires).

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: DataSource.cacheData

### Description
For a [DataSource.cacheAllData](#attr-datasourcecachealldata) or client-only DataSource, a set of records to use as a dataset, specified as an Array of JavaScript Objects representing records.

See [this discussion](../kb_topics/clientOnlyDataSources.md#kb-topic-client-only-datasources) for ways to populate a client-only DataSource with cache data.

Additionally, when a DataSource is loaded in [DataSource.mockMode](#attr-datasourcemockmode), `cacheData`, if provided, is used as the mock data.

For any other DataSource, `cacheData` is dropped when loaded.

### Groups

- clientData

**Flags**: IRW

---
## Attr: DataSource.ID

### Description
Unique identifier for this DataSource. Required for all DataSources. DataSources will make themselves available as JavaScript globals under the same name as their ID only if [DataSource.addGlobalId](#attr-datasourceaddglobalid) is set.

### Groups

- identity

### See Also

- [memoryLeaks](../kb_topics/memoryLeaks.md#kb-topic-memory-leaks)

**Flags**: IR

---
## Attr: DataSource.maxFileVersions

### Description
If [automatic file versioning](#attr-datasourcefileversionfield) is enabled for a FileSource DataSource, this property configures the maximum number of versions to retain.

### Groups

- fileSource

### See Also

- [DataSource.fileVersionField](#attr-datasourcefileversionfield)

**Flags**: IR

---
## Attr: DataSource.tagName

### Description
Tag name to use when serializing to XML. If unspecified, the `dataSource.ID` will be used.

### Groups

- clientDataIntegration

**Flags**: IRA

---
## Attr: DataSource.generateAuditDS

### Description
For an [audited](#attr-datasourceaudit) DataSource, controls whether the Framework will attempt to auto-generate the audit DataSource. Note that this property is independent of [DataSource.auditDataSourceID](#attr-datasourceauditdatasourceid) so that, by default, even when the audit DataSource is given a non-default ID, the Framework will still attempt to auto-generate it.

**Flags**: IR

---
## Attr: DataSource.useStrictJSON

### Description
Should HTTP responses to requests by this dataSource be formatted using the strict JSON subset of the javascript language? If set to true, responses returned by the server should match the format described [here](https://www.json.org/json-en.html).

Only applies to dataSources which send requests to a server and have [DataSource.dataFormat](#attr-datasourcedataformat) set to "json" or "iscServer".

**Note:** using strict JSON avoids a known issue in Internet Explorer 9 where datasource transactions can leak memory due to a browser behavior where the native `eval()` method fails to clean up references when the objects go out of scope. See [RPCManager.allowIE9Leak](RPCManager.md#classattr-rpcmanagerallowie9leak) for more on this.

**Flags**: IR

---
## Attr: DataSource.allowClientRequestedSummaries

### Description
If a [DSRequest](../reference.md#object-dsrequest) arrives from the client that requests [server-calculated summaries](../kb_topics/serverSummaries.md#kb-topic-server-summaries), should it be allowed?

Note this setting **only** affects `dsRequests` that come from the browser (or another client). This setting has no effect on server summaries declared in .ds.xml files or summaries configured in DSRequests created programmatically on the server side, which are always allowed.

Default value of null means this DataSource will use the system-wide default, which is set via `datasources.allowClientRequestedSummaries` in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file), and defaults to allowing client-requested summaries.

If client-requested summarization is allowed, but the server-side `<operationBinding>` provides specific summarization settings, the client-requested summarization is ignored.

### Groups

- serverSummaries

### See Also

- [DataSourceField.allowClientRequestedSummaries](DataSourceField.md#attr-datasourcefieldallowclientrequestedsummaries)

**Flags**: IR

---
## Attr: DataSource.testData

### Description
For a client-only DataSource, a set of records to use as a dataset, specified as an Array of JavaScript Objects.

See [this discussion](../kb_topics/clientOnlyDataSources.md#kb-topic-client-only-datasources) for ways to populate a client-only DataSource with test data.

### Groups

- clientData

**Deprecated**

**Flags**: IRW

---
## Attr: DataSource.enforceSecurityOnClient

### Description
Indicates that [declarativeSecurity](../kb_topics/declarativeSecurity.md#kb-topic-declarative-security) should be enforced on the client. This property only applies to [Client Only DataSources](../kb_topics/clientOnlyDataSources.md#kb-topic-client-only-datasources). If property is unset for a clientOnly DataSource it will be set `true` automatically. Set this property to `false` to explicitly disable this feature for a clientOnly DataSource.

Note that certain security features are not supported on the client like Velocity rules.

### Groups

- declarativeSecurity

**Flags**: IR

---
## Attr: DataSource.useLocalValidators

### Description
Whether to attempt validation on the client at all for this DataSource. If unset (the default), client-side validation is enabled.

Disabling client-side validation entirely is a good way to test server-side validation.

### Groups

- validation

**Flags**: IRWA

---
## Attr: DataSource.enumTranslateStrategy

### Description
Sets the strategy this DataSource uses to translate Java enumerated types (objects of type enum) to and from Javascript. This property is only applicable if you are using the SmartClient server

**Flags**: IA

---
## Attr: DataSource.clientOnly

### Description
A clientOnly DataSource simulates the behavior of a remote data store by manipulating a static dataset in memory as [DSRequests](../reference.md#object-dsrequest) are executed on it. Any changes are lost when the user reloads the page or navigates away.

A clientOnly DataSource will return responses asynchronously, just as a DataSource accessing remote data does. This allows a clientOnly DataSource to be used as a temporary placeholder while a real DataSource is being implemented - if a clientOnly DataSource is replaced by a DataSource that accesses a remote data store, UI code for components that used the clientOnly DataSource will not need be changed.

A clientOnly DataSource can also be used as a shared cache of modifiable data across multiple UI components when immediate saving is not desirable. In this case, several components may interact with a clientOnly DataSource and get the benefit of [ResultSet](ResultSet.md#class-resultset) behaviors such as automatic cache sync and in-browser data filtering and sorting. When it's finally time to save, [DataSource.cacheData](#attr-datasourcecachedata) can be inspected for changes and data can be saved to the original DataSource via [DataSource.addData](#method-datasourceadddata), [DataSource.updateData](#method-datasourceupdatedata) and [DataSource.removeData](#method-datasourceremovedata), possibly in a [transactional queue](RPCManager.md#classmethod-rpcmanagerstartqueue). Note that [DataSource.getClientOnlyDataSource](#method-datasourcegetclientonlydatasource) lets you easily obtain a `clientOnly` DataSource representing a subset of the data available from a normal DataSource.

See also [DataSource.cacheAllData](#attr-datasourcecachealldata) - a `cacheAllData` behaves like a write-through cache, performing fetch and filter operations locally while still performing remote save operations immediately.

ClientOnly DataSources can be populated programmatically via [DataSource.cacheData](#attr-datasourcecachedata) - see [this discussion](../kb_topics/clientOnlyDataSources.md#kb-topic-client-only-datasources) for other ways to populate a client-only DataSource with data.

### Groups

- clientOnlyDataSources

**Flags**: IR

---
## Attr: DataSource.ignoreTextMatchStyleCaseSensitive

### Description
For fields on this dataSource that specify [ignoreTextMatchStyle](DataSourceField.md#attr-datasourcefieldignoretextmatchstyle) true, the prevailing textMatchStyle is ignored and SmartClient matches exact values. This property dictates whether that match is case-sensitive like the "exactCase" textMatchStyle, or case-insensitive like the "exact" textMatchStyle (the default). Please see the [TextMatchStyle documentation](../reference_2.md#type-textmatchstyle) for a discussion of the nuances of case-sensitive matching.

**Flags**: IR

---
## Attr: DataSource.cacheAllData

### Description
Set this property to true to have a DataSource fetch all of its data client-side on the first fetch request. However, unlike a [clientOnly](#attr-datasourceclientonly) DataSource, this DataSource will still save changes normally, sending remote requests.

You can manually set this attribute after initialization by calling [DataSource.setCacheAllData](#method-datasourcesetcachealldata); setting [DataSource.autoCacheAllData](#attr-datasourceautocachealldata):true causes a DataSource to automatically switch to `cacheAllData:true` when a fetch results in the entire dataset being brought client-side.

To cause automatic cache updates, you can set [DataSource.cacheMaxAge](#attr-datasourcecachemaxage) to a number of seconds and once data has been client-side for that length of time, the next fetch causes the cache to be dropped and a new cache retrieved.

Note that multiple [DataSource.operationBindings](#attr-datasourceoperationbindings) of type "fetch" which return distinct results will not work with `cacheAllData`: only one cache is created and is used for all fetch operations, regardless of whether [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) has been set. However, "fetch" operationBindings used as a [OperationBinding.cacheSyncOperation](OperationBinding.md#attr-operationbindingcachesyncoperation) will work normally, so long as they return all data fields that are returned by the default "fetch" operation, so that the cache can be updated.

To specify which operationId to use for fetching all data, use [cacheAllOperationId](#attr-datasourcecachealloperationid).

To use the cache only for requests that have the `cacheAllOperationId`, allowing any other operationId (or absence of an operationId) to contact the server as normal, set [cacheAcrossOperationIds](#attr-datasourcecacheacrossoperationids).

### Groups

- clientData

**Flags**: IRW

---
## Attr: DataSource.criteriaPolicy

### Description
Decides under what conditions the [ResultSet](ResultSet.md#class-resultset) cache should be dropped when the [ResultSet.criteria](ResultSet.md#attr-resultsetcriteria) changes.

### See Also

- [DataSource.compareCriteria](#method-datasourcecomparecriteria)

**Flags**: IRWA

---
## Attr: DataSource.logSlowAdd

### Description
Allows you to specify ["add" operation](../reference.md#type-dsoperationtype) SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category.

See [DataSource.logSlowSQL](#attr-datasourcelogslowsql) for more details.

**Flags**: IR

---
## Attr: DataSource.callbackParam

### Description
Applies only to dataFormat: "json" and [DataSource.dataTransport](#attr-datasourcedatatransport):"scriptInclude". Specifies the name of the query parameter that tells your JSON service what function to call as part of the response.

### Groups

- clientDataIntegration

### See Also

- [DataSource.dataFormat](#attr-datasourcedataformat)
- [DataSource.operationBindings](#attr-datasourceoperationbindings)
- [OperationBinding.callbackParam](OperationBinding.md#attr-operationbindingcallbackparam)

**Flags**: IR

---
## Attr: DataSource.auditTimeStampFieldName

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), specifies the field name used to store the timestamp when the operation was performed (in a field of type "datetime"). If empty string is specified as the field name, the audit DataSource will not store this field.

**Flags**: IR

---
## Attr: DataSource.mockDataCriteria

### Description
When [DataSource.mockMode](#attr-datasourcemockmode) is enabled, criteria to use in an initial "fetch" DSRequest to retrieve sample data.

**Flags**: IR

---
## Attr: DataSource.progressiveLoadingThreshold

### Description
Indicates the dataset size that will cause SmartClient Server to automatically switch into [progressive loading mode](#attr-datasourceprogressiveloading) for this DataSource. To prevent automatic switching to progressive loading, set this property to -1. This may also be prevented on a per-request basis by setting [DSRequest.progressiveLoading](DSRequest.md#attr-dsrequestprogressiveloading) to `false`.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](#attr-datasourceprogressiveloading)
- [DSRequest.progressiveLoading](DSRequest.md#attr-dsrequestprogressiveloading)

**Flags**: IRW

---
## Attr: DataSource.showLocalFieldsOnly

### Description
For a DataSource that inherits [DataSource.fields](#attr-datasourcefields) from another DataSource (via [DataSource.inheritsFrom](#attr-datasourceinheritsfrom)), indicates that only the fields listed in this DataSource should be shown. All other inherited parent fields will be marked "hidden:true".

### Groups

- fields

**Flags**: IR

---
## Attr: DataSource.addGlobalId

### Description
Whether to make this DataSource available as a global variable for convenience.

### Groups

- identity

**Flags**: IRA

---
## Attr: DataSource.deepCloneNonFieldValuesOnEdit

### Description
When editing values in [DataBoundComponent](../reference.md#interface-databoundcomponent)s bound to this dataSource, should we perform a deep clone of values that are not associated with a field (ie, attributes on the record that do not map to a component field either directly by name, or by [dataPath](FormItem.md#attr-formitemdatapath)). If this flag is not explicitly set, it defaults to the value of the same-named static property, [DataSource.deepCloneNonFieldValuesOnEdit](#classattr-datasourcedeepclonenonfieldvaluesonedit). This flag can also be overridden per-component - see [DataBoundComponent.deepCloneNonFieldValuesOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepclonenonfieldvaluesonedit).

Note, a "deep clone" is one created by traversing the original values object recursively, cloning the contents of nested objects and arrays; a "shallow clone" is a copy created by simply copying the top-level attributes of an object; if you have nested objects that are copied like this, the "copies" are actual references to the original objects.

Like the other `deepCloneOnEdit` settings, this flag only has an effect if you are editing a values object that contains nested objects or arrays.

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [FormItem.dataPath](FormItem.md#attr-formitemdatapath)
- [DataBoundComponent.deepCloneOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepcloneonedit)
- [DataBoundComponent.deepCloneNonFieldValuesOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepclonenonfieldvaluesonedit)
- [ValuesManager.deepCloneOnEdit](ValuesManager.md#attr-valuesmanagerdeepcloneonedit)

**Flags**: IRWA

---
## Attr: DataSource.cacheAllOperationId

### Description
[DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) to use for fetching data in case [cacheAllData](#attr-datasourcecachealldata) is true. By default a standard fetch operation is used (with no `operationId` specified).

### Groups

- clientData

**Flags**: IR

---
## Attr: DataSource.useTestDataFetch

### Description
When set, causes a [client-only](#attr-datasourceclientonly) or [DataSource.cacheAllData](#attr-datasourcecachealldata) DataSource to create a second DataSource to perform it's one-time fetch. By default, this attribute will be considered true when clientOnly is true, cacheAllData is false or unset and a dataURL or testFileName is specified on the DataSource.

### Groups

- clientData

**Flags**: IRW

---
## Attr: DataSource.serviceNamespace

### Description
For an XML DataSource, URN of the WebService to use to invoke operations. This URN comes from the "targetNamespace" attribute of the <wsdl:definitions> element in a WSDL (Web Service Description Language) document, and serves as the unique identifier of the service.

Having loaded a WebService using [XMLTools.loadWSDL](XMLTools.md#classmethod-xmltoolsloadwsdl), setting `serviceNamespace` combined with specifying [operationBindings](OperationBinding.md#class-operationbinding) that set [OperationBinding.wsOperation](OperationBinding.md#attr-operationbindingwsoperation) will cause a DataSource to invoke web service operations to fulfill DataSource requests ([DSRequests](../reference.md#object-dsrequest)).

Setting `serviceNamespace` also defaults [dataURL](#attr-datasourcedataurl) to the service's location, [dataFormat](#attr-datasourcedataformat) to "xml" and [dataProtocol](OperationBinding.md#attr-operationbindingdataprotocol) to "soap".

### Groups

- wsdlBinding
- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.fileVersionField

### Description
The native field name used by this DataSource on the server to represent `fileVersion` for [FileSource Operations](../kb_topics/fileSource.md#kb-topic-filesource-operations).

Automatic file versioning is configured by the presence of this property: if you want automatic versioning for a FileSource DataSource, it is sufficient to simply define a `fileVersionField`. When automatic versioning is on:

*   Calls to [DataSource.saveFile](#method-datasourcesavefile) will save a new version of the file, retaining previous versions up to the maximum configured by [DataSource.maxFileVersions](#attr-datasourcemaxfileversions); when that maximum is reached, the oldest version is overwritten
*   The [DataSource.getFile](#method-datasourcegetfile) API always returns the most recent version
*   The [DataSource.listFiles](#method-datasourcelistfiles) API only includes the most recent version of any file
*   You can view and retrieve earlier versions of a file with the [DataSource.listFileVersions](#method-datasourcelistfileversions) and [DataSource.getFileVersion](#method-datasourcegetfileversion) APIs. Note that retrieving a previous version of a file and then calling `saveFile()` goes through the normal process of saving a new version

The `fileVersion` field is expected to be of type "datetime", and automatic versioning will not work otherwise. Note, to minimize the possibility of version timestamp collisions, we recommend that `fileVersion` fields specify [storeMilliseconds](DataSourceField.md#attr-datasourcefieldstoremilliseconds): true.

If the fileVersionField is not configured, no automatic file versioning will be done.

### Groups

- fileSource

### See Also

- [DataSource.maxFileVersions](#attr-datasourcemaxfileversions)
- [DataSource.listFileVersions](#method-datasourcelistfileversions)
- [DataSource.getFileVersion](#method-datasourcegetfileversion)
- [DataSource.removeFileVersion](#method-datasourceremovefileversion)

**Flags**: IR

---
## Attr: DataSource.unionFields

### Description
Only applicable to "union" dataSources, this is a comma-separated list of the names of the dataSource fields that make up the union. This property is optional; if it is not supplied, SmartClient Server will derive a list of fields from the member dataSources (see [unionOf](#attr-datasourceunionof)), where name and data type match. See [defaultUnionFieldsStrategy](#attr-datasourcedefaultunionfieldsstrategy) for more details.

Note, this setting is only useful for fields that are named the same on the member dataSources. For a more flexible and powerful way to define the unioned fields, that does not rely on field names being the same in member dataSources, you can use [field-level unionOf definitions](DataSourceField.md#attr-datasourcefieldunionof).

### Groups

- unionDataSource

### See Also

- [OperationBinding.unionFields](OperationBinding.md#attr-operationbindingunionfields)

**Flags**: IR

---
## Attr: DataSource.noNullUpdates

### Description
When true, indicates that fields in this DataSource will never be positively updated to the null value; they may arrive at null values by being omitted, but we will not send actual null values in update requests. When false (the default), null is not treated in any special way.

Setting this value causes null-assigned fields to be replaced with the field's [nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue), if one is declared. If no `nullReplacementValue` is declared for the field, the null assignment is replaced with the DataSource's [nullStringValue](#attr-datasourcenullstringvalue), [nullIntegerValue](#attr-datasourcenullintegervalue), [nullFloatValue](#attr-datasourcenullfloatvalue) or [nullDateValue](#attr-datasourcenulldatevalue), depending on the field type.

For "add" operations, setting [omitNullDefaultsOnAdd](#attr-datasourceomitnulldefaultsonadd) causes null-valued fields to be removed from the request entirely, rather than replaced with default values as described above.

**Flags**: IR

---
## Attr: DataSource.transformMultipleFields

### Description
If set to "false", transformation of values for [multiple:true](DataSourceField.md#attr-datasourcefieldmultiple) fields, normally controlled by [DataSourceField.multipleStorage](DataSourceField.md#attr-datasourcefieldmultiplestorage), is instead disabled for this entire DataSource.

### Groups

- multipleField

**Flags**: IR

---
## Attr: DataSource.suppressManualAggregation

### Description
For DataSources of [serverType](#attr-datasourceservertype) "generic" only, indicates whether we should suppress automatic aggregation and grouping handling logic. By default, the framework applies a post-fetch in-memory operation to handle aggregation and grouping, as described in the [allowAggregation](#attr-datasourceallowaggregation) documentation. You can suppress this automatic behavior by setting this flag true.

Note, this is primarily intended as a back-compatibility flag, to allow you to compensate for situations where your own custom DataSource implementations have their own aggregation handling, pre-dating the automatic in-memory aggregation feature. In this circumstance, set this flag true to retain the existing behavior. If you want to suppress the manual aggregation for **all** dataSources by default (you can still re-enable it per-DataSource if required, using this `suppressManualAggregation` flag), add the following to your `server.properties` file:

```
     datasource.suppress.manual.aggregation: true
 
```
Also note, this flag is ignored for SQL, JPA and Hibernate DataSources; those DataSource types handle aggregation inherently, using the underlying persistence engine's query language. If for some reason you need to suppress inherent aggregation for a given DataSource, mark it `[allowAggregation](#attr-datasourceallowaggregation):false`

### Groups

- serverDataIntegration

### See Also

- [DataSource.allowAggregation](#attr-datasourceallowaggregation)

**Flags**: IRA

---
## Attr: DataSource.simplifyCriteriaListsToOrClause

### Description
For [SQL DataSources](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) only, this flag indicates that we should render List-valued criteria elements as a series of simple comparisons linked with "OR" operators, rather than an SQL "IN" operation. For example, given any of the following simple or advanced criteria definitions (which are equivalent):
```
    {myField: ["x","y","z"]}
    {fieldName: "myField", operator:"equals", value: ["x","y","z"]}
    {fieldName: "myField", operator:"inSet", value: ["x","y","z"]}
 
```
We would generate an SQL WHERE clause similar to this:
```
    WHERE myField="x" OR myField="y" OR myField="z"
 
```
This is as opposed to the default handling of List-valued criteria elements, which is to render them as a simple SQL "IN" comparison, if the field is of text or numeric type:
```
    WHERE myField IN("x","y","z") 
 
```
**NOTE:** As mentioned above, the use of SQL "IN" by default is only for text and numeric fields; for any other field type, we always simplify a list in criteria to a series of OR comparisons, regardless of the setting of this flag. Also please note that this is intended as a backward-compatibility flag only, in case you have some special reason for wanting the OR-clause approach. The default use of "IN" leads to functionally equivalent but simpler SQL that may be more efficient or more easily optimized by some databases.

It is possible to apply this setting as the default for all DataSources - just add the following setting to your `server.properties` file:

```
    sql.simplifyCriteriaListsToOrClause: true
 
```

**Flags**: IRWA

---
## Attr: DataSource.enumConstantProperty

### Description
The name of the property this DataSource uses for constant name when translating Java enumerated types to and from Javascript, if the [EnumTranslateStrategy](../reference_2.md#type-enumtranslatestrategy) is set to "bean". Defaults to "\_constant" if not set.

This property is only applicable if you are using the SmartClient server

**Flags**: IA

---
## Attr: DataSource.recordName

### Description
Provides a default value for [OperationBinding.recordName](OperationBinding.md#attr-operationbindingrecordname).

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.sendParentNode

### Description
Set this attribute if you need to send the dsRequest.parentNode to the server-side.

**Flags**: IRWA

---
## Attr: DataSource.clientRequestMaxRows

### Description
Applies to [SQL DataSources](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) only.

If this attribute is set to a non-negative value, it acts as a hard safety limit for client-initiated [DSRequest](../reference.md#object-dsrequest)s for "all rows". If the server encounters more rows in a response than this safety limit, it will abort immediately with an Exception.

**This attribute is not meant to be a regular application facility.** As mentioned above, it is a safety mechanism, intended primarily to prevent bugs in development from causing long delays or server Out Of Memory crashes by unintentionally issuing requests that fetch huge numbers of rows (eg, by failing to specify filter criteria).

Note the following:

*   This limit only has an effect when "all rows" are requested - ie, when the request does not specify an [endRow](DSRequest.md#attr-dsrequestendrow), or specifies `endRow:-1`. If you specify a non-negative `endRow`, it will be honored even if that means we need to return more than `clientRequestMaxRows` records
*   If you need to handle very large datasets in a manageable way, consider using [progressiveLoading](../kb_topics/progressiveLoading.md#kb-topic-progressive-loading) to stream the data progressively
*   Note that this attribute applies to client-initiated requests only. If you want to provide a hard safety limit for all fetches, including requests initiated on the server, set a [DataSource.requestMaxRows](#attr-datasourcerequestmaxrows) instead. If both properties are specified, `clientRequestMaxRows` wins for client-initiated requests, so it is possible to configure different limits for client- and server-initiated requests

To set a default `clientRequestMaxRows` that will apply to all dataSources that do not specify the attribute, add the following to your `server.properties` file:

```
     # Fail with an error if we try to fetch more than 10000 rows in a client request
     sql.clientRequestMaxRows: 10000
 
```

### See Also

- [DataSource.clientRequestMaxRows](#attr-datasourceclientrequestmaxrows)
- [DataSource.progressiveLoading](#attr-datasourceprogressiveloading)

**Flags**: IRW

---
## Attr: DataSource.dataTransport

### Description
Transport to use for all operations on this DataSource. Defaults to [RPCManager.defaultTransport](RPCManager.md#classattr-rpcmanagerdefaulttransport). This would typically only be set to enable "scriptInclude" transport for contacting [JSON](#attr-datasourcedataformat) web services hosted on servers other than the origin server.

When using the "scriptInclude" transport, be sure to set [DataSource.callbackParam](#attr-datasourcecallbackparam) or [OperationBinding.callbackParam](OperationBinding.md#attr-operationbindingcallbackparam) to match the name of the query parameter name expected by your JSON service provider.

### Groups

- clientDataIntegration

### See Also

- [RPCTransport](../reference.md#type-rpctransport)
- [DataSource.callbackParam](#attr-datasourcecallbackparam)

**Flags**: IR

---
## Attr: DataSource.dropExtraFields

### Description
Indicates that for server responses, for any data being interpreted as DataSource records, only data that corresponds to declared fields should be retained; any extra fields should be discarded.

For [JSON](#attr-datasourcedataformat) data, this means extra properties in selected objects are dropped.

By default, for DMI DSResponses, DSResponse.data is filtered on the server to just the set of fields defined on the DataSource (see the overview in [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation)).

This type of filtering can also be enabled for non-DMI DSResponses. By default it is enabled for Hibernate and JPA datasources to avoid unintentional lazy loading too much of a data model. For the rest of datasources this is disabled by default.

Explicitly setting this property to `false` disables (or to `true` enables) this filtering for this DataSource only. This setting overrides the configuration in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file). This setting can be overridden by [ServerObject.dropExtraFields](ServerObject.md#attr-serverobjectdropextrafields).

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.dbName

### Description
For DataSources using the [SmartClient SQL engine](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) for persistence, which database configuration to use. Database configurations can be created using the [Admin Console](../kb_topics/adminConsole.md#kb-topic-admin-console). If unset, the default database configuration is used (which is also settable using the "Databases" tab).

### Groups

- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.quoteTableName

### Description
For SQL DataSources, tells the framework whether to surround the associated [table name](#attr-datasourcetablename) with quotation marks whenever it appears in generated queries. This is only required if you have to connect to a table with a name that is in breach of your database product's naming conventions. For example, some products (eg, Oracle) internally convert all unquoted references to upper case, so if you create a table called `**myTest**`, the database actually calls it `**MYTEST**` unless you quoted the name in the create command, like this:

  `**CREATE TABLE "myTest"**`

If you _do_ quote the name like this, or if you have to connect to a legacy table that has been named in this way, then you must set this property to tell the SQL engine that it must quote any references to this table name (this requirement depends on the database in use - as noted below, some are not affected by this problem). If you do not, you will see exceptions along the lines of "Table or view 'myTest' does not exist".

Note, other database products (eg, Postgres) convert unquoted names to lower case, which leads to the same issues. Still others (eg, SQL Server) are not case sensitive and are not affected by this issue.

Generally, we recommend that you avoid using this property unless you have a specific reason to do so. It is preferable to avoid the issue altogether by simply not quoting table names at creation time, if you are able to do so.

### Groups

- serverDataIntegration

### See Also

- [DataSource.tableName](#attr-datasourcetablename)
- [DataSource.quoteColumnNames](#attr-datasourcequotecolumnnames)

**Flags**: IRA

---
## Attr: DataSource.fileLastModifiedField

### Description
The native field name used by this DataSource on the server to represent `fileLastModified` for [FileSource Operations](../kb_topics/fileSource.md#kb-topic-filesource-operations).

If the fileLastModifiedField is not configured, then a field named "fileLastModified" will be used, if it exists. Otherwise, the server will look for a field with a "modifierTimestamp" type. If that is not found, the DataSource will not keep track of the last modified date.

### Groups

- fileSource

**Flags**: IR

---
## Attr: DataSource.descriptionField

### Description
Name of the field that has a long description of the record, or has the primary text data value for a record that represents an email message, SMS, log or similar.

For example, for a DataSource representing employees, a field containing the employee's "bio" might be a good choice, or for an email message, the message body.

If descriptionField is unset, it defaults to any field named "description" or "desc" in the record, or the first long text field (greater than 255 characters) in the record, or null if no such field exists.

### Groups

- dsSpecialFields

**Flags**: IR

---
## Attr: DataSource.serverObject

### Description
For Direct Method Invocation (DMI) binding, declares the ServerObject to use as the default target for all [DataSource.operationBindings](#attr-datasourceoperationbindings). Specifying this attribute in an XML DataSource stored on the server enables DMI for this DataSource.

_Note that if a dataSource configuration has both a [`<script>`](OperationBinding.md#attr-operationbindingscript) block and a specified `serverObject` for some operation, the script block will be executed, and the serverObject ignored._

### Groups

- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.validateRelatedRecords

### Description
If true, indicates that the SmartClient Server should automatically apply a [ValidatorType](../reference.md#type-validatortype) of "hasRelatedRecord" to every field on this dataSource that has a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) defined.

**Flags**: IR

---
## Attr: DataSource.logSlowCustom

### Description
Allows you to specify ["custom" operation](../reference.md#type-dsoperationtype) SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category.

See [DataSource.logSlowSQL](#attr-datasourcelogslowsql) for more details.

**Flags**: IR

---
## Attr: DataSource.autoDeriveTitles

### Description
If set, titles are automatically derived from [field.name](DataSourceField.md#attr-datasourcefieldname) for any field that does not have a [field.title](DataSourceField.md#attr-datasourcefieldtitle) and is not marked [hidden](DataSourceField.md#attr-datasourcefieldhidden):true, by calling the method [DataSource.getAutoTitle](#method-datasourcegetautotitle).

**Flags**: IR

---
## Attr: DataSource.sparseUpdates

### Description
When true, indicates that any updates for this DataSource include only those fields that have actually changed (and primaryKey fields); when false (the default), all field values are included in updates, whether they have changed or not

**Flags**: IR

---
## Attr: DataSource.strictSQLFiltering

### Description
If set to true, both client and server-side advanced filtering used by SmartClient will follow SQL99 behavior for dealing with NULL values, which is often counter-intuitive to users. Specifically, when a field has NULL value, all of the following expressions are false:
```
    field == "someValue"  (normally false)
    field != "someValue"  (normally true)
    not (field == "someValue")   (normally true)
    not (field != "someValue")   (normally false)
 
```
This property can be overridden per-query by specifying `strictSQLFiltering` directly as a property on the [AdvancedCriteria](../reference.md#object-advancedcriteria).

**NOTE:** On the server side, this property is only applicable if you are using the SQL DataSource; the other built-in types (Hibernate and JPA/JPA2) do not offer this mode.

**Flags**: IRA

---
## Attr: DataSource.progressiveLoading

### Description
If true, causes SmartClient Server to use the "progressive loading" pattern for fetches on this dataSource, as described in the **Paging and total dataset length** section of the [ResultSet documentation](ResultSet.md#class-resultset). Essentially, this means that we avoid issuing a row count query and instead advertise total rows as being slightly more than the number of rows we have already read (see [endGap](#attr-datasourceendgap)). This allows users to load more of a dataset by scrolling past the end of the currently-loaded rows, but it prevents them from scrolling directly to the end of the dataset.

Generally, progressive loading is appropriate when you have to deal with very large datasets. Note that by default, a dataSource will switch into progressive loading mode automatically when it detects that it is dealing with a dataset beyond a certain size - see [DataSource.progressiveLoadingThreshold](#attr-datasourceprogressiveloadingthreshold).

This setting can be overridden for individual fetch operations with the [OperationBinding.progressiveLoading](OperationBinding.md#attr-operationbindingprogressiveloading) property, and also at the level of the individual [DSRequest](DSRequest.md#attr-dsrequestprogressiveloading). You can also specify `progressiveLoading` on [DataBoundComponents](DataBoundComponent.md#attr-databoundcomponentprogressiveloading) and certain types of `FormItem` - [SelectItem](SelectItem.md#attr-selectitemprogressiveloading) and [ComboBoxItem](ComboBoxItem.md#attr-comboboxitemprogressiveloading).

Currently, this property only applies to users of the built-in SQLDataSource, but you could use it in custom DataSource implementations to trigger the server behavior described in the `ResultSet` documentation linked to above.

### Groups

- progressiveLoading

### See Also

- [OperationBinding.progressiveLoading](OperationBinding.md#attr-operationbindingprogressiveloading)
- [DataSource.progressiveLoadingThreshold](#attr-datasourceprogressiveloadingthreshold)
- [DataSource.lookAhead](#attr-datasourcelookahead)
- [DataSource.endGap](#attr-datasourceendgap)

**Flags**: IRW

---
## Attr: DataSource.configBean

### Description
For DataSources of [serverType](#attr-datasourceservertype) "hibernate", the name of a Spring bean to query to obtain Hibernate Configuration for this particular DataSource. Note that this is intended for DataSource-specific configuration overrides for unusual circumstances, such as a DataSource whose physical data store is a completely different database to that used by other DataSources. See the [Integration with Hibernate](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) article for more information

### Groups

- serverDataIntegration

**Flags**: IRA

---
## Attr: DataSource.schemaBean

### Description
For DataSources that specify [DataSource.autoDeriveSchema](#attr-datasourceautoderiveschema), this property indicates the name of the Spring bean, Hibernate mapping or fully-qualified Java class to use as parent schema.

### Groups

- fields

### See Also

- [DataSource.autoDeriveSchema](#attr-datasourceautoderiveschema)

**Flags**: IR

---
## Attr: DataSource.discoverTreeSettings

### Description
Settings to use when discoverTree() is automatcially called because [DataSource.autoDiscoverTree](#attr-datasourceautodiscovertree) is set to true for this DataSource

**Flags**: IR

---
## Attr: DataSource.auditDSConstructor

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), optionally specifies the [DataSource.serverConstructor](#attr-datasourceserverconstructor) for the automatically generated audit DataSource. The default is to use the same `serverConstructor` as the DataSource where `audit="true"` was declared.

This property is primarily intended to allow the use of SQLDataSource ([serverType:"sql"](#attr-datasourceservertype)) as an audit DataSource for a DataSource that might be of another type. For example, you might have a DataSource that implements all CRUD operations via Java logic in [DMI declaration](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) methods, and so doesn't provide generic storage; by using SQLDataSource as the type of your audit DataSource, you don't need to implement your own scheme for storing and querying audit data, and the necessary audit tables will be automatically generated in the database.

Similarly, even if you do use a reusable DataSource type such as the built-in JPADataSource, using SQLDataSource for audit DataSources means there's no need to write a JPA bean just to achieve storage of an audit trail.

To simplify this intended usage, the string "sql" is allowed for `auditDSConstructor` as a means of specifying that the built-in SQLDataSource class should be used. For any other type, use the fully qualified Java classname, as is normal for `serverConstructor`.

**Flags**: IR

---
## Attr: DataSource.cacheSyncTiming

### Description
The [cacheSyncTiming](../reference_2.md#type-cachesynctiming) to use for operations on this DataSource. Can be overridden at the [operation](OperationBinding.md#attr-operationbindingcachesynctiming) and [DSRequest](DSRequest.md#attr-dsrequestcachesynctiming) levels. The default value of null is the same as specifying "immediate".

Note that `cacheSyncTiming` is not applicable to many common types of request, and is simply ignored for these request types. See the [CacheSyncTiming type documentation](../reference_2.md#type-cachesynctiming) for more details.

### Groups

- cacheSynchronization

### See Also

- [DataSource.cacheSyncStrategy](#attr-datasourcecachesyncstrategy)
- [OperationBinding.cacheSyncTiming](OperationBinding.md#attr-operationbindingcachesynctiming)
- [DSRequest.cacheSyncTiming](DSRequest.md#attr-dsrequestcachesynctiming)

**Flags**: IR

---
## Attr: DataSource.enumOrdinalProperty

### Description
The name of the property this DataSource uses for ordinal number when translating Java enumerated types to and from Javascript, if the [EnumTranslateStrategy](../reference_2.md#type-enumtranslatestrategy) is set to "bean". Defaults to "\_ordinal" if not set.

This property is only applicable if you are using the SmartClient server

**Flags**: IA

---
## Attr: DataSource.useAnsiJoins

### Description
For DataSources using the [SmartClient SQL engine](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) for persistence, whether to use ANSI-style joins (ie, joins implemented with JOIN directives in the table clause, as opposed to additional join expressions in the where clause). The default value of null has the same meaning as setting this flag to false.

Note, outer joins (see [joinType](DataSourceField.md#attr-datasourcefieldjointype)) do not work with all supported database products unless you use ANSI joins. Other than that, the join strategies are equivalent.

If you wish to switch on ANSI-style joins for every DataSource, without the need to manually set this property on all of them, set [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) flag `sql.useAnsiJoins` to true.

### Groups

- serverDataIntegration

### See Also

- [OperationBinding.includeAnsiJoinsInTableClause](OperationBinding.md#attr-operationbindingincludeansijoinsintableclause)

**Flags**: IR

---
## Attr: DataSource.showPrompt

### Description
Whether RPCRequests sent by this DataSource should enable [RPCRequest.showPrompt](RPCRequest.md#attr-rpcrequestshowprompt) in order to block user interactions until the request completes.

DataSource requests default to blocking UI interaction because, very often, if the user continues to interact with an application that is waiting for a server response, some kind of invalid or ambiguous situation can arise.

Examples include pressing a "Save" button a second time before the first save completes, making further edits while edits are still being saved, or trying to initiate editing on a grid that hasn't loaded data.

Defaulting to blocking the UI prevents these bad interactions, or alternatively, avoids the developer having to write repetitive code to block invalid interactions on every screen.

If an operation should ever be non-blocking, methods that initiate DataSource requests (such as [DataSource.fetchData](#method-datasourcefetchdata)) will generally have a `requestProperties` argument allowing `showPrompt` to be set to false for a specific request.

**Flags**: IRW

---
## Attr: DataSource.defaultTextMatchStyle

### Description
The default textMatchStyle to use for [DSRequest](../reference.md#object-dsrequest)s that do not explicitly state a [textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle). Note, however, that DSRequests issued by [ListGrid](ListGrid_1.md#class-listgrid)s and other [components](../reference.md#interface-databoundcomponent) will generally have a setting for textMatchStyle on the component itself (see [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle), for example).

### Groups

- clientDataIntegration
- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.patternSingleWildcard

### Description
When using the [pattern operators](../kb_topics/patternOperators.md#kb-topic-patternoperators) [search operator](../reference.md#type-operatorid), character that matches any single character.

Pass multiple strings to provide multiple alternative wildcards.

**Flags**: IR

---
## Attr: DataSource.mockDataRows

### Description
When [DataSource.mockMode](#attr-datasourcemockmode) is enabled, number of rows of data to retrieve via an initial "fetch" DSRequest, for use as sample data. Set to null to retrieve all available rows.

**Flags**: IR

---
## Attr: DataSource.requiredMessage

### Description
The required message when a field that has been marked as [required](DataSourceField.md#attr-datasourcefieldrequired) is not filled in by the user.

Note that [DataSourceField.requiredMessage](DataSourceField.md#attr-datasourcefieldrequiredmessage) wins over this setting if both are set.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DataSource.autoConvertRelativeDates

### Description
Whether to convert relative date values to concrete date values before sending to the server. Default value is true, which means that the server does not need to understand how to filter using relative dates - it receives all date values as absolute dates.

If the server would receive relative date values from the client, by default they would be unchanged in DMI and automatically converted during the request execution. This may be changed via `server.properties` setting `datasources.autoConvertRelativeDates` which can be set to the following values:

*   `postDMI` - the default value described above
*   `preDMI` - relative date values will be converted to absolute date values right away, so they will be already converted in DMI
*   `disabled` - relative date values will not be automatically converted, so it must be done completely manually or by calling the `DSRequest.convertRelativeDates()` server-side API.

Normally there is no need to convert relative dates on the server, this is done by default on the client before the request is sent to the server. The primary purpose for converting relative dates on the server is when there is a need to store and use relative dates at a later point such as in an automated job without any involvement from the client. See more details in the javadoc for `DataSource.convertRelativeDates(Criterion)` server-side API.

**Flags**: IR

---
## Attr: DataSource.title

### Description
User-visible name for this DataSource.

For example, for the supplyItem DataSource, "Supply Item".

If is unset, `getAutoTitle()` method will be used with `dataSource.ID`. value in order to derive a default value for the title.

For example "employee" ID will be derived to "Employee", "team\_member" ID will be derived to "Team Member".

### Groups

- titles

**Flags**: IRW

---
## Attr: DataSource.globalNamespaces

### Description
Namespaces definitions to add to the root element of outbound XML messages sent to a web service, as a mapping from namespace prefix to namespace URI.

The default value is:

```
   globalNamespaces : {
      xsi: "http://www.w3.org/2001/XMLSchema-instance",
      xsd: "http://www.w3.org/2001/XMLSchema"
   },
 
```
This default value allows the use of the xsi:type and xsi:nil attributes without further declarations.

Note that some web services will only accept specific revisions of the XML Schema URI. If xsi-namespaced attributes seem to be ignored by an older webservice, try the URI "http://www.w3.org/1999/XMLSchema-instance" instead.

**Flags**: IRW

---
## Attr: DataSource.sendExtraFields

### Description
Analogous to [DataSource.dropExtraFields](#attr-datasourcedropextrafields), for data sent to the server. Setting this attribute to false ensures that for any records in the data object, only fields that correspond to declared dataSource fields will be present on the dsRequest data object passed to [DataSource.transformRequest](#method-datasourcetransformrequest) and ultimately sent to the server.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.implicitCriteria

### Description
Criteria that are implicitly applied to all fetches made through this DataSource. These criteria are never shown to or edited by the user and are cumulative with any other criteria provided on the DSRequest.

For example, a DataSource might \*always\* implicitly limit its fetch results to records owned by the current user's department. Components and ResultSets requesting data from the DataSource can then apply further implicitCriteria of their own, separately from their regular, user-editable criteria.

For instance, a grid bound to this dataSource might be further limited to implicitly show only the subset of records created by the current user. See [DataBoundComponent.implicitCriteria](DataBoundComponent.md#attr-databoundcomponentimplicitcriteria) and [ResultSet.implicitCriteria](ResultSet.md#attr-resultsetimplicitcriteria) for more on these localized options.

Note that, while `implicitCriteria` can be declared in a server DataSource file using [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml), it is an entirely client-side feature, added by client-side components. So it does not affect server-side requests, and will not be added to client-side requests that don't come from a SmartClient UI (eg RestHandler).

**Flags**: IRW

---
## Attr: DataSource.pluralTitle

### Description
User-visible plural name for this DataSource.

For example, for the supplyItem DataSource, "Supply Items".

Defaults to `dataSource.title` + "s".

### Groups

- titles

**Flags**: IR

---
## Attr: DataSource.tableName

### Description
For DataSources using the [SmartClient SQL engine](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) for persistence, what database table name to use. The default is to use the DataSource ID as the table name.

### Groups

- serverDataIntegration

### See Also

- [DataSource.quoteTableName](#attr-datasourcequotetablename)

**Flags**: IR

---
## Attr: DataSource.unionOf

### Description
Only applicable to "union" dataSources, this is a comma-separated list of the names of the member dataSources that make up the union. If all the named dataSources are [SQL DataSource](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources)s, or union dataSources whose members are SQL dataSurces, the union will be implemented purely in SQL, which is the most efficient thing to do.

**Nesting Union DataSources**  
It is valid for union DataSources to be nested inside other union DataSources; nesting is valid to any depth. If you are nesting union dataSources, bear in mind the following considerations:

*   If you are renaming fields from underlying SQL DataSources in a union DataSource, and you then include that union DataSource as a nested element of another union DataSource, it is the renamed fields that should be referenced in the outer union DataSource. For example, if you have union DataSource "union1" that specifes a unioned field like this:
    ```
        <field name="c" unionOf="sqlDS1.a, sqlDS2.b" />
    ```
    If you want to then include dataSource "union1" as a member dataSource of another union dataSource, "union2", you need to refer to the field as "c", not "a" or "b":
    ```
        <field name="myField" unionOf="union1.c, sqlDS3.xyz" />
    ```
    SmartClient will follow the chain of field renames to ensure that the appropriate SQL-level fields are unioned together, and renamed consistently
*   It is not an error to specify the same dataSource as a member of a union dataSource multiple times, but it is also not correct and may have performance implications. If you configure duplicate member dataSources directly, eg:
    ```
        <DataSource serverType="union" unionOf="sqlDS1,sqlDS2,sqlDS1">
    ```
    SmartClient will simply remove the duplicate entries. However, with nested union dataSources, it becomes possible to indirectly include the same member dataSource more than once. Eg:
    ```
        <DataSource ID="bigUnion" serverType="union" unionOf="union1,union2">
    ```
    and
    ```
        <DataSource ID="union1" serverType="union" unionOf="sqlDS1,sqlDS2">
    ```
    and
    ```
        <DataSource ID="union2" serverType="union" unionOf="sqlDS2,sqlDS3">
    ```
    You can see, dataSource "sqlDS2" is going to be included twice. This will result in the union DataSource generating SQL that fetches the rows from "sqlDS2" twice, but because of the way the SQL "UNION" keyword works, all the duplicate rows will be dropped. So the end result will be correct, but the system will have wasted time fetching and then dropping duplicate rows.
*   The ability to nest union dataSources within other union dataSources introduces a whole category of extra considerations. For example, you need to make sure you do not set up self references or looping structures, and as mentioned above, field renaming becomes potentially more involved

### Groups

- unionDataSource

**Flags**: IR

---
## Attr: DataSource.recordXPath

### Description
See [OperationBinding.recordXPath](OperationBinding.md#attr-operationbindingrecordxpath). `recordXPath` can be specified directly on the DataSource for a simple read-only DataSource only capable of "fetch" operations, or on clientOnly DataSources using [testData](../kb_topics/testData.md#kb-topic-test-data)

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.useSubselectForRowCount

### Description
This property is only applicable to [SQL](#attr-datasourceservertype) DataSources, and only for [operations](OperationBinding.md#class-operationbinding) that express a [customSQL](OperationBinding.md#attr-operationbindingcustomsql) clause. In these circumstances, we generally switch off paging because we are unable to generate a "row count" query that tells the framework the size of the complete, unpaged resultset.

The `useSubselectForRowCount` flag causes the framework to derive a rowcount query by simply wrapping the entire customSQL clause in a subselect, like so:    `SELECT COUNT(*) FROM ({customSQL clause here})`

However, this is not guaranteed to give good results. Because the customSQL clause can contain anything that you can write in SQL, running it inside a subselect in order to count the rows might not work, might have unintended side-effects (if, for example, it is a stored procedure call that performs updates as part of its function), or it might just be a bad idea - for example, if the customSQL query is slow-running, you'll make it twice as slow with this flag, simply because you'll be running it twice. We recommend using this flag with care.

NOTE: This setting can be overridden per-operation - see [OperationBinding.useSubselectForRowCount](OperationBinding.md#attr-operationbindingusesubselectforrowcount). You can also set a global default for this setting, so you don't have to specify it in every dataSource - define `useSubselectForRowCount` as true in your [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) file.

### Groups

- sqlPaging

**Flags**: IR

---
## Attr: DataSource.fileContentsField

### Description
The native field name used by this DataSource on the server to represent the `fileContents` for [FileSource Operations](../kb_topics/fileSource.md#kb-topic-filesource-operations).

If the fileContentsField is not configured, then a field named "fileContents" or "contents" will be used, if it exists. If not found, the longest text field which is not the [fileNameField](#attr-datasourcefilenamefield), [fileTypeField](#attr-datasourcefiletypefield) or [fileFormatField](#attr-datasourcefileformatfield) will be used.

Note that the only method which will actually return the fileContents is [getFile()](#method-datasourcegetfile) -- the other [FileSource](../kb_topics/fileSource.md#kb-topic-filesource-operations) methods omit the fileContents for the sake of efficiency.

### Groups

- fileSource

**Flags**: IR

---
## Attr: DataSource.serverType

### Description
For a DataSource stored in .xml format on the SmartClient server, indicates what server-side connector to use to execute requests, that is, what happens if you call dsRequest.execute() in server code.

### Groups

- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.dataProtocol

### Description
Controls the format in which inputs are sent to the dataURL when fulfilling DSRequests. May be overridden for individual request types using [operation bindings](OperationBinding.md#attr-operationbindingdataprotocol).

### Groups

- clientDataIntegration
- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.requestMaxRows

### Description
Applies to [SQL DataSources](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) only.

The same as [clientRequestMaxRows](#attr-datasourceclientrequestmaxrows), but applies to all requests, not just client-initiated ones. See the documentation for `clientRequestMaxRows` for details. To reiterate the warning given for that property, this is a safety limit that results in an Exception being thrown: **it is not intended to be used as a regular application facility**

To set a default `requestMaxRows` that will apply to all dataSources that do not specify the attribute, add the following to your `server.properties` file:

```
     # Fail with an error if we try to fetch more than 50000 rows in any request
     sql.clientRequestMaxRows: 50000
 
```

### See Also

- [DataSource.clientRequestMaxRows](#attr-datasourceclientrequestmaxrows)
- [DataSource.progressiveLoading](#attr-datasourceprogressiveloading)

**Flags**: IRW

---
## Attr: DataSource.skipJSONValidation

### Description
Sets what level of JSON validation will apply for this DataSource.

Note that the point of "partial" validation mode is that if the JSON ihat's delivered is correct, we'll still need to validate to get "date" and such in the correct time, but shouldn't need to for the rest.

**Flags**: IRW

---
## Attr: DataSource.preventHTTPCaching

### Description
If set, the DataSource will ensure that it never uses a cached HTTP response, even if the server marks the response as cacheable.

Note that this does not disable caching at higher levels in the framework, for example, the caching performed by [ResultSet](ResultSet.md#class-resultset).

**Flags**: IR

---
## Attr: DataSource.canMultiSort

### Description
When true, indicates that this DataSource supports multi-level sorting.

**Flags**: IR

---
## Attr: DataSource.requiresAuthentication

### Description
Whether a user must be authenticated in order to access this DataSource. This establishes a default for the DataSource as a whole; individual [DataSource.operationBindings](#attr-datasourceoperationbindings) within the DataSource may still override this setting by explicitly setting [OperationBinding.requiresAuthentication](OperationBinding.md#attr-operationbindingrequiresauthentication).

Whether the user is authenticated is determined by calling `httpServletRequest.getRemoteUser()`, hence works with both simple J2EE security (realms and form-based authentication) and JAAS (Java Authentication & Authorization Service).

If you wish to use an authentication scheme that does not make use of the servlet API's standards, SmartClient Server also implements the `setAuthenticated` method on `RPCManager`. You can use this API to tell SmartClient that all the requests in the queue currently being processed are associated with an authenticated user; in this case, SmartClient will not attempt to authenticate the user via `httpServletRequest.getRemoteUser()`

You can set the default value for this property via setting "authentication.defaultRequired" in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file). This allows you to, for example, cause all DataSources to require authentication for all operations by default.

Note that setting this property does not automatically cause an authentication mechanism to appear - you still need to separately configure an authentication system. Likewise, setting requiresAuthentication="false" does not automatically allow users to bypass your authentication mechanism - you need to set up a URL that will accept DSRequests and process them similar to the default "IDACall" servlet, and which is not protected by the authentication system. See [Deploying SmartClient](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets) for details on the IDACall servlet.

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: DataSource.logSlowFetch

### Description
Allows you to specify ["fetch" operation](../reference.md#type-dsoperationtype) SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category.

See [DataSource.logSlowSQL](#attr-datasourcelogslowsql) for more details.

**Flags**: IR

---
## Attr: DataSource.isSampleDS

### Description
Used by Reify to identify DataSources that are provided as samples. Reify will not automatically alter sample DataSource relations when removing DataSources from a project.

**Flags**: IR

---
## Attr: DataSource.translatePatternOperators

### Description
[Search operators](../reference.md#type-operatorid) like "matchesPattern" use patterns like "foo\*txt" to match text values. The patterns are similar to the patterns you use to match names of files in a command-line interface, or to the pattern allowed for the SQL "LIKE" operator.

`translatePatternOperators` controls whether these pattern operators should be translated to a nested series of "startsWith"/"endsWidth"/"contains" operators before being sent to the server. This allows a server that only implements simple operators like "startsWith" to support pattern operators such as "matchesPattern" and "containsPattern", but with caveats:

*   single-character wildcards are not supported
*   multiple wildcards are not truly order-dependent, for example \*1\*2\*3\* will match 1,2,3 as interior characters in any order.
*   may be less efficient than a direct server-side implementation that is able to translate the pattern directly to the underlying storage engine.

Note that since "containsPattern" is essentially equivalent to "matchesPattern" but with "\*" wildcards at the beginning and end of every pattern, the second limitation (pattern not really order dependent) may be fairly obvious to users when using this feature. For example, "m\*t" will match "we meet" and "we teem".

The following are examples of how patterns are translated to simpler operators. Note that the case sensitive version of the operator is referred to below, but of course "iMatchesPattern" and "iContainsPattern" will be translated to case-insensitive versions of these operators, such as "iStartsWith".

\*foo (endsWith)  
foo\* (startsWith)  
\*foo\* (contains)  
\*foo\*bar (contains and endsWith)  
foo\*bar\* (startsWith and contains)  
foo\*bar (startsWith and endsWith)  
\*foo\*bar\* (multiple contains)

Also supported: one startsWith, multiple contains, one endsWith.

**Flags**: IR

---
## Attr: DataSource.cacheSyncStrategy

### Description
The [cacheSyncStrategy](../reference_2.md#type-cachesyncstrategy) to use for operations on this DataSource. Can be overridden at the [operation](OperationBinding.md#attr-operationbindingcachesyncstrategy) and [DSRequest](DSRequest.md#attr-dsrequestcachesyncstrategy) levels.

If `cacheSyncStrategy` is not explicitly set for a `DataSource`, we will use the default strategy for this [DataSource type](#attr-datasourceservertype). The defaults as shipped, are:

| Server Type | Strategy |
|---|---|
| sql | requestValuesPlusSequences |
| hibernate | refetch |
| jpa/jpa1 | refetch |
| rest | responseValues |
| generic | refetch |

You can override these default strategies by adding a "`default.{server-type}.cache.sync.strategy`" setting to your `server.properties` file, like these examples:

```
    default.sql.cache.sync.strategy: refetch
    default.rest.cache.sync.strategy: none
 
```
Note that global `cacheSyncStrategy` settings are defaults only; SmartClient Server will override them intelligently in some circumstances. See the "CacheSyncStrategy" section of the [cache synchronization overview](../kb_topics/cacheSynchronization.md#kb-topic-automatic-cache-synchronization) for details of when and why we do this.

### Groups

- cacheSynchronization

### See Also

- [OperationBinding.cacheSyncStrategy](OperationBinding.md#attr-operationbindingcachesyncstrategy)
- [DSRequest.cacheSyncStrategy](DSRequest.md#attr-dsrequestcachesyncstrategy)

**Flags**: IR

---
## Attr: DataSource.titleField

### Description
Best field to use for a user-visible title for an individual record from this dataSource.

For example, for a DataSource of employees, a "full name" field would probably most clearly label an employee record.

If not explicitly set, the titleField is determined by looking for fields named "name", "_dataSourceId_Name", "title", "_dataSourceId_Title", "label", "_dataSourceId_Label", "id" and "_dataSourceId_Id". For example, for a DataSource with ID "customer", a field called _customerName_ would be found if there were no "name" field. Search is case insensitive, and an underscore is allowed after _dataSourceId_ (so that, for example, "CUSTOMER\_NAME" would also be found and preferred).

For purposes of this search, any trailing numerals in the DataSource ID are discarded, so a DataSource with ID "office2" will search for title fields as if the ID were just "office".

If no field is found that matches any of the names above, then the first field is designated as the titleField.

### Groups

- titles
- dsSpecialFields

**Flags**: IR

---
## Attr: DataSource.defaultUnionFieldsStrategy

### Description
Only applicable to "union" dataSources. Determines the strategy we adopt when automatically deriving a list of fields when no explicit [unionFields](#attr-datasourceunionfields) setting is provided. Note that explicit field declarations that include [unionOf](DataSourceField.md#attr-datasourcefieldunionof) definitions take precedence over whatever `defaultUnionFieldsStrategy` is defined. As an example of how this property affects field derivation, assume our unionDataSource specifies three member dataSources in its [unionOf](#attr-datasourceunionof) setting:

*   **ds1** has fields **f1 (integer)**, **f2 (text)** and **f3 (boolean)**
*   **ds2** has fields **f1 (integer)**, **f2 (text)** and **f4 (datetime)**
*   **ds3** has fields **f1 (integer)**, **f2 (float)**, **f4 (datetime)** and **f5 (text)**

Given this, the different unionFieldsStrategy settings would derive the following fields:

*   **intersect** would give just **f1** (**f2** exists on every dataSource, but the data type is not the same in every case)
*   **matching** would derive **f1** and **f4** - again, **f2** would be excluded because of the data type discrepancy. Records from **ds1** would contribute a null value for **f4**
*   **all** would derive all fields except **f2**, excluded because of the data type discrepancy. Values for missing fields from any given dataSource would be null

### Groups

- unionDataSource

### See Also

- [OperationBinding.unionFields](OperationBinding.md#attr-operationbindingunionfields)

**Flags**: IR

---
## Attr: DataSource.multiInsertBatchSize

### Description
For dataSources of [serverType](#attr-datasourceservertype) "sql" only, this property sets the multi-insert batch size for add requests on this [dataSource](#class-datasource). Only has an effect if the [add request](#method-datasourceadddata) specifies a list of records as the data, and only if [multiInsertStrategy](#attr-datasourcemultiinsertstrategy) is set to "multipleValues", either globally or at the [DSRequest](../reference.md#object-dsrequest), [OperationBinding](OperationBinding.md#class-operationbinding), or [DataSource](#class-datasource) level.

The multi-insert batch size determines the maximum number of `VALUES` clauses SmartClient Server will generate for a single `INSERT` operation. The optimum value for this setting depends on the underlying database, but typically larger batches yield better performance. if the number of records in the request exceeds the batch size, we break it up into however many batches are required. For example, if the batch size is 55 and the request contains 200 records, we would create 4 database `INSERT` operations - 3 with 55 `VALUES` clauses, and a final one with the remaining 35.

Note that this setting (along with the other multi-insert properties, [multiInsertStrategy](#attr-datasourcemultiinsertstrategy) and [multiInsertNonMatchingStrategy](#attr-datasourcemultiinsertnonmatchingstrategy)) can be overridden at the [operationBinding level](OperationBinding.md#attr-operationbindingmultiinsertbatchsize) and the [dsRequest level](DSRequest.md#attr-dsrequestmultiinsertbatchsize). If you wish to configure multi-insert setting globally, see the documentation for [multiInsertStrategy](#attr-datasourcemultiinsertstrategy).

### See Also

- [DataSource.multiInsertStrategy](#attr-datasourcemultiinsertstrategy)
- [DataSource.multiInsertNonMatchingStrategy](#attr-datasourcemultiinsertnonmatchingstrategy)

**Flags**: IRW

---
## Attr: DataSource.allowAggregation

### Description
This property indicates whether this DataSource supports aggregation/summarization and grouping of field values using the [summaryFunction](DSRequest.md#attr-dsrequestsummaryfunctions) mechanism. All the [built-in DataSource types](#attr-datasourceservertype) support aggregation by default: SQL, Hibernate and JPA DataSources support aggregation inherently, using the underlying persistence engine's query language. Other server-side implementations support aggregation and grouping as a post-fetch, in-memory operation; and because this in-memory aggregation happens after the DataSource has fetched data, and is transparent to the DataSource, it will also automatically apply to your own custom DataSource implementations without any effort, unless you switch it off (see [DataSource.suppressManualAggregation](#attr-datasourcesuppressmanualaggregation)).

[clientOnly](#attr-datasourceclientonly) DataSources also support aggregation and grouping, using a similar approach to the server-side post-fetch aggregation described above (but running on the client, obviously).

This property is intended as a means of preventing attempts to run aggregations on a given DataSource. For example, if you know that running aggregations on a particular DataSource can cause performance problems, you can set this flag false to disallow all aggregations on that DataSource. The only meaningful place to specify this property is in a DataSource descriptor (`.ds.xml` file), which will cause it to be enforced on the server. This means that if you run a fetch involving summaryFunctions at the [DSRequest](DSRequest.md#attr-dsrequestsummaryfunctions), [OperationBinding](OperationBinding.md#attr-operationbindingsummaryfunctions) or [field](DataSourceField.md#attr-datasourcefieldincludesummaryfunction) level, against a DataSource that advertises itself as `allowAggregation:false`, it will be rejected.

### See Also

- [DataSource.suppressManualAggregation](#attr-datasourcesuppressmanualaggregation)

**Flags**: IRWA

---
## Attr: DataSource.creatorOverrides

### Description
Indicates that declarative security rules are waived for rows that were created by the current user. Practically, this means that when a security check fails, instead of a security exception being thrown, we alter the criteria to ensure that the request can only return or affect rows that were created by the current authenticated user. This allows you to create security regimes whereby users can see and edit data they created, but have access to other users' data forbidden or limited.

In order for this to work, we require two things:

*   The DataSource must specify a field of type "creator" - this field type is described on [this page](../reference_2.md#type-fieldtype)
*   The authentication regime in use must include the idea of a "current user". The authentication provided by the Servlet API is an example of such a regime.

This setting can be overridden at operationBinding and field level, allowing extremely fine-grained control.

### Groups

- fieldLevelAuth
- declarativeSecurity

### See Also

- [OperationBinding.creatorOverrides](OperationBinding.md#attr-operationbindingcreatoroverrides)
- [DataSourceField.creatorOverrides](DataSourceField.md#attr-datasourcefieldcreatoroverrides)

**Flags**: IR

---
## Attr: DataSource.resultSetClass

### Description
Class for ResultSets used by this datasource. If null, defaults to using [ResultSet](ResultSet.md#class-resultset).

This can be set to a custom subclass of ResultSet that, for example, hangs onto to extra information necessary for integration with web services.

**Flags**: IRA

---
## Attr: DataSource.logSlowSQL

### Description
Allows you to specify SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category.

This setting applies to all SQL queries, unless more specific thresholds are set using [DataSource.logSlowFetch](#attr-datasourcelogslowfetch), [DataSource.logSlowAdd](#attr-datasourcelogslowadd), [DataSource.logSlowUpdate](#attr-datasourcelogslowupdate), [DataSource.logSlowRemove](#attr-datasourcelogslowremove), [DataSource.logSlowCustom](#attr-datasourcelogslowcustom) or even more specific affecting just the operationBinding it is configured in your DS XML as operationBinding.logSlowSQL.

If none of the thresholds above are set, global _sql.log.queriesSlowerThan_ [server.properties SQL setting](../kb_topics/sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties) will be used.

For the details on how to setup the logging part see the [Special logging category: com.isomorphic.SLOW\_SQL](../kb_topics/serverLogging.md#kb-topic-server-logging)

**Flags**: IR

---
## Attr: DataSource.ownerIdNullAccess

### Description
If [ownerIdField](#attr-datasourceowneridfield) is in force, specifies the access that is allowed to records with a null `ownerIdField`. This property has no effect if `ownerIdField` is not specified.

This property can be used in conjunction with [DataSource.ownerIdNullRole](#attr-datasourceowneridnullrole) to create the concept of shared, or public, records. For example, if you set `ownerIdNullRole` to "administrator", any users with the "administrator" role will be allowed to write records with a null `ownerIdField`. If you also set `ownerIdNullAccess` to "view", all those records with a null owner will be viewable by all, in addition to their own records. We use this functionality with the [Saved Searches feature](SavedSearches.md#class-savedsearches), to enable precisely this: users can save their own searches, which are private to them, but administrators can also save searches with a null `ownerIdField`, which become standard, shared searches that appear to all users, in addition to their own private searches.

### See Also

- [DataSource.ownerIdField](#attr-datasourceowneridfield)
- [DataSource.ownerIdNullRole](#attr-datasourceowneridnullrole)

**Flags**: IR

---
## Attr: DataSource.iconField

### Description
Designates a field of [type](../reference_2.md#type-fieldtype):"image" as the field to use when rendering a record as an image, for example, in a [TileGrid](TileGrid.md#class-tilegrid).

For example, for a DataSource of employees, a "photo" field of type "image" should be designated as the iconField.

If not explicitly set, iconField looks for fields named "picture", "thumbnail", "icon", "image" and "img", in that order, and will use any of these fields as the iconField if it exists and has type "image".

To avoid any field being used as the iconField, set iconField to `null`.

### Groups

- dsSpecialFields

**Flags**: IR

---
## Attr: DataSource.useHttpProxy

### Description
Like [OperationBinding.useHttpProxy](OperationBinding.md#attr-operationbindingusehttpproxy), but serves as a default for this DataSource that may be overridden by individual operationBindings.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.forceSort

### Description
For DataSources of [serverType](#attr-datasourceservertype) "sql" only, indicates whether we should automatically add a sort field for [paged fetches](ResultSet.md#attr-resultsetfetchmode) on this DataSource. If left unset, this property defaults to the one of the global values described in the [defaultSortField](#attr-datasourcedefaultsortfield) documentation. Also note, this property can be overridden [per-operationBinding](OperationBinding.md#attr-operationbindingforcesort).

Note, the ability to set this property per-DataSource is only provided to allow for complete configurability in unusual cases. See the `defaultSortField` docs for details of why use of this property should be considered a red flag.

### Groups

- serverDataIntegration

**Flags**: IRA

---
## Attr: DataSource.addedAuditFields

### Description
The list of extra manually managed fields that will be added to the [DataSource.fields](#attr-datasourcefields) of the [Audit DataSource](#attr-datasourceaudit).

This feature enables the storage of additional information in the `Audit DataSource` alongside the standard audit data. In order to do that the audited DataSource needs to declare [DataSource.auditDSConstructor](#attr-datasourceauditdsconstructor) referring custom [DataSource.serverConstructor](#attr-datasourceserverconstructor), so that all requests to add data to the Audit DataSource could be intercepted allowing to make changes to the new records (obtained using `DSRequest.getValues()` server-side API). In this particular use case values for the `addedAuditFields` need to be provided.

Example of an audited DataSource (schematically):

```
 <DataSource audit="true" auditDSConstructor="package.AuditDS">
 <fields>....</fields>
 <addedAuditFields>
      <addedAuditField name="altitude" type="float" />
      <addedAuditField name="longitude" type="float" />
      <addedAuditField name="logCorrelationId" type="text" />
 </addedAuditFields>
 </DataSource>
 
```
An example implementation of AuditDS could be as follows:
```
 public class AuditDS extends SQLDataSource {
     public DSResponse executeAdd(DSRequest req) throws Exception {
         // populate additional fields
         Map values = req.getValues();
         values.put("altitude", 54.685);
         values.put("longitude", 25.286);
         values.put("logCorrelationId", "foobar");
         // execute "add" request
         return super.executeAdd(req);
     }
 }
 
```

### Groups

- fields

### See Also

- [DataSourceField](../reference_2.md#object-datasourcefield)

**Flags**: IR

---
## Attr: DataSource.fields

### Description
The list of fields that compose records from this DataSource.

Each DataSource field can have type, user-visible title, validators, and other metadata attached.

After a DataSource has been [created](Class.md#classmethod-classcreate), access the list of fields via [DataSource.getFieldNames](#method-datasourcegetfieldnames) and access individual fields via [DataSource.getField](#method-datasourcegetfield).

### Groups

- fields

### See Also

- [DataSourceField](../reference_2.md#object-datasourcefield)

**Flags**: IR

---
## Attr: DataSource.ownerIdNullRole

### Description
If [ownerIdField](#attr-datasourceowneridfield) is in force, specifies a role that will allow the `ownerIdField` to take a null value. Any user that has that role is allowed to create client-initiated "add" and "update" operations that specify a null value for the `ownerIdField`, and the system will persist the null value rather than forcing in the currently authenticated user's user id as it normally would. If any client-initiated "add" or "update" request specifies _any_ non-null value for the `ownerIdField`, the normal behavior of the system will reassert and the current user's user id will be forced into the `ownerIdField`. This allows authorised users (ie, those with the necessary role) to choose between saving public or private records, just by sending a null or non-null value for the `ownerIdField`.

This property has no effect if `ownerIdField` is not specified.

This property can be used in conjunction with [DataSource.ownerIdNullAccess](#attr-datasourceowneridnullaccess) to create the concept of shared, or public, records - see that property's documentation for an example.

### See Also

- [DataSource.ownerIdField](#attr-datasourceowneridfield)
- [DataSource.ownerIdNullAccess](#attr-datasourceowneridnullaccess)

**Flags**: IR

---
## Attr: DataSource.endGap

### Description
If we are [loading progressively](#attr-datasourceprogressiveloading), indicates the number of extra records SmartClient Server will advertise as being available, if it detects that there are more records to view (see [lookAhead](#attr-datasourcelookahead)). This property has no effect if we are not progressive-loading.

Note that when viewing DataSource data in a ListGrid, it is not recommended to have the endGap be larger than the [ResultSet.resultSize](ResultSet.md#attr-resultsetresultsize). This can result in a situation where the entire range requested by the ResultSet is beyond the true end of the data set, with unpredictable results.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](#attr-datasourceprogressiveloading)
- [DataSource.lookAhead](#attr-datasourcelookahead)

**Flags**: IRW

---
## Attr: DataSource.omitNullDefaultsOnAdd

### Description
When true, and [noNullUpdates](#attr-datasourcenonullupdates) is also true, indicates that "add" requests on this DataSource will have null-valued fields removed from the request entirely before it is sent to the server, as opposed to the default behavior of replacing such null values with defaults.

### See Also

- [DataSource.noNullUpdates](#attr-datasourcenonullupdates)

**Flags**: IR

---
## Attr: DataSource.nullStringValue

### Description
If [DataSource.noNullUpdates](#attr-datasourcenonullupdates) is set, the value to use for any text field that has a null value assigned on an update operation, and does not specify an explicit [nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue).

### See Also

- [DataSource.noNullUpdates](#attr-datasourcenonullupdates)
- [DataSourceField.nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue)

**Flags**: IR

---
## Attr: DataSource.useOfflineStorage

### Description
Whether we store server responses for this DataSource into [browser-based offline storage](Offline.md#class-offline), and then use those stored responses at a later time if we are offline (ie, the application cannot connect to the server). Note that by default we do NOT use offline storage for a dataSource.

### Groups

- offlineGroup

**Flags**: IRW

---
## Attr: DataSource.projectFileKey

### Description
For DataSources with type [`projectFile`](../reference_2.md#type-dsservertype), looks up the locations to use as [projectFileLocations](#attr-datasourceprojectfilelocations) from the project's configuration (i.e. project.properties, [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) etc.).

For instance, to look up the value of project.datasources and use it for `projectFileLocations`, use "datasources" as the `projectFileKey`.

If you specify both `projectFileKey` and `projectFileLocations`, then both with be used, with the `projectFileLocations` applied last.

### Groups

- fileSource

### See Also

- [DataSource.projectFileLocations](#attr-datasourceprojectfilelocations)

**Flags**: IR

---
## Attr: DataSource.logSlowUpdate

### Description
Allows you to specify ["update" operation](../reference.md#type-dsoperationtype) SQL query execution time threshold in milliseconds, which if exceeded query is identified as "slow" and may be logged under specific logging category.

See [DataSource.logSlowSQL](#attr-datasourcelogslowsql) for more details.

**Flags**: IR

---
## Attr: DataSource.sampleData

### Description
An optional array of sample data records. These may be actual records from the data source or artificial data that is representative of records from the data source.

AI may be provided this sample data when AI is asked to work with the data source, to give it a better idea of what the data in the data source "looks like".

When defining the data source in a .ds.xml file (see [dataSourceDeclaration](../kb_topics/dataSourceDeclaration.md#kb-topic-creating-datasources)), it will likely be helpful to use the XMLSchema-Instance `type` attribute to be able to change the value type from the default (string) to boolean, int, float, date, etc. For example:

```
 <sampleData xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   <country>
     <continent>North America</continent>
     <countryName>United States</countryName>
     <countryCode>US</countryCode>
     <area xsi:type="float">9372610</area>
     <population xsi:type="int">266476278</population>
     <gdp xsi:type="float">7247700</gdp>
     <independence xsi:type="date">1776-07-04</independence>
     <government>federal republic</government>
     <capital>Washington</capital>
     <member_g8 xsi:type="boolean">true</member_g8>
   </country>
 ...
 
```

### See Also

- [DataSource.description](#attr-datasourcedescription)
- [DataSourceField.description](DataSourceField.md#attr-datasourcefielddescription)

**Flags**: IRW

---
## Attr: DataSource.useSpringTransaction

### Description
This flag is part of the Automatic Transactions feature; it is only applicable in Power Edition and above.

If true, causes all transactional operations on this DataSource to use the current Spring-managed transaction, if one exists. If there is no current Spring transaction to use at the time of execution, a server-side Exception is thrown. Note, a "transactional operation" is one that would have joined the SmartClient shared transaction in the absence of Spring integration - see [auotJoinTransactions](#attr-datasourceautojointransactions).

This feature is primarily intended for situations where you have [DMI methods](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) that make use of both Spring DAO operations and SmartClient DSRequest operations, and you would like all of them to share the same transaction. An example of the primary intended use case:

```
   @Transactional(isolation=Isolation.READ_COMMITTED, propagation=Propagation.REQUIRED)
   public class WorldService {

     public DSResponse doSomeStuff(DSRequest dsReq, HttpServletRequest servletReq) 
     throws Exception 
     {
     	 ApplicationContext ac = (ApplicationContext)servletReq.getSession().getServletContext().getAttribute("applicationContext");
       WorldDao dao = (WorldDao)ac.getBean("worldDao");
       dao.insert(req.getValues());
       DSRequest other = new DSRequest("MyOtherDataSource", "add");
       // Set up the 'other' dsRequest with critiera, values, etc
       //  ...

       // This dsRequest execution will use the same transaction that the DAO operation
       // above used; if it fails, the DAO operation will be rolled back
       other.execute();

       return new DSResponse();
     }
   }
```
Note: if you want to rollback an integrated Spring-managed transaction, you can use any of the normal Spring methods for transaction rollback:

*   Programmatically mark the transaction for rollback with the `setRollbackOnly()` API
*   Throw a `RuntimeException`, or
*   Throw an ordinary checked `Exception`. but configure Spring to rollback on that Exception. This can be done in the @Transactional annotation:
    ```
         @Transactional(isolation=Isolation.READ_COMMITTED, propagation=Propagation.REQUIRED, rollbackFor=MyRollbackException.class)
    ```
    

Spring's exception-handling model is different from SmartClient's, so care must be taken to get the correct error processing. If a transactional DSRequest fails, SmartClient code will throw an ordinary checked `Exception`; but Spring will ignore that `Exception`. So you can either:

*   Wrap every `DSRequest.execute()` in a try/catch block. Catch `Exception` and throw a `RuntimeException` instead
*   Just use the "rollbackFor" annotation to make your transactional method rollback for all instances of `Exception`

  
Note: Spring transaction integration is conceptually different from SmartClient's [built-in transaction feature](#attr-datasourceautojointransactions), because SmartClient transactions apply to a queue of DSRequests, whereas Spring transactions are scoped to a single method invocation. If you want to make a whole SmartClient queue share a single Spring-managed transaction, you can wrap the processing of an entire queue in a call to a transactional Spring method. See the _Using Spring Transactions with SmartClient DMI_ section at the bottom of the [Spring integration page](../kb_topics/springIntegration.md#kb-topic-integration-with-spring) for more details.

You can set `useSpringTransaction` as the default setting for all dataSources for a given database provider by adding the property `{dbName}.useSpringTransaction` to your `server.properties` file. For example, `Mysql.useSpringTransaction: true` or `hibernate.useSpringTransaction: true`. You can set it as the default for all providers with a `server.properties` setting like this: `useSpringTransaction: true`. When `useSpringTransaction` is the default, you can switch it off for a specific dataSource by explicitly setting the flag to false for that DataSource.

Finally, this setting can be overridden at the operationBinding level - see [OperationBinding.useSpringTransaction](OperationBinding.md#attr-operationbindingusespringtransaction)

#### Configuration
When using Spring transactions, SmartClient needs a way to lookup the JNDI connection being used by Spring, and this needs to be configured. First, register a bean like this in your applicationContext.xml file:
```
   <bean id="dataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
       <!-- Set this to the JNDI name Spring is using -->
       <property name="jndiName" value="isomorphic/jdbc/defaultDatabase"/>
   </bean>
 
```
and then add a line like this to your server.properties:
```
   # Set this property to match the "id" of the JndiObjectFactoryBean registered in Spring
   sql.spring.jdbcDataSourceBean: dataSource
 
```

### See Also

- [DataSource.autoJoinTransactions](#attr-datasourceautojointransactions)
- [OperationBinding.useSpringTransaction](OperationBinding.md#attr-operationbindingusespringtransaction)
- [springIntegration](../kb_topics/springIntegration.md#kb-topic-integration-with-spring)

**Flags**: IR

---
## Attr: DataSource.transformResponseScript

### Description
A scriptlet to be executed on the server after running any operation on this dataSource. The intention is that this scriptlet transforms the response data in some way. It is provided to allow complex, programmatic transformations without having to handle the operation in a [DMI](DMI.md#class-dmi) or [handler script](#attr-datasourcescript). To avoid confusion, it should be noted that, in many cases, you could instead write response transformation logic in a [script](#attr-datasourcescript) that first invokes execute() on the DSRequest to run the default behavior. The advantage of `transformResponseScript` is that it allows you partition any script logic appropriately, and is more self-documenting.

If [OperationBinding.transformResponseScript](OperationBinding.md#attr-operationbindingtransformresponsescript) is also specified, it will be executed for the operation binding in question _in addition to_ and _after_ the DataSource-level script.

All of the variables available in a normal [script](#attr-datasourcescript) are available to a `transformResponseScript`, but the framework also provides somes additional variables useful in the specific context of transforming response data:

*   **dsResponse**The actual `DSResponse` object
*   **responseObjects** is the response data as a list of objects, either Maps or Javabeans, depending on what data model you are using - see [beanClassName](#attr-datasourcebeanclassname). If the underlying response data is actually a single object, this is just that single object wrapped in a List
*   **responseObject** is the response data as a single object. If the underlying response data is not a single object - ie, it is a list of objects - this will just be the first item in the list

Normally, `responseObjects` are "live". This means that any changes you make to them in your script will affect the underlying objects in the response data and be seen in downstream processing. This means that your script can modify things in place and does not need to return a value; this is the recommended approach.

If your script _does_ return a value, we will assign that value as the response data on return from the script.

**Warning:** It is advisable to explicitly return null if you do not wish to return a value. See the section "Returning values and JavaScript", which also applies to Groovy and some other JSR223 languages, in the [server scripting overview](../kb_topics/serverScript.md#kb-topic-server-scripting).

Note, if you prefer a Java solution rather than placing scripts in your `.ds.xml` files, you can instead extend the Java `BasicDataSource` class and override its `transformResponse()` method. If you both override the Java method and provide a `transformResponseScript`, the Java method runs first and any transformations it makes will be visible to the script. See [serverConstructor](#attr-datasourceserverconstructor) for details of how to use a custom class to implement a DataSource server-side.

### Groups

- serverScript

### See Also

- [DataSource.script](#attr-datasourcescript)
- [DataSource.transformRequestScript](#attr-datasourcetransformrequestscript)
- [OperationBinding.transformResponseScript](OperationBinding.md#attr-operationbindingtransformresponsescript)
- [DataSourceField.fieldValueScript](DataSourceField.md#attr-datasourcefieldfieldvaluescript)

**Flags**: IR

---
## Attr: DataSource.transformRequestScript

### Description
A scriptlet to be executed on the server prior to running any operation on this dataSource. The intention is that this scriptlet transforms the DSRequest in some way - probably its [criteria](DSRequest.md#attr-dsrequestdata) and/or [values](DSRequest.md#attr-dsrequestdata), but maybe something less obvious, such as adding to its templateContext Map - prior to running the operation proper. It is provided to allow more complex, programmatic transformations than is possible with declarative [DSRequestModifier](../reference.md#object-dsrequestmodifier)s, without having to handle the operation in a [DMI](DMI.md#class-dmi) or [handler script](#attr-datasourcescript). To avoid confusion, it should be noted that, in many cases, you could instead write request transformation logic in a [script](#attr-datasourcescript) and then have that script invoke execute() on the DSRequest to proceed with default behavior. The advantage of `transformRequestScript` is that it allows you partition any script logic appropriately, and is more self-documenting.

If [OperationBinding.transformRequestScript](OperationBinding.md#attr-operationbindingtransformrequestscript) is also specified, it will be executed for the operation binding in question _in addtion to_ and _after_ the DataSource-level script.

All of the variables available in a normal [script](#attr-datasourcescript) are available to a `transformRequestScript`, including the three you are most likely to use: `dsRequest`, `criteria` and `values`. All three of these variables are "live" - any changes you make to them will affect the underlying object and be seen in downstream processing. This means that your script can modify things in place and does not need to return a value; this is the recommended approach.

If your script _does_ return a value, we will assign that value to criteria for a fetch or remove operation, and to values for an add or update operation. This may well be what you want, but it may not - this is why we recommend modifying in place and not returning a value.

**Warning:** It is advisable to explicitly return null if you do not wish to return a value. See the section "Returning values and JavaScript", which also applies to Groovy and some other JSR223 languages, in the [server scripting overview](../kb_topics/serverScript.md#kb-topic-server-scripting).

### Groups

- serverScript

### See Also

- [DataSource.script](#attr-datasourcescript)
- [DataSource.transformResponseScript](#attr-datasourcetransformresponsescript)
- [OperationBinding.transformRequestScript](OperationBinding.md#attr-operationbindingtransformrequestscript)

**Flags**: IR

---
## Attr: DataSource.cacheAcrossOperationIds

### Description
When [cacheAllData](#attr-datasourcecachealldata) mode is enabled and a [DataSource.cacheAllOperationId](#attr-datasourcecachealloperationid) has been set, this flag affects whether cached results are used for all "fetch" requests regardless of their [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid), or are used only for "fetch" requests that use the `cacheAllOperationId`, allowing other requests to go to server normally.

Default of `true` means that the `cacheAllOperationId` will be used to fetch all rows, but the resulting cache will be used for all "fetch" operations regardless of the `operationId` specified on the request.

Switching to "false" effectively creates caching just for one specific `operationId` - the `cacheAllOperationId` - while allowing all other requests to go to the server normally.

### Groups

- clientData

**Flags**: IR

---
## Attr: DataSource.defaultBooleanStorageStrategy

### Description
For [serverType:"sql"](#attr-datasourceservertype) DataSources, sets the default [sqlStorageStrategy](DataSourceField.md#attr-datasourcefieldsqlstoragestrategy) to use for boolean fields where no `sqlStorageStrategy` has been declared on the field.

Can also be set system-wide via the [server_properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) setting `sql.defaultBooleanStorageStrategy`, or for a particular database configuration by setting `sql._dbName_.defaultBooleanStorageStrategy` (see [Admin Console overview](../kb_topics/adminConsole.md#kb-topic-admin-console) for more information on SQL configuration).

Note that when this property is unset, the default [DataSourceField.sqlStorageStrategy](DataSourceField.md#attr-datasourcefieldsqlstoragestrategy) strategy is effectively "string".

### Groups

- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.defaultMultiUpdatePolicy

### Description
Controls when primary keys are required for "update" and "remove" server operations, when allowMultiUpdate has not been explicitly configured on either the [operationBinding.allowMultiUpdate](OperationBinding.md#attr-operationbindingallowmultiupdate) or via the server-side API `DSRequest.setAllowMultiUpdate()`.

Default value of null means this DataSource will use the system-wide default, which is set via `datasources.defaultMultiUpdatePolicy` in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file), and defaults to not allowing multi updates for requests associated with an RPCManager, see [MultiUpdatePolicy](../reference.md#type-multiupdatepolicy) for details.

### See Also

- [OperationBinding.allowMultiUpdate](OperationBinding.md#attr-operationbindingallowmultiupdate)

**Flags**: IR

---
## Attr: DataSource.sqlSuffix

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For DataSources of [serverType](#attr-datasourceservertype) "sql" only, some text to add right at the end of any generated query, after all other text. See the documentation for the [operationBinding level](OperationBinding.md#attr-operationbindingsqlsuffix) property for more detail.

### Groups

- customQuerying

**Flags**: IR

---
## Attr: DataSource.useParentFieldOrder

### Description
For a DataSource that inherits [DataSource.fields](#attr-datasourcefields) from another DataSource (via [DataSource.inheritsFrom](#attr-datasourceinheritsfrom)), indicates that the parent's field order should be used instead of the order of the fields as declared in this DataSource. New fields, if any, are placed at the end.

### Groups

- fields

**Flags**: IR

---
## Attr: DataSource.idClassName

### Description
For JPA and Hibernate DataSources this property indicates, that data source has composite primary key and specifies fully-qualified Java class:

*   with **`@EmbeddedId`** you have to specify class name of declared id
*   with **`@IdClass`** you have to specify class specified in annotation declaration

### Groups

- fields

**Flags**: IR

---
## Attr: DataSource.auditChangedFieldsFieldName

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), specifies the field name used to store the names of the fields which were updated. If empty string is specified as the field name, the audit DataSource will not store this field.

Note that this field will only be set for [update](../reference.md#type-dsoperationtype) operations.

**Flags**: IR

---
## Attr: DataSource.patternEscapeChar

### Description
When using the [pattern operators](../kb_topics/patternOperators.md#kb-topic-patternoperators) [search operator](../reference.md#type-operatorid), character that escapes the [DataSource.patternSingleWildcard](#attr-datasourcepatternsinglewildcard) or [DataSource.patternMultiWildcard](#attr-datasourcepatternmultiwildcard) if placed before it, so that it is treated as a literal character.

**Flags**: IR

---
## Attr: DataSource.deepCloneOnEdit

### Description
Before we start editing values in [DataBoundComponent](../reference.md#interface-databoundcomponent)s bound to this dataSource, should we perform a deep clone of the underlying values (a "deep clone" is one created by traversing the original values object recursively, cloning the contents of nested objects and arrays). If this flag is explicitly set to false, we perform a shallow clone of the underlying values before edit (a "shallow clone" is a copy created by simply copying the top-level attributes of an object). Note, this setting only affects deep-cloning of attributes that are bound to a field; for other, non-field values, see [DataSource.deepCloneNonFieldValuesOnEdit](#attr-datasourcedeepclonenonfieldvaluesonedit).

If this flag is not explicitly set, it defaults to the value of the same-named static property, [DataSource.deepCloneOnEdit](#classattr-datasourcedeepcloneonedit). This flag can also be overridden per-component and per-field - see [DataBoundComponent.deepCloneOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepcloneonedit) and [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit).

Note, this flag only has an effect if you are editing a values object that contains nested objects or arrays, using [dataPath](Canvas.md#attr-canvasdatapath)s. When editing "flat" data - the mainstream case - there is no difference between a deep clone and a shallow clone.

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [FormItem.dataPath](FormItem.md#attr-formitemdatapath)
- [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit)
- [DataBoundComponent.deepCloneOnEdit](DataBoundComponent.md#attr-databoundcomponentdeepcloneonedit)
- [ValuesManager.deepCloneOnEdit](ValuesManager.md#attr-valuesmanagerdeepcloneonedit)

**Flags**: IRWA

---
## Attr: DataSource.defaultSortField

### Description
For DataSources of [serverType](#attr-datasourceservertype) "sql" only, the name of a field to include in the `ORDER BY` clause as a means of enforcing a stable sort order, _for [paged fetches](ResultSet.md#attr-resultsetfetchmode) only_. This property has no effect for non-SQL dataSources, or for non-paged fetches.

Generally speaking, databases make no guarantee about the order of rows in a resultset unless an `ORDER BY` clause was provided. This is not usually a problem if you actually don't care about the row order, but there is a catch if you are using paged fetching: because the pages are fetched using completely different queries, the database is at liberty to use different orderings from one fetch to another, and in some cases, with some databases, that is what actually happens. This leads to broken paging behavior, with some records duplicated and others omitted.

Note that it is unusual for a database to change strategies between queries like this; generally speaking, rows are ordered in some kind of natural ordering in the absence of an explicit order - typically insertion order, or by primary key value. However, it does happen, and is more likely with some database products than others.

This property only has an effect if `forceSort` is in effect for the fetch operation. See below for DataSource- and operation-level options, but ordinarily this is arranged by setting the `forceSort` property for the current database configuration in your `server.properties` file:

```
   # Given this database definition
   sql.MyDB.database.type: mysql

   # Either of these settings will enable automatic sorting
   sql.MyDB.forceSort: true
   # Or
   sql.mysql.forceSort: true
 
```
Note, the `defaultSortField` should ideally provide a unique ordering: so for an employee table, payroll number would be preferable to employee name. A non-unique ordering will usually be sufficient to ensure stablity of ordering from one query to the next, because it will usually ensure that the database is forced to use the same index in each case. However, the database may still choose to order rows differently within the confines of the non-unique ordering, so only a unique ordering is guaranteed to ensure stability.

Fields of [type](../reference_2.md#type-fieldtype) `creatorTimestamp` are also good candidates for this purpose - assuming you have a suitable index in place, and assuming sorting by temporal values does not introduce performance problems with your database of choice - as they are often unique or near-to-unique, and they reflect the insertion order, which is the "natural ordering" in some (not all) databases.

Note that this automatic sorting does not interfere with the ordinary sorting that your application may do: it is applied _in addition to_ any application sort order. So if your application imposes no [sort order](ListGrid_2.md#method-listgridsetsort), the resultset will be sorted by the `defaultSortField`; if your application requests a sort order of, eg, "state" then "city", the resultset will be ordered by "state", then "city", and then the `defaultSortField`

If `forceSort` is enabled and you do not provide a `defaultSortField` for a given database, SmartClient will instead use the [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) field(s). If the dataSource does not define a `primaryKey`, we will just use the dataSource's first defined field. **Recommendation**: Unless you have a reason to explicitly declare a `defaultSortField`, we recommend that you leave it undefined for any DataSource that declares a `primaryKey` (and we recommend that all dataSources declare a `primaryKey`). The `primaryKey` field is usually the ideal candidate for this purpose, because it is unique and almost certainly indexed.

Note that `forceSort` is enabled by default for PostgreSQL, because this product is known to be less likely to retain a stable sort order between two similar, unordered queries.

#### DataSource- and OperationBinding-level forceSort flag
As well as the above-mentioned global settings, it is possible to configure automatic sorting behavior for paged fetches at both the individual [DataSource level](#attr-datasourceforcesort) and [operationBinding level](OperationBinding.md#attr-operationbindingforcesort). However, this facility is only provided to allow complete configurability in unusual cases. Generally speaking, if a database requires ordering for correct behavior with paged fetches, it _always_ requires ordering for correct behavior with paged fetches; you can't ordinarily pick and choose which tables or which individual fetches need to be ordered.

That said, there may be real world cases where a database that normally requires ordering for correct behavior, nevertheless has individual cases where that is not required - maybe on tables that have only a single index, or in cases where there are no joins involved, or maybe in other circumstances related to how that specific database product works internally. Or again, there may be unusual individual cases where a database that ordinarily works fine for paged fetches without requiring ordering, needs to apply an ordering.

We provide the DataSource- and operation-level `forceSort` flags to allow you to work around or take advantage of these database-specific quirks. However, use of them should be considered a red flag because they might cause problems if things change in the future (new database release, change in the underlying query, addition of a foreignKey relation at the database level, etc).

### Groups

- serverDataIntegration

**Flags**: IRA

---
## Attr: DataSource.autoDeriveSchema

### Description
This property allows you to specify that your DataSource's schema (field definitions) should be automatically derived from some kind of metadata. This causes SmartClient to create a special super-DataSource, which is used purely as a source of default schema for this DataSource; this is arranged by causing the autoDerived DataSource to automatically [inherit from](#attr-datasourceinheritsfrom) the special super-DataSource. This allows you to auto-derive schema from existing metadata, whilst still being able to override any or all of it as required. By default additional derived field definitions are placed at the end, but that can be changed by [DataSource.useParentFieldOrder](#attr-datasourceuseparentfieldorder) flag. Also, derived field definitions may be hidden using [DataSource.showLocalFieldsOnly](#attr-datasourceshowlocalfieldsonly).

This property has a different implementation depending upon the [serverType](#attr-datasourceservertype) of the DataSource:

*   For a DataSource with serverType: "sql", automatically derive the dataSource's schema from the Spring bean or Java class specified in [schemaBean](#attr-datasourceschemabean). If `schemaBean` is not specified, derive the schema from the columns in the SQL table specified in [tableName](#attr-datasourcetablename). More information on SQL DataSources is [here](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources)
*   For a DataSource with serverType: "hibernate", automatically derive the dataSource's schema from the Spring bean, Hibernate mapping or Java class named in the [schemaBean](#attr-datasourceschemabean) property. If no such thing exists, derive the schema from the Hibernate mapping or Java class specified in the [beanClassName](#attr-datasourcebeanclassname) property (this allows you to specify schema and mapping separately, in the unusual circumstance that you have a need to do so). Note that the "mappings" referred to here can mean either `.hbm.xml` files or annotated classes; both are supported. If neither of these is successful, derive the schema from the underlying SQL table specified in [tableName](#attr-datasourcetablename). More information on Hibernate DataSources is [here](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate)
*   For a DataSource with serverType: "jpa1" or "jpa", automatically derive the dataSource's schema from the annotated JPA class named in the [schemaBean](#attr-datasourceschemabean) property. If the schemaBean property is not defined, derive the schema from the annotated JPA class named in the [beanClassName](#attr-datasourcebeanclassname) property (as with Hibernate, this allows you to specify schema and mapping separately if you need to do so). JPA DataSource generation relies on annotations (the orm.xml mapping file is not supported). More information on JPA DataSources is [here](../kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa)
*   For other DataSource types, attempt to find a Spring bean with the name specified in the [schemaBean](#attr-datasourceschemabean) property. If no such bean is found (or Spring is not present), attempt to instantiate an object whose fully-qualified class name is the value in the `schemaBean` property. If one of these approaches succeeds, we derive the schema from the discovered object (by treating it as a Java Bean and assuming that each one of its getters corresponds to a like-named field in the DataSource). More information on custom DataSource implementations is [here](../kb_topics/writeCustomDataSource.md#kb-topic-custom-server-datasources).

Note that when dataSource schema is derived by introspecting the Java class or Spring bean the derived fields are sorted alphabetically, but with [primary key](DataSourceField.md#attr-datasourcefieldprimarykey) fields at the top.
#### Field types
The following table shows how SQL types are derived into [DataSource types](../reference_2.md#type-fieldtype) when we use an SQL table as a source of metadata for a SQL or Hibernate DataSource:

| SQL type | [DataSource type](DataSourceField.md#attr-datasourcefieldtype) |
|---|---|
| CHAR, VARCHAR, LONGVARCHAR, TEXT, CLOB | text |
| BIT, TINYINT, SMALLINT, INTEGER, BIGINT, DECIMAL*, NUMBER** | integer |
| REAL, FLOAT, DOUBLE, DECIMAL*, NUMBER** | float |
| DATE | date |
| TIME | time |
| TIMESTAMP | datetime |
| BLOB, BINARY, VARBINARY, LONGVARBINARY | binary |

\*For DECIMAL types, we inspect the "DECIMAL\_DIGITS" attribute of the JDBC metadata and designate the field type "integer" if that attribute is 0, or "float" if it is some other value.  
\*\*NUMBER is an Oracle-only type that appears in the JDBC metadata as DECIMAL and is handled exactly the same way as DECIMAL

The following table shows how Java types are derived into DataSource types when we use an unannotated Java class (Spring bean, Hibernate mapping or POJO) as a source of metadata for a SQL, Hibernate or custom DataSource:

| Java type | [DataSource type](DataSourceField.md#attr-datasourcefieldtype) |
|---|---|
| boolean, Boolean | boolean |
| char, Character, String, Reader | text |
| byte, short, int, long, Byte, Short, Integer, Long, BigInteger | integer |
| float, double, Float, Double, BigDecimal | float |
| Enum | enum (see discussion below) |
| InputStream | binary |
| java.sql.Date, java.util.Date, java.util.Calendar | date |
| java.sql.Time | time |
| java.sql.Timestamp | datetime |

Finally, this table shows how Java types are derived into DataSource types when we use an annotated class as a source of metadata. Note annotated classes are necessary for JPA DataSources, but you can choose to use them for other types of DataSource as well. For Hibernate DataSources, this is very worthwhile because Hibernate will also make use of the annotations as config, meaning you don't need to specify `.hbm.xml` files. For SQL and custom DataSources, there is no benefit at the persistence level, but it may still be worthwhile because the use of an annotated class gives us better metadata and allows us to generate a better, closer-fitting autoDerive DataSource than we can from examination of SQL schema or plain Java Beans:

| Java type | [DataSource type](DataSourceField.md#attr-datasourcefieldtype) |
|---|---|
| boolean, Boolean | boolean |
| char, Character, String, Reader | text |
| byte, short, int, long, Byte, Short, Integer, Long, BigInteger | integer |
| float, double, Float, Double, BigDecimal | float |
| InputStream | binary |
| java.util.Date (with Temporal set to DATE), java.sql.Date | date |
| java.util.Date (with Temporal set to TIME), java.sql.Time | time |
| java.util.Date (with Temporal set to TIMESTAMP), java.util.Calendar, java.sql.Timestamp | datetime |
| Enum (with Enumerated set to STRING) | enum (see discussion below) |
| Enum (with Enumerated set to ORDINAL) | intEnum (see discussion below) |
| Field with Lob annotation | binary |
| Field with GeneratedValue annotation | sequence, if the field is an integer type (see discussion below) |

#### Primary keys, sequences and identity columns
We attempt to derive information about primary keys from the metadata we have.

If the metadata source is an SQL table:

*   If the table does not have a native primary key constraint, no attempt is made to identify primary key fields. Otherwise:
*   The column or columns that make up the table's native primary key constraint are identified using the JDBC `DatabaseMetaData.getPrimaryKeys()` API
*   Each DataSource field that corresponds to one of these native primary key columns is marked `primaryKey: true`
*   For each of these columns, the metadata returned by `DatabaseMetaData.getColumns()` is inspected. If the metadata includes `IS_AUTOINCREMENT=YES`, we mark the corresponding field as `type="sequence"`. This information should be reliably provided by databases that implement "auto-increment" or "identity" column types, such as MySQL or Microsoft SQL Server
*   If the previous step does not identify a column as a sequence, we inspect the `ResultSetMetaData` obtained by running a dummy query on the table. If the `isAutoIncrement()` API returns true for that column, we mark the corresponding field as `type="sequence"`
*   If the previous steps have not identified the column as a sequence, we check the `TYPE_NAME` in the column metadata. If it is "serial", this means the column is a PostgreSQL "serial" or "serial8" type column. Postgres does not transparently implement auto-increment columns, but it does provide this serial type, which causes the column to be implicitly bound to an underlying sequence. So this type causes us to mark the field `type="sequence"`, and we also set [implicitSequence](DataSourceField.md#attr-datasourcefieldimplicitsequence) true
*   If the previous steps have not identified the column as a sequence, we check the `COLUMN_DEF` in the column metadata. If this contains the token "$$ISEQ" and ends with "NEXTVAL", this means the column is an Oracle "GENERATED AS IDENTITY" column. This type of column was introduced in Oracle 12c and is conceptually exactly the same thing as the Postgres "serial" column described above. We treat it the same way: mark it `type="sequence"` and `implicitSequence="true"`
*   If the previous steps have not identified the column as a sequence, then you may be using a pure sequence database, such as an Oracle version earlier than 12c, or you may be using a database where both sequences and identity columns are available (Oracle, Postgres, DB2), and a sequence is being used either by design or because the table was created before the database product supported identity columns. In this case, we cannot determine if the column should be a sequence or not. However, in many applications, the fact that the column is an integer and is a primary key would imply that it is also a sequence. Therefore, if the column is an integer and the `server.properties` flag `auto.derive.integer.pk.always.sequence` is true, we mark the field as `type="sequence"`
*   If, after all this, SmartClient ends up incorrectly marking a primary key field as a sequence (or vice versa), you can always override it on a per-field basis by simply redeclaring the field with the correct type in your `.ds.xml` file:
    ```
      <DataSource serverType="sql" tableName="myTable" autoDeriveSchema="true">
        <fields>
          <!-- This field was incorrectly marked as a sequence -->
          <field name="notASeq" type="integer" />
          <!-- This field was incorrectly marked as an integer when it should be a sequence -->
          <field name="isASeq" type="sequence" />
        </fields>
      </DataSource>
    ```
    

If the metadata source is Hibernate mappings described in a `.hbm.xml` file:

*   The first field we encounter that is described in the mapping with an `<id>` tag is marked as a primaryKey
*   If that field is marked as being generated, we set its type to "sequence"

If the metadata source is an annotated object (whether JPA, Hibernate or just an annotated POJO):

*   Any field with an `@Id` annotation is is marked as a primaryKey (this differs from the Hibernate `.hbm.xml` file case because that is specific to Hibernate, which does support composite keys, but not by specifying multiple `<id>` tags. Annotations are supported, via annotated POJOs, for any kind of persistence strategy, so multiple `@Id` fields are perfectly valid)
*   Any field with a `@GeneratedValue` annotation is either marked as `type="sequence"` (if it is an integer type) or as `[autoGenerated](DataSourceField.md#attr-datasourcefieldautogenerated)="true"` (for other field types)

Finally, if the metadata is a plain, unannotated Java object, no attempt is made to derive primary key fields.
#### enums and valueMaps
When we come across Java `Enum` properties in plain or annotated classes, as well as setting the field type as noted in the above tables, we also generate a valueMap for the field, based on the `Enum` members.

For cases where we generate a field of SmartClient type "enum" (see the above tables), the keys of the valueMap are the result of calling `name()` on each member of the underlying Java Enum (in other words, its value exactly as declared in its enum declaration). For cases where we generate a field of SmartClient type "intEnum", the keys of the valueMap are strings representing the ordinal number of each member in the Java Enum - "0", "1", etc. Note that this behavior will be overriden by [DataSource.enumTranslateStrategy](#attr-datasourceenumtranslatestrategy) if both are set.

In both of these case, the display values generated for the valueMap are the result of calling `toString()` on each Enum member. If that gives the same value as calling `name()`, the value is passed through `DataTools.deriveTitleFromName()`, which applies the same processing rules as [DataSource.getAutoTitle](#classmethod-datasourcegetautotitle) to derive a more user-friendly display value.

#### Further notes
`schemaBean` implies `autoDeriveSchema`, because it has no other purpose than to name the bean to use for auto-derived schema. Thus, if you specify `schemaBean` you do not need to specify `autoDeriveSchema` as well (though it does no harm to do so). However, `tableName` and `beanClassName` can be validly specified without implying `autoDeriveSchema`, so in those cases you must explicitly specify `autoDeriveSchema`.

The underlying super-DataSource is cached in server memory, so that it does not have to be derived and created each time you need it. However, the cache manager will automatically refresh the cached copy if it detects that the deriving DataSource has changed. Thus, if you change the metadata your DataSource is deriving (if, for example, you add a column to a table), all you need to do is touch the `.ds.xml` file (ie, update its last changed timestamp - you don't actually have to change it) and the cached copy will be refreshed next time it is needed.

When autoDeriveSchema is set, SQLDataSource will automatically discover foreignKeys and deliver table and column name information to the client in hashed form so that two DataSources that are linked by native SQL foreign keys will automatically discover each other if loaded into the same application, and set [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) automatically. Because the table and column names are delivered as cryptohashes, there is no information leakage, but regardless, the feature can be disabled via setting `datasource.autoLinkFKs` to false in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file). This hashed linkage information is delivered to the client in properties [DataSource.tableCode](#attr-datasourcetablecode) and [DataSourceField.fkTableCode](DataSourceField.md#attr-datasourcefieldfktablecode)/[fkColumnCode](DataSourceField.md#attr-datasourcefieldfkcolumncode)

### Groups

- fields

**Flags**: IR

---
## Attr: DataSource.useSequences

### Description
For a DataSource with [serverType:"sql"](#attr-datasourceservertype), this flag indicates whether any fields of [type](DataSourceField.md#attr-datasourcefieldtype) "sequence" should be backed by a native database sequence (if the flag is true) or an auto-increment/identity column (if it is false). It is only applicable in cases where the database in use supports both approaches, _and_ SmartClient supports both strategies with that particular database. For most databases, even those that natively support either approach, SmartClient uses one or the other, and this cannot be configured.

Right now, the only supported database is Microsoft SQL Server. If you specify this flag on a non-SQL DataSource or if any database other than SQL Server is in use, the flag is simply ignored.

If not set, this flag defaults to the `server.properties` setting `sql.{dbName}.use.sequences`, which in turn defaults to false.

**Flags**: IR

---
## Attr: DataSource.allowAdvancedCriteria

### Description
By default, all DataSources are assumed to be capable of handling [AdvancedCriteria](../reference.md#object-advancedcriteria) on fetch or filter type operations. This property may be set to `false` to indicate that this dataSource does not support advancedCriteria. See [DataSource.supportsAdvancedCriteria](#method-datasourcesupportsadvancedcriteria) for further information on this.

**NOTE:** If you specify this property in a DataSource descriptor (`.ds.xml` file), it is enforced on the server. This means that if you run a request containing AdvancedCriteria against a DataSource that advertises itself as `allowAdvancedCriteria:false`, it will be rejected.

### See Also

- [OperationBinding.allowAdvancedCriteria](OperationBinding.md#attr-operationbindingallowadvancedcriteria)

**Flags**: IRWA

---
## Attr: DataSource.schema

### Description
**This property only applies to the built-in SQL DataSource provided in Pro and better editions of SmartClient**

Defines the name of the schema we use to qualify the [tableName](#attr-datasourcetablename) in generated SQL. If you do not provide this property, we will try to use the SmartClient default schema for this [dbName](../kb_topics/dbConfigTool.md#kb-topic-database-configuration); you specify this for a given `dbName` in your `server.properties` file like this:

```
    sql.the_dbName.default.schema: myDefaultSchema
 
```
If there is no DataSource-specific schema and no SmartClient default schema, table names will not be qualified in generated SQL, and thus the database default schema will be used. Support for multiple schemas (or schemata) varies quite significantly across the supported databases, as does the meaning of the phrase "default schema". In addition, some databases allow you to override the default schema in the JDBC connection URL, which is a preferable approach if all your tables are in the same (non-default) schema, because it makes the generated SQL simpler (no need to qualify every table)

The following table provides information by product:

| Product | Notes |
|---|---|
| DB2 | Arbitrarily named schemas are supported. The default schema is named after the connecting user, though this can be overridden by specifying the "currentSchema" property on the JDBC connection URL |
| DB2 for iSeries | Arbitrarily named schemas are supported. "Schema" is synonymous with "library". The default schema depends on the setting of the "naming" connection property. When this is set to "sql", behavior is similar to other DB2 editions: the default schema is named after the connecting user, unless overridden by specifying a library name in the JDBC connection URL. When "naming" is set to "system", the schema of an unqualified table is resolved using a traditional search of the library list; the library list can be provided in the "libraries" property |
| Firebird | Firebird does not support the concept of schema at all - all "schema objects" like tables and indexes belong directly to the database. In addition, Firebird actively rejects qualified table names in queries as syntax errors; therefore, you should not set the schema property for a DataSource that will be backed by a Firebird database |
| HSQLDB | Arbitrarily named schemas are supported. The default schema is auto-created when the database is created; by default it is called "PUBLIC", but can be renamed. It is not possible to set the default schema in the JDBC connection URL |
| Informix | Informix databases can be flagged as "ANSI mode" at creation time. ANSI-mode databases behave similarly to DB2 for schema support: arbitrarily named schemas are supported, and the default schema is the one named after the connected user. Non-ANSI databases have no real schema support at all. It is not possible to set the default schema in the JDBC connection URL with either type of database |
| Microsoft SQL Server | Prior to SQL Server 2005, schema support is similar to Oracle: "schema" is synonymous with "owner". As of SQL Server 2005, schema is supported as a separate concept, and a user's default schema can be configured (though it still defaults to a schema with the same name as the user). It is not possible to set the default schema in the JDBC connection URL |
| MySQL | MySQL does not have a separate concept of "schema"; it treats the terms "schema" and "database" interchangeably. In fact MySQL databases actually behave more like schemas, in that a connection to database X can refer to a table in database Y simply by qualifying the name in the query. Also, because schema and database are the same concept in MySQL, overriding the "default schema" is done implicitly when you specify which database to connect to in your JDBC connection URL |
| Oracle | Arbitrarily named schemas are not supported; in Oracle, "schema" is synonymous with "user", so each valid user in the database is associated implicitly with a schema of the same name, and there are no other schemas possible. It is possible to refer to tables in another user's schema (assuming you have the privileges to do so) by simply qualifying the table name. The default schema is always implied by the connecting user and cannot be overridden. |
| Postgres | Arbitrarily named schemas are supported. Rather than the concept of a "default schema", Postgres supports the idea of a search path of schemas, whereby unqualified table references cause a search of the list of schemas in order, and the first schema in the path is the "current" one for creation purposes. Unfortunately, there is no way to specify this search path on the JDBC connection URL, so the default schema comes from the user definition, ultimately defaulting to the default "public" schema |

**Flags**: IR

---
## Attr: DataSource.nullIntegerValue

### Description
If [DataSource.noNullUpdates](#attr-datasourcenonullupdates) is set, the value to use for any integer field that has a null value assigned on an update operation, and does not specify an explicit [nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue).

### See Also

- [DataSource.noNullUpdates](#attr-datasourcenonullupdates)
- [DataSourceField.nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue)

**Flags**: IR

---
## Attr: DataSource.audit

### Description
Enables saving of a log of changes to this DataSource in a second DataSource with the same fields, called the "audit DataSource". **NOTE**: this feature applies to Enterprise Edition only; for more information on edition-specific features, see [http://smartclient.com/product](http://smartclient.com/product).

When auditing is enabled, every time a DSRequest modifies this DataSource, a Record is added to the audit DataSource that shows the record as it existed after the change was made (or for a "remove", the values of the record at the time of deletion). In addition, the audit DataSource has the following additional metadata fields:

*   ["audit\_operationType"](#attr-datasourceaudittypefieldname): type of the change ("update", "add" or "remove")
*   ["audit\_modifier"](#attr-datasourceaudituserfieldname): username of the user that made the change. The username is determined in the same way that the [Declarative Security](OperationBinding.md#attr-operationbindingrequiresrole) subsystem determines the current user.
*   ["audit\_changeTime"](#attr-datasourceaudittimestampfieldname): a field of type "datetime" recording the timestamp of the change
*   ["audit\_revision"](#attr-datasourceauditrevisionfieldname): a field of type "sequence" recording a simple increasing integer value
*   ["audit\_changedFields"](#attr-datasourceauditchangedfieldsfieldname): a ["multiple"](DataSourceField.md#attr-datasourcefieldmultiple) field of type "string". For "update" operations, records which fields have changed; otherwise, null

If any of the field names above collide with field names of the DataSource being audited, an integer suffix will also be added, starting with 2 (for example, "audit\_modifier2", then "audit\_modifier3", etc).

To omit a data field from the automatically generated audit DataSource, just set [DataSourceField.audit](DataSourceField.md#attr-datasourcefieldaudit) to false. Audit can be disabled for a given DSRequest via the server-side API `DSRequest.setSkipAudit()`, or for a specific operation via the [operationBinding.skipAudit](OperationBinding.md#attr-operationbindingskipaudit) setting.

When viewing DataSources in the [DataSource Navigator](../kb_topics/dataSourcesTab.md#kb-topic-datasources-tab), a button will be shown at the top of a DataSource's section if it has an audit DataSource to let you conveniently open another section to view it.

Note: The DataSource audit feature works only with single row operations; operations with [allowMultiUpdate](OperationBinding.md#attr-operationbindingallowmultiupdate) enabled are not supported.

#### Auto-generated Audit DataSources

The audit DataSource is normally automatically generated, and unless otherwise specified with [DataSource.auditDataSourceID](#attr-datasourceauditdatasourceid), the ID of the audit DataSource will be `audit_[OriginalDSID]`.

By default, the automatically generated audit DataSource will be of the same type as the DataSource being audited, however, if the DataSource being audited is not already a SQLDataSource, we recommend using [auditDSConstructor:"sql"](#attr-datasourceauditdsconstructor) to use a SQLDataSource as the audit DataSource. This is because a SQLDataSource used an audit DataSource will automatically generate a SQL table for storing audit data the first time changes are made. JPA would require manual creation of a Java Bean, and Hibernate requires [hbm2ddl.auto=update](http://www.google.com/search?q=hbm2ddl.auto) to be set, which is widely considered unsafe for production use.

Note that the automatically generated audit DataSource may have additional fields that can be populated when new audit data is added. See [DataSource.addedAuditFields](#attr-datasourceaddedauditfields) for more details.

Automatically created audit DataSources can be loaded and queried just like other DataSources, using the DataSourceLoader, and using the server-side API `DataSource.getAuditDataSource()`. However, you **must** load the DataSource being audited before loading its automatically created audit DataSource.

Note, that automatic SQL tables creation can be disabled. See [autoCreateAuditTable](#attr-datasourceautocreateaudittable) for details.

#### Connecting custom "Users" DataSource to auto-generated Audit DataSources

Audit DataSources utilize authenticated username (see the docs for `RPCManager.getUserId()` server-side API) to populate the "audit\_modifier" field. To enable quick access to additional user information, you can associate them with a custom "Users" DataSource.

This association can be configured via the framework setting "userDataSource.foreignKey" in the "server.properties" file, which establishes a relationship between authenticated user and your custom "Users" DataSource. Declaring this informs the system that the authenticated username is a valid ID for records within a specific "Users" DataSource. Use the regular [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) format, where, in example below, "UserDS" represents the name of the related "Users" DataSource, and "userName" serves as the primary key of that DataSource:

```
 userDataSource.foreignKey: UserDS.userName
 
```
This configuration enables you to access additional user information seamlessly through built-in framework features like [DSRequest.additionalOutputs](DSRequest.md#attr-dsrequestadditionaloutputs) and [ListGridField.includeFrom](ListGridField.md#attr-listgridfieldincludefrom) when reviewing audit data. For instance, if "UserDS" declares fields such as "firstName" and "lastName," you can retrieve them using additional listGridFields:
```
 {name: "userFirstName", includeFrom: "UserDS.firstName"},
 {name: "userLastName", includeFrom: "UserDS.lastName"}
 
```
Alternatively, if you're fetching data manually, you can utilize additionalOutputs as follows:
```
 additionalOutputs: "userFirstName!UserDS.firstName,userLastName!UserDS.lastName"
 
```
#### Manually created Audit DataSources

The audit DataSource can also be manually created. In this case, you can can either follow the naming conventions described above for the ID of the audit DataSource and the names of metadata fields, or use the linked properties to assign custom names. If you omit any data fields from the tracked DataSource in your audit DataSource, those fields will be ignored for auditing purposes, exactly as though [DataSourceField.audit](DataSourceField.md#attr-datasourcefieldaudit) had been set to false for an automatically-generated audit DataSource.

Also, note that in case of manually defined audit DataSource, if this DataSource is defined so it inherits the audited DataSource, all the audited DataSource's fields will be inherited, this including the primary keys. Since for the audit DataSource the primary key should be the revision field, in order to prevent the audit DataSource having two primary keys, the inherited DataSource's primary key will have to be declared in audit DataSource, but with the primaryKey attribute omitted (as well not being of type "sequence") in the audit DataSource.

### Groups

- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.resultTreeClass

### Description
Class for ResultTrees used by this datasource. If null, defaults to using [ResultTree](ResultTree.md#class-resulttree).

This can be set to a custom subclass of ResultTree that, for example, hangs on to extra information necessary for integration with web services.

**Flags**: IRA

---
## Attr: DataSource.guestUserId

### Description
Value to use for the [ownerIdField](#attr-datasourceowneridfield) if no one has authenticated.

This setting can be overridden at the operationBinding level.

### See Also

- [DataSource.ownerIdField](#attr-datasourceowneridfield)
- [OperationBinding.guestUserId](OperationBinding.md#attr-operationbindingguestuserid)
- [DataSource.ownerIdNullRole](#attr-datasourceowneridnullrole)
- [DataSource.ownerIdNullAccess](#attr-datasourceowneridnullaccess)

**Flags**: IR

---
## Attr: DataSource.autoCreateAuditTable

### Description
Setting `autoCreateAuditTable` to `true` indicates that audit DataSource will automatically create SQL table when [auditing](#attr-datasourceaudit) is enabled.

Note, that `autoCreateAuditTable` attribute takes effect only if framework setting `audit.autoCreateTables` in `server.properties` is set to `false`, which by default is set to `true`.

**Flags**: IR

---
## Attr: DataSource.serverOnly

### Description
Setting a DataSource to be `serverOnly="true"` ensures that it will not be visible to the client. Any request through IDACall to this DataSource will return a failure response. Only requests which have been initiated on the server-side will be executed against this DataSource.

**Flags**: IR

---
## Attr: DataSource.multiInsertStrategy

### Description
For dataSources of [serverType](#attr-datasourceservertype) "sql" only, this property sets the multi-insert strategy for add requests on this [dataSource](#class-datasource). Only has an effect if the [add request](#method-datasourceadddata) specifies a list of records as the data. See the docs for [MultiInsertStrategy](../reference_2.md#type-multiinsertstrategy) for more information.

Note that this setting (along with the other multi-insert properties, [multiInsertBatchSize](#attr-datasourcemultiinsertbatchsize) and [multiInsertNonMatchingStrategy](#attr-datasourcemultiinsertnonmatchingstrategy)) can be overridden at the [operationBinding level](OperationBinding.md#attr-operationbindingmultiinsertstrategy) and the [dsRequest level](DSRequest.md#attr-dsrequestmultiinsertstrategy). If you wish to configure multi-insert setting globally, you can add the following properties to your `server.properties` file:

`sql.multi.insert.strategy` Global equivalent of [multiInsertStrategy](#attr-datasourcemultiinsertstrategy)  
`sql.multi.insert.batchSize` Global equivalent of [multiInsertBatchSize](#attr-datasourcemultiinsertbatchsize)  
`sql.multi.insert.non.matching.strategy` Global equivalent of [multiInsertNonMatchingStrategy](#attr-datasourcemultiinsertnonmatchingstrategy)

Example `server.properties` settings:

```
   sql.multi.insert.strategy: multipleValues
   sql.multi.insert.batchSize: 300
   sql.multi.insert.non.matching.strategy: dropMissing
 
```
See the "Batch inserting" paragraph of the [addData() documentation](#method-datasourceadddata) for a description of the multi-insert implementation.

### See Also

- [DataSource.multiInsertBatchSize](#attr-datasourcemultiinsertbatchsize)
- [DataSource.multiInsertNonMatchingStrategy](#attr-datasourcemultiinsertnonmatchingstrategy)

**Flags**: IRW

---
## Attr: DataSource.mockMode

### Description
If set, causes this DataSource to use a read-only "mock" or "test" dataset, if specified, or if no test data is available, then to load data normally but then operate similarly to a [DataSource.clientOnly](#attr-datasourceclientonly) DataSource, never writing changes back to the server.

`mockMode` has no effect on [MockDataSource](MockDataSource.md#class-mockdatasource) or a [DataSource.clientOnly](#attr-datasourceclientonly) DataSource.

For other DataSources, a one-time fetch will be performed to retrieve sample data, similar to a [DataSource.cacheAllData](#attr-datasourcecachealldata) DataSource, except that changes will never be saved back to the server. Only a subset of data will be retrieved, based on [DataSource.mockDataRows](#attr-datasourcemockdatarows). [DataSource.mockDataCriteria](#attr-datasourcemockdatacriteria) can optionally be set to retrieve specific data.

Alternatively, mock data can be provided with [DataSource.cacheData](#attr-datasourcecachedata).

DataSources can be loaded in `mockMode` via passing settings to [DataSource.load](#classmethod-datasourceload), or if loaded with a screen or project, by passing settings to [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen) or the server-side Project.load() API.

**Flags**: IRW

---
## Attr: DataSource.description

### Description
An optional description of the DataSource's content. It is not automatically exposed on any component, but it is useful for developer documentation, and as such it is included on any [OpenAPI specification](../kb_topics/openapiSupport.md#kb-topic-openapi-specification-oas-support) generated by the framework. Markdown is a commonly-used syntax, but you may also embed HTML content. When embedding HTML in the description in a .ds.xml file (see [dataSourceDeclaration](../kb_topics/dataSourceDeclaration.md#kb-topic-creating-datasources)), it is recommended to wrap the HTML in a CDATA tag.

This description is also provided to AI when AI is asked to work with the data source. Best practices for the description are:

*   Start with a plain language explanation of what the data source and records within it represent, their business concept or core purpose.
*   Describe how the data source relates to other data sources in the application.
*   Mention the approximate size of the data source and whether/when records are updated, added, and removed, as well as the approximate rates of updates, additions, and removals.
*   Identify any known data issues or anomalies.

In addition to the data source-level description, each field can be described via [DataSourceField.description](DataSourceField.md#attr-datasourcefielddescription).

### See Also

- [DataSource.sampleData](#attr-datasourcesampledata)

**Flags**: IR

---
## Attr: DataSource.requiresRole

### Description
Similar to [OperationBinding.requiresRole](OperationBinding.md#attr-operationbindingrequiresrole), but controls access to the DataSource as a whole.

### Groups

- auth
- declarativeSecurity

**Flags**: IR

---
## Attr: DataSource.compareMetadataForAuditChangeStatus

### Description
Only applicable to [binary fields](../kb_topics/binaryFields.md#kb-topic-binary-fields) on [audited](#attr-datasourceaudit) DataSources.

When determining if a binary field has changed for auditing purposes, should we compare the metadata values (ie, the associated `_filename` and `_filesize` fields) or the actual binary content? If you set this flag to false, this will cause SmartClient to fetch the existing content of any binary field from the database before any update, and then compare it byte by byte to the new content. You should consider if this will have performance implications for your application, particularly if you store large binary values.

Note that value comparison of any kind is only performed if the field's [DataSourceField.audit](DataSourceField.md#attr-datasourcefieldaudit) setting is "change", but also note that this is the default setting for binary fields

**Flags**: IR

---
## Attr: DataSource.quoteColumnNames

### Description
If set, tells the SQL engine to quote column names in all generated DML and DDL statements for this dataSource. This will ensure that queries generated against tables that do not follow the database product's natural column-naming conventions will still work.

In general we recommend that you allow the database to use its natural naming scheme when creating tables (put more simply, just do not quote column names in the `CREATE TABLE` statement); if you do this, you will not need to worry about quoting column names when querying. However, if you are dealing with pre-existing tables, or do not have control over the database naming conventions used, this property may become necessary. This property may also be necessary if you are using field/column names that clash with reserved words in the underlying database (these vary by database, but a field called "date" or "timestamp" would have problems with most database products)

**Note:** Only applicable to dataSources of [serverType](#attr-datasourceservertype) "sql".

**Flags**: IR

---
## Attr: DataSource.fileFormatField

### Description
The native field name used by this DataSource on the server to represent the `fileFormat` for [FileSource Operations](../kb_topics/fileSource.md#kb-topic-filesource-operations).

If the fileFormatField is not configured, then a field named "fileFormat" will be used, if it exists. Otherwise, the DataSource will not track fileFormats -- this may be acceptable if, for instance, the fileFormat is always the same.

The fileFormat is specified according to the extension that would have been used in the filesystem -- for instance, the fileFormat for employees.ds.xml would be "xml".

### Groups

- fileSource

**Flags**: IR

---
## Attr: DataSource.trimMilliseconds

### Description
For this dataSource, should the millisecond portion of time and datetime values be trimmed off before before being sent from client to server or vice versa. By default, millisecond information is preserved (ie, it is not trimmed). You only need to consider trimming millisecond values if their presence causes a problem - for example, a custom server that is not expecting that extra information and so fails parsing.

Note that there is no inherent support for millisecond precision in SmartClient widgets; if you need millisecond-precise visibility and editability of values in your client, you must write custom formatters and editors (or sponsor the addition of such things to the framework). Server-side, millisecond-precise values are delivered to and obtained from DataSources, so DataSource implementations that are capable of persisting and reading millisecond values should work transparently. Of the built-in DataSource types, the JPA and Hibernate DataSources will transparently handle millisecond-precise values as long as the underlying database supports millisecond precision, and the underlying column is of an appropriate type. The SQLDataSource provides accuracy to the nearest second by default; you can switch on millisecond precision per-field with the [storeMilliseconds](DataSourceField.md#attr-datasourcefieldstoremilliseconds) attribute.

**Flags**: IR

---
## Attr: DataSource.requestProperties

### Description
Additional properties to pass through to the [DSRequest](../reference.md#object-dsrequest)s made by this DataSource. This must be set before any [DSRequest](../reference.md#object-dsrequest)s are issued and before any component is bound to the DataSource.

These properties are applied before [DataSource.transformRequest](#method-datasourcetransformrequest) is called.

### Groups

- clientDataIntegration
- serverDataIntegration

### See Also

- [DSRequest](../reference.md#object-dsrequest)
- [OperationBinding.requestProperties](OperationBinding.md#attr-operationbindingrequestproperties)

**Flags**: IRW

---
## Attr: DataSource.auditTypeFieldName

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), specifies the field name used to store the [operationType](../reference.md#type-dsoperationtype) (in a field of type "text"). If empty string is specified as the field name, the audit DataSource will not store this field.

**Flags**: IR

---
## Attr: DataSource.tableCode

### Description
**Only applicable to the built-in SQL DataSource**

`tableCode` and the related properties [DataSourceField.columnCode](DataSourceField.md#attr-datasourcefieldcolumncode), [DataSourceField.fkTableCode](DataSourceField.md#attr-datasourcefieldfktablecode) and [DataSourceField.fkColumnCode](DataSourceField.md#attr-datasourcefieldfkcolumncode) are read-only attributes that are secure and unique cryptographic hashes of table and column names used by this DataSource.

These properties are used automatically by client-side framework code to link dataSources together by [foreign key](DataSourceField.md#attr-datasourcefieldforeignkey) when a `foreignKey` is not explicitly declared, but is found in the SQL schema via the [DataSource.autoDeriveSchema](#attr-datasourceautoderiveschema) feature.

A secure hash is used rather than the actual SQL table or column name for security reasons - sending the actual SQL table or column name to the client could aid in attempted SQL injection attacks.

This feature can be disabled system-wide via setting `datasource.autoLinkFKs` to `false` in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file).

**Flags**: R

---
## Attr: DataSource.sqlPrefix

### Description
**This feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

For DataSources of [serverType](#attr-datasourceservertype) "sql" only, some text to add right at the beginning of any generated query, before all other text. See the documentation for the [operationBinding level](OperationBinding.md#attr-operationbindingsqlprefix) property for more detail.

### Groups

- customQuerying

**Flags**: IR

---
## Attr: DataSource.arrayCriteriaForceExact

### Description
With ordinary [simple criteria](../reference_2.md#type-criteria), it is possible to provide an array of values for a given field, which means "any of these values". For example:
```
  var criteria = {
    field1 : "value1",
    field2 : ["value2", "value3"]
 }
```
At first glance, this criteria appears to mean "select records where 'field1' is 'value1' and 'field2' is one of 'value2' or 'value3'". However, if the prevailing [textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is "substring" - as it would be if, for example, you had issued a [filterData()](#method-datasourcefilterdata) call - then this criteria means "select records where 'field1' contains 'value1' somewhere, and 'field2' contains either 'value2' or 'value3'"

Depending on your requirement, this may or may not be what you want, and you can control it by setting the `textMatchStyle` on your [DSRequest](../reference.md#object-dsrequest), or by setting a default `textMatchStyle` on the DataSource ([DataSource.defaultTextMatchStyle](#attr-datasourcedefaulttextmatchstyle)), or by specifying that the `textMatchStyle` should be ignored for certain fields ([DataSourceField.ignoreTextMatchStyle](DataSourceField.md#attr-datasourcefieldignoretextmatchstyle))

However, a common use case is that you want "substring" style filtering on one or more single-valued fields, but exact matching on a list-valued field. For example, say you want a list of customers based in certain cities, with a name matching the substring "software":

```
  var criteria = {
    name : "software",
    city : ["York", "Newport", "Orleans"]
 }
```
Here, using substring matching on the "city" field is likely to give incorrect results, as it will match a number of US cities in addition to the three European cities intended (New York, Yorktown, New Orleans, Newport News, and probably others). And even if this is not an issue for your particular use case, and correct results can be obtained with a substring search, it is very likely to be more costly performance-wise than the exact value match that you really need (potentially much more costly).

You could achieve exact matching in the above case by marking the "city" field as `ignoreTextMatchStyle:true`, but that would mean you couldn't perform substring searches on that field in other use cases where that might be desirable.

In cases like this, SmartClient by default treats list-valued simple criteria as if `ignoreTextMatchStyle` is in force for that field. If you want to switch this behavior off, and have list-valued simple criteria handled with the prevailing `textMatchStyle`, set `arrayCriteriaForceExact` to false. It is also possible to set this flag per-operationBinding and per-DSRequest - see [OperationBinding.arrayCriteriaForceExact](OperationBinding.md#attr-operationbindingarraycriteriaforceexact) and [DSRequest.arrayCriteriaForceExact](DSRequest.md#attr-dsrequestarraycriteriaforceexact)

If you want to switch this behavior off across the entire system, set the flag in your `server.properties` file:

```
     arrayCriteriaForceExact: false
 
```
This will only have an effect for server-side DataSources; if you want to change this flag globally for [clientOnly](#attr-datasourceclientonly) dataSources, change the default in the client-side [DataSource](#class-datasource) class, like so:
```
     isc.DataSource.addProperties({arrayCriteriaForceExact: false});
 
```
If you do change the global defaults, it is still possible to override per-dataSource or per-operationBinding, as described above.

Note, all of this only applies to _simple_ criteria. If your dataSource [supports AdvancedCriteria](#method-datasourcesupportsadvancedcriteria), that gives you much finer and more complete control over the exact meaning of individual criterions.

### Groups

- clientDataIntegration
- serverDataIntegration

**Flags**: IR

---
## Attr: DataSource.auditChangedFieldsFieldLength

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), specifies the length of the field used to store the names of the fields which were updated. See also [DataSource.auditChangedFieldsFieldName](#attr-datasourceauditchangedfieldsfieldname)

To set the changedFields field length for all DataSources that do not override the default, set `audit.auditChangedFieldsFieldLength` in your `server.properties` file. For example

```
        audit.auditChangedFieldsFieldLength: 512
 
```

**Flags**: IR

---
## Attr: DataSource.inheritanceMode

### Description
For dataSources of [serverType](#attr-datasourceservertype) "sql" and "hibernate", specifies the inheritance mode to use. This property has no effect for any other type of DataSource.

### Groups

- fields

### See Also

- [DataSource.inheritsFrom](#attr-datasourceinheritsfrom)

**Flags**: IR

---
## Attr: DataSource.nullFloatValue

### Description
If [DataSource.noNullUpdates](#attr-datasourcenonullupdates) is set, the value to use for any float field that has a null value assigned on an update operation, and does not specify an explicit [nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue).

### See Also

- [DataSource.noNullUpdates](#attr-datasourcenonullupdates)
- [DataSourceField.nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue)

**Flags**: IR

---
## Attr: DataSource.schemaNamespace

### Description
For a DataSource derived from WSDL or XML schema, the XML namespace this schema belongs to. This is a read-only attribute automatically present on DataSources returned from [SchemaSet.getSchema](SchemaSet.md#method-schemasetgetschema) and [WebService.getSchema](WebService.md#method-webservicegetschema).

### Groups

- wsdlBinding
- clientDataIntegration

**Flags**: R

---
## Attr: DataSource.qualifyColumnNames

### Description
For dataSources of [serverType](#attr-datasourceservertype) "sql", determines whether we qualify column names with table names in any SQL we generate. This property can be overridden on specific operationBindings.

### See Also

- [OperationBinding.qualifyColumnNames](OperationBinding.md#attr-operationbindingqualifycolumnnames)

**Flags**: IR

---
## Attr: DataSource.auditRevisionFieldName

### Description
For DataSources with [auditing enabled](#attr-datasourceaudit), specifies the field name used to store the revision number for the change (in a field of type "sequence"). If empty string is specified as the field name, the audit DataSource will not store this field.

**Flags**: IR

---
## Attr: DataSource.dataURL

### Description
Default URL to contact to fulfill all DSRequests. Can also be set on a per-operationType basis via [OperationBinding.dataURL](OperationBinding.md#attr-operationbindingdataurl).

NOTE: Best practice is to use the same `dataURL` for all DataSources which fulfill DSRequests via the server-side RPCManager API. Otherwise, cross-DataSource [operation queuing](RPCManager.md#classmethod-rpcmanagerstartqueue) will not be possible.

### Groups

- clientDataIntegration

**Flags**: IR

---
## Attr: DataSource.jsonPrefix

### Description
Allows you to specify an arbitrary prefix string to apply to all json format responses sent from the server to this application.

The inclusion of such a prefix ensures your code is not directly executable outside of your application, as a preventative measure against [javascript hijacking](http://www.google.com/search?q=javascript+hijacking).

Only applies to responses formatted as json objects. Does not apply to responses returned via scriptInclude type transport.  
Note: If the prefix / suffix served by your backend is not a constant, you can use [dataFormat:"custom"](OperationBinding.md#attr-operationbindingdataformat) instead and explicitly parse the prefix out as part of [transformResponse()](#method-datasourcetransformresponse).

### See Also

- [OperationBinding.dataFormat](OperationBinding.md#attr-operationbindingdataformat)
- [OperationBinding.dataTransport](OperationBinding.md#attr-operationbindingdatatransport)

**Flags**: IRA

---
## Attr: DataSource.relatedTableAlias

### Description
For a [SQL DataSource](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) that is referred by [additional foreign keys](DataSourceField.md#attr-datasourcefieldotherfks), this property defines the table alias name to use in generated SQL. If omitted [DataSource ID](#attr-datasourceid) will be used to construct the alias.

Aliasing is necessary when the same table appears more than once in a query. In addition to use cases described in [DataSourceField.relatedTableAlias](DataSourceField.md#attr-datasourcefieldrelatedtablealias), this may happen when `includeFrom` field using [foreign key defined in otherFKs](DataSourceField.md#attr-datasourcefieldotherfks) would be included multiple times in a related DataSource.

See the "Automatically generated table aliases" section of the [SQL Templating](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview) for the complete set of general rules how aliases are generated. Also, see [dataSourceField.otherFKs](DataSourceField.md#attr-datasourcefieldotherfks) for more details and usage samples.

### Groups

- dataSourceRelations

### See Also

- [DataSourceField.otherFKs](DataSourceField.md#attr-datasourcefieldotherfks)
- [DataSourceField.includeVia](DataSourceField.md#attr-datasourcefieldincludevia)
- [DataSourceField.relatedTableAlias](DataSourceField.md#attr-datasourcefieldrelatedtablealias)

**Flags**: IR

---
## Attr: DataSource.cacheMaxAge

### Description
The maximum time, in seconds, to maintain the client-side cache. If a fetch occurs after the cacheMaxAge has expired, the current cache will be dropped and another complete cache fetched.

### Groups

- clientData

**Flags**: IRW

---
## Attr: DataSource.projectFileLocations

### Description
For DataSources with type [`projectFile`](../reference_2.md#type-dsservertype), specifies locations for the project files. In XML, each location is expressed with a ``<location>`` tag, e.g.:
```
     <projectFileLocations>
         <location>[WEBROOT]/shared/ds</location>
         <location>ds://datasources</location>
     </projectFileLocations>
 
```
Directories should be specified as absolute paths on the server. If you want to construct a webroot-relative path, then prefix the path with `[WEBROOT]` (unlike in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file), where you would use `$webRoot` as the prefix).

To specify another DataSource to be used via [fileSource operations](../kb_topics/fileSource.md#kb-topic-filesource-operations), use `ds://dsName` (where "dsName" is the name of the other DataSource).

A `projectFile` DataSource uses the standard [fileSource](../kb_topics/fileSource.md#kb-topic-filesource-operations) field names: `fileName`, `fileType`, `fileFormat`, `fileContents`, `fileSize` and `fileLastModified`. When defining a `projectFile` DataSource, you can use [inheritsFrom](#attr-datasourceinheritsfrom) with a value of "ProjectFile" to inherit definitions for these fields -- e.g.:

```
     <DataSource ID="MyDataSources" type="projectFile" inheritsFrom="ProjectFile">
         <projectFileLocations>
             <location>[WEBROOT]/shared/ds</location>
             <location>ds://datasources</location>
         </projectFileLocations>
     </DataSource> 
 
```

For directory locations, the `fileName` is relative to the directory specified. Note that the `fileName` does not include any extension for type or format. For instance, for "employees.ds.xml", the `fileName` would be "employees", the `fileType` would be "ds" and the `fileFormat` would be "xml".

A projectFile DataSource executes the various [fileSource operations](../kb_topics/fileSource.md#kb-topic-filesource-operations) in the following manner. The general rule is that `fileName`, `fileType`, and `fileFormat` are treated as primary keys. If files with the same combination of those attributes exist in more than one of the configured locations, the locations are considered in **reverse** order, with priority given to the location listed last. When modifying an existing file, the last location which contains the file will be used. When creating a new file, the file will be created in the last configured location.

[listFiles](#method-datasourcelistfiles)

Returns a combined list of files from all configured locations. Note that `listFiles` does not recurse into subdirectories. If the same combination of `fileName / fileType / fileFormat` exists in more than one configured location, then the data for `fileSize` and `fileLastModified` will be taken from the last configured location which contains the file.

[hasFile](#method-datasourcehasfile)

Indicates whether the file exists in any of the configured locations.

[getFile](#method-datasourcegetfile)

Returns file data by searching the locations in reverse order.

[saveFile](#method-datasourcesavefile)

If the file exists, it will be saved in the last location in which it exists. If it is a new file, it will be saved in the last configured location.

[renameFile](#method-datasourcerenamefile)

The file will be renamed in the last location in which it exists. Note that if the file exists in more than one location, the rename will not affect other locations. Thus, a subsequent `listFiles` operation will return the file from the other location (as well as the renamed file).

[removeFile](#method-datasourceremovefile)

The file will be removed from the last location in which it exists. Note that if the file exists in more than one location, the removal will not affect other locations. Thus, a subsequent `listFiles` operation will return the file from the other location.

For convenience, a `projectFile` DataSource also responds to the standard DataSource operations, in the following manner:

add

Executes a `saveFile` operation, either adding the file or updating an existing file.

fetch

Executes a `listFiles` operation. Note that the results will not include the `fileContents`. In order to obtain the `fileContents`, you must use a [getFile operation](#method-datasourcegetfile).

update

Executes a `renameFile` operation. Note that this will not update the `fileContents` -- for that, you need to use "add", or a [saveFile operation](#method-datasourcesavefile).

remove

Executes a `removeFile` operation.

If you specify both [projectFileKey](#attr-datasourceprojectfilekey) and `projectFileLocations`, then both with be used, with the `projectFileLocations` applied last.

### Groups

- fileSource

### See Also

- [DataSource.projectFileKey](#attr-datasourceprojectfilekey)

**Flags**: IR

---
## Attr: DataSource.ownerIdField

### Description
Requires that the currently authenticated user match the contents of this field, for client-initiated requests (i.e., where `DSRequest.isClientRequest()` returns true on the server).

Note, the behaviors described below can be affected by the dataSource properties [ownerIdNullRole](#attr-datasourceowneridnullrole) and [ownerIdNullAccess](#attr-datasourceowneridnullaccess), so please read the documentation for those two properties in conjunction with this article.

When a new row is added by a client-initiated [DSRequest](../reference.md#object-dsrequest), the ownerIdField will be automatically populated with the currently authenticated user (clobbering any value supplied by the client). Client-initiated attempts to update the ownerIdField will also be prevented.

If you wish to set the ownerIdField to a different value via an "add" or "update" operation, you can do so in server-side DMI code (possibly consulting `DSRequest.getClientSuppliedValues()` to get the value that was clobbered).

For client-initiated "fetch", "update" or "remove" operations, the server will modify client-supplied criteria so that only rows whose ownerIdField matches the currently authenticated user can be read, updated or deleted. For built-in DataSource types (SQL, Hibernate and JPA), the additional criteria required to match the `ownerIdField` field will ignore the prevailing [textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) and always use exact equality. If you have a custom or generic DataSource implementation, you will want to do the same thing, to avoid false positives on partial matches (eg, a user with name "a" gets records where the owner is any user with an "a" in the name). You can determine when this is necessary by looking for a [DSRequest](../reference.md#object-dsrequest) attribute called "restrictedOwnerIdField". For example, code similar to the following:

```
	String restrictedField = (String)dsRequest.getAttribute("restrictedOwnerIdField");
	if (field.getName() != null && field.getName().equals(restrictedField)) {
		// Use exact matching for this field
	} else {
		OK to use the textMatchStyle
	}
 
```
Also note, for server-initiated requests, this automatic criteria-narrowing is not applied; if your application requires server-initiated "fetch", "update" and "remove" requests to be limited to the currently-authenticated user, your code must add the necessary criteria to the request.

The ownerIdField setting can be overridden at the [OperationBinding.ownerIdField](OperationBinding.md#attr-operationbindingowneridfield) level.

If ownerIdField is specified, [requiresAuthentication](#attr-datasourcerequiresauthentication) will default to `true`. If `requiresAuthentication` is explicitly set to `false`, then unauthenticated users will be able to see all records. To avoid this, you can use [guestUserId](#attr-datasourceguestuserid) to specify a default user to apply when no one has authenticated.

### See Also

- [OperationBinding.ownerIdField](OperationBinding.md#attr-operationbindingowneridfield)
- [DataSource.guestUserId](#attr-datasourceguestuserid)

**Flags**: IR

---
## Attr: DataSource.lookAhead

### Description
If we are [loading progressively](#attr-datasourceprogressiveloading), indicates the number of extra records SmartClient Server will read beyond the end record requested by the client, in order to establish if there are more records to view. This property has no effect if we are not progressive-loading.

This property can be tweaked in conjunction with [endGap](#attr-datasourceendgap) to change behavior at the end of a dataset. For example, with the default values of `lookAhead: 1` and `endGap: 20`, we can end up with the viewport shrinking if we get a case where there really was only one more record (because the client was initially told there were 20 more). This is not a problem per se, but it may be surprising to the user. You could prevent this happening (at the cost of larger reads) by setting `lookAhead` to be `endGap+1`.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](#attr-datasourceprogressiveloading)
- [DataSource.endGap](#attr-datasourceendgap)

**Flags**: IRW

---
## Attr: DataSource.childrenField

### Description
fieldName for a field in the dataSource expected to contain an explicit array of child nodes. Enables loading a databound tree as a hierarchical data structure, rather than a flat list of nodes linked by foreignKey.  
Note this is an alternative to setting [DataSourceField.childrenProperty](DataSourceField.md#attr-datasourcefieldchildrenproperty) directly on the childrenField object.

By default the children field will be assumed to be [multiple](DataSourceField.md#attr-datasourcefieldmultiple), for XML databinding. This implies that child data should be delivered in the format:

```
      <childrenFieldName>
          <item name="firstChild" ...>
          <item name="secondChild" ...>
      </childrenFieldName>
 
```
However data may also be delivered as a direct list of `childrenFieldName` elements:
```
      <childrenFieldName name="firstChild" ...>
      <childrenFieldName name="secondChild" ...>
 
```
If you want to return your data in this format, you will need to explicitly set `multiple` to false in the appropriate dataSource field definition.

### Groups

- dataSourceRelations

### See Also

- [DataSourceField.childrenProperty](DataSourceField.md#attr-datasourcefieldchildrenproperty)

**Flags**: IR

---
## Attr: DataSource.inheritsFrom

### Description
ID of another DataSource this DataSource inherits its [DataSource.fields](#attr-datasourcefields) from.

Local fields (fields defined in this DataSource) are added to inherited fields to form the full set of fields. Fields with the same name are merged in the same way that [databound component fields](DataBoundComponent.md#attr-databoundcomponentfields) are merged with DataSource fields.

The default order of the combined fields is new local fields first (including any fields present in the parent DataSource which the local DataSource re-declares), then parent fields. You can set [DataSource.useParentFieldOrder](#attr-datasourceuseparentfieldorder) to instead use the parent's field order, with new local fields appearing last. You can set [DataSource.showLocalFieldsOnly](#attr-datasourceshowlocalfieldsonly) to have all non-local fields hidden.

Note that **only fields are inherited** - other properties such as dataURL and dataFormat are not. You can use ordinary inheritance, that is, creating a subclass of DataSource, in order to share properties such as dataURL across a series of DataSources that also inherit fields from each other via `inheritsFrom`.

This feature can be used for:

*   creating a customized view (eg, only certain fields shown) which will be used by multiple [databound components](../reference.md#interface-databoundcomponent).
*   adding presentation-specific attributes to metadata that has been automatically derived from [XML Schema](XMLTools.md#classmethod-xmltoolsloadxmlschema) or other metadata formats
*   modeling object subclassing and extension in server-side code and storage systems
*   modeling relational database joins, and the equivalents in other systems
*   creating hooks for others to customize your application in a maintainable way. For example, if you have a dataSource "employee", you can create a dataSource "customizedEmployee" which inherits from "employee" but does not initially define any fields, and bind all [databound components](../reference.md#interface-databoundcomponent) to "customizedEmployee". Customizations of fields (including appearance changes, field order, new fields, hiding of fields, and custom validation rules) can be added to "customizedEmployee", so that they are kept separately from the original field data and have the best possible chance of working with future versions of the "employee" dataSource.

### Groups

- fields

**Flags**: IR

---
## Attr: DataSource.dropUnknownCriteria

### Description
If the criteria applied to a fetch type operation contain fields that are not present in the dataSource, should they be ignored when performing filtering on the client. This property is useful for cases where you custom server logic makes use of criteria values to determine what set of records to return to the client, but the data does not actually have record values for these fields and as such the client-side filtering logic should ignore them.

**Flags**: IR

---
## Attr: DataSource.auditedDataSourceID

### Description
For audit DataSources, this required property specifies the ID of the [audited](#attr-datasourceaudit) DataSource. Automatically populated for [auto-generated](#attr-datasourcegenerateauditds) audit DataSources.

**Flags**: IR

---
## Attr: DataSource.patternMultiWildcard

### Description
When using the [pattern operators](../kb_topics/patternOperators.md#kb-topic-patternoperators) [search operator](../reference.md#type-operatorid), character that matches a series of one or more characters.

Pass multiple strings to provide multiple alternative wildcards.

**Flags**: IR

---
## Attr: DataSource.nullBooleanValue

### Description
If [DataSource.noNullUpdates](#attr-datasourcenonullupdates) is set, the value to use for any boolean field that has a null value assigned on an update operation, and does not specify an explicit [nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue).

### See Also

- [DataSource.noNullUpdates](#attr-datasourcenonullupdates)
- [DataSourceField.nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue)

**Flags**: IR

---
## Attr: DataSource.nullDateValue

### Description
If [DataSource.noNullUpdates](#attr-datasourcenonullupdates) is set, the value to use for any date or time field that has a null value assigned on an update operation, and does not specify an explicit [nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue).

Unlike strings and numbers, there is no "natural" choice for a null replacement value for dates. The default value we have chosen is midnight on January 1st 1970, simply because this is "the epoch" - the value that is returned by calling "new Date(0)"

### See Also

- [DataSource.noNullUpdates](#attr-datasourcenonullupdates)
- [DataSourceField.nullReplacementValue](DataSourceField.md#attr-datasourcefieldnullreplacementvalue)

**Flags**: IR

---
## Attr: DataSource.dataField

### Description
Name of the field that has the most pertinent numeric, date, or enum value, for use when a [DataBoundComponent](../reference.md#interface-databoundcomponent) needs to show a short summary of a record.

For example, for a DataSource of employees, good choices might be the "salary" field, "hire date" or "status" (active, vacation, on leave, etc).

Unlike [DataSource.titleField](#attr-datasourcetitlefield), dataField is not automatically determined in the absence of an explicit setting.

### Groups

- dsSpecialFields

**Flags**: IR

---
## ClassMethod: DataSource.makeFileSpec

### Description
Converts a file path to a [FileSpec](../reference.md#object-filespec).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| path | [String](#type-string) | false | — | The path to convert, e.g. "employees.ds.xml" |

### Returns

`[FileSpec](#type-filespec)` — The equivalent FileSpec, e.g. {fileName: "employees", fileType: "ds", fileFormat: xml"}

### Groups

- fileSource

---
## ClassMethod: DataSource.getDataSource

### Description
Lookup a DataSource by ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [GlobalId](../reference.md#type-globalid) | false | — | DataSource ID |

### Returns

`[DataSource](#type-datasource)` — the DataSource with this ID, if loaded, otherwise null.

---
## ClassMethod: DataSource.flattenCriteria

### Description
Returns new criteria that has at most one top-level LogicalOperator ("and" or "or"). This new criteria will be considered "flat" by [DataSource.isFlatCriteria](#classmethod-datasourceisflatcriteria).

Not all AdvancedCriteria can be flattened and remain logically equivalent. When criteria will be logically modified by flattening, all criteria that appear anywhere in the AdvancedCriteria structure will appear under a single top-level operator, which will be the same top-level operator as the passed AdvancedCriteria.

For example, given criteria like this (in the JSON representation of AdvancedCriteria):

```
      { operator: "and", criteria: [
         { fieldName: "continent", operator: "equals", value: "Europe"},
         { operator: "or", criteria: [
            { fieldName: "countryName", operator: "iEndsWith", value: "land"},
            { fieldName: "population", operator: "lessThan", value: 3000000}
         ]}
        ]
      }
 
```
The returned criteria would be:
```
      { operator: "and", criteria: [
         { fieldName: "continent", operator: "equals", value: "Europe"},
         { fieldName: "countryName", operator: "iEndsWith", value: "land"},
         { fieldName: "population", operator: "lessThan", value: 3000000}
       ]}
 
```
This returned criteria is not logically equivalent to the passed criteria - the "iEndsWith" and "lessThan" criteria that were formerly nested under a logical "or" operator must now _both_ be satisfied instead of _either_ being satisfied. You can use [DataSource.canFlattenCriteria](#classmethod-datasourcecanflattencriteria) to detect whether an AdvancedCriteria is going to be changed by `flattenCriteria()`.

Because the returned criteria may not be logically equivalent, `flattenCriteria` should not be used as a means of simplifying criteria to make server implementation easier or anything of the kind. The primary purpose of returning logically different criteria is to enable an end user to switch from an interface for editing nested criteria to an interface that can't handle nested criteria and convert the criteria while preserving as much as possible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | the AdvancedCriteria to flatten |

### Returns

`[AdvancedCriteria](#type-advancedcriteria)` — flattened criteria

---
## ClassMethod: DataSource.addSearchOperator

### Description
Add a new search operator to all DataSources.

See also [DataSource.addSearchOperator](#method-datasourceaddsearchoperator) for adding operators to specific DataSources only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operator | [Operator](#type-operator) | false | — | definition of the operator to add |

### Groups

- advancedFilter

---
## ClassMethod: DataSource.getSimpleErrors

### Description
Getter method for extracting server-side validation errors for an attempted "update" or "add" operation, as a JS Object where each property name is a field name from the record and each property value is an array of error message strings. For example:
```
     {
         userId : ["A user with this userId already exists"],
         orderId : ["Must be a numeric value", "No Order with ID '6A18294' exists"]
     }
 
```
The Java API DSResponse.addError(fieldName, errorMessage) is used to send server-side errors to the client. See the Java Server Reference for details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | response from which you want to extract the errors |

### Returns

`[Object](../reference.md#type-object)` — Map of fieldName to error messages for the errors included in the DSResponse.

### Groups

- errorHandling

---
## ClassMethod: DataSource.isFlatCriteria

### Description
Returns true if a given AdvancedCriteria is "flat." That is, the criteria consists of either:

*   a top-level "and" or "or" [Criterion](../reference_2.md#object-criterion), where none of the [subcriteria](Criterion.md#attr-criterioncriteria) use [logical operators](../reference_2.md#type-logicaloperator), hence have no subcriteria of their own
*   a single Criterion that is not a logical operator, hence has no subcriteria

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | the AdvancedCriteria to check for flatness |

### Returns

`[boolean](../reference.md#type-boolean)` — true if criteria is flat

---
## ClassMethod: DataSource.loadWithParents

### Description
Variation of [DataSource.load](#classmethod-datasourceload) that will also automatically load any DataSources that the requested DataSources inherit from (via [DataSource.inheritsFrom](#attr-datasourceinheritsfrom)).

If the parent DataSource is already loaded, calling `loadWithParents` will not automatically reload them unless the forceReload parameter is passed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsID | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | DataSource ID or Array of DataSource IDs |
| callback | [Function](#type-function) | false | — | Callback to fire after DataSource loading completes |
| forceReload | [boolean](../reference.md#type-boolean)|[DSLoadSettings](#type-dsloadsettings) | true | — | Forcibly reload a dataSource if it's already loaded |

---
## ClassMethod: DataSource.registerRecordSummaryFunction

### Description
Register a new [RecordSummaryFunction](../reference_2.md#type-recordsummaryfunction). This will then be available by calling [DataSource.applyRecordSummaryFunction](#classmethod-datasourceapplyrecordsummaryfunction) and passing in the `functionName`, or by setting the [ListGridField.recordSummaryFunction](ListGridField.md#attr-listgridfieldrecordsummaryfunction) property of a summary field to `functionName`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| functionName | [String](#type-string) | false | — | identifier for the new record summary function |
| summaryFunction | [Function](#type-function)|[StringMethod](../reference.md#type-stringmethod) | false | — | new summary function implementation. This method takes 3 parameters: `record` (the record for which the summary is being generated), `fields` (an array of the available fields) and `summaryField` (the summary field). |

---
## ClassMethod: DataSource.load

### Description
Load a DataSource or an array of DataSources using the DataSourceLoader servlet. When a callback is specified, this is fired after the DataSources are loaded. The callback is passed a single parameter, the `dsID` list passed into the method. If no loading occurs because the requested DataSource(s) are already loaded, a warning is logged and the callback is fired immediately.

To force reloading of DataSources that have already been loaded, pass `true` for the forceReload parameter. Note that if a DataSource has been created locally with the specified ID, even if this is a [MockDataSource](MockDataSource.md#class-mockdatasource), the `forceReload` parameter will be required to force the "real" dataSource to be loaded.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsID | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | DataSource ID or Array of DataSource IDs |
| callback | [Function](#type-function) | false | — | Callback to fire after DataSource loading completes |
| forceReload | [boolean](../reference.md#type-boolean)|[DSLoadSettings](#type-dsloadsettings) | true | — | Forcibly reload a dataSource if it's already loaded |

---
## ClassMethod: DataSource.convertCriteria

### Description
Converts criteria expressed in SmartClient's simple criteria format to an AdvancedCriteria object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | simple criteria |
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | default style of matching text. Defaults to "substring" |

### Returns

`[AdvancedCriteria](#type-advancedcriteria)` — equivalent AdvancedCriteria object

---
## ClassMethod: DataSource.saveValueViaDataPath

### Description
Helper method to save the argument value inside the argument values record, storing the value at the supplied dataPath, or at the field's declared dataPath if the argument dataPath is null. This method is only of real use when you are dealing with complex nested data via [dataPath](Canvas.md#attr-canvasdatapath); it is obviously a trivial matter to store a field value in a flat record directly.

This method will call the [updateAtomicValue()](SimpleType.md#method-simpletypeupdateatomicvalue) method of custom [SimpleType](SimpleType.md#class-simpletype) fields where this is required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield)|[ListGridField](#type-listgridfield)|[DetailViewerField](#type-detailviewerfield)|[FormItem](#type-formitem) | false | — | Field definition from a dataSource or dataBoundComponent. |
| dataPath | [String](#type-string) | false | — | The dataPath to store the value at. If null, the dataPath will be picked up from the field |
| value | [Any](#type-any) | false | — | The value to save |
| values | [Record](#type-record) | false | — | The valueset in which to save the field value |
| reason | [String](#type-string) | false | — | An optional reason for the save request, to be passed into any [SimpleType.updateAtomicValue](SimpleType.md#method-simpletypeupdateatomicvalue) method - see that API for details |

---
## ClassMethod: DataSource.getSortBy

### Description
Given an array of [SortSpecifier](../reference.md#object-sortspecifier)s, return a simple list of Strings in the format expected by [DSRequest.sortBy](DSRequest.md#attr-dsrequestsortby).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | The list of specifiers to return in sortBy format |

### Returns

`[Array of String](#type-array-of-string)` — An array of sort-definitions in the format expected by [DSRequest.sortBy](DSRequest.md#attr-dsrequestsortby)

---
## ClassMethod: DataSource.combineCriteria

### Description
Combines two criteria (either simple criteria objects or AdvancedCriteria) using the "outerOperator". Note that the combined criteria object will be an AdvancedCriteria unless:

*   both input criteria objects are simple, and
*   the "outerOperator" is "and", and
*   there is no collision of key names on the two criteria

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria1 | [Criteria](../reference_2.md#type-criteria) | false | — | first criteria object |
| criteria2 | [Criteria](../reference_2.md#type-criteria) | false | — | second criteria object |
| outerOperator | [CriteriaCombineOperator](../reference_2.md#type-criteriacombineoperator) | true | — | operator to use to combine the criteria. Defaults to "and" |
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | style of matching text, if it is necessary to convert a simple criteria object to an AdvancedCriteria. Defaults to "substring" |

### Returns

`[Criteria](../reference_2.md#type-criteria)` — The combined criteria

---
## ClassMethod: DataSource.clearValueAtDataPath

### Description
Helper method to save the argument value inside the argument values record, storing the value at the supplied dataPath, or at the field's declared dataPath if the argument dataPath is null. This method is only of real use when you are dealing with complex nested data via [dataPath](Canvas.md#attr-canvasdatapath); it is obviously a trivial matter to store a field value in a flat record directly.

This method will call the [updateAtomicValue()](SimpleType.md#method-simpletypeupdateatomicvalue) method of custom [SimpleType](SimpleType.md#class-simpletype) fields where this is required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield)|[ListGridField](#type-listgridfield)|[DetailViewerField](#type-detailviewerfield)|[FormItem](#type-formitem) | false | — | Field definition from a dataSource or dataBoundComponent. |
| dataPath | [String](#type-string) | false | — | The dataPath at which to clear the value. If null, the dataPath will be picked up from the field |
| values | [Record](#type-record) | false | — | The valueset from which to clear the field value |

---
## ClassMethod: DataSource.applyRecordSummaryFunction

### Description
Applies a [RecordSummaryFunction](../reference_2.md#type-recordsummaryfunction) to a record and returns the result.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| summaryFunction | [RecordSummaryFunction](../reference_2.md#type-recordsummaryfunction) | false | — | The record summary function to execute. |
| record | [Record](#type-record) | false | — | Record to retrieve a summary for. |
| fields | [Array of Field](#type-array-of-field) | false | — | The available fields. |
| summaryField | [DBCField](#type-dbcfield) | false | — | The summary field. |

### Returns

`[Any](#type-any)` — summary value for the record

---
## ClassMethod: DataSource.setLoaderURL

### Description
Sets the URL where the DataSourceLoader servlet has been installed; this is used by the [DataSource.load](#classmethod-datasourceload) method. Note, one reason you may wish to modify the loader URL is to include a Cross-Site Request Forgery (CSRF) token, as described [here](RPCManager.md#classattr-rpcmanageractionurl)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| url | [String](#type-string) | false | — | The new loaderURL |

---
## ClassMethod: DataSource.canFlattenCriteria

### Description
Returns true if calling [DataSource.flattenCriteria](#classmethod-datasourceflattencriteria) on the passed criteria would produce logically equivalent criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | the AdvancedCriteria to check for flatness |

### Returns

`[boolean](../reference.md#type-boolean)` — true if criteria can be flattened without logical change

---
## ClassMethod: DataSource.setTypeOperators

### Description
Set the list of valid [OperatorId](../reference.md#type-operatorid)s for a given FieldType.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [String](#type-string)|[FieldType](../reference_2.md#type-fieldtype) | false | — | — |
| operators | [Array of OperatorId](#type-array-of-operatorid)[] | false | — | available Operators |

### Groups

- advancedFilter

---
## ClassMethod: DataSource.getSortSpecifiers

### Description
Return an array of [SortSpecifier](../reference.md#object-sortspecifier)s, given an array of Strings in the format expected by [DSRequest.sortBy](DSRequest.md#attr-dsrequestsortby).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortBy | [Array of String](#type-array-of-string) | false | — | A list of sortBy strings in the format expected by [DSRequest.sortBy](DSRequest.md#attr-dsrequestsortby) |
| context | [DataSource](#type-datasource)|[DataBoundComponent](#type-databoundcomponent) | true | — | Context dataSource or component. |

### Returns

`[Array of SortSpecifier](#type-array-of-sortspecifier)` — An array of [SortSpecifier](../reference.md#object-sortspecifier)s equivalent to the passed in string array

---
## ClassMethod: DataSource.get

### Description
Synonym of [DataSource.getDataSource](#classmethod-datasourcegetdatasource): Lookup a DataSource by ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [GlobalId](../reference.md#type-globalid) | false | — | DataSource ID |

### Returns

`[DataSource](#type-datasource)` — the DataSource with this ID, if loaded, otherwise null.

---
## ClassMethod: DataSource.copyCriteria

### Description
Create a copy of a criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | criteria to copy |

### Returns

`[Criteria](../reference_2.md#type-criteria)` — copy of criteria

---
## ClassMethod: DataSource.verifyDataSourcePair

### Description
A utility that checks for discrepancies between any two DataSources, typically used to warn about issues commonly found during the Reify design / development cycle, and logs its findings to the console. Similar to the server-side [ReifyDataSourceValidator](server/javadoc/validator) in scope, but with no support for server-only attributes (e.g., Declarative Security).

INFO level messages are logged when any of the following conditions are discovered:

*   A field defined in "live" is not also present in mock
*   A field defined in "live" has a different title than mock (fields using i18n titles are not checked)

WARN level messages are logged when any of the following conditions are discovered:

*   A field defined in mock is not also present in "live"
*   A field defined in mock has a different type than in live (and the live type is a not a sub-type of the mock type)
*   Fields in mock have a different order than in "live" (after ignoring any fields that mock lacks)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| live | [DataSource](#type-datasource) | false | — | DataSource to compare using 'live' rules |
| mock | [DataSource](#type-datasource) | false | — | DataSource to compare using 'mock' rules |

### Returns

`[Array of Object](#type-array-of-object)` — Each message logged, with its fieldName & severity level

---
## ClassMethod: DataSource.getAdvancedCriteriaDescription

### Description
Returns a human-readable string describing the clauses in this advanced criteria or criterion.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria)|[Criterion](#type-criterion) | false | — | Criteria to convert to a readable string |
| dataSource | [DataSource](#type-datasource) | false | — | DataSource to provide definitions of operators |
| criteriaOutputSettings | [CriteriaOutputSettings](#type-criteriaoutputsettings) | true | — | optional configuration settings for the output |

### Returns

`[String](#type-string)` — Human-readable string describing the clauses in the passed criteria

---
## ClassMethod: DataSource.getFieldValue

### Description
Helper method to return the value of the supplied field from within the supplied record, looking up the value from the supplied dataPath. This method is only of real use when you are dealing with complex nested data via [dataPath](Canvas.md#attr-canvasdatapath); it is obviously a trivial matter to obtain a field value from a flat record directly.

If the dataPath is null, this method will follow any [dataPath](ListGridField.md#attr-listgridfielddatapath) specified on the component field instead. In either case, it will also extract [atomic values](SimpleType.md#method-simpletypegetatomicvalue) from custom [SimpleType](SimpleType.md#class-simpletype) fields where this is required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield)|[ListGridField](#type-listgridfield)|[DetailViewerField](#type-detailviewerfield)|[FormItem](#type-formitem) | false | — | Field definition from a dataSource or dataBoundComponent. |
| record | [Record](#type-record) | false | — | The valueset in which to look up the field value |
| dataPath | [String](#type-string) | false | — | Optionally, a string expressing the dataPath to use for value lookup. If null, the dataPath from the field will be used |
| component | [Canvas](#type-canvas) | false | — | Optionally, a component to prvide extra context for the dataPath search. This is typically required if the dataPath traverses a list |
| reason | [String](#type-string) | false | — | An optional reason for the get request, to be passed into any [SimpleType.getAtomicValue](SimpleType.md#method-simpletypegetatomicvalue) method - see that API for details |

### Returns

`[Any](#type-any)` — —

---
## ClassMethod: DataSource.hasCustomTypeOperators

### Description
Returns true if the operator list for the passed type has been customized via a call to [DataSource.setTypeOperators](#method-datasourcesettypeoperators).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [String](#type-string)|[FieldType](../reference_2.md#type-fieldtype) | false | — | — |
| ds | [DataSource](#type-datasource) | false | — | — |

### Groups

- advancedFilter

---
## ClassMethod: DataSource.exportClientData

### Description
Exports arbitrary client-side data, with client-side formatters applied, so is suitable for direct display to users. This method can be used to export data formatted outside of any kind of visual component.

Requires the SmartClient server, but does not rely on any server-side DataSources. If you need to intervene in the export process server-side - for example, if you need to do something not directly supported with the exported object, such as attach it to an email - use the [instance method](#method-datasourceexportclientdata) with an appropriate [OperationBinding](OperationBinding.md#class-operationbinding), as described in the method documentation.

To export unformatted data, see [exportData](#method-datasourceexportdata) which does not include client-side formatters, but requires both the SmartClient server and the presence of server-side DataSources.

Note that field [displayFormat](DataSourceField.md#attr-datasourcefielddateformatter) is honored for "date" and "datetime" fields when exporting direct to Excel; see the displayFormat docs for details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Array of Record](#type-array-of-record) | false | — | Array of Records to export |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Optional callback. Note that this is only applicable if you also specify [exportToClient](DSRequest.md#attr-dsrequestexporttoclient): false in the request properties |

---
## ClassMethod: DataSource.getLoaderURL

### Description
Returns the [loaderURL](#classmethod-datasourcesetloaderurl)

### Returns

`[String](#type-string)` — The loaderURL

---
## ClassMethod: DataSource.getAutoTitle

### Description
Utility method to derive a reasonable user-visible title from an identifier.

The following approach is taken:

*   any underscores (\_) or dollar signs ($) become spaces, except that there will never be either a leading or trailing space.
*   if the fieldName is either entirely uppercase or lowercase, all words separated by spaces are given a leading capital letter. Example USER\_NAME or user\_name -> "User Name".
*   if there is any use of mixed case, camelCaps convention is assumed, and the field name is split into separate words based on 1) everywhere an uppercase letter appears after a lowercase letter 2) everywhere a series of uppercase letters ends. Letter case will not be modified, with the exception that the first word or any word after an underscore will have its first letter capitalized. Examples: useHTTPProxy -> "Use HTTP Proxy", audit\_userName -> "Audit User Name"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| identifier | [String](#type-string) | false | — | identifier for which a title is desired. |

### Returns

`[String](#type-string)` — auto-derived title

### Groups

- title

---
## Method: DataSource.getFieldOperators

### Description
Get the list of [OperatorId](../reference.md#type-operatorid)s available for this field.

By default, if [field.validOperators](DataSourceField.md#attr-datasourcefieldvalidoperators) is set, returns that list, otherwise returns the result of [DataSource.getTypeOperators](#method-datasourcegettypeoperators).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[DataSourceField](#type-datasourcefield) | false | — | Field (or field name) to obtain operators for |

### Returns

`[Array of OperatorId](#type-array-of-operatorid)` — available Operators

### Groups

- advancedFilter

---
## Method: DataSource.createAlias

### Description
Assigns an alias to this DataSource

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| alias | [String](#type-string) | false | — | The alias assigned to this DataSource. |

---
## Method: DataSource.xmlSerialize

### Description
Serialize a JavaScript object as XML.

The JavaScript Object passed to [DataSource.xmlSerialize](#method-datasourcexmlserialize) becomes an XML element named after the [DataSource.tagName](#attr-datasourcetagname) (or [DataSource.ID](#attr-datasourceid) if tagName is unset). Each property of the object becomes a subElement. For example, using a DataSource to serialize like this:

```
     var inputObject = {
        startRow : 5,
        endRow : 50,
        data : [
           { field1 : "value1", field2: new Date() },
           { field1 : "value3", field2: null }
        ]
     };
     var myDS = isc.DataSource.create({ tagName:"DSRequest" });
     myDS.xmlSerialize(inputObject);
 
```
.. produces the following XML:
```
     <DSRequest>
         <startRow>5</startRow>
         <endRow>50</endRow>
         <data>
             <field1>value1</field1>
             <field2>2005-10-14T18:01:16</field2>
         </data>
         <data>
             <field1>value3</field1>
             <field2></field2>
         </data>
     </DSRequest>
 
```

Various properties on the DataSource and DataSourceField can affect how serialization is performed, see for example [DataSource.tagName](#attr-datasourcetagname), [DataSource.schemaNamespace](#attr-datasourceschemanamespace), [DataSourceField.xmlAttribute](DataSourceField.md#attr-datasourcefieldxmlattribute), [DataSourceField.multiple](DataSourceField.md#attr-datasourcefieldmultiple) and [DataSourceField.childTagName](DataSourceField.md#attr-datasourcefieldchildtagname). By setting the [type of a field](DataSourceField.md#attr-datasourcefieldtype) to the ID of another DataSource which has further XML serialization settings, you can control serialization of nested structures.

If you are working with a WSDL-described web service, XML serialization is performed automatically by APIs like [WebService.callOperation](WebService.md#method-webservicecalloperation) - you only need to know about serialization in order to understand how to put together JavaScript data that will fill in an XML message properly, and for simple messages, setting [DSRequest.useFlatFields](DSRequest.md#attr-dsrequestuseflatfields) makes that unnecessary as well.

**Note:** when trying to send data to a web service, it is best to avoid putting together any XML yourself, instead modify the JavaScript data being fed to SmartClient's SOAP engine. This is because the WSDL and SOAP rules for correctly namespacing and encoding Web Service messages are very complex and are subject to change with new versions of the web service you are contacting, whereas the data itself is easy to manipulate and less likely to change.

To troubleshoot message formation, you can set the log category "xmlSerialize" to `INFO` or `DEBUG` level in order to see diagnostics about XML message formation, and you can use the RPC tab in the Developer Console to see the actual messages being passed to web services.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Any](#type-any) | false | — | data to be serialized |
| flags | [SerializationContext](#type-serializationcontext) | false | — | options for the serialization engine |

### Returns

`[String](#type-string)` — data as serialized to XML

**Flags**: A

---
## Method: DataSource.renameFile

### Description
Rename a file stored in this DataSource. Note, if [automatic file versioning](#attr-datasourcefileversionfield) is switched on for the dataSource, all versions of the file are renamed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldFileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat of the file to rename. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. Depending on the configuration of the DataSource, the fileType and fileFormat may be optional. |
| newFileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat to rename the file to. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If the fileType or fileFormat are not provided, then they will not be changed. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Callback executed with the results. The `data` parameter is either an array of records represening the renamed file(s), or null to indicate an error. The records will have their `fileName` fields and `fileType` fields populated, but not the `fileContents` field. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.recordsAreEqual

### Description
Convenience method to test if two records are equal. Testing is done only for the fields defined in the DataSource, anything else is ignored.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record1 | [Any](#type-any) | false | — | record to be compared against. |
| record2 | [Any](#type-any) | false | — | record to be compared. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the records are equal, false otherwise.

---
## Method: DataSource.formatFieldValue

### Description
Formats the supplied value using the [SimpleType](SimpleType.md#class-simpletype) derived from the field definition.

Note that if [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat) is defined for a date, time or numeric-based value, or [DataSourceField.dateFormatter](DataSourceField.md#attr-datasourcefielddateformatter) or [DataSourceField.timeFormatter](DataSourceField.md#attr-datasourcefieldtimeformatter) is defined for a date or time-based value, that format is given priority and used to format the value rather than the `SimpleType`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield)|[FieldName](../reference.md#type-fieldname) | false | — | name of the field to use to format value |
| value | [Any](#type-any) | false | — | raw value to be formatted |

### Returns

`[String](#type-string)` — formatted value or null

---
## Method: DataSource.updateData

### Description
Perform an "update" DataSource operation against this DataSource, to update values in an existing DataSource record.

If a callback was provided, it will be invoked when the operation completes successfully. If the operation fails, the callback will not be invoked unless [DSRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) is true. See the [error handling overview](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| updatedRecord | [Record Properties](#type-record-properties) | false | — | updated record |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.getDataProtocol

### Description
Returns the appropriate [OperationBinding.dataProtocol](OperationBinding.md#attr-operationbindingdataprotocol) for a [DSRequest](../reference.md#object-dsrequest)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | DataSource Request object |

### Returns

`[DSProtocol](../reference_2.md#type-dsprotocol)` — DataProtocol to be used for this request operation.

**Flags**: A

---
## Method: DataSource.getSearchOperator

### Description
Get the [Operator](../reference.md#object-operator) definition for an [OperatorId](../reference.md#type-operatorid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operatorId | [OperatorId](../reference.md#type-operatorid) | false | — | the id of the operator |

### Returns

`[Operator](#type-operator)` — the [Operator](../reference.md#object-operator) definition

### Groups

- advancedFilter

---
## Method: DataSource.viewFile

### Description
Display a file stored in a field of type:"binary" in a new browser window.

This will open a new browser window to show the file. Depending on the file type, the user's installed plugins and applications, and the user's browser settings, this may cause the file to be actually displayed in the new browser window, or may prompt the user to either launch an external application to view the file or save the file to disk.

Note that if this method is called for a record with no associated file, the target window's new URL may not be functional. By default when dataSources encounter a [binary type fields](../reference_2.md#type-fieldtype), an additional field, ``<fieldName>`_filename`, is generated to store the filename for the binary field value. If this field is present in the data source but has no value for this record, developers can assume they're working with a record with no stored file. If this field is not present in some custom dataSource configuration, or the record is not loaded on the client, an additional server transaction may be required to determine whether the record has an associated file before calling this method to view a file.

See the overview of [Binary Fields](../kb_topics/binaryFields.md#kb-topic-binary-fields) for details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record) | false | — | Record to download. Only required to have a value for the primary key field. |
| fieldName | [FieldName](../reference.md#type-fieldname) | true | — | Optional name of the binary field containing the file. If not provided, the first binary field is used. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Additional properties to set on the DSRequest that will be issued. |

---
## Method: DataSource.getFieldOperatorMap

### Description
Get the list of [Operator](../reference.md#object-operator)s available for this field, as a [ValueMap](../reference_2.md#type-valuemap) from [OperatorId](../reference.md#type-operatorid) to the [Operator.title](Operator.md#attr-operatortitle) specified for the [Operator](../reference.md#object-operator), or the corresponding property in [Operators](Operators.md#class-operators) if [Operator.titleProperty](Operator.md#attr-operatortitleproperty) is set.

This valueMap is suitable for use in a UI for building queries, similar to the [FilterBuilder](FilterBuilder.md#class-filterbuilder), and optionally omits operators marked [Operator.hidden](Operator.md#attr-operatorhidden):true.

It is also possible to have this function return only operators of a given [OperatorValueType](../reference_2.md#type-operatorvaluetype), or everything except operators of that type. This is useful, for example, if you want to return all the logical operators (like "and"), or everything except the logical operators.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[DataSourceField](#type-datasourcefield) | false | — | Field (or field name) to obtain operator map for. |
| includeHidden | [boolean](../reference.md#type-boolean) | true | — | whether to include Operators marked hidden:true |
| valueType | [OperatorValueType](../reference_2.md#type-operatorvaluetype) | true | — | If passed, returns only operators of this [OperatorValueType](../reference_2.md#type-operatorvaluetype) |
| omitValueType | [boolean](../reference.md#type-boolean) | true | — | If set, reverses the meaning of the `valueType` parameter, so operators of that [OperatorValueType](../reference_2.md#type-operatorvaluetype) are the only ones omitted |

### Returns

`[ValueMap](../reference_2.md#type-valuemap)` — mapping from [OperatorId](../reference.md#type-operatorid) to title, as described above

### Groups

- advancedFilter

### See Also

- [DataSource.getTypeOperatorMap](#method-datasourcegettypeoperatormap)

---
## Method: DataSource.compareDates

### Description
Convenience method to compare two Date objects appropriately, depending on whether the passed-in fieldName refers to a field of [type](../reference_2.md#type-fieldtype) "datetime" or "date". In the former case, the dates are compared using [DateUtil.compareDates](DateUtil.md#classmethod-dateutilcomparedates); in the latter case, or if the supplied fieldName is null or unknown to this DataSource, the dates are compared using [DateUtil.compareLogicalDates](DateUtil.md#classmethod-dateutilcomparelogicaldates).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date1 | [Date](#type-date) | false | — | First date in comparison |
| date2 | [Date](#type-date) | false | — | Second date in comparison |
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | The name of the field for which the comparison is being run |

### Returns

`[Number](#type-number)` — 0 if equal, -1 if first date > second date, 1 if second date > first date

**Flags**: A

---
## Method: DataSource.setCacheAllData

### Description
Call this method to switch cacheAllData on or off after initialization. Passing a `shouldCache` value of false clears any existing client-side cache, cancels any outstanding requests for a full cache and issues any other pending requests normally.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| shouldCache | [Boolean](#type-boolean) | false | — | New value for [DataSource.cacheAllData](#attr-datasourcecachealldata) |

### Groups

- clientData

---
## Method: DataSource.getCacheData

### Description
Returns the complete set of data cached by this dataSource. Note that this may have been supplied via [DataSource.cacheData](#attr-datasourcecachedata), or may have been fetched from the server for dataSources with [DataSource.cacheAllData](#attr-datasourcecachealldata) set to true.

### Returns

`[Array of Record](#type-array-of-record)` — entire cached set of data

---
## Method: DataSource.hasAllData

### Description
When [DataSource.cacheAllData](#attr-datasourcecachealldata) is true, has all the data been retrieved to the client?

### Returns

`[Boolean](#type-boolean)` — All data has been fetched from the server and is available client-side

### Groups

- clientData

---
## Method: DataSource.getXMLRequestBody

### Description
Get the XML to be posted to the dataURL based on the passed DSRequest.

This API is intended to be overridden in order to integrate with web services that expect XML messages rather than simple HTTP parameters, but lack a WSDL description. For WSDL-described web services, having loaded the service description, SmartClient knows the correct XML message structure, so customization is best done by modifying the JavaScript data that is used to form the message.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | the request to encode as an XML message. |

### Returns

`[String](#type-string)` — the entire XML request as a String, including SOAP envelope if SOAP is used

### See Also

- [XMLTools.loadWSDL](XMLTools.md#classmethod-xmltoolsloadwsdl)

**Flags**: A

---
## Method: DataSource.exportData

### Description
Perform a "fetch" DataSource operation against this DataSource, sending search criteria, retrieving matching records and exporting the results. See [OperationBinding.exportResults](OperationBinding.md#attr-operationbindingexportresults) or [DSRequest.exportResults](DSRequest.md#attr-dsrequestexportresults) and for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion. Note that this parameter only applies where [DSRequest.exportToClient](DSRequest.md#attr-dsrequestexporttoclient) is explicitly set to false, because file downloads do not provide ordinary SmartClient callbacks |

### Groups

- operations

---
## Method: DataSource.getFieldNames

### Description
Retrieves the list of fields declared on this DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| excludeHidden | [boolean](../reference.md#type-boolean) | false | — | If true, returns only those fields that are not marked as hidden |

### Returns

`[Array of FieldName](#type-array-of-fieldname)` — names of all fields declared on this DataSource

---
## Method: DataSource.validateData

### Description
Contacts the server to run server-side validation on a DSRequest and either returns [DSResponse.errors](DSResponse.md#attr-dsresponseerrors) validation errors or a [DSResponse.status](DSResponse.md#attr-dsresponsestatus) code of 0.

A "validate" dsRequest is effectively always [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror):true. It is a normal condition for a "validate" DSResponse to have validation errors and the response will never go to system-wide handling for unexpected errors ([RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Record](#type-record) | false | — | record values to validate |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.convertDataSourceCriteria

### Description
Converts criteria expressed in SmartClient's simple criteria format to an AdvancedCriteria object. This instance method differs from the class method [DataSource.convertCriteria](#classmethod-datasourceconvertcriteria) in that it makes use of the dataSource as schema to help in the conversion. For example, this method is able to honor [DataSourceField.ignoreTextMatchStyle](DataSourceField.md#attr-datasourcefieldignoretextmatchstyle) and use the dataSource's [defaultTextMatchStyle](#attr-datasourcedefaulttextmatchstyle) rather than assuming "substring"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | simple criteria |
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | default style of matching text. Defaults to the dataSource's defaultTextMatchStyle |

### Returns

`[AdvancedCriteria](#type-advancedcriteria)` — equivalent AdvancedCriteria object

---
## Method: DataSource.cloneDSResponse

### Description
Creates a shallow copy of the given [DSResponse](DSResponse.md#class-dsresponse). All properties that would affect the processing of the response are copied into the resulting DSResponse so that the cloned response could substitute for the original response. The response's [data](DSResponse.md#attr-dsresponsedata), if any, is shallow copied in the cloned response.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | the DSResponse to clone. |

### Returns

`[DSResponse](#type-dsresponse)` — a clone of the given DSResponse object.

### See Also

- [DataSource.cloneDSRequest](#method-datasourceclonedsrequest)

**Flags**: A

---
## Method: DataSource.recordsFromText

### Description
Derive a list of Records from Microsoft Excel-compatible tab-separated-values format, using the current DataSource field order, or an explicitly specified list of fields.

If a specified field does not exist in the DataSource, it's assumed the values for that field should end up as Strings.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| text | [String](#type-string) | false | — | records as CSV/TSV (separator can be specified) |
| settings | [TextImportSettings Properties](#type-textimportsettings-properties) | true | — | optional settings for the import |

### Returns

`[Array of Record](#type-array-of-record)` — records derived from TSV

---
## Method: DataSource.dataChanged

### Description
Notification method fired when a DataSource operation such as an [add](#method-datasourceadddata), [remove](#method-datasourceremovedata) or [update](#method-datasourceupdatedata) modifies the underlying data for a DataSource.

This method is used by [ResultSet](ResultSet.md#class-resultset)s to keep the user-visible data up to date as changes are made.

Note: rather than overriding this method, we recommend using [observation](Class.md#method-classobserve) to be notified when it is fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | response from the operation that modified the underlying data set |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | request that initiated the data change |

---
## Method: DataSource.exportClientData

### Description
Exports arbitrary client-side data, with client-side formatters applied, so is suitable for direct display to users. This method can be used to export data formatted outside of any kind of visual component.

If you do not specify an [operationId](OperationBinding.md#attr-operationbindingoperationid) in the `requestProperties` you pass to this method, it behaves exactly the same as the [static classMethod](#classmethod-datasourceexportclientdata) of the same name. If you do specify an `operationId`, the framework expects your DataSource to configure an [OperationBinding](OperationBinding.md#class-operationbinding) of [operationType](OperationBinding.md#attr-operationbindingoperationtype) "clientExport" with the same `operationId`. The framework will then send the `exportClientData` request via the ordinary [DSRequest](../reference.md#object-dsrequest) mechanism, which allows you to use normal framework features in the client data export.

For example, you could add a [DMI declaration](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) to your `operationBinding`, which would allow you to write server-side code that intervenes in the export process - for instance, by calling the `getExportObject()` API to do something special with the export document, like saving it to a database table or sending it to an email list.

When you use the specific `operationId` version of this API, both the SmartClient Server and server-side DataSources are required.

To export unformatted data, see [exportData](#method-datasourceexportdata) which does not include client-side formatters, but requires both the SmartClient server and the presence of server-side DataSources.

Note that field [displayFormat](DataSourceField.md#attr-datasourcefielddateformatter) is honored for "date" and "datetime" fields when exporting direct to Excel; see the displayFormat docs for details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Array of Record](#type-array-of-record) | false | — | Array of Records to export |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Optional callback. Note that this is only applicable if you also specify [exportToClient](DSRequest.md#attr-dsrequestexporttoclient): false in the request properties |

---
## Method: DataSource.applyFilter

### Description
Returns records in the passed Array that match the provided filter [criteria](../reference_2.md#type-criteria). Handles simple or [advanced](../reference.md#object-advancedcriteria) criteria.

By default:

*   any criteria that do not correspond to a DataSource field are ignored
*   for simple criteria, any null or empty string criteria are ignored and all other criteria are passed to [DataSource.fieldMatchesFilter](#method-datasourcefieldmatchesfilter)
*   for advanced criteria, each criterion is evaluated via [DataSource.evaluateCriterion](#method-datasourceevaluatecriterion)

This method is called by [ResultSet.applyFilter](ResultSet.md#method-resultsetapplyfilter) to provide filtering when a ResultSet has a complete cache and filtering can be performed client-side. You may want to override this method in order to mimic the filtering behavior that your server performs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Array of Record](#type-array-of-record) | false | — | the list of rows |
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | the filter criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | optional dataSource request properties |
| startPos | [Integer](../reference_2.md#type-integer) | true | — | starting index - earlier rows are excluded |
| endPos | [Integer](../reference_2.md#type-integer) | true | — | ending index (exclusive) - this row and beyond are excluded |

### Returns

`[Array](#type-array)` — the list of matching rows

---
## Method: DataSource.removeFile

### Description
Remove a file stored in this DataSource. Note, if [automatic file versioning](#attr-datasourcefileversionfield) is switched on for the dataSource, all versions of the file are removed (to remove an individual file version, use the [DataSource.removeFileVersion](#method-datasourceremovefileversion) API).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. Depending the configuration of the DataSource, the fileType and fileFormat may be optional. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Callback executed with the results. The `data` parameter is either an array of records represening the removed file(s), or null to indicate an error. The records will have their `fileName` fields and `fileType` fields populated, but not the `fileContents` field. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.getFieldDefaultOperator

### Description
Get the default [OperatorId](../reference.md#type-operatorid) for this field.

By default, if [field.defaultOperator](DataSourceField.md#attr-datasourcefielddefaultoperator) is set, returns that value, otherwise returns the data-type default from [SimpleType.defaultOperator](SimpleType.md#attr-simpletypedefaultoperator).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[DataSourceField](#type-datasourcefield) | false | — | Field (or field name) to obtain the default operator for |

### Returns

`[Array of OperatorId](#type-array-of-operatorid)` — available Operators

### Groups

- advancedFilter

---
## Method: DataSource.getFile

### Description
Gets the contents of a file stored in this DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType and fileFormat are not provided, will return the first file with the specified fileName. |
| callback | [GetFileCallback](#type-getfilecallback) | false | — | [Callback](Callbacks.md#method-callbacksgetfilecallback) executed with the results. The `data` parameter is either a String with the contents of the file, or null to indicate error (such as file not found). You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.copyRecord

### Description
Copies all DataSource field values of a Record (including a TreeNode) to a new Record, omitting component-specific metadata such as selected state from grids, or parent folders for TreeNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | The record to be copied. |

### Returns

`[Record](#type-record)` — A new copy of the record provided as an argument, with component-specific metata data removed.

---
## Method: DataSource.processResponse

### Description
Process a dsResponse for a request initiated by a DataSource with [dataProtocol:"clientCustom"](OperationBinding.md#attr-operationbindingdataprotocol). `requestId` parameter should be dsRequest.requestId as found on the dsRequest passed to [DataSource.transformRequest](#method-datasourcetransformrequest).

You must provide a response for both error and non-error cases. For an error case, a sufficient response is:

```
 { status : -1 }
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestId | [String](#type-string) | false | — | requestId attribute from the associated dataSource request object |
| dsResponse | [DSResponse Properties](#type-dsresponse-properties) | false | — | Configuration for the dsResponse |

**Flags**: A

---
## Method: DataSource.getFileVersion

### Description
Gets the contents of a particular file version stored in this DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType and fileFormat are not provided, will return the first file with the specified fileName. |
| version | [Date](#type-date) | false | — | A version timestamp. This must exactly match the version timestamp recorded in the DataSource. You can obtain the list of versions for a given file with the [DataSource.listFileVersions](#method-datasourcelistfileversions) API. |
| callback | [GetFileVersionCallback](#type-getfileversioncallback) | false | — | [Callback](Callbacks.md#method-callbacksgetfileversioncallback) executed with the results. The `data` parameter is either a String with the contents of the file, or null to indicate error (such as file not found). You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.getFieldForDataPath

### Description
Return the field definition object corresponding to the supplied dataPath

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataPath | [String](#type-string) | false | — | dataPath of the field to retrieve |

### Returns

`[DataSourceField](#type-datasourcefield)` — field object, or null if no field corresponds to the supplied dataPath

---
## Method: DataSource.getPrimaryKeyFieldName

### Description
Returns the primary key fieldName for this DataSource. If this dataSource has a composite primary key (ie, multiple primaryKey fields), returns just the first primaryKey field name.

### Returns

`[String](#type-string)` — primary key field name

### See Also

- [DataSource.getPrimaryKeyFieldNames](#method-datasourcegetprimarykeyfieldnames)

---
## Method: DataSource.supportsTextMatchStyle

### Description
Does this dataSource support the specified "textMatchStyle" when performing a filter operation against a text field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | false | — | textMatchStyle to check. If passed a null value, assume an exact match is being requested. |

**Flags**: A

---
## Method: DataSource.listFileVersions

### Description
Get the list of a given file's versions from the dataSource, sorted in version order (most recent version first). If the dataSource does not specify a [fileVersionField](#attr-datasourcefileversionfield), this API will return an error

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType and fileFormat are not provided, will return the first file with the specified fileName. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | false | — | Callback executed with the results. The `data` parameter is either an array of records, or null to indicate an error. The records will have the `[fileName](#attr-datasourcefilenamefield)`, `[fileType](#attr-datasourcefiletypefield)`, `[fileFormat](#attr-datasourcefileformatfield)`, `[fileLastModified](#attr-datasourcefilelastmodifiedfield)` and `[fileVersion](#attr-datasourcefileversionfield)` fields populated, but not the `[fileContents](#attr-datasourcefilecontentsfield)` field. (You can use [getFileVersion()](#method-datasourcegetfileversion) to get the `fileContents`). You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.setTestData

### Description
Call this method to set the data in the client-side test-data after initialization.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Array of Record](#type-array-of-record) | false | — | Array of records to apply as the client-side test-data |

### Groups

- clientData

**Deprecated**

---
## Method: DataSource.getAutoTitle

### Description
Return a reasonable user-visible title given a fieldName. Called when [DataSource.autoDeriveTitles](#attr-datasourceautoderivetitles) is true and by default, calls the class method [DataSource.getAutoTitle](#classmethod-datasourcegetautotitle). Override to provide a different policy for auto-deriving titles for a particular DataSource or subclass of DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| identifier | [String](#type-string) | false | — | identifier for which a title is desired. |

### Returns

`[String](#type-string)` — auto-derived title

### Groups

- title

---
## Method: DataSource.saveFile

### Description
Save a file to the DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. Depending on the configuration of the DataSource, the fileType and fileFormat may be optional. |
| contents | [String](#type-string) | false | — | The contents of the file |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Callback executed with the results. The `data` parameter is either a record represening the new file, or null to indicate an error. The record will have its `fileName`, `fileType` and `fileFormat` field populated, but not the `fileContents` field. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.splitCriteria

### Description
Split a criteria apart based on `fields`.

This method will take a simple or [Advanced](../reference.md#object-advancedcriteria) criteria object and extract the subcriteria that apply to the specified array of fields. If passed an AdvancedCriteria, the criteria should be [flat](#classmethod-datasourceisflatcriteria) and the outer operator must be `"and"`.

A new criteria object is returned with any criteria applicable to the specified fields. The passed `criteria` is then modified to remove these fields resulting in two distinct criteria.

To avoid modifying an original criteria, use [DataSource.copyCriteria](#classmethod-datasourcecopycriteria) to make a copy to be passed in.

By default the field-specific criteria returned will be in simple criteria format even if the criteria passed in was Advanced. Developers may suppress this conversion by passing in the `preserveAdvanced` parameter. Note that not every [criterion operator](../reference.md#type-operatorid) can be converted to a simple format. This method will only to convert field level criterion with operators that correspond to one of the available [textMatchStyle](../reference_2.md#type-textmatchstyle) options - namely `"equals"`, `"iEquals"` `"iContains"` or `"startsWith"`.

This method will return an empty criteria object if it was unable to split the specified criteria by the specified fields.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | criteria to be split. May be modified if criteria is extracted. |
| fields | [Array of String](#type-array-of-string) | false | — | list of fields to extract from criteria |
| preserveAdvanced | [Boolean](#type-boolean) | true | — | If passed an AdvancedCriteria, should the returned field-specific split criteria object also be an AdvancedCriteria. |

### Returns

`[Criteria](../reference_2.md#type-criteria)` — extracted criteria

---
## Method: DataSource.getUpdatedData

### Description
Helper method to retrieve the updated data from a successful dataSource update or add operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | Update request object passed to the server. Note that this request may have been modified by [DataSource.transformRequest](#method-datasourcetransformrequest) |
| dsResponse | [DSResponse](#type-dsresponse) | false | — | Response returned by the server |
| useDataFromRequest | [boolean](../reference.md#type-boolean) | false | — | If [DSResponse.data](DSResponse.md#attr-dsresponsedata) is empty, should data be derived from the submitted request. |

### Returns

`[DataSourceRecord](#type-datasourcerecord)|[Array of DataSourceRecords](#type-array-of-datasourcerecords)` — dataUpdated data.

**Flags**: A

---
## Method: DataSource.fetchData

### Description
Perform a "fetch" DataSource operation against this DataSource, sending search criteria and retrieving matching records.

**NOTE:** do not attempt to override this method to create a custom DataSource. For a server-side custom DataSource, use the [DataSource.serverConstructor](#attr-datasourceserverconstructor) attribute, and the *Custom DataSource samples*. For a client-side custom DataSource, see [dataProtocol:"custom"](#attr-datasourcedataprotocol).

In contrast to [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata), which creates a [ResultSet](ResultSet.md#class-resultset) to manage the returned data, calling `dataSource.fetchData()` provides the returned data in the callback as a simple JavaScript Array of JavaScript Objects. Calling `dataSource.fetchData()` does not automatically update any visual components or caches: code in the callback passed to `fetchData()` decides what to do with the returned data.

For example, given a ListGrid "myGrid" and a DataSource "employees", the following code would populate "myGrid" with data fetched from the DataSource:

```
    isc.DataSource.get("employees").fetchData(null, "myGrid.setData(data)");
    
 
```
Unlike calling `myGrid.fetchData()`, which creates a [ResultSet](ResultSet.md#class-resultset), the data provided to the grid is "disconnected" data, unmanaged by SmartClient's databinding facilities and safe to directly modify. This is useful when, for example, a ListGrid is being used as a more sophisticated version of HTML's multi-select component.

Disconnected datasets may be used to populate various visual components. For example, while an individual FormItem can be configured to fetch [valueMap](FormItem.md#attr-formitemvaluemap) options from a DataSource via the [optionDataSource](FormItem.md#attr-formitemoptiondatasource) property, the following code shows storing a dataset to derive valueMaps from later:

```
    
    isc.DataSource.get("countries").fetchData(null, "window.countries = data");

    ... later, a form is created dynamically ...

    function showForm() {
       isc.DynamicForm.create({
           items : [
              { name:"country", title:"Pick Country",
                valueMap: window.countries.getValueMap("countryId", "countryName")
              },
       ...
    
    
 
```

You can also create a ResultSet from the data retrieved from `fetchData()`, like so:

```
    
    isc.DataSource.get("countries").fetchData(null,
        function (dsResponse, data) {
            isc.ResultSet.create({
                dataSource:"countries",
                allRows:data
            })
        }
    )
    
    
 
```

This gives you a dataset that supports client-side filtering (via [setCriteria()](ResultSet.md#method-resultsetsetcriteria)), can provide [filtered valueMaps](ResultSet.md#method-resultsetgetvaluemap), will [automatically reflect updates](ResultSet.md#attr-resultsetdisablecachesync) to the DataSource made via other components, and can be re-used with multiple visual components.

See also [DataSource.getClientOnlyDataSource](#method-datasourcegetclientonlydatasource) and [DataSource.cacheAllData](#attr-datasourcecachealldata) for similar capabilities for dealing with smaller datasets entirely within the browser, or working with modifiable caches representing subsets of the data available from a DataSource.

See also the server-side com.isomorphic.js.JSTranslater class in the *Java Server Reference* for other, similar approaches involving dumping data into the page during initial page load. **Note:** care should be taken when using this approach. Large datasets degrade the basic performance of some browsers, so use [optionDataSource](PickList.md#attr-picklistoptiondatasource) and similar facilities to manage datasets that may become very large.

**Data-Driven Visual Component Creation**

`DataSource.fetchData()` can also be used to create SmartClient components in a data-driven way. Many properties on SmartClient visual components are configured via an Array of Objects - the same data format that `dataSource.fetchData()` returns. These include [ListGrid.fields](ListGrid_1.md#attr-listgridfields), [TabSet.tabs](TabSet.md#attr-tabsettabs), [DynamicForm.items](DynamicForm.md#attr-dynamicformitems), [Facet.values](Facet.md#attr-facetvalues) and even [DataSource.fields](#attr-datasourcefields).

For example, if you had a DataSource "myFormFields" whose fields included the basic properties of [FormItems](FormItem.md#class-formitem) (name, title, type, etc), this example code would create a form based on stored field definitions, loaded from the "myFormFields" DataSource on the fly:

```
    isc.DataSource.get("myFormFields").fetchData(null, 
        "isc.DynamicForm.create({ items:data })"
    )
 
```
This capability to dynamically create visual components from dynamically fetched data provides a foundation for creating interfaces that can be customized by end users. See also the server-side API com.isomorphic.datasource.DataSource.addDynamicDSGenerator() for dynamically creating DataSources supporting all server-side DataSource features, and [DataSource.inheritsFrom](#attr-datasourceinheritsfrom) for sharing field definitions across multiple DataSources.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.setTypeOperators

### Description
Set the list of [OperatorId](../reference.md#type-operatorid)s valid for a given FieldType.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [FieldType](../reference_2.md#type-fieldtype)|[String](#type-string) | false | — | — |
| operators | [Array of OperatorId](#type-array-of-operatorid)[] | false | — | available Operators |

### Groups

- advancedFilter

---
## Method: DataSource.setClientOnly

### Description
Switch into or out of clientOnly mode, taking the cache from the cacheAllData ResultSet if it exists.

### Groups

- clientData

---
## Method: DataSource.getDefaultPathToRelation

### Description
Returns the path having the shortest distance between this and the given targetDS, as determined by [DataSource.getShortestPathToRelation](#method-datasourcegetshortestpathtorelation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetDS | [String](#type-string)|[DataSource](#type-datasource) | false | — | The DataSource at the relationship's other end. |

### Returns

`[RelationPath](#type-relationpath)` — The path having the least number of 1:M relationships from this to the given targetDS.

---
## Method: DataSource.transformRequest

### Description
For a dataSource using [client-side data integration](../kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration), return the data that should be sent to the [DataSource.dataURL](#attr-datasourcedataurl).

By default, HTTP requests sent to non-SmartClient servers do not include DSRequest metadata such as [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow), [endRow](DSRequest.md#attr-dsrequestendrow), and [oldValues](DSRequest.md#attr-dsrequestoldvalues). Only the core [datasource protocol data](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) is sent, such as the criteria passed to [fetchData()](ListGrid_2.md#method-listgridfetchdata) or the updated values submitted by [form.saveData()](DynamicForm.md#method-dynamicformsavedata).

transformRequest() allows you to transform dsRequest metadata into a format understood by your server and include it in the HTTP request, so that you can integrate DataSource features such as data paging with servers that support such features.

How the data is actually sent to the URL is controlled by [OperationBinding.dataProtocol](OperationBinding.md#attr-operationbindingdataprotocol). If using the "getParams" or "postParams" protocol, data is expected to be a JavaScript Object where each property will become a GET or POST'd parameter. If using dataProtocol:"soap" or "postXML", data will be serialized as an XML message by [DataSource.xmlSerialize](#method-datasourcexmlserialize).

As an example, if you have a dataURL that can return paged data given URL parameters "start" and "end", you could implement transformRequest like so:

```
   isc.DataSource.create({
      ... 
      transformRequest : function (dsRequest) {
         if (dsRequest.operationType == "fetch") {
             var params = {
                start : dsRequest.startRow,
                end : dsRequest.endRow
             };
             // combine paging parameters with criteria
             return isc.addProperties({}, dsRequest.data, params);
         }
      }
   });
 
```
Other reasons to implement transformRequest():

*   transform a [Criteria](../reference_2.md#type-criteria) object into the custom query language of a web service
*   add a session id to requests that require authentication
*   detect colliding updates by sending both updated values and the values the user originally retrieved before editing began (available as [DSRequest.oldValues](DSRequest.md#attr-dsrequestoldvalues))

_Special case:_ If the `dataProtocol` is `"clientCustom"` the SmartClient system will not attempt to send data to the server in any way. Instead transformRequest should be implemented such that it accesses or updates the underlying data-set and calls [DataSource.processResponse](#method-datasourceprocessresponse) when the operation is complete. This setting allows straightforward integration with non SmartClient comm mechanisms that directly send requests to the server (such as GWT-RPC), or handle data manipulation without sending HTTP at all (such as Google Gears).  
Developers should not generate a response for a request and call `processResponse()` synchronously from within `transformRequest` as this can lead to unpredictable results. If you're integrating with a synchronous data provider or able to process requests synchronously from data in browser memory, we'd recommend using a [clientOnly dataSource](#attr-datasourceclientonly) with a custom [DataSource.getClientOnlyResponse](#method-datasourcegetclientonlyresponse) implementation instead.

A `transformRequest` override may also be used to set the [DSRequest.dataProtocol](DSRequest.md#attr-dsrequestdataprotocol) to clientCustom at runtime, giving developers a way to intercept normal handling for some particular request, and provide entirely custom handling written on the client.

Note: The [RestDataSource](RestDataSource.md#class-restdatasource) class overrides transformRequest() to handle xml-serializing the request (including meta data) into a standard format.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | the DSRequest being processed |

### Returns

`[Any](#type-any)` — data to be sent to the dataURL

**Flags**: A

---
## Method: DataSource.updateCaches

### Description
Causes any components using this DataSource to be notified of changes that have been made to the remote dataset accessed via this DataSource, as though the provided DSResponse had just successfully completed. This will cause cache managers such as [ResultSet](ResultSet.md#class-resultset) or [ResultTree](ResultTree.md#class-resulttree) to automatically update their caches, and components using such cache managers to visually update to show modified data.

This API should be used when you have found out about changes made by other users or by automatic processes. For example, using the SmartClient [Messaging](Messaging.md#class-messaging) system to receive real-time updates via HTTP streaming, you may get updates that should affect a ListGrid which is using a ResultSet to view a portion of a large dataset.

See the [concurrentEdits](../kb_topics/concurrentEdits.md#kb-topic-handling-concurrent-edits-in-smartclient-datasources) overview for more on handling concurrent edits in SmartClient DataSources.

The provided `DSResponse` should have [operationType](DSResponse.md#attr-dsresponseoperationtype) "update", "add" or "remove" - there is no way for a "fetch" response to meaningfully update arbitrary caches. However, if you have a list of updated records (possibly retrieved via [DataSource.fetchData](#method-datasourcefetchdata)) you can still call `updateCaches()`with DSResponses of type "update". Typically DataSource operations that manipulate data operate on a single record at a time, but if you explicitly set the `response.data` attribute to an array of records, framework code will handle this as it would multiple updates.

Example usage: if you had a ListGrid bound to the `supplyItem` sample DataSource, and that ListGrid was showing a Record with `itemId` 23, and you wanted to update the `unitCost` field to a new value, you would use the following code:  
  
     `// updatedRecord is the record we want to update        var record = supplyItemDS.copyRecord(updatedRecord);        record.unitCost = 500;        var dsResponse = {            data: [record],            operationType: "update"        };        supplyItemDS.updateCaches(dsResponse);`

To cause all components that have cache managers to drop their caches, provide a DSResponse with [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache) set.

As an alternative to calling `updateCaches()` directly, if updates to other DataSources occur as a result of server-side logic, you can use the server-side API DSResponse.addRelatedUpdate(DSResponse) (Pro Edition and above), which ultimately calls `updateCaches()` for you - see that method's documentation for details.

**NOTE:**: if `updateCaches` is called for a [clientOnly](#attr-datasourceclientonly) DataSource, it will update [DataSource.cacheData](#attr-datasourcecachedata) synchronously in addition to notifying all cache managers as normal.

If a DataSource has [DataSource.cacheAllData](#attr-datasourcecachealldata) set and a full cache has been obtained, calling `updateCaches` will automatically update the cache.

Note that the DSResponse provided to this method will **not** go through [DataSource.transformResponse](#method-datasourcetransformresponse) or other processing that would normally occur for a DSResponse resulting from a DSRequest sent by the application in this page.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | the provided DSResponse must minimally have dataSource, operationType, and data set |
| dsRequest | [DSRequest](#type-dsrequest) | true | — | optional dsRequest. If not specified, a DSRequest will be automatically created based on the DataSource and operationType of the DSResponse |

---
## Method: DataSource.transformResponse

### Description
Modify the DSResponse object derived from the response returned from the [dataURL](#attr-datasourcedataurl).

This is an override point that makes it possible to use DataSource features such as paging with web services that support such features, by allowing you to fill in metadata fields in the DSResponse object (such as [DSResponse.startRow](DSResponse.md#attr-dsresponsestartrow)) based on service-specific metadata fields contained in the service's response.

The DSResponse passed to this method already has [DSResponse.data](DSResponse.md#attr-dsresponsedata), which is derived differently depending on the [dataFormat](#attr-datasourcedataformat) setting:

*   `dataFormat:"xml"` : either the [recordXPath](OperationBinding.md#attr-operationbindingrecordxpath) or [recordName](OperationBinding.md#attr-operationbindingrecordname) is used to select the XML elements that represent DataSource records. The selected XML elements are passed to [DataSource.recordsFromXML](#method-datasourcerecordsfromxml), which transforms the XML elements to typed JavaScript data using the DataSource as a schema.
*   `dataFormat:"json"` : the [recordXPath](OperationBinding.md#attr-operationbindingrecordxpath), if specified, is used to select records from the returned JSON data via [XMLTools.selectObjects](XMLTools.md#classmethod-xmltoolsselectobjects). [DataSourceField.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) is used to derive correctly typed field values.
*   `dataFormat:"custom"` : `dsResponse.data` is the raw response in String form. It must be parsed into an Array of Objects for subsequent processing to work.

In addition to `dsResponse.data`, [DSResponse.status](DSResponse.md#attr-dsresponsestatus) is defaulted to 0 (indicating no error), and [DSResponse.startRow](DSResponse.md#attr-dsresponsestartrow) is assumed to be zero, with [endRow](DSResponse.md#attr-dsresponseendrow) and [totalRows](DSResponse.md#attr-dsresponsetotalrows) both set to `dsResponse.data.length - 1`, that is, the returned data is assumed to be all records that matched the filter criteria.

Examples of using this API include:

*   setting [startRow](DSResponse.md#attr-dsresponsestartrow), [endRow](DSResponse.md#attr-dsresponseendrow) and [totalRows](DSResponse.md#attr-dsresponsetotalrows) to allow paging for a service that supports it. For example, if an XML service returns a "resultRow" tag that contained the row number of the first row of the returned results:
    ```
          dsResponse.startRow = isc.XMLTools.selectNumber(xmlData, "//resultRow");
        
    ```
    
*   setting [DSResponse.status](DSResponse.md#attr-dsresponsestatus) to recognized ISC error values based on service-specific errors, in order to trigger standard ISC error handling. For example, setting `dsResponse.status` to [RPCResponse.STATUS_VALIDATION_ERROR](RPCResponse.md#classattr-rpcresponsestatus_validation_error) and filling in [DSResponse.errors](DSResponse.md#attr-dsresponseerrors) in order to cause validation errors to be shown in forms and grids.
*   for services that either do not return cache update data, or return partial data, using [DSRequest.oldValues](DSRequest.md#attr-dsrequestoldvalues) to create cache update data (whether this is appropriate is application-specific), or setting [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache).

NOTE: this method is NOT an appropriate time to call methods on visual components such as grids, initiate new DSRequests or RPCRequests, or in general do anything other than fill in fields on the DSResponse based on data that is already available. Any actions that need to be taken as a result of the web service response should be implemented exactly as for a DataSource where `transformResponse()` has not been overridden, that is, use the callback passed to high-level methods such as [`grid.fetchData()`](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods), and do error handling via either [DataSource.handleError](#method-datasourcehandleerror) or by setting [willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | default DSResponse derived from the response data |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | DSRequest object that initiated this request |
| data | [XMLDocument](../reference.md#type-xmldocument)|[JSON](#type-json) | false | — | XML document or JSON objects returned by the web service |

### Returns

`[DSResponse](#type-dsresponse)` — response derived

**Flags**: A

---
## Method: DataSource.filterData

### Description
Perform a "fetch" DataSource operation against this DataSource, sending search criteria and retrieving matching records.

This is identical to [DataSource.fetchData](#method-datasourcefetchdata) except that [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is set to "substring" to cause case insensitive substring matching (if the server respects this setting).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.removeData

### Description
Perform a "remove" DataSource operation against this DataSource, to delete an existing DataSource record.

If a callback was provided, it will be invoked when the operation completes successfully. If the operation fails, the callback will not be invoked unless [DSRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) is true. See the [error handling overview](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record)|[PrimaryKeys](#type-primarykeys) | false | — | primary key values of record to delete, (or complete record) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.addData

### Description
Perform an "add" DataSource operation against this DataSource, to create a new DataSource record. If a callback was provided, it will be invoked when the operation completes successfully.

If the operation fails, the callback will not be invoked unless [DSRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) is true. See the [error handling overview](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) for more information.

**NOTE:** do not use repeated calls to `addData()` to provide the initial dataset for a [clientOnly](#attr-datasourceclientonly) DataSource, instead, provide initial data via [DataSource.cacheData](#attr-datasourcecachedata). Using `addData()` for subsequent, incremental updates from sources like user editing is fine.

#### Batch inserting
`addData()` can be passed a [List](../reference_2.md#interface-list) of records to insert, rather than a single record. Actual support for this kind of multi-add is entirely dependent on the server-side DataSource implementation; only the built-in `SQLDataSource` has support for multi-add out-of-the-box. If you are using `SQLDataSource` (ie, your dataSource's [serverType](#attr-datasourceservertype) is "sql"), the default behavior of the server when it receives an "add" request with a list of records is to invoke a single-record add on the `DataSource` for each of the records in the provided list.

However, you can also configure the server to generate a true "batch insert", and this will typically be significantly faster. Instead of generating multiple `INSERT` queries, `SQLDataSource` will generate a single `INSERT` with multiple `VALUES`, like so:

```
    INSERT INTO myDataSource (field1, field2, field3)
        VALUES(97, 'test string', 117)
        VALUES(1, 'Another test', 73)
        . . .
        VALUES(8056, 'Final record', 70707)
 
```
Note, the Oracle database product does not support this syntax, so we implement batch insert in a different way - using subselects - with that one database. This difference is transparent from the perspective of a SmartClient developer, and is only mentioned for completeness.

Batch inserting can be configured at the [DSRequest](../reference.md#object-dsrequest), [DataSource](#class-datasource) and [OperationBinding](OperationBinding.md#class-operationbinding) levels, and it can also be globally configured in `server.properties`. See the [multiInsertStrategy](#attr-datasourcemultiinsertstrategy) documentation for details.

#### Cache Synchronization and Audit
This optimized batch insert style of multi-record add only supports [cache synchronization](OperationBinding.md#attr-operationbindingcansynccache) in a limited way, because database products do not provide a reliable way to determine the generated keys of rows inserted in this way. We support cache synchronization of batch-inserted records only when

*   The DataSource does not specify any "sequence" fields, and
*   The `requestValuesPlusSequences` [cacheSyncStrategy](../reference_2.md#type-cachesyncstrategy) is in force

We support [automatic audit](#attr-datasourceaudit) of batch-inserted records only when both of the above conditions are true, and the `sql.multi.insert.allowAudit` flag is set to `true` in your `server.properties` file.

Additionally, be aware that any values missing from the original request data for whatever reason, will also be missing from both the cache-sync data and the audit records.

"Simple" multi-record add, where each record is added with a discrete INSERT, does fully support cache-sync by default, but you may wish to consider turning it off when adding large numbers of records because the extra cache sync fetches can add significantly to the overall operation time (note, this only applies to the default "refetch" cache-sync strategy, so it does not affect the limited cache sync applicable to optimized batch inserts, described above). In fact, the elapsed time of a large multi-record `addData()` operation using "simple" multi-insert is more than doubled with "refecth" cache sync switched on, with all major databases, and it is significantly more than double on some of them. You can switch off cache sync for an operation by setting the [canSyncCache](OperationBinding.md#attr-operationbindingcansynccache) flag to `false` on your `OperationBinding`; alternatively, you can switch to `cacheSyncStrategy` "requestValuesPlusSequences" if that is an option for your use case (ie, you do not have database-generated field values, or can live without them). Note, auditing is not possible if cache sync is completely switched off.

#### Additional notes
Please note a couple of provisos about batch inserting; since batch insert has a specialized and quite narrow set of use cases, we do not currently plan to remove any of these restrictions

*   It is not supported by all database products. The following databases have been tested and verified to work: MySQL/MariaDB, HSQLDB, Microsoft SQL Server, PostgreSQL Oracle and DB/2. Other databases may work, but we do not guaranteee it
*   It is not properly supported with [SQL templating](../kb_topics/customQuerying.md#kb-topic-custom-querying-overview). If you try to make use of **$valuesClause** in a custom querying scenario where batch inserting is in force, you will only get the `valuesClause` applicable to the first valueSet. The same restriction applies to **$values** references in things like [custom SQL expressions](DataSourceField.md#attr-datasourcefieldcustominsertexpression)
*   It does not fully support binary fields. We do support values being sent from the client for fields of type "binary" as Base64-encoded strings, and we also support server-side Java code adding `InputStream` objects to valueSets before the SQL subsystem sees them (for example, by using a [DMI](#attr-datasourceserverobject)). However, we do not support upload of real binary files in a multi-record "add" request, primarily because there is no clear way to discern which of the records the uploaded file(s) belong with

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newRecord | [Record](#type-record) | false | — | new record |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Callback to invoke on completion. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.cloneDSRequest

### Description
Creates a shallow copy of the given [DSRequest](../reference.md#object-dsrequest). The request's [data](DSRequest.md#attr-dsrequestdata), if any, is shallow copied in the cloned request.

The [callback](DSRequest.md#attr-dsrequestcallback) property of the given request is not copied into the cloned request.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | the DSRequest to clone. |

### Returns

`[DSRequest](#type-dsrequest)` — a clone of the given DSRequest object.

### See Also

- [DataSource.cloneDSResponse](#method-datasourceclonedsresponse)

**Flags**: A

---
## Method: DataSource.execute

### Description
Executes the given DSRequest on this DataSource.

This method is typically used by a DataSource whose [dataProtocol](#attr-datasourcedataprotocol) is set to "clientCustom". Execution of a DSRequest can be delayed, either after a timeout or until some condition is met, by saving the DSRequest object passed to the [DataSource.transformRequest](#method-datasourcetransformrequest) override and calling execute() on the DSRequest at a later time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | the DSRequest to execute. |

**Flags**: A

---
## Method: DataSource.getFieldCriterion

### Description
Returns the depth-first match of a criterion matching the given fieldName.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criteria](../reference_2.md#type-criteria) | false | — | the criteria to search |
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | the fieldName to find criteria for |

### Returns

`[Criteria](../reference_2.md#type-criteria)` — the depth-first matching criterion for the passed fieldName

---
## Method: DataSource.copyRecords

### Description
Copies all DataSource field values of an (Array) of Records (including a TreeNode) to a new array of Records, omitting component-specific metadata such as selected state from grids, or parent folders for TreeNodes. This method calls [DataSource.copyRecord](#method-datasourcecopyrecord) for each item in the array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record) | false | — | The array of Record objects to be copied. |

### Returns

`[Array of Record](#type-array-of-record)` — A new copy of each record provided in the array argument, with component-specific metata data removed.

---
## Method: DataSource.useOfflineResponse

### Description
Override point to allow application code to suppress use of a particular offline response. For example, application code may wish to examine the response's [offlineTimestamp](DSResponse.md#attr-dsresponseofflinetimestamp) to make a decision about whether the response is too stale to be useful.

This is an application override point only; there is no default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The dsRequest object |
| dsResponse | [DSResponse](#type-dsresponse) | false | — | The corresponding dsResponse object returned from offline cache |

### Returns

`[boolean](../reference.md#type-boolean)` — true to allow this response to be used, false to prevent it

### Groups

- offlineGroup

---
## Method: DataSource.hasFileVersion

### Description
Indicates whether a particular file version exists in this DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType or fileFormat are not provided, will indicate whether any file with the provided fileName exists. |
| version | [Date](#type-date) | false | — | A version timestamp. This must exactly match the version timestamp recorded in the DataSource for `hasFileVersion` to return true. Note, you can obtain the list of versions for a given file with the [DataSource.listFileVersions](#method-datasourcelistfileversions) API. |
| callback | [HasFileCallback](#type-hasfilecallback) | false | — | [Callback](Callbacks.md#method-callbackshasfileversioncallback) executed with the results. The `data` parameter is a boolean indicating whether the file version is present. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.getClientOnlyResponse

### Description
Return a "spoofed" response for a [clientOnly](#attr-datasourceclientonly) or [DataSource.cacheAllData](#attr-datasourcecachealldata) DataSource.

The default implementation will use [DataSource.cacheData](#attr-datasourcecachedata) to provide an appropriate response, by using [client-side filtering](#method-datasourceapplyfilter) for a "fetch" request, and by modifying the `cacheData` for other requests.

Override this method to provide simulations of other server-side behavior, such as modifying other records, or to implement **synchronous** client-side data providers (such as Google Gears). For **asynchronous** third-party data providers, such as GWT-RPC, HTML5 sockets, or bridges to plug-in based protocols (Java, Flash, Silverlight..), use [dataProtocol:"clientCustom"](../reference_2.md#type-dsprotocol) instead.

Overriding this method is also a means of detecting that a normal DataSource (not clientOnly) would be contacting the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [DSRequest](#type-dsrequest) | false | — | DataSource request to respond to |
| serverData | [Array of Record](#type-array-of-record) | false | — | for cacheAllData DataSources, the data from the local cache |

### Returns

`[DSResponse](#type-dsresponse)` — —

---
## Method: DataSource.fieldMatchesFilter

### Description
Compares a criteria value to a field value and returns whether they match, as follows:

*   any non-String filter value is directly compared (==) to the field value
*   any String filter value is compared according to [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) in the passed `requestProperties`, regardless of the actual field type
*   if the filter value is an Array, the comparison is a logical OR. If textMatchStyle is "exact", it matches if fieldValue (or any of it's entries, if it's also an array) is contained in the filterValue Array. If textMatchStyle if substring, it matches if any of the entries in filterValue appear as a case-insensitive substring of any of the entries in fieldValue.
*   Dates are compared as logical dates if either the field value or the filter value is a logical date. Only if none of them is a logical date they will be compared as standard Dates

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldValue | [Any](#type-any) | false | — | field value to be compared |
| filterValue | [Any](#type-any) | false | — | filter value to be compared |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | optional dataSource request properties |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the filter and field values match, false otherwise

---
## Method: DataSource.setCacheData

### Description
Call this method to set the data in the client-side cache after initialization.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Array of Record](#type-array-of-record) | false | — | Array of records to apply as the client-side cache |

### Groups

- clientData

---
## Method: DataSource.performCustomOperation

### Description
Invoke an operation declared with [OperationBinding.operationType](OperationBinding.md#attr-operationbindingoperationtype) "custom".

**This is a rarely used API.** If the operation you are performing can be thought of as one of the standard "CRUD" [operation types](../reference.md#type-dsoperationtype), declare it with a CRUD operationType. For example, if your operation updates a record, declare it with operationType "update" and invoke it via [DataSource.updateData](#method-datasourceupdatedata) - this will cause [cache sync](ResultSet.md#class-resultset) to work correctly.

In particular:

*   do not use this API just because you need to add additional server-side logic to a CRUD operation ([DMI](DMI.md#class-dmi) allows this)
*   do not use this API to implement variants of core CRUD operations ([DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) is the correct way to do this)
*   do not use this API just because an operation affects more than one record. Most kinds of multi-record operations should use [queuing](RPCManager.md#classmethod-rpcmanagerstartqueue). However, a custom operation _is_ appropriate for genuine "batch" updates, as opposed to just a number of ordinary updates by primaryKey - see [OperationBinding.allowMultiUpdate](OperationBinding.md#attr-operationbindingallowmultiupdate)
*   do not use this API just because you are calling a stored procedure in SQL - if the stored procedure performs some kind of CRUD operation on the records of this DataSource, use a standard CRUD operationType

Instead, the specific purpose of this API is to bypass all checks and side effects that normally occur for CRUD operations, for example, that a "fetch" requires valid Criteria or that an "update" or "remove" operation contains a valid primary key, or that an "add" operation returns the newly added record. `performCustomOperation` allows you to pass an arbitrary Record to the server, act on it with custom code, and return arbitray results or even no results.

The "data" parameter becomes [dsRequest.data](DSRequest.md#attr-dsrequestdata). With the SmartClient Server Framework, the data is accessible server-side via DSRequest.getValues() and in [Velocity templates](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables) (such as `<customSQL>`) as $values.

Note that with SQLDataSource, `performCustomOperation` must be used if you plan to have a `<customSQL>` tag in your operationBinding that will execute SQL operations other than SELECT, UPDATE, INSERT, DELETE (such as creating a new table). By declaring [OperationBinding.operationType](OperationBinding.md#attr-operationbindingoperationtype) "custom" in your .ds.xml file, all checks related to normal CRUD operations will be skipped and your `<customSQL>` can do arbitrary things.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationId | [String](#type-string) | false | — | the operation ID |
| data | [Record Properties](#type-record-properties) | true | — | data to pass to the server. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- operations

---
## Method: DataSource.getPrimaryKeyFieldNames

### Description
Returns a list of the names of this DataSource's [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) fields.

### Returns

`[Array of String](#type-array-of-string)` — The list of the names of this datasource's primaryKey fields

### See Also

- [DataSource.getPrimaryKeyFields](#method-datasourcegetprimarykeyfields)

---
## Method: DataSource.hasCustomTypeOperators

### Description
Returns true if the operator list for the passed type has been customized via a call to [DataSource.setTypeOperators](#method-datasourcesettypeoperators).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [String](#type-string)|[FieldType](../reference_2.md#type-fieldtype) | false | — | — |

### Groups

- advancedFilter

---
## Method: DataSource.removeFileVersion

### Description
Remove a particular file version stored in this DataSource. Any other versions of the file are left untouched.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType and fileFormat are not provided, will return the first file with the specified fileName. |
| version | [Date](#type-date) | false | — | A version timestamp. This must exactly match the version timestamp recorded in the DataSource. You can obtain the list of versions for a given file with the [DataSource.listFileVersions](#method-datasourcelistfileversions) API. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Callback executed with the results. The `data` parameter is either a record representing the removed file version, or null to indicate an error. The record will have its `[fileName](#attr-datasourcefilenamefield)`, `[fileType](#attr-datasourcefiletypefield)`, `[fileFormat](#attr-datasourcefileformatfield)`, `[fileLastModified](#attr-datasourcefilelastmodifiedfield)`, and `[fileVersion](#attr-datasourcefileversionfield)` fields populated, but not the `[fileContents](#attr-datasourcefilecontentsfield)` field. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.getPrimaryKeyField

### Description
Returns a pointer to the primaryKey field for this DataSource. If this dataSource has a composite primary key (ie, multiple primaryKey fields), returns just the first primaryKey field.

### Returns

`[DataSourceField](#type-datasourcefield)` — primary key field object

### See Also

- [DataSource.getPrimaryKeyFields](#method-datasourcegetprimarykeyfields)

---
## Method: DataSource.getShortestPathToRelation

### Description
Returns the path having the shortest distance between this and the given targetDS. In case of a tie, only the first as determined by depth-first search is returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetDS | [String](#type-string)|[DataSource](#type-datasource) | false | — | The DataSource at the relationship's other end. |

### Returns

`[RelationPath](#type-relationpath)` — The path having the least number of 1:M relationships from this to the given targetDS.

---
## Method: DataSource.compareCriteria

### Description
Given two sets of criteria, determine whether they are equivalent, the new criteria is guaranteed more restrictive, or the new criteria is not guaranteed more restrictive, returning 0, 1 or -1 respectively.

Comparisons between [AdvancedCriteria](../reference.md#object-advancedcriteria) are made via recursively calling [Operator.compareCriteria](Operator.md#method-operatorcomparecriteria) for all criteria involved.

For simple [Criteria](../reference_2.md#type-criteria), by default ([CriteriaPolicy](../reference_2.md#type-criteriapolicy):"dropOnShortening"), returns:

*   \-1 if the new criteria has fewer properties than the old criteria (indicating that it isn't more restrictive)
*   \-1 if the value for any property in the old criteria is an array and 1) the value for the same property in the new criteria isn't an array, or 2) is an array but of different length, or 3) the arrays do not contain the exact same set of objects (order can be different)
*   \-1 if the value for any given property in the old criteria is not an array, and the the value for the same property property in the new criteria is different
*   \-1 if both values for a given property are strings and the new criteria value doesn't contain the old criteria value
*   1 if none of the above are true and, for at least one of the properties, the respective criteria values are both strings, and the old criteria value is a substring of, and is shorter than, the new criteria value
*   0 otherwise (indicating the sets of criteria are equivalent)

For ([CriteriaPolicy](../reference_2.md#type-criteriapolicy):"dropOnChange"), returns:

*   \-1 if the two sets of criteria have a different number of properties
*   \-1 if the value for any property in the old criteria is an array and 1) the value for the same property in the new criteria isn't an array, or 2) is an array but of different length, or 3) the arrays do not contain the exact same set of objects (order can be different)
*   \-1 if the value for any given property in the old criteria is not an array, and the the value for the same property in the new criteria is different
*   0 otherwise (indicating the sets of criteria are equivalent)

This method is called by [ResultSet.compareCriteria](ResultSet.md#method-resultsetcomparecriteria) to determine whether a change in criteria should cause the cache to be invalidated. You may want to override this method in order to mimic the filtering behavior that your server performs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new filter criteria |
| oldCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | previous filter criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | dataSource request properties |
| policy | [String](#type-string) | true | — | overrides [CriteriaPolicy](../reference_2.md#type-criteriapolicy) |

### Returns

`[Number](#type-number)` — 0 if the filters are equivalent, 1 if newCriteria is guaranteed more restrictive, and -1 if newCriteria is not guaranteed more restrictive

### See Also

- [CriteriaPolicy](../reference_2.md#type-criteriapolicy)

---
## Method: DataSource.getTypeOperators

### Description
Get the list of [OperatorId](../reference.md#type-operatorid)s available on this DataSource for the given [FieldType](../reference_2.md#type-fieldtype).

If [DataSource.setTypeOperators](#method-datasourcesettypeoperators) has been called for this DataSource and FieldType, returns that list, otherwise, returns the set of valid operators for the [FieldType](../reference_2.md#type-fieldtype) as specified by [SimpleType.validOperators](SimpleType.md#attr-simpletypevalidoperators), otherwise, the system-wide set of valid operators for the type as registered via [DataSource.addSearchOperator](#classmethod-datasourceaddsearchoperator).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [FieldType](../reference_2.md#type-fieldtype)|[String](#type-string) | true | — | Defaults to "text" if not passed. |

### Returns

`[Array of OperatorId](#type-array-of-operatorid)` — available Operators

### Groups

- advancedFilter

---
## Method: DataSource.getField

### Description
Return the field definition object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | Name of the field to retrieve |

### Returns

`[DataSourceField](#type-datasourcefield)` — field object

---
## Method: DataSource.listFiles

### Description
Get a list of files from the DataSource. Note, if [automatic file versioning](#attr-datasourcefileversionfield) is switched on for the dataSource, the resulting list contains only the most recent version of each file.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | Criteria to apply. References to `fileName`, `fileType` and `fileFormat` fields will be translated to the native field names configured for this DataSource. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | false | — | Callback executed with the results. The `data` parameter is either an array of records, or null to indicate an error. The records will have the `[fileName](#attr-datasourcefilenamefield)`, `[fileType](#attr-datasourcefiletypefield)`, `[fileFormat](#attr-datasourcefileformatfield)`, `[fileLastModified](#attr-datasourcefilelastmodifiedfield)`, and `[fileVersion](#attr-datasourcefileversionfield)` fields populated, but not the `[fileContents](#attr-datasourcefilecontentsfield)` field. (You can use [getFile()](#method-datasourcegetfile) to get the `fileContents`). You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

### See Also

- [DataSource.listFileVersions](#method-datasourcelistfileversions)

---
## Method: DataSource.getFetchDataURL

### Description
Returns a URL to DataSource fetch operation. This API is intended to return media such as images or videos to the browser.

Note that because the entirety of the request is encoded in the URL, there is an inherent limitation on the amount of data that you can send viat he criteria argument to the server. The actual length depends on your server configuration and other factors such as the size of cookies (if any) being sent to the server and other HTTP headers in use. Conservatively, assume that you have about 2 kilobytes to work with.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | Criteria to be sent to server. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Returns

`[String](#type-string)` — a URL that targets the specified fetch operation.

---
## Method: DataSource.getAllPathsToRelation

### Description
Returns all known paths between this and the given targetDS.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetDS | [String](#type-string)|[DataSource](#type-datasource) | false | — | The DataSource at the relationship's other end. |

### Returns

`[RelationPath](#type-relationpath)` — Array ofAll known paths between this and the given targetDS.

---
## Method: DataSource.getFileURL

### Description
Returns a direct URL to access a file stored in a field of type:"binary".

This URL can be used as the "src" attribute of an Img widget or `<img>` tag (if the file is an image), or can be used in an ordinary HTML link (`<a>` tag) to download the file. However, for the latter use case, see also [DataSource.downloadFile](#method-datasourcedownloadfile) and [DataSource.viewFile](#method-datasourceviewfile).

The URL returned is not to a static file on disk, rather, the returned URL essentially encodes a DSRequest as URL parameters, in a format understood by the IDACall servlet that comes with the Server Framework.

Hence, this URL will dynamically retrieve whatever file is currently stored in the binary field via executing a normal DSRequest server side. The request will run through normal security checks, so if your application requires authentication, the user must have a valid session and be authorized to access the binary field.

Note that if this method is called for a record with no associated file, the returned URL may not be functional. By default when dataSources encounter a [binary type fields](../reference_2.md#type-fieldtype), an additional field, ``<fieldName>`_filename`, is generated to store the filename for the binary field value. If this field is present in the data source but has no value for this record, developers can assume they're working with a record with no stored file. If this field is not present in some custom dataSource configuration, or the record is not loaded on the client, an additional server transaction may be required to determine whether the record has an associated file before calling this method to retrieve a download URL.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record)|[PKValue](#type-pkvalue) | false | — | Record containing at least the primary key field, or just the value of the primary key field. |
| fieldName | [FieldName](../reference.md#type-fieldname) | true | — | Optional name of the binary field containing the file. If not provided, the first binary field is used. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Additional properties to set on the DSRequest that will be issued. |

### Returns

`[String](#type-string)` — a URL to directly access the stored file

---
## Method: DataSource.recordsAsText

### Description
Converts a list of Records to simple text formats with a Record per line and values separated by a configurable separator, including both tab-separated-values and comma-separated-values (aka CSV).

In addition to the `settings` parameter for this method, [DataSourceField.exportForceText](DataSourceField.md#attr-datasourcefieldexportforcetext) can be set.

If two or more different text exports are needed for the same DataSource creating a conflict for any DataSourceField setting, [DataSource.inheritsFrom](#attr-datasourceinheritsfrom) can be used to create a child DataSource where these settings can be changed without recapitulating all field definitions.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record) | false | — | records to convert |
| settings | [TextExportSettings Properties](#type-textexportsettings-properties) | true | — | settings for the export |

### Returns

`[String](#type-string)` — records as CSV/TSV (separator can be specified)

---
## Method: DataSource.fetchRecord

### Description
Fetch a single record from the DataSource by [primary key](DataSourceField.md#attr-datasourcefieldprimarykey). This simply calls [DataSource.fetchData](#method-datasourcefetchdata) after creating [Criteria](../reference_2.md#type-criteria) that contain the primary key field and value.

If you call this method on a DataSource with a composite primary key - ie, one with multiple primaryKey fields - this method returns the first record where the first defined primary field matches the supplied pkValue; this may or may not be meaningful, depending on your use case. Generally, for DataSources with composite keys, it makes more sense to use `fetchData()` directly, rather than this convenience method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pkValue | [Any](#type-any) | false | — | value for the field marked [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey):true in this DataSource (or the first field so marked if there is more than one) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

---
## Method: DataSource.supportsAdvancedCriteria

### Description
Do fetch and filter operations on this dataSource support being passed [AdvancedCriteria](../reference.md#object-advancedcriteria)?

For a DataSource to support being passed AdvancedCriteria, it must be [clientOnly:true](#attr-datasourceclientonly) or [cacheAllData:true](#attr-datasourcecachealldata), or have server side logic which can process AdvancedCriteria objects passed from the client.

AdvancedCriteria are supported on the server for standard [SQL](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources), [Hibernate](../kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) and [JPA](../kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa) DataSources in SmartClient Enterprise or Power editions (not supported in SmartClient Pro).

The framework assumes that custom dataSources support AdvancedCriteria; if you have a a custom DataSource implementation that does not support AdvancedCriteria, you can set the [DataSource.allowAdvancedCriteria](#attr-datasourceallowadvancedcriteria) property to false.

### Returns

`[Boolean](#type-boolean)` — true if this dataSource supports being passed AdvancedCriteria in fetch and filter type operations, false otherwise.

---
## Method: DataSource.getDisplayValue

### Description
Given a fieldName and a dataValue, apply any [DataSourceField.valueMap](DataSourceField.md#attr-datasourcefieldvaluemap) for the field and return the display value for the field

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | name of the field to retrieve a value for |
| value | [Any](#type-any) | false | — | data value for the field |

### Returns

`[Any](#type-any)` — display value for the field

---
## Method: DataSource.isCalculated

### Description
Does the specified field have its value dynamically calculated?

This method will return true if the field has explicitly been marked as [calculated:true](DataSourceField.md#attr-datasourcefieldcalculated).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield)|[String](#type-string) | false | — | Field or fieldName |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a field with dynamically calculated values

---
## Method: DataSource.handleError

### Description
If you define this method on a DataSource, it will be called whenever the server returns a DSResponse with a status other than [RPCResponse.STATUS_SUCCESS](RPCResponse.md#classattr-rpcresponsestatus_success). You can use this hook to do DataSource-specific error handling. Unless you return `false` from this method, [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror) will be called by SmartClient right after this method completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [DSResponse](#type-dsresponse) | false | — | the DSResponse or DSResponse object returned from the server |
| request | [DSRequest](#type-dsrequest) | false | — | the DSRequest or DSRequest that was sent to the server |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror)

### Groups

- errorHandling

### See Also

- [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror)

**Flags**: A

---
## Method: DataSource.hasFile

### Description
Indicates whether a file exists in this DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileSpec | [FileSpec](#type-filespec)|[String](#type-string) | false | — | Either a FileSpec, or a String which will be parsed to determine the fileName, fileType and fileFormat. For instance, "employees.ds.xml" would be parsed as {fileName: "employees", fileType: "ds", fileFormat: "xml"}. If fileType or fileFormat are not provided, will indicate whether any file with the provided fileName exists. |
| callback | [HasFileCallback](#type-hasfilecallback) | false | — | [Callback](Callbacks.md#method-callbackshasfilecallback) executed with the results. The `data` parameter is a boolean indicating whether the file is present. You can examine `[dsResponse.status](DSResponse.md#attr-dsresponsestatus)` and `[dsResponse.data](DSResponse.md#attr-dsresponsedata)` for additional information about any error. |

### Groups

- fileSource

---
## Method: DataSource.convertRelativeDates

### Description
Takes all relative date values found anywhere within a Criteria / AdvancedCriteria object and converts them to concrete date values, returning the new criteria object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | criteria to convert |
| timezoneOffset | [String](#type-string) | true | — | optional timezone offset. Defaults to the current timezone |
| firstDayOfWeek | [Integer](../reference_2.md#type-integer) | true | — | first day of the week (zero is Sunday). Defaults to [DateChooser.firstDayOfWeek](DateChooser.md#attr-datechooserfirstdayofweek) |
| baseDate | [Date](#type-date) | true | — | base value for relative conversion - defaults to now |

### Returns

`[Criteria](../reference_2.md#type-criteria)` — new copy of the criteria with all relative dates converted

---
## Method: DataSource.addSearchOperator

### Description
Add a new search operator, only to this DataSource.

If an existing [Operator](../reference.md#object-operator) is passed, restricts the set of FieldTypes to which that operator can be applied in this DataSource.

See also [DataSource.addSearchOperator](#classmethod-datasourceaddsearchoperator) for adding operators to all DataSources.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operator | [Operator](#type-operator) | false | — | definition of the operator to add |
| types | [Array of FieldType](#type-array-of-fieldtype) | true | — | types to which this operator applies |

### Groups

- advancedFilter

---
## Method: DataSource.invalidateCache

### Description
Drop the current dataSource cache. This has two effects:

*   For DataSources [DataSource.cacheAllData](#attr-datasourcecachealldata) or [clientOnly](#attr-datasourceclientonly), discard the current client-side cache data.
*   If `notify` is passed, cause all [data objects](ResultSet.md#class-resultset) associated with this dataSource to drop their caches. This occurs regardless of the dataSource type - and can be thought of as equivalent to processing a response with [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache) set.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| notify | [boolean](../reference.md#type-boolean) | true | — | Should data objects associated with this dataSource have their cache invalidated? |

### Groups

- clientData

---
## Method: DataSource.downloadFile

### Description
Download a file stored in a field of type:"binary" in a DataSource record.

This will trigger the browser's "Save As" dialog and allow the user to save the file associated with some record.

Note that if this method is called for a record with no associated file, the download URL may not be functional. By default when dataSources encounter a [binary type fields](../reference_2.md#type-fieldtype), an additional field, ``<fieldName>`_filename`, is generated to store the filename for the binary field value. If this field is present in the data source but has no value for this record, developers can assume they're working with a record with no stored file. If this field is not present in some custom dataSource configuration, or the record is not loaded on the client, an additional server transaction may be required to determine whether the record has an associated file before calling this method to download a file.

See the overview of [Binary Fields](../kb_topics/binaryFields.md#kb-topic-binary-fields) for more details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record) | false | — | Record to download. Only required to have a value for the primary key field. |
| fieldName | [FieldName](../reference.md#type-fieldname) | true | — | Optional name of the binary field containing the file. If not provided, the first binary field is used. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Additional properties to set on the DSRequest that will be issued. |

---
## Method: DataSource.getClientOnlyDataSource

### Description
Produces a clientOnly "copy" of a particular subset of data from a normal DataSource, via calling fetchData() to fetch matching rows, and constructing a clientOnly DataSource that [DataSource.inheritsFrom](#attr-datasourceinheritsfrom) the original DataSource.

This clientOnly "copy" can be useful in situations where you want to allow a series of local changes without immediately committing to the server. See also [ListGrid.autoSaveEdits](ListGrid_1.md#attr-listgridautosaveedits) for more fine-grained tracking of edits (eg, special styling for uncommitted changes).

The new DataSource is returned via the "callback" argument. If [DataSource.cacheAllData](#attr-datasourcecachealldata) is enabled and [DataSource.hasAllData](#method-datasourcehasalldata) returns true, the new DataSource is synchronously returned as the result of the method. In this case, if a callback was passed, it also is executed synchronously.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | The criteria for the clientOnly DS |
| callback | [ClientOnlyDataSourceCallback](#type-clientonlydatasourcecallback) | false | — | The callback to fire passing the clientOnly DS |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | optional properties to pass through to the DSRequest |
| dataSourceProperties | [DataSource Properties](#type-datasource-properties) | true | — | optional properties to pass through to the clientOnly DS |

---
## Method: DataSource.getPrimaryKeyFields

### Description
Returns this DataSource's [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) fields as a map of fieldName to field.

### Returns

`[Record](#type-record)` — Javascript object containing all this datasource's primaryKey fields, as a map of field name to field

### See Also

- [DataSource.getPrimaryKeyField](#method-datasourcegetprimarykeyfield)
- [DataSource.getPrimaryKeyFieldNames](#method-datasourcegetprimarykeyfieldnames)

---
## Method: DataSource.getTypeOperatorMap

### Description
Get the list of [Operator](../reference.md#object-operator)s available for this [FieldType](../reference_2.md#type-fieldtype), as a [ValueMap](../reference_2.md#type-valuemap) from [OperatorId](../reference.md#type-operatorid) to the [Operator.title](Operator.md#attr-operatortitle) specified for the [Operator](../reference.md#object-operator), or the corresponding property in [Operators](Operators.md#class-operators) if [Operator.titleProperty](Operator.md#attr-operatortitleproperty) is set.

This valueMap is suitable for use in a UI for building queries, similar to the [FilterBuilder](FilterBuilder.md#class-filterbuilder), and optionally omits operators marked [Operator.hidden](Operator.md#attr-operatorhidden) : true.

It is also possible to have this function return only operators of a given [OperatorValueType](../reference_2.md#type-operatorvaluetype), or everything except operators of that type. This is useful, for example, if you want to return all the logical operators (like "and"), or everything except the logical operators.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [FieldType](../reference_2.md#type-fieldtype) | true | — | Type to obtain operator map for. Defaults to "text" if not passed. |
| includeHidden | [boolean](../reference.md#type-boolean) | true | — | whether to include Operators marked hidden:true |
| valueType | [OperatorValueType](../reference_2.md#type-operatorvaluetype) | true | — | If passed, returns only operators of this [OperatorValueType](../reference_2.md#type-operatorvaluetype) |
| omitValueType | [boolean](../reference.md#type-boolean) | true | — | If set, reverses the meaning of the `valueType` parameter, so operators of that [OperatorValueType](../reference_2.md#type-operatorvaluetype) are the only ones omitted |

### Returns

`[ValueMap](../reference_2.md#type-valuemap)` — mapping from [OperatorId](../reference.md#type-operatorid) to title, as described above

### Groups

- advancedFilter

### See Also

- [DataSource.getFieldOperatorMap](#method-datasourcegetfieldoperatormap)

---
## Method: DataSource.getLegalChildTags

### Description
For a DataSource that describes a DOM structure, the list of legal child elements that can be contained by the element described by this DataSource.

For a DataSource described by XML schema, this is the list of legal subelements **of complexType** (elements of simpleType become DataSourceFields with atomic type).

Note that currently, if an XML schema file contains ordering constraints, DataSources derived from XML Schema do not capture these constraints.

### Groups

- xmlSchema

---
## Method: DataSource.evaluateCriterion

### Description
Evaluate the given criterion with respect to the passed record.

Typically called by the [condition](Operator.md#method-operatorcondition) function of a custom [Operator](../reference.md#object-operator) to evaluate [sub-criteria](Criterion.md#attr-criterioncriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record to evaluate |
| criterion | [Criterion](#type-criterion) | false | — | criterion to use |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the record meets the supplied [Criterion](../reference_2.md#object-criterion)

### Groups

- advancedFilter

---
