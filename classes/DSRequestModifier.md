# DSRequestModifier Documentation

[← Back to API Index](../reference.md)

---

## Attr: DSRequestModifier.fieldName

### Description
The name of the field to add or replace on the DSRequest - whether this appears in the DSRequest's values or criteria depends on whether this is part of a [OperationBinding.values](OperationBinding.md#attr-operationbindingvalues) or [OperationBinding.criteria](OperationBinding.md#attr-operationbindingcriteria) attribute.

**Flags**: IR

---
## Attr: DSRequestModifier.operator

### Description
The name of the operator to apply when constructing criteria. This property only applies to criteria; it is ignored if specified as part of a [OperationBinding.values](OperationBinding.md#attr-operationbindingvalues) attribute.

**Flags**: IR

---
## Attr: DSRequestModifier.start

### Description
The value to use for the start of a range. This property only applies to criteria, and it only applies to operators of type "rangeCheck" - for example, the "between" operator. It is ignored if specified as part of a [OperationBinding.values](OperationBinding.md#attr-operationbindingvalues) attribute, or for an inapplicable operator type.

The same rules apply to this attribute as apply to [value](#attr-dsrequestmodifiervalue), so you can use Velocity expressions if you have a Power or better license.

### Groups

- transactionChaining

**Flags**: IR

---
## Attr: DSRequestModifier.end

### Description
The value to use for the end of a range. This property only applies to criteria, and it only applies to operators of type "rangeCheck" - for example, the "between" operator. It is ignored if specified as part of a [OperationBinding.values](OperationBinding.md#attr-operationbindingvalues) attribute, or for an inapplicable operator type.

The same rules apply to this attribute as apply to [value](#attr-dsrequestmodifiervalue), so you can use Velocity expressions if you have a Power or better license.

### Groups

- transactionChaining

**Flags**: IR

---
## Attr: DSRequestModifier.value

### Description
The value to assign to the field named by [fieldName](#attr-dsrequestmodifierfieldname). This value can be static, and for Pro licenses that is the only option. With Power and better licenses, this value can be an expression in the Velocity template language. In this latter case, all the standard [Velocity context variables](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables) provided by SmartClient Server are available to you.

Note, `dsRequestModifier` values are evaluated during [DSRequest](../reference_2.md#object-dsrequest) setup, before the request's `execute()` method is called. This means that variables added to the Velocity context by calling `addToTemplateContext()` from a [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) method or [custom DataSource implementation](DataSource.md#attr-datasourceserverconstructor) will not be available. In this case, you can either

*   Apply the variable values directly to the `DSRequest`'s criteria and values from your Java code. See the server-side Javadoc for `DSRequest`
*   Add your template variables to the `DSRequest`'s template context before `dsRequestModifier` evaluation takes place, in a custom override of [the IDACall servlet](../kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration)

#### masterId and responseData
There is also one additional Velocity context variable available in this specific case: **$masterId**. If there is a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) from the DataSource for the current operation to another DataSource for which an add or update operation has taken place earlier in the queue, this is the value of the target field of the foreign key, taken from the response data of that earlier operation (the most recent one, if there are several). This is useful because it will typically yield the (possibly just generated) primary key of the "master" record.

Consider a queued batch of "add" operations for an order header and its details. The detail additions need to know the unique primary key that was assigned to the order, but this will typically be generated at the time of inserting the order row into the database, so it is not known up-front. However, this value will be in the response to the DSRequest that added the order header, so it is accessible via **$responseData**; if there is a declared foreign key relationship from the detail DataSource to the header DataSource, the header's unique key value will also be accesible as **$masterId**. See this example: *queuedAdd example*.

`$responseData` - which is an instance of `com.isomorphic.velocity.ResponseDataHandler` - exposes various overloads of `first()` and `last()` APIs that can be called to obtain the actual record data of prior responses. These methods return an instance of `com.isomorphic.velocity.ResponseDataWrapper`, which allows convenient handling of response data whether it is a single record or a list. Response data can be treated as a single record even if it is a List, so you can access the response data directly, with no need for an index; when you do this, and the data is actually a List or array, you get the first record. If the response data is a list or array, you can also access individual records in that list using Velocity index notation, and you can use the special value "last" to access the last element of a List or array.

Examples of the Velocity syntax needed:

`$responseData.first.myField` is the myField property of the first response in the queue. Note, this works whether that response returned a single record or a list. If it returned a list, this Velocity expression gets the first record in the list. This is a particularly useful shorthand for 'add' and 'update' operations, where the response data is typically a List containing a single record

`$responseData.first('order').myField` is the myField property of the first response to an operation (any operation) on the "order" DataSource

`$responseData.first('order', 'add').myField` is the myField property of the first response to an "add" operation on the "order" DataSource

`$responseData.first('order', 'fetch').last.myField` is the myField property of the last record in the response data of the first fetch in the queue (fetch operations always return a List of records)

`$responseData.first('order', 'fetch')[0].myField` is the myField property of a specific record (in this case, the first) in the response data of the first response in the queue. Note that this is shown for completeness only: there is no need to use index notation to explicitly request the first record, unless you are iterating over the entire list or have some other out-of-the-ordinary use case. The first record is assumed if you omit the index notation, so this example is equivalent to the simpler: `$responseData.first('order', 'fetch')[0].myField`

`$responseData.first('order', 'fetch').allRecords.myField` returns a list containing the myField property of every record in the response data of the first fetch in the queue on the 'order' DataSource. This feature is useful if you want to use the output of one fetch as the input of a later fetch: for example, the automatic [keepParentsOnFilter algorithm](ResultTree.md#attr-resulttreematchingleafjoindepth) makes use of this feature to use the results of one fetch in the criteria of the next fetch in the queue.

All of these syntactic variations are also available on the `$responseData.last` object - "last" here meaning the most recent response matching the DataSource and operation type (if applicable). Note, "last" potentially has three different meanings, depending on context: If your DataSource contains a field that is actually called "last", the following expression would be the correct way to obtain the value of the field called "last", on the last record of the last (most recent) response: `$responseData.last.last.last`

Please see the server-side Javadoc for the `com.isomorphic.velocity.ResponseDataHandler` class.

### Groups

- transactionChaining

### See Also

- [velocitySupport](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables)

**Flags**: IR

---
