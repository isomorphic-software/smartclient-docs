# ReifyLoadConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: ReifyLoadConfig.dataSource

### Description
ID of a DataSource to open when Reify loads.

**Flags**: IR

---
## Attr: ReifyLoadConfig.project

### Description
Name of a project to open when Reify loads.

**Flags**: IR

---
## Attr: ReifyLoadConfig.target

### Description
For `mode:"inline"`, a [Layout](Layout.md#class-layout) to add the Reify instance to as a member. If not specified, the Reify instance is created but not added to the page — call [Canvas.draw](Canvas.md#method-canvasdraw) or add it to a layout manually.

**Flags**: IR

---
## Attr: ReifyLoadConfig.reifyProperties

### Description
For `mode:"inline"`, additional properties to apply to the [Reify](Reify.md#class-reify) instance when it is created.

**Flags**: IR

---
## Attr: ReifyLoadConfig.mode

### Description
How to load the Reify editor: `"inline"` loads Reify as a [Canvas](Canvas.md#class-canvas) in the current page; `"window"` opens Reify in a new browser tab.

**Flags**: IR

---
## Attr: ReifyLoadConfig.screen

### Description
Name of a screen to open when Reify loads.

**Flags**: IR

---
## Attr: ReifyLoadConfig.rtmChannel

### Description
For `mode:"window"` with `useRTM:true`, the RTM channel name to use for communication. Defaults to a randomly generated session ID.

**Flags**: IR

---
## Attr: ReifyLoadConfig.windowFeatures

### Description
For `mode:"window"`, a window features string to pass to `window.open()`. See the MDN documentation for `Window.open()` for valid values.

**Flags**: IR

---
## Attr: ReifyLoadConfig.useRTM

### Description
For `mode:"window"`, whether to use [realtimeMessaging](#kb-topic-realtimemessaging) for communication between the host page and the Reify window. By default, `window.postMessage` is used, which requires same-origin. Set `useRTM:true` for cross-origin scenarios.

**Flags**: IR

---
