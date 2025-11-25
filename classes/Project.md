# Project Documentation

[← Back to API Index](../main.md)

---

## Class: Project

### Description
Represents a [reify](../kb_topics/reify.md#kb-topic-reify-overview) project loaded from the server via [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject). A project contains cached screens and [DataSources](DataSource.md#class-datasource) that can be used to create actual screens by calling [Project.createScreen](#method-projectcreatescreen) or [Project.createStartScreen](#method-projectcreatestartscreen).

### See Also

- [Reify.loadProject](#method-reifyloadproject)

---
## ClassMethod: Project.get

### Description
Returns a cached project given its name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | name of project to retrieve |

### Returns

`[Project](#type-project)` — cached project, or null if it's not cached

---
## Method: Project.destroy

### Description
Releases cached screens and [DataSources](DataSource.md#class-datasource) associated with this project, and unregisters it so [Project.get](#classmethod-projectget) no longer can find it by name. After destroying a project, it is an error to call any instance method on it.

---
## Method: Project.createScreen

### Description
Creates a screen from screen definitions cached in the [Project](#class-project).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name of screen to create |
| settings | [CreateScreenSettings](#type-createscreensettings)|[Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs, or a widget remap config |

### Returns

`[Canvas](#type-canvas)` — last top-level widget in the screen definition

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

---
## Method: Project.getScreenNames

### Description
Return the names of the screens cached in this project.

### Returns

`[Array of String](#type-array-of-string)` — names of cached screens

### See Also

- [Project.createScreen](#method-projectcreatescreen)

---
## Method: Project.getDataSourceNames

### Description
Return the names of the [DataSources](DataSource.md#class-datasource) cached in this project.

### Returns

`[Array of String](#type-array-of-string)` — names of cached DataSources

---
## Method: Project.getDataSource

### Description
Returns an instance of the requested [DataSource](DataSource.md#class-datasource) by creating it from the project's cache. If the ID is not globally bound, the framework will globally bind the instance before returning it.

Note that when a screen cached in the project is created, all project DataSources in the screen will be automatically instantiated from the project cache, so this method need not be called before creating a screen just to ensure its DataSources are available.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [Identifier](../main.md#type-identifier) | false | — | ID of the DataSource to create |

### Returns

`[DataSource](#type-datasource)` — requested DataSource instance

---
## Method: Project.createStartScreen

### Description
Creates screen from first definition cached in the project.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [CreateScreenSettings](#type-createscreensettings)|[Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs, or a widget remap config |

### Returns

`[Canvas](#type-canvas)` — last top-level widget in the screen definition

### See Also

- [Project.createScreen](#method-projectcreatescreen)
- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

---
