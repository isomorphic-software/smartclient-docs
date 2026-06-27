# PublishScreenConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: PublishScreenConfig.screenXml

### Description
Raw screen XML to publish. Mutually exclusive with [PublishScreenConfig.editContext](#attr-publishscreenconfigeditcontext). Must already have a DataView root.

**Flags**: IR

---
## Attr: PublishScreenConfig.projectName

### Description
Name of the Reify project the screen is added to. Created if it does not exist.

**Flags**: IR

---
## Attr: PublishScreenConfig.skin

### Description
Skin name baked into the published URL.

**Flags**: IR

---
## Attr: PublishScreenConfig.screenName

### Description
Name for the screen in Reify storage. If omitted, a timestamp-suffixed name is generated automatically (`Screen_YYYYMMDD_HHMMSS`).

**Flags**: IR

---
## Attr: PublishScreenConfig.dataSources

### Description
DataSource IDs to register in the project's ``<datasources>`` section via [Reify.addDataSourcesToProject](Reify.md#classmethod-reifyadddatasourcestoproject). The DS definitions must already exist in `vbDataSources` storage.

**Flags**: IR

---
## Attr: PublishScreenConfig.editContext

### Description
The EditContext whose contents should be published. Mutually exclusive with [PublishScreenConfig.screenXml](#attr-publishscreenconfigscreenxml). The EditContext is serialized and wrapped in a DataView root via [Reify._ensureDataViewRoot](#classmethod-reify_ensuredataviewroot) automatically.

**Flags**: IR

---
