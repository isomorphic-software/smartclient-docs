# Direct Method Invocation

[← Back to API Index](../reference.md)

---

## KB Topic: Direct Method Invocation

### Description
Direct Method Invocation (DMI) allows Ajax requests from the UI to directly invoke methods on server-side objects via XML configuration. See also [DMI Scripts](../classes/OperationBinding.md#attr-operationbindingscript), which allows you to place code directly into the XML file instead of in a separate .java file; this is a useful approach when DMI code is short.

When using DMI, request data from the UI is translated to Java objects and passed to the Java method you designate with an XML declaration. Your Java method simply declares the parameters it needs and they are automatically provided (see "Method Invocation" below). The return value of your method is automatically wrapped as a valid response and delivered to the browser.

DMI requires the [SmartClient Server](iscServer.md#kb-topic-smartclient-server-summary). Note that SmartClient also supports several approaches for interacting with [non-Java backends](nonJavaBackend.md#kb-topic-net-php-serverless-integration) and/or Java backends not running the ISC server.

**DataSource DMI**  
See also [Server DataSource Integration](serverDataIntegration.md#kb-topic-server-datasource-integration) overview.  
To enable DMI for a given DataSource, simply include a ``<serverObject>`` configuration block in that DataSource's configuration either at [DataSource.serverObject](../classes/DataSource.md#attr-datasourceserverobject) or on a particular operationBinding via [OperationBinding.serverObject](../classes/OperationBinding.md#attr-operationbindingserverobject). The ServerObject specifies the target of the method invocation and [OperationBinding.serverMethod](../classes/OperationBinding.md#attr-operationbindingservermethod) specifies the method that will be called.

For example, the following Datasource DMI declaration would route "fetch" operations for this DataSource to the method "fetch" on an object stored in the servlet session under the name "beanFetcher":

```
 <DataSource>
   <operationBindings>
       <binding operationType="fetch" serverMethod="fetch">
           <serverObject  
                lookupStyle="attribute" 
                attributeScope="session" 
                attributeName="beanFetcher"/>
       </binding>
   </operationBindings>
   ...
 </DataSource>
 
```
Method overloading is not supported - there must be exactly one method on the target class with the name specified in [OperationBinding.serverMethod](../classes/OperationBinding.md#attr-operationbindingservermethod). The method must be public, but can be either an instance or static method. If no operationBinding is specified or the operationBinding does not specify a `serverMethod` then it defaults to the name of the operation (eg "fetch").

By default, the DSResponse data sent back by DataSource DMIs is filtered to just the set of fields specified on the DataSource. This allows you to simply return beans that potentially have getter methods for fields other than are defined in the DataSource without that (potentially private) data being sent to the client. If you want to disable this functionality, you can do so on a per-operation basis by setting [ServerObject.dropExtraFields](../classes/ServerObject.md#attr-serverobjectdropextrafields), on a per-DataSource level by setting [DataSource.dropExtraFields](../classes/DataSource.md#attr-datasourcedropextrafields), or globally by setting the config parameter `DMI.dropExtraFields` to `false` in [\[webroot\]/WEB-INF/classes/server.properties](../reference.md#kb-topic-serverproperties-file). Non-DMI DSResponse data is, by default, not filtered in this manner for backward compatibility reasons. If you want to enable this type of filtering for non-DMI DSResponse data, you can do so by setting the config parameter `DSResponse.dropExtraFields` to `true` in [\[webroot\]/WEB-INF/classes/server.properties](../reference.md#kb-topic-serverproperties-file). `DMI.dropExtraFields` and `DSResponse.dropExtraFields` can be enabled/disabled independently of each other - that is, setting one does not side-effect the other. [server.properties](../reference.md#kb-topic-serverproperties-file) settings can be overridden by an explicit setting in [DataSource.dropExtraFields](../classes/DataSource.md#attr-datasourcedropextrafields) which in turn can be overridden by an explicit setting in [ServerObject.dropExtraFields](../classes/ServerObject.md#attr-serverobjectdropextrafields) (this last one for DMI only since non-DMI operations don't have a serverObject context).

**DataSource DMI and regular RPCManager dispatch**  
It is possible to use DMI to incorporate your own code into what is otherwise the regular process flow of an ordinary, non-DMI DataSource request. This is particularly valuable if you are using the built-in SQL or Hibernate DataSources, because it allows you to inject extra functionality (validations, processing steps, messages to other systems, anything you can code) into a fetch or update request that is otherwise handled for you by the SmartClient Server.

To do this, just configure an operationBinding for DMI, as described above. Then, in your server-side method, invoke `execute()` on the `DSRequest` your method is passed. If you create a DMI method that does nothing **but** invoke `dsRequest.execute()`, then you have a DMI method that behaves exactly like the normal RPCManager dispatch code. Customizing "normal RPCManager dispatch code" is now a simple matter of adding logic to your DMI method. See *this example* of this technique in the Feature Explorer.

**RPC DMI**  
RPC DMI makes a set of methods from a server-side class available as client-side methods for direct invocation (via [DMI.call](../classes/DMI.md#classmethod-dmicall)). This provides a way to perform arbitrary client/server interactions outside of the DataSource subsystem.

RPC DMI is an alternative approach to using the [RPCManager](../classes/RPCManager.md#class-rpcmanager) class directly to send requests to some `actionURL` where your server code would receive a generalized [request object](../reference.md#object-rpcrequest), to be routed to appropriate methods yourself. Which interface (DMI or RPCManager) you choose is largely a matter of preference - they provide equivalent functionality.

RPC DMI also uses a [ServerObject](../reference_2.md#object-serverobject) configuration block to specify the server-side DMI end-point, but in the case of RPCs, the [ServerObject](../reference_2.md#object-serverobject) definition goes into an `rpcBindings` section of an [Application definition](applicationDeclaration.md#kb-topic-application-declaration-files) in a `*.app.xml` file. For an example, see the `example.app.xml` file in the /shared/app directory of the SmartClient SDK. The only difference between the RPC DMI ServerObject definition and the DataSource DMI version is the addition of the [ServerObject.visibleMethods](../classes/ServerObject.md#attr-serverobjectvisiblemethods) block that specifies which methods are callable on this ServerObject. This section is not consulted for DataSource DMIs because the [OperationBinding.serverMethod](../classes/OperationBinding.md#attr-operationbindingservermethod) is used to specify the callable method in that case.

**Method Invocation**  
SmartClient can pass a set of stock context variables to your DMI method and also performs some type adaptation logic to make this interface more flexible. For DataSource DMI, you can declare your method to take any number of the following types of arguments and they will be passed to you:

*   javax.servlet.http.HttpServletRequest
*   javax.servlet.http.HttpServletResponse
*   javax.servlet.ServletContext
*   javax.servlet.http.HttpSession
*   com.isomorphic.rpc.RPCManager
*   com.isomorphic.datasource.DSRequest
*   com.isomorphic.servlet.RequestContext (from com.isomorphic.servlet)
*   com.isomorphic.datasource.DataSource (same as DSRequest.getDataSource())
*   org.springframework.beans.factory.BeanFactory (when applicable)
*   org.springframework.context.ApplicationContext (when applicable)
*   java.util.Map (same as DSRequest.getValues())
*   Arbitrary Java Bean (auto-populated from DSRequest.getValues())

See server-side javadoc for `DataTools.setProperties()` for details how Java Beans are populated including notes on Joda-Time and Java 8 Date/Time API support.

DataSource DMI methods can return any of the following types of values:

*   com.isomorphic.datasource.DSResponse (used as the DSResponse verbatim)
*   java.util.List (valid response to a fetch operation - gets auto-popuplated into a DSResponse for you via setData())
*   java.util.Map or arbitrary Java Bean (valid response to add, update, remove operations - gets auto-populated into a DSResponse for you via setData()).

Note that to take advantage of some SmartClient features like paging and custom validation, you need to return a DSResponse and provide the required metadata (like startRow/endRow/totalRows for paging). You can simply return a `List` instead, but this won't work for large datasets.

So, for example, all of the following DataSource DMI method signatures are valid:

```
 public List myFetch(Map criteria)
 public List myFetch(SupplyItem criteria)
 public DSResponse myAdd(HttpSession session, 
                         DataSource ds, 
                         DSRequest dsRequest)
 
```

See [the supplyItemDMI example](/examples/server_integration/#customDataSourceIntegrationDMI) for an example of DataSource DMI.

RPC DMIs work slightly differently. Unlike DataSource DMIs, RPC DMIs can have an arbitrary number of required arguments, and also some optional context arguments. For example, let's say you call a method from the client like so (note that there's a cleaner way to invoke DMIs if you use the [loadDMIStubsTag](loadDMIStubsTag.md#kb-topic-isomorphicloaddmistubs) JSP tag):  

```
 DMI.call("myApp", "com.sample.MyClass", "doSomething",
          1, "zoo", [1, 2, 3], "clientCallback()");
 
```
The server-side implementation of the method invoked must have a signature that will accept the arguments passed in from the client. In the example above `com.sample.MyClass.doSomething` should accept a Number, String, and a List as arguments. SmartClient will try to adapt arguments where possible - so for example the first argument can be a Long or an Integer, or a native type (`long` or `int`) instead and the invocation will still work. JavaScript objects passed from the client becomes a Map on the server and will be automatically applied to a bean if the method argument takes a Bean in that position. See [RPCRequest.data](../classes/RPCRequest.md#attr-rpcrequestdata) for a table of type conversions.

In addition to the parameters explicitly passed from the client, your method signature can include some additional arguments to pick up information about the request passed in. If your server side method is declared with arguments of the following type they will be passed to your DMI method.

*   javax.servlet.http.HttpServletRequest
*   javax.servlet.http.HttpServletResponse
*   javax.servlet.ServletContext
*   javax.servlet.http.HttpSession
*   com.isomorphic.rpc.RPCManager
*   com.isomorphic.rpc.RPCRequest
*   org.springframework.beans.factory.BeanFactory (when applicable)
*   org.springframework.context.ApplicationContext (when applicable)

Your server side method can return a `RPCResponse` object giving you full control over the response sent to the server. If your method does not return a response, one will be created automatically and the return value from the server method will become the `data` value on the response.  
See [RPCRequest.data](../classes/RPCRequest.md#attr-rpcrequestdata) for an overview of how server side java data types are mapped to client side values.

See [the getTimeStampDMI example](/examples/server_integration/#genericRPCIntegrationDMI) for an example of RPC DMI.

### See Also

- [applicationDeclaration](applicationDeclaration.md#kb-topic-application-declaration-files)
- [loadDMIStubsTag](loadDMIStubsTag.md#kb-topic-isomorphicloaddmistubs)
- [ServerObject](../reference_2.md#object-serverobject)
- [DataSource.serverObject](../classes/DataSource.md#attr-datasourceserverobject)
- [OperationBinding.serverObject](../classes/OperationBinding.md#attr-operationbindingserverobject)
- [clientServerIntegration](clientServerIntegration.md#kb-topic-client-server-integration)

---
