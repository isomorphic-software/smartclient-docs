# CreateScreenSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: CreateScreenSettings.componentSubstitutions

### Description
Defines the map of new widget [ids](Class.md#method-classgetid) to existing class instances, or to new instances that will be of a different class. A substituted class instance is returned immediately from [Class.create](Class.md#classmethod-classcreate) without modification. Otherwise, the constructor for the new instance is run, but targeting the substituted class rather than the original.

Note that where we return an existing instance, not even its [Canvas.ID](Canvas.md#attr-canvasid) will be changed. An alternative is programmtic replacement using [Layout.replaceMember](Layout.md#method-layoutreplacemember).

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

**Flags**: IR

---
## Attr: CreateScreenSettings.classSubstitutions

### Description
Maps class names of widgets in the screen to new class names, so that if a widget would normally be constructed as an instance of a class, and that class is in the map, it's instead constructed as an instance of the new class.

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

**Flags**: IR

---
