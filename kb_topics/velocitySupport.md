# Velocity context variables

[← Back to API Index](../reference.md)

---

## KB Topic: Velocity context variables

### Description
The SmartClient Server provides a number of standard context variables for use in the Velocity templates you write to implement [custom queries](customQuerying.md#kb-topic-custom-querying-overview), [transaction chaining](transactionChaining.md#kb-topic-transaction-chaining), [dynamic security checking](../classes/OperationBinding.md#attr-operationbindingrequires), [templated mail messages](../classes/Mail.md#class-mail), and in other templating contexts. The variables available depend on the exact use case - for example, variables related to a [DSRequest](../reference.md#object-dsrequest) are not available in contexts where there is no `DSRequest`, such as when we are loading a DataSource definition, and variables relating to the servlet environment are not available in a standalone context. The full list of available context variables:

*   **$currentDate**. The current date/time with millisecond precision
*   **$currentDateUTC**. $currentDate in UTC
*   **$transactionDate**. The date/time that this transaction started, with millisecond precision. If you are not using [queuing](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue), this value will be identical to **$currentDate**
*   **$transactionDateUTC**. $transactionDate in UTC
*   **$currentDateTime**. The current date/time with millisecond precision (Joda DateTime object)
*   **$currentDateTimeUTC**. $currentDateTime in UTC
*   **$transactionDateTime**. The date/time that this transaction started, with millisecond precision. If you are not using [queuing](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue), this value will be identical to **$currentDateTime**
*   **$transactionDateTimeUTC**. $transactionDateTime in UTC
*   **$userId**. The currently-authenticated user. This is a shortcut for "$rpc.getUserId()"
*   **$config**. The global `Config` object (though of course this is a server-side object, so please see the server-side Javadocs)
*   **$servletRequest**. The associated `HttpServletRequest`
*   **$dsRequest**. The associated [DSRequest](../reference.md#object-dsrequest) (though of course this is a server-side `DSRequest` object, so please also see the server-side Javadocs)
*   **$primaryDSRequest**. Only present on cache-sync operations, this is the original update `DSRequest` that caused the cache-sync request to be created
*   **$session**. The associated `HttpSession`
*   **$httpParameters**. This variable gives you access to the parameters Map of the associated `HttpServletRequest`; it is an alternate form of `$servletRequest.getParameter`
*   **$requestAttributes**. This variable gives you access to the attributes Map of the associated `HttpServletRequest`; it is an alternate form of `$servletRequest.getAttribute`
*   **$sessionAttributes**. This variable gives you access to the attributes Map of the associated `HttpSession`; it is an alternate form of `$session.getAttribute`
*   **$dataSources**. This variable gives you access to SmartClient [DataSource](../classes/DataSource.md#class-datasource)s. You access a dataSource by suffixing its name to the `$dataSources` designation. For example, `$dataSources.supplyItem` refers to the DataSource object called "supplyItem". You can use this approach to execute any valid DataSource method. One especially useful method in this context is `hasRecord(fieldName, value)` - see the server-side Javadocs for more details.
*   **$util** - A `DataTools` object, giving you access to all of that class's useful helper functions
*   **$log** - A `Logger` instance in category "velocityTemplate"
*   **$rpc** - the current `RPCManager`
*   **$rpcManager** - the current `RPCManager` (synonym to $rpc)
*   **$storedRecord** - (_available in validators only_) The record as it currently exists in storage. Fetched only if accessed. Fetched only once per validation run. If record does not exist in storage (add operation) velocity engine will complain about missing properties. To avoid it - use special property **recordExists** to test if specified record is found in storage. For example (new value can only be greater then existing):
    ```
             #if ($storedRecord.recordExists())
                 $value > $storedRecord.valInt
             #else
                 true
             #end
    ```
    
*   **$editedRecord** - (_available in validators only_) The stored record with submitted record overlaid as changes. If record does not exists $editedRecord will contain only properties submitted in request. This variable is recalculated for every validator, picking up any changes caused by setting Validator.resultingValue. Validation occurs in the same order that fields are defined in the DataSource. Using $editedRecord, it is invalid to assume that validation for other fields has completed therefore it is not guaranteed that properties will contain correct (validated) values. It can be wrong type (String instead of Integer) as well.
*   **$responseData**. The data member of a DSResponse object associated with an earlier DSRequest in the same queue, as an instance of `com.isomorphic.velocity.ResponseDataWrapper`; see the server-side Javadoc for details of that class. This context variable is particularly useful in a [transactionChaining](transactionChaining.md#kb-topic-transaction-chaining) context, as you can optionally refer to the first or last DSResponse for a given DataSource or DataSource/operation type combination. This support is implemented by `com.isomorphic.velocity.ResponseDataHandler`; see its server-side Javadoc for details. Note, this variable is only present if you have Power Edition or better
*   **$responses**. The actual DSResponse object associated with an earlier DSRequest in the same queue. As with `$responseData`, you can optionally refer to the first or last response for a given DataSource or DataSource/operation type combination. See the server-side Javadoc for `com.isomorphic.velocity.ResponsesHandler` for details. Note, this variable is only present if you have Power Edition or better
*   **$sql**. Provides _partialWhere(fieldNames)_, _whereWithout(fieldNames)_, _partialHaving(fieldNames)_ and _havingWithout(fieldNames)_ utilities providing access to corresponding `com.isomorphic.sql.SQLDataSource` APIs `getPartialWhere(DSRequest, fieldNames)`, `getWhereWithout(DSRequest, fieldNames)` etc. These utilities allow to get SQL for partial criteria. Please see the server-side javadoc for the corresponding methods for more details on the behavior. _Note_ that $sql variable methods omit `DSRequest` parameter, it is provided internally and is the same DSRequest as referred by _$dsRequest_ variable. Example usage:
    ```
         <whereClause>$sql.partialWhere("fieldName1", "fieldName2" ...)</whereClause>
         
    ```
    

All of these variables (other than the two dates and the userId) represent objects that can contain other objects (attributes or parameters or object properties). The variables based on the Servlet API (session, sessionAttributes, httpParameters, servletRequest and requestAttributes) all implement the `Map` interface, so you can use the Velocity "property" shorthand notation to access them. The following usage examples show five equivalent ways to return the value of the session attribute named "foo":
```
    $session.foo
    $session.get("foo")
    $session.getAttribute("foo")
    $sessionAttributes.foo
    $sessionAttributes.get("foo")
 
```
In the case of `$servletRequest`, the shorthand approach accesses the attributes - you need to use either `$httpParameters` or `$servletRequest.getParameter` to access parameters. These examples all return the value of the HTTP parameter named "bar":
```
    $httpParameters.bar
    $httpParameters.get("bar")
    $servletRequest.getParameter("bar")
 
```
When you use these Velocity variables in a [customSQL](../classes/OperationBinding.md#attr-operationbindingcustomsql) clause or SQL snippet such as a [whereClause](../classes/OperationBinding.md#attr-operationbindingwhereclause), all of these template variables return values that have been correctly quoted and escaped according to the syntax of the underlying database. We do this because "raw" values are vulnerable to [SQL injection attacks](http://en.wikipedia.org/wiki/SQL_injection). If you need access to the raw value of a variable in a SQL template, you can use the **$rawValue** qualifier in front of any of the template variables, like this:  
  
  `$rawValue.session.foo`

This also works for the **$criteria** and **$values** context variables (see [customQuerying](customQuerying.md#kb-topic-custom-querying-overview) for details of these variables). So:  
  
  `$rawValue.criteria.customerName`

Note that `$rawValue` is only available in SQL templates. It is not needed in other contexts, such as [Transaction Chaining](transactionChaining.md#kb-topic-transaction-chaining), because the value is not escaped and quoted in these contexts.

**Warning**: Whenever you access a template variable for use in a SQL statement, bear in mind that it is **dangerous** to use `$rawValue`. There are some cases where using the raw value is necessary, but even so, all such cases are likely to be vulnerable to injection attacks. Generally, the presence of `$rawValue` in a SQL template should be viewed as a red flag.

Finally, some example usages of these values. These [values](../classes/OperationBinding.md#attr-operationbindingvalues) clauses set "price" to a value extracted from the session, and "lastUpdated" to the date/time that this transaction started:  
  
  ``<values fieldName="price" value="$session.somePrice" />`     `<values fieldName="lastUpdated" value="$transactionDate" />``

This whereClause selects some users based on various values passed in the criteria and as HTTP parameters:  
  
  ``<whereClause>`department = $httpParameters.userDept AND dob >= $criteria.dateOfBirth`</whereClause>``

This whereClause selects some users based on various values obtained from the servletRequest's attributes, using a number of equivalent techniques for accessing the attributes:

```
   <whereClause>
         department = $servletRequest.dept 
     AND startDate >= $requestAttributes.dateOfBirth 
     AND salary < $servletRequest.getAttribute("userSalary")
   </whereClause>
 
```

If you are using the Java server and would like to add your own Java objects to the server-side Velocity context, you can do so on a per-request basis via `DSRequest.addToTemplateContext()` or globally by using Velocity Tools. The Velocity Tools mechanism is described here: [http://velocity.apache.org/tools/releases/2.0/index.html](http://velocity.apache.org/tools/releases/2.0/index.html). Just add the velocity tools jars to your deployment and place your tools.xml configuration file in the CLASSPATH (typically WEB-INF/classes).

Additionally, if you would like to modify the Velocity Engine defaults, you can provide your own `velocity.properties` at the top level of the CLASSPATH (again, typically in WEB-INF/classes). These settings will overlay and override the defaults provided the velocity.properties file that ships inside the Velocity jar.

### Related

- [VelocityExpression](../reference_2.md#type-velocityexpression)

---
