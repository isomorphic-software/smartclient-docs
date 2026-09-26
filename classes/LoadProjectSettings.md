# LoadProjectSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: LoadProjectSettings.drawFirstScreen

### Description
Determines whether the [LoadProjectSettings.currentScreenName](#attr-loadprojectsettingscurrentscreenname) screen is drawn after all screens have been loaded. If not drawn, the screen will not be created.

This setting only affects the first project specified in the `projectNames` argument to [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject).

### See Also

- [Project.createScreen](Project.md#method-projectcreatescreen)
- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

**Flags**: IRW

---
## Attr: LoadProjectSettings.currentScreenName

### Description
The name of the screen within the project to return first when loading. A null value means to use the currentScreenName as specified in the project file.

This setting only affects the first project specified in the `projectNames` argument to [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject).

**Flags**: IRW

---
## Attr: LoadProjectSettings.requestProperties

### Description
Allows customizing the projectLoader servlet request properties. Properties that conflict with proper operation of the servlet will be overridden by [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject).

**Flags**: IRA

---
## Attr: LoadProjectSettings.verifyAsError

### Description
Enable [verifyAsError](RPCManager.md#classattr-rpcmanagerverifyaserror) behavior only for requests using these settings.

### See Also

- [CreateScreenSettings.verifyAsError](CreateScreenSettings.md#attr-createscreensettingsverifyaserror)
- [LoadProjectSettings.verifyAsError](#attr-loadprojectsettingsverifyaserror)

**Flags**: IRW

---
## Attr: LoadProjectSettings.password

### Description
Overrides [Reify.password](Reify.md#classattr-reifypassword) setting the account password for [Reify.loadProject](#method-reifyloadproject).

Note that this setting only applies when using [Reify.loadProject](#method-reifyloadproject).

**Flags**: IR

---
## Attr: LoadProjectSettings.verifyComponents

### Description
Enables verification that any screen [created](#attr-loadprojectsettingsdrawfirstscreen) on load contains a component having a `localId` equal to the given key, and that it is an instance (or subclass) of the key's value. Example:
```
   {'customerListGrid': 'ListGrid'}
 
```
You may verify the presence of Tabs, SectionStackSections, and FormItems by providing their names following the parent component's id in dot-separated notation. Example:
```
   {
     'mainTabSet.customersTab': 'ImgTab',
     'mainSectionStack.customerStackSection': 'SectionStackSection',
     'customerDetailsForm.customerNameItem': 'TextItem'
   }
 
```
Findings are always reported to the console, and may also be presented to the user with a warning dialog by setting [LoadProjectSettings.verifyAsError](#attr-loadprojectsettingsverifyaserror) or [RPCManager.verifyAsError](RPCManager.md#classattr-rpcmanagerverifyaserror).

### See Also

- [LoadProjectSettings.verifyDataSources](#attr-loadprojectsettingsverifydatasources)
- [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject)

**Flags**: IR

---
## Attr: LoadProjectSettings.allowPlaceholders

### Description
Should [Placeholders](Placeholder.md#class-placeholder) in loaded screens be rendered as placeholders? If property is not set actual components are created instead of the Placeholders.

**Flags**: IR

---
## Attr: LoadProjectSettings.userName

### Description
Overrides [Reify.userName](Reify.md#classattr-reifyusername) setting the account name for [Reify.loadProject](#method-reifyloadproject).

Note that this setting only applies when using [Reify.loadProject](#method-reifyloadproject).

**Flags**: IR

---
## Attr: LoadProjectSettings.dataContext

### Description
[DataContext](../reference.md#object-datacontext) that will be provided to the top-level component as [dataContext](Canvas.md#attr-canvasdatacontext) in each screen cached for the project.

To understand how `dataContext` is used to automatically populate [DataBoundComponents](../reference.md#interface-databoundcomponent), see [Canvas.autoPopulateData](Canvas.md#attr-canvasautopopulatedata).

### Groups

- dataContext

**Flags**: IR

---
## Attr: LoadProjectSettings.screenNames

### Description
A comma-separated string containing the names of screens within the project that should be loaded. A null value causes all screens to be loaded.

This setting only affects the first project specified in the `projectNames` argument to [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject).

**Flags**: IRW

---
## Attr: LoadProjectSettings.locale

### Description
The name of a locale to use for resolving i18n tags in the component XML of the screen. The default value of null omits locale loading, which effectively means the framework default "en" locale is used.

**Flags**: IRW

---
## Attr: LoadProjectSettings.omitLoadedDataSources

### Description
Whether to implicitly add all DataSources currently loaded on the client to [LoadProjectSettings.omitDataSources](#attr-loadprojectsettingsomitdatasources) in [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject). Setting this false would only make sense in connection with setting [LoadProjectSettings.clobberDataSources](#attr-loadprojectsettingsclobberdatasources) true, and would create more potential work for the server since many more DataSources could be output.

Note that here we consider the "loaded DataSources" to be those that are registered with the DataSource module (i.e. available by ID via [DataSource.get](DataSource.md#classmethod-datasourceget)), regardless of whether they're actually bound to the browser `window` object.

**Flags**: IRW

---
## Attr: LoadProjectSettings.clobberDataSources

### Description
Should DataSources referenced by the [first screen](#attr-loadprojectsettingsdrawfirstscreen) clobber existing, globally-bound DataSources on the client if the screen is created? The default of false means that any DataSources defined in the screen will be discarded if they collide with existing, globally-bound DataSources.

Here we consider a DataSource to be "globally bound" if it can be retrieved by ID using the method [DataSource.get](DataSource.md#classmethod-datasourceget), regardless of whether it's actually bound to the browser `window` object.

Note that this setting only has an impact if [LoadProjectSettings.drawFirstScreen](#attr-loadprojectsettingsdrawfirstscreen) is true.

**Flags**: IRW

---
## Attr: LoadProjectSettings.projectLoaderPath

### Description
Path relative to the [server root](#attr-loadprojectsettingsserverurl), to target to use the project loader servlet, instead of [Reify.projectLoaderPath](Reify.md#classattr-reifyprojectloaderpath).

Note that this setting only applies when using [Reify.loadProject](#method-reifyloadproject).

**Flags**: IR

---
## Attr: LoadProjectSettings.omitDataSources

### Description
DataSource IDs in the project to skip and not load when the project is loaded. It is assumed that these IDs represent DataSources that are already globally-bound on the client.

The special value of "\*" can be specified for this property to indicate that **all** DataSources should be omitted.

Note that, unless [LoadProjectSettings.omitLoadedDataSources](#attr-loadprojectsettingsomitloadeddatasources) is false, all loaded DataSources will by default be added to whatever value you provide (making that also the default for this property).

**Flags**: IR

---
## Attr: LoadProjectSettings.serverURL

### Description
URL of Reify server to use when calling [Reify.loadProject](#method-reifyloadproject) instead of [Reify.serverURL](Reify.md#classattr-reifyserverurl).

Note that this setting only applies when using [Reify.loadProject](#method-reifyloadproject).

**Flags**: IR

---
## Attr: LoadProjectSettings.timeout

### Description
Sets the timeout for the projectLoader servlet request. This is a convenience property so that [LoadProjectSettings.requestProperties](#attr-loadprojectsettingsrequestproperties) need not be set. If unset, the timeout is determined by [RPCManager.defaultTimeout](RPCManager.md#classattr-rpcmanagerdefaulttimeout).

**Flags**: IRA

---
## Attr: LoadProjectSettings.verifyDataSources

### Description
Enables DataSource verification, causing warnings to be output about differences between DataSources loaded with a project vs those that are already present in the page (if any are present). Findings are always reported to the console, and may also be presented to the user with a warning dialog by setting [LoadProjectSettings.verifyAsError](#attr-loadprojectsettingsverifyaserror). For discussion of which issues will be reported and how, see [DataSource.verifyDataSourcePair](DataSource.md#classmethod-datasourceverifydatasourcepair).

Setting this property will default [LoadProjectSettings.omitLoadedDataSources](#attr-loadprojectsettingsomitloadeddatasources) to false, and will cause the special [LoadProjectSettings.omitDataSources](#attr-loadprojectsettingsomitdatasources) value of "\*" to be ignored (but not other ID values). It's important to keep in mind when using this property that loading a project with all of its DataSources can be very slow, if there is a large amount of test data, for example.

Note that this behavior can be enabled globally by setting [Reify.verifyDataSources](Reify.md#classattr-reifyverifydatasources) to true. It often makes sense to set it there during development, and turn off in production, since it slightly slows down DataSource loading.

### See Also

- [LoadProjectSettings.verifyComponents](#attr-loadprojectsettingsverifycomponents)
- [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject)

**Flags**: IR

---
## Attr: LoadProjectSettings.ownerId

### Description
Use this attribute to specify a project owner. Only applicable if project source supports owner identification.

**Flags**: IRW

---
## Attr: LoadProjectSettings.willHandleError

### Description
Whether to call the provided [callback](Callbacks.md#method-callbacksloadprojectcallback) even if an error was encountered trying to load the project, so that you can run your own error handling. In this case, the list of projects loaded by the callback will be reported as empty.

If true, the framework won't log any messages specifically reporting the failure to load the requested projects, but depending on the situation, the browser itself may report errors from the servlet request in the console.

### See Also

- [RPCManager.getLoadProjectErrorStatus](RPCManager.md#classmethod-rpcmanagergetloadprojecterrorstatus)
- [RPCManager.getLoadProjectErrorMessage](RPCManager.md#classmethod-rpcmanagergetloadprojecterrormessage)

**Flags**: IR

---
