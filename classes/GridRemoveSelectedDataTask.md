# GridRemoveSelectedDataTask Documentation

[← Back to API Index](../main.md)

---

## Class: GridRemoveSelectedDataTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Remove data that is selected in a grid.

### See Also

- [ListGrid.removeSelectedData](ListGrid_2.md#method-listgridremoveselecteddata)

---
## Attr: GridRemoveSelectedDataTask.confirmationMessage

### Description
Message shown to user to confirm deleting a single record on a bound grid.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only three dynamic variables, dsTitle; dsPluralTitle and recordTitle, are available and represent the bound [DataSource.title](DataSource.md#attr-datasourcetitle) and [DataSource.pluralTitle](DataSource.md#attr-datasourcepluraltitle) and the value of the [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) from the first selected record.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.unboundConfirmationMessage

### Description
Message shwon to user to confirm deleting a single record on an unbound grid.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, recordTitle, is available and represents the value of the [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) from the first selected record.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.multipleConfirmationMessage

### Description
Message shown to user to confirm deleting a group of records on a bound grid.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only two dynamic variables, dsTitle and dsPluralTitle, are available and represent the bound [DataSource.title](DataSource.md#attr-datasourcetitle) and [DataSource.pluralTitle](DataSource.md#attr-datasourcepluraltitle) .

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.refuseMultiRemoveMessage

### Description
Message to be shown when multiple records are selected for removal but [GridRemoveSelectedDataTask.allowMultiRecordRemove](#attr-gridremoveselecteddatataskallowmultirecordremove) is not set.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.showConfirmation

### Description
Should we show a confirmation message before removal and allow the user to cancel the operation? If user cancels the removal the workflow is terminated.

Message to be shown is defined in the properties: [GridRemoveSelectedDataTask.confirmationMessage](#attr-gridremoveselecteddatataskconfirmationmessage), [GridRemoveSelectedDataTask.unboundConfirmationMessage](#attr-gridremoveselecteddatataskunboundconfirmationmessage), [GridRemoveSelectedDataTask.multipleConfirmationMessage](#attr-gridremoveselecteddatataskmultipleconfirmationmessage) and [GridRemoveSelectedDataTask.unboundMultipleConfirmationMessage](#attr-gridremoveselecteddatataskunboundmultipleconfirmationmessage). The appropriate message is chosen based on the grid configuration and the number of records being removed.

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.failureElement

### Description
ID of the next sequence or element to proceed to if a failure condition arises from operation.

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.allowMultiRecordRemove

### Description
Can multiple records be removed? If not and multiple records are selected, the [GridRemoveSelectedDataTask.refuseMultiRemoveMessage](#attr-gridremoveselecteddatataskrefusemultiremovemessage) is shown as a warning and the workflow is terminated.

Default is true unless set to `false`.

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.unboundMultipleConfirmationMessage

### Description
Message shown to user to confirm deleting a group of records on an unbound grid.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, recordTitle, is available and represents the value of the [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) from the first selected record.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: GridRemoveSelectedDataTask.requestProperties

### Description
Additional properties to set on the [removeSelectedData](ListGrid_2.md#method-listgridremoveselecteddata) call to perform removal.

Note that `willHandleError` will always be set `true`.

**Flags**: IR

---
