# GridSelectRecordsTask Documentation

[← Back to API Index](../reference.md)

---

## Class: GridSelectRecordsTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Select or deselect one or more records as specified by criteria. Target records will also be scrolled into view or, for a tree, parent folders will be opened to reveal the node.

Task Output:

*   On a select, the set of newly selected records is the output, even if other records are also selected.
*   On a deselect, the entire set of de-selected records is the output.

---
## Attr: GridSelectRecordsTask.criteria

### Description
Criteria defining the records that should be selected or deselected. All records are selected or deselected if not specified.

To target a single record just specify criteria for its primary key.

**Flags**: IR

---
## Attr: GridSelectRecordsTask.scrollIntoView

### Description
Set to `false` to prevent the first affected record from being scrolled into view.

**Flags**: IR

---
## Attr: GridSelectRecordsTask.select

### Description
Set to `false` to clear selection.

**Flags**: IR

---
## Attr: GridSelectRecordsTask.selectMultiple

### Description
Should multiple records matching [Criteria](../reference_2.md#type-criteria) be affected? If set to `false` only the first matching record is affected.

**Flags**: IR

---
## Attr: GridSelectRecordsTask.keepExistingSelection

### Description
For grids that allow multiple selection, should any existing selection be retained? Only applies when selecting records.

**Flags**: IR

---
