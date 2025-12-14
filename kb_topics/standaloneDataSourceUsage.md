# Standalone DataSource Usage

[← Back to API Index](../reference.md)

---

## KB Topic: Standalone DataSource Usage

### Description
The DataSource layer can be used in a standalone application separate from a servlet engine, for use cases like offline batch data processing, sending emails based on database state, or integration of SmartClient Server logic into a standalone Java Swing application.

In addition, the section below on "Transactions in standalone applications" also applies to any transaction that is initiated separately from an RPCManager and/or the HttpServletRequest lifecycle. This includes use cases like non-servlet web apps (using NIO servers like Grizzly), web apps that set timers to perform delayed actions (using frameworks such as Quartz), as well JMS or other Java frameworks that may introduce non-HttpServletRequest threads within a servlet container.

Note that we do still require `servlet-api.jar` to be on the classpath of standalone applications. This is only to satisfy class-loading requirements; there are cases where running inside a servlet engine allows us to provide extra functionality, such as declarative authentication and authorization features, so some classes do have member variables or method parameters of types in the Servlet API. They all operate correctly when these variables or parameters are null, but the JVM will still try to load the classes and will crash if they are missing.

Using the DataSource layer to run DataSource operations in your standalone applications is extremely straightforward. This example fetches and prints every record from the "customers" DataSource:

```
   public static void main(String[] args) {
     DataSource ds = DataSourceManager.get("customers");
     List records = ds.fetch();
     for (Iterator i = records.iterator; i.hasNext(); ) {
       System.out.println(i.next());
     }
   }
 
```
To make this example fetch just customers in the United States:
```
     Map criteria = new HashMap();
     criteria.put("countryCode", "US");
     List records = ds.fetch(criteria);
 
```
This example shows how to run a specific fetch operation, specifying both selection criteria and a sort order, using a `DSRequest` rather than a `DataSource` convenience method:
```
   public static void main(String[] args) {
     DSRequest dsReq = new DSRequest("customers", "fetch");
     dsReq.setOperationId("specialFetch");
     Map criteria = new HashMap();
     criteria.put("countryCode", "US");
     criteria.put("region", "CA");
     dsReq.setCriteria(criteria);
     dsReq.setSortBy("customerName");
     List records = dsReq.execute().getDataList();
   }
 
```
This example shows how to do a simple update:
```
   public static void main(String[] args) {
     DataSource ds = DataSourceManager.get("customers");
     Map criteria = new HashMap();
     criteria.put("customerNo", 12345);
     Map values = new HashMap();
     values.put("creditLimit", 10000);
     values.put("currencyCode", "USD");
     ds.update(criteria, values);
   }
 
```
Finally, this example shows how to perform a specific update operation via a `DSRequest`:
```
   public static void main(String[] args) {
     DSRequest dsReq = new DSRequest("customers", "update");
     dsReq.setOperationId("specialUpdate");
     Map criteria = new HashMap();
     criteria.put("customerNo", 12345);
     Map values = new HashMap();
     values.put("creditLimit", 10000);
     values.put("currencyCode", "USD");
     dsReq.setCriteria(criteria);
     dsReq.setValues(values);
     dsReq.execute();
   }
 
```
**NOTES**

Because we are not running inside a servlet container, SmartClient's built-in logic to work out where its application root is does not work. Therefore, you need to manually set a "webRoot" in your [server.properties](server_properties.md#kb-topic-serverproperties-file) file. The webRoot should point to the root folder of your application (note for SmartGWT applications, this is typically the "war" subfolder of your project). Example entries:

`webRoot: /home/testUser/myProject`

or:

`webRoot: C:\Projects\MyProject\war`

