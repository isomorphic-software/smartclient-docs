# RemoteWindow Documentation

[← Back to API Index](../reference.md)

---

## Class: RemoteWindow

### Description
Provides APIs that manipulate a SmartClient browser window. Within the [OpenFin](https://developers.openfin.co/of-docs/docs) environment, the underlying implementation is actually via the [OpenFinWindow](../reference.md#class-openfinwindow) class.

### Groups

- experimental

### See Also

- [MultiWindow](MultiWindow.md#class-multiwindow)

---
## Method: RemoteWindow.isShowing

### Description
Checks whether this RemoteWindow is showing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowBooleanCallback](#type-remotewindowbooleancallback) | false | — | callback to receive output |

---
## Method: RemoteWindow.getInfo

### Description
Checks whether this RemoteWindow is showing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowMapCallback](#type-remotewindowmapcallback) | false | — | callback to receive output |

---
## Method: RemoteWindow.move

### Description
Moves this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [number](#type-number) | false | — | desired x-offset of left edge |
| y | [number](#type-number) | false | — | desired y-offset of top edge |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's moved |

---
## Method: RemoteWindow.resize

### Description
Resizes this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [number](#type-number) | false | — | desired new width |
| height | [number](#type-number) | false | — | desired new height |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's resized |

---
## Method: RemoteWindow.getName

### Description
Returns the name of this RemoteWindow.

### Returns

`[String](#type-string)` — window name

---
## Method: RemoteWindow.bringToFront

### Description
Brings this RemoteWindow to the front in window stacking order.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after raising window |
| errorCallback | [RemoteWindowErrorCallback](#type-remotewindowerrorcallback) | true | — | callback run if raising fails |

---
## Method: RemoteWindow.deactivate

### Description
Blurs (deactivates) this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's deactivated |

---
## Method: RemoteWindow.getWindow

### Description
Returns the browser `window` object associated with this RemoteWindow.

### Returns

`[Object](../reference.md#type-object)` — browser window

---
## Method: RemoteWindow.getParent

### Description
Returns the parent [RemoteWindow](#class-remotewindow) instance that opened this RemoteWindow.

### Returns

`[RemoteWindow](#type-remotewindow)` — instance wrapping the parent window or null

---
## Method: RemoteWindow.focus

### Description
Focuses (activates) this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's activated |

---
## Method: RemoteWindow.blur

### Description
Blurs (deactivates) this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's deactivated |

---
## Method: RemoteWindow.restore

### Description
Restores this RemoteWindow from being maximized or minimized.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after restoration |
| errorCallback | [RemoteWindowErrorCallback](#type-remotewindowerrorcallback) | true | — | callback run if restoring fails |

---
## Method: RemoteWindow.minimize

### Description
Minimizes this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after minimization |
| errorCallback | [RemoteWindowErrorCallback](#type-remotewindowerrorcallback) | true | — | callback run if minimizing fails |

---
## Method: RemoteWindow.show

### Description
Shows this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after showing the window |
| errorCallback | [RemoteWindowErrorCallback](#type-remotewindowerrorcallback) | true | — | callback run if showing fails |

---
## Method: RemoteWindow.maximize

### Description
Maximizes this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after maximization |
| errorCallback | [RemoteWindowErrorCallback](#type-remotewindowerrorcallback) | true | — | callback run if maximizing fails |

---
## Method: RemoteWindow.getContainerWindow

### Description
Returns the container window, if present, wrapping the browser window for this RemoteWindow. If OpenFin is present, this will return the associated OpenFin [Window](https://cdn.openfin.co/docs/javascript/stable/Window.html).

### Returns

`[Object](../reference.md#type-object)` — OpenFin window

---
## Method: RemoteWindow.activate

### Description
Focuses (activates) this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's activated |

---
## Method: RemoteWindow.hide

### Description
Hides this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after hiding the window |
| errorCallback | [RemoteWindowErrorCallback](#type-remotewindowerrorcallback) | true | — | callback run if hiding fails |

---
## Method: RemoteWindow.close

### Description
Closes this RemoteWindow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| force | [boolean](../reference.md#type-boolean) | true | — | whether to force it closed |
| callback | [RemoteWindowCallback](#type-remotewindowcallback) | true | — | callback run after it's closed |

---
