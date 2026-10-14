# DSLoadSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: DSLoadSettings.forceReload

### Description
Forcibly reload a dataSource if it's already loaded.

**Flags**: IRW

---
## Attr: DSLoadSettings.mockMode

### Description
Place loaded DataSource into [mockMode](DataSource_1.md#attr-datasourcemockmode)

**Flags**: IRW

---
## Attr: DSLoadSettings.allowMissing

### Description
Treat a requested DataSource that does not exist on the server as an ordinary outcome rather than an error: it is skipped without any error on the client or the server, the callback fires as usual, and [DataSource.get](DataSource.md#classmethod-datasourceget) returns null for it. Use this when a DataSource is legitimately present in some deployments and absent in others, for example one belonging to an optional server feature, and the page should check for it and adapt.

Only a DataSource that is not defined at all is treated this way. One that is defined but cannot be loaded, or a missing parent loaded through [DSLoadSettings.loadParents](#attr-dsloadsettingsloadparents), is still reported as an error.

**Flags**: IRW

---
## Attr: DSLoadSettings.loadParents

### Description
Load parent DataSources automatically for DataSources that have an [inheritsFrom](DataSource_1.md#attr-datasourceinheritsfrom) defined. Otherwise a DataSource with inheritsFrom will be broken if the parent DataSource is not already loaded.

**Flags**: IRW

---
