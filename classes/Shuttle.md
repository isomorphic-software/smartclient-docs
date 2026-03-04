# Shuttle Documentation

[← Back to API Index](../reference.md)

---

## Class: Shuttle

*Inherits from:* [HLayout](../reference.md#class-hlayout)

### Description
Shuttle-style selection component allowing uses to select records by moving them from a set of source records to a set of target records

---
## Attr: Shuttle.deselectAllButtonHeight

### Description
Height for the [Shuttle.deselectAllButton](#attr-shuttledeselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.deselectAllButton

### Description
ImgButton for deselecting the full set of selected data in the shuttle.

**Flags**: IR

---
## Attr: Shuttle.sourceGridTitle

### Description
Title for the source grid, shown as a [Canvas.groupTitle](Canvas.md#attr-canvasgrouptitle)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Shuttle.fetchOperation

### Description
[OperationId](DSRequest.md#attr-dsrequestoperationid) for fetching records from the shuttle's [DataSource](DataSource.md#class-datasource).

**Flags**: IR

---
## Attr: Shuttle.sortDirection

### Description
[Sort direction](ListGrid_1.md#attr-listgridsortdirection) for this item's list of options. Will be applied to [Shuttle.sourceGrid](#attr-shuttlesourcegrid) and [Shuttle.targetGrid](#attr-shuttletargetgrid). To specify initial sort for each grid separately, these properties may be set per grid using the standard [autoChild pattern](../reference.md#type-autochild).

**Flags**: IR

---
## Attr: Shuttle.selectedValues

### Description
Initial selected values for the shuttle.

If specified, the shuttle will be initialized with records with matching [Shuttle.valueField](#attr-shuttlevaluefield) being selected.

See also [Shuttle.selectedRecords](#attr-shuttleselectedrecords) for initializing selection with specific records. If both properties are specified, `selectedValues` will have no effect

To update the selection by value at runtime use [Shuttle.setSelectedByValue](#method-shuttlesetselectedbyvalue)

**Flags**: IR

---
## Attr: Shuttle.valueField

### Description
This field is expected to be unique for records within the shuttle's data set. If not explicitly specified the [dataSource.primaryKey](DataSource.md#class-datasource) will be used.

May be used to [select records by value](#method-shuttlesetselectedbyvalue) and to retrieve the current [selected values](#method-shuttlegetselectedvalues).

**Flags**: IR

---
## Attr: Shuttle.targetGrid

### Description
List grid containing the selected set of records. The user may unselect items by dragging them from this grid to the [Shuttle.sourceGrid](#attr-shuttlesourcegrid).

**Flags**: IR

---
## Attr: Shuttle.selectAllButtonIcon

### Description
Icon for the [Shuttle.selectAllButton](#attr-shuttleselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.controlBar

### Description
VLayout autoChild holding the [Shuttle.selectAllButton](#attr-shuttleselectallbutton), [Shuttle.selectButton](#attr-shuttleselectbutton), [Shuttle.deselectButton](#attr-shuttledeselectbutton) and [Shuttle.deselectAllButton](#attr-shuttledeselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.selectButton

### Description
ImgButton for selecting a single record

**Flags**: IR

---
## Attr: Shuttle.sortField

### Description
[Sort field](ListGrid_1.md#attr-listgridsortfield) for this item's list of options. Will be applied to [Shuttle.sourceGrid](#attr-shuttlesourcegrid) and [Shuttle.targetGrid](#attr-shuttletargetgrid). To specify initial sort for each grid separately, these properties may be set per grid using the standard [autoChild pattern](../reference.md#type-autochild).

**Flags**: IR

---
## Attr: Shuttle.sourceGrid

### Description
List grid containing the (unselected) set of records. The user may select items by dragging them from this grid to the [Shuttle.targetGrid](#attr-shuttletargetgrid).

**Flags**: IR

---
## Attr: Shuttle.deselectButtonWidth

### Description
Width for the [Shuttle.deselectButton](#attr-shuttledeselectbutton)

**Flags**: IR

---
## Attr: Shuttle.selectButtonWidth

### Description
Width for the [Shuttle.selectButton](#attr-shuttleselectbutton)

**Flags**: IR

---
## Attr: Shuttle.targetGridTitle

### Description
Title for the target grid, shown as a [Canvas.groupTitle](Canvas.md#attr-canvasgrouptitle)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Shuttle.incompleteDataWarning

### Description
Warning to display when the user attempts to [select all](#attr-shuttleselectallbutton) records from a [partially loaded](ResultSet.md#method-resultsetallmatchingrowscached) data set.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Shuttle.deselectButtonHeight

### Description
Height for the [Shuttle.deselectButton](#attr-shuttledeselectbutton)

**Flags**: IR

---
## Attr: Shuttle.fields

### Description
Fields for the [Shuttle.sourceGrid](#attr-shuttlesourcegrid) and [Shuttle.targetGrid](#attr-shuttletargetgrid).

As with other databound components, if fields are not explicitly specified, they will be derived from the [Shuttle.dataSource](#attr-shuttledatasource) as described [here](DataBoundComponent.md#attr-databoundcomponentfields)

**Flags**: IR

---
## Attr: Shuttle.selectButtonIcon

### Description
Icon for the [Shuttle.selectButton](#attr-shuttleselectbutton)

**Flags**: IR

---
## Attr: Shuttle.deselectButton

### Description
ImgButton for deselecting a single record

**Flags**: IR

---
## Attr: Shuttle.selectAllButtonWidth

### Description
Width for the [Shuttle.selectAllButton](#attr-shuttleselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.initialSort

### Description
[Initial sort specifiers](ListGrid_1.md#attr-listgridinitialsort) for this item's list of options. Will be applied to [Shuttle.sourceGrid](#attr-shuttlesourcegrid) and [Shuttle.targetGrid](#attr-shuttletargetgrid). To specify initial sort for each grid separately, these properties may be set per grid using the standard [autoChild pattern](../reference.md#type-autochild).

**Flags**: IR

---
## Attr: Shuttle.deselectAllButtonWidth

### Description
Width for the [Shuttle.deselectAllButton](#attr-shuttledeselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.selectAllButton

### Description
ImgButton for selecting the full set of data in the shuttle.

**Flags**: IR

---
## Attr: Shuttle.filterContext

### Description
DSRequest configuration for retrieving records from this shuttle's dataSource.

**Flags**: IR

---
## Attr: Shuttle.dataSource

### Description
DataSource for this shuttle's data set. The list of options will be fetched from this dataSource unless an explicit [Shuttle.data](#attr-shuttledata) object was also provided.

Note that a shuttle must have either a dataSource or data object.

**Flags**: IR

---
## Attr: Shuttle.data

### Description
List of options for this shuttle.

Note that a shuttle must have either a data object or a dataSource specified

**Flags**: I

---
## Attr: Shuttle.selectedRecords

### Description
Initial set of selected records for the shuttle.

See also [Shuttle.selectedValues](#attr-shuttleselectedvalues) for initializing selection based on record values.

To update the selection at runtime use [Shuttle.selectRecords](#method-shuttleselectrecords) and [Shuttle.deselectRecords](#method-shuttledeselectrecords).

**Flags**: IR

---
## Attr: Shuttle.selectAllButtonHeight

### Description
Height for the [Shuttle.selectAllButton](#attr-shuttleselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.selectButtonHeight

### Description
Height for the [Shuttle.selectButton](#attr-shuttleselectbutton)

**Flags**: IR

---
## Attr: Shuttle.deselectAllButtonIcon

### Description
Icon for the [Shuttle.deselectAllButton](#attr-shuttledeselectallbutton)

**Flags**: IR

---
## Attr: Shuttle.implicitCriteria

### Description
Implicit criteria for retrieving records from this shuttle's dataSource.

These criteria may be combined with `"inSet"` or `"notInSet"` sub criteria for the [Shuttle.valueField](#attr-shuttlevaluefield) in order to populate the set of unselected records in the [Shuttle.sourceGrid](#attr-shuttlesourcegrid). They are [ListGrid.implicitCriteria](ListGrid_1.md#attr-listgridimplicitcriteria) meaning that any user-entered [filter criteria](ListGrid_1.md#attr-listgridshowfiltereditor) will be overlayed on top of these criteria.

**Flags**: IRW

---
## Attr: Shuttle.loadingPlaceholderAttribute

### Description
This attribute will be set to true for any loading placeholder records returned by [Shuttle.getSelectedRecords](#method-shuttlegetselectedrecords)

**Flags**: IRA

---
## Attr: Shuttle.textMatchStyle

### Description
TextMatchStyle for retrieving records from this shuttle's dataSource.

**Flags**: IR

---
## Attr: Shuttle.deselectButtonIcon

### Description
Icon for the [Shuttle.deselectButton](#attr-shuttledeselectbutton)

**Flags**: IR

---
## Method: Shuttle.selectionUpdated

### Description
Notification method fired when records are selected or unselected in this shuttle.

Use [Shuttle.getSelectedRecords](#method-shuttlegetselectedrecords) or [Shuttle.getSelectedValues](#method-shuttlegetselectedvalues) to retrieve the current selection.

---
## Method: Shuttle.getSelectedRecords

### Description
Returns the current set of selected records.

Note that if a user called [Shuttle.setSelectedByValue](#method-shuttlesetselectedbyvalue) for a record that was not loaded in the source list, we may not yet have a selected record for that value. See [Shuttle.valuesFetchInProgress](#method-shuttlevaluesfetchinprogress).

In this case no record will be returned by this method for that record by default. The `includeLoadingPlaceholders` parameter will cause this method to also return placeholder record objects for these unloaded records, which have two properties specified - the [Shuttle.valueField](#attr-shuttlevaluefield) value [\_isLoadingPlaceholder:true](#attr-shuttleloadingplaceholderattribute).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| includeLoadingPlaceholders | [boolean](../reference.md#type-boolean) | true | — | should we include loading placeholder records for selected values whose records have not yet been loaded? |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — currently selected records

---
## Method: Shuttle.setSelectedByValue

### Description
Method to add or remove records from the current selection where the [Shuttle.valueField](#attr-shuttlevaluefield) matches the values passed in.

If the source listGrid does not have a [complete data set](ResultSet.md#method-resultsetallmatchingrowscached) and does not contain an entry for any of the requested values, a separate fetch request will be issued against our [DataSource](DataSource.md#class-datasource) to pick up the records for the specified value(s). The [Shuttle.valuesFetchInProgress](#method-shuttlevaluesfetchinprogress) and [Shuttle.valuesFetchComplete](#method-shuttlevaluesfetchcomplete) methods provide information about this fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Array of String](#type-array-of-string)|[Array of Number](#type-array-of-number) | false | — | Array of values to select |
| selected | [Boolean](#type-boolean) | false | — | New selected state for the records |

---
## Method: Shuttle.getValueFieldName

### Description
Returns the [Shuttle.valueField](#attr-shuttlevaluefield) for this shuttle

### Returns

`[String](#type-string)` — value field name

---
## Method: Shuttle.selectRecords

### Description
Programmatically select a set of records from this shuttle's dataSource. The specified records will be added to any existing selection.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord) | false | — | Records to select |
| fireSelectionChanged | [boolean](../reference.md#type-boolean) | true | — | Fire the [Shuttle.selectionUpdated](#method-shuttleselectionupdated) notification? |

---
## Method: Shuttle.getSelectedValues

### Description
Returns the [valueField](#method-shuttlegetvaluefieldname) value from the current set of selected records.

Note that if a user called [Shuttle.setSelectedByValue](#method-shuttlesetselectedbyvalue) for a record that was not loaded in the source list, we may not yet have a selected record for that value. See [Shuttle.valuesFetchInProgress](#method-shuttlevaluesfetchinprogress).

The `includeUnloadedValues` parameter can be used to return values for these unloaded records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| includeUnloadedValues | [boolean](../reference.md#type-boolean) | true | — | should we include values where the associated record has not yet been loaded? |

### Returns

`[Array of String](#type-array-of-string)|[Array of Number](#type-array-of-number)` — currently selected records' valueField values.

---
## Method: Shuttle.deselectRecords

### Description
Programmatically deselect a set of records that are currently selected and displayed in the target grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord) | false | — | Records to deselect |
| fireSelectionChanged | [boolean](../reference.md#type-boolean) | true | — | Fire the [Shuttle.selectionUpdated](#method-shuttleselectionupdated) notification? |

---
## Method: Shuttle.valuesFetchInProgress

### Description
Returns true if this shuttle is currently fetching record(s) associated with values passed to [Shuttle.setSelectedByValue](#method-shuttlesetselectedbyvalue)

If no explicit `value` parameter was passed, this method will return true if this shuttle has any outstanding values fetches.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | true | — | if passed, this method will return true only if there is an outstanding fetch to retrieve the associated record for this specified value |

### Returns

`[boolean](../reference.md#type-boolean)` — true if there is an outstanding values fetch

---
## Method: Shuttle.clearSelection

### Description
Deselect all currently selected records

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fireSelectionChanged | [boolean](../reference.md#type-boolean) | true | — | Fire the [Shuttle.selectionUpdated](#method-shuttleselectionupdated) notification? |

---
## Method: Shuttle.valuesFetchComplete

### Description
Notification method fired when a fetch to retrieve records for an array of values passed to [Shuttle.setSelectedByValue](#method-shuttlesetselectedbyvalue) is complete.

Note that if no associated record for the specified value was found in the dataSource, this method will still fire.

### Returns

`[boolean](../reference.md#type-boolean)` — true if there is an outstanding values fetch

---
## Method: Shuttle.setImplicitCriteria

### Description
Update the [Shuttle.implicitCriteria](#attr-shuttleimplicitcriteria) for the shuttle.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | new implicitCriteria |

---
