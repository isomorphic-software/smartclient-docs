# Declarative Security

[← Back to API Index](../reference.md)

---

## KB Topic: Declarative Security

### Description
The Declarative Security system allows you to attach role based access control to DataSource operations and DataSource fields, as well as create a mix of authenticated and non authenticated operations for applications that support limited publicly accessible functionality.

See the [QuickStart Guide](/smartclient-release/docs/SmartClient_Quick_Start_Guide.pdf) for more in depth documentation on how declarative security works and how to use it in your application.

See [Standalone DataSource Usage](standaloneDataSourceUsage.md#kb-topic-standalone-datasource-usage) for information on how to use declarative security in a standalone application.

**NOTE:** Declarative security only works for DataSource operations (including DataSource DMI operations). If you want to limit access to an ordinary RPC-DMI method - so it can only be called by authenticated users, only users with a certain role, etc - you have two choices:

*   Have your DMI method accept a parameter of type `HttpServletRequest`; that will cause SmartClient to pass the current servlet request into your method, and you can directly call the `getRemoteUser()` and `isUserInRole()` methods to implement your own security
*   Migrate your RPC-DMIs to DataSource DMI operations and get full declarative security support that way. Note that **any** plain RPC-DMI function can be reworked as a DataSource DMI operation; even if your RPC-DMI manifestly is not fetching a dataset or updating a record, you can use a [custom operation](../classes/DataSource.md#method-datasourceperformcustomoperation)

Requests that fail to pass Declarative Security checks will return a response with status of [STATUS\_AUTHORIZATION\_FAILURE](../classes/RPCResponse.md#classattr-rpcresponsestatus_authorization_failure).

#### Client-side declarative security
Client-only dataSources automatically _**simulate**_ the server-side Declarative Security system. Although this is obviously not useful in a production setting, the simulator is extremely valuable because it allows you to implement and test the effect of roles on the UI, and then switch over to the real authentication system without changing any of the UI code. This is in keeping with the SmartClient philosophy on dataSources, which is that you should be able to test with a local, client-only dataSource and local test data, and then switch to a real server-side dataSource with confidence that no client code will be affected.

To use client-side declarative security simulation, just create a [clientOnly dataSource](../classes/DataSource.md#attr-datasourceclientonly) that specifies some of the declarative security rules linked to below. All of these rules, at a minimum, require authentication, so you will also have to provide a dummy authenticated user to the simulator by use of the [client side Authentication class](../classes/Authentication.md#class-authentication)

```
    isc.Authentication.setCurrentUser({userId: "john_doe"});
 
```
Many declarative security rules also require a role, such as "payroll" or "manager", so you may also need to provide roles to the client-side simulator
```
    isc.Authentication.setRoles(["order_handling","supervisor"]);
 
```
The example linked below shows how to use the client-side declarative security simulator to implement and test role-based security rules on both operations and individual fields.

### Related

- [DataSource.requiresAuthentication](../classes/DataSource.md#attr-datasourcerequiresauthentication)
- [DataSource.requiresRole](../classes/DataSource.md#attr-datasourcerequiresrole)
- [DataSource.requires](../classes/DataSource.md#attr-datasourcerequires)
- [DataSource.creatorOverrides](../classes/DataSource.md#attr-datasourcecreatoroverrides)
- [DataSourceField.viewRequiresAuthentication](../classes/DataSourceField.md#attr-datasourcefieldviewrequiresauthentication)
- [DataSourceField.editRequiresAuthentication](../classes/DataSourceField.md#attr-datasourcefieldeditrequiresauthentication)
- [DataSourceField.initRequiresAuthentication](../classes/DataSourceField.md#attr-datasourcefieldinitrequiresauthentication)
- [DataSourceField.updateRequiresAuthentication](../classes/DataSourceField.md#attr-datasourcefieldupdaterequiresauthentication)
- [DataSourceField.viewRequiresRole](../classes/DataSourceField.md#attr-datasourcefieldviewrequiresrole)
- [DataSourceField.editRequiresRole](../classes/DataSourceField.md#attr-datasourcefieldeditrequiresrole)
- [DataSourceField.initRequiresRole](../classes/DataSourceField.md#attr-datasourcefieldinitrequiresrole)
- [DataSourceField.updateRequiresRole](../classes/DataSourceField.md#attr-datasourcefieldupdaterequiresrole)
- [DataSourceField.viewRequires](../classes/DataSourceField.md#attr-datasourcefieldviewrequires)
- [DataSourceField.editRequires](../classes/DataSourceField.md#attr-datasourcefieldeditrequires)
- [DataSourceField.initRequires](../classes/DataSourceField.md#attr-datasourcefieldinitrequires)
- [DataSourceField.updateRequires](../classes/DataSourceField.md#attr-datasourcefieldupdaterequires)
- [DataSourceField.creatorOverrides](../classes/DataSourceField.md#attr-datasourcefieldcreatoroverrides)
- [OperationBinding.requiresAuthentication](../classes/OperationBinding.md#attr-operationbindingrequiresauthentication)
- [OperationBinding.requiresRole](../classes/OperationBinding.md#attr-operationbindingrequiresrole)
- [OperationBinding.requires](../classes/OperationBinding.md#attr-operationbindingrequires)
- [OperationBinding.creatorOverrides](../classes/OperationBinding.md#attr-operationbindingcreatoroverrides)
- [DataSource.enforceSecurityOnClient](../classes/DataSource.md#attr-datasourceenforcesecurityonclient)

### See Also

- [standaloneDataSourceUsage](standaloneDataSourceUsage.md#kb-topic-standalone-datasource-usage)

---
