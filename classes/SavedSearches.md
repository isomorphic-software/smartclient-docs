# SavedSearches Documentation

[← Back to API Index](../reference.md)

---

## Class: SavedSearches

### Description
Data components such as [ListGrid](ListGrid_1.md#class-listgrid) or [TileGrid](TileGrid.md#class-tilegrid) may allow users to set up their own search criteria within an application, either via an external [SearchForm](SearchForm.md#class-searchform), or through built in UI such as the [ListGrid.filterEditor](ListGrid_1.md#attr-listgridfiltereditor).

The "Saved Search" subsystem allows users to save out their criteria (and in some cases user-configured view state) so when the application is reloaded they can easily restore a search or view from a previous session.

_**Note:** The SavedSearches feature requires [SmartClient Pro](https://www.smartclient.com/product/) or better._

User interface components for storing and retreiving saved searches are available via the built in ListGrid features [ListGrid.canSaveSearches](ListGrid_1.md#attr-listgridcansavesearches) and [ListGrid.savedSearchStoredState](ListGrid_1.md#attr-listgridsavedsearchstoredstate), as well as the explicit the [SavedSearchForm](SavedSearchForm.md#class-savedsearchform) and [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) classes.

#### The SavedSearches class
`SavedSearches` is a "singleton" class that provides central handling of storing and loading saved search data.

You acquire the `SavedSearches` singleton via [SavedSearches.get](#classmethod-savedsearchesget) and you can configure defaults via [Class.addProperties](Class.md#method-classaddproperties) or [Class.changeDefaults](Class.md#classmethod-classchangedefaults).

Saved searches are stored [serialized as JSON](JSONEncoder.md#class-jsonencoder) in [DataSource](DataSource.md#class-datasource) Records.  
By default saved searches are stored in [HTML5 browser localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) via automatically generated custom DataSources. In this mode the searches are only retained for a specific user on a particular machine, and searches cannot be shared with other users - but this approach is sufficient for many applications, works out of the box, does not require any storage and has no impact on scalability.

For more capable saved search storage and retrieval, an explicit saved search dataSource backed by permanent storage such as an SQL database table may be specified.  
Typically this is done by setting up the [SavedSearches.defaultDataSource](#attr-savedsearchesdefaultdatasource). This will store searches for all users and for every component and the same dataSource may even be used for multiple applications.  
For finer grained control, individual saved search dataSources may also be specified [per component](ListGrid_1.md#attr-listgridsavedsearchds).

See [SavedSearches.getSavedSearchDataSource](#method-savedsearchesgetsavedsearchdatasource) for how to retrieve the dataSource for a component.

A SavedSearch dataSource has the following fields, some of which are optional, all of which can be renamed as needed. (Click the links to see the purpose of each field):

*   ["pk"](#attr-savedsearchesprimarykeyfield) (primary key field, typically of type "sequence")
*   ["data"](#attr-savedsearchesdatafield)
*   ["searchName"](#attr-savedsearchessearchnamefield)
*   ["componentId"](#attr-savedsearchescomponentidfield)
*   ["projectId"](#attr-savedsearchesprojectidfield)
*   ["screenId"](#attr-savedsearchesscreenidfield)
*   ["applicationId"](#attr-savedsearchesapplicationidfield)
*   ["userId"](#attr-savedsearchesuseridfield)
*   ["admin"](#attr-savedsearchesadminfield) See "Admin-Configured Shared Searches" below.
*   ["isDefault"](#attr-savedsearchesdefaultfield), See "Default Searches" below.
*   ["isSharedDefault"](#attr-savedsearchesadmindefaultfield), See "Default Searches" below.

In your SDK, look for `sc_SavedSearches.ds.xml` for a sample SQL-based implementation of saved-search (entirely declarative). Note that [DataSource.cacheAllData](DataSource.md#attr-datasourcecachealldata) is set to true - this causes all searches applicable to a given user to be loaded in advance, the first time any component requests saved searches. For most applications, this is the right approach, and is much better than performing server requests each time a new component is shown that _might_ have saved searches.

Note that the SavedSearches system can be used to store any kind of component setting; in particular, [ListGrids](ListGrid_1.md#attr-listgridcansavesearches) used `SavedSearches` to store complete [viewState](ListGrid_2.md#method-listgridgetviewstate), which includes field order & visibility, sorting and group state in addition to search criteria.

#### Admin-Configured Shared Searches

_Shared searches_ (also referred to as _"Admin Searches"_) are special searches that appear for **all** users, as pre-configured default saved searches. While any user can create and edit their own personal saved searches, admin searches can only be created or edited by users with the [SavedSearches.adminRole](#attr-savedsearchesadminrole) (see below).

Admin searches are not available when no dataSource was configured to store the savedSearch data. In this case a user's searches are stored to their machine rather than in a central database, and the concept of sharing admin-created searches does not apply.

Admin searches are identified by either having the [userIdField](#attr-savedsearchesuseridfield) null, or by the separate boolean [adminField](#attr-savedsearchesadminfield) set to true.

UI components such as [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) will offer a UI for adding, editing and removing admin searches if the user has the [SavedSearches.adminRole](#attr-savedsearchesadminrole), as determined by [Authentication.hasRole](Authentication.md#classmethod-authenticationhasrole).

In addition to this, for security reasons the server should also enforce role-based authentication for creating and editing admin searches.  
Note: the sample `sc_SavedSearches.ds.xml` dataSource has no "admin" field to identify shared or "admin" searches. Instead records in this dataSource with "userId" set to null are considered to be shared searches.  
The `ownerIdField`, `ownerIdNullAccess` and `ownerIdNullRole` attributes enforce the appropriate restrictions for editing admin searches -- these settings allow all users to view records with `userId:null` but only users with the "admin" role may create or edit them.

#### Default Searches

Default searches are searches which will be automatically applied to a component on draw. The SavedSearch subsystem supports two notions of "default" searches. A user may select their personal default search, in which case the next time they load the page this search will be applied to the component automatically. Or an administrator may mark a shared admin search as the default for all users. In this case anyone who loads the application will see this search applied.

If a user has a stored personal default search preference, this always takes precedence over any admin-default search.

Like any admin-searches, admin-default searches only apply when a dataSource was configured to store the savedSearch data.

#### Saving default searches
If [SavedSearches.saveDefaultSearchToServer](#attr-savedsearchessavedefaultsearchtoserver) is false (the default), the user-default search preference will be stored in browser `localStorage`.  
This is done because the user may choose an Admin Search as their default search, and since Admin Search records are shared between all users, we can't mark the Admin Search record in the database as the default for a specific user (at least not without more complex storage).  
The drawback is that a user switching browsers or device will not have their default search preserved.

If you want to persist default searches chosen by the user to permanent storage on the server, you can set [SavedSearches.saveDefaultSearchToServer](#attr-savedsearchessavedefaultsearchtoserver) to true. In this case the SavedSearch dataSource must include a boolean [SavedSearches.defaultField](#attr-savedsearchesdefaultfield). Typically this will need to be populated via custom server logic when fetching records to indicate that the record in question is the chosen default for the current user. When `saveDefaultSearchToServer` is true, the client will issue a custom update operation when the user wants to modify their default search - see [SavedSearches.setDefaultUserSearchOperation](#attr-savedsearchessetdefaultusersearchoperation).

Admin default searches are stored on the server regardless of whether [SavedSearches.saveDefaultSearchToServer](#attr-savedsearchessavedefaultsearchtoserver) is true. The dataSource should include a boolean [SavedSearches.adminDefaultField](#attr-savedsearchesadmindefaultfield) to indicate that an admin search record is the shared-default search.  
If an admin user updates a record to be the new shared default search, the client will issue a different custom update operation - see [SavedSearches.setDefaultAdminSearchOperation](#attr-savedsearchessetdefaultadminsearchoperation).  
Note that we'd recommend marking this operation as `requiresRole="admin"` on the server, as in the sample `sc_SharedSearches.ds.xml` dataSource configuration.

#### Identifying components associated with Saved Searches

Stored saved search records will have the `componentId` field set to the identifier returned by [SavedSearches.getSavedSearchId](#method-savedsearchesgetsavedsearchid) for a component. By default this method returns an identifer based on the a [local ID](Canvas.md#method-canvasgetlocalid) and [DataSource ID](DataBoundComponent.md#attr-databoundcomponentdatasource). This means that if you assign a unique ID to a component that saves searches, and don't change that ID, stored saved searches will always be associated with the component and its current DataSource.

If you don't set a unique global ID on the component, and your component isn't part of a Reify screen, and so doesn't have a separate [local ID](Canvas.md#method-canvasgetlocalid), the default saved search identifier is not guaranteed to be consistent across changes to your app, and in that case, previously stored searches will no longer be associated with the component.

Alternatively you can bypass the [ID](Canvas.md#method-canvasgetlocalid) dependency altogether and define an explicit [DataBoundComponent.savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid). This allows you to define a stable identifier for storing saved searches without setting a component [ID](Canvas.md#attr-canvasid).

Note that developers may explicitly change the [DataBoundComponent.savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid) at runtime. In this case, if the saved search ID changes, the component will be associated with a new set of saved searches. When an explicit `savedSearchId` is provided, it will not automatically be changed if a new DataSource is bound to the component. To keep the saved searches applicable to the current DataSource, developers may want to explicitly update `savedSearchId` in this case.

#### Security Concerns

If you provide your own [DataSource for storing searches](#attr-savedsearchesdefaultdatasource), you should enforce the following restrictions on the server:

*   Limiting fetch operations such that the logged-in user can only see their own searches (searches where the current userId matches the [userIdField](#attr-savedsearchesuseridfield)), and shared or "admin" searches (searches where the [adminField](#attr-savedsearchesadminfield) is `true`, or if there is no admin field, searches where the `userIdField` value is null).
*   Ensuring that logged in users without the [adminRole](#attr-savedsearchesadminrole) can only add, edit and remove records where the [userIdField](#attr-savedsearchesuseridfield) matches their userId.
*   For logged in users with the [adminRole](#attr-savedsearchesadminrole), also allowing users to add, update and remove admin searches. What this means in concrete terms depends on whether the dataSource includes an [adminField](#attr-savedsearchesadminfield).  
    If an adminField exists, admin users are exempt from userId restrictions when editing or removing records where this field value is set to true. When adding a new record it is still recommended the admin user's own userId should be stored in the `userIdField`.  
    If no adminField exists, admin searches are identified by having the `userIdField` set to `null`. In this case admin users should be able to add, remove and edit records where the `userIdField` matches their own userId, or is null.

If you are not providing your own [DataSource for storing searches](#attr-savedsearchesdefaultdatasource), searches will be stored to each user's browser LocalStorage. Developers should be aware that objects stored in LocalStorage are accessible by all applications deployed to the same host + port. This means that if you're loading multiple SmartClient applications from the save server they could potentially access each others' SavedSearches from localStorage, if the same userName and componentId exist in both applications.  
This should not typically be an issue, as we default the [applicationId](#attr-savedsearchesapplicationid) value to the `window.location.pathname` which can't be shared by two applications deployed to the same server, but it could come up if [allowNullApplicationId](#attr-savedsearchesallownullapplicationid) was set to true.

`searchName` field escaping: by default, any character is allowed in the `searchName` field, and `searchName` are [escaped](DataSourceField.md#attr-datasourcefieldescapehtml) when displayed by built-in UI components. If you provide your own UI for saved searches, you should escape the `searchName` field before displaying. Otherwise, users could render your application partly non-functional by using special characters or inline script, or a malicious admin could inject code into other user's browsers. If you prefer to just limit the `searchName` field to non-special characters, you can just add a [dataSourceField validator](DataSourceField.md#attr-datasourcefieldvalidators) to do this, and the built-in UIs for saved search will handle the validation error as expected (block the save or edit and tell the user what's wrong).

If you fail to implement all of the above, then it will be possible for users to save searches for other users or as admin searches, and those saved searches could have malicious code that is then injected into other user's browsers.

As noted above - the SavedSearches feature requires [SmartClient Pro](https://www.smartclient.com/product/) or better.

---
## Attr: SavedSearches.screenIdField

### Description
Type: "string". Required because component IDs are not unique if components are loaded as [screens](RPCManager.md#classmethod-rpcmanagerloadscreen), especially [Reify Screens](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers).

**Flags**: RW

---
## Attr: SavedSearches.setDefaultAdminSearchOperation

### Description
[operationId](OperationBinding.md#attr-operationbindingoperationid) for the custom update operation to invoke when updating the default admin search.

The update data for this operation will be the saved search record to mark as the shared default with the [SavedSearches.adminDefaultField](#attr-savedsearchesadmindefaultfield) set to indicate whether the saved search is being set or cleared.

When marking a search as the new shared default, the dataSource implementation for this custom update operation must clear the adminDefaultField value on any previous shared default search. The server should also use the `dsResponse.relatedUpdates` feature to notify the client that the previous default was unset.

**Flags**: IRW

---
## Attr: SavedSearches.savedSearchIDPrefix

### Description
Prefix applied to a specified [DataBoundComponent.savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid) by [SavedSearches.getSavedSearchId](#method-savedsearchesgetsavedsearchid). This is required to handle the case where a component's savedSearchId matches the ID of some other component.

**Flags**: IRA

---
## Attr: SavedSearches.projectIdField

### Description
Type: "string". Required because component IDs are not unique if components are loaded as [screens](RPCManager.md#classmethod-rpcmanagerloadscreen), especially [Reify Screens](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers).

**Flags**: RW

---
## Attr: SavedSearches.searchNameField

### Description
Type: "string". Name dataSource field used for storing names of saved searches.

**Flags**: RW

---
## Attr: SavedSearches.userIdField

### Description
Type: "string" _(optional)_. This stores the `userId` of the user saving the search, populated from [the current userId](Authentication.md#classmethod-authenticationgetcurrentuserid). This field is only optional in the sense that you could instead build a DataSource that returns user-specific saved searches through some other mechanism (for example, by inserting a userId value and forcing userId criteria on the server side).

**Flags**: RW

---
## Attr: SavedSearches.applicationIdField

### Description
Type: "string" _(optional)_. This field exists to allow a single DataSource to be used across multiple applications without colliding on `componentId`. Set [SavedSearches.applicationId](#attr-savedsearchesapplicationid) to cause all search lookups to use `applicationId` as criteria, and all newly saved searches to store that `applicationId`.

Note that if [SavedSearches.applicationId](#attr-savedsearchesapplicationid) is not explicitly set, the [window.location.pathname](https://www.w3schools.com/jsref/prop_loc_pathname.asp) will be used as a default. This behavior can be disabled by setting [SavedSearches.allowNullApplicationId](#attr-savedsearchesallownullapplicationid) to true.

**Flags**: RW

---
## Attr: SavedSearches.adminField

### Description
_(optional)_, type "boolean". Designates this search as an admin search, visible to all users

**Flags**: RW

---
## Attr: SavedSearches.componentIdField

### Description
Type: "string". Stores a unique ID for the component the saved search is associated with. This does not have to be the [Canvas.ID](Canvas.md#attr-canvasid) and is usually a [AutoTestLocator](../reference_2.md#type-autotestlocator)

**Flags**: RW

---
## Attr: SavedSearches.setDefaultUserSearchOperation

### Description
[operationId](OperationBinding.md#attr-operationbindingoperationid) for the custom update operation to invoke when updating the default user search if [SavedSearches.saveDefaultSearchToServer](#attr-savedsearchessavedefaultsearchtoserver) is true.

The update data for this operation will be the saved search record to mark as the user default with the [SavedSearches.defaultField](#attr-savedsearchesdefaultfield) set to indicate whether the saved search is being set or cleared.

**Flags**: IRA

---
## Attr: SavedSearches.defaultField

### Description
_optional_, type "boolean". Designates this search as the default search for this user.

This field is only required if [SavedSearches.saveDefaultSearchToServer](#attr-savedsearchessavedefaultsearchtoserver) is true.  
See the "Default Searches" section of the [SavedSearches overview](#class-savedsearches) for more information.

**Flags**: RW

---
## Attr: SavedSearches.applicationId

### Description
The applicationId that will be saved to ["applicationIdField"](#attr-savedsearchesapplicationidfield) to disambiguate from other applications that use the same dataSource.

If no applicationId was specified, [SavedSearches.getApplicationId](#method-savedsearchesgetapplicationid) will return the current [window.location.pathname](https://www.w3schools.com/jsref/prop_loc_pathname.asp) by default. This behavior can be turned off by setting [allowNullApplicationId:true](#attr-savedsearchesallownullapplicationid).

The `applicationId` allows the same dataSource to be used to store savedSearches for different applications. It also ensures that if no [explicit dataSource](#attr-savedsearchesdefaultdatasource) was specified, and searches are being stored to [browser local storage](#method-savedsearchesgetlocaldatasource), saved searches will be associated with the current application even if another application running under the same domain/port has a component with the same [componentId](#method-savedsearchesgetsavedsearchid).

**Flags**: RW

---
## Attr: SavedSearches.primaryKeyField

### Description
Type: "string". Name dataSource field used as the primary key.

This is expected to be populated automatically when new search records are added to the data set, so will typically be of [type:sequence](../reference_2.md#type-fieldtype).

**Flags**: RW

---
## Attr: SavedSearches.adminRole

### Description
The name of the adminRole (used via [Authentication.hasRole](Authentication.md#classmethod-authenticationhasrole)) to check to see if the current user has admin privileges.

**Flags**: RW

---
## Attr: SavedSearches.allowNullApplicationId

### Description
If [SavedSearches.applicationId](#attr-savedsearchesapplicationid) is not explicitly specified, it will be defaulted to the current [window.location.pathname](https://www.w3schools.com/jsref/prop_loc_pathname.asp).

Set this flag to true to disable this behavior and allow SavedSearches to be stored with no explicit applicationId.

**Flags**: IRWA

---
## Attr: SavedSearches.adminDefaultField

### Description
Type "boolean". Designates an admin search as the shared default search for all users.

The user's _chosen_ default search is normally stored separately; the `adminDefaultField` exists as a way to mark a search as the default for a user that hasn't chosen one yet.

See the "Default Searches" section of the [SavedSearches overview](#class-savedsearches) for more information.

**Flags**: RW

---
## Attr: SavedSearches.dataField

### Description
Type: "string". Name dataSource field used for storing the saved search itself with at least 8k of storage (it's possible for searches to get yet larger, but rare).

**Flags**: RW

---
## Attr: SavedSearches.defaultDataSource

### Description
Default DataSource used for persistence of saved searches. This may be overridden for individual components via [component.savedSearchDS](ListGrid_1.md#attr-listgridsavedsearchds).

If no default dataSource is explicitly provided, the system will automatically generated a custom DataSource for each component that stores saved searches in HTML5 `localStorage`. See [SavedSearches.getLocalDataSource](#method-savedsearchesgetlocaldatasource).

This means the searches are only retained for that specific user on that particular machine, and searches cannot be shared with other users. However, this approach does mean that you don't have to provide storage for saved searches and saving searches has no impact on scalability.

**Flags**: RW

---
## Attr: SavedSearches.saveDefaultSearchToServer

### Description
Should a user's default search preferences be stored to the server?

Default user searches are normally saved in browser `localStorage` - see the "Default Searches" section of the [SavedSearches](#class-savedsearches) doc and also the docs for [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch).

If you want to store the default search on the server instead, you can add an [OperationBinding](OperationBinding.md#class-operationbinding) of type "update" called ["setDefaultUserSearch"](#attr-savedsearchessetdefaultusersearchoperation) to your [SavedSearches.defaultDataSource](#attr-savedsearchesdefaultdatasource). This will be called with the PK value of the record to be made the default search, plus a boolean true value for the [SavedSearches.defaultField](#attr-savedsearchesdefaultfield). The expectation is that the search identified by the PK is marked as default and any other searches previously marked as default are unmarked.

Since Admin Search records are shared among all users, the expectation is that the underlying storage actually stores default markers separately from admin searches, and the [SavedSearches.defaultDataSource](#attr-savedsearchesdefaultdatasource) is acting as a [facade DataSource](../kb_topics/dsFacade.md#kb-topic-datasource-facade-pattern).

Updating a user's default search in the dataSource data should not modify any admin-default search.

**Flags**: IR

---
## Attr: SavedSearches.offlineStorageKey

### Description
If no explicit [SavedSearches.defaultDataSource](#attr-savedsearchesdefaultdatasource) was provided, a custom HTML5 `local storage` backed dataSource will be automatically created per component to store saved searches (see [SavedSearches.getLocalDataSource](#method-savedsearchesgetlocaldatasource)).

This property denotes a base storage key for these dataSources.  
The [calculated savedSearch identifier](#method-savedsearchesgetsavedsearchid) for the component will be appended to this value to create the key to use when storing serialized searches in local storage.

**Flags**: IR

---
## ClassMethod: SavedSearches.get

### Description
Singleton accessor method.

### Returns

`[SavedSearches](#type-savedsearches)` — an instance of SavedSearches

---
## Method: SavedSearches.getApplicationId

### Description
Retrieves the value to saves as the link{SavedSearches.applicationIdField,"applicationIdField"} value for saved searches within this application.

Returns [this.applicationId](#attr-savedsearchesapplicationid) if specified, otherwise the current [window.location.pathname](https://www.w3schools.com/jsref/prop_loc_pathname.asp) will be returned by default.  
Set [SavedSearches.allowNullApplicationId](#attr-savedsearchesallownullapplicationid) to suppress this behavior of defaulting to the location.pathname.

### Returns

`[String](#type-string)` — applicationId to be stored for saved searches.

---
## Method: SavedSearches.getLocalDataSource

### Description
This method returns an automatically generated custom DataSource to store saved searches for a component in HTML5 localStorage. Note that this dataSource will only be used to store savedSearches if there is no [shared default dataSource](#attr-savedsearchesdefaultdatasource) specified, and if [ListGrid.savedSearchDS](ListGrid_1.md#attr-listgridsavedsearchds) is not set for the component.

The offline storage key for the data will be generated by combining the [SavedSearches.offlineStorageKey](#attr-savedsearchesofflinestoragekey) with the component identifier retrieved from [SavedSearches.getSavedSearchId](#method-savedsearchesgetsavedsearchid).

**Note:** The dataSources returned by this method will suppress logging their requests to the [Developer Console RPC tag](../kb_topics/devConsoleRPCTab.md#kb-topic-the-developer-console-rpc-tab) by default. This is done so developers can more easily see dataSource requests and responses that were explicitly initiated by application code, to simplify debugging. However, if a developer has explicitly created a SavedSearch dataSource either as the [global default](#attr-savedsearchesdefaultdatasource) or at the [component level](ListGrid_1.md#attr-listgridsavedsearchds), requests to access and update SavedSearch data will be logged as with any other dataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| componentId | [Canvas](#type-canvas)|[String](#type-string) | false | — | Component to retrieve the dataSource for, or saved search component identifier as returned by [SavedSearches.getSavedSearchId](#method-savedsearchesgetsavedsearchid) |

### Returns

`[DataSource](#type-datasource)` — dataSource for SavedSearches backed by HTML5 local storage.

---
## Method: SavedSearches.getSavedSearchDataSource

### Description
Retrieves the DataSource used for persistence of saved searches for some component.

If [component.savedSearchDS](ListGrid_1.md#attr-listgridsavedsearchds) is specified this will be returned.  
Otherwise if an explicit [default dataSource](#attr-savedsearchesdefaultdatasource) was specified, it will be used.  

If no explicit dataSource was provided either at the component level or as a default for all SavedSearches, this method will return the result of [SavedSearches.getLocalDataSource](#method-savedsearchesgetlocaldatasource).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [DataBoundComponent](#type-databoundcomponent) | false | — | component to retrieve the SavedSearch dataSource for |

### Returns

`[DataSource](#type-datasource)` — the DataSource used to store saved searches for the target component

---
## Method: SavedSearches.getSavedSearchId

### Description
Returns the identifier used to uniquely identify saved searches for some component.

This is the value that will be set on the [SavedSearches.componentIdField](#attr-savedsearchescomponentidfield) when storing saved searches to a DataSource.  
If there is no explicly specified dataSource for storing saved searches, it will also be used to configure the offline storage key for data stored by the automatically generated [local storage backed dataSource](#method-savedsearchesgetlocaldatasource) for the component.

The returned value is calculated as follows:

*   If [DataBoundComponent.savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid) is set, this method will return the [SavedSearches.savedSearchIDPrefix](#attr-savedsearchessavedsearchidprefix) + [component.savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid).
*   Otherwise, the component's [local ID](Canvas.md#method-canvasgetlocalid) (which falls back to the [global ID](Canvas.md#attr-canvasid) if no local ID is present) will be returned. If [DataBoundComponent.showSavedSearchesByDS](DataBoundComponent.md#attr-databoundcomponentshowsavedsearchesbyds) is set and the component has a DataSource, the method will instead return the local ID + ":" + the DataSource ID, where the delimiter avoids potential collisions otherwise possible.

Note: The returned ID string is not guaranteed to be immutable over a widget's lifespan.

If no explicit component `savedSearchId` was set, the system will rely on the widget's local or global ID, which can change unless explicit due to app changes, and on the DataSource ID bound to the component, which may change at runtime. Since this property is used to identify the savedSearch records associated with this component, when it changes a different set of saved searches will be available to the user.

If you want to control this explicitly, you can do so by setting an explicit [savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid). Changing the `savedSearchId` at runtime also allows you to deliberately associate a component with a new set of SavedSearches depending on application state. One common case where this might be desirable is if a component is bound to a dataSource and you want to bind to a new DataSource where the savedSearch criteria would not be applicable.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [Canvas](#type-canvas) | false | — | component to retrieve the identifier for |

### Returns

`[String](#type-string)` — component saved search ID

---
## Method: SavedSearches.setDefaultUserSearch

### Description
Update the user's default search.

This will invoke the [SavedSearches.setDefaultUserSearchOperation](#attr-savedsearchessetdefaultusersearchoperation) if [SavedSearches.saveDefaultSearchToServer](#attr-savedsearchessavedefaultsearchtoserver) is true, otherwise it will persist the default into offline storage

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [DataBoundComponent](#type-databoundcomponent) | false | — | component being updated |
| isDefault | [boolean](../reference.md#type-boolean) | false | — | whether the default is being set to true or false |
| searchRecord | [Record](#type-record) | false | — | record containing details of the search to be updated |
| callback | [Callback](../reference.md#type-callback) | false | — | callback to invoke when the search has been updated. Takes no arguments. |

---
## Method: SavedSearches.getDefaultDataSource

### Description
Retrieves the DataSource used for persistence of saved searches.

If a [SavedSearches.defaultDataSource](#attr-savedsearchesdefaultdatasource) was explicitly specified, it will be returned, otherwise this method returns null.

To retrieve the dataSource used to store savedSearches for a specific component see [SavedSearches.getSavedSearchDataSource](#method-savedsearchesgetsavedsearchdatasource)

### Returns

`[DataSource](#type-datasource)` — DataSource used to persist saved searches to the server

---
## Method: SavedSearches.setDefaultAdminSearch

### Description
Update the admin default search for some component

This will invoke the [SavedSearches.setDefaultAdminSearchOperation](#attr-savedsearchessetdefaultadminsearchoperation) to update the admin search record on the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [DataBoundComponent](#type-databoundcomponent) | false | — | component being updated |
| isDefault | [boolean](../reference.md#type-boolean) | false | — | whether the default is being set to true or false |
| searchRecord | [Record](#type-record) | false | — | record containing details of the search to be updated |
| callback | [Callback](../reference.md#type-callback) | false | — | callback to invoke when the search has been updated. Takes no arguments. |

---
