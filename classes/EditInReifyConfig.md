# EditInReifyConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: EditInReifyConfig.screenContents

### Description
Raw screen XML content, as an alternative to providing an [EditInReifyConfig.editContext](#attr-editinreifyconfigeditcontext).

**Flags**: IR

---
## Attr: EditInReifyConfig.projectName

### Description
Project to add the screen to. If the project does not exist, it is created. If omitted, a new project is created with an auto-assigned name.

**Flags**: IR

---
## Attr: EditInReifyConfig.screenName

### Description
Name for the screen in Reify storage. Required.

**Flags**: IR

---
## Attr: EditInReifyConfig.mode

### Description
How to load Reify — passed through to [ReifyLoadConfig.mode](ReifyLoadConfig.md#attr-reifyloadconfigmode).

**Flags**: IR

---
## Attr: EditInReifyConfig.editContext

### Description
The EditContext whose component tree should be saved to Reify. Mutually exclusive with [EditInReifyConfig.screenContents](#attr-editinreifyconfigscreencontents).

**Flags**: IR

---
## Attr: EditInReifyConfig.target

### Description
For inline mode — passed through to [ReifyLoadConfig.target](ReifyLoadConfig.md#attr-reifyloadconfigtarget).

**Flags**: IR

---
