# CellSelection Documentation

[← Back to API Index](../reference.md)

---

## Class: CellSelection

### Description
Maintains a representation of selection over a 2-dimensional grid of objects.  
Automatically created to manage cell-selection on [CubeGrid](CubeGrid.md#class-cubegrid) widgets.

---
## Method: CellSelection.selectSingleCell

### Description
select a single cell and deselect everything else

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row index of cell to select |
| colNum | [int](../reference.md#type-int) | false | — | column index of cell to select |

### Returns

`[Boolean](#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: CellSelection.selectionChanged

### Description
Observable handler fired whenever the cell selection is modified

### Groups

- selection

---
## Method: CellSelection.getSelectedRecord

### Description
Returns the first record that has any cells selected.

### Returns

`[ListGridRecord](#type-listgridrecord)` — first selected record, or null if nothing selected

### Groups

- selection

---
## Method: CellSelection.deselectCell

### Description
Deselect a particular cell

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row index of the cell to select |
| colNum | [int](../reference.md#type-int) | false | — | column index of the cell to select |

### Returns

`[Boolean](#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: CellSelection.selectCellList

### Description
select an array of cells

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array of Array of int](#type-array-of-array-of-int) | false | — | Array of cells to select. Each cell can be specified as a 2 element array `[rowNum, colNum]` |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: CellSelection.cellIsSelected

### Description
Return true if a particular item is selected

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row index of the cell to check |
| colNum | [int](../reference.md#type-int) | false | — | column index of the cell to check |

### Returns

`[Boolean](#type-boolean)` — true == object is selected false == object is not selected

### Groups

- selection

---
## Method: CellSelection.selectCell

### Description
Select a particular cell

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row index of cell to select |
| colNum | [int](../reference.md#type-int) | false | — | column index of cell to select |

### Returns

`[Boolean](#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: CellSelection.deselectCellList

### Description
deselect an array of cells

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array of Array of int](#type-array-of-array-of-int) | false | — | Array of cells to deselect. Each cell can be specified as a 2 element array `[rowNum, colNum]` |

### Returns

`[boolean](../reference.md#type-boolean)` — true == selection actually changed, false == no change

### Groups

- selection

---
## Method: CellSelection.anySelected

### Description
Is anything in the list selected?

### Returns

`[Boolean](#type-boolean)` — true == at least one item is selected false == nothing at all is selected

### Groups

- selection

---
## Method: CellSelection.getSelectedCells

### Description
Returns an array of the currently selected cells. Each cell is returned as a 2 element array in the form `[rowNum, colNum]`.

### Returns

`[Array](#type-array)` — an array of the selected cells, as 2 element arrays

### Groups

- selection

---