Again in [server.properties](server_properties.md#kb-topic-serverproperties-file), you may need to set `isomorphicPathRootRelative` to match the standalone project's layout if you make the standalone mode separate:

`isomorphicPathRootRelative: myProject/sc`

You should place the [server.properties](server_properties.md#kb-topic-serverproperties-file) file somewhere on your classpath. Typically, the root of your `bin` or `classes` folder structure is the most suitable place for it.

Both the built-in DataSources and custom DataSources can be used in standalone applications, **but only if you do not introduce dependencies on the servlet container in your DataSource code**. For example, if you have a security check in a DMI or custom DataSource that depends on checking the current logged-in user, code in a means of bypassing this, or create a parallel operationBinding that is accessible only to the superuser.  

#### Declarative Security

When you use the DataSource layer in a standalone application, [Declarative Security](../classes/DataSource.md#attr-datasourcerequiresauthentication) has to be explicitly controlled.

To enable a request for security checks you simply need to call `dsRequest.setUserId()` or `dsRequest.setUserRoles()`. If the request is apart of a transaction then security can also be defaulted using `dsTransaction.setClientRequest(true/false)`, however any value set on an individual request will still take priority. For instance if you call `dsTransaction.setClientRequest(false)` but then also call `dsRequest.setUserId(id)`, then security checks will still take place for that request as it has had security enabled which takes priority over the value on `DSTransaction`.

Note: If you have Declarative Security checks in your DataSources and/or enabled via your Java code, and you want to completely disable such checks system-wide, you can set `security.disabled: true` in [server_properties](server_properties.md#kb-topic-serverproperties-file). This causes API calls like `dsRequest.setClientRequest()` to be completely ignored.

#### Transactions

In standalone mode, transactions cannot be automatically initiated with the HTTP request lifecyle, however you can still manually initiate and commit transactions (note, only available with a Power or better license). To do so, create a `DSTransaction` object and associated each `DSRequest` with it via `dsRequest.setDSTransaction()`. At the end of processing, call `DSTransaction.complete()` to ensure commits and rollbacks are executed and that resources are freed up.

Usage Example:

```
     DSTransaction dst = new DSTransaction();
     DSRequest req1 = new DSRequest("myDataSource", "update");
     req1.setDsTransaction(dst);

     DSRequest req2 = new DSRequest("myDataSource", "add");
     req2.setDsTransaction(dst);

     DSRequest req3 = new DSRequest("myDataSource", "update");
     req3.setDsTransaction(dst);

     try {
         // This will process the queue of requests which have been registered with the transaction.
         dst.processQueue();
     } finally {
         // We put this in a "finally" block to ensure it always runs even on exceptions.
         dst.complete();
     }
 
```

You can also handle the requests manually instead of using `dsTransaction.processQueue()`. This can be handy if you wish to perform another operation in between each request or if one request depends on data from the other. At the end of processing, call `DSTransaction.complete()` to ensure commits and rollbacks are executed and that resources are freed up.

Usage Example:

```
     DSTransaction dst = new DSTransaction();

     try {
         DSRequest req1 = new DSRequest("myDataSource", "fetch");
         req1.setDsTransaction(dst);

         DSRequest req2 = new DSRequest("myDataSource", "update");
         req2.setDsTransaction(dst);

         req1.execute();
         // Use the response from req1 to modify req2 here
         req2.execute();
     } catch (Exception e) {
         throw new RuntimeException(e);
     } finally {
         // We put this in a "finally" block to ensure it always runs even on exceptions.
         dst.complete();
     }
 
```

Please note that [Transaction chaining](transactionChaining.md#kb-topic-transaction-chaining) is supported while using transactions in a standalone use case - expressions such as `$responseData` will refer to results from previous `DSRequests` that are part of the same `DSTransaction`.

**Note the following about standalone transactions:**

*   DSRequests that have not had `setDSTransaction()` called will be outside of any transactional processing - they will be auto-committed at the end of request processing.
*   You may partition your updates into multiple transactions, simply by creating multiple `DSTransaction` objects and assigning them to DSRequests as required. Note, this will tie up a database connection per `DSTransaction` until the transactions are committed or rolled back.
*   When using the DSTransaction's built in `processQueue()` method, error handling will be taken care of automatically for each `DSRequest.execute()` call and a proper `DSResponse` will always be returned.
*   Your code is responsible for calling the `complete()` method, which will commit the transaction if every DSRequest was successful, or roll it back if there were any failures, and then release the database connection. If you do not call `complete()`, you will leak database connections, so consider placing the call inside a `finally` block
*   If you do not want SmartClient Server's default behavior of automatically rolling back if any DSRequest failed, you can manually take over the transaction management by calling `commit()` or `rollback()` instead of `complete()`. Note, if you do this you also take on responsibility for releasing the database connection by calling `freeQueueResources()` or `freeAllResources()`. If you fail to do this, you will leak database connections
*   A DSTransaction object can be re-used after `complete()` has been called. When you do this, a new database connection is borrowed or established, and a new transaction is started

#### Spring Framework

In a typical web application, Spring configuration is picked up from an "applicationContext" file by a servlet or listener, and then made available to the rest of the app via the servletContext. When running standalone, this is not possible, so instead we read the applicationContext file manually when we need to, eg, create a DataSource object that is configured as a Spring bean.

By default, the framework will look in the "normal" place for for this configuration: `WEB-INF/applicationContext.xml`. If you have changed the location or name of this file, and you want to run the application outside of a servlet engine, you can tell the framework where to find the configuration file by specifying property `standalone.spring.applicationContext` in your [server.properties](server_properties.md#kb-topic-serverproperties-file). The default setting for this property looks like this:

```
    standalone.spring.applicationContext: $webRoot/WEB-INF/applicationContext.xml
 
```

### See Also

- [transactionChaining](transactionChaining.md#kb-topic-transaction-chaining)

---
