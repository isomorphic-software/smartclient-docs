# SystemWaitConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: SystemWaitConfig.includeFileLoader

### Description
Should the system wait for any outstanding [FileLoader](#classmethod-fileloaderloadfiles) requests? to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

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
