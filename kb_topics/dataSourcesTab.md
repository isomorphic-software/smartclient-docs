# DataSources Tab

[← Back to API Index](../reference.md)

---

## KB Topic: DataSources Tab

### Description
The DataSources tab, found in the [Admin Console](adminConsole.md#kb-topic-admin-console) and [Developer Console](debugging.md#kb-topic-debugging), lets you view, search and edit data from any DataSource in the currently loaded application, or, if you have the Pro edition or better, any DataSource defined on the server, even if the current application hasn't loaded it.

**Security**

If you are using our server product and you have [deployed the tools](toolsDeployment.md#kb-topic-tools-deployment), then the DataSources tab bypasses normal security restrictions and allows any operation on any DataSource. Otherwise, if the tools are not deployed or not accessible to the current user, then the DataSources tab only lets you do whatever the currently authorized user can do.

If you use the [DataSource auditing](../classes/DataSource.md#attr-datasourceaudit) feature, the DataSources tab also allows you to access the audit trail for any DataSource where auditing is enabled.

**Usage**

The DataSources tab will present you with a list of the available DataSources. If you click on one, a new section will be opened showing the data from that DataSource in a ListGrid, offering filtering via the standard [FilterEditor](../classes/ListGrid_1.md#attr-listgridshowfiltereditor), and editing via standard [grid editing](editing.md#kb-topic-grid-editing). At the bottom of the section, buttons are shown to add a new record, and export the data in various formats to a file (or the screen if not using the server product).

**Reify Export**

To upload data to [Reify](reifyForDevelopers.md#kb-topic-reify-for-developers), a special "Reify Export" button is shown in the header of the DataSources list section. When clicked, the behavior will temporarily change so that you can click DataSources to build up a selection without new sections opening. To finalize your selection, click the same button again, which will appear as "Done Selecting".

When selection is complete, a configuration dialog will open to let you customize how many rows will be fetched for each DataSource (or how many levels for Tree DataSources). Both global and per-DataSource limits are allowed, with a section in the dialog shown for each selected DataSource. If desired, additional per-DataSource criteria can be applied via a [FilterBuilder](../classes/FilterBuilder.md#class-filterbuilder) in its dedicated configuration section. Through a radio button at the top of the dialog, you can also select whether to save the export to a file, or show the output in a dialog. Click the "Export" button to complete configuration and run the export.

---
