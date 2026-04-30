# MockDSExportSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: MockDSExportSettings.includeCustomSimpleTypes

### Description
Whether to include custom-defined [SimpleTypes](SimpleType.md#class-simpletype).

**Flags**: IR

---
## Attr: MockDSExportSettings.localFKsOnly

### Description
When true, foreign-key declarations whose target [DataSource](DataSource_1.md#class-datasource) is not in the set of DataSources being exported are automatically stripped from the output. This prevents the exported file from containing dangling FK references to DataSources that do not exist at runtime, which would cause inner-join filtering to silently drop records and generate console warnings.

This is a convenient alternative to manually enumerating many [MockDSExportSettings.omitRelations](#attr-mockdsexportsettingsomitrelations) entries when the export set is a small subset of a large interconnected schema.

### See Also

- [MockDSExportSettings.omitRelations](#attr-mockdsexportsettingsomitrelations)
- [MockDSExportSettings.includeFKs](#attr-mockdsexportsettingsincludefks)

**Flags**: IR

---
## Attr: MockDSExportSettings.requestProperties

### Description
The properties that will be specified on the [DSRequest](../reference_2.md#object-dsrequest) when fetching records. You can pass an array of different request properties matching the length of the `dsNames` param of [Reify.getMockDS](Reify.md#classmethod-reifygetmockds) or [Reify.showMockDS](Reify.md#classmethod-reifyshowmockds) if you want the fetch for each [DataSource](DataSource_1.md#class-datasource) made with different properties.

**Flags**: IR

---
## Attr: MockDSExportSettings.numLevels

### Description
The number of levels of nodes to include, for DataSources that define a [tree relationship](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) between fields by declaring a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) on one field that refers to another from that same DataSource.

### See Also

- [MockDSExportSettings.rootCriteriaOnly](#attr-mockdsexportsettingsrootcriteriaonly)

**Flags**: IR

---
## Attr: MockDSExportSettings.includeImageFields

### Description
Should [image fields](../reference_2.md#type-fieldtype) be included in the export or serialization of the [DataSource](DataSource_1.md#class-datasource)? They are excluded by default since the stored paths are unlikely to be correct when placed in any other environment, such as Reify.

**Flags**: IR

---
## Attr: MockDSExportSettings.criteria

### Description
The [criteria](../reference_2.md#type-criteria) used to fetch the records returned as part of the export or serialization.

**Flags**: IR

---
## Attr: MockDSExportSettings.nonTreeDataSources

### Description
[IDs](DataSource_1.md#attr-datasourceid) of DataSources that should not be treated as [tree DataSources](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) despite having self-referential [foreign\\n keys](DataSourceField.md#attr-datasourcefieldforeignkey). Self-FKs on these DataSources are preserved in the exported schema but do not trigger the automatic multi-level tree fetching that normally occurs when a self-FK is detected.

Use this when a self-referential FK represents a data relationship rather than a parent-child hierarchy — for example, a sales order referencing the quotation it was created from, or an employee referencing the colleague who referred them. In these cases, tree fetching would issue an unbounded root-node query covering most of the table.

See also [MockDSExportSettings.maxTreeRoots](#attr-mockdsexportsettingsmaxtreeroots), which detects these cases automatically without requiring you to enumerate DataSources.

### See Also

- [MockDSExportSettings.maxTreeRoots](#attr-mockdsexportsettingsmaxtreeroots)

**Flags**: IR

---
## Attr: MockDSExportSettings.validatorMode

### Description
Controls which [validators](Validator.md#class-validator), if any, to include in the fields of the exported [MockDataSource](MockDataSource.md#class-mockdatasource). Since MockDataSources are client-only, server-only validators are not exported. Auto-generated validators are also not exported, since they will be recreated based on the type of the field during the import process.

**Flags**: IR

---
## Attr: MockDSExportSettings.hideEmptyFields

### Description
When true, fields whose values are `null` or `undefined` in every fetched record are automatically marked [detail](DataSourceField.md#attr-datasourcefielddetail):`true` in the exported [MockDataSource](MockDataSource.md#class-mockdatasource). This keeps structurally important fields (primary keys and foreign keys) visible regardless of data content, while demoting columns that carry no data so they don't clutter default views.

See also [MockDSExportSettings.dropEmptyFields](#attr-mockdsexportsettingsdropemptyfields) to fully remove empty fields from the exported schema and record data.

### See Also

- [MockDSExportSettings.dropEmptyFields](#attr-mockdsexportsettingsdropemptyfields)

**Flags**: IR

---
## Attr: MockDSExportSettings.sequentialFetching

### Description
When `true`, fetches records from each [DataSource](DataSource_1.md#class-datasource) one at a time rather than batching all independent fetches into a single queued request. This is recommended when exporting from large production databases where concurrent queries can exhaust connection pools. See the [Large Database Export](#kb-topic-largedatabaseexport) overview for guidance.

### See Also

- [MockDSExportSettings.nonTreeDataSources](#attr-mockdsexportsettingsnontreedatasources)
- [MockDSExportSettings.maxTreeRoots](#attr-mockdsexportsettingsmaxtreeroots)

**Flags**: IR

---
## Attr: MockDSExportSettings.perDSCriteria

### Description
An object mapping [DataSource IDs](DataSource_1.md#attr-datasourceid) to [Criteria](../reference_2.md#type-criteria) that should be applied when fetching records for that DataSource. The criteria are combined with any global [Criteria](../reference_2.md#type-criteria) and any relation-derived criteria using [DataSource.combineCriteria](DataSource.md#classmethod-datasourcecombinecriteria).

For tree DataSources, per-DS criteria are applied to **every** level of the tree fetch. To restrict only which roots are fetched while allowing unrestricted child expansion, use [MockDSExportSettings.treeRoots](#attr-mockdsexportsettingstreeroots) instead.

### See Also

- [Criteria](../reference_2.md#type-criteria)
- [MockDSExportSettings.treeRoots](#attr-mockdsexportsettingstreeroots)

**Flags**: IR

---
## Attr: MockDSExportSettings.format

### Description
Determines the format emitted by [Reify.getMockDS](Reify.md#classmethod-reifygetmockds).

**Flags**: IR

---
## Attr: MockDSExportSettings.rootCriteriaOnly

### Description
For DataSources that define a [tree relationship](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) between fields by declaring a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) on one field that refers to another from that same DataSource, should [MockDSExportSettings.criteria](#attr-mockdsexportsettingscriteria) be applied only to the root node? If false, the criteria will be applied to all nodes.

### See Also

- [MockDSExportSettings.numLevels](#attr-mockdsexportsettingsnumlevels)

**Flags**: IR

---
## Attr: MockDSExportSettings.includeFrom

### Description
Should [DataSourceField.includeFrom](DataSourceField.md#attr-datasourcefieldincludefrom) declarations be preserved in the exported [MockDataSource](MockDataSource.md#class-mockdatasource)? When `true`, the export reconstructs `includeFrom` paths from the server-resolved field metadata so the clientOnly DataSource can resolve cross-DS field lookups at runtime.

### See Also

- [MockDSExportSettings.includeFKs](#attr-mockdsexportsettingsincludefks)

**Flags**: IR

---
## Attr: MockDSExportSettings.omitRelations

### Description
[Foreign key](DataSourceField.md#attr-datasourcefieldforeignkey) relationships to exclude from the dependency graph that determines fetch order and relation criteria. Omitted FKs do not generate dependency-chain fetch criteria, but FK declarations are still preserved in the exported schema so that [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) and [DataSourceField.displayField](DataSourceField.md#attr-datasourcefielddisplayfield) can resolve display values at runtime from the related [MockDataSource](MockDataSource.md#class-mockdatasource)'s [cacheData](DataSource_1.md#attr-datasourcecachedata). To fully strip FK declarations for DataSources not in the export set, use [MockDSExportSettings.localFKsOnly](#attr-mockdsexportsettingslocalfksonly) instead.

Entries can use either of two formats:

*   **targetDS.targetField** – omits _every_ FK that references that target, from any DataSource. Use this for lookup/reference tables whose broad criteria would dilute the dependency chain.
*   **sourceDS.sourceField** – omits only the named field's FK on the named DataSource, leaving other DataSources' references to the same target intact. Use this to break circular FK dependencies.

### See Also

- [MockDSExportSettings.includeFKs](#attr-mockdsexportsettingsincludefks)

**Flags**: IR

---
## Attr: MockDSExportSettings.numRows

### Description
The number of rows of data to include, if more meet the [MockDSExportSettings.criteria](#attr-mockdsexportsettingscriteria).

**Flags**: IR

---
## Attr: MockDSExportSettings.treeRoots

### Description
An object mapping [DataSource IDs](DataSource_1.md#attr-datasourceid) to arrays of primary key values identifying the specific root nodes to include for tree DataSources. Unlike [MockDSExportSettings.perDSCriteria](#attr-mockdsexportsettingsperdscriteria), which filters every level of the tree, `treeRoots` restricts only the initial root-level fetch — child nodes under the specified roots are fetched without the root restriction.

This is useful when you want a complete subtree under specific known roots. For example, to export only the "Electronics" and "Clothing" product category trees:

```
   treeRoots: { productCategory: ["electronics", "clothing"] }
 
```

### See Also

- [MockDSExportSettings.perDSCriteria](#attr-mockdsexportsettingsperdscriteria)
- [MockDSExportSettings.numLevels](#attr-mockdsexportsettingsnumlevels)

**Flags**: IR

---
## Attr: MockDSExportSettings.followFKDepth

### Description
When non-zero, automatically discovers [DataSources](DataSource_1.md#class-datasource) reachable from the explicitly requested DataSources via [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) relationships, up to this many hops. A value of 1 adds DataSources directly referenced by a foreignKey on any requested DataSource; a value of 2 additionally adds DataSources referenced by those, and so on.

This is useful when exporting a set of interlinked DataSources and you want to automatically include all related DataSources without enumerating them manually. The traversal walks both directions: from a field's `foreignKey` to the target DataSource, and from a target DataSource back to any DataSource that references it. Self-referential (tree) FKs are not counted as a hop.

**Flags**: IR

---
## Attr: MockDSExportSettings.includeFKs

### Description
Should [foreign key](DataSourceField.md#attr-datasourcefieldforeignkey) relationships be included in the export or serialization of the [DataSource](DataSource_1.md#class-datasource)?

**Flags**: IR

---
## Attr: MockDSExportSettings.dropEmptyFields

### Description
When true, fields whose values are `null` or `undefined` in every fetched record are completely omitted from the exported [MockDataSource](MockDataSource.md#class-mockdatasource) — both the field declaration and the corresponding record property are dropped. This produces a compact schema containing only fields that carry actual data, which is ideal for reporting demos and other contexts where schema noise should be minimized.

Primary-key and foreign-key fields are always retained regardless of data content, since they are structurally required.

This setting is stronger than [MockDSExportSettings.hideEmptyFields](#attr-mockdsexportsettingshideemptyfields): when both are true, `dropEmptyFields` takes precedence and empty fields are removed rather than merely demoted to `detail:true`.

### See Also

- [MockDSExportSettings.hideEmptyFields](#attr-mockdsexportsettingshideemptyfields)

**Flags**: IR

---
## Attr: MockDSExportSettings.maxTreeRoots

### Description
When a self-referential [foreign\\n key](DataSourceField.md#attr-datasourcefieldforeignkey) is detected, an exploratory fetch counts the root nodes before committing to tree-style multi-level fetching. If there are more root nodes than `maxTreeRoots`, the DataSource is exported as a flat table with the standard [MockDSExportSettings.numRows](#attr-mockdsexportsettingsnumrows) limit instead.

This prevents unbounded queries on DataSources where a self-FK is not a true tree hierarchy. Common cases include an orders table where most orders are roots (not created from a quotation), or an employees table where a "referred by" self-FK yields thousands of unlinked root nodes.

Set to `null` to disable the exploratory check entirely.

### See Also

- [MockDSExportSettings.nonTreeDataSources](#attr-mockdsexportsettingsnontreedatasources)
- [MockDSExportSettings.numLevels](#attr-mockdsexportsettingsnumlevels)

**Flags**: IR

---
