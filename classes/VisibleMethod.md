# VisibleMethod Documentation

[← Back to API Index](../reference.md)

---

## Attr: VisibleMethod.language

### Description
The script language if method is implemented via [serverScript](../kb_topics/serverScript.md#kb-topic-server-scripting). If omitted the default system-wide language will be used, defined in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) by setting `script.defaultLanguage`.

**Flags**: IR

---
## Attr: VisibleMethod.scriptImport

### Description
Comma or space separated script imports if method is scripted. See the "Java Imports" section of the [serverScript](../kb_topics/serverScript.md#kb-topic-server-scripting) overview.

**Flags**: IR

---
## Attr: VisibleMethod.script

### Description
The script body if method is imlemented via [serverScript](../kb_topics/serverScript.md#kb-topic-server-scripting). The presense of this attribute actually defines that method is scripted. See examples in [Application declaration](../kb_topics/applicationDeclaration.md#kb-topic-application-declaration-files) overview.

**Flags**: IR

---
## Attr: VisibleMethod.name

### Description
The method name. In case if it refers the `ServerObject` method the names must match and it is the only property required. See examples in [Application declaration](../kb_topics/applicationDeclaration.md#kb-topic-application-declaration-files) overview.

**Flags**: IR

---
## Attr: VisibleMethod.args

### Description
For the methods implemented via [serverScript](../kb_topics/serverScript.md#kb-topic-server-scripting) defines the name of the arguments array variable to access parameters passed via [DMI.call](DMI.md#classmethod-dmicall) inside the script. See examples in [Application declaration](../kb_topics/applicationDeclaration.md#kb-topic-application-declaration-files) overview.

**Flags**: IR

---
