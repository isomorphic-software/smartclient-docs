# Batch Widget Creation

[← Back to API Index](../reference.md)

---

## KB Topic: Batch Widget Creation

### Description
When many widgets are created at once before any of them draw (such as during [RPCManager.createScreen](../classes/RPCManager.md#classmethod-rpcmanagercreatescreen) or [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen)), certain initialization work can be deferred to draw time for a significant speedup. This includes visual decorations (edges, shadows, back masks), layout margin computation, icon setup, validator scanning, rule evaluation, and topElement propagation.

[Canvas.startBatchCreation](../classes/Canvas.md#classmethod-canvasstartbatchcreation) enables this mode, and [Canvas.endBatchCreation](../classes/Canvas.md#classmethod-canvasendbatchcreation) disables it. A thread-exit action (TEA) is automatically registered as a safety net to ensure the mode is always disabled at the end of the current JavaScript thread, even if `endBatchCreation()` is not called explicitly.

This mode is used automatically by `createScreen()` and `loadScreen()`. It can also be used by application code that creates many widgets programmatically before drawing any of them.

See also [Class.assumeGoodCode](../classes/Class.md#attr-classassumegoodcode), which separately skips input-validation checks.

### Related

- [Canvas.startBatchCreation](../classes/Canvas.md#classmethod-canvasstartbatchcreation)
- [Canvas.endBatchCreation](../classes/Canvas.md#classmethod-canvasendbatchcreation)

---
