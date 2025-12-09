# Printing

[← Back to API Index](../reference.md)

---

## KB Topic: Printing

### Description
The browser's built-in support for printing will at best print what you see, which in the case of a web application will often be useless, illegible, or partial.

SmartClient has specialized printing support that can take any page built with SmartClient components and provide a reasonable printed view. The default printed view:

*   renders components without clipping or scrolling regions, so that a scrolling grid shows all rows in the cached range around the first visible row
*   removes certain decorative images, such as image-based backgrounds, which may print poorly in black and white
*   converts editing controls into static representations of the data being edited
*   removes interactive elements such as buttons and menus, which don't work on paper and waste space

The default printed view can be customized with settings and method overrides as necessary, including the ability to created printed representations of custom components you have created.

For simple, built in printing support, see the [Canvas.showPrintPreview](../classes/Canvas.md#classmethod-canvasshowprintpreview) and [Canvas.getPrintPreview](../classes/Canvas.md#classmethod-canvasgetprintpreview) APIs, or for finer grained control developers may call [Canvas.getPrintHTML](../classes/Canvas.md#method-canvasgetprinthtml) directly and work with the [PrintCanvas](../classes/PrintCanvas.md#class-printcanvas) or [PrintWindow](../reference.md#class-printwindow) class.

Note that the [CubeGrid](../classes/CubeGrid.md#class-cubegrid) component does not currently support WYSIWYG printing (as documented [in that class](../classes/CubeGrid.md#method-cubegridgetprinthtml)).

### Related

- [Canvas.printComponents](../classes/Canvas.md#classmethod-canvasprintcomponents)
- [Canvas.getPrintPreview](../classes/Canvas.md#classmethod-canvasgetprintpreview)
- [Canvas.showPrintPreview](../classes/Canvas.md#classmethod-canvasshowprintpreview)
- [Canvas.getPrintHTML](../classes/Canvas.md#method-canvasgetprinthtml)
- [Canvas.print](../classes/Canvas.md#method-canvasprint)
- [CubeGrid.getPrintHTML](../classes/CubeGrid.md#method-cubegridgetprinthtml)
- [FormItem.getPrintValueIconStyle](../classes/FormItem.md#method-formitemgetprintvalueiconstyle)
- [FormItem.getPrintValueIcon](../classes/FormItem.md#method-formitemgetprintvalueicon)
- [DrawPane.getPrintHTML](../classes/DrawPane.md#method-drawpanegetprinthtml)
- [FacetChart.getPrintHTML](../classes/FacetChart.md#method-facetchartgetprinthtml)
- [PrintProperties](../reference_2.md#object-printproperties)
- [PrintCanvas](../classes/PrintCanvas.md#class-printcanvas)
- [PrintWindow](../reference.md#class-printwindow)
- [Canvas.printChildrenAbsolutelyPositioned](../classes/Canvas.md#attr-canvasprintchildrenabsolutelypositioned)
- [Canvas.shouldPrint](../classes/Canvas.md#attr-canvasshouldprint)
- [PrintProperties.omitControls](../classes/PrintProperties.md#attr-printpropertiesomitcontrols)
- [PrintProperties.includeControls](../classes/PrintProperties.md#attr-printpropertiesincludecontrols)
- [PrintProperties.printForExport](../classes/PrintProperties.md#attr-printpropertiesprintforexport)
- [DetailViewer.printCellStyle](../classes/DetailViewer.md#attr-detailviewerprintcellstyle)
- [DetailViewer.printLabelStyle](../classes/DetailViewer.md#attr-detailviewerprintlabelstyle)
- [DetailViewer.printHeaderStyle](../classes/DetailViewer.md#attr-detailviewerprintheaderstyle)
- [ListGridField.shouldPrint](../classes/ListGridField.md#attr-listgridfieldshouldprint)
- [ListGrid.checkboxFieldPartialImage](../classes/ListGrid_1.md#attr-listgridcheckboxfieldpartialimage)
- [ListGrid.printCheckboxFieldTrueImage](../classes/ListGrid_1.md#attr-listgridprintcheckboxfieldtrueimage)
- [ListGrid.printCheckboxFieldFalseImage](../classes/ListGrid_1.md#attr-listgridprintcheckboxfieldfalseimage)
- [ListGrid.printCheckboxFieldPartialImage](../classes/ListGrid_1.md#attr-listgridprintcheckboxfieldpartialimage)
- [ListGrid.printBooleanBaseStyle](../classes/ListGrid_1.md#attr-listgridprintbooleanbasestyle)
- [ListGrid.printBooleanTrueImage](../classes/ListGrid_1.md#attr-listgridprintbooleantrueimage)
- [ListGrid.printBooleanFalseImage](../classes/ListGrid_1.md#attr-listgridprintbooleanfalseimage)
- [ListGrid.printBooleanPartialImage](../classes/ListGrid_1.md#attr-listgridprintbooleanpartialimage)
- [ListGrid.printAutoFit](../classes/ListGrid_1.md#attr-listgridprintautofit)
- [ListGrid.printWrapCells](../classes/ListGrid_1.md#attr-listgridprintwrapcells)
- [ListGrid.printHeaderStyle](../classes/ListGrid_1.md#attr-listgridprintheaderstyle)
- [ListGrid.printBaseStyle](../classes/ListGrid_1.md#attr-listgridprintbasestyle)
- [ListGrid.printMaxRows](../classes/ListGrid_1.md#attr-listgridprintmaxrows)
- [FormItem.printTitleStyle](../classes/FormItem.md#attr-formitemprinttitlestyle)
- [FormItem.printTextBoxStyle](../classes/FormItem.md#attr-formitemprinttextboxstyle)
- [FormItem.printReadOnlyTextBoxStyle](../classes/FormItem.md#attr-formitemprintreadonlytextboxstyle)
- [TextItem.printFullText](../classes/TextItem.md#attr-textitemprintfulltext)
- [CheckboxItem.printCheckedImage](../classes/CheckboxItem.md#attr-checkboxitemprintcheckedimage)
- [CheckboxItem.printUncheckedImage](../classes/CheckboxItem.md#attr-checkboxitemprintuncheckedimage)
- [CheckboxItem.printPartialSelectedImage](../classes/CheckboxItem.md#attr-checkboxitemprintpartialselectedimage)
- [CheckboxItem.printUnsetImage](../classes/CheckboxItem.md#attr-checkboxitemprintunsetimage)
- [CheckboxItem.printBooleanBaseStyle](../classes/CheckboxItem.md#attr-checkboxitemprintbooleanbasestyle)
- [TextAreaItem.printFullText](../classes/TextAreaItem.md#attr-textareaitemprintfulltext)
- [FacetChart.printZoomChart](../classes/FacetChart.md#attr-facetchartprintzoomchart)

---
