# Handling Unsaved Records

[← Back to API Index](../reference.md)

---

## KB Topic: Handling Unsaved Records

### Description
APIs such as [startEditingNew()](../classes/ListGrid_2.md#method-listgridstarteditingnew) or [listEndEditAction:"next"](../classes/ListGrid_1.md#attr-listgridlistendeditaction) allow editing records that have not been saved to the server. These unsaved records are special in several ways:

*   there is no actual Record object in the dataset for them: `getRecord(rowNum)` will return null, instead, `getEditValues(rowNum)` allows access to field values for the unsaved record
*   rows for editing these records always appear at the end of the grid and do not sort with other rows
*   because unsaved records lack an actual Record object and lack a [DataSourceField.primaryKey](../classes/DataSourceField.md#attr-datasourcefieldprimarykey) value, they have limited functionality: they cannot be selected, and do not support [ListGrid.showRecordComponents](../classes/ListGrid_1.md#attr-listgridshowrecordcomponents) and certain other features.

If you need to work with unsaved records and have all ListGrid features apply to them, this is usually a sign that you should re-think your UI for adding new records. Consider the following approaches - which works best will depend on the application:

*   actually save a new record to persistent storage, then start editing it. This has the advantage that the user will never lose data by exiting the application with unsaved records, which can be important if there is a lot of data entry before the record is ready to save (for example, a new issue report in an issue-tracking applications, or a new blog entry). This is also a good approach if the user may want to get a unique ID for the new record right away (again useful for a new issue report or blog entry).
    
    If values for several fields are required before the record should be visible on other screens or to other users, you can add a field to the record to flag it as incomplete so that it is not shown on other screens. Alternatively, require certain fields to be entered via an external form or dialog before the record is added to the grid.
    
    Saving a new record and editing it can be done via [DataSource.addData](../classes/DataSource.md#method-datasourceadddata) followed by a call to [ListGrid.startEditing](../classes/ListGrid_2.md#method-listgridstartediting) once the record has been saved.
    
*   edit new records via a separate [form](../classes/DynamicForm.md#class-dynamicform) instead, possibly in a modal [Window](../classes/Window.md#class-window) - then unsaved records never need to be shown in the grid. Similar to the approach above, this modal form might have only certain minimum fields to make a valid new record, then further editing could continue in the grid.
*   use a [clientOnly DataSource](../classes/DataSource.md#attr-datasourceclientonly) so that records can be saved immediately without contacting the server. This is a good approach if several unsaved records need to be manipulated by multiple components before they are finally saved.
*   use [DataSource.updateCaches](../classes/DataSource.md#method-datasourceupdatecaches) with an "add" DSResponse to cause a new record to be added to the grid due to [automatic cache synchronization](../classes/ResultSet.md#class-resultset). At this point the grid will believe the record exists on the server and it will be treated like any other saved record. This means your server code will need to handle the fact that the ListGrid will submit "update" DSRequests for any subsequent edits.

**NOTE about validation:** by design, SmartClient assumes that any record that has been saved is valid and does not validate field values that appear in records loaded from the server. This includes records added to a clientOnly DataSource via [DataSource.setCacheData](../classes/DataSource.md#method-datasourcesetcachedata) as well as records added due to a call to [DataSource.updateCaches](../classes/DataSource.md#method-datasourceupdatecaches).

Usually the best approach is to avoid this situation by editing such records in a form or other control until they are valid rather than showing invalid records in a grid. However, if such records need to be considered invalid, one approach is to take field values and add them as editValues via [ListGrid.setEditValues](../classes/ListGrid_2.md#method-listgridseteditvalues). At this point the ListGrid will consider the values as user edits and will validate them.

---
