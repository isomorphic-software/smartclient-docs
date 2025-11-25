# LoadScreenSettings Documentation

[← Back to API Index](../main.md)

---

## Attr: LoadScreenSettings.missingDSIsNotFatal

### Description
If true, server logic does not crash out if it cannot load a DataSource specified in the screen definition. Instead, a stub DataSource is returned, which consists of nothing except the ID and an `unableToLoad` flag, which client-side code can use to determine that the DataSource could not be loaded on the server. Optional, defaults to false (ie, a missing DataSource causes a crash by default)

**Flags**: IRW

---
## Attr: LoadScreenSettings.requestProperties

### Description
Specifies optional [RPCRequest](../main.md#object-rpcrequest) properties for the request.

**Flags**: IRW

---
## Attr: LoadScreenSettings.omitDataSources

### Description
DataSource IDs in the screen to skip and not load when the screen is loaded. It is assumed that these IDs represent DataSources that are already globally-bound on the client.

The special value of "\*" can be specified for this property to indicate that **all** DataSources should be omitted.

Note that, unless [LoadScreenSettings.omitLoadedDataSources](#attr-loadscreensettingsomitloadeddatasources) is false, all loaded DataSources will by default be added to whatever value you provide (making that also the default for this property).

**Flags**: IRW

---
## Attr: LoadScreenSettings.verifyAsError

### Description
Enable [verifyAsError](RPCManager.md#classattr-rpcmanagerverifyaserror) behavior only for requests using these settings.

### See Also

- [CreateScreenSettings.verifyAsError](CreateScreenSettings.md#attr-createscreensettingsverifyaserror)
- [LoadProjectSettings.verifyAsError](LoadProjectSettings.md#attr-loadprojectsettingsverifyaserror)

**Flags**: IRW

---
## Attr: LoadScreenSettings.omitLoadedDataSources

### Description
Whether to implicitly add all DataSources currently loaded on the client to [LoadScreenSettings.omitDataSources](#attr-loadscreensettingsomitdatasources) in [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen). Setting this false would only make sense in connection with setting [LoadScreenSettings.clobberDataSources](#attr-loadscreensettingsclobberdatasources) true, and would create more potential work for the server since many more DataSources could be output.

Note that here we consider the "loaded DataSources" to be those that are registered with the DataSource module (i.e. available by ID via [DataSource.get](DataSource.md#classmethod-datasourceget)), regardless of whether they're actually bound to the browser `window` object.

**Flags**: IRW

---
## Attr: LoadScreenSettings.suppressAutoDraw

### Description
If true, prevents any screen from being drawn when it's loaded, even if there's an explicit [Canvas.autoDraw](Canvas.md#attr-canvasautodraw):true setting on it.

**Flags**: IR

---
## Attr: LoadScreenSettings.locale

### Description
The name of a locale to use for resolving i18n tags in the component XML of the screen.

**Flags**: IRW

---
## Attr: LoadScreenSettings.willHandleError

### Description
Whether to call the provided [callback](Callbacks.md#method-callbacksloadscreencallback) even if an error was encountered trying to load the screen (or it was simply not found), so that you can run your own error handling. In this case, the screen and "suppressed globals" will be reported as null.

Note that for backward compatibility, the default of null means that the callback will still happen if the screen is not found, but not for a response with a server error. To have all such cases handled automatically, set this property explicitly false.

**Flags**: IR

---
## Attr: LoadScreenSettings.clobberDataSources

### Description
Should DataSources referenced by the screen clobber existing, globally-bound DataSources on the client when the screen is loaded? The default of false means that any DataSources defined in the screen will be discarded if they collide with existing, globally-bound DataSources.

Note that here we consider a DataSource to be "globally bound" if it can be retrieved by ID using the method [DataSource.get](DataSource.md#classmethod-datasourceget), regardless of whether it's actually bound to the browser `window` object.

**Flags**: IRW

---
## Attr: LoadScreenSettings.cacheScreen

### Description
Caches screen much like [RPCManager.cacheScreens](RPCManager.md#classmethod-rpcmanagercachescreens), so [RPCManager.isScreenCached](RPCManager.md#classmethod-rpcmanagerisscreencached) reports true.

**Flags**: IR

---
## Attr: LoadScreenSettings.verifyComponents

### Description
Enables verification that the created screen contains a component having a `localId` equal to the given key, and that it is an instance (or subclass) if the key's value. Example:
```
   {customerListGrid: 'ListGrid'}
 
```
You may verify the presence of Tabs, SectionStackSections, and FormItems by providing their names following the parent component's id in dot-separated notation. Example:
```
   {
     'mainTabSet.customersTab': 'ImgTab',
     'mainSectionStack.customerStackSection': 'SectionStackSection',
     'customerDetailsForm.customerNameItem': 'TextItem'
   }
 
```
Findings are always reported to the console, and may also be presented to the user with a warning dialog by setting [LoadScreenSettings.verifyAsError](#attr-loadscreensettingsverifyaserror) or [RPCManager.verifyAsError](RPCManager.md#classattr-rpcmanagerverifyaserror).

### See Also

- [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen)

**Flags**: IR

---
