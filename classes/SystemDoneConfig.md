# SystemDoneConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: SystemDoneConfig.includeNetworkOperations

### Description
Should the system wait for any outstanding [RPC Requests](RPCManager.md#class-rpcmanager) to complete before [isSystemDone](#method-issystemdone) returns true?

If not explicitly set, [AutoTest.implicitNetworkWait](AutoTest.md#classattr-autotestimplicitnetworkwait) will be consulted

**Flags**: IR

---
## Attr: SystemDoneConfig.includeRedraws

### Description
Should the system wait for any outstanding redraws to complete before [isSystemDone](#method-issystemdone) returns true?

**Flags**: IR

---
## Attr: SystemDoneConfig.includeFileLoader

### Description
Should the system wait for any outstanding [FileLoader](#classmethod-fileloaderloadfiles) requests? to complete before [isSystemDone](#method-issystemdone) returns true?

**Flags**: IR

---
## Attr: SystemDoneConfig.includeTimers

### Description
Should the system wait for all outstanding registered [timer actions](Timer.md#classmethod-timersettimeout) to complete before [isSystemDone](#method-issystemdone) returns true?

**Flags**: IR

---
