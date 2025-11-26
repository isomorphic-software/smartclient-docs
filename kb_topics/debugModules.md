# Using the Debug Modules

[← Back to API Index](../reference.md)

---

## KB Topic: Using the Debug Modules

### Description
SmartClient comes with a debug / readable version of the SmartClient JS files that may be useful during development.

**Note: These are useful only if you are interested in step-through debugging of framework JavaScript code using a JavaScript debugger, and we strongly discourage this as a primary approach to debugging: the SmartClient framework code provides many, many advanced features and is extremely sophisticated as a result. Learning the internals of large parts of SmartClient is unnecessary and ineffective as a debugging approach, and the other approaches discussed in [debugging](debugging.md#kb-topic-debugging) should be your primary approaches to troubleshooting.**

To use the debug modules, simply change each `<script>` tag's SRC to the URI of the debug version of the module. For example:

```
<script src="/isomorphic/system/modules/ISC_Core.js"></script>
```
should be changed to:
```
<script src="/isomorphic/system/modules-debug/ISC_Core.js"></script>
```

Alternatively, the <isomorphic:loadISC> and <isomorphic:loadModules> tags support a `useDebugModules` attribute:

```
<isomorphic:loadISC skin="Enterprise" useDebugModules="true"/>
```

Note that the debug modules are intended to help in debugging your own application, and not the SmartClient Feature Explorer. The Feature Explorer is not present in modules-debug, and the non-debug version requires the other non-debug files.

### See Also

- [debugging](debugging.md#kb-topic-debugging)

---
