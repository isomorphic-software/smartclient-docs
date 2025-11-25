# MockDSExportSettings Documentation

[← Back to API Index](../main.md)

---

## Attr: MockDSExportSettings.includeCustomSimpleTypes

### Description
Whether to include custom-defined [SimpleTypes](SimpleType.md#class-simpletype).

**Flags**: IR

---
## Attr: MockDSExportSettings.requestProperties

### Description
The properties that will be specified on the [DSRequest](../main_2.md#object-dsrequest) when fetching records. You can pass an array of different request properties matching the length of the `dsNames` param of [Reify.getMockDS](Reify.md#classmethod-reifygetmockds) or [Reify.showMockDS](Reify.md#classmethod-reifyshowmockds) if you want the fetch for each [DataSource](DataSource.md#class-datasource) made with different properties.

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
Should [image fields](../main_2.md#type-fieldtype) be included in the export or serialization of the [DataSource](DataSource.md#class-datasource)? They are excluded by default since the stored paths are unlikely to be correct when placed in any other environment, such as Reify.

**Flags**: IR

---
## Attr: MockDSExportSettings.criteria

### Description
The [criteria](../main_2.md#type-criteria) used to fetch the records returned as part of the export or serialization.

**Flags**: IR

---
## Attr: MockDSExportSettings.validatorMode

### Description
Controls which [validators](Validator.md#class-validator), if any, to include in the fields of the exported [MockDataSource](MockDataSource.md#class-mockdatasource). Since MockDataSources are client-only, server-only validators are not exported. Auto-generated validators are also not exported, since they will be recreated based on the type of the field during the import process.

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
## Attr: MockDSExportSettings.omitRelations

### Description
If including [foreign key](DataSourceField.md#attr-datasourcefieldforeignkey) relationships, those relationships to skip. This can be used to avoid dangling references to [DataSources](DataSource.md#class-datasource) that are not being exported or serialized.

### See Also

- [MockDSExportSettings.includeFKs](#attr-mockdsexportsettingsincludefks)

**Flags**: IR

---
## Attr: MockDSExportSettings.numRows

### Description
The number of rows of data to include, if more meet the [MockDSExportSettings.criteria](#attr-mockdsexportsettingscriteria).

**Flags**: IR

---
## Attr: MockDSExportSettings.includeFKs

### Description
Should [foreign key](DataSourceField.md#attr-datasourcefieldforeignkey) relationships be included in the export or serialization of the [DataSource](DataSource.md#class-datasource)?

**Flags**: IR

---
