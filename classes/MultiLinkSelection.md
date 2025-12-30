# MultiLinkSelection Documentation

[← Back to API Index](../reference.md)

---

## Class: MultiLinkSelection

### Description
Maintains a 'selected' subset of a [multi-link tree](Tree.md#attr-treemultilinktree). Multi-link trees cannot use the [regular selection manager](Selection.md#class-selection) because they allow multiple occurences of the same node; therefore, selection caching must be done in a way that allows duplicate nodes to be unambiguously identified. Because the base `Selection` class caches pointers to the selected nodes or records directly, it is fundamentally unable to do this. `MultiLinkSelection`, by contrast, caches [NodeLocator](../reference_2.md#object-nodelocator) objects.

Includes methods for programmatically selecting node occurences and checking which node occurences are selected, and also for selecting node occurences as a result of mouse events, including drag selection support. The selection object is used automatically to handle selection APIs on [TreeGrid](TreeGrid.md#class-treegrid) instances where the data model is multi-linked (see [ResultTree.linkDataSource](ResultTree.md#attr-resulttreelinkdatasource) and [Tree.linkData](Tree.md#attr-treelinkdata) for further details).

Note that selection and deselection are skipped for nodes that aren't enabled, or that are marked as non-selectable; the relevant properties are [ListGrid.recordEnabledProperty](ListGrid_1.md#attr-listgridrecordenabledproperty) and [ListGrid.recordCanSelectProperty](ListGrid_1.md#attr-listgridrecordcanselectproperty). The recommended approach to affect disabled objects via the Selection APIs is to temporarily enable them beforehand.

### See Also

- [ListGrid.selectionManager](ListGrid_1.md#attr-listgridselectionmanager)
- [DataBoundComponent.selectRange](DataBoundComponent.md#method-databoundcomponentselectrange)
- [DataBoundComponent.selectRecord](DataBoundComponent.md#method-databoundcomponentselectrecord)

---
## Method: MultiLinkSelection.getSelection

### Description
Returns the selected nodes in this grid as a list of [NodeLocator](../reference_2.md#object-nodelocator)s.

### Returns

`[Array of NodeLocator](#type-array-of-nodelocator)` — The list of selected node occurences in the grid

### Groups

- selection

---
## Method: MultiLinkSelection.select

### Description
Select a particular node occurence. Note if you do not pass a [NodeLocator](../reference_2.md#object-nodelocator), the recordNum parameter is required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | false | — | node to select, or a NodeLocator that identifies it |
| recordNum | [Integer](../reference_2.md#type-integer) | true | — | Optional index into the underlying Tree's openList (which will be the same as the record number in a [TreeGrid](TreeGrid.md#class-treegrid)) |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: MultiLinkSelection.deselect

### Description
Deselect a particular node occurence. Note if you do not pass a [NodeLocator](../reference_2.md#object-nodelocator), the recordNum parameter is required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | false | — | node to deselect, or a NodeLocator that identifies it |
| recordNum | [Integer](../reference_2.md#type-integer) | true | — | Optional index into the underlying Tree's openList (which will be the same as the record number in a [TreeGrid](TreeGrid.md#class-treegrid)) |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: MultiLinkSelection.getSelectedRecords

### Description
Returns the selected nodes in this grid as a direct array of records. Contrast this with [MultiLinkSelection.getSelection](#method-multilinkselectiongetselection), which returns a list of [NodeLocator](../reference_2.md#object-nodelocator)s. Note, because this is `MultiLinkSelection`, this method may return an array containing the same node multiple times, with no way of discerning which particular occurence(s) are selected. If you need an unambiguous list of selected node occurences, use `getSelection()`.

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — The list of selected nodes in the grid

### Groups

- selection

---
## Method: MultiLinkSelection.selectSingle

### Description
Select a single node occurence and deselect everything else. Note if you do not pass a [NodeLocator](../reference_2.md#object-nodelocator), the recordNum parameter is required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | false | — | node to select, or a NodeLocator that identifies it |
| recordNum | [Integer](../reference_2.md#type-integer) | true | — | Optional index into the underlying Tree's openList (which will be the same as the record number in a [TreeGrid](TreeGrid.md#class-treegrid)) |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
