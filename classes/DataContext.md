# DataContext Documentation

[← Back to API Index](../reference.md)

---

## Attr: DataContext.sharedCriteria

### Description
Cross-component filter [Criteria](../reference_2.md#type-criteria) applied to every subscribing [DataBoundComponent](../reference.md#interface-databoundcomponent) in this DataContext's scope - the "Shared Criteria" system described above. In this global form, matching is by [fieldName](Criterion.md#attr-criterionfieldname) against each component's DataSource fields.

Normally not written directly: call [Canvas.setDataContextCriteria](Canvas.md#method-canvassetdatacontextcriteria) on the dataContext's owner, which updates this key and re-fetches all affected components. That method also supports DataSource-scoped and per-contributor publishing (several independent sources AND-combining their criteria), whose bookkeeping is stored under this key alongside the global criteria - another reason to go through the setter rather than assigning criteria here. The current effective state is readable via [Canvas.getDataContextCriteria](Canvas.md#method-canvasgetdatacontextcriteria).

Seeding `sharedCriteria` (even as an empty object) when creating the dataContext declares that this scope participates in cross-component filtering.

### Groups

- dataContext

**Flags**: IRW

---
