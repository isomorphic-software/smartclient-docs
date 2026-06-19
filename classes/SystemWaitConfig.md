# SystemWaitConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: SystemWaitConfig.includeFileLoader

### Description
Should the system wait for any outstanding [FileLoader](FileLoader.md#classmethod-fileloaderload) requests to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
## Attr: SystemWaitConfig.timeout

### Description
Timeout for [AutoTest.waitForElement](AutoTest.md#classmethod-autotestwaitforelement) in ms.

If unset a default timeout of 30 seconds will be used.

**Flags**: IR

---
## Attr: SystemWaitConfig.includeNetworkOperations

### Description
Should the system wait for any outstanding [RPC Requests](RPCManager.md#class-rpcmanager) to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

If not explicitly set, [AutoTest.implicitNetworkWait](AutoTest.md#classattr-autotestimplicitnetworkwait) will be consulted

**Flags**: IR

---
## Attr: SystemWaitConfig.includeRedraws

### Description
Should the system wait for any outstanding redraws to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
## Attr: SystemWaitConfig.includeTimers

### Description
Should the system wait for all outstanding registered [timer actions](Timer.md#classmethod-timersettimeout) to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
## Attr: SystemWaitConfig.includeFieldRebuild

### Description
Should the system wait for any pending field-rebuild work to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

When `true`, [AutoTest.isGridDone](AutoTest.md#classmethod-autotestisgriddone) is checked for all [ListGrids](ListGrid_1.md#class-listgrid) — including grids that have not yet been drawn — to detect pending asynchronous field generation (e.g. formula or summary field computation). For already-drawn grids this check happens automatically; the flag extends it to not-yet-drawn grids, and also makes the intent explicit in tests that modify field state via actions such as `addFormulaField` or `restoreState`.

**Flags**: IR

---
## Attr: SystemWaitConfig.includeReflows

### Description
Should the system wait for all [Layouts](Layout.md#class-layout) to complete pending [reflows](Layout.md#method-layoutreflownow) before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
