# Authentication Documentation

[← Back to API Index](../reference.md)

---

## Class: Authentication

### Description
The Authentication or [Auth](../reference.md#class-auth) class represents a convenient, standard place to keep information about the currently logged in user and their assigned user roles.

The intended usage is that a server authentication system would require the user to log in, then provide data about the currently logged in user via [Authentication.setCurrentUser](#classmethod-authenticationsetcurrentuser) and [Authentication.setRoles](#classmethod-authenticationsetroles). This data is then available in the [Rule Scope](Canvas.md#attr-canvasrulescope) so that components can use it to enable or disable or hide themselves, via properties such as [FormItem.readOnlyWhen](FormItem.md#attr-formitemreadonlywhen).

The format for user records is not explicitly defined or restricted by the Authentication subsystem but we recommend using the format described by [Authentication.getUserSchema](#classmethod-authenticationgetuserschema).  
Having a standardized user record allows application designers to rely on a well-known set of field names at design time, and then at deployment time when a particular authentication system is chosen, the deployer can simply fill in the standardized user record from the data that the chosen authentication system returns. This also allows authentication systems to be swapped out in the future without the need to change application code.

The DataSource returned by [Authentication.getUserSchema](#classmethod-authenticationgetuserschema) is used solely for visual tools to help with application authoring.  
It is not intended to be used directly to store and retrieve user data, and while we recommend this format it is not a requirement that user records conform to it.

There are no security implications to calling `setRoles()` or other APIs on the `Authentication` class. The provided data affects only client-side components. All actual security enforcement must be done server-side - see the QuickStart Guide, especially the sections on Declarative Security, to understand how role-based authorization can be used on the server.

**Rule Context**

The default ruleContext obtained from [Canvas.getRuleContext](Canvas.md#method-canvasgetrulecontext) includes a property for the current authentication information (based on [Authentication.getUserSchema](#classmethod-authenticationgetuserschema)):

*   auth

*   currentUser

*   firstName
*   lastName
*   ... other fields in schema

*   roles
*   isSuperUser

The default rule context would therefore include something like the following, expressed in JSON:
```
 {
  auth : {
     currentUser : {
        userId: "lisa",
        firstName: "Lisa",
        lastName: "Admin",
        roles: "admin",
        ..other properties..
     },
     roles : ['admin'],
     isSuperUser : false
  },
  ..other properties..
 }
 
```
Since the `currentUser` information is based on `getUserSchema()` any changes to the schema implemented as an override will be reflected in the rule context.

---
## ClassAttr: Authentication.logOutURL

### Description
URL to open for logging the current user out.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

The dynamic variables available are the fields in the [Authentication.getCurrentUser](#classmethod-authenticationgetcurrentuser) record.

**Flags**: IR

---
## ClassAttr: Authentication.resetPasswordURL

### Description
URL to open for reseting the current user's password.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

The dynamic variables available are the fields in the [Authentication.getCurrentUser](#classmethod-authenticationgetcurrentuser) record.

**Flags**: IR

---
## ClassMethod: Authentication.setAvailableRoles

### Description
Specify the full set of available user roles.

Note that if the current user has been marked as a [superUser](#classmethod-authenticationissuperuser), [Authentication.getRoles](#classmethod-authenticationgetroles) will return the full set of available roles.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| roles | [Array of String](#type-array-of-string) | false | — | full set of possible user roles. |

---
## ClassMethod: Authentication.setCurrentUser

### Description
Set up the current user. This method makes the user record available in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope) as "auth.currentUser".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| user | [Record](#type-record) | false | — | Record with attributes detailing the current user |

---
## ClassMethod: Authentication.getCurrentUserId

### Description
Convenience method to return the `"userId"` attribute of the [current user](#classmethod-authenticationgetcurrentuser) if there is one.

### Returns

`[String](#type-string)` — userId attribute of the [current user record](#classmethod-authenticationgetcurrentuser) if there is one.

---
## ClassMethod: Authentication.setSuperUser

### Description
Mark the current user as a super-user. This causes [Authentication.getRoles](#classmethod-authenticationgetroles) to return the full set of [available roles](#classmethod-authenticationgetavailableroles) if specified

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isSuperUser | [Boolean](#type-boolean) | false | — | New super user status |

---
## ClassMethod: Authentication.getAvailableRoles

### Description
Returns the full set of available user roles specified by [Authentication.setAvailableRoles](#classmethod-authenticationsetavailableroles).

### Returns

`[Array of String](#type-array-of-string)` — full set of possible user roles.

---
## ClassMethod: Authentication.getUserSchema

### Description
Returns a DataSource describing the standard schema for user data.

The schema contains the following fields:

| Field Name | Type |
|---|---|
| "userId" | "text" |
| "email" | "text" |
| "firstName" | "text" |
| "lastName" | "text" |
| "title" | "text" |
| "phone" | "phoneNumber" |
| "superUser" | "boolean" |

### Returns

`[DataSource](#type-datasource)` — user schema dataSource

---
## ClassMethod: Authentication.getRoles

### Description
Returns the current set of user roles. For [super users](#classmethod-authenticationsetsuperuser) this will be the intersection of any roles specified by [Authentication.setRoles](#classmethod-authenticationsetroles) and the full set of [available roles](#classmethod-authenticationsetavailableroles) - otherwise it will be the set of roles specified by [Authentication.setRoles](#classmethod-authenticationsetroles).

Current set of user roles are available in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope) as a top-level property "userRoles", so that it can be used in criteria such as [Canvas.visibleWhen](Canvas.md#attr-canvasvisiblewhen) or [FormItem.readOnlyWhen](FormItem.md#attr-formitemreadonlywhen).

### Returns

`[Array of String](#type-array-of-string)` — set of roles which apply to the current user

---
## ClassMethod: Authentication.getCurrentUser

### Description
Returns the current user specified by [Authentication.setCurrentUser](#classmethod-authenticationsetcurrentuser).

This method returns the user record currently available in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope) as "auth.currentUser".

### Returns

`[Record](#type-record)` — Record with attributes detailing the current user

---
## ClassMethod: Authentication.hasRole

### Description
Is the current user assigned to the specified role?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| role | [String](#type-string) | false | — | role to check in current roles |

### Returns

`[Boolean](#type-boolean)` — true if the user has the role in its [Authentication.getRoles](#classmethod-authenticationgetroles) list; false otherwise

### See Also

- [Authentication.getRoles](#classmethod-authenticationgetroles)

---
## ClassMethod: Authentication.setRoles

### Description
Set the user roles for the current user. Roles may be retrieved via [Authentication.getRoles](#classmethod-authenticationgetroles).

Calling setRoles() makes the specified set of user roles available in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope) as a top-level property "userRoles", so that it can be used in criteria such as [Canvas.visibleWhen](Canvas.md#attr-canvasvisiblewhen) or [FormItem.readOnlyWhen](FormItem.md#attr-formitemreadonlywhen).

Note that if this current user has been [marked as a super-user](#classmethod-authenticationsetsuperuser), [Authentication.getRoles](#classmethod-authenticationgetroles) will return the full set of available roles rather than the set of roles specified here.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| roles | [Array of String](#type-array-of-string) | false | — | set of roles which apply to the current user |

---
## ClassMethod: Authentication.isSuperUser

### Description
Has the current user been marked as a super-user via [Authentication.setSuperUser](#classmethod-authenticationsetsuperuser)?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isSuperUser | [Boolean](#type-boolean) | false | — | New super user status |

---
