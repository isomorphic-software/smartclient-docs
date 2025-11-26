# ValuesManager Documentation

[← Back to API Index](../reference.md)

---

## Class: ValuesManager

### Description
The ValuesManager manages data from multiple member forms.

If a single logical form needs to be separated into multiple DynamicForm instances for Layout purposes (for example, spanning one logical form across multiple Tabs), a ValuesManager can be used to make the forms act as one logical form, supporting all value-related APIs otherwise called on DynamicForm directly.

A ValuesManager has no visual representation - it is strictly a logical entity, and the member forms provide the user interface. You can initialize a ValuesManager with a set of member forms (by setting [ValuesManager.members](#attr-valuesmanagermembers) at init) or add and remove member forms dynamically.

Calling [ValuesManager.setValues](#method-valuesmanagersetvalues) on a ValuesManager will automatically route new field values to whichever member form is showing an editor for that field. Likewise, calling [ValuesManager.validate](#method-valuesmanagervalidate) will validate all member forms, and [ValuesManager.saveData](#method-valuesmanagersavedata) will initiate a save operation which aggregates values from all member forms.

Like a DynamicForm, a ValuesManager can be databound by setting [ValuesManager.dataSource](#attr-valuesmanagerdatasource). In this case all member forms must also be bound to the same DataSource.

In general, when working with a ValuesManager and its member forms, call APIs on the ValuesManager whenever you are dealing with values that span multiple forms, and only call APIs on member forms that are specific to that form or its fields.

Note that, just as a DynamicForm can track values that are not shown in any FormItem, a ValuesManager may track values for which there is no FormItem in any member form. However, when using a ValuesManager these extra values are only allowed on the ValuesManager itself. Member forms will not track values for which they do not have FormItems.

### See Also

- [memoryLeaks](../kb_topics/memoryLeaks.md#kb-topic-memory-leaks)

---
## Attr: ValuesManager.updateOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) to use when performing update operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: ValuesManager.deepCloneNonFieldValuesOnEdit

### Description
When editing values in this ValuesManager in one or more DataBoundComponents, should we perform a deep clone of values that are not associated with a field (ie, attributes on the record that do not map to a component field either directly by name, or by [FormItem.dataPath](FormItem.md#attr-formitemdatapath). If this value is not explicitly set, it defaults to the value of [DataSource.deepCloneNonFieldValuesOnEdit](DataSource.md#attr-datasourcedeepclonenonfieldvaluesonedit) if there is a dataSource, or to the value of the static [DataSource.deepCloneNonFieldValuesOnEdit](DataSource.md#classattr-datasourcedeepclonenonfieldvaluesonedit) if there is no dataSource.

Like the other `deepCloneOnEdit` settings, this flag only has an effect if you are editing a values object that contains nested objects or arrays.

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [FormItem.dataPath](FormItem.md#attr-formitemdatapath)
- [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit)
- [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit)

**Flags**: IRWA

---
## Attr: ValuesManager.fetchOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) to use when performing fetch operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: ValuesManager.autoSynchronize

### Description
If explicitly set to false, prevents the ValuesManager from automatically propagating data value changes to its members. You can manually synchronize member data values at any time with a call to [ValuesManager.synchronizeMembers](#method-valuesmanagersynchronizemembers).

**Flags**: IRWA

---
## Attr: ValuesManager.dataSource

### Description
Specifies a dataSource for this valuesManager. This dataSource will then be used for validation and client-server flow methods. Can be specified as a dataSource object or an identifier for the dataSource.  
Note that member forms should have the same dataSource applied to them to allow their items to inherit properties from the DataSource fields.

### See Also

- [ValuesManager.setDataSource](#method-valuesmanagersetdatasource)
- [ValuesManager.getDataSource](#method-valuesmanagergetdatasource)

**Flags**: IRW

---
## Attr: ValuesManager.removeOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) to use when performing remove operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: ValuesManager.saveOperationType

### Description
Default [DSOperationType](../reference.md#type-dsoperationtype) to be performed when [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) is called. This property is automatically set on a call to [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) or [DynamicForm.editNewRecord](DynamicForm.md#method-dynamicformeditnewrecord), or may be set directly via [DynamicForm.setSaveOperationType](DynamicForm.md#method-dynamicformsetsaveoperationtype).

If `saveOperationType` is unset, the form will heuristically determine whether an "add" or "update" operation is intended based on whether the primaryKey field is present and editable.

**Flags**: IRW

---
## Attr: ValuesManager.suppressValidationErrorCallback

### Description
When calling [ValuesManager.saveData](#method-valuesmanagersavedata) on a form or valuesManager, by default if the server returns an error code, any callback passed into saveData() will not be fired. If the error code returned by the server indicates a validation error, it will be displayed to the user by updating the form items to show the error messages, and firing any specified hiddenValidationErrors handler, otherwise the standard RPCManager error handling logic would be invoked.

Developers who want to handle errors themselves can override this default by specifying [dsRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) on the DSRequest. In this case the callback passed in will be fired even if the server returns an error status code.

If `suppressValidationErrorCallback` is set to true, if a save attempt returns a _validation_ error code, the user-specified callback will not be fired _even if `willHandleError:true` was specified on the dsRequest_ - though for other error codes, the callback would be fired if willHandleError is specified on the request. Note that this is the historical behavior for SmartClient builds 8.0 and earlier

**Flags**: IRWA

---
## Attr: ValuesManager.addOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) to use when performing add operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: ValuesManager.disableValidation

### Description
If set to true, client-side validators will not run on the form when validate() is called. Server-side validators (if any) will still run on attempted save.

### Groups

- validation

### See Also

- [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata)
- [DynamicForm.submit](DynamicForm.md#method-dynamicformsubmit)

**Flags**: IRWA

---
## Attr: ValuesManager.deepCloneOnEdit

### Description
Before we start editing the values of this ValuesManager in one or more DataBoundComponents, should we perform a deep clone of the underlying values. See [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit) for details of what this means.

If this value is not explicitly set, it defaults to the value of [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit). This value can be overridden per-field with [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit).

Like the other `deepCloneOnEdit` settings, this flag only has an effect if you are editing a values object that contains nested objects or arrays, using [dataPath](Canvas.md#attr-canvasdatapath)s.

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [FormItem.dataPath](FormItem.md#attr-formitemdatapath)
- [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit)
- [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit)

**Flags**: IRWA

---
## Attr: ValuesManager.members

### Description
The set of member components for this valuesManager. These can be specified at init time via the `members` property, or updated at runtime via `addMember()` and `removeMember()`.  
Note: Alternatively a DataBoundComponent can be initialized as a member of a valuesManager by setting the `valuesManager` property of the component to a pre-defined valuesManager instance, or by calling `setValuesManager` on the component.

### See Also

- [ValuesManager.addMember](#method-valuesmanageraddmember)
- [ValuesManager.removeMember](#method-valuesmanagerremovemember)
- [Canvas.setValuesManager](Canvas.md#method-canvassetvaluesmanager)

**Flags**: IRW

---
## Attr: ValuesManager.operator

### Description
What operator should be used to combine sub-criteria from member forms when [ValuesManager.getValuesAsCriteria](#method-valuesmanagergetvaluesascriteria) is called?

**Flags**: IR

---
## ClassMethod: ValuesManager.getById

### Description
Retrieve a ValuesManager by it's global [ID](Canvas.md#attr-canvasid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | global ID of the ValuesManager |

### Returns

`[ValuesManager](#type-valuesmanager)` — the ValuesManager, or null if not found

---
## Method: ValuesManager.itemChanged

### Description
Handler fired whenever a change to a FormItem fires itemChanged() on one of the member forms. Fires after that event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the FormItem where the change event occurred |
| newValue | [Any](#type-any) | false | — | new value for the FormItem |

---
## Method: ValuesManager.editRecord

### Description
Edit an existing record. Updates this editors values to match the values of the record passed in, via [ValuesManager.setValues](#method-valuesmanagersetvalues).

This method will also call [DynamicForm.setSaveOperationType](DynamicForm.md#method-dynamicformsetsaveoperationtype) to ensure subsequent calls to `saveData()` will use an `update` rather than an `add` operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record to be edited as a map of field names to their corresponding values |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata)

---
## Method: ValuesManager.showErrors

### Description
Method to explicitly show the latest set of validation errors present on this ValuesManager.  
Will redraw all member forms to display (or clear) currently visible errors, and fire [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors) to allow custom handling of hidden errors.

### Groups

- errors

---
## Method: ValuesManager.isNewRecord

### Description
Returns true if [ValuesManager.saveOperationType](#attr-valuesmanagersaveoperationtype) is currently "add". See [ValuesManager.saveOperationType](#attr-valuesmanagersaveoperationtype).

### Returns

`[Boolean](#type-boolean)` — whether this form will use an "add" operation when saving

---
## Method: ValuesManager.getValuesAsCriteria

### Description
Retrieves the combined [criteria values](DynamicForm.md#method-dynamicformgetvaluesascriteria) for all member forms.

As with the DynamicForm getValuesAsCriteria, this method may return [AdvancedCriteria](../reference.md#object-advancedcriteria) or simple [Criteria](../reference_2.md#type-criteria) depending on whether the `advanced` parameter was passed, whether the [ValuesManager.operator](#attr-valuesmanageroperator) is set to `"or"` rather than `"and"`, and whether any member forms return [AdvancedCriteria](../reference.md#object-advancedcriteria).

Note that developers can also use [DataSource.combineCriteria](DataSource.md#classmethod-datasourcecombinecriteria) to combine sub-criteria from various sources, including member forms of a ValuesManager, into a combined criteria object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| advanced | [boolean](../reference.md#type-boolean) | false | — | if true, return an [AdvancedCriteria](../reference.md#object-advancedcriteria) object even if the form item values could be represented in a simple [Criterion](../reference_2.md#object-criterion) object. |
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | This parameter may be passed to indicate whether the criteria are to be applied to a substring match (filter) or exact match (fetch). When advanced criteria are returned this parameter will cause the appropriate `operator` to be generated for individual fields' criterion clauses. |

### Returns

`[Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria)` — a [Criteria](../reference_2.md#type-criteria) object, or [AdvancedCriteria](../reference.md#object-advancedcriteria)

### Groups

- criteriaEditing

---
## Method: ValuesManager.getValuesAsAdvancedCriteria

### Description
Return an AdvancedCriteria object based on the current set of values within memberForms.

Similar to [ValuesManager.getValuesAsCriteria](#method-valuesmanagergetvaluesascriteria), except the returned criteria object is guaranteed to be an AdvancedCriteria object, even if none of the form's fields has a specified [FormItem.operator](FormItem.md#attr-formitemoperator)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | If specified the text match style will be used to generate the appropriate `operator` for per field criteria. |

### Returns

`[AdvancedCriteria](#type-advancedcriteria)` — a [AdvancedCriteria](../reference.md#object-advancedcriteria) based on the form's current values

### Groups

- criteriaEditing

---
## Method: ValuesManager.filterData

### Description
Retrieve data that matches the provided criteria, and edit the first record returned.  
Differs from [DynamicForm.fetchData](DynamicForm.md#method-dynamicformfetchdata) in that a case insensitive substring match will be performed against the criteria to retrieve the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: ValuesManager.getValidatedValues

### Description
Call [ValuesManager.validate](#method-valuesmanagervalidate) to check for validation errors. If no errors are found, return the current values for this valuesManager, otherwise return null.

### Returns

`[Object](../reference.md#type-object)` — current values or null if validation failed.

### Groups

- errors

---
## Method: ValuesManager.checkForValidationErrors

### Description
Performs silent validation of the value manager values, like [ValuesManager.valuesAreValid](#method-valuesmanagervaluesarevalid). In contrast to [ValuesManager.valuesAreValid](#method-valuesmanagervaluesarevalid), this method allows checking for server-side errors, and finding out what the errors are.

The callback must be passed unless server-side validation is being skipped, and If passed, it always fires, errors or not, firing synchronously if server validation is skipped.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [ValidationStatusCallback](#type-validationstatuscallback) | false | — | callback to invoke after validation is complete |
| skipServerValidation | [boolean](../reference.md#type-boolean) | true | — | whether to skip doing server-side validation |

### Returns

`[Map](#type-map)` — null if server-side validation is required, or no errors are present; otherwise, an object mapping field names to the associated errors, for those fields that failed validation.

### Groups

- validation

---
## Method: ValuesManager.synchronizeMember

### Description
Update the parameter ValuesManager member to reflect the current values held by the ValuesManager. Note, it is not normally necessary to manually synchronize members

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | Member component to synchronize |

### See Also

- [ValuesManager.synchronizeMembers](#method-valuesmanagersynchronizemembers)
- [ValuesManager.synchronizeMembersOnDataPath](#method-valuesmanagersynchronizemembersondatapath)

---
## Method: ValuesManager.getItem

### Description
Retrieve a [FormItem](FormItem.md#class-formitem) from this ValuesManager.

Takes a field [name](FormItem.md#attr-formitemname) or [DataPath](../reference_2.md#type-datapath), and searches through the members of this valuesManager for an editor for that field. If found the appropriate formItem will be returned. If the "retrieveAll" parameter is true, this method will return all FormItems that are bound to the supplied name or dataPath (a dataPath can be bound to more than one FormItem, as long as those FormItems are on different forms); if "retrieveAll" is false or unset, and there is more than one binding for the dataPath, this method just returns the first one it finds.

Note that if a dataPath is passed in, it should be the full data path for the item, including any canvas level [dataPath](Canvas.md#attr-canvasdatapath) specified on the member form containing this form item.  
Note: Unlike the `DynamicForm` class, this method will not return an item by index

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemID | [FieldName](../reference.md#type-fieldname)|[DataPath](../reference_2.md#type-datapath) | false | — | item fieldName or dataPath identifier |
| retrieveAll | [boolean](../reference.md#type-boolean) | true | — | If true, return the list of all FormItems that are bound to this name or dataPath on a member form of this ValuesManager |

### Returns

`[FormItem](#type-formitem)` — form item for editing/displaying the appropriate field, or null if no formItem can be found for the field.

---
## Method: ValuesManager.hasFieldErrors

### Description
Are there any errors associated with a field in this valuesManager?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to check for errors |

### Returns

`[Boolean](#type-boolean)` — returns true if there are any outstanding validation errors, false otherwise.

### Groups

- errors

---
## Method: ValuesManager.addMember

### Description
Add a new member to this valuesManager. Any [Canvas](Canvas.md#class-canvas) can be a member of a valuesManager, even components like [Layout](Layout.md#class-layout) or [TabSet](TabSet.md#class-tabset) that do not actually have any values to manage. When "valueless" components like these bind to a ValuesManager, it is in order to provide their own child components with a shared valuesManager so that complex data can be displayed and edited - see [DataPath](../reference_2.md#type-datapath) for more details.

For components like [DynamicForm](DynamicForm.md#class-dynamicform) and [ListGrid](ListGrid_1.md#class-listgrid), which do have a set of values to manage, the component's values will subsequently be available through this valuesManager.

Note on pre-existent values when the member component is a [DynamicForm](DynamicForm.md#class-dynamicform):  
If the valuesManager has a value specified for some field, for which the member form has an item, this value will be applied to the member form. This is true whether the item has a value or not.  
However if the member form has a value for some field, and the ValuesManager does not have a specified value for the same field, we allow the valuesManager to pick up the value from the member form.

**Caution:** If a DynamicForm without a [DataSource](DataSource.md#class-datasource) is passed to this method, [DataBoundComponent.setDataSource](DataBoundComponent.md#method-databoundcomponentsetdatasource) will be called on that form, recreating the items from copies of the item configuration stored at the time the form was created. This means that any properties or handlers added to the items after form creation will be lost. When in doubt, set the DataSource in the form as soon as possible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [DynamicForm](#type-dynamicform)|[String](#type-string) | false | — | component (or ID of component) to add to this valuesManager as a member. |

### Groups

- members

### See Also

- [ValuesManager.addMembers](#method-valuesmanageraddmembers)

---
## Method: ValuesManager.setDataSource

### Description
Specifies a dataSource for this valuesManager. This dataSource will then be used for validation and client-server flow methods.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSource | [DataSource](#type-datasource)|[GlobalId](../reference.md#type-globalid) | false | — | Datasource object or identifier to bind to. |

**Flags**: A

---
## Method: ValuesManager.memberSynchronized

### Description
Fires after a member component's values have been synchronized from the ValuesManager's values, upon completion of the [ValuesManager.synchronizeMember](#method-valuesmanagersynchronizemember) call. No default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | Member component that has just completed synchronization |

### See Also

- [ValuesManager.synchronizeMember](#method-valuesmanagersynchronizemember)
- [ValuesManager.synchronizeMembers](#method-valuesmanagersynchronizemembers)
- [ValuesManager.synchronizeMembersOnDataPath](#method-valuesmanagersynchronizemembersondatapath)

---
## Method: ValuesManager.synchronizeMembers

### Description
Update all of this ValuesManager's members to reflect the current values held by the ValuesManager. It is not normally necessary to manually synchronize members, but you will need to do so if you switch off [automatic synchronization](#attr-valuesmanagerautosynchronize).

### See Also

- [ValuesManager.synchronizeMember](#method-valuesmanagersynchronizemember)
- [ValuesManager.synchronizeMembersOnDataPath](#method-valuesmanagersynchronizemembersondatapath)

---
## Method: ValuesManager.handleAsyncValidationReply

### Description
Notification fired when an asynchronous validation completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| success | [boolean](../reference.md#type-boolean) | false | — | true if validation succeeded, false if it failed |
| errors | [Object](../reference.md#type-object) | false | — | Map of errors by fieldName. Will be null if validation succeeded. |

---
## Method: ValuesManager.synchronizeMembersOnDataPath

### Description
Update just those of this ValuesManager's members that have the parameter [dataPath](Canvas.md#attr-canvasdatapath), to reflect the current values held by the ValuesManager. Note, it is not normally necessary to manually synchronize members

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataPath | [String](#type-string) | false | — | dataPath to synchronize |

### See Also

- [ValuesManager.synchronizeMember](#method-valuesmanagersynchronizemember)
- [ValuesManager.synchronizeMembers](#method-valuesmanagersynchronizemembers)

---
## Method: ValuesManager.getFieldErrors

### Description
Returns any validation errors for some field in this valuesManager. Errors will be returned as either a string (a single error message), or an array of strings. If no errors are present, will return null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | fieldName to check for errors |

### Returns

`[String](#type-string)|[Array of String](#type-array-of-string)` — error messages for the field passed in

### Groups

- errors

---
## Method: ValuesManager.handleHiddenValidationErrors

### Description
Method to display validation error messages for a valuesManager when there is not currently visible form item displaying the errors. This will be called when validation fails for  
\- a field in a hidden or undrawn member form  
\- a hidden field in a visible member form  
\- for databound ValuesManagers, a datasource field with specified validators, but not associated item in any member.  
Implement this to provide custom validation error handling for these fields.  
By default hidden validation errors will be logged as warnings in the developerConsole. Return false from this method to suppress that behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errors | [Object](../reference.md#type-object) | false | — | The set of errors returned - this is an object of the form  
  `{fieldName:errors}`  
Where the 'errors' object is either a single string or an array of strings containing the error messages for the field. |

### Returns

`[boolean](../reference.md#type-boolean)` — false from this method to suppress that behavior

**Flags**: A

---
## Method: ValuesManager.validate

### Description
Validate the current set of values for this values manager against validators defined in the member forms. For databound valuesManagers, also perform validation against any validators defined on datasource fields.

Note that if validation errors occur for a value that is not shown in any member forms, those errors will cause a warning and [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors) will be called. This can occur if:  
\- A datasource field has no corresponding item in any member form  
\- The item in question is hidden  
\- The member form containing the item is hidden.

If this form has any fields which require server-side validation (see [Validator.serverCondition](Validator.md#attr-validatorservercondition)) this will also be initialized. Such validation will occur asynchronously. Developers can use [ValuesManager.isPendingAsyncValidation](#method-valuesmanagerispendingasyncvalidation) and [ValuesManager.handleAsyncValidationReply](#method-valuesmanagerhandleasyncvalidationreply) to detect and respond to asynchronous validation.

Note that for silent validation, [ValuesManager.valuesAreValid](#method-valuesmanagervaluesarevalid) (client-side) and [ValuesManager.checkForValidationErrors](#method-valuesmanagercheckforvalidationerrors) (client and server-side) can be used instead.

### Returns

`[Boolean](#type-boolean)` — true if all validation passed

### See Also

- [DynamicForm.validate](DynamicForm.md#method-dynamicformvalidate)

---
## Method: ValuesManager.getMemberValues

### Description
Returns the subset of this valuesManager's values associated with some member form.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | ID of the member form for which we want to retrieve the values. |

### Returns

`[Object](../reference.md#type-object)` — a map of the values for the appropriate member form.

### Groups

- formValues

---
## Method: ValuesManager.clearFieldErrors

### Description
Clear all validation errors associated with some field in this form

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field for which errors should be cleared |
| show | [boolean](../reference.md#type-boolean) | false | — | if true, and the field is present in one of our member forms, redraw it to clear any currently visible validation errors |

### Groups

- errors

---
## Method: ValuesManager.getValue

### Description
Returns the value for some field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | Which value to be returned |
| component | [Canvas](#type-canvas) | true | — | Optional, the component for which we are trying to retrieve a value. This is used to identify which of the potential records to use when the ValuesManager is managing a complex structure involving nested Lists |

### Returns

`[Any](#type-any)` — current value of the appropriate field

### Groups

- formValues

---
## Method: ValuesManager.getErrors

### Description
Returns the set of errors for this valuesManager. Errors will be returned as an object of the format  
`{field1:errors, field2:errors}`  
Where each errors object is either a single error message or an array of error message strings.

### Returns

`[Object](../reference.md#type-object)` — Object containing mapping from field names to error strings. Returns null if there are no errors for this valuesManager.

### Groups

- errors

---
## Method: ValuesManager.clearErrors

### Description
Clears all errors from member forms.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showErrors | [boolean](../reference.md#type-boolean) | false | — | If true, clear any visible error messages. |

### Groups

- errors

---
## Method: ValuesManager.submitValues

### Description
Optional [StringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview) to fire when [ValuesManager.submit](#method-valuesmanagersubmit) is called on this valuesManager (or any form included in this valuesManager).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | the valuesManager values |
| valuesManager | [ValuesManager](#type-valuesmanager) | false | — | the valuesManager being submitted |

### Groups

- submitting

### See Also

- [ValuesManager.submit](#method-valuesmanagersubmit)

---
## Method: ValuesManager.resetValues

### Description
Same as [DynamicForm.reset](DynamicForm.md#method-dynamicformreset).

### Groups

- formValues

---
## Method: ValuesManager.valuesHaveChanged

### Description
Compares the current set of values with the values stored by the call to the [DynamicForm.rememberValues](DynamicForm.md#method-dynamicformremembervalues) method. `rememberValues()` runs when the form is initialized and on every call to [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues). Returns true if the values have changed, and false otherwise.

### Returns

`[Boolean](#type-boolean)` — true if current values do not match remembered values

### Groups

- formValues

### See Also

- [ValuesManager.getChangedValues](#method-valuesmanagergetchangedvalues)
- [ValuesManager.getOldValues](#method-valuesmanagergetoldvalues)

---
## Method: ValuesManager.getDataSource

### Description
Returns the dataSource for this valuesManager. Will return null if this is not a data-bound valuesManager instance.

### Returns

`[DataSource](#type-datasource)` — Datasource object for this valuesManager.

**Flags**: A

---
## Method: ValuesManager.hasErrors

### Description
Are there any errors associated with any fields in this valuesManager?

### Returns

`[Boolean](#type-boolean)` — returns true if there are any outstanding validation errors, false otherwise.

### Groups

- errors

---
## Method: ValuesManager.removeMembers

### Description
Remove multiple member forms from this valuesManager.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| members | [Array of DynamicForm](#type-array-of-dynamicform) | false | — | array of forms to remove |

### Groups

- members

### See Also

- [ValuesManager.removeMember](#method-valuesmanagerremovemember)

---
## Method: ValuesManager.saveData

### Description
Validate and then save the form's current values to the [DataSource](DataSource.md#class-datasource) this form is bound to.

If client-side validators are defined, they are executed first, and if any errors are found the save is aborted and the form will show the errors.

If client-side validation passes, a [DSRequest](../reference_2.md#object-dsrequest) will be sent, exactly as though [DataSource.addData](DataSource.md#method-datasourceadddata) or [DataSource.updateData](DataSource.md#method-datasourceupdatedata) had been called with ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','the form\\'s values')} as data. The [DSRequest.operationType](DSRequest.md#attr-dsrequestoperationtype) will be either "update" or "add", depending on the current [DynamicForm.saveOperationType](DynamicForm.md#attr-dynamicformsaveoperationtype).

On either a client-side or server-side validation failure, validation errors will be displayed in the form. Visible items within a DynamicForm will be redrawn to display errors. Validation failure occurring on hidden items, or DataSource fields with no associated form items may be handled via [DynamicForm.handleHiddenValidationErrors](DynamicForm.md#method-dynamicformhandlehiddenvalidationerrors) or [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors).

In the case of a validation error, the callback will **not** be called by default since the form has already handled the failed save by displaying the validation errors to the user. If you need to do something additional in this case, you can set [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) via the `requestProperties` parameter to force your callback to be invoked. However, first consider:

*   if you are trying to customize display of validation errors, there are several [built-in modes](DynamicForm.md#attr-dynamicformshowerroricons) and [DynamicForm.showErrors](DynamicForm.md#method-dynamicformshowerrors) may be a better place to put customizations.
*   for unrecoverable general errors (eg server is down), [central error handling](RPCManager.md#classmethod-rpcmanagerhandleerror) in invoked, so consider placing customizations there unless an unrecoverable error should be handled specially by this specific form.

**Note:** If a form is to be cleared after saving data, we recommend clearing the form from the callback rather than calling saveData() and then synchronously clearing the form. This gives users a chance to view and respond to any validation errors returned by the server. It is also required to ensure forms containing an [upload field](FileItem.md#class-fileitem), have a chance to upload the file to the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: ValuesManager.getMembers

### Description
Retrieves an array of pointers to all the members for this valuesManager.

### Returns

`[Array of DynamicForm](#type-array-of-dynamicform)` — array of member forms

### Groups

- members

---
## Method: ValuesManager.getChangedValues

### Description
Returns all values within this DynamicForm that have changed since [DynamicForm.rememberValues](DynamicForm.md#method-dynamicformremembervalues) last ran. Note that [DynamicForm.rememberValues](DynamicForm.md#method-dynamicformremembervalues) runs on dynamicForm initialization, and with every call to [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues) so this will typically contain all values the user has explicitly edited since then.

### Returns

`[Object](../reference.md#type-object)` — changed values in the form

### Groups

- formValues

### See Also

- [ValuesManager.getOldValues](#method-valuesmanagergetoldvalues)

---
## Method: ValuesManager.fetchData

### Description
Retrieve data that matches the provided criteria, and edit the first record returned

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: ValuesManager.clearValue

### Description
Clear the value for some field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | Which field to set the value for |

### Groups

- formValues

---
## Method: ValuesManager.getMember

### Description
Returns a pointer to a specific member.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | ID of the member component to retrieve |

### Returns

`[Canvas](#type-canvas)` — member (or null if unable to find a member with the specified ID).

### Groups

- members

---
## Method: ValuesManager.valuesAreValid

### Description
Method to determine whether the current set of values for this values manager would pass validation by the validators defined in the member forms. This method operates client-side, without contacting the server, running validators on the forms' values and returning a value indicating whether validation was successful.

Note that, like [ValuesManager.validate](#method-valuesmanagervalidate), this method will perform value validation even if:

*   A datasource field has no corresponding item in any member form
*   The item in question is hidden
*   The member form containing the item is hidden

Unlike [ValuesManager.validate](#method-valuesmanagervalidate) this method will not store the errors on the forms or display them to the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| returnErrors | [boolean](../reference.md#type-boolean) | true | — | If unset, this method returns a simple boolean value indicating success or failure of validation. If this parameter is passed, this method will return an object mapping each field name to the errors(s) encountered on validation failure, or null if validation was successful. |

### Returns

`[boolean](../reference.md#type-boolean)|[Map](#type-map)` — Boolean value indicating validation success, or if `returnErrors` was specified, an object mapping field names to the associated errors, for those fields that failed validation, or null if validation succeeded.

### Groups

- validation

---
## Method: ValuesManager.setMemberValues

### Description
Set the values for some member form.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | ID of the member form to update |
| values | [Object](../reference.md#type-object) | false | — | new values for the form |

### Groups

- formValues

---
## Method: ValuesManager.editNewRecord

### Description
Prepare to edit a new record by clearing the current set of values (or replacing them with initialValues if specified).  
This method will also call [DynamicForm.setSaveOperationType](DynamicForm.md#method-dynamicformsetsaveoperationtype) to ensure subsequent calls to `saveData()` will use an `add` rather than an `update` operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| initialValues | [Record](#type-record)|[Object](../reference.md#type-object) | true | — | initial set of values for the editor as a map of field names to their corresponding values |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata)

---
## Method: ValuesManager.setValue

### Description
Set the value for some field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | Which field to set the value for |
| newValue | [Any](#type-any) | false | — | New value for the field. |

### Groups

- formValues

---
## Method: ValuesManager.editSelectedData

### Description
Edit the record selected in the specified selection component (typically a [ListGrid](ListGrid_1.md#class-listgrid)).

Updates the values of this editor to match the selected record's values.

If this form has a dataSource, then saving via [ValuesManager.saveData](#method-valuesmanagersavedata) will use the "update" operation type.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionComponent | [ListGrid](#type-listgrid)|[TileGrid](#type-tilegrid)|[ID](#type-id) | false | — | the ListGrid or TileGrid or ID of a [ListGrid](ListGrid_1.md#class-listgrid)/[TileGrid](TileGrid.md#class-tilegrid) whose currently record(s) is/are to be edited |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata)

---
## Method: ValuesManager.submit

### Description
`submit()` is automatically called when a [SubmitItem](../reference.md#class-submititem) in a member form is clicked, or if [saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) is set for some member form, when the "Enter" key is pressed in a text input. Submit can also be manually called.

If [valuesManager.submitValues()](#method-valuesmanagersubmitvalues) exists, it will be called, and no further action will be taken.

Otherwise, [ValuesManager.saveData](#method-valuesmanagersavedata) will be called to handle saving via SmartClient databinding.

The parameters to `submit()` apply only if `submit()` will be calling [ValuesManager.saveData](#method-valuesmanagersavedata). If you override `submit()`, you can safely ignore the parameters as SmartClient framework code does not pass them.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion. |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [ValuesManager.submitValues](#method-valuesmanagersubmitvalues)

---
## Method: ValuesManager.removeMember

### Description
Remove a member form from this valuesManager, so its values are no longer managed by this instance. This does not clear the values associated with the form from the valuesManager - they will still be available via `valuesManager.getValues()`, but will not be updated as the form is manipulated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [DynamicForm](#type-dynamicform)|[String](#type-string) | false | — | form (or ID of form) to remove from this valuesManager |

### Groups

- members

### See Also

- [ValuesManager.removeMembers](#method-valuesmanagerremovemembers)

---
## Method: ValuesManager.getValues

### Description
Returns the current set of values for the values manager instance. This includes the values from any form managed by this manager, as well as any values explicitly applied via [ValuesManager.setValues](#method-valuesmanagersetvalues).

Note that modifying the returned object is not a supported way of adding or modifying values. Instead use [ValuesManager.setValue](#method-valuesmanagersetvalue) or [ValuesManager.setValues](#method-valuesmanagersetvalues).

### Returns

`[Object](../reference.md#type-object)` — a map of the values for this manager

### Groups

- formValues

### See Also

- [DynamicForm.getValues](DynamicForm.md#method-dynamicformgetvalues)

---
## Method: ValuesManager.cancel

### Description
This method exists for clean integration with existing server frameworks that have a 'cancel' feature which typically clears session state associated with the form. When this method is called, an RPC is sent to the server. You must pass the appropriate params property in the request properties as required by your server framework.

For example:

```
 var requestProperties = {
     params: {CANCEL: "cancel"}
 };
 
```
Note that no other form data is sent. By default the current top-level page is replaced with the reply. If you wish to ignore the server reply instead, include the following request properties:
```
 var requestProperties = { 
     // other props ...
     ignoreTimeout: true,
     target: null
 };
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest](#type-dsrequest) | false | — | additional properties to set on the RPCRequest that will be issued |

### Groups

- submitting

### See Also

- [DynamicForm.cancelEditing](DynamicForm.md#method-dynamicformcancelediting)

**Deprecated**

---
## Method: ValuesManager.clearValues

### Description
Clear out all the values managed by this values manager.

### Groups

- formValues

---
## Method: ValuesManager.addMembers

### Description
Add multiple new member forms to this valuesManager.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| members | [Array of DynamicForm](#type-array-of-dynamicform) | false | — | array of forms to add to this valuesManager as members. |

### Groups

- members

### See Also

- [ValuesManager.addMember](#method-valuesmanageraddmember)

---
## Method: ValuesManager.isPendingAsyncValidation

### Description
Is this `ValuesManager` waiting for an asynchronous validation to complete? This method will return true after [ValuesManager.validate](#method-valuesmanagervalidate) is called on a component with server-side validators for some field(s), until the server responds.

Note that the notification method [ValuesManager.handleAsyncValidationReply](#method-valuesmanagerhandleasyncvalidationreply) will be fired when validation completes.

### Returns

`[Boolean](#type-boolean)` — true if this widget has pending asynchronous validations in process

---
## Method: ValuesManager.rememberValues

### Description
Make a snapshot of the current set of values, so we can reset to them later. Creates a new object, then adds all non-method properties of values to the new object. Use `resetValues()` to revert to these values. Note that this method is automatically called when the values for this form are set programmatically via a call to [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues).

### Returns

`[Object](../reference.md#type-object)` — copy of current form values

### Groups

- formValues

---
## Method: ValuesManager.setSaveOperationType

### Description
Setter for the default [DSOperationType](../reference.md#type-dsoperationtype) when [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) is called. Note that this property can also be set by calling [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) or [DynamicForm.editNewRecord](DynamicForm.md#method-dynamicformeditnewrecord)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationType | [DSOperationType](../reference.md#type-dsoperationtype) | false | — | Operation type to use as a default. Valid values are `"add"` or `"update"`. |

---
## Method: ValuesManager.setValues

### Description
Replaces the current values of the ValuesManager and all member components with the values passed in.

Values should be provided as an Object containing the new values as properties, where each propertyName is the name of a [form item](../reference.md#kb-topic-form-items) in one of the member forms, and each property value is the value to apply to that form item via [FormItem.setValue](FormItem.md#method-formitemsetvalue).

Values with no corresponding form item may also be passed, will be tracked by the valuesManager and returned by subsequent calls to [ValuesManager.getValues](#method-valuesmanagergetvalues).

Any [FormItem](FormItem.md#class-formitem) for which a value is not provided will revert to its [defaultValue](FormItem.md#attr-formitemdefaultvalue). To cause all FormItems to revert to default values, pass null.

This method also calls [ValuesManager.rememberValues](#method-valuesmanagerremembervalues) so that a subsequent later call to [ValuesManager.resetValues](#method-valuesmanagerresetvalues) will revert to the passed values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | new set of values for this values manager. |

### Groups

- formValues

---
## Method: ValuesManager.getOldValues

### Description
Returns the set of values last stored by [DynamicForm.rememberValues](DynamicForm.md#method-dynamicformremembervalues). Note that `rememberValues()` is called automatically by [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues), and on form initialization, so this typically contains all values as they were before the user edited them.

### Returns

`[Object](../reference.md#type-object)` — old values in the form

### Groups

- formValues

### See Also

- [ValuesManager.getChangedValues](#method-valuesmanagergetchangedvalues)

---
## Method: ValuesManager.addFieldErrors

### Description
Adds validation errors to the existing set of errors for the field in question. Errors passed in should be a string (for a single error message) or an array of strings. Pass in the showErrors parameter to immediately display the errors to the user by redrawing the appropriate member form item (or if no visible item is found for the field firing [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of field to apply errors to |
| errors | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | error messages for the field |
| showErrors | [boolean](../reference.md#type-boolean) | false | — | should the error(s) be immediately displayed to the user? |

### Groups

- errors

---
## Method: ValuesManager.getSaveOperationType

### Description
Returns the [DSOperationType](../reference.md#type-dsoperationtype) to be performed when [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) or [ValuesManager.saveData](#method-valuesmanagersavedata) is called.  
Valid options are `"add"` or `"update"`.

If a [DSRequest](../reference_2.md#object-dsrequest) configuration object is passed in containing an explicit operationType this will be returned. Otherwise [this.saveOperationType](DynamicForm.md#attr-dynamicformsaveoperationtype) will be returned if set. Note that `saveOperationType` is automatically set via calls to data binding methods such as [DynamicForm.editNewRecord](DynamicForm.md#method-dynamicformeditnewrecord), or it may be [set explicitly](DynamicForm.md#method-dynamicformsetsaveoperationtype).

If no explicit saveOperationType is present, the system will use the following heuristic to determine the save operationType:

*   If the form has no value for the [primaryKey field](DataSource.md#method-datasourcegetprimarykeyfield) this method will return "add". The assumption is that this is a new record, and the field will be populated when the record is created, (as with a "sequence" type field).
*   If, ${isc.DocUtils.linkForRef('method:DynamicForm.setValues','when the form\\'s values were populated')}, the form had value for the [primaryKey field](DataSource.md#method-datasourcegetprimarykeyfield) but it has subsequently be changed, this method will return "add". In this case the value has been changed, either by the user or programmatically so a different (new) record is assumed. This is determined by looking at the [oldValues](DynamicForm.md#method-dynamicformgetoldvalues) for the form.
*   If the [primaryKey field](DataSource.md#method-datasourcegetprimarykeyfield) is editable and a value is now present for the primary key field, but was not present in the [oldValues](DynamicForm.md#method-dynamicformgetoldvalues) for the form, this method will return "add". In this case either no initial values were provided, or a 'sparse' set of values for a new record (with no primary key) were provided to the form and the user has subsequently explicitly entered a new primaryKey field value.
*   Otherwise this method will return "update". Either the primaryKey field is non editable, or the user has not changed it from its initial value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Optional DSRequest config block for the save operation |

### Returns

`[DSOperationType](../reference.md#type-dsoperationtype)` — Operation type for the save request.

---
## Method: ValuesManager.showFieldErrors

### Description
Method to explicitly show the latest set of validation errors present on some field within this ValuesManager.  
If the field in question is present as a visible item in a member form, the form item will be redrawn to display the error message(s). Otherwise [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors) will be fired to allow custom handling of hidden errors.

### Groups

- errors

---
## Method: ValuesManager.setFieldErrors

### Description
Sets validation errors for some field in the valuesManager.  
Errors passed in should be a string (for a single error message) or an array of strings. Pass in the showErrors parameter to immediately display the errors to the user by redrawing the appropriate member form item (or if no visible item is found for the field firing [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of field to apply errors to |
| errors | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | error messages for the field |
| showErrors | [boolean](../reference.md#type-boolean) | false | — | should the error(s) be immediately displayed to the user? |

### Groups

- errors

---
## Method: ValuesManager.setErrors

### Description
Sets validation errors for this valuesManager to the specified set of errors. Errors should be of the format:  
`{field1:errors, field2:errors}`  
where each `errors` object is either a single error message string or an array of error messages.  
If `showErrors` is passed in, error messages will be displayed in the appropriate member form items. For fields with no visible form item, [ValuesManager.handleHiddenValidationErrors](#method-valuesmanagerhandlehiddenvalidationerrors) will be fired instead.  
Note that if `showErrors` is false, errors may be shown at any time via a call to [ValuesManager.showErrors](#method-valuesmanagershowerrors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errors | [Object](../reference.md#type-object) | false | — | list of errors as an object with the field names as keys |
| showErrors | [boolean](../reference.md#type-boolean) | false | — | If true display errors now. |

### Groups

- errors

**Flags**: A

---
## Method: ValuesManager.getMemberForField

### Description
Given a fieldName or dataPath, this method will find the member responsible for interacting with that field's value. If no form is found, returns null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | fieldName or dataPath to check |

### Returns

`[Canvas](#type-canvas)` — member responsible for displaying this field (may be null).

### Groups

- members

---
