# ReifyRemote Documentation

[← Back to API Index](../reference.md)

---

## Class: ReifyRemote

### Description
A handle returned by [Reify.loadReify](Reify.md#classmethod-reifyloadreify) that provides a uniform API for controlling and receiving notifications from a Reify editor instance, whether inline or in a separate window.

Use [subscribe](#method-subscribe) to listen for events and the various command methods to control Reify.

---
## Attr: ReifyRemote.mode

### Description
How the Reify instance was loaded: "inline", "window". Set automatically by [Reify.loadReify](Reify.md#classmethod-reifyloadreify).

**Flags**: IR

---
## Method: ReifyRemote.loadScreen

### Description
Tell the Reify instance to load a specific screen within the current project.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | screen to load |

---
## Method: ReifyRemote.close

### Description
Close the Reify instance. For inline mode, destroys the Reify Canvas. For window mode, closes the browser window.

---
## Method: ReifyRemote.loadDataSource

### Description
Tell the Reify instance to focus on a specific DataSource within the current project.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID to focus on |

---
## Method: ReifyRemote.subscribe

### Description
Register a handler for events from the Reify instance.

Available event types include all existing Reify PubSub messages (prefixed with "reify\_") plus the new cross-window messages:

*   `reify_projectLoaded` — a project was loaded
*   `reify_projectSaved` — a project was saved
*   `reify_projectRenamed` — project was renamed
*   `reify_screenLoaded` — a screen was loaded
*   `reify_screenSaved` — a screen was saved
*   `reify_screenRenamed` — a screen was renamed
*   `reify_screenChanged` — current screen was edited
*   `reify_skinChanged` — skin was changed
*   `reify_dataSourceAdded` — a DS was added to the project
*   `reify_dataSourceRemoved` — a DS was removed
*   `reify_availableScreensChanged` — the set of screens changed
*   `reify_availableComponentsChanged` — the set of components changed
*   `reify_ready` — Reify has finished loading
*   `reify_closed` — Reify was closed

Pass `null` as the type to receive all events.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [String](#type-string) | false | — | event type, or null for all events |
| callback | [Function](#type-function) | false | — | handler: function(type, payload) |

---
## Method: ReifyRemote.isOpen

### Description
Whether the Reify instance is still open / alive.

### Returns

`[Boolean](#type-boolean)` — —

---
## Method: ReifyRemote.destroy

### Description
Clean up the ReifyRemote, removing all listeners.

---
## Method: ReifyRemote.loadProject

### Description
Tell the Reify instance to load a project by name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | project to load |

---
