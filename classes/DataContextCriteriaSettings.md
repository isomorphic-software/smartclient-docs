# DataContextCriteriaSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: DataContextCriteriaSettings.beforeCriteria

### Description
Criteria on the records, applied by each component the contribution applies to as [DSRequest.beforeCriteria](DSRequest.md#attr-dsrequestbeforecriteria). See [Canvas.setDataContextCriteria](Canvas_1.md#method-canvassetdatacontextcriteria).

**Flags**: IR

---
## Attr: DataContextCriteriaSettings.contributorID

### Description
Unique identifier for the criteria source. When multiple independent components (such as [Slicers](Slicer.md#class-slicer)) each publish criteria for the same DataSource, pass a distinct `contributorID` per source; all contributors' criteria are AND-combined automatically. Without one, each call to [Canvas.setDataContextCriteria](Canvas_1.md#method-canvassetdatacontextcriteria) replaces the previous anonymous contribution for the same DataSources. Applies only to contributions that name a [dataSource](#attr-datacontextcriteriasettingsdatasource); with none, criteria go to the single global slot and the `contributorID` is ignored.

**Flags**: IR

---
## Attr: DataContextCriteriaSettings.criteria

### Description
Ordinary criteria, combined into the criteria of each component the contribution applies to. See [Canvas.setDataContextCriteria](Canvas_1.md#method-canvassetdatacontextcriteria) for how they differ from [beforeCriteria](#attr-datacontextcriteriasettingsbeforecriteria) and [afterCriteria](#attr-datacontextcriteriasettingsaftercriteria).

**Flags**: IR

---
## Attr: DataContextCriteriaSettings.afterCriteria

### Description
Criteria on totals, applied as [DSRequest.afterCriteria](DSRequest.md#attr-dsrequestaftercriteria) by each component the contribution applies to whose request can interpret them. See [Canvas.setDataContextCriteria](Canvas_1.md#method-canvassetdatacontextcriteria).

**Flags**: IR

---
## Attr: DataContextCriteriaSettings.dataSource

### Description
ID of the DataSource the contribution applies to, or an Array of IDs. When omitted, the contribution's [criteria](#attr-datacontextcriteriasettingscriteria) apply to every DataSource by field-name match - see [Canvas.setDataContextCriteria](Canvas_1.md#method-canvassetdatacontextcriteria).

**Flags**: IR

---
## Attr: DataContextCriteriaSettings.filterRelated

### Description
When true, components bound to DataSources that have a [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) relationship to the target DataSource are also filtered, via a `valueQuery` sub-criterion on their foreign-key column: the contribution's [criteria](#attr-datacontextcriteriasettingscriteria) and [beforeCriteria](#attr-datacontextcriteriasettingsbeforecriteria) become criteria of the same kind there. Its [afterCriteria](#attr-datacontextcriteriasettingsaftercriteria) test totals of the target DataSource's fields, which a related component does not produce, so they do not cascade. Only supported when [dataSource](#attr-datacontextcriteriasettingsdatasource) names a single DataSource.

**Flags**: IR

---
