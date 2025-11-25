# SystemDoneConfig Documentation

[← Back to API Index](../main.md)

---

## Attr: SystemDoneConfig.includeReflows

### Description
Should the system wait for all [Layouts](Layout.md#class-layout) to complete pending [reflows](Layout.md#method-layoutreflownow) before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
## Attr: SystemDoneConfig.includeNetworkOperations

### Description
Should the system wait for any outstanding [RPC Requests](RPCManager.md#class-rpcmanager) to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

If not explicitly set, [AutoTest.implicitNetworkWait](AutoTest.md#classattr-autotestimplicitnetworkwait) will be consulted

**Flags**: IR

---
## Attr: SystemDoneConfig.includeRedraws

### Description
Should the system wait for any outstanding redraws to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
## Attr: SystemDoneConfig.includeFileLoader

### Description
Should the system wait for any outstanding [FileLoader](#classmethod-fileloaderloadfiles) requests? to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
## Attr: SystemDoneConfig.includeTimers

### Description
Should the system wait for all outstanding registered [timer actions](Timer.md#classmethod-timersettimeout) to complete before [AutoTest.isSystemDone](AutoTest.md#classmethod-autotestissystemdone) returns true?

**Flags**: IR

---
