# LoadProjectSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: LoadProjectSettings.drawFirstScreen

### Description
Determines whether the [LoadProjectSettings.currentScreenName](#attr-loadprojectsettingscurrentscreenname) screen is drawn after all screens have been loaded.

**Flags**: IRW

---
## Attr: LoadProjectSettings.currentScreenName

### Description
The name of the screen within the project to draw after loading. A null value means to use the currentScreenName as specified in the project file of the first project specified in the projectNames argument to [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject).

**Flags**: IRW

---
## Attr: LoadProjectSettings.screenNames

### Description
A comma-separated string containing the names of screens within the project that should be loaded. A null value causes all screens to be loaded.

**Flags**: IRW

---
## Attr: LoadProjectSettings.locale

### Description
The name of a locale to use for resolving i18n tags in the component XML of the screen. The default value of null omits locale loading, which effectively means the framework default "en" locale is used.

**Flags**: IRW

---
## Attr: LoadProjectSettings.ownerId

### Description
Use this attribute to specify a project owner. Only applicable if project source supports owner identification.

**Flags**: IRW

---
