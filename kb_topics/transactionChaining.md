# Transaction Chaining

[← Back to API Index](../reference.md)

---

## KB Topic: Transaction Chaining

### Description
_Transaction Chaining_ allows [queues](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue) of [DSRequest](../reference_2.md#object-dsrequest)s to be "chained" together, such that later `DSRequests` in the queue can use the results of previous requests in the queue. This allows you to declaratively handle various situations where information only becomes available during the processing of a queue.

To see an example of server-driven transaction chaining used to commit a mixed transaction of an `Order` and related `OrderItem`s, see the [Master/Detail Add](https://www.smartclient.com/smartclient-latest/showcase/?id=queuedAdd) sample.

Transaction Chaining is only available with Power Edition licenses or better. See the [Editions & Pricing page](http://smartclient.com/product/) for details.

As an example of Transaction Chaining, consider an application that needs to do a master-detail add, which involves saving a new Record representing a sales order to an `order` DataSource, and also saving several related Records representing individual items in the order to an `orderItem` DataSource. The Records for the individual `orderItem`s need to set up foreign keys referencing the primary key assigned to the Record for the `order`, but the primary key of the `order` record is assigned only when the Record is inserted into the database; it cannot be known up-front.

You could resolve this programmatically - for example, you could use DMIs to store and retrieve the PK value using `servletRequest` attributes - but Transaction Chaining gives you an elegant, declarative, code-free alternative, giving you a way to declare that the foreignKey value for the `orderItem` records should use the primary key value resulting from the creation of the `order` record earlier in the same queue.

As another example, consider an application that allows a user to submit a free-form question which must be persisted to the database like a normal update, but which should initially show the user a list of previously-provided answers that appear to be relevant. The operation that handles the add of the question categorizes it by analyzing the text, and the category is added to the record inserted into the database, and thus to the record returned in the response. Now, via transaction chaining, a "fetch" operation later in the queue can pick up the newly assigned category and use it in criteria to fetch the list of related answers.

Transaction Chaining is implemented by specifying [DSRequestModifier](../reference_2.md#object-dsrequestmodifier)s in [OperationBinding.values](../classes/OperationBinding.md#attr-operationbindingvalues) and [OperationBinding.criteria](../classes/OperationBinding.md#attr-operationbindingcriteria). These two properties provide a general means of declaratively modifying DSRequests server-side, and transaction chaining is only one of their uses. They can also be used, for example, to implement security rules, by adding the currently-authorized user to the criteria of all fetch requests.

Specifically for transaction chaining, you specify `criteria` and/or `values` entries on the `operationBinding` where the [value](../classes/DSRequestModifier.md#attr-dsrequestmodifiervalue) property references the **$responseData** Velocity context variable - see the "value" link for more details. Alternatively, you can use the `RPCManager` APIs `getFirstResponse()` and `getLastResponse()` to get access to the same information, either programmatically from DMI or custom DataSource Java code, or in [JSR 223 scripts](serverScript.md#kb-topic-server-scripting), or in Velocity expressions via the **$rpc** context variable.

#### Client-driven Transaction Chaining
A limited form of transaction chaining (limited for security reasons) is possible without server-side operationBinding configuration, using [fieldValueExpressions](../classes/DSRequest.md#attr-dsrequestfieldvalueexpressions). The primary intended use case is a master-detail add, where the detail records require the master's primary key for use as foreign keys, but that value is not known until the master record has been inserted. In such a case, you create a [queue](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue) of requests, with the add of the master record first, followed by the detail records, each of which has `fieldValueExpressions` set up to use `$masterId` like so:
```
     myDataSource.addData(record, callback, 
         {fieldValueExpressions: { fkField: "$masterId"}});
 
```
It is also possible to achieve the same thing in a less compact but more flexible way by using the `$responseData` context variable (note that client-driven usages of `$responseData` are limited for security reasons - see [fieldValueExpressions](../classes/DSRequest.md#attr-dsrequestfieldvalueexpressions) for details). This approach allows you to reference values where there is no declared foreignKey relationship, and it allows you to reference responses other than the most recent one. For example:
```
     myDataSource.addData(record, callback, 
         {fieldValueExpressions: { anyField: "$responseData.first.anyOtherField"}});
 
```
To see an example of client-driven transaction chaining used to commit a mixed transaction of an `Order` and related `OrderItem`s, see the [Master/Detail Add](https://www.smartclient.com/smartclient-latest/showcase/?id=queuedAdd) sample.

As with Server-Side Transaction Chaining, `fieldValueExpressions` can be used to affect `dsRequest.criteria` as well. For example, perhaps you are fetching the most recent Order and its related OrderItems, by sorting the returned Orders by `orderDate` and asking for only one record. Since you are fetching the most recent Order, you don't have the Order.orderId value available to fetch related OrderItems by passing the `Order.orderId` value as criteria for `OrderItem.orderId`. You need the `primaryKey` of whichever Order turns out to be most recent. Use `fieldValueExpressions` like so to solve this case:

```
      isc.RPCManager.startQueue();
      isc.DS.get("Order").fetchData({}, null, 
          { operationType: "fetch", startRow: 0, endRow: 1, sortBy: [{ property: "orderDate", direction: "descending" }] }
      );
      isc.DS.get("OrderItem").fetchData({}, null, {fieldValueExpressions: { orderId: "$responseData.first.orderId"}});
      isc.RPCManager.sendQueue();
 
```

#### Stand-alone Application Transaction Chaining
Transaction chaining is supported when using transactions standalone. Every request within the same transaction will be eligible during the chaining. It works in the same way as it would if your application was a full blown SmartClient application. See [Standalone DataSource Usage](standaloneDataSourceUsage.md#kb-topic-standalone-datasource-usage) for examples on how to do this.

### Related

- [DSRequestModifier](../reference_2.md#object-dsrequestmodifier)
- [DSRequest.fieldValueExpressions](../classes/DSRequest.md#attr-dsrequestfieldvalueexpressions)
- [DSRequestModifier.value](../classes/DSRequestModifier.md#attr-dsrequestmodifiervalue)
- [DSRequestModifier.start](../classes/DSRequestModifier.md#attr-dsrequestmodifierstart)
- [DSRequestModifier.end](../classes/DSRequestModifier.md#attr-dsrequestmodifierend)
- [OperationBinding.criteria](../classes/OperationBinding.md#attr-operationbindingcriteria)
- [OperationBinding.values](../classes/OperationBinding.md#attr-operationbindingvalues)

---
