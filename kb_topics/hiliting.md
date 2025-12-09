# Hiliting

[← Back to API Index](../reference.md)

---

## KB Topic: Hiliting

### Description
Hiliting means special visual styling which is applied to specific data values that meet certain criteria.

A [Hilite](../reference_2.md#object-hilite) definition contains styling information such as [Hilite.cssText](../classes/Hilite.md#attr-hilitecsstext) and [Hilite.htmlBefore](../classes/Hilite.md#attr-hilitehtmlbefore) that define what the hilite looks like, as well as properties defining where the hilite is applied. If you create hilites manually, they should ideally specify [textColor](../classes/Hilite.md#attr-hilitetextcolor) and/or [backgroundColor](../classes/Hilite.md#attr-hilitebackgroundcolor) in order to be editable in a [HiliteEditor](../classes/HiliteEditor.md#class-hiliteeditor). If these are not provided, however, note that they will be manufactured automatically from the [cssText](../classes/Hilite.md#attr-hilitecsstext) attribute if it is present.

A hilite can be applied to data **either** by defining [criteria](../classes/Hilite.md#attr-hilitecriteria) or by explicitly including markers on the data itself.

Hiliting rules such as hiliting different ranges of values with different colors can be accomplished entirely client-side by defining [AdvancedCriteria](../reference.md#object-advancedcriteria) in hilite definitions that pick out values to be highlighted.

Hiliting rules that require server-side calculations can be achieved by assigning a [Hilite.id](../classes/Hilite.md#attr-hiliteid) to a hilite definition, and setting the [DataBoundComponent.hiliteProperty](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteproperty) on the records that should show that highlight. This can be used, for example, to hilite the record with the maximum value for a dataset that the application will load incrementally.

### Related

- [HiliteIconPosition](../reference_2.md#type-hiliteiconposition)
- [DataBoundComponent.getHilites](../classes/DataBoundComponent.md#method-databoundcomponentgethilites)
- [DataBoundComponent.setHilites](../classes/DataBoundComponent.md#method-databoundcomponentsethilites)
- [DataBoundComponent.enableHilite](../classes/DataBoundComponent.md#method-databoundcomponentenablehilite)
- [DataBoundComponent.disableHilite](../classes/DataBoundComponent.md#method-databoundcomponentdisablehilite)
- [DataBoundComponent.enableHiliting](../classes/DataBoundComponent.md#method-databoundcomponentenablehiliting)
- [DataBoundComponent.disableHiliting](../classes/DataBoundComponent.md#method-databoundcomponentdisablehiliting)
- [DataBoundComponent.editHilites](../classes/DataBoundComponent.md#method-databoundcomponentedithilites)
- [CubeGrid.setHilites](../classes/CubeGrid.md#method-cubegridsethilites)
- [CubeGrid.hiliteCell](../classes/CubeGrid.md#method-cubegridhilitecell)
- [CubeGrid.hiliteCellList](../classes/CubeGrid.md#method-cubegridhilitecelllist)
- [CubeGrid.hiliteFacetValue](../classes/CubeGrid.md#method-cubegridhilitefacetvalue)
- [DetailViewer.setHilites](../classes/DetailViewer.md#method-detailviewersethilites)
- [ListGrid.hilitesChanged](../classes/ListGrid_2.md#method-listgridhiliteschanged)
- [TileGrid.setHilites](../classes/TileGrid.md#method-tilegridsethilites)
- [ColumnTree.setHilites](../classes/ColumnTree.md#method-columntreesethilites)
- [DynamicForm.setHilites](../classes/DynamicForm.md#method-dynamicformsethilites)
- [Hilite](../reference_2.md#object-hilite)
- [Hilite.id](../classes/Hilite.md#attr-hiliteid)
- [Hilite.cssText](../classes/Hilite.md#attr-hilitecsstext)
- [Hilite.fieldName](../classes/Hilite.md#attr-hilitefieldname)
- [Hilite.criteria](../classes/Hilite.md#attr-hilitecriteria)
- [Hilite.htmlBefore](../classes/Hilite.md#attr-hilitehtmlbefore)
- [Hilite.htmlAfter](../classes/Hilite.md#attr-hilitehtmlafter)
- [Hilite.htmlValue](../classes/Hilite.md#attr-hilitehtmlvalue)
- [Hilite.disabled](../classes/Hilite.md#attr-hilitedisabled)
- [Hilite.canEdit](../classes/Hilite.md#attr-hilitecanedit)
- [Hilite.title](../classes/Hilite.md#attr-hilitetitle)
- [Hilite.textColor](../classes/Hilite.md#attr-hilitetextcolor)
- [Hilite.backgroundColor](../classes/Hilite.md#attr-hilitebackgroundcolor)
- [Hilite.icon](../classes/Hilite.md#attr-hiliteicon)
- [Hilite.replacementValue](../classes/Hilite.md#attr-hilitereplacementvalue)
- [DataBoundComponent.canEditHilites](../classes/DataBoundComponent.md#attr-databoundcomponentcanedithilites)
- [DataBoundComponent.hilites](../classes/DataBoundComponent.md#attr-databoundcomponenthilites)
- [DataBoundComponent.hiliteIcons](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteicons)
- [DataBoundComponent.hiliteIconPosition](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteiconposition)
- [DataBoundComponent.hiliteIconSize](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteiconsize)
- [DataBoundComponent.hiliteIconWidth](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteiconwidth)
- [DataBoundComponent.hiliteIconHeight](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteiconheight)
- [DataBoundComponent.hiliteIconLeftPadding](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteiconleftpadding)
- [DataBoundComponent.hiliteIconRightPadding](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteiconrightpadding)
- [DataBoundComponent.hiliteEditor](../classes/DataBoundComponent.md#attr-databoundcomponenthiliteeditor)
- [CubeGrid.hilites](../classes/CubeGrid.md#attr-cubegridhilites)
- [DetailViewer.hiliteIcons](../classes/DetailViewer.md#attr-detailviewerhiliteicons)
- [DetailViewer.hiliteIconPosition](../classes/DetailViewer.md#attr-detailviewerhiliteiconposition)
- [DetailViewer.hiliteIconSize](../classes/DetailViewer.md#attr-detailviewerhiliteiconsize)
- [DetailViewer.hiliteIconWidth](../classes/DetailViewer.md#attr-detailviewerhiliteiconwidth)
- [DetailViewer.hiliteIconHeight](../classes/DetailViewer.md#attr-detailviewerhiliteiconheight)
- [DetailViewer.hiliteIconLeftPadding](../classes/DetailViewer.md#attr-detailviewerhiliteiconleftpadding)
- [DetailViewer.hiliteIconRightPadding](../classes/DetailViewer.md#attr-detailviewerhiliteiconrightpadding)
- [DetailViewerField.canHilite](../classes/DetailViewerField.md#attr-detailviewerfieldcanhilite)
- [DetailViewerField.hiliteIconPosition](../classes/DetailViewerField.md#attr-detailviewerfieldhiliteiconposition)
- [DetailViewerField.hiliteIconSize](../classes/DetailViewerField.md#attr-detailviewerfieldhiliteiconsize)
- [DetailViewerField.hiliteIconWidth](../classes/DetailViewerField.md#attr-detailviewerfieldhiliteiconwidth)
- [DetailViewerField.hiliteIconHeight](../classes/DetailViewerField.md#attr-detailviewerfieldhiliteiconheight)
- [DetailViewerField.hiliteIconLeftPadding](../classes/DetailViewerField.md#attr-detailviewerfieldhiliteiconleftpadding)
- [DetailViewerField.hiliteIconRightPadding](../classes/DetailViewerField.md#attr-detailviewerfieldhiliteiconrightpadding)
- [ListGrid.hiliteIcons](../classes/ListGrid_1.md#attr-listgridhiliteicons)
- [ListGrid.hiliteIconPosition](../classes/ListGrid_1.md#attr-listgridhiliteiconposition)
- [ListGrid.hiliteIconSize](../classes/ListGrid_1.md#attr-listgridhiliteiconsize)
- [ListGrid.hiliteIconWidth](../classes/ListGrid_1.md#attr-listgridhiliteiconwidth)
- [ListGrid.hiliteIconHeight](../classes/ListGrid_1.md#attr-listgridhiliteiconheight)
- [ListGrid.hiliteIconLeftPadding](../classes/ListGrid_1.md#attr-listgridhiliteiconleftpadding)
- [ListGrid.hiliteIconRightPadding](../classes/ListGrid_1.md#attr-listgridhiliteiconrightpadding)
- [ListGridField.hiliteIconPosition](../classes/ListGridField.md#attr-listgridfieldhiliteiconposition)
- [ListGridField.hiliteIconSize](../classes/ListGridField.md#attr-listgridfieldhiliteiconsize)
- [ListGridField.hiliteIconWidth](../classes/ListGridField.md#attr-listgridfieldhiliteiconwidth)
- [ListGridField.hiliteIconHeight](../classes/ListGridField.md#attr-listgridfieldhiliteiconheight)
- [ListGridField.hiliteIconLeftPadding](../classes/ListGridField.md#attr-listgridfieldhiliteiconleftpadding)
- [ListGridField.hiliteIconRightPadding](../classes/ListGridField.md#attr-listgridfieldhiliteiconrightpadding)
- [ListGrid.hiliteCanReplaceValue](../classes/ListGrid_1.md#attr-listgridhilitecanreplacevalue)
- [ListGrid.canEditHilites](../classes/ListGrid_1.md#attr-listgridcanedithilites)
- [ListGrid.hilites](../classes/ListGrid_1.md#attr-listgridhilites)

---
