# Selection Documentation

[← Back to API Index](../reference.md)

---

## Class: Selection

### Description
Maintains a 'selected' subset of a List or Array of objects, such as records in a record set, or widgets in a selectable header.

Includes methods for selecting objects and checking which objects are selected, and also for selecting objects as a result of mouse events, including drag selection support. The selection object is used automatically to handle selection APIs on [ListGrid](ListGrid_1.md#class-listgrid) and [TreeGrid](TreeGrid.md#class-treegrid) instances.

Note that selection and deselection are skipped for objects that aren't enabled, or that are marked as non-selectable. For a [ListGrid](ListGrid_1.md#class-listgrid), the relevant properties are [ListGrid.recordEnabledProperty](ListGrid_1.md#attr-listgridrecordenabledproperty) and [ListGrid.recordCanSelectProperty](ListGrid_1.md#attr-listgridrecordcanselectproperty). The recommended approach to affect disabled objects via the Selection APIs is to temporarily enable them beforehand.

### See Also

- [ListGrid.selectionManager](ListGrid_1.md#attr-listgridselectionmanager)
- [DataBoundComponent.selectRange](DataBoundComponent.md#method-databoundcomponentselectrange)
- [DataBoundComponent.selectRecord](DataBoundComponent.md#method-databoundcomponentselectrecord)

---
## ClassAttr: Selection.NONE

### Description
A declared value of the enum type [SelectionStyle](../reference.md#type-selectionstyle).

**Flags**: R

---
## ClassAttr: Selection.MULTIPLE

### Description
A declared value of the enum type [SelectionStyle](../reference.md#type-selectionstyle).

**Flags**: R

---
## ClassAttr: Selection.SIMPLE

### Description
A declared value of the enum type [SelectionStyle](../reference.md#type-selectionstyle).

**Flags**: R

---
## ClassAttr: Selection.SINGLE

### Description
A declared value of the enum type [SelectionStyle](../reference.md#type-selectionstyle).

**Flags**: R

---
## Attr: Selection.selectionRangeNotLoadedMessage

### Description
Message to display to the user in a `warn` dialog if [Selection.selectRange](#method-selectionselectrange) is called for a selection on a ResultSet, where the range of records to be selected has not been loaded.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Method: Selection.deselectItem

### Description
Deselect a particular item by its position in the list

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| position | [number](#type-number) | false | — | index of the item to be selected |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.isSelected

### Description
Return true if a particular item is selected

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../reference.md#type-object) | false | — | object to check |

### Returns

`[boolean](../reference.md#type-boolean)` — true == object is selected, false == object is not selected

### Groups

- selection

---
## Method: Selection.isPartiallySelected

### Description
When using tree-oriented selection modes like [TreeGrid.cascadeSelection](TreeGrid.md#attr-treegridcascadeselection), returns true if the record is considered partially selected because only some of it's children are selected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../reference.md#type-object) | false | — | object to check |

### Returns

`[boolean](../reference.md#type-boolean)` — true == object is partially selected false == object is not partially selected

### Groups

- selection

---
## Method: Selection.deselectList

### Description
Deselect an array of items (subset of the entire list). Equivalent to calling +link{Selection.selectList(),selectList(list, false)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array of Object](#type-array-of-object)[] | false | — | array of objects to select |
| rowNums | [Array of Object](#type-array-of-object)[] | false | — | array of objects to select |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.selectRange

### Description
Select range of records from `start` to `end`, non-inclusive.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start index to select |
| end | [number](#type-number) | false | — | end index (non-inclusive) |
| newState | [boolean](../reference.md#type-boolean) | true | — | optional new selection state to set. True means selected, false means unselected. Defaults to true. |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.select

### Description
Select a particular item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../reference.md#type-object) | false | — | object to select |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.selectAll

### Description
Select all records of the list.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| visibleNodesOnly | [boolean](../reference.md#type-boolean) | true | — | If this selection's data object is a tree, if `true` is passed for this parameter, only visible nodes will be selected. Nodes embedded in a closed parent folder (and thus hidden from the user) will not be selected. |

### Returns

`[boolean](../reference.md#type-boolean)` — Returns `true` if the selection actually changed, `false` if not.

### Groups

- selection

---
## Method: Selection.deselectRange

### Description
Deselect range of records from `start` to `end`, non-inclusive

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start index to select |
| end | [number](#type-number) | false | — | end index (non-inclusive) |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.anySelected

### Description
Whether at least one item is selected

### Returns

`[boolean](../reference.md#type-boolean)` — true == at least one item is selected false == nothing at all is selected

### Groups

- selection

---
## Method: Selection.multipleSelected

### Description
Whether multiple items are selected

### Returns

`[boolean](../reference.md#type-boolean)` — true == more than one item is selected false == no items are selected, or only one item is selected

### Groups

- selection

---
## Method: Selection.selectItem

### Description
Select a particular item by its position in the list

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| position | [number](#type-number) | false | — | index of the item to be selected |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.setSelected

### Description
Select or deselect a particular item.  
  
All other selection routines go through this one, so by observing this routine you can monitor all selection changes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../reference.md#type-object) | false | — | object to select |
| newState | [boolean](../reference.md#type-boolean) | false | — | turn selection on or off |
| recordNum | [Integer](../reference_2.md#type-integer) | false | — | The record number to select. Only used in the case of selection in a [multi-link tree](Tree.md#attr-treemultilinktree), where the node itself is not enough to unambiguously identify an occurrence in the tree |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

**Flags**: A

---
## Method: Selection.selectList

### Description
Select an array of items (subset of the entire list)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array of Object](#type-array-of-object) | false | — | array of objects to select or deselect |
| newState | [Boolean](#type-boolean) | true | — | true to select objects, false to deselect. Defaults to true |
| rowNums | [Array of Integer](#type-array-of-integer) | true | — | optional array of row numbers corresponding to the objects in the "list" param. Required for [multi-link trees](Tree.md#attr-treemultilinktree), unless "list" contains [NodeLocator](../reference_2.md#object-nodelocator)s rather than records |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.selectSingle

### Description
Select a single item and deselect everything else

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../reference.md#type-object) | false | — | object to select |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.getLength

### Description
Returns the number of selected records.

### Returns

`[int](../reference.md#type-int)` — number of selected records

### Groups

- selection

---
## Method: Selection.deselect

### Description
Deselect a particular item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../reference.md#type-object) | false | — | object to select |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.deselectAll

### Description
Deselect ALL records of the list

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: Selection.getSelectedRecord

### Description
Return the first item in the list that is selected.  
  
Note that this should only be used if you know that one only one item may be selected, or you really don't care about items after the first one.  
  
To get all selected objects, use `[Selection.getSelection](#method-selectiongetselection)`

### Returns

`[Object](../reference.md#type-object)` — first selected record, or null if nothing selected

### Groups

- selection

---
## Method: Selection.getSelection

### Description
Return an ordered array of all of the selected items

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| excludePartialSelections | [Boolean](#type-boolean) | true | — | When true, partially selected records will not be returned. Otherwise, all fully and partially selected records are returned. |

### Returns

`[Array](#type-array)` — list of selected items

### Groups

- selection

---
