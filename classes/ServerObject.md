# ServerObject Documentation

[← Back to API Index](../reference.md)

---

## Attr: ServerObject.bean

### Description
For use when [ServerObject.lookupStyle](#attr-serverobjectlookupstyle) is `"spring"` or `"cdi"`, id (name) of the bean to ask Spring (CDI) to create.

**Flags**: IR

---
## Attr: ServerObject.dropExtraFields

### Description
By default, for DMI DSResponses, DSResponse.data is filtered on the server to just the set of fields defined on the DataSource. This behavior can be overridden in several ways - see the overview in [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) for details. The value of this attribute overrides [DataSource.dropExtraFields](DataSource.md#attr-datasourcedropextrafields).

**Flags**: IR

---
## Attr: ServerObject.methodName

### Description
Specifies the name of the method to call for operations using this ServerObject. This is a DataSource-level default; you can override it for individual operations either by specifying the [OperationBinding.serverMethod](OperationBinding.md#attr-operationbindingservermethod) attribute, or by declaring an operation-level serverObject that specifies a different methodName (if you specify both an operationBinding.serverMethod and an operation-level serverObject.methodName, the latter takes precedence)

**Flags**: IR

---
## Attr: ServerObject.attributeName

### Description
Specifies the name of the attribute by which to look up the DMI instance. This attribute is consulted only when the value of [ServerObject.lookupStyle](#attr-serverobjectlookupstyle) is `"attribute"`.

### See Also

- [ServerObject.attributeScope](#attr-serverobjectattributescope)
- [ServerObject.lookupStyle](#attr-serverobjectlookupstyle)

**Flags**: IR

---
## Attr: ServerObject.className

### Description
Specifies the fully-qualified class name that provides the server-side endpoint of the DMI ([ServerObject.lookupStyle](#attr-serverobjectlookupstyle):"new") or the class name of the factory that produces the DMI instance ([ServerObject.lookupStyle](#attr-serverobjectlookupstyle):"factory").

This is one of the values that you need to pass to [DMI.call](DMI.md#classmethod-dmicall) to invoke the DMI from the client.

The value of this attribute is used for `"new"` and `"factory"` values of [ServerObject.lookupStyle](#attr-serverobjectlookupstyle).

It is also used for `"cdi"` value of [ServerObject.lookupStyle](#attr-serverobjectlookupstyle), to provide class name of the bean to ask CDI to create.

### See Also

- [ServerObject.lookupStyle](#attr-serverobjectlookupstyle)
- [ServerObject.ID](#attr-serverobjectid)
- [DMI.call](DMI.md#classmethod-dmicall)

**Flags**: IR

---
## Attr: ServerObject.lookupStyle

### Description
Specifies the mechanism for locating the class instance on which to invoke the method. Valid values are as follows:

*   "spring": For use with the [Spring framework](https://spring.io/projects/spring-framework). [ServerObject.bean](#attr-serverobjectbean) contains the name of the bean to invoke. Which application context is used can be configured via web.xml (see the example web.xml in the SDK). See also [serverInit](../kb_topics/serverInit.md#kb-topic-server-framework-initialization) for special concerns with framework initialization when using Spring.
*   "cdi": For use with [CDI (Contexts and Dependency Injection)](http://docs.oracle.com/javaee/6/tutorial/doc/giwhb.html). Use [ServerObject.bean](#attr-serverobjectbean) to configure the name of the bean to invoke or, alternatively, [ServerObject.className](#attr-serverobjectclassname) to configure its class name.
*   "new": A new instance of the class specified by [ServerObject.className](#attr-serverobjectclassname) will be created and the DMI method will be invoked on that instance (unless the specified method is static, in which case no instance is created, but the class specified by [ServerObject.className](#attr-serverobjectclassname) is still used).
*   "factory": A custom factory provides the class instance on which the DMI method is to be invoked. In this case, [ServerObject.className](#attr-serverobjectclassname) specifies the className of the factory that will provide the instance on which the DMI method is to be invoked. The class specified by [ServerObject.className](#attr-serverobjectclassname) must provide exactly one method named `create` that must return the class instance on which you wish the DMI method to be invoked. Like the DMI methods, the `create` method can request a standard set of values as arguments. See [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) for a list of available values.
*   "attribute": The instance on which the DMI method is to be invoked is looked up in the scope defined by [ServerObject.attributeScope](#attr-serverobjectattributescope) via the attribute name specified in [ServerObject.attributeName](#attr-serverobjectattributename).

### See Also

- [ServerObject.className](#attr-serverobjectclassname)
- [ServerObject.bean](#attr-serverobjectbean)
- [ServerObject.attributeName](#attr-serverobjectattributename)
- [ServerObject.attributeScope](#attr-serverobjectattributescope)

**Flags**: IR

---
## Attr: ServerObject.visibleMethods

### Description
When the [ServerObject](../reference_2.md#object-serverobject) appears in a .app.xml file (for RPC DMI), this property specifies the list of methods on the ServerObject that are callable from the client. See the builtin.app.xml file in the /shared/app directory of the SDK for an example of a visibleMethods declaration block.

### See Also

- [DMI](DMI.md#class-dmi)

**Flags**: IR

---
## Attr: ServerObject.attributeScope

### Description
Specifies the scope in which the DMI instance is to be looked up. Valid values are: `"request"`, `"session"`, and `"application"`. If `attributeScope` is left out of the `ServerObject` definition, then all scopes are searched in the order in which they are listed above.

This attribute is consulted only when the value of [ServerObject.lookupStyle](#attr-serverobjectlookupstyle) is `"attribute"`.

### See Also

- [ServerObject.attributeName](#attr-serverobjectattributename)
- [ServerObject.lookupStyle](#attr-serverobjectlookupstyle)

**Flags**: IR

---
## Attr: ServerObject.ID

### Description
You can optionally specify an ID on the ServerObject config block - in which case you can use that value as the "className" argument when calling [DMI.call](DMI.md#classmethod-dmicall). This allows you to hide the name of the server-side class used as the factory or implementer of the DMI from the browser as a security precaution.

### See Also

- [ServerObject.className](#attr-serverobjectclassname)
- [DMI.call](DMI.md#classmethod-dmicall)

**Flags**: IR

---
## Attr: ServerObject.targetXPath

### Description
If set, the SmartClient server will use JXPath to call your server code. The `JXPathContext` (start point) will be the object arrived at by applying the [lookupStyle](#attr-serverobjectlookupstyle) and related ServerObject properties. The intention of this property is to allow easier access to your existing Java objects and reduce the need to write SmartClient-specific server code.

**Flags**: IR

---
## Attr: ServerObject.crudOnly

### Description
For a ServerObject defined at the [DataSource level](DataSource.md#attr-datasourceserverobject), by default we only allow it to intercept standard CRUD operations (ie, ordinary fetches, adds, updates and removes). To allow the ServerObject to intercept other types of operation - custom operations, validations, etc - set this property to false. Note that ServerObjects declared at the [OperationBinding level](OperationBinding.md#attr-operationbindingserverobject) always intercept that operation, whatever its type, and this property has no effect.

**NOTE:** If you are intercepting operations on the server because you wish to inspect them before deciding whether to process them with bespoke code or allow them to proceed with normal processing, the way to invoke normal processing without causing any interference is:

```
    return dsRequest.execute();
 
```

**Flags**: IR

---
