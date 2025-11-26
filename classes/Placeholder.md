# Placeholder Documentation

[← Back to API Index](../reference.md)

---

## Class: Placeholder

*Inherits from:* [Label](Label.md#class-label)

### Description
A Placeholder is used in place of component while [editing](../kb_topics/devTools.md#kb-topic-dashboards--tools-framework-overview) when an instance of the actual component cannot be created or when required properties are not yet provided that allow correct creation. See the _Designing Components for Editing & Using Placeholder_ section of [Reify](../kb_topics/reify.md#kb-topic-reify-overview) for details.

Placeholder is a special class in that the properties that are directly assigned to the instance are not used by the placeholder. These are assumed to apply to the actual component for which the placeholder is replacing. Properties that control the placeholder itself are in [placeholderDefaults](#attr-placeholderplaceholderdefaults).

On creation a Placeholder will automatically replace itself with the target component ([PlaceholderDefaults.placeholderFor](../reference.md#attr-placeholderdefaultsplaceholderfor)) when created from [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen) unless the project was loaded with [LoadProjectSettings.allowPlaceholders](LoadProjectSettings.md#attr-loadprojectsettingsallowplaceholders) is `true`.

Note that `Placeholder` has a lowercase H because it is a single word in English.

### Groups

- devTools

---
## Attr: Placeholder.placeholderDefaults

### Description
Defaults applied to the placeholder instance when not replaced by the target component.

**Flags**: IR

---
