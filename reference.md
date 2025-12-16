# SmartClient API Reference (14.0)

This is the central API reference for the SmartClient framework.
## Table of Contents

### Classes

- [Class](classes/Class.md)
  - [BaseWidget](#class-basewidget)
    - [Canvas](classes/Canvas.md)
      - [Layout](classes/Layout.md)
        - [VLayout](#class-vlayout)
          - [ListGrid](classes/ListGrid.md)
            - [TreeGrid](classes/TreeGrid.md)
              - [EditTree](classes/EditTree.md)
              - [TreePalette](#class-treepalette)
              - [PickTreeMenu](#class-picktreemenu)
              - [DOMGrid](#class-domgrid)
            - [CubeGrid](classes/CubeGrid.md)
            - [Menu](classes/Menu.md)
              - [SelectionTreeMenu](#class-selectiontreemenu)
              - [MenuPalette](#class-menupalette)
            - [TableView](classes/TableView.md)
            - [CalendarView](classes/CalendarView.md)
            - [RecordEditor](classes/RecordEditor.md)
            - [PickListMenu](classes/PickListMenu.md)
            - [ListPalette](#class-listpalette)
            - [DateGrid](#class-dategrid)
          - [DateChooser](classes/DateChooser.md)
          - [SectionStack](classes/SectionStack.md)
          - [FormulaBuilder](classes/FormulaBuilder.md)
            - [SummaryBuilder](classes/SummaryBuilder.md)
              - [AIFieldBuilder](classes/AIFieldBuilder.md)
                - [AISortFieldBuilder](#class-aisortfieldbuilder)
          - [RichTextEditor](classes/RichTextEditor.md)
          - [RibbonGroup](classes/RibbonGroup.md)
            - [ToolStripGroup](#class-toolstripgroup)
          - [Reify](classes/Reify.md)
          - [EventCanvas](classes/EventCanvas.md)
            - [ZoneCanvas](#class-zonecanvas)
            - [IndicatorCanvas](#class-indicatorcanvas)
          - [SeleneseRecorder](classes/SeleneseRecorder.md)
          - [FieldPicker](classes/FieldPicker.md)
          - [SavedSearchEditor](classes/SavedSearchEditor.md)
          - [HiliteEditor](classes/HiliteEditor.md)
          - [ScreenLoader](classes/ScreenLoader.md)
          - [CSSEditor](classes/CSSEditor.md)
          - [GradientEditor](classes/GradientEditor.md)
          - [DataView](classes/DataView.md)
        - [SplitPane](classes/SplitPane.md)
          - [NavPanel](classes/NavPanel.md)
          - [TriplePane](#class-triplepane)
        - [Window](classes/Window.md)
          - [ColorPicker](classes/ColorPicker.md)
          - [Dialog](classes/Dialog.md)
            - [BuildViaAIProgressDialog](#class-buildviaaiprogressdialog)
              - [BuildUIViaAIProgressDialog](#class-builduiviaaiprogressdialog)
              - [FilterViaAIProgressDialog](#class-filterviaaiprogressdialog)
              - [HiliteViaAIProgressDialog](#class-hiliteviaaiprogressdialog)
          - [MultiSortDialog](classes/MultiSortDialog.md)
          - [LoginDialog](classes/LoginDialog.md)
          - [MultiGroupDialog](classes/MultiGroupDialog.md)
          - [Portlet](classes/Portlet.md)
          - [ModalWindow](classes/ModalWindow.md)
          - [DatabaseBrowser](classes/DatabaseBrowser.md)
          - [TourWindow](classes/TourWindow.md)
          - [HibernateBrowser](classes/HibernateBrowser.md)
          - [DateRangeDialog](classes/DateRangeDialog.md)
          - [ListPropertiesDialog](classes/ListPropertiesDialog.md)
          - [FieldPickerWindow](classes/FieldPickerWindow.md)
          - [PrintWindow](#class-printwindow)
          - [EditSearchWindow](#class-editsearchwindow)
          - [InlineWindow](#class-inlinewindow)
          - [AIWindow](#class-aiwindow)
          - [AISortProgressDialog](#class-aisortprogressdialog)
        - [PortalLayout](classes/PortalLayout.md)
        - [ColumnTree](classes/ColumnTree.md)
        - [FilterBuilder](classes/FilterBuilder.md)
        - [VStack](#class-vstack)
          - [BatchUploader](classes/BatchUploader.md)
          - [AdvancedHiliteEditor](classes/AdvancedHiliteEditor.md)
          - [MultiFilePicker](#class-multifilepicker)
        - [HLayout](#class-hlayout)
          - [Shuttle](classes/Shuttle.md)
          - [NavigationBar](classes/NavigationBar.md)
          - [ImgSectionHeader](classes/ImgSectionHeader.md)
          - [HiliteRule](classes/HiliteRule.md)
        - [Toolbar](classes/Toolbar.md)
          - [TabBar](classes/TabBar.md)
            - [VerticalTabBar](#class-verticaltabbar)
          - [MenuBar](classes/MenuBar.md)
        - [FilterClause](classes/FilterClause.md)
        - [MultiSortPanel](classes/MultiSortPanel.md)
        - [MultiGroupPanel](classes/MultiGroupPanel.md)
        - [AdaptiveMenu](classes/AdaptiveMenu.md)
        - [ToolStrip](classes/ToolStrip.md)
          - [RibbonBar](classes/RibbonBar.md)
          - [Header](classes/Header.md)
        - [Deck](classes/Deck.md)
        - [ListPropertiesPane](classes/ListPropertiesPane.md)
        - [HStack](#class-hstack)
      - [DrawPane](classes/DrawPane.md)
        - [FacetChart](classes/FacetChart.md)
        - [Gauge](classes/Gauge.md)
      - [Calendar](classes/Calendar.md)
        - [Timeline](#class-timeline)
      - [DynamicForm](classes/DynamicForm.md)
        - [SavedSearchForm](classes/SavedSearchForm.md)
        - [SearchForm](classes/SearchForm.md)
        - [HandPlacedForm](#class-handplacedform)
        - [PropertySheet](#class-propertysheet)
      - [TileLayout](classes/TileLayout.md)
        - [TileGrid](classes/TileGrid.md)
          - [TilePalette](#class-tilepalette)
        - [FlowLayout](#class-flowlayout)
      - [GridRenderer](classes/GridRenderer.md)
      - [TabSet](classes/TabSet.md)
        - [VerticalTabs](#class-verticaltabs)
      - [EditPane](classes/EditPane.md)
      - [DetailViewer](classes/DetailViewer.md)
      - [StatefulCanvas](classes/StatefulCanvas.md)
        - [StretchImg](classes/StretchImg.md)
          - [StretchImgButton](classes/StretchImgButton.md)
            - [ImgTab](classes/ImgTab.md)
            - [MiniNavControl](#class-mininavcontrol)
          - [Scrollbar](classes/Scrollbar.md)
          - [Splitbar](classes/Splitbar.md)
            - [LayoutResizeBar](classes/LayoutResizeBar.md)
            - [Snapbar](classes/Snapbar.md)
          - [Progressbar](classes/Progressbar.md)
          - [ScrollThumb](#class-scrollthumb)
        - [Button](classes/Button.md)
          - [RibbonButton](classes/RibbonButton.md)
            - [RibbonMenuButton](#class-ribbonmenubutton)
            - [IconButton](#class-iconbutton)
              - [IconMenuButton](#class-iconmenubutton)
          - [Label](classes/Label.md)
            - [ViewLoader](classes/ViewLoader.md)
            - [SectionHeader](classes/SectionHeader.md)
            - [RowRangeDisplay](classes/RowRangeDisplay.md)
            - [Placeholder](classes/Placeholder.md)
          - [MenuButton](classes/MenuButton.md)
            - [IMenuButton](classes/IMenuButton.md)
            - [TreeMenuButton](classes/TreeMenuButton.md)
              - [ITreeMenuButton](#class-itreemenubutton)
            - [ToolStripMenuButton](#class-toolstripmenubutton)
            - [TextMenuButton](#class-textmenubutton)
          - [NavigationButton](classes/NavigationButton.md)
          - [SecondaryButton](#class-secondarybutton)
          - [IButton](#class-ibutton)
          - [SimpleTabButton](#class-simpletabbutton)
          - [AutoFitButton](#class-autofitbutton)
          - [ToolStripButton](#class-toolstripbutton)
        - [Img](classes/Img.md)
          - [ImgButton](classes/ImgButton.md)
            - [IconImgButton](classes/IconImgButton.md)
          - [ImgSplitbar](classes/ImgSplitbar.md)
            - [ToolStripResizer](#class-toolstripresizer)
          - [ToolStripSeparator](#class-toolstripseparator)
          - [MockupElement](#class-mockupelement)
        - [ToggleSwitch](classes/ToggleSwitch.md)
        - [SimpleTile](classes/SimpleTile.md)
      - [Slider](classes/Slider.md)
      - [HTMLFlow](classes/HTMLFlow.md)
        - [HTMLPane](classes/HTMLPane.md)
      - [MinimalScrollbar](classes/MinimalScrollbar.md)
      - [EdgedCanvas](classes/EdgedCanvas.md)
      - [DrawKnob](classes/DrawKnob.md)
      - [BrowserPlugin](#class-browserplugin)
        - [Flashlet](classes/Flashlet.md)
          - [FusionChart](classes/FusionChart.md)
        - [ActiveXControl](classes/ActiveXControl.md)
        - [SVG](#class-svg)
      - [RangeSlider](classes/RangeSlider.md)
      - [RichTextCanvas](classes/RichTextCanvas.md)
      - [PrintCanvas](classes/PrintCanvas.md)
      - [NativeScrollbar](#class-nativescrollbar)
      - [LayoutSpacer](#class-layoutspacer)
        - [ToolStripSpacer](#class-toolstripspacer)
        - [FixedSpacer](#class-fixedspacer)
        - [FlexSpacer](#class-flexspacer)
      - [HandPlacedContainer](#class-handplacedcontainer)
    - [DrawItem](classes/DrawItem.md)
      - [DrawGroup](classes/DrawGroup.md)
      - [DrawLabel](classes/DrawLabel.md)
      - [DrawOval](classes/DrawOval.md)
      - [DrawLinePath](classes/DrawLinePath.md)
      - [DrawRect](classes/DrawRect.md)
      - [DrawImage](classes/DrawImage.md)
      - [DrawCurve](classes/DrawCurve.md)
        - [DrawBlockConnector](#class-drawblockconnector)
      - [DrawSector](classes/DrawSector.md)
      - [DrawLine](classes/DrawLine.md)
      - [DrawPath](classes/DrawPath.md)
        - [DrawPolygon](classes/DrawPolygon.md)
          - [DrawTriangle](#class-drawtriangle)
      - [DrawShape](classes/DrawShape.md)
      - [DrawDiamond](classes/DrawDiamond.md)
    - [Sound](classes/Sound.md)
  - [DataSource](classes/DataSource.md)
    - [RestDataSource](classes/RestDataSource.md)
    - [MockDataSource](classes/MockDataSource.md)
    - [FacadeDataSource](classes/FacadeDataSource.md)
    - [XJSONDataSource](classes/XJSONDataSource.md)
    - [WSDataSource](#class-wsdatasource)
  - [FormItem](classes/FormItem.md)
    - [TextItem](classes/TextItem.md)
      - [ComboBoxItem](classes/ComboBoxItem.md)
      - [SpinnerItem](classes/SpinnerItem.md)
      - [UploadItem](classes/UploadItem.md)
      - [ColorItem](classes/ColorItem.md)
        - [ColorPickerItem](#class-colorpickeritem)
      - [LinkItem](classes/LinkItem.md)
      - [FloatItem](#class-floatitem)
        - [DoubleItem](#class-doubleitem)
      - [AIAssistItem](#class-aiassistitem)
      - [IntegerItem](#class-integeritem)
      - [PasswordItem](#class-passworditem)
      - [DataPathItem](#class-datapathitem)
    - [SelectItem](classes/SelectItem.md)
      - [SavedSearchItem](classes/SavedSearchItem.md)
      - [PresetCriteriaItem](classes/PresetCriteriaItem.md)
        - [PresetDateRangeItem](classes/PresetDateRangeItem.md)
    - [DateItem](classes/DateItem.md)
      - [DateTimeItem](classes/DateTimeItem.md)
    - [TimeItem](classes/TimeItem.md)
    - [StaticTextItem](classes/StaticTextItem.md)
      - [MultiPickerItem](classes/MultiPickerItem.md)
        - [SetFilterItem](classes/SetFilterItem.md)
      - [MiniDateRangeItem](classes/MiniDateRangeItem.md)
    - [CanvasItem](classes/CanvasItem.md)
      - [RelativeDateItem](classes/RelativeDateItem.md)
      - [MultiComboBoxItem](classes/MultiComboBoxItem.md)
      - [DateRangeItem](classes/DateRangeItem.md)
      - [FileItem](classes/FileItem.md)
        - [ViewFileItem](#class-viewfileitem)
      - [PickTreeItem](classes/PickTreeItem.md)
        - [IPickTreeItem](#class-ipicktreeitem)
      - [ShuttleItem](classes/ShuttleItem.md)
      - [MultiFileItem](classes/MultiFileItem.md)
      - [SliderItem](classes/SliderItem.md)
      - [ButtonItem](classes/ButtonItem.md)
        - [SubmitItem](#class-submititem)
        - [CancelItem](#class-cancelitem)
        - [ResetItem](#class-resetitem)
      - [SectionItem](classes/SectionItem.md)
      - [RichTextItem](classes/RichTextItem.md)
      - [ToolbarItem](classes/ToolbarItem.md)
      - [ToggleItem](#class-toggleitem)
    - [TextAreaItem](classes/TextAreaItem.md)
      - [AutoFitTextAreaItem](#class-autofittextareaitem)
    - [CheckboxItem](classes/CheckboxItem.md)
    - [RadioGroupItem](classes/RadioGroupItem.md)
    - [HiddenItem](classes/HiddenItem.md)
    - [HeaderItem](classes/HeaderItem.md)
    - [BlurbItem](classes/BlurbItem.md)
    - [SpacerItem](#class-spaceritem)
      - [RowSpacerItem](#class-rowspaceritem)
    - [NativeCheckboxItem](#class-nativecheckboxitem)
      - [RadioItem](#class-radioitem)
    - [BooleanItem](#class-booleanitem)
  - [OperationBinding](classes/OperationBinding.md)
  - [RPCManager](classes/RPCManager.md)
  - [Tree](classes/Tree.md)
    - [ResultTree](classes/ResultTree.md)
  - [ResultSet](classes/ResultSet.md)
    - [FilteredList](classes/FilteredList.md)
  - [ValuesManager](classes/ValuesManager.md)
  - [EditContext](classes/EditContext.md)
  - [AutoTest](classes/AutoTest.md)
  - [DateUtil](classes/DateUtil.md)
  - [Callbacks](classes/Callbacks.md)
  - [Page](classes/Page.md)
  - [SavedSearches](classes/SavedSearches.md)
  - [Validator](classes/Validator.md)
  - [EventHandler](classes/EventHandler.md)
  - [SimpleType](classes/SimpleType.md)
  - [ProcessElement](classes/ProcessElement.md)
    - [Task](classes/Task.md)
      - [UserTask](classes/UserTask.md)
        - [TourStep](classes/TourStep.md)
        - [TourConfirmStep](classes/TourConfirmStep.md)
      - [ServiceTask](classes/ServiceTask.md)
        - [DSRemoveTask](#class-dsremovetask)
        - [DSUpdateTask](#class-dsupdatetask)
        - [DSFetchTask](#class-dsfetchtask)
        - [DSAddTask](#class-dsaddtask)
      - [ScriptTask](classes/ScriptTask.md)
        - [StartProcessTask](classes/StartProcessTask.md)
      - [StateTask](classes/StateTask.md)
    - [ComponentTask](classes/ComponentTask.md)
      - [GridRemoveSelectedDataTask](classes/GridRemoveSelectedDataTask.md)
      - [SetTitleTask](classes/SetTitleTask.md)
      - [FormSaveDataTask](classes/FormSaveDataTask.md)
      - [GridEditRecordTask](classes/GridEditRecordTask.md)
      - [ShowHideTask](classes/ShowHideTask.md)
      - [AddScreenTask](classes/AddScreenTask.md)
      - [GridFetchDataTask](classes/GridFetchDataTask.md)
      - [GetPropertiesTask](classes/GetPropertiesTask.md)
      - [GridSelectRecordsTask](classes/GridSelectRecordsTask.md)
      - [EnableDisableTask](classes/EnableDisableTask.md)
      - [SetPropertiesTask](classes/SetPropertiesTask.md)
      - [PrintCanvasTask](#class-printcanvastask)
      - [FormSetValuesTask](#class-formsetvaluestask)
      - [ShowNextToComponentTask](#class-shownexttocomponenttask)
      - [FormValidateValuesTask](#class-formvalidatevaluestask)
      - [FetchRelatedDataTask](#class-fetchrelateddatatask)
      - [NavigateSplitPaneTask](#class-navigatesplitpanetask)
      - [SetScreenDataTask](#class-setscreendatatask)
      - [GridSetEditValueTask](#class-gridseteditvaluetask)
      - [FormEditNewRecordTask](#class-formeditnewrecordtask)
        - [FormEditRecordTask](#class-formeditrecordtask)
      - [FormSetFieldValueTask](#class-formsetfieldvaluetask)
      - [GridExportClientDataTask](#class-gridexportclientdatatask)
      - [FormDisableFieldTask](#class-formdisablefieldtask)
      - [GridViewSelectedDataTask](#class-gridviewselecteddatatask)
      - [GridExportDataTask](#class-gridexportdatatask)
      - [FormEditSelectedTask](#class-formeditselectedtask)
      - [GridTransferDataTask](#class-gridtransferdatatask)
      - [GridSaveAllEditsTask](#class-gridsavealleditstask)
      - [GridDiscardAllEditsTask](#class-griddiscardalleditstask)
      - [FormClearValuesTask](#class-formclearvaluestask)
      - [FormResetValuesTask](#class-formresetvaluestask)
      - [ShowComponentTask](#class-showcomponenttask)
    - [SendEmailTask](classes/SendEmailTask.md)
    - [DecisionTask](classes/DecisionTask.md)
      - [XORGateway](#class-xorgateway)
    - [MultiDecisionTask](classes/MultiDecisionTask.md)
      - [DecisionGateway](classes/DecisionGateway.md)
    - [SendSMSTask](classes/SendSMSTask.md)
    - [UserConfirmationTask](classes/UserConfirmationTask.md)
      - [AskForValueTask](#class-askforvaluetask)
    - [ShowNotificationTask](classes/ShowNotificationTask.md)
    - [ShowMessageTask](#class-showmessagetask)
    - [ProcessSequence](#class-processsequence)
    - [EndProcessTask](#class-endprocesstask)
    - [UserConfirmationGateway](#class-userconfirmationgateway)
    - [ResetPasswordTask](#class-resetpasswordtask)
    - [LogOutTask](#class-logouttask)
    - [StartTransactionTask](#class-starttransactiontask)
    - [SendTransactionTask](#class-sendtransactiontask)
  - [TabIndexManager](classes/TabIndexManager.md)
  - [Log](classes/Log.md)
  - [XMLTools](classes/XMLTools.md)
  - [EventStream](classes/EventStream.md)
  - [Process](classes/Process.md)
    - [Tour](classes/Tour.md)
      - [Tutorial](#class-tutorial)
  - [AI](classes/AI.md)
  - [Time](classes/Time.md)
  - [Notify](classes/Notify.md)
  - [RPCResponse](classes/RPCResponse.md)
    - [DSResponse](classes/DSResponse.md)
  - [WebService](classes/WebService.md)
  - [MultiWindow](classes/MultiWindow.md)
  - [EditProxy](classes/EditProxy.md)
    - [CanvasEditProxy](#class-canvaseditproxy)
      - [LayoutEditProxy](#class-layouteditproxy)
        - [GridEditProxy](classes/GridEditProxy.md)
        - [WindowEditProxy](#class-windoweditproxy)
        - [HeaderEditProxy](#class-headereditproxy)
        - [SectionStackEditProxy](#class-sectionstackeditproxy)
        - [SplitPaneEditProxy](#class-splitpaneeditproxy)
        - [TileGridEditProxy](#class-tilegrideditproxy)
      - [DetailViewerEditProxy](classes/DetailViewerEditProxy.md)
      - [MenuEditProxy](classes/MenuEditProxy.md)
      - [TabSetEditProxy](classes/TabSetEditProxy.md)
      - [StatefulCanvasEditProxy](#class-statefulcanvaseditproxy)
        - [ProgressbarEditProxy](#class-progressbareditproxy)
        - [LabelEditProxy](#class-labeleditproxy)
          - [SectionStackSectionEditProxy](#class-sectionstacksectioneditproxy)
        - [RibbonButtonEditProxy](#class-ribbonbuttoneditproxy)
        - [ImgEditProxy](#class-imgeditproxy)
      - [FormEditProxy](#class-formeditproxy)
      - [ScreenLoaderEditProxy](#class-screenloadereditproxy)
      - [DrawPaneEditProxy](#class-drawpaneeditproxy)
    - [FormItemEditProxy](classes/FormItemEditProxy.md)
      - [SelectItemEditProxy](classes/SelectItemEditProxy.md)
        - [SavedSearchItemEditProxy](#class-savedsearchitemeditproxy)
        - [RadioGroupItemEditProxy](#class-radiogroupitemeditproxy)
      - [TextItemEditProxy](classes/TextItemEditProxy.md)
        - [TextAreaItemEditProxy](#class-textareaitemeditproxy)
        - [SectionItemEditProxy](#class-sectionitemeditproxy)
        - [BlurbItemEditProxy](#class-blurbitemeditproxy)
      - [CheckboxItemEditProxy](#class-checkboxitemeditproxy)
      - [ButtonItemEditProxy](#class-buttonitemeditproxy)
      - [DateItemEditProxy](classes/DateItemEditProxy.md)
      - [ToolbarItemEditProxy](#class-toolbaritemeditproxy)
      - [FileItemEditProxy](#class-fileitemeditproxy)
    - [FacetChartEditProxy](classes/FacetChartEditProxy.md)
    - [DrawItemEditProxy](#class-drawitemeditproxy)
      - [DrawLabelEditProxy](#class-drawlabeleditproxy)
    - [LayoutResizeBarEditProxy](#class-layoutresizebareditproxy)
    - [ValuesManagerEditProxy](#class-valuesmanagereditproxy)
    - [HandPlacedContainerEditProxy](#class-handplacedcontainereditproxy)
  - [Operators](classes/Operators.md)
  - [Selection](classes/Selection.md)
  - [Browser](classes/Browser.md)
  - [Mail](classes/Mail.md)
  - [Hover](classes/Hover.md)
  - [Authentication](classes/Authentication.md)
    - [Auth](#class-auth)
  - [NumberUtil](classes/NumberUtil.md)
  - [Facet](classes/Facet.md)
  - [GroupingMessages](classes/GroupingMessages.md)
  - [RemoteWindow](classes/RemoteWindow.md)
    - [OpenFinWindow](#class-openfinwindow)
  - [Media](classes/Media.md)
  - [Messaging](classes/Messaging.md)
  - [Offline](classes/Offline.md)
  - [StyleSheetHandler](classes/StyleSheetHandler.md)
  - [DMI](classes/DMI.md)
  - [MathFunction](classes/MathFunction.md)
  - [MultiLinkSelection](classes/MultiLinkSelection.md)
  - [AsyncUtil](classes/AsyncUtil.md)
  - [JSONEncoder](classes/JSONEncoder.md)
  - [VoiceAssist](classes/VoiceAssist.md)
  - [CellSelection](classes/CellSelection.md)
  - [CancellationController](classes/CancellationController.md)
  - [Project](classes/Project.md)
  - [JSON](classes/JSON.md)
  - [SortSpecifierUtil](classes/SortSpecifierUtil.md)
  - [FontLoader](classes/FontLoader.md)
  - [SelectOtherItem](classes/SelectOtherItem.md)
  - [SelectionOutline](classes/SelectionOutline.md)
  - [TextSettings](classes/TextSettings.md)
    - [TextExportSettings](classes/TextExportSettings.md)
    - [TextImportSettings](classes/TextImportSettings.md)
  - [AIEngine](classes/AIEngine.md)
  - [Comm](classes/Comm.md)
  - [SchemaSet](classes/SchemaSet.md)
  - [Timer](classes/Timer.md)
  - [FieldPickerField](classes/FieldPickerField.md)
  - [SyntaxHiliter](#class-syntaxhiliter)
    - [XMLSyntaxHiliter](#class-xmlsyntaxhiliter)
    - [JSSyntaxHiliter](#class-jssyntaxhiliter)
  - [WindowMaximizeButton](#class-windowmaximizebutton)
  - [WindowMinimizeButton](#class-windowminimizebutton)
  - [WindowCloseButton](#class-windowclosebutton)
  - [WindowFooterSpacer](#class-windowfooterspacer)
  - [WindowHeaderLabel](#class-windowheaderlabel)
  - [WindowHeaderIcon](#class-windowheadericon)
  - [WindowResizer](#class-windowresizer)
  - [QuartzManager](#class-quartzmanager)
  - [HiddenPalette](#class-hiddenpalette)
  - [OpenFin](#class-openfin)
  - [RibbonGroupEditProxy](#class-ribbongroupeditproxy)
  - [ToolStripSeparatorEditProxy](#class-toolstripseparatoreditproxy)
  - [React](#class-react)

### Knowledge Base

- [Accessibility / Section 508 compliance](kb_topics/accessibility.md)
- [Admin Console](kb_topics/adminConsole.md)
- [Advanced Filtering](kb_topics/advancedFilter.md)
- [ancestry](#kb-topic-ancestry)
- [Angular Integration](kb_topics/angularIntegration.md)
- [appearance](kb_topics/appearance.md)
- [Application Declaration Files](kb_topics/applicationDeclaration.md)
- [Array Math](#kb-topic-array-math)
- [autoChildren](kb_topics/autoChildren.md)
- [Using AutoChildren](kb_topics/autoChildUsage.md)
- [Automated Testing](kb_topics/automatedTesting.md)
- [Background Download](kb_topics/backgroundDownload.md)
- [Mockup Importer](kb_topics/balsamiqImport.md)
- [baseLine](#kb-topic-baseline)
- [Binary Fields](kb_topics/binaryFields.md)
- [Supported Browsers](kb_topics/browserSupport.md)
- [Native Browser Zoom Support](kb_topics/browserZoom.md)
- [builtinGroupingModes](kb_topics/builtinGroupingModes.md)
- [Button Icon](kb_topics/buttonIcon.md)
- [Automatic Cache Synchronization](kb_topics/cacheSynchronization.md)
- [Caching](kb_topics/caching.md)
- [cellStyleSuffixes](kb_topics/cellStyleSuffixes.md)
- [Client-side Data Integration](kb_topics/clientDataIntegration.md)
- [Client Only DataSources](kb_topics/clientOnlyDataSources.md)
- [Client-Server Integration](kb_topics/clientServerIntegration.md)
- [ComboBoxItem PickList Filtering](kb_topics/comboBoxFiltering.md)
- [ComboBoxItem criteria](kb_topics/comboBoxItemCriteria.md)
- [Component Binding](#kb-topic-component-binding)
- [Component Schema](kb_topics/componentSchema.md)
- [Component XML](kb_topics/componentXML.md)
- [CompoundFormItem_skinning](#kb-topic-compoundformitem_skinning)
- [Compression](kb_topics/compression.md)
- [Handling concurrent edits in SmartClient DataSources](kb_topics/concurrentEdits.md)
- [Component Containment and Hierarchy](kb_topics/containment.md)
- [Criteria Editing](kb_topics/criteriaEditing.md)
- [cues](#kb-topic-cues)
- [Custom Querying Overview](kb_topics/customQuerying.md)
- [Customizing Sass-based Skins](kb_topics/customSassSkins.md)
- [Including custom elements in the tab order](kb_topics/customTabElements.md)
- [DataBinding](kb_topics/databinding.md)
- [DataBound Component Methods](kb_topics/dataBoundComponentMethods.md)
- [Data Changes](#kb-topic-data-changes)
- [Creating DataSources](kb_topics/dataSourceDeclaration.md)
- [DataSource and Component XML Localization](kb_topics/dataSourceLocalization.md)
- [DataSource Operations](kb_topics/dataSourceOperations.md)
- [Relations](kb_topics/dataSourceRelations.md)
- [DataSources Tab](kb_topics/dataSourcesTab.md)
- [Date and Time Format and Storage](kb_topics/dateFormatAndStorage.md)
- [Database Configuration](kb_topics/dbConfigTool.md)
- [debug](kb_topics/debug.md)
- [Debugging](kb_topics/debugging.md)
- [Using the Debug Modules](kb_topics/debugModules.md)
- [Declarative Security](kb_topics/declarativeSecurity.md)
- [Deployment Management Console](kb_topics/deploymentManagement.md)
- [The Developer Console RPC Tab](kb_topics/devConsoleRPCTab.md)
- [Dashboards & Tools Framework Overview](kb_topics/devTools.md)
- [Direct Method Invocation](kb_topics/dmiOverview.md)
- [SmartClient Reference Overview](#kb-topic-smartclient-reference-overview)
- [DOM Integration & Third-party Components](kb_topics/domIntegration.md)
- [Drag and Drop](kb_topics/dragdrop.md)
- [drawing](#kb-topic-drawing)
- [DataSource Facade pattern](kb_topics/dsFacade.md)
- [DSRequest data auto-converted to bean types](kb_topics/dsRequestBeanTypes.md)
- [dsRequestEquivalence](kb_topics/dsRequestEquivalence.md)
- [dsSpecialFields](kb_topics/dsSpecialFields.md)
- [dynamicCriteria](kb_topics/dynamicCriteria.md)
- [Grid Editing](kb_topics/editing.md)
- [elements](#kb-topic-elements)
- [Enabling and Disabling](kb_topics/enable.md)
- [Error Handling Overview](kb_topics/errorHandling.md)
- [errors](kb_topics/errors.md)
- [eventBubbling](#kb-topic-eventbubbling)
- [events](kb_topics/events.md)
- [Copy and Paste with Excel](kb_topics/excelPasting.md)
- [Experimental Features](kb_topics/experimental.md)
- [Exports & Cell Background Color](kb_topics/exportBGColor.md)
- [Exports & Formatting](kb_topics/exportFormatting.md)
- [Feature Explorer Overview](kb_topics/featureExplorerOverview.md)
- [Server Features and Custom Persistence](kb_topics/featuresCustomPersistence.md)
- [Field-Level Security](kb_topics/fieldLevelAuth.md)
- [File Assembly](kb_topics/fileAssembly.md)
- [files](kb_topics/files.md)
- [FileSource Operations](kb_topics/fileSource.md)
- [Flag Abbreviations](#kb-topic-flag-abbreviations)
- [Focus](kb_topics/focus.md)
- [FormItem Styling](kb_topics/formItemStyling.md)
- [Form Layout](kb_topics/formLayout.md)
- [Form Titles](kb_topics/formTitles.md)
- [formulaFields](kb_topics/formulaFields.md)
- [DataSourceField formula functions](kb_topics/formulaFunction.md)
- [Values Manager](#kb-topic-values-manager)
- [Frozen Fields](kb_topics/frozenFields.md)
- [Google Application Engine (GAE)](#kb-topic-google-application-engine-gae)
- [Determining the size of a drawn canvas](kb_topics/gettingCanvasSize.md)
- [Grid Filtering Overview](kb_topics/gridFiltering.md)
- [gridHeader](kb_topics/gridHeader.md)
- [gridValidation](kb_topics/gridValidation.md)
- [Beans and the DSRequest / DSResponse](kb_topics/hbBeans.md)
- [Integration with Hibernate](kb_topics/hibernateIntegration.md)
- [Hiliting](kb_topics/hiliting.md)
- [Internationalization and Localization](kb_topics/i18n.md)
- [I18n Messages](kb_topics/i18nMessages.md)
- [Internet Explorer "filter" effects](kb_topics/IEFilters.md)
- [image](#kb-topic-image)
- [imageColumns](kb_topics/imageColumns.md)
- [images](kb_topics/images.md)
- [Integrating AI Technology](kb_topics/integratingAI.md)
- [Integrating into Existing Apps](kb_topics/integrationIntoExistingApps.md)
- [Installing the SmartClient runtime](kb_topics/iscInstall.md)
- [SmartClient Server Summary](kb_topics/iscServer.md)
- [Form Items](#kb-topic-form-items)
- [Iteration](#kb-topic-iteration)
- [Java Module Dependencies](kb_topics/javaModuleDependencies.md)
- [JPA & Hibernate Relations](kb_topics/jpaHibernateRelations.md)
- [Integration with JPA](kb_topics/jpaIntegration.md)
- [Integration with JSF](kb_topics/jsfIntegration.md)
- [SmartClient JSP Tags](#kb-topic-smartclient-jsp-tags)
- [<isomorphic:jsString>](#kb-topic-isomorphicjsstring)
- [JUnit + Selenium WebDriver](kb_topics/jUnitWebDriver.md)
- [Keyboard Events](kb_topics/keyboardEvents.md)
- [layoutMember](#kb-topic-layoutmember)
- [<isomorphic:loadAssembly>](kb_topics/loadAssemblyTag.md)
- [<isomorphic:loadDMIStubs>](kb_topics/loadDMIStubsTag.md)
- [<isomorphic:loadDS>](kb_topics/loadDSTag.md)
- [Loading Optional Modules](kb_topics/loadingOptionalModules.md)
- [<isomorphic:loadISC>](kb_topics/loadISCTag.md)
- [<isomorphic:loadModules>](#kb-topic-isomorphicloadmodules)
- [<isomorphic:loadProject>](kb_topics/loadProjectTag.md)
- [<isomorphic:loadUI>](kb_topics/loadUITag.md)
- [<isomorphic:loadWSDL>](kb_topics/loadWSDLTag.md)
- [<isomorphic:loadXMLSchema>](kb_topics/loadXMLSchemaTag.md)
- [Localized Number Formatting](#kb-topic-localized-number-formatting)
- [Logging migration](kb_topics/loggingMigration.md)
- [longEvents](#kb-topic-longevents)
- [Manual JPA & Hibernate Integration](kb_topics/manualJpaHibernate.md)
- [Maven Support](kb_topics/mavenSupport.md)
- [Memory Leaks](kb_topics/memoryLeaks.md)
- [Real-Time Messaging](kb_topics/messaging.md)
- [Metadata Import](kb_topics/metadataImport.md)
- [Mobile Application Development](kb_topics/mobileDevelopment.md)
- [multiAutoChildren](#kb-topic-multiautochildren)
- [Transparent Multi-Tenancy](kb_topics/multiTenancy.md)
- [Network Performance](kb_topics/networkPerformance.md)
- [Don't Misuse Frames](kb_topics/noFrames.md)
- [.NET, PHP, Serverless Integration](kb_topics/nonJavaBackend.md)
- [NPMJS Support](kb_topics/npmjs.md)
- [Observation](#kb-topic-observation)
- [Server-side OData DataSource](kb_topics/odataDataSource.md)
- [OpenAPI Specification (OAS) Support](kb_topics/openapiSupport.md)
- [Operations Overview](kb_topics/operations.md)
- [patternOperators](kb_topics/patternOperators.md)
- [Canvas Percentage sizing](kb_topics/percentSizing.md)
- [Integration with PhoneGap](kb_topics/phonegapIntegration.md)
- [pickList](kb_topics/pickList.md)
- [Platform Dependencies](kb_topics/platformDependencies.md)
- [Writing AutoTests for multiple environments](kb_topics/portableAutoTests.md)
- [positioning](kb_topics/positioning.md)
- [Printing](kb_topics/printing.md)
- [Progressive Loading](kb_topics/progressiveLoading.md)
- [Prompting](#kb-topic-prompting)
- [Quartz DataSources](kb_topics/quartzAdapters.md)
- [Integrating Pre-Existing SmartClient Apps with React](kb_topics/reactIntegration.md)
- [Using SmartClient with React](kb_topics/reactSupport.md)
- [Registering Classes for Reflection](kb_topics/reflection.md)
- [Reify Overview](kb_topics/reify.md)
- [Reify OnSite: Adding Custom Workflow Tasks](kb_topics/reifyAddWorkflowTask.md)
- [Adding Custom Components to Reify](kb_topics/reifyCustomComponents.md)
- [Adding Custom DataSources to Reify](kb_topics/reifyCustomDataSources.md)
- [Reify for Developers](kb_topics/reifyForDevelopers.md)
- [Importing from Reify](kb_topics/reifyMaven.md)
- [Reify Messaging](kb_topics/reifyMessaging.md)
- [Reify OnSite](kb_topics/reifyOnSite.md)
- [Generating Reliable AutoTestLocators](kb_topics/reliableLocators.md)
- [Relogin](kb_topics/relogin.md)
- [Remote Debugging](kb_topics/remoteDebugging.md)
- [Grid row-range and row-count display](kb_topics/rowRangeDisplay.md)
- [rpcPrompt](#kb-topic-rpcprompt)
- [Dynamic Rules](kb_topics/ruleCriteria.md)
- [Safe Skinning](kb_topics/safeSkinning.md)
- [scrolling](kb_topics/scrolling.md)
- [Deploying the SmartClient SDK](kb_topics/sdkInstall.md)
- [Selection](kb_topics/selection.md)
- [server.properties file](kb_topics/server_properties.md)
- [Server DataSource Integration](kb_topics/serverDataIntegration.md)
- [Notes on Server-side DataSource Implementations](kb_topics/serverDataSourceImplementation.md)
- [Server Framework Initialization](kb_topics/serverInit.md)
- [Server logging](kb_topics/serverLogging.md)
- [Server-side REST Connector](kb_topics/serverRestConnector.md)
- [Server Scripting](kb_topics/serverScript.md)
- [Server Summaries](kb_topics/serverSummaries.md)
- [The Core and Optional SmartClient servlets](kb_topics/servletDetails.md)
- [Sharing Nodes](kb_topics/sharingNodes.md)
- [Porting Showcase samples to React](kb_topics/showcasePorting.md)
- [Simple Names mode](kb_topics/simpleNamesMode.md)
- [sizing](kb_topics/sizing.md)
- [Skin Editor](kb_topics/skinEditor.md)
- [Skinning / Theming](kb_topics/skinning.md)
- [skins](kb_topics/skins.md)
- [SmartClient Architecture](kb_topics/smartArchitecture.md)
- [Integrating SmartClient with Cypress](kb_topics/smartClientCypress.md)
- [snapGridDragging](kb_topics/snapGridDragging.md)
- [snapPositioning](#kb-topic-snappositioning)
- [Integration with Spring](kb_topics/springIntegration.md)
- [SQL Connection Pooling](kb_topics/sqlConnectionPooling.md)
- [SQL DataSources](kb_topics/sqlDataSource.md)
- [SQL Database Settings in server.properties](kb_topics/sqlSettings.md)
- [SQL DataSource vs JPA, EJB, MyBatis and other technologies](kb_topics/sqlVsJPA.md)
- [Standalone DataSource Usage](kb_topics/standaloneDataSourceUsage.md)
- [state](kb_topics/state.md)
- [Stateful Images](kb_topics/statefulImages.md)
- [statusCodes](kb_topics/statusCodes.md)
- [StockIcons Overview](kb_topics/stockIcons.md)
- [Strict Mode](kb_topics/strictMode.md)
- [String Methods Overview](kb_topics/stringMethods.md)
- [submitting](kb_topics/submitting.md)
- [Sun's java-engine implementation - Notice and Disclaimer](kb_topics/sunNotice.md)
- [SVG Symbols Overview](kb_topics/svgSymbols.md)
- [Tab Order Overview](kb_topics/tabOrderOverview.md)
- [Task Input Expressions](kb_topics/taskInputExpression.md)
- [Task Input / Output](kb_topics/taskIO.md)
- [Test Data](kb_topics/testData.md)
- [TestRunner](kb_topics/testRunner.md)
- [Text Direction](#kb-topic-text-direction)
- [Integration with Titanium](kb_topics/titaniumIntegration.md)
- [Tools Deployment](kb_topics/toolsDeployment.md)
- [Transaction Chaining](kb_topics/transactionChaining.md)
- [Tree DataBinding](kb_topics/treeDataBinding.md)
- [TreeGrid drag and drop](kb_topics/treeGridDrop.md)
- [Troubleshooting thread deadlocks on the server](kb_topics/troubleshootingServerDeadlocks.md)
- [TypeScript Support](kb_topics/typeScriptSupport.md)
- [Union DataSources](kb_topics/unionDataSource.md)
- [Handling Unsaved Records](kb_topics/unsavedRecords.md)
- [Uploading Files](kb_topics/upload.md)
- [Using Selenium Scripts (Selenese)](kb_topics/usingSelenium.md)
- [validation](kb_topics/validation.md)
- [validatorExecution](#kb-topic-validatorexecution)
- [valueMap](#kb-topic-valuemap)
- [values](#kb-topic-values)
- [Velocity context variables](kb_topics/velocitySupport.md)
- [visibility](kb_topics/visibility.md)
- [Window Header](#kb-topic-window-header)
- [Custom Server DataSources](kb_topics/writeCustomDataSource.md)
- [WSDL Binding](kb_topics/wsdlBinding.md)
- [xmlClientVsServer](#kb-topic-xmlclientvsserver)
- [xmlCriteriaShorthand](kb_topics/xmlCriteriaShorthand.md)
- [<isomorphic:XML>](kb_topics/xmlTag.md)
- [XSS and CSRF Security](kb_topics/xssAndCSRFSecurity.md)
- [zIndex](#kb-topic-zindex)

---
## Class: BaseWidget

### Description
Base class for [Canvas](classes/Canvas.md#class-canvas) and [DrawItem](classes/DrawItem.md#class-drawitem).

---
## Class: VLayout

*Inherits from:* [Layout](classes/Layout.md#class-layout)

### Description
A subclass of Layout that applies a sizing policy along the vertical axis, interpreting percent and "\*" sizes as proportions of the height of the layout. VLayouts will set any members that do not have explicit widths to match the layout.

### See Also

- [Layout.vPolicy](classes/Layout.md#attr-layoutvpolicy)

---
## Class: VStack

*Inherits from:* [Layout](classes/Layout.md#class-layout)

### Description
A subclass of Layout that simply stacks members on the vertical axis without trying to manage their height. On the horizontal axis, any members that do not have explicit widths will be sized to match the width of the stack.

### See Also

- [Layout.vPolicy](classes/Layout.md#attr-layoutvpolicy)

---
## Class: HLayout

*Inherits from:* [Layout](classes/Layout.md#class-layout)

### Description
A subclass of Layout that applies a sizing policy along the horizontal axis, interpreting percent and "\*" sizes as proportions of the width of the layout. HLayouts will set any members that do not have explicit heights to match the layout.

### See Also

- [Layout.hPolicy](classes/Layout.md#attr-layouthpolicy)

---
## Class: CanvasEditProxy

*Inherits from:* [EditProxy](classes/EditProxy.md#class-editproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Canvas](classes/Canvas.md#class-canvas) objects when editMode is enabled.

### Groups

- devTools

---
## Class: LayoutEditProxy

*Inherits from:* [CanvasEditProxy](#class-canvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Layout](classes/Layout.md#class-layout) objects when editMode is enabled.

### Groups

- devTools

---
## Class: BrowserPlugin

*Inherits from:* [Canvas](classes/Canvas.md#class-canvas)

### Description
Container for a Browser Plugin.

---
## Class: RibbonMenuButton

*Inherits from:* [RibbonButton](classes/RibbonButton.md#class-ribbonbutton)

### Description
A simple subclass of [RibbonButton](classes/RibbonButton.md#class-ribbonbutton) that shows a menuIcon by default and implements showMenu().

This class has [showMenuIcon](classes/RibbonButton.md#attr-ribbonbuttonshowmenuicon) set to `true` by default, and has a [RibbonButton.menuIconClick](classes/RibbonButton.md#method-ribbonbuttonmenuiconclick) handler which will show the specified [RibbonButton.menu](classes/RibbonButton.md#attr-ribbonbuttonmenu) via a call to [RibbonButton.showMenu](classes/RibbonButton.md#method-ribbonbuttonshowmenu). This menuIconClick handler cancels default click behavior, so, if a user clicks the menu icon, any specified [click handler](classes/Canvas.md#method-canvasclick) for the button as a whole will not fire.

---
## Attr: RibbonMenuButton.showMenuIcon

### Description
Whether to show the [menu-icon](classes/RibbonButton.md#attr-ribbonbuttonmenuiconsrc) which fires the [RibbonButton.menuIconClick](classes/RibbonButton.md#method-ribbonbuttonmenuiconclick) notification method when clicked.

### Groups

- menu

**Flags**: IRW

---
## Class: CheckboxItemEditProxy

*Inherits from:* [FormItemEditProxy](classes/FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [CheckboxItem](classes/CheckboxItem.md#class-checkboxitem) when editMode is enabled.

### Groups

- devTools

---
## Method: CheckboxItemEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's value as \[ \] or \[x\].

---
## Method: CheckboxItemEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component value |

---
## Class: ButtonItemEditProxy

*Inherits from:* [FormItemEditProxy](classes/FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [ButtonItems](classes/ButtonItem.md#class-buttonitem) when editMode is enabled.

### Groups

- devTools

---
## Method: ButtonItemEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's `title` or `name`.

---
## Method: ButtonItemEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `defaultValue`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component defaultValue |

---
## Class: DrawItemEditProxy

*Inherits from:* [EditProxy](classes/EditProxy.md#class-editproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [DrawItems](classes/DrawItem.md#class-drawitem) except for [DrawLabels](classes/DrawLabel.md#class-drawlabel) when editMode is enabled.

### Groups

- devTools

---
## Method: DrawItemEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's title.

---
## Method: DrawItemEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component title |

---
## Class: StatefulCanvasEditProxy

*Inherits from:* [CanvasEditProxy](#class-canvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [StatefulCanvas](classes/StatefulCanvas.md#class-statefulcanvas) objects when editMode is enabled.

### Groups

- devTools

---
## Method: StatefulCanvasEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component title |

---
## Method: StatefulCanvasEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's title.

---
## Class: ProgressbarEditProxy

*Inherits from:* [StatefulCanvasEditProxy](#class-statefulcanvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Progressbar](classes/Progressbar.md#class-progressbar) objects when editMode is enabled.

### Groups

- devTools

---
## Method: ProgressbarEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `percentDone`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component percentDone |

---
## Method: ProgressbarEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's `percentDone`.

---
## Class: DrawLabelEditProxy

*Inherits from:* [DrawItemEditProxy](#class-drawitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [DrawLabels](classes/DrawLabel.md#class-drawlabel) when editMode is enabled.

### Groups

- devTools

---
## Method: DrawLabelEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `contents`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component contents |

---
## Method: DrawLabelEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's `contents`.

---
## Class: LabelEditProxy

*Inherits from:* [StatefulCanvasEditProxy](#class-statefulcanvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Label](classes/Label.md#class-label) objects when editMode is enabled.

### Groups

- devTools

---
## Method: LabelEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's `contents`.

---
## Method: LabelEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `contents`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component contents |

---
## Class: PrintWindow

*Inherits from:* [Window](classes/Window.md#class-window)

### Description
Subclass of [Window](classes/Window.md#class-window) used for displaying a printable view. Includes a "Print" button header control to trigger printing of content.

### Groups

- printing

---
## Attr: PrintWindow.printButtonTitle

### Description
Title for the print button

**Flags**: IRW

---
## Attr: PrintWindow.title

### Description
Title for the print window

**Flags**: IRW

---
## Attr: PrintWindow.externalStylesheet

### Description
Setting this property will cause the specified stylesheet to be loaded in this window's printable HTML frame.

The stylesheet should be specified as a URL to load.

**Flags**: IRWA

---
## Method: PrintWindow.setPrintButtonTitle

### Description
Setter for title for the print button

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| printButtonTitle | [String](#type-string) | false | — | new title for the print button |

---
## Class: WindowEditProxy

*Inherits from:* [LayoutEditProxy](#class-layouteditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Window](classes/Window.md#class-window) objects when editMode is enabled.

### Groups

- devTools

---
## Method: WindowEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component title |

---
## Method: WindowEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's title.

---
## Class: HeaderEditProxy

*Inherits from:* [LayoutEditProxy](#class-layouteditproxy)

### Description
[HeaderEditProxy](#class-headereditproxy) that handles [Header](classes/Header.md#class-header) objects when editMode is enabled.

### Groups

- devTools

---
## Method: HeaderEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `title`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component title |

---
## Method: HeaderEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](classes/EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's `title`.

---
## Class: DrawTriangle

*Inherits from:* [DrawPolygon](classes/DrawPolygon.md#class-drawpolygon)

### Description
DrawItem subclass to render triangles

---
## Attr: DrawTriangle.points

### Description
Array of points of the triangle. specified in the [local coordinate system](classes/DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Method: DrawTriangle.resizeBy

### Description
Resize by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](#type-distance) | false | — | number of pixels to resize by horizontally |
| dY | [Distance](#type-distance) | false | — | number of pixels to resize by vertically |

---
## Method: DrawTriangle.getCenter

### Description
Returns the [incenter](http://en.wikipedia.org/wiki/Incenter#Cartesian_coordinates) of the triangle in [local coordinates](classes/DrawPane.md#class-drawpane).

### Returns

`[Point](#type-point)` — the incenter in local coordinates

---
## Class: NativeScrollbar

*Inherits from:* [Canvas](classes/Canvas.md#class-canvas)

### Description
The NativeScrollbar widget will render in the browser as a native scrollbar, and has APIs allowing it to be applied to scroll content any another widget on the page. Essentially this behaves similarly to the [Scrollbar](classes/Scrollbar.md#class-scrollbar) class but will be rendered as a native browser scrollbar rather than using media, thus providing the advantages of an independant scrollbar (support for rendering the scrollbar separate from the content it effects, support for "virtual scrolling" mechanisms where content size is unknown at initial render, etc), with a native look and feel and without requiring the loading of additional media on the page.

To enable this for a component simply set [Canvas.showCustomScrollbars](classes/Canvas.md#attr-canvasshowcustomscrollbars) to true and set [Canvas.scrollbarConstructor](classes/Canvas.md#attr-canvasscrollbarconstructor) to `"NativeScrollbar"`

---
## Class: PrintCanvasTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Print canvas by showing print preview.

### See Also

- [Canvas.showPrintPreview](classes/Canvas.md#classmethod-canvasshowprintpreview)
- [RPCManager.exportContent](classes/RPCManager.md#classmethod-rpcmanagerexportcontent)

---
## Attr: PrintCanvasTask.exportAsPdf

### Description
Should the canvas contents be exported to a PDF file instead of a print preview?

An export file name can be specified in [PrintCanvasTask.exportFilename](#attr-printcanvastaskexportfilename).

**Flags**: IR

---
## Attr: PrintCanvasTask.printWindowProperties

### Description
Properties to apply to the generated print window.

**Flags**: IR

---
## Attr: PrintCanvasTask.printProperties

### Description
PrintProperties object for customizing the print HTML output.

**Flags**: IR

---
## Attr: PrintCanvasTask.exportFilename

### Description
Default name of the exported PDF file.

**Flags**: IR

---
## Class: FormSetValuesTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Set form values.

### See Also

- [DynamicForm.setValues](classes/DynamicForm.md#method-dynamicformsetvalues)

---
## Attr: FormSetValuesTask.values

### Description
Values to be set on the form.

Data values prefixed with "$" will be treated as a [taskInputExpression](kb_topics/taskInputExpression.md#kb-topic-task-input-expressions). Use [FormSetValuesTask.fixedValues](#attr-formsetvaluestaskfixedvalues) for any values that start with "$" but should be treated as a literal.

**Flags**: IR

---
## Attr: FormSetValuesTask.fixedValues

### Description
Values to be combined with the data from the [ServiceTask.values](classes/ServiceTask.md#attr-servicetaskvalues) if specified, via simple copying of fields, with explicitly specified [ServiceTask.values](classes/ServiceTask.md#attr-servicetaskvalues) overriding `fixedValues`.

**Flags**: IR

---
## Class: EditSearchWindow

*Inherits from:* [Window](classes/Window.md#class-window)

### Description
Window that simply contains a [SavedSearchEditor](classes/SavedSearchEditor.md#class-savedsearcheditor) as the [AutoChild](#type-autochild) `savedSearchEditor`.

Automatically used by [SavedSearchItem](classes/SavedSearchItem.md#class-savedsearchitem) and [ListGrid.canSaveSearches](classes/ListGrid_1.md#attr-listgridcansavesearches); cannot be used directly and is documented only for skinning and internationalization purposes.

---
## Attr: EditSearchWindow.title

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: EditSearchWindow.savedSearchEditor

### Description
Has no effect unless [ListGrid.showBackgroundComponents](classes/ListGrid_1.md#attr-listgridshowbackgroundcomponents) is `true`.

[SavedSearchEditor](classes/SavedSearchEditor.md#class-savedsearcheditor) embedded in the EditSearchWindow.

**Flags**: IR

---
## Class: TreePalette

*Inherits from:* [TreeGrid](classes/TreeGrid.md#class-treegrid)

### Description
A TreeGrid that implements the Palette behavior, so it can be used as the source for drag and drop instantiation of components when combined with an [EditContext](classes/EditContext.md#class-editcontext) as the drop target.

Each [TreeNode](reference_2.md#object-treenode) within [TreeGrid.data](classes/TreeGrid.md#attr-treegriddata) can be a [PaletteNode](#object-palettenode).

### Groups

- devTools

---
## Attr: TreePalette.componentDefaults

### Description
Defaults to apply to all components originating from this palette.

### Groups

- devTools

**Flags**: IR

---
## Attr: TreePalette.canSaveSearches

### Description
Option to save searches is disabled for treePalettes

**Flags**: IRA

---
## Attr: TreePalette.canShowFilterEditor

### Description
Option to show filter editor is disabled for treePalettes

**Flags**: IRA

---
## Class: MultiFilePicker

*Inherits from:* [VStack](#class-vstack)

### Description
The MultiFilePicker is a pop-up picker used by the [MultiFileItem](classes/MultiFileItem.md#class-multifileitem) to allow the user to enter several files for upload.

### Groups

- upload

---
## Attr: MultiFilePicker.showInWindow

### Description
If set true, the picker will be displayed inside a Window.

**Flags**: IR

---
## Attr: MultiFilePicker.title

### Description
Title for the Window implemented as a container for this picker in some skins.

### Groups

- basics

**Flags**: IRW

---
## Attr: MultiFilePicker.minUploadFields

### Description
Minimum number of upload fields to show. This many fields will show up initially.

**Flags**: IRW

---
## Attr: MultiFilePicker.maxUploadFields

### Description
The maximum number of upload fields to show. If not specified, user can add as many upload fields as he wishes.

**Flags**: IRW

---
## Class: SpacerItem

*Inherits from:* [FormItem](classes/FormItem.md#class-formitem)

### Description
A SpacerItem takes up a single cell in the FormLayout, of arbitrary size.

---
## Attr: SpacerItem.showTitle

### Description
we never show a separate title cell for spacers

### Groups

- appearance

**Flags**: IRW

---
## Attr: SpacerItem.width

### Description
default width for the spacer

### Groups

- appearance

**Flags**: IRW

---
## Attr: SpacerItem.height

### Description
default height for the spacer

### Groups

- appearance

**Flags**: IRW

---
## Class: RowSpacerItem

*Inherits from:* [SpacerItem](#class-spaceritem)

### Description
Form item that renders as a blank row in the form layout.  
Set [RowSpacerItem.startRow](#attr-rowspaceritemstartrow) to `false` to create a rowSpacer that simply takes up every remaining column in the current row rather than starting a new row.

---
## Attr: RowSpacerItem.colSpan

### Description
by default, separators span all remaining columns

### Groups

- appearance

**Flags**: IRW

---
## Attr: RowSpacerItem.startRow

### Description
these items are in a row by themselves by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: RowSpacerItem.showTitle

### Description
we never show a separate title cell for separators

### Groups

- appearance

**Flags**: IRW

---
## Attr: RowSpacerItem.endRow

### Description
these items are in a row by themselves by default

### Groups

- appearance

**Flags**: IRW

---
## Class: ShowNextToComponentTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Show a component next to some other component.

### See Also

- [Canvas.showNextTo](classes/Canvas.md#method-canvasshownextto)

---
## Attr: ShowNextToComponentTask.canOcclude

### Description
Can this component can be positioned on top of the other component if there isn't room to show next to it?

**Flags**: IR

---
## Attr: ShowNextToComponentTask.side

### Description
Which side of the other canvas should we show? Options are "top", "bottom", "left", "right". (Defaults to "right")

**Flags**: IR

---
## Attr: ShowNextToComponentTask.nextToComponentId

### Description
The other component where this component will show.

**Flags**: IR

---
## Attr: ShowNextToComponentTask.skipAnimation

### Description
Set to `false` to not use animation to show component.

**Flags**: IR

---
## Class: WSDataSource

*Inherits from:* [DataSource](classes/DataSource.md#class-datasource)

### Description
A WSDataSource is a DataSource that is preconfigured to contact the WSDL web service built into the SDK (see isomorphic/system/schema/SmartClientOperations.wsdl). This WSDL service can be easily implemented on Java and non-Java backends.

WSDataSource supports all 4 DataSource operations (fetch, add, update, remove) and can be used with ListGrids, DynamicForms and other [DataBoundComponent](#interface-databoundcomponent)s just like other DataSources.

Note that WSDataSource is specifically designed for use with SmartClientOperations.wsdl. If you are trying to connect to a pre-existing WSDL service, start with just [DataSource](classes/DataSource.md#class-datasource), not WSDataSource, and see the [WSDL Integration](kb_topics/wsdlBinding.md#kb-topic-wsdl-binding) chapter for an overview.

---
## Class: FloatItem

*Inherits from:* [TextItem](classes/TextItem.md#class-textitem)

### Description
A TextItem for managing a text field that displays a floating point value. FloatItem is the default FormItem if the [FormItem.type](classes/FormItem.md#attr-formitemtype) is "float".

FloatItem displays its value according to the [FormItem.decimalPrecision](classes/FormItem.md#attr-formitemdecimalprecision) and [FormItem.decimalPad](classes/FormItem.md#attr-formitemdecimalpad) properties of the FormItem. While the value is being edited, the item will display the value with its original precision and without extra zero-padding.

### Groups

- gwtFloatVsDouble

---
## Attr: FloatItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](classes/FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Class: SyntaxHiliter

### Description
Abstract base class for regular expression-based source code colorizer.

An instance of this class is never instantiated. Instead, use one of the source-specific subclasses: [XMLSyntaxHiliter](#class-xmlsyntaxhiliter) or [JSSyntaxHiliter](#class-jssyntaxhiliter).

_NOTE: This class exists only for use with the SmartClient Feature Explorer and SmartGWT Showcases and cannot be used in any other environment._

---
## Method: SyntaxHiliter.hilite

### Description
Highlights the passed in source by applying span style elements to matched tokens and returns it as a string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [String](#type-string) | false | — | the source to be colorized |

### Returns

`[String](#type-string)` — the marked-up source as HTML

---
## Class: ToolStripSeparator

*Inherits from:* [Img](classes/Img.md#class-img)

### Description
Simple subclass of Img with appearance appropriate for a ToolStrip separator

---
## Attr: ToolStripSeparator.vSrc

### Description
Image for vertically oriented separator (for horizontal toolstrips).

**Flags**: IR

---
## Attr: ToolStripSeparator.editProxyConstructor

### Description
Default class used to construct the [EditProxy](classes/EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](classes/Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ToolStripSeparator.hSrc

### Description
Image for horizontally oriented separator (for vertical toolstrips).

**Flags**: IR

---
## Attr: ToolStripSeparator.skinImgDir

### Description
Path to separator image.

**Flags**: IR

---
## Class: ZoneCanvas

*Inherits from:* [EventCanvas](classes/EventCanvas.md#class-eventcanvas)

### Description
A subclass of [EventCanvas](classes/EventCanvas.md#class-eventcanvas), used to render [styled areas](classes/Calendar.md#attr-calendarzones) in [calendar views](classes/CalendarView.md#class-calendarview).

A ZoneCanvas is a semi-transparent canvas that highlights a portion of a calendar view, by rendering across all lanes and behind normal [events](classes/Calendar.md#attr-calendardata).

By default, the canvas shows a bottom-aligned label containing the [zone name](classes/CalendarEvent.md#attr-calendareventname). Default styling is specified at the [calendar level](classes/Calendar.md#attr-calendarzonestylename) and can be overridden for [individual zones](classes/CalendarEvent.md#attr-calendareventstylename).

---
## Class: IndicatorCanvas

*Inherits from:* [EventCanvas](classes/EventCanvas.md#class-eventcanvas)

### Description
A subclass of [EventCanvas](classes/EventCanvas.md#class-eventcanvas), used to render [indicator lines](classes/Calendar.md#attr-calendarindicators) at important points in [calendar views](classes/CalendarView.md#class-calendarview).

An IndicatorCanvas is a non-interactive, semi-transparent canvas that highlights a portion of a calendar view, by rendering across all lanes and behind normal [events](classes/Calendar.md#attr-calendardata).

By default, the canvas shows no label but does show a hover.

Default styling is specified at the [calendar level](classes/Calendar.md#attr-calendarindicatorstylename) and can be overridden for [individual indicators](classes/CalendarEvent.md#attr-calendareventstylename).

---
## Class: FormValidateValuesTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Validate a form and show errors to user.

### See Also

- [DynamicForm.validate](classes/DynamicForm.md#method-dynamicformvalidate)

---
## Attr: FormValidateValuesTask.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)?

See [taskInputExpressions](kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state outputs.

Note that this property does not affect the task at all but is an indicator to the user and to the workflow editor of the behavior of the task as coded (See [Process.passThruTaskOutput](classes/Process.md#method-processpassthrutaskoutput)).

**Flags**: IR

---
## Class: AISortFieldBuilder

*Inherits from:* [AIFieldBuilder](classes/AIFieldBuilder.md#class-aifieldbuilder)

### Description
Shows an interface allowing a user to enter a description of how they would like the AI to sort the grid records. A new AI-generated field will be created from that and populated via AI. The description of an existing AI field may also be edited.

---
## Attr: AISortFieldBuilder.instructionsTextStart

### Description
Text providing instructions for using the `AISortFieldBuilder`.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AISortFieldBuilder.titleFieldTitle

### Description
The [TextItem.title](classes/FormItem.md#attr-formitemtitle) of the [FormulaBuilder.titleField](classes/FormulaBuilder.md#attr-formulabuildertitlefield).

### Groups

- i18nMessages

**Flags**: IRWA

---
## Class: ShowMessageTask

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Show an informational message and wait for the user to acknowledge.

---
## Attr: ShowMessageTask.textFormula

### Description
Formula to be used to calculate the message contents. Use [ShowMessageTask.message](#attr-showmessagetaskmessage) property to assign a static message instead.

Available fields for use in the formula are the current [rule context](classes/Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: ShowMessageTask.message

### Description
Message to display. To display a dynamic message see [ShowMessageTask.textFormula](#attr-showmessagetasktextformula).

**Flags**: IR

---
## Attr: ShowMessageTask.type

### Description
Message type.

**Flags**: IR

---
## Class: PickTreeMenu

*Inherits from:* [TreeGrid](classes/TreeGrid.md#class-treegrid)

### Description
[TreeGrid](classes/TreeGrid.md#class-treegrid) subclass used, by default, by FormItems which implement [PickList](reference_2.md#interface-picklist) to display a [collapsible tree](classes/PickList.md#attr-picklistdatasettype) of selectable options.

Can be subclassed, customized and assigned to FormItems via the [pickTreeConstructor](classes/ComboBoxItem.md#attr-comboboxitempicktreeconstructor) attribute.

---
## Attr: PickTreeMenu.canSaveSearches

### Description
Option to save searches is disabled for PickTreeMenus

**Flags**: IRA

---
## Attr: PickTreeMenu.canShowFilterEditor

### Description
Option to show filter editor is disabled for pickTreeMenus by default

**Flags**: IRA

---
## Class: BuildViaAIProgressDialog

*Inherits from:* [Dialog](classes/Dialog.md#class-dialog)

### Description
A dialog that can be used to inform the user of progress made on a build-via-AI process.

If [BuildViaAIProgressDialog.canCancel](#attr-buildviaaiprogressdialogcancancel) is set to `true`, then a cancel button will be displayed that, when clicked, will cancel the build-via-AI process.

---
## Attr: BuildViaAIProgressDialog.title

### Description
Title for this Window, shown if [showTitle](classes/Window.md#attr-windowshowtitle) is true in the [header](classes/Window.md#attr-windowheader) (if drawn).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: BuildViaAIProgressDialog.canCancel

### Description
Whether to allow the user to cancel the AI process.

**Flags**: IR

---
## Class: FetchRelatedDataTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Fetch data related to a record in another component.

### See Also

- [ListGrid.fetchRelatedData](classes/ListGrid_2.md#method-listgridfetchrelateddata)

---
## Attr: FetchRelatedDataTask.dataSource

### Description
The DataSource used with [FetchRelatedDataTask.recordSourceComponent](#attr-fetchrelateddatataskrecordsourcecomponent) to pull related data. If not specified, [FetchRelatedDataTask.recordSourceComponent](#attr-fetchrelateddatataskrecordsourcecomponent) will be used to obtain the schema.

**Flags**: IR

---
## Attr: FetchRelatedDataTask.recordSourceComponent

### Description
Component to pull record for locating related data.

**Flags**: IR

---
## Class: NavigateSplitPaneTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Causes the list pane component to load data and update its title based on the current selection in the source pane. Also shows the pane if it's not already visible.

### See Also

- [SplitPane.navigatePane](classes/SplitPane.md#method-splitpanenavigatepane)

---
## Attr: NavigateSplitPaneTask.showRecursively

### Description
Set to `false` to not show a component's parents.

**Flags**: IR

---
## Attr: NavigateSplitPaneTask.targetPane

### Description
Pane target to be navigated from the current pane.

**Flags**: IR

---
## Attr: NavigateSplitPaneTask.title

### Description
Title to show instead of the automatically chosen one.

**Flags**: IR

---
## Class: SVG

*Inherits from:* [BrowserPlugin](#class-browserplugin)

### Description
ISC Abstraction for SVG controls

---
## Attr: SVG.src

### Description
Location from which to load the SVG.

Note: if you do not specify a src value, ISC will load the special svg 'svgCanvas.svg' from the helpers directory. This SVG is simply an empty root element - essentially a blank canvas. You can use this feature to write components that programmatically manipulate the SVG DOM without needing to ship placeholder SVG files.

**Flags**: IR

---
## Attr: SVG.pluginsPage

### Description
This attribute specifies the page the user should go to to get the plugin required to view this SVG.

The default pluginsPage is: "http://www.adobe.com/svg/viewer/install/"

**Flags**: IR

---
## Class: MiniNavControl

*Inherits from:* [StretchImgButton](classes/StretchImgButton.md#class-stretchimgbutton)

### Description
Compact control for up/down navigation that roughly looks like an up arrowhead next to a down arrowhead.

---
## Attr: MiniNavControl.upButtonSrc

### Description
Image used for the up arrowhead.

**Flags**: IR

---
## Attr: MiniNavControl.skinImgDir

### Description
—

**Flags**: IR

---
## Attr: MiniNavControl.downButtonSrc

### Description
Image used for the down arrowhead.

**Flags**: IR

---
## Method: MiniNavControl.upClick

### Description
Notification method fired when the up button is clicked.

---
## Method: MiniNavControl.downClick

### Description
Notification method fired when the down button is clicked.

---
## Class: ListPalette

*Inherits from:* [ListGrid](classes/ListGrid_1.md#class-listgrid)

### Description
A ListGrid that implements the [Palette](#interface-palette) behavior, so it can be used as the source for drag and drop instantiation of components when combined with an [EditContext](classes/EditContext.md#class-editcontext) as the drop target.

Each [ListGridRecord](reference_2.md#object-listgridrecord) can be a [PaletteNode](#object-palettenode).

### Groups

- devTools

---
## Attr: ListPalette.canShowFilterEditor

### Description
Option to show filter editor is disabled for listPalettes

**Flags**: IRA

---
## Attr: ListPalette.canSaveSearches

### Description
Option to save searches is disabled for listPalettes

**Flags**: IRA

---
## Class: SetScreenDataTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Sets an embedded screen's [dataContext](classes/Canvas.md#attr-canvasdatacontext) with the [dataContextBinding](#attr-setscreendatataskdatacontextbinding) evaluated in the scope of this task.

### See Also

- [ScreenLoader.setDataContextBinding](classes/ScreenLoader.md#method-screenloadersetdatacontextbinding)
- [Canvas.setDataContext](classes/Canvas.md#method-canvassetdatacontext)

---
## Attr: SetScreenDataTask.dataContextBinding

### Description
A [DataContextBinding](#object-datacontextbinding) to be applied to the screen via [Canvas.setDataContext](classes/Canvas.md#method-canvassetdatacontext).

**Flags**: IR

---
## Class: DoubleItem

*Inherits from:* [FloatItem](#class-floatitem)

### Description
TextForm item for managing a text field that displays a decimal value.

---
## Attr: DoubleItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](classes/FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Method: DoubleItem.getValueAsDouble

### Description
Return the value tracked by this form item as a Double. If the value cannot be parsed to a valid double, null will be returned.

### Returns

`[Double](#type-double)` — the value of this element

### See Also

- [FormItem.getValue](classes/FormItem.md#method-formitemgetvalue)

---
## Class: ProcessSequence

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
An Array of [ProcessElement](classes/ProcessElement.md#class-processelement)s involved in a [Process](classes/Process.md#class-process). A `ProcessSequence` is used to reduce the number of explicit [ProcessElement.ID](classes/ProcessElement.md#attr-processelementid)s that need to be assigned, by creating an implicit next element - the next in the sequence.

A sequence cannot be executed outside of a Process and has no state.

---
## Attr: ProcessSequence.elements

### Description
The [ProcessElement](classes/ProcessElement.md#class-processelement)s in this sequence.

**Flags**: IR

---
## Class: GridSetEditValueTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Sets the edit value of a given field. The targeted row is determined in the following order:

1.  the current edit row
2.  the selected rows
3.  the first row in the grid
4.  a new edit row

### See Also

- [ListGrid.setEditValue](classes/ListGrid_2.md#method-listgridseteditvalue)

---
## Attr: GridSetEditValueTask.value

### Description
Value to assign to [GridSetEditValueTask.targetField](#attr-gridseteditvaluetasktargetfield).

**Flags**: IR

---
## Attr: GridSetEditValueTask.targetField

### Description
Target field in current edit row to be updated

**Flags**: IR

---
## Class: VerticalTabs

*Inherits from:* [TabSet](classes/TabSet.md#class-tabset)

### Description
Simple subclass of [TabSet](classes/TabBar.md#class-tabbar), with vertical orientation and a custom skin style-set.

---
## Attr: VerticalTabs.tabBarPosition

### Description
In this sublass of [TabSet](classes/TabSet.md#class-tabset), the [tabBar](classes/TabSet.md#attr-tabsettabbar) is always vertical, and this setting controls whether it appears on the "left" or "right" of the tab content.

**Flags**: IR

---
## Attr: VerticalTabs.vertical

### Description
This attribute is set to true and cannot be changed in this sublass of [TabSet](classes/TabSet.md#class-tabset).

**Flags**: IR

---
## Class: Timeline

*Inherits from:* [Calendar](classes/Calendar.md#class-calendar)

### Description
Timeline is a trivial subclass of [Calendar](classes/Calendar.md#class-calendar) that configures the Calendar with settings typical for a standalone timeline view: hides the [day](classes/Calendar.md#attr-calendardayview), [week](classes/Calendar.md#attr-calendarweekview) and [month](classes/Calendar.md#attr-calendarmonthview) tabs and the [controls bar](classes/Calendar.md#attr-calendarcontrolsbar) by default.

Note that the [Calendar module](kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) must be loaded to make use of the Timeline class.

---
## Class: IPickTreeItem

*Inherits from:* [PickTreeItem](classes/PickTreeItem.md#class-picktreeitem)

### Description
Subclass of [PickTreeItem](classes/PickTreeItem.md#class-picktreeitem) which shows an [IMenuButton](classes/IMenuButton.md#class-imenubutton) rather than a simple [MenuButton](classes/MenuButton.md#class-menubutton) as it's main button.

---
## Attr: IPickTreeItem.button

### Description
This item is an [AutoChild](#type-autochild) generated [Canvas](classes/Canvas.md#class-canvas) displayed by the IPickTreeItem and is an instance of [ITreeMenuButton](#class-itreemenubutton) by default.

**Flags**: R

---
## Class: DOMGrid

*Inherits from:* [TreeGrid](classes/TreeGrid.md#class-treegrid)

### Description
Provides a tree view of any DOM-compliant structure, such as an XML or HTML document.

---
## Attr: DOMGrid.rootElement

### Description
Root element (or document) to view in the tree.

**Flags**: IRW

---
## Method: DOMGrid.setRootElement

### Description
Set the root element (or document) to view in the tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rootElement | [DOMElement](#type-domelement) | false | — | new root element |

---
## Class: FormEditNewRecordTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Start editing a new record.

### See Also

- [DynamicForm.editNewRecord](classes/DynamicForm.md#method-dynamicformeditnewrecord)

---
## Attr: FormEditNewRecordTask.initialValues

### Description
Initial values for new edit record.

Data values prefixed with "$" will be treated as a [taskInputExpression](kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) excluding "$input" and "$inputRecord" references.

**Flags**: IR

---
## Class: FormEditRecordTask

*Inherits from:* [FormEditNewRecordTask](#class-formeditnewrecordtask)

### Description
Edit a record currently showing in some other component. The source record is obtained as follows:

*   for a ListGrid: the first selected record or, if none is selected, the first record
*   for a DynamicForm: the form values
*   for a DetailViewer: the first record

### See Also

- [DynamicForm.editRecord](classes/DynamicForm.md#method-dynamicformeditrecord)

---
## Attr: FormEditRecordTask.recordSourceComponent

### Description
Component to pull record for editing.

**Flags**: IR

---
## Class: SubmitItem

*Inherits from:* [ButtonItem](classes/ButtonItem.md#class-buttonitem)

### Description
Button that saves the data in the form, by calling [DynamicForm.submit](classes/DynamicForm.md#method-dynamicformsubmit) when clicked. [DynamicForm.submit](classes/DynamicForm.md#method-dynamicformsubmit) for details on how to control what happens when a form is submitted.

### See Also

- [operations](kb_topics/operations.md#kb-topic-operations-overview)

---
## Attr: SubmitItem.title

### Description
SubmitItems show a title of `"Submit"` by default. May be overridden.

**Flags**: IRW

---
## Class: XORGateway

*Inherits from:* [DecisionTask](classes/DecisionTask.md#class-decisiontask)

### Description
Chooses one or another next process element based on AdvancedCriteria applied to [Process.state](classes/Process.md#attr-processstate).

If the AdvancedCriteria evaluate to true, the [nextElement](classes/DecisionTask.md#attr-decisiontasknextelement) is chosen, otherwise the [failureElement](classes/DecisionTask.md#attr-decisiontaskfailureelement).

Note that "XOR" in `XORGateway` means "exclusive or" - only one next element is chosen.

**Deprecated**

---
## Class: FlowLayout

*Inherits from:* [TileLayout](classes/TileLayout.md#class-tilelayout)

### Description
Arranges a set of Canvas components into rows, flowing into available space so that different numbers of components may appear in each row.

`FlowLayout` is essentially just a subclass of [TileLayout](classes/TileLayout.md#class-tilelayout) where the default [TileLayout.layoutPolicy](classes/TileLayout.md#attr-tilelayoutlayoutpolicy) is "flow" instead of "fit".

### See Also

- [TileLayout.layoutPolicy](classes/TileLayout.md#attr-tilelayoutlayoutpolicy)

---
## Class: SelectionTreeMenu

*Inherits from:* [Menu](classes/Menu.md#class-menu)

### Description
A simple subclass of [Menu](classes/Menu.md#class-menu) created by [TreeMenuButton](classes/TreeMenuButton.md#class-treemenubutton). Shows the selected node's path in a custom style.

**Important Note**: this class is not directly usable except for skinning and for subclassing when setting [TreeMenuButton.treeMenuConstructor](classes/TreeMenuButton.md#attr-treemenubuttontreemenuconstructor) on a [TreeMenuButton](classes/TreeMenuButton.md#class-treemenubutton).

---
## Class: WindowMaximizeButton

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.headerControls](classes/Window.md#attr-windowheadercontrols) that the header maximize button should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every header control can be declared as a class.

---
## Class: WindowMinimizeButton

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.headerControls](classes/Window.md#attr-windowheadercontrols) that the header minimize button should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every header control can be declared as a class.

---
## Class: WindowCloseButton

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.headerControls](classes/Window.md#attr-windowheadercontrols) that the header close button should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every header control can be declared as a class.

---
## Class: CancelItem

*Inherits from:* [ButtonItem](classes/ButtonItem.md#class-buttonitem)

### Description
Button that cancels any changes in the form, by calling [DynamicForm.cancelEditing](classes/DynamicForm.md#method-dynamicformcancelediting) when clicked. See [DynamicForm.cancelEditing](classes/DynamicForm.md#method-dynamicformcancelediting) for details on what happens when a form editing is cancelled.

---
## Attr: CancelItem.title

### Description
CancelItems show a title of `"Cancel"` by default. May be overridden.

**Flags**: IRW

---
## Class: WindowFooterSpacer

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.footerControls](classes/Window.md#attr-windowfootercontrols) that the footer spacer should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every footer control can be declared as a class.

---
## Class: WindowHeaderLabel

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.headerControls](classes/Window.md#attr-windowheadercontrols) that the header label should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every header control can be declared as a class.

---
## Class: WindowHeaderIcon

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.headerControls](classes/Window.md#attr-windowheadercontrols) that the header icon should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every header control can be declared as a class.

---
## Class: WindowResizer

### Description
Marker class available in our [React JSX support](kb_topics/reactSupport.md#kb-topic-using-smartclient-with-react) and [Component XML](kb_topics/componentXML.md#kb-topic-component-xml) to indicate within the [Window.footerControls](classes/Window.md#attr-windowfootercontrols) that the footer resizer should be rendered. Note that an instance of this class is never drawn, and it's only made available in these cases to allow for a simple syntax where every footer control can be declared as a class.

---
## Class: FormSetFieldValueTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Put a value in just one field of a form.

### See Also

- [DynamicForm.setValue](classes/DynamicForm.md#method-dynamicformsetvalue)

---
## Attr: FormSetFieldValueTask.targetField

### Description
Field to assign new value.

**Flags**: IR

---
## Attr: FormSetFieldValueTask.value

### Description
Value to assign to [FormSetFieldValueTask.targetField](#attr-formsetfieldvaluetasktargetfield).

**Flags**: IR

---
## Class: ViewFileItem

*Inherits from:* [FileItem](classes/FileItem.md#class-fileitem)

### Description
A simple subclass of [FileItem](classes/FileItem.md#class-fileitem) for displaying the contents of "imageFile" fields in DynamicForms.

Displays one of two UIs, according to the value of [showFileInline](classes/FileItem.md#attr-fileitemshowfileinline). If showFileInline is false, this Item displays the View and Download icons and the filename. Otherwise, it streams the image-file and displays it inline.

### Groups

- upload

---
## Class: SecondaryButton

*Inherits from:* [Button](classes/Button.md#class-button)

### Description
A simple [Button](classes/Button.md#class-button) subclass with a de-emphasized appearance, applied by a separate [CSS style-series](classes/StatefulCanvas.md#attr-statefulcanvasbasestyle) named "secondaryButton".

`SecondaryButton` is mostly intended for skinning purposes and the framework doesn't automatically use it anywhere - you should create instances directly if you want a secondary, de-emphasized appearance for buttons.

---
## Class: ITreeMenuButton

*Inherits from:* [TreeMenuButton](classes/TreeMenuButton.md#class-treemenubutton)

### Description
Button used to display a hierarchical Menu group for representing / selecting tree data. This is derived from the [MenuButton](classes/MenuButton.md#class-menubutton) and is [StretchImgButton](classes/StretchImgButton.md#class-stretchimgbutton) based.

_**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

---
## Class: AIAssistItem

*Inherits from:* [TextItem](classes/TextItem.md#class-textitem)

### Description
FormItem that can be bound to a [rootCanvas](classes/Canvas.md#class-canvas) and allows a user to ask the SmartClient AI system about that part of the UI, without directly showing the AI Assistant window.

---
## Attr: AIAssistItem.rootCanvas

### Description
Limits the UI available to the AI when it considers your questions and responds.

By default, the AI has access to the entire UI.

### Groups

- ai

**Flags**: IRW

---
## Class: NativeCheckboxItem

*Inherits from:* [FormItem](classes/FormItem.md#class-formitem)

### Description
A checkbox for manipulating 2-valued fields based on the native checkbox element.

---
## Attr: NativeCheckboxItem.showLabel

### Description
Should we show the label text next to the checkbox item.

**Flags**: IRW

---
## Attr: NativeCheckboxItem.textBoxStyle

### Description
Base CSS class applied to this item's title text (rendered next to the checkbox element).

### Groups

- appearance

**Flags**: IRW

---
## Class: MockupElement

*Inherits from:* [Img](classes/Img.md#class-img)

### Description
MockupElements are produced by the [Balsamiq Mockup Importer](kb_topics/balsamiqImport.md#kb-topic-mockup-importer) as placeholders for Balsamiq controls that cannot be meaningfully translated to SmartClient controls (such as the big red X markup control).

MockupElement is just an instance of Img that uses .png files stored in the tools/mockups folder.

MockupElement is not intended to be included in any final applications.

---
## Class: TilePalette

*Inherits from:* [TileGrid](classes/TileGrid.md#class-tilegrid)

### Description
A [TileGrid](classes/TileGrid.md#class-tilegrid) that implements the [Palette](#interface-palette) behavior, so it can be used as the source for drag and drop instantiation of components when combined with an [EditContext](classes/EditContext.md#class-editcontext) as the drop target.

Each [TileGrid.tile](classes/TileGrid.md#attr-tilegridtile) can be a [PaletteNode](#object-palettenode).

### Groups

- devTools

---
## Class: InlineWindow

*Inherits from:* [Window](classes/Window.md#class-window)

### Description
This class is a synonym for Window that can be used to make intent clearer. It is used by some development tools for that purpose.

---
## Attr: InlineWindow.editProxyConstructor

### Description
Default class used to construct the [EditProxy](classes/EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](classes/Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Class: ToolStripResizer

*Inherits from:* [ImgSplitbar](classes/ImgSplitbar.md#class-imgsplitbar)

### Description
Simple subclass of ImgSplitbar with appearance appropriate for a ToolStrip resizer.

---
## Attr: ToolStripResizer.hSrc

### Description
Image for horizontal resizer for a vertical Toolstrip

**Flags**: IRW

---
## Attr: ToolStripResizer.vSrc

### Description
Image for resizer

**Flags**: IRW

---
## Attr: ToolStripResizer.skinImgDir

### Description
Path to resizer image.

**Flags**: IR

---
## Class: GridExportClientDataTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Export data currently shown in a grid keeping all grid-specific formatting.

### See Also

- [ListGrid.exportClientData](classes/ListGrid_2.md#method-listgridexportclientdata)

---
## Attr: GridExportClientDataTask.requestProperties

### Description
Additional properties to set on the DSRequest that will be issued to perform client-side export.

**Flags**: IR

---
## Class: ToggleItem

*Inherits from:* [CanvasItem](classes/CanvasItem.md#class-canvasitem)

### Description
FormItem that uses a [ToggleSwitch](classes/ToggleSwitch.md#class-toggleswitch) component to present an interface for picking from either a continuous range or a range with a small number of discrete values.

---
## Attr: ToggleItem.toggleConstructor

### Description
Constructor class for this item's [ToggleSwitch](classes/ToggleSwitch.md#class-toggleswitch).

**Flags**: IR

---
## Class: EndProcessTask

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Task that ends a workflow. This task is not necessary to end a workflow - having a task execute with no [ProcessElement.nextElement](classes/ProcessElement.md#attr-processelementnextelement) is sufficient to end the workflow.

This task is primarily used in the workflow editor to render a "no-op" task or as an explicit visual marker for the end of workflow.

---
## Class: IButton

*Inherits from:* [Button](classes/Button.md#class-button)

### Description
The IButton widget class is a class that implements the same APIs as the [Button](classes/Button.md#class-button) class. Depending on the current skin, `IButton`s may be on the [StretchImgButton](classes/StretchImgButton.md#class-stretchimgbutton) component, which renders via images, or may be based on the [Button](classes/Button.md#class-button) component, which renders via CSS styles.

---
## Class: FormDisableFieldTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Disable or enable a form field.

### See Also

- [FormItem.setDisabled](classes/FormItem.md#method-formitemsetdisabled)

**Deprecated**

---
## Attr: FormDisableFieldTask.targetField

### Description
Field to show/hide.

**Flags**: IR

---
## Attr: FormDisableFieldTask.disable

### Description
Should the target form item be disabled?

**Flags**: IR

---
## Class: FormEditProxy

*Inherits from:* [CanvasEditProxy](#class-canvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [DynamicForms](classes/DynamicForm.md#class-dynamicform) when editMode is enabled.

### Groups

- devTools

---
## Attr: FormEditProxy.selectItemsMode

### Description
Controls which parts of a [FormItem](classes/FormItem.md#class-formitem) respond to a click and result in selecting the component.

**Flags**: IRW

---
## Class: GridViewSelectedDataTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
View a record currently selected in some other component. Ignored if nothing is selected.

### See Also

- [DetailViewer.viewSelectedData](classes/DetailViewer.md#method-detailviewerviewselecteddata)

---
## Attr: GridViewSelectedDataTask.selectionComponentId

### Description
Component to pull record for viewing.

**Flags**: IR

---
## Class: GridExportDataTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Export data currently shown in a grid.

### See Also

- [DataBoundComponent.exportData](classes/DataBoundComponent.md#method-databoundcomponentexportdata)

---
## Attr: GridExportDataTask.requestProperties

### Description
Additional properties to set on the DSRequest that will be issued to perform server-side export.

**Flags**: IR

---
## Class: FormEditSelectedTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Edit a record currently selected in some other component. If nothing is selected a new record is edited.

### See Also

- [DynamicForm.editRecord](classes/DynamicForm.md#method-dynamicformeditrecord)

---
## Attr: FormEditSelectedTask.selectionComponentId

### Description
Component to pull record for editing.

**Flags**: IR

---
## Class: MenuPalette

*Inherits from:* [Menu](classes/Menu.md#class-menu)

### Description
A Menu that implements the [Palette](#interface-palette) behavior, so it can be used as the source for drag and drop instantiation of components when combined with an [EditContext](classes/EditContext.md#class-editcontext) as the drop target.

Each [MenuItem](reference_2.md#object-menuitem) can be a [PaletteNode](#object-palettenode).

### Groups

- devTools

---
## Class: UserConfirmationGateway

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Chooses one or another next process element based on confirmation of a message shown to user.

If the user clicks OK, the [nextElement](classes/DecisionTask.md#attr-decisiontasknextelement) is chosen, otherwise the choice is [failureElement](classes/DecisionTask.md#attr-decisiontaskfailureelement).

**Deprecated**

---
## Class: GridTransferDataTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Transfer selected records from one grid to another.

### See Also

- [ListGrid.transferSelectedData](classes/ListGrid_2.md#method-listgridtransferselecteddata)

---
## Attr: GridTransferDataTask.sourceComponent

### Description
Source component from which the record(s) will be transferred.

**Flags**: IR

---
## Class: GridSaveAllEditsTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Save all changes in a grid which has auto-saving disabled. Before the save, any pending edit rows are saved to the grid.

### See Also

- [ListGrid.endEditing](classes/ListGrid_2.md#method-listgridendediting)
- [ListGrid.saveAllEdits](classes/ListGrid_2.md#method-listgridsavealledits)

---
## Class: SimpleTabButton

*Inherits from:* [Button](classes/Button.md#class-button)

### Description
Simple subclass of [Button](classes/Button.md#class-button) used for tabs in a [TabSet](classes/TabSet.md#class-tabset) if [TabSet.useSimpleTabs](classes/TabSet.md#attr-tabsetusesimpletabs) is true. See also [TabSet.simpleTabButtonConstructor](classes/TabSet.md#attr-tabsetsimpletabbuttonconstructor).

---
## Class: BuildUIViaAIProgressDialog

*Inherits from:* [BuildViaAIProgressDialog](#class-buildviaaiprogressdialog)

### Description
—

---
## Attr: BuildUIViaAIProgressDialog.title

### Description
Title for this Window, shown if [showTitle](classes/Window.md#attr-windowshowtitle) is true in the [header](classes/Window.md#attr-windowheader) (if drawn).

### Groups

- i18nMessages

**Flags**: IRW

---
## Class: FilterViaAIProgressDialog

*Inherits from:* [BuildViaAIProgressDialog](#class-buildviaaiprogressdialog)

### Description
—

---
## Attr: FilterViaAIProgressDialog.title

### Description
Title for this Window, shown if [showTitle](classes/Window.md#attr-windowshowtitle) is true in the [header](classes/Window.md#attr-windowheader) (if drawn).

### Groups

- i18nMessages

**Flags**: IRW

---
## Class: HiliteViaAIProgressDialog

*Inherits from:* [BuildViaAIProgressDialog](#class-buildviaaiprogressdialog)

### Description
—

---
## Attr: HiliteViaAIProgressDialog.title

### Description
Title for this Window, shown if [showTitle](classes/Window.md#attr-windowshowtitle) is true in the [header](classes/Window.md#attr-windowheader) (if drawn).

### Groups

- i18nMessages

**Flags**: IRW

---
## Class: AutoFitTextAreaItem

*Inherits from:* [TextAreaItem](classes/TextAreaItem.md#class-textareaitem)

### Description
Class for editable multi-line text areas (uses HTML ``<TEXTAREA>`` object) automatically expands to accommodate its content

---
## Attr: AutoFitTextAreaItem.maxHeight

### Description
If specified, the autoFitTextArea will not grow taller than this height

**Flags**: IRW

---
## Class: RadioItem

*Inherits from:* [NativeCheckboxItem](#class-nativecheckboxitem)

### Description
Form item representing a member of a radio group, subclassed from [NativeCheckboxItem](#class-nativecheckboxitem). RadioItems items are created and managed automatically by [RadioGroupItem](classes/RadioGroupItem.md#class-radiogroupitem) instances and should not be instantiated directly.

---
## Class: HStack

*Inherits from:* [Layout](classes/Layout.md#class-layout)

### Description
A subclass of Layout that simply stacks members on the horizontal axis without trying to manage their width. On the vertical axis, any members that do not have explicit heights will be sized to match the height of the stack.

### See Also

- [Layout.hPolicy](classes/Layout.md#attr-layouthpolicy)

---
## Class: Tutorial

*Inherits from:* [Tour](classes/Tour.md#class-tour)

### Description
The Tutorial class is a specialized version of the Tour class with [Tour.mode](classes/Tour.md#attr-tourmode) set to "tutorial".

---
## Attr: Tutorial.mode

### Description
The tour mode allows step configuration to be simplified by using the context to apply appropriate defaults.

**Flags**: IRW

---
## Class: IntegerItem

*Inherits from:* [TextItem](classes/TextItem.md#class-textitem)

### Description
FormItem intended for inputting integer numbers.

---
## Attr: IntegerItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](classes/FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Class: LayoutSpacer

*Inherits from:* [Canvas](classes/Canvas.md#class-canvas)

### Description
Add a spacer to a [Layout](classes/Layout.md#class-layout) that takes up space just like a normal member, without actually drawing anything. A `LayoutSpacer` is semantically equivalent to using an empty canvas, but higher performance for this particular use case.

---
## Class: AIWindow

*Inherits from:* [Window](classes/Window.md#class-window)

### Description
Window subclass used by the "Filter via AI…" and "Hilite via AI…" [ListGrid](classes/ListGrid_1.md#class-listgrid) header context menu items to allow the user to filter or hilite by a natural language description of a filter or hilite, respectively.

---
## Class: QuartzManager

### Description
A simple user interface for managing scheduled jobs via [Quartz DataSource](kb_topics/quartzAdapters.md#kb-topic-quartz-datasources) adapters, as seen in the Scheduler tab of the [Admin Console](kb_topics/adminConsole.md#kb-topic-admin-console). Exercise caution when exposing any such feature to end users.

---
## Class: ToolStripMenuButton

*Inherits from:* [MenuButton](classes/MenuButton.md#class-menubutton)

### Description
Simple subclass of MenuButton with appearance appropriate for a ToolStrip menu button. Can be used to create an icon-only menu button, and icon with text, or a text only button by setting the icon and title attibutes as required.

---
## Class: AutoFitButton

*Inherits from:* [Button](classes/Button.md#class-button)

### Description
A button that automatically sizes to the length of its title. Implemented via the [StatefulCanvas.autoFit](classes/StatefulCanvas.md#attr-statefulcanvasautofit) property.

### See Also

- [Button](classes/Button.md#class-button)

**Deprecated**

---
## Class: SavedSearchItemEditProxy

*Inherits from:* [SelectItemEditProxy](classes/SelectItemEditProxy.md#class-selectitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [SavedSearchItems](classes/SavedSearchItem.md#class-savedsearchitem) when editMode is enabled.

### Groups

- devTools

---
## Class: RadioGroupItemEditProxy

*Inherits from:* [SelectItemEditProxy](classes/SelectItemEditProxy.md#class-selectitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [RadioGroupItems](classes/RadioGroupItem.md#class-radiogroupitem) when editMode is enabled.

### Groups

- devTools

---
## Class: ToolStripButton

*Inherits from:* [Button](classes/Button.md#class-button)

### Description
Simple subclass of Button with appearance appropriate for a ToolStrip button. Can be used to create an icon-only button, and icon with text, or a text only button by setting the icon and title attributes as required.

---
## Class: TextAreaItemEditProxy

*Inherits from:* [TextItemEditProxy](classes/TextItemEditProxy.md#class-textitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [TextAreaItems](classes/TextAreaItem.md#class-textareaitem) when editMode is enabled.

### Groups

- devTools

---
## Class: ToolStripSpacer

*Inherits from:* [LayoutSpacer](#class-layoutspacer)

### Description
Simple subclass of LayoutSpacer with appearance appropriate for a ToolStrip spacer

---
## Attr: ToolStripSpacer.space

### Description
Size of spacer. If not specified, spacer fills remaining space.

**Flags**: IR

---
## Class: AISortProgressDialog

*Inherits from:* [Window](classes/Window.md#class-window)

### Description
Dialog informing user of the progress when doing an AI sort. When the AI sort field has been populated for all records, the dialog will auto-dismiss and the grid will be sorted by the newly added field.

---
## Class: ToolbarItemEditProxy

*Inherits from:* [FormItemEditProxy](classes/FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [ToolbarItems](classes/ToolbarItem.md#class-toolbaritem) when editMode is enabled.

### Groups

- devTools

---
## Class: LayoutResizeBarEditProxy

*Inherits from:* [EditProxy](classes/EditProxy.md#class-editproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [LayoutResizeBar](classes/LayoutResizeBar.md#class-layoutresizebar) objects when editMode is enabled.

### Groups

- devTools

---
## Class: SectionItemEditProxy

*Inherits from:* [TextItemEditProxy](classes/TextItemEditProxy.md#class-textitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [SectionItem](classes/SectionItem.md#class-sectionitem) when editMode is enabled.

### Groups

- devTools

---
## Class: XMLSyntaxHiliter

*Inherits from:* [SyntaxHiliter](#class-syntaxhiliter)

### Description
Regular expression-based source code colorizer for XML source.

_NOTE: This class exists only for use with the SmartClient Feature Explorer and SmartGWT Showcases and cannot be used in any other environment._

---
## Class: JSSyntaxHiliter

*Inherits from:* [SyntaxHiliter](#class-syntaxhiliter)

### Description
Regular expression-based source code colorizer for JS source.

_NOTE: This class exists only for use with the SmartClient Feature Explorer and SmartGWT Showcases and cannot be used in any other environment._

---
## Class: RibbonButtonEditProxy

*Inherits from:* [StatefulCanvasEditProxy](#class-statefulcanvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [RibbonButton](classes/RibbonButton.md#class-ribbonbutton) objects when editMode is enabled.

### Groups

- devTools

---
## Class: TextMenuButton

*Inherits from:* [MenuButton](classes/MenuButton.md#class-menubutton)

### Description
A simple subclass of [MenuButton](classes/MenuButton.md#class-menubutton) that uses a separate CSS class to render as just stateful text and menu-icon, without background, borders or shadows.

---
## Class: BlurbItemEditProxy

*Inherits from:* [TextItemEditProxy](classes/TextItemEditProxy.md#class-textitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [BlurbItems](classes/BlurbItem.md#class-blurbitem) when editMode is enabled.

### Groups

- devTools

---
## Class: ToolStripGroup

*Inherits from:* [RibbonGroup](classes/RibbonGroup.md#class-ribbongroup)

### Description
A simple subclass of [RibbonGroup](classes/RibbonGroup.md#class-ribbongroup), which groups other controls for use in [ribbon-bars](classes/RibbonBar.md#class-ribbonbar).

**Deprecated**

---
## Class: ValuesManagerEditProxy

*Inherits from:* [EditProxy](classes/EditProxy.md#class-editproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [ValuesManager](classes/ValuesManager.md#class-valuesmanager) objects when editMode is enabled.

### Groups

- devTools

---
## Class: FileItemEditProxy

*Inherits from:* [FormItemEditProxy](classes/FormItemEditProxy.md#class-formitemeditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [FileItems](classes/FileItem.md#class-fileitem) when editMode is enabled.

### Groups

- devTools

---
## Class: ResetPasswordTask

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Show user password reset dialog by opening the [Auth.resetPasswordURL](classes/Authentication.md#classattr-authenticationresetpasswordurl) in another tab or window.

---
## Class: OpenFinWindow

*Inherits from:* [RemoteWindow](classes/RemoteWindow.md#class-remotewindow)

### Description
Provides a SmartClient wrapper around an [OpenFin](https://developers.openfin.co/of-docs/docs) window.

### Groups

- experimental

### See Also

- [OpenFin](#class-openfin)

---
## Class: GridDiscardAllEditsTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Discard all changes in a grid which has auto-saving disabled.

### See Also

- [ListGrid.discardAllEdits](classes/ListGrid_2.md#method-listgriddiscardalledits)

---
## Class: HiddenPalette

### Description
A Palette with no visible representation that handles programmatic creation of components.

### Groups

- devTools

---
## Attr: HiddenPalette.data

### Description
A list of [PaletteNodes](#object-palettenode) for component creation.

**Flags**: IR

---
## Class: ScreenLoaderEditProxy

*Inherits from:* [CanvasEditProxy](#class-canvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [ScreenLoader](classes/ScreenLoader.md#class-screenloader) objects when editMode is enabled.

### Groups

- devTools

---
## Class: SectionStackEditProxy

*Inherits from:* [LayoutEditProxy](#class-layouteditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [SectionStack](classes/SectionStack.md#class-sectionstack) objects when editMode is enabled.

### Groups

- devTools

---
## Class: HandPlacedForm

*Inherits from:* [DynamicForm](classes/DynamicForm.md#class-dynamicform)

### Description
This class is a DynamicForm with the default [itemLayout](classes/DynamicForm.md#attr-dynamicformitemlayout) property set to "absolute".

Another synonym is AbsoluteForm.

---
## Class: HandPlacedContainerEditProxy

*Inherits from:* [EditProxy](classes/EditProxy.md#class-editproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Canvas](classes/Canvas.md#class-canvas) objects when editMode is enabled.

### Groups

- devTools

---
## Class: SectionStackSectionEditProxy

*Inherits from:* [LabelEditProxy](#class-labeleditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [SectionStackSection](#object-sectionstacksection) objects when editMode is enabled.

### Groups

- devTools

---
## Class: ColorPickerItem

*Inherits from:* [ColorItem](classes/ColorItem.md#class-coloritem)

### Description
Form item for selecting a color via a pop-up [ColorPicker](classes/ColorPicker.md#class-colorpicker). This is an alias of [ColorItem](classes/ColorItem.md#class-coloritem).

---
## Class: ResetItem

*Inherits from:* [ButtonItem](classes/ButtonItem.md#class-buttonitem)

### Description
Button that resets the form to default values, by calling `DynamicForm.resetValues()` If you define a click handler on this item, you can return false to cancel the reset.

---
## Class: SplitPaneEditProxy

*Inherits from:* [LayoutEditProxy](#class-layouteditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [SplitPane](classes/SplitPane.md#class-splitpane) objects when editMode is enabled.

### Groups

- devTools

---
## Class: HandPlacedContainer

*Inherits from:* [Canvas](classes/Canvas.md#class-canvas)

### Description
This class is a synonym for Canvas that can be used to make intent clearer. It is used by some development tools for that purpose.

Another synonym is AbsoluteContainer.

---
## Class: TileGridEditProxy

*Inherits from:* [LayoutEditProxy](#class-layouteditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [TileGrid](classes/TileGrid.md#class-tilegrid) components when editMode is enabled.

### Groups

- devTools

---
## Class: OpenFin

### Description
Contains [OpenFin](https://developers.openfin.co/of-docs/docs)\-specific code to implement [MultiWindow](classes/MultiWindow.md#class-multiwindow) for OpenFin via special calls to the OpenFin Application API.

### Groups

- experimental

---
## Class: ImgEditProxy

*Inherits from:* [StatefulCanvasEditProxy](#class-statefulcanvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [Img](classes/Img.md#class-img) objects when editMode is enabled.

### Groups

- devTools

---
## Class: DrawPaneEditProxy

*Inherits from:* [CanvasEditProxy](#class-canvaseditproxy)

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [DrawPanes](classes/DrawPane.md#class-drawpane) when editMode is enabled.

### Groups

- devTools

---
## Class: LogOutTask

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Logs out the current user by opening the [Auth.logOutURL](classes/Authentication.md#classattr-authenticationlogouturl) in another tab or window.

---
## Class: AskForValueTask

*Inherits from:* [UserConfirmationTask](classes/UserConfirmationTask.md#class-userconfirmationtask)

### Description
Ask the user to input a value.

---
## Attr: AskForValueTask.defaultValue

### Description
Default value.

**Flags**: IR

---
## Class: FormClearValuesTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Clear form values and errors.

### See Also

- [DynamicForm.clearValues](classes/DynamicForm.md#method-dynamicformclearvalues)

---
## Class: FormResetValuesTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Revert unsaved changes in a form.

### See Also

- [DynamicForm.reset](classes/DynamicForm.md#method-dynamicformreset)

---
## Class: TriplePane

*Inherits from:* [SplitPane](classes/SplitPane.md#class-splitpane)

### Description
This class is a synonym for SplitPane that can be used to make intent clearer. It is used by some development tools for that purpose.

---
## Class: ScrollThumb

*Inherits from:* [StretchImg](classes/StretchImg.md#class-stretchimg)

### Description
Class used for the draggable "thumb" of a scrollbar. Do not use directly; this class is documented only for skinning purposes.

---
## Class: StartTransactionTask

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Starts queuing all DataSource operations so they can be sent to the server all together as a transaction.

---
## Class: FixedSpacer

*Inherits from:* [LayoutSpacer](#class-layoutspacer)

### Description
This class is a synonym for LayoutSpacer that can be used to make intent clearer. It is used by some development tools for that purpose.

---
## Class: FlexSpacer

*Inherits from:* [LayoutSpacer](#class-layoutspacer)

### Description
This class is a synonym for LayoutSpacer that can be used to make intent clearer. It is used by some development tools for that purpose.

---
## Class: SendTransactionTask

*Inherits from:* [ProcessElement](classes/ProcessElement.md#class-processelement)

### Description
Sends any currently queued DataSource operations, as a single transactional request to the server.

---
## Class: ShowComponentTask

*Inherits from:* [ComponentTask](classes/ComponentTask.md#class-componenttask)

### Description
Show a currently hidden component.

### See Also

- [Canvas.show](classes/Canvas.md#method-canvasshow)

---
## Class: RibbonGroupEditProxy

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [RibbonGroup](classes/RibbonGroup.md#class-ribbongroup) objects when editMode is enabled.

### Groups

- devTools

---
## Class: ToolStripSeparatorEditProxy

### Description
[EditProxy](classes/EditProxy.md#class-editproxy) that handles [ToolStripSeparator](#class-toolstripseparator) objects when editMode is enabled.

### Groups

- devTools

---
## Class: PropertySheet

*Inherits from:* [DynamicForm](classes/DynamicForm.md#class-dynamicform)

### Description
Editor with a minimalist appearance, tuned for editing large numbers of properties in a constrained space.

---
## Class: IconButton

*Inherits from:* [RibbonButton](classes/RibbonButton.md#class-ribbonbutton)

### Description
A simple subclass of [RibbonButton](classes/RibbonButton.md#class-ribbonbutton).

**Deprecated**

---
## Class: DSRemoveTask

*Inherits from:* [ServiceTask](classes/ServiceTask.md#class-servicetask)

### Description
A [ServiceTask](classes/ServiceTask.md#class-servicetask) configured to perform a remove.

---
## Class: DSUpdateTask

*Inherits from:* [ServiceTask](classes/ServiceTask.md#class-servicetask)

### Description
A [ServiceTask](classes/ServiceTask.md#class-servicetask) configured to perform a update.

---
## Class: Auth

*Inherits from:* [Authentication](classes/Authentication.md#class-authentication)

### Description
Synonym for the [Authentication](classes/Authentication.md#class-authentication) class

---
## Class: DSFetchTask

*Inherits from:* [ServiceTask](classes/ServiceTask.md#class-servicetask)

### Description
A [ServiceTask](classes/ServiceTask.md#class-servicetask) configured to perform a fetch.

---
## Class: PasswordItem

*Inherits from:* [TextItem](classes/TextItem.md#class-textitem)

### Description
FormItem for password fields, where text input by the user should not be shown in readable text.

---
## Class: DSAddTask

*Inherits from:* [ServiceTask](classes/ServiceTask.md#class-servicetask)

### Description
A [ServiceTask](classes/ServiceTask.md#class-servicetask) configured to perform an add.

---
## Class: VerticalTabBar

*Inherits from:* [TabBar](classes/TabBar.md#class-tabbar)

### Description
Simple subclass of [TabBar](classes/TabBar.md#class-tabbar), with customized buttons.

---
## Class: DrawBlockConnector

*Inherits from:* [DrawCurve](classes/DrawCurve.md#class-drawcurve)

### Description
DrawItem subclass to render multi-segment, orthogonal-routing paths.

---
## Class: IconMenuButton

*Inherits from:* [IconButton](#class-iconbutton)

### Description
A simple subclass of [RibbonMenuButton](#class-ribbonmenubutton).

**Deprecated**

---
## Class: BooleanItem

*Inherits from:* [FormItem](classes/FormItem.md#class-formitem)

### Description
Boolean form item, implemented with customizable checkbox images

---
## Class: DateGrid

*Inherits from:* [ListGrid](classes/ListGrid_1.md#class-listgrid)

### Description
A ListGrid subclass that manages calendar views.

---
## Class: DataPathItem

*Inherits from:* [TextItem](classes/TextItem.md#class-textitem)

### Description
TextItem subclass for managing a DataPath

---
## Class: React

### Description
Container for various helper methods used by our React wrapper classes.

---
## KB Topic: ancestry

### Description
Parent/child relationships

### Related

- [DisplayNodeType](reference_2.md#type-displaynodetype)

---
## KB Topic: Array Math

### Description
Math operations on entire Arrays at once

### Related

- [Array.intersect](classes/Array.md#method-arrayintersect)
- [Array.max](classes/Array.md#method-arraymax)
- [Array.min](classes/Array.md#method-arraymin)
- [Array.sum](classes/Array.md#method-arraysum)
- [Array.and](classes/Array.md#method-arrayand)
- [Array.or](classes/Array.md#method-arrayor)
- [List.intersect](classes/List.md#method-listintersect)

---
## KB Topic: baseLine

### Description
The baseLine is StretchImg that is placed along the edge of the TabBar that borders on the pane, occluding the pane's actual border but matching it exactly. The selected tab is in front of the baseLine, and the rest are behind it.

### Related

- [TabBar.baseLineThickness](classes/TabBar.md#attr-tabbarbaselinethickness)
- [TabBar.baseLineSrc](classes/TabBar.md#attr-tabbarbaselinesrc)
- [TabBar.baseLineCapSize](classes/TabBar.md#attr-tabbarbaselinecapsize)

---
## KB Topic: Component Binding

### Description
Properties that control how a [DataBoundComponent](#interface-databoundcomponent) binds to this data source.

### Related

- [DataSourceField.title](classes/DataSourceField.md#attr-datasourcefieldtitle)
- [DataSourceField.canView](classes/DataSourceField.md#attr-datasourcefieldcanview)
- [DataSourceField.canEdit](classes/DataSourceField.md#attr-datasourcefieldcanedit)
- [DataSourceField.canSave](classes/DataSourceField.md#attr-datasourcefieldcansave)
- [DataSourceField.editorType](classes/DataSourceField.md#attr-datasourcefieldeditortype)
- [DataSourceField.readOnlyEditorType](classes/DataSourceField.md#attr-datasourcefieldreadonlyeditortype)
- [DataSourceField.filterEditorType](classes/DataSourceField.md#attr-datasourcefieldfiltereditortype)
- [DataSourceField.hidden](classes/DataSourceField.md#attr-datasourcefieldhidden)
- [DataSourceField.ignore](classes/DataSourceField.md#attr-datasourcefieldignore)
- [DataSourceField.detail](classes/DataSourceField.md#attr-datasourcefielddetail)

---
## KB Topic: CompoundFormItem_skinning

### Description
When skinning basic FormItems like SelectItem and TextItem, consider that compound form items like DateItem and ComboBox reuse simpler items like SelectItem and TextItem, so adding a border to SelectItem would also apply a border to each select item within DateItem.  
To avoid such side-effects, if you want to add styling to all SelectItems used in your application, you can create an application-specific subclass like MySelectItem and apply properties there.

---
## KB Topic: cues

### Description
Visual hints for the user that something can be done to this object

### Related

- [Cursor](#type-cursor)
- [Canvas.setOpacity](classes/Canvas.md#method-canvassetopacity)
- [Canvas.setCursor](classes/Canvas.md#method-canvassetcursor)
- [Canvas.cursor](classes/Canvas.md#attr-canvascursor)
- [Canvas.disabledCursor](classes/Canvas.md#attr-canvasdisabledcursor)
- [Canvas.noDropCursor](classes/Canvas.md#attr-canvasnodropcursor)
- [Canvas.opacity](classes/Canvas.md#attr-canvasopacity)
- [Canvas.contextMenu](classes/Canvas.md#attr-canvascontextmenu)
- [Canvas.menuConstructor](classes/Canvas.md#attr-canvasmenuconstructor)
- [DrawItem.contextMenu](classes/DrawItem.md#attr-drawitemcontextmenu)
- [FormItemIcon.cursor](classes/FormItemIcon.md#attr-formitemiconcursor)
- [FormItemIcon.disabledCursor](classes/FormItemIcon.md#attr-formitemicondisabledcursor)
- [Button.iconCursor](classes/Button.md#attr-buttoniconcursor)
- [Button.disabledIconCursor](classes/Button.md#attr-buttondisablediconcursor)

---
## KB Topic: Data Changes

### Description
Operations that change the Array

---
## KB Topic: SmartClient Reference Overview

### Description
Welcome to the SmartClient Reference. Click on a topic in the tree on the left to show documentation in this pane or type some search terms into the search box in the upper left and hit Enter.

---
## KB Topic: drawing

### Description
Rendering an object on the page.

### Related

- [Canvas.isDrawn](classes/Canvas.md#method-canvasisdrawn)
- [Canvas.getInnerHTML](classes/Canvas.md#method-canvasgetinnerhtml)
- [Canvas.draw](classes/Canvas.md#method-canvasdraw)
- [Canvas.isDirty](classes/Canvas.md#method-canvasisdirty)
- [Canvas.markForRedraw](classes/Canvas.md#method-canvasmarkforredraw)
- [Canvas.redraw](classes/Canvas.md#method-canvasredraw)
- [FormItem.getFieldName](classes/FormItem.md#method-formitemgetfieldname)
- [FormItem.getTitle](classes/FormItem.md#method-formitemgettitle)
- [FormItem.isDrawn](classes/FormItem.md#method-formitemisdrawn)
- [ListGrid.markForRedraw](classes/ListGrid_2.md#method-listgridmarkforredraw)
- [Canvas.autoDraw](classes/Canvas.md#attr-canvasautodraw)
- [Canvas.redrawOnResize](classes/Canvas.md#attr-canvasredrawonresize)

---
## KB Topic: elements

### Description
Manipulating native form elements

### Related

- [DynamicForm.setItems](classes/DynamicForm.md#method-dynamicformsetitems)
- [DynamicForm.setFields](classes/DynamicForm.md#method-dynamicformsetfields)
- [DynamicForm.getFields](classes/DynamicForm.md#method-dynamicformgetfields)
- [DynamicForm.getItems](classes/DynamicForm.md#method-dynamicformgetitems)

---
## KB Topic: eventBubbling

### Description
Event "bubbling" refers to the propagation of an event up the containment hierachy, so that it's fired on each widget in the chain, unless canceled. See [EventHandler](classes/EventHandler.md#class-eventhandler) for further discussion.

---
## KB Topic: Flag Abbreviations

### Description
*   **I**: "initializable": property can be initialized. For a simple [Object](#type-object), it means the property is valid to define on the Object. For a [Class](classes/Class.md#class-class) such as [Canvas](classes/Canvas.md#class-canvas), this means a property can be provided in the [Object](#type-object) passed to [Class.create](classes/Class.md#classmethod-classcreate).
*   **R**: "readable": property be read. If a getter method exists, it must be called.
*   **W**: "writable": property can be written to after initialization. If a setter method exists, it must be called. If no setter method exists, [setProperty()](classes/Class.md#method-classsetproperty) must be called.
*   **A**: "advanced": this property or method is meant for advanced use cases. If you are considering using an API marked "advanced" and your use case is simple or common, this is a hint that you may have missed a simpler approach

---
## KB Topic: Values Manager

### Description
Values Manager references.

### Related

- [DynamicForm.setValuesManager](classes/DynamicForm.md#method-dynamicformsetvaluesmanager)
- [DynamicForm.valuesManager](classes/DynamicForm.md#attr-dynamicformvaluesmanager)

---
## KB Topic: Google Application Engine (GAE)

### Description
Google App Engine (GAE) is a platform-as-a-service (PaaS) offering from Google, which supports cloud deployment of applications written in Java and other languages, as well as SQL or JPA access to highly scalable storage (both Google CloudSQL and BigTable-based solutions).

SmartClient applications, including those based on the SmartClient Server Framework, can be deployed to GAE and can integrate with Google CloudSQL either via SQLDataSource or via JPA, and can also use Google's BigTable-based storage via JPA.

For further information, setup instructions and example configuration, see our [public wiki](http://wiki.smartclient.com/display/Main/Google+App+Engine)

### See Also

- [jpaIntegration](kb_topics/jpaIntegration.md#kb-topic-integration-with-jpa)

---
## KB Topic: image

### Description
Utilities to render images

---
## KB Topic: Form Items

### Description
Manipulating the items that belong to a form.  
  
An item manages an atomic value (eg a String, Number, Date, etc) that appears as one of the properties in the overall form's values. Some items exist purely for layout or appearance purposes (eg SpacerItem) and do not manage a value.

### Related

- [DynamicForm.getItem](classes/DynamicForm.md#method-dynamicformgetitem)
- [DynamicForm.getField](classes/DynamicForm.md#method-dynamicformgetfield)
- [DynamicForm.items](classes/DynamicForm.md#attr-dynamicformitems)
- [DynamicForm.fields](classes/DynamicForm.md#attr-dynamicformfields)
- [ToolbarItem.buttons](classes/ToolbarItem.md#attr-toolbaritembuttons)

---
## KB Topic: Iteration

### Description
Operations on entire Arrays at once

### Related

- [Array.getProperty](classes/Array.md#method-arraygetproperty)
- [Array.map](classes/Array.md#method-arraymap)
- [Array.callMethod](classes/Array.md#method-arraycallmethod)
- [Array.setProperty](classes/Array.md#method-arraysetproperty)
- [Array.clearProperty](classes/Array.md#method-arrayclearproperty)
- [List.getProperty](classes/List.md#method-listgetproperty)
- [ResultSet.getProperty](classes/ResultSet.md#method-resultsetgetproperty)

---
## KB Topic: SmartClient JSP Tags

### Description
The SmartClient Java Server component ships with a number of custom JSP tags designed to make development with SmartClient easier. The custom tags are defined in the isc.tld file bundled with the isomorphic\_core\_rpc JAR. To make use of these tags, you can use the standard JSP taglib directive with the uri as distributed (which requires no additional configuration):
```
 <%@ taglib uri="http://www.smartclient.com/taglib" prefix="isomorphic" %>
 
```

All SmartClient JSP tags produce either HTML or JavaScript output, so you can easily see what any given tag is generating by doing a "View->Source" in your browser after browsing to the JSP that contains your tag. Tags that produce HTML must be located in the HTML BODY context in your JSP - that is, outside of any ``<SCRIPT>`` tags and inside ``<BODY>`` tags. Tags that produce JavaScript must be located inside ``<SCRIPT>`` tags.

---
## KB Topic: <isomorphic:jsString>

### Description
See [jspTags](#kb-topic-smartclient-jsp-tags)

_produces:_JavaScript

This tag takes everything in its body and outputs a correctly-escaped JavaScript string. This is useful for capturing HTML for display in a Canvas or Label, for example.

**Tag Attributes:**

**var**  
_value format_: Any legal JavaScript variable name _default value_: NONE

If specified, the escaped string is assigned to a newly created variable of the specified name. e.g: var foo = "bar";

**filename**  
_value format_: webRoot-relative path to file _default value_: NONE

If specified, the resulting string content is loaded from the specified file instead of from the tag body.

---
## KB Topic: layoutMember

### Description
Properties that can be set on members of a layout to control how the layout is done

### Related

- [Canvas.setShowResizeBar](classes/Canvas.md#method-canvassetshowresizebar)
- [Layout.getMemberOffset](classes/Layout.md#method-layoutgetmemberoffset)
- [Layout.getMemberDefaultBreadth](classes/Layout.md#method-layoutgetmemberdefaultbreadth)
- [Canvas.canDropBefore](classes/Canvas.md#attr-canvascandropbefore)
- [Layout.defaultLayoutAlign](classes/Layout.md#attr-layoutdefaultlayoutalign)
- [Layout.memberOverlap](classes/Layout.md#attr-layoutmemberoverlap)
- [Canvas.layoutAlign](classes/Canvas.md#attr-canvaslayoutalign)
- [Canvas.showResizeBar](classes/Canvas.md#attr-canvasshowresizebar)
- [Canvas.resizeBarTarget](classes/Canvas.md#attr-canvasresizebartarget)
- [Canvas.extraSpace](classes/Canvas.md#attr-canvasextraspace)
- [SectionStackSection.canDropBefore](classes/SectionStackSection.md#attr-sectionstacksectioncandropbefore)
- [SectionStack.itemIndent](classes/SectionStack.md#attr-sectionstackitemindent)
- [SectionStack.itemStartIndent](classes/SectionStack.md#attr-sectionstackitemstartindent)
- [SectionStack.itemEndIndent](classes/SectionStack.md#attr-sectionstackitemendindent)

---
## KB Topic: <isomorphic:loadModules>

### Description
See [jspTags](#kb-topic-smartclient-jsp-tags)

_produces:_ HTML

This tag works just like [loadISCTag](kb_topics/loadISCTag.md#kb-topic-isomorphicloadisc) except it does not load a skin. All other attributes are supported on this tag just as on `loadISC`. This tag is useful if you have a single "header" JSP that has the `loadISC` tag that you then include in other SmartClient-enabled JSPs that require additional modules. The JSPs that require additional modules can then use the `loadModules` to load additional SmartClient modules.

---
## KB Topic: Localized Number Formatting

### Description
Use the special [field types](classes/DataSourceField.md#attr-datasourcefieldtype) "localeInt", "localeFloat" and "localeCurrency" to have locale-specific formatting applied to numeric values, as well as automatic parsing of user inputs that use locale-specific decimal and grouping separators.

These special types rely on the settings [NumberUtil.decimalSymbol](classes/NumberUtil.md#classattr-numberutildecimalsymbol), [NumberUtil.groupingSymbol](classes/NumberUtil.md#classattr-numberutilgroupingsymbol) and [NumberUtil.currencySymbol](classes/NumberUtil.md#classattr-numberutilcurrencysymbol). These are normally set automatically when you load a language pack for the current locale.

See [i18n](kb_topics/i18n.md#kb-topic-internationalization-and-localization) for more background on internationalization and loading language packs for the current locale.

---
## KB Topic: longEvents

### Description
When events fill a day or span multiple days, it becomes impractical to view and interact with them in normal Calendar views. Users need a clear means of viewing and interacting with those events

---
## KB Topic: multiAutoChildren

### Description
A MultiAutoChild is an [AutoChild](#type-autochild) where the creating component usually creates more than one, hence, unlike a normal AutoChild, the AutoChild is not accessible as `creator.[autoChildName]`.

See [Using AutoChildren](kb_topics/autoChildUsage.md#kb-topic-using-autochildren) for more information on configuring a MultiAutoChild.

### See Also

- [Class.createAutoChild](classes/Class.md#method-classcreateautochild)

---
## KB Topic: Observation

### Description
Observation is the ability to take an action whenever a method is called.

### Related

- [Class.observe](classes/Class.md#method-classobserve)
- [Class.ignore](classes/Class.md#method-classignore)
- [Class.isObserving](classes/Class.md#method-classisobserving)

---
## KB Topic: Prompting

### Description
Objects / methods used for displaying prompts and warnings to the user via (possibly modal) isc Dialog objects.

### Related

- [isc.showPrompt](classes/isc.md#staticmethod-iscshowprompt)
- [isc.clearPrompt](classes/isc.md#staticmethod-iscclearprompt)
- [isc.showFadingPrompt](classes/isc.md#staticmethod-iscshowfadingprompt)
- [isc.warn](classes/isc.md#staticmethod-iscwarn)
- [isc.say](classes/isc.md#staticmethod-iscsay)
- [isc.ask](classes/isc.md#staticmethod-iscask)
- [isc.confirm](classes/isc.md#staticmethod-iscconfirm)
- [isc.askForValue](classes/isc.md#staticmethod-iscaskforvalue)
- [isc.dismissCurrentDialog](classes/isc.md#staticmethod-iscdismisscurrentdialog)
- [isc.showLoginDialog](classes/isc.md#staticmethod-iscshowlogindialog)
- [LoginDialog](classes/LoginDialog.md#class-logindialog)
- [Dialog.Prompt](classes/Dialog.md#classattr-dialogprompt)
- [Dialog.Warn](classes/Dialog.md#classattr-dialogwarn)
- [Dialog.Ask](classes/Dialog.md#classattr-dialogask)

---
## KB Topic: rpcPrompt

### Description
The properties in this group all deal with setting and styling a modal prompt during an RPC call to the server.

### Related

- [RPCManager.defaultPrompt](classes/RPCManager.md#classattr-rpcmanagerdefaultprompt)
- [RPCManager.promptStyle](classes/RPCManager.md#classattr-rpcmanagerpromptstyle)
- [RPCManager.useCursorTracker](classes/RPCManager.md#classattr-rpcmanagerusecursortracker)
- [RPCManager.promptCursor](classes/RPCManager.md#classattr-rpcmanagerpromptcursor)
- [RPCManager.showPrompt](classes/RPCManager.md#classattr-rpcmanagershowprompt)
- [RPCManager.promptDelay](classes/RPCManager.md#classattr-rpcmanagerpromptdelay)
- [RPCRequest.promptStyle](classes/RPCRequest.md#attr-rpcrequestpromptstyle)
- [RPCRequest.useCursorTracker](classes/RPCRequest.md#attr-rpcrequestusecursortracker)
- [RPCRequest.promptCursor](classes/RPCRequest.md#attr-rpcrequestpromptcursor)
- [RPCRequest.prompt](classes/RPCRequest.md#attr-rpcrequestprompt)
- [RPCRequest.showPrompt](classes/RPCRequest.md#attr-rpcrequestshowprompt)
- [RPCRequest.promptDelay](classes/RPCRequest.md#attr-rpcrequestpromptdelay)

---
## KB Topic: snapPositioning

### Description
[Canvas.snapTo](classes/Canvas.md#attr-canvassnapto) and related properties for positioning widgets relative to other widgets edges and corners. Snapped widgets will then move with the widget they are "snapped to" whenever that widget moves.

### Related

- [Canvas.getSnapPosition](classes/Canvas.md#classmethod-canvasgetsnapposition)
- [Canvas.setSnapOffsetTop](classes/Canvas.md#method-canvassetsnapoffsettop)
- [Canvas.getSnapTo](classes/Canvas.md#method-canvasgetsnapto)
- [Canvas.setSnapEdge](classes/Canvas.md#method-canvassetsnapedge)
- [Canvas.getSnapEdge](classes/Canvas.md#method-canvasgetsnapedge)
- [Canvas.snapTo](classes/Canvas.md#attr-canvassnapto)
- [Canvas.snapEdge](classes/Canvas.md#attr-canvassnapedge)
- [Canvas.snapOffsetLeft](classes/Canvas.md#attr-canvassnapoffsetleft)
- [Canvas.snapOffsetTop](classes/Canvas.md#attr-canvassnapoffsettop)
- [PointerSettings.snapTo](classes/PointerSettings.md#attr-pointersettingssnapto)
- [PointerSettings.snapOffsetLeft](classes/PointerSettings.md#attr-pointersettingssnapoffsetleft)
- [PointerSettings.snapOffsetTop](classes/PointerSettings.md#attr-pointersettingssnapoffsettop)
- [TourStep.pointerSnapTo](classes/TourStep.md#attr-toursteppointersnapto)

---
## KB Topic: Text Direction

### Description
The direction in which text is expected to flow. Since the browser is responsible for reversing much of the native content, it is necessary to set the dir attribute in the BODY tag. See [Page.isRTL](classes/Page.md#classmethod-pageisrtl).

### Related

- [Page.isRTL](classes/Page.md#classmethod-pageisrtl)

---
## KB Topic: validatorExecution

### Description
*   Explicitly defined validators on the dataSource field are run in the order in which they are defined on the client and on the server. Obviously any server-only validators are skipped on the client, and any client-only validators are skipped on the server.
*   Implicit type validators (an "isInteger" validator being applied automatically to all fields of type "Integer", for example) are run before any validators applied explicitly at the field level.
*   If a component has explicitly applied validators in addition to those picked up from the DataSourceField definition, the component-level validators will execute first. (This of course does not apply to server side validation).

---
## KB Topic: valueMap

### Description
A [ValueMap](reference_2.md#type-valuemap) defines the set of legal values for a field, and optionally allows you to provide a mapping from stored values to values as seen by the end user.

### Related

- [FormItem.getDisplayValue](classes/FormItem.md#method-formitemgetdisplayvalue)
- [FormItem.setValueMap](classes/FormItem.md#method-formitemsetvaluemap)
- [SelectItem.setValueMap](classes/SelectItem.md#method-selectitemsetvaluemap)
- [CheckboxItem.setValueMap](classes/CheckboxItem.md#method-checkboxitemsetvaluemap)
- [FormItem.valueMap](classes/FormItem.md#attr-formitemvaluemap)
- [CheckboxItem.valueMap](classes/CheckboxItem.md#attr-checkboxitemvaluemap)

---
## KB Topic: values

### Description
Manipulating the values stored in the form.

### Related

- [FormItem.changeOnKeypress](classes/FormItem.md#attr-formitemchangeonkeypress)
- [TextItem.changeOnKeypress](classes/TextItem.md#attr-textitemchangeonkeypress)
- [TextAreaItem.changeOnKeypress](classes/TextAreaItem.md#attr-textareaitemchangeonkeypress)
- [DetailViewer.valueAlign](classes/DetailViewer.md#attr-detailviewervaluealign)

---
## KB Topic: Window Header

### Description
Things related to the header subobject of Window

### Related

- [Window.setShowCloseButton](classes/Window.md#method-windowsetshowclosebutton)
- [Window.setShowTitle](classes/Window.md#method-windowsetshowtitle)
- [Window.headerControls](classes/Window.md#attr-windowheadercontrols)
- [Window.showTitle](classes/Window.md#attr-windowshowtitle)
- [Window.showHeaderIcon](classes/Window.md#attr-windowshowheadericon)
- [Window.showCloseButton](classes/Window.md#attr-windowshowclosebutton)
- [Window.showMinimizeButton](classes/Window.md#attr-windowshowminimizebutton)
- [Window.showMaximizeButton](classes/Window.md#attr-windowshowmaximizebutton)

---
## KB Topic: xmlClientVsServer

### Description
Server benefits - faster client-side processing Server neutral - heavy customization of XML transform, if any, written in Java Client benefits - faster server-side processing Client neutral - heavy customization of XML transform, if any, written in JavaScript

---
## KB Topic: zIndex

### Description
Object's "stacking order" above or below other objects

### Related

- [Canvas.getZIndex](classes/Canvas.md#method-canvasgetzindex)
- [Canvas.bringToFront](classes/Canvas.md#method-canvasbringtofront)
- [Canvas.sendToBack](classes/Canvas.md#method-canvassendtoback)
- [Canvas.moveAbove](classes/Canvas.md#method-canvasmoveabove)
- [Canvas.moveBelow](classes/Canvas.md#method-canvasmovebelow)
- [DrawItem.getZIndex](classes/DrawItem.md#method-drawitemgetzindex)
- [DrawItem.setZIndex](classes/DrawItem.md#method-drawitemsetzindex)
- [DrawItem.bringToFront](classes/DrawItem.md#method-drawitembringtofront)
- [DrawItem.sendToBack](classes/DrawItem.md#method-drawitemsendtoback)
- [DrawItem.zIndex](classes/DrawItem.md#attr-drawitemzindex)

---
## Type: AdminSearches

### Description
Policy for choosing between admin searches fetched from the DataSource vs. those declared locally on a component.

### Values

| Value | Description |
|-------|-------------|
| "preferSaved" | Combine both sets of records, but report the search record from the DataSource if two records have the same search name. |
| "preferLocal" | Combine both sets of records, but report the search record from [adminSavedSearches](#attr-databoundcomponentadminsavedsearches) if two records have the same search name. |
| "localOnly" | Only report the records from [adminSavedSearches](#attr-databoundcomponentadminsavedsearches). |

---
## Type: AIContentType

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "text" | Text content. |
| "jpegImage" | JPEG image. |
| "pngImage" | PNG image. |
| "number" | A number. |
| "object" | JSON-encodable object. Note, however, that when requesting an object response, the schema of the object is not guaranteed. |
| "array" | Array of JSON-encodable objects. Similar to "object", the schema of the elements of the array is not guaranteed. |

---
## Type: AIMessageSource

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "system" | Content that frames the context of the request and how AI should operate. If not specified, the default is generally along the lines of "You are a helpful assistant." |
| "user" | Content from the user. |
| "AI" | Content to be seen as generated via AI, although it does not necessarily need to have been generated via AI. |

---
## Type: AIProgressMessageCategory

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "success" | Something succeeded. |
| "detail" | Informational detail. |
| "recoverableError" | Concerns a recoverable error. |
| "error" | Concerns an error. |

---
## Type: AIResponseErrorType

### Description
For an [AIResponse](reference_2.md#object-airesponse) of [type](classes/AsyncOperationResult.md#attr-asyncoperationresulttype) "error", the type of error, if known.

### Values

| Value | Description |
|-------|-------------|
| "requestRateLimitExceeded" | the request exceeds a rate limit |
| "requestSizeLimitExceeded" | the request's size exceeds a limit |
| "requestUnsafe" | the request was deemed unsafe |
| "responseSizeLimitExceeded" | the response's size exceeded a limit |
| "responseUnsafe" | the generated response was deemed unsafe |

---
## Type: AIServiceMode

### Description
The mode for how AI should respond to AI-powered component view requests, such as filering, sorting, and hiliting via AI.

The amount of interaction with AI is lowest in AI Assist mode. AIDE requires more interaction with AI, and Hybrid mode requires the most amount of interaction. More interaction with AI generally requires more time to process the component view request.

### Values

| Value | Description |
|-------|-------------|
| "aiAssist" | AI Assist - AI is driving existing UI on the user's behalf. An example of this is: AI converts the user's description of what records they would like to see into [AdvancedCriteria](#object-advancedcriteria). |
| "AIDE" | AI Data Enhance - Per-record augmentation or enhancements provided via AI. Examples of this are AI-generated fields, where the field values are not derived from the records, but rather, supplied via AI. |
| "hybrid" | AI decides whether AI Assist, AIDE, or some combination of both approaches should be used to best respond to the component view request. |

### See Also

- [integratingAI](kb_topics/integratingAI.md#kb-topic-integrating-ai-technology)

---
## Type: AnimationAcceleration

### Description
Acceleration effect for animations. Can either be a ratio function or a string. Ratio functions take a value between 0 and 1 which represents how much of the animation's duration has elapsed, and return another value between 0 and 1 indicating how close the animation is to completion. For a completely linear animation, the function would return the value it was passed. This allows you to bias animations to \[for example\] speed up toward the end of the animation.  
The following strings are also supported for common ratio bias effects:

### Values

| Value | Description |
|-------|-------------|
| "smoothStart" | \- animation will speed up as time elapses |
| "smoothEnd" | \- animation will slow down as time elapses |
| "smoothStartEnd" | \- animation will speed up in the middle |
| "none" | \- no bias |

---
## Type: AnimationLayoutMode

### Description
During a [size animation](classes/Canvas.md#method-canvasanimateresize). when should the layout of the children be updated?

### Values

| Value | Description |
|-------|-------------|
| "always" | \- for every change to the target's width or height |
| "overflow" | \- for every size change which leaves the target overflowed |
| "atEnd" | \- only layout the children at the end of the animation |

---
## Type: ArrowKeyEditAction

### Description
What to do if the user hits Up or Down arrow key while editing a cell.

### Values

| Value | Description |
|-------|-------------|
| "none" | The grid will take no special action when the user presses up or down arrow keys within an editor |
| "editNext" | The grid will intercept up and down arrow keypresses and navigate to the next or previous edit row by generating an appropriate [EditCompletionEvent](#type-editcompletionevent) |

### Groups

- editing

---
## Type: AsyncOperationResultType

### Description
The type of result of an asynchronous operation.

### Values

| Value | Description |
|-------|-------------|
| "success" | The asynchronous operation completed successfully. |
| "error" | The asynchronous operation encountered an error. |
| "canceled" | The asynchronous operation was canceled. |
| "disabled" | The asynchronous operation is disabled. |
| "deferred" | The asynchronous operation was deferred. |

### See Also

- [AsyncOperationResult](#object-asyncoperationresult)

---
## Type: AutoChild

### Description
An autoChild is an automatically generated subcomponent that a component creates to handle part of its presentation or functionality. An example is the Window component and its subcomponent the "header".

See [Using AutoChildren](kb_topics/autoChildUsage.md#kb-topic-using-autochildren) for more information.

### Groups

- autoChildren

---
## Type: AutoChildShortcut

### Description
A string with the format "autoChild:_autoChildName_" passed as a [Tab.pane](classes/Tab.md#attr-tabpane) or [section item](classes/SectionStackSection.md#attr-sectionstacksectionitems) instead of an actual [Canvas](classes/Canvas.md#class-canvas) or ID.

### See Also

- [autoChildren](kb_topics/autoChildren.md#kb-topic-autochildren)

---
## Type: AutoComplete

### Description
AutoComplete behavior for [FormItems](classes/FormItem.md#class-formitem).

### Values

| Value | Description |
|-------|-------------|
| "none" | Disable browser autoComplete. Note that some browsers will disregard this setting and still perform native autoComplete for certain items - typically only for log in / password forms. See the discussion [here](classes/FormItem.md#attr-formitemautocomplete). |
| "native" | Allow native browser autoComplete. |

### Groups

- autoComplete

---
## Type: AutoFitEvent

### Description
Event on a listGrid header to trigger auto-fit of the listgrid field.

### Values

| Value | Description |
|-------|-------------|
| "doubleClick" | React to a double click on the listGrid header. |
| "click" | React to a click on the listGrid header. |
| "none" | No event will trigger auto-fit. |

### Groups

- autoFitFields

---
## Type: AutoScrollDataApproach

### Description
What should drive the automatic expansion of the chart?

### Values

| Value | Description |
|-------|-------------|
| "labels" | Expand the chart to make room for data label facet value. Unused in Bar-type charts |
| "clusters" | Expand the chart to accommodate [FacetChart.barMargin](classes/FacetChart.md#attr-facetchartbarmargin), [FacetChart.minBarThickness](classes/FacetChart.md#attr-facetchartminbarthickness), and [FacetChart.getMinClusterSize](classes/FacetChart.md#method-facetchartgetminclustersize). |
| "both" | Expand the chart to make room for both labels and clusters (whichever requires more space). |

---
## Type: AutoSelectionModel

### Description
Selection model for [CubeGrid](classes/CubeGrid.md#class-cubegrid) indicating which cells in the body should be selected when row or column headers are selected.

### Values

| Value | Description |
|-------|-------------|
| "both" | Rows and Columns will be selected on header selection |
| "rows" | Rows will be selected on row-header selection |
| "cols" | Columns will be selected on column-header selection |
| "none" | Selecting row or column headers will not select cells in the body. |

---
## Locator Structure

[AutoTest locators](reference_2.md#type-autotestlocator) consist of a series of segments, delineated by "/" characters.

Each segment identifies a step in a hierarchy from a root component to the target element. Individual segments may represent a Canvas, a FormItem, an interior DOM element or some other construction specific to the locator in question.

Note that the segments in an AutoTestLocator do not necessarily match parent-child relationships in the widget hierarchy.

**Root locator segment** The root component of a locator may designated in one of the following ways:

*   **Component ID:** If a component has an explicitly specified [ID](classes/Canvas.md#attr-canvasid) this may be used along with the class of the widget to reliably identify it, regardless of where it is in the page's widget hierarchy.  
    For example a VLayout with ID `"leftPane"` would be identified as:
    
    `//VLayout[ID="leftPane"]`
    
    Or, if [Canvas.locateByIDOnly](classes/Canvas.md#attr-canvaslocatebyidonly) is true, the class of the widget will not be recorded - the locator segment to identify the root will be just the widget ID prefixed by three slash characters - for example:
    
    `///leftPane`
    
*   **Locator Test Root:** Developers may designate a component within an application as the explicit [testRoot](classes/AutoTest.md#classmethod-autotestsettestroot). This component can then be referenced by the special root locator segment
    
    `//testRoot[]`
    
    This is useful for cases where a standard widget hierarchy may be dynamically rendered inside some component (such as a [screen](classes/RPCManager.md#classmethod-rpcmanagerloadscreen)) - see the [portableAutoTests](kb_topics/portableAutoTests.md#kb-topic-writing-autotests-for-multiple-environments) topic for more information
    
*   **Base Search Segment:** The AutoTest subsystem supports searching for components by a [defining property value](classes/Canvas.md#attr-canvasdefiningproperty). If a target element is not a descendant of a component with an explicitly specified ID, and is also not contained within the specified [testRoot](classes/AutoTest.md#classmethod-autotestsettestroot) for the application, but is contained within a component that has a specified [definingProperty value](classes/Canvas.md#attr-canvasdefiningproperty), this may be used to identify the root component for the locator.
    
    Base search segments are prefixed with `"//:"` and include the class name for the target component along with the defining property value.
    
    For example - [dataSource](classes/ListGrid_1.md#attr-listgriddatasource) is a defining property for ListGrids. The following locator would identify a ListGrid bound to a dataSource with the ID `"someDS"` wherever it appeared in the page's widget hierarchy:
    
    `//:ListGrid[dataSource="someDS"]`
    
    [AutoTest.getLocator](classes/AutoTest.md#classmethod-autotestgetlocator) will only generate a locator with a base search segment if the defining property value would unambiguously identify the base component within the application. The above locator would not be generated in an app with more than one visible ListGrid bound to `"someDS"`.
    
    Note that by default hidden and/or undrawn components are not considered when generating and resolving locator search segments, but the special `"?"` character indicates that both hidden and visible components must be considered when resolving a search segment.
    
    For example the locator `//:?ListGrid[dataSource="someDS"]` would retrieve a ListGrid bound to `"someDS"` whether visible or hidden.
    
    [AutoTest.getLocator](classes/AutoTest.md#classmethod-autotestgetlocator) will generate this locator format if the target element was hidden, or if passed the [searchSegmentsIncludeHidden](classes/AutoTestLocatorConfiguration.md#attr-autotestlocatorconfigurationsearchsegmentsincludehidden) attribute of the settings argument.
    

**Interior locator segments**

In some cases a single segment may be sufficient to identify a target element or object on the page, but in most cases, the root component locator will be suffixed with a number of interior locator segments to identify the path from the root component to the target element.

The format of individual segments within a locator will be different for different widget hierarchies and target elements. SmartClient does not exhaustively document every possible locator format for every widget, but the patterns used are consistent and can inform application design:

*   **Named AutoChildren:** Named [autoChildren](kb_topics/autoChildren.md#kb-topic-autochildren) will be identified within their creator by their autoChild name - for example
    
    `//Window[ID="mainWindow"]/body`
    
    This happens regardless of the interim widget hierarchy between the creator and its auto-child.
    
*   **Explicit locatorChildren:** Components with an explicit [named locator child](classes/Canvas.md#method-canvassetlocatorparent) relationship will be identified within their locator parent by name. For example marking a member of a Layout with the locator child name `"myView"` might produce a locator like:
    
    `//VLayout[ID="mainLayout"]/myView`
    
    Once again, this is regardless of the interim widget hierarchy between the locator parent and its locator-child.
    
*   **Search Segments:** Interior search segments in a locator are prefixed with `"//"`. Interior search segments indicate that a component may be uniquely identified by a [defining property value](classes/Canvas.md#attr-canvasdefiningproperty) within the component identified by the previous segment in the locator.
    
    For example the following locator would search for a ListGrid bound to `"someDS"` within the body of a window with ID `"mainWindow"`:
    
    `//Window[ID="mainWindow"]/body//ListGrid[dataSource="someDS"]`
    
    Note that the [AutoTest.getLocator](classes/AutoTest.md#classmethod-autotestgetlocator) method will never return a locator with a search segment that is ambiguous in the current application.
    
    If the AutoTest system can uniquely identify a component by defining property across the app as a whole, it will typically be used as a base search segment. If not the system will find the highest-level ancestor containing only one descendant with the specified definingProperty, and ensure the previous segment in the locator identifies that ancestor. This ensures that the final locator string is as compact as possible while unambiguously identifying the target.
    
    As with base search segments, a `"?"` character is used to indicate that hidden or undrawn components should be considered when resolving search locators. For example the following locator:
    
    `//Window[ID="mainWindow"]/body//?ListGrid[dataSource="someDS"]`
    
    would include hidden listGrids when searching for the grid bound to the specified dataSource.
    
*   **Locator segment fallback attributes:** If a target element or component cannot be identified within its parent by a simple identifier such as autoChildName or defining property, the AutoTest subsystem will generate a segment containing one or more attributes to identify the target. When multiple attributes are recorded it allows the SmartClient framework to use several strategies to find the target. These additional locator segment attributes are referred to as "fallback attributes".
    
    For example a locator segment with a full set of fallback attributes identifying a member of a Layout might look like this:
    
    `VLayout[ID="mainLayout"]/member[Class=TreeGrid||index=1||length=3||classIndex=0||classLength=1||roleIndex=0||roleLength=1||scRole=tree]/`
    
    This specific segment indicates that the target component is a member of a layout. The target is a TreeGrid, and is the first of 3 members. It also indicates this is the only member TreeGrid in the members array \[indicated by the `classIndex` and `classLength` attributes\], and that it is the only member with [role](classes/Canvas.md#attr-canvasariarole) set to `"tree"`.
    
    The parent layout will use these _fallback attributes_ in the locator as necessary to find the appropriate member. If the layout has three members, and the first is a TreeGrid, the target may be resolved to this member with some confidence.
    
    If this is not the case, but there is exactly one TreeGrid in the members array, or exactly one element with `role` set to tree, it will fallback to those secondary locator strategies. If fallback locator strategies are used, a warning will be logged so developers are aware of any potentially incorrect locator parsing.
    
    Developers may influence how recorded locator attributes are resolved via properties on the locator parent. For Layouts this would include [Layout.locateMembersBy](classes/Layout.md#attr-layoutlocatemembersby) and [Layout.locateMembersType](classes/Layout.md#attr-layoutlocatememberstype).
    
    For brevity and readability, when generating locators, developers may choose whether or not to include multiple fallback attributes in locator segments by setting [useMinimalFallbackAttributes](classes/AutoTest.md#classattr-autotestuseminimalfallbackattributes) to false globally, or on the `settings` parameter passed to [AutoTest.getLocator](classes/AutoTest.md#classmethod-autotestgetlocator).
    
*   **Component interior locators:** Different SmartClient components have their own patterns for identifying significant elements in the DOM within their handles. For example, ListGrid cell elements are located by row and column data. Where appropriate, properties to control how component-interior locators behave will be documented on the class in question.

### Groups

- autoTest

### See Also

- [AutoTest](classes/AutoTest.md#class-autotest)
- [automatedTesting](kb_topics/automatedTesting.md#kb-topic-automated-testing)

---
## Type: boolean

### Description
A Boolean which is either true or false. May not be null.

---
## Type: BuildUIViaAIValidationType

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "default" | default validation |
| "custom" | custom validation |

---
## Type: CalendarSaveScenario

### Description
Indicates how a given Calendar Save was initiated - values are _dialog_, _editor_ and _mouse_.

### Values

| Value | Description |
|-------|-------------|
| "dialog" | the user saved via the [Calendar.eventDialog](classes/Calendar.md#attr-calendareventdialog) |
| "editor" | the user saved via the [Calendar.eventEditor](classes/Calendar.md#attr-calendareventeditor) |
| "mouse" | the user moved or resized an [event](classes/EventCanvas.md#class-eventcanvas) with the mouse |

---
## Type: Callback

### Description
A `Callback` is an arbitrary action to be fired - usually passed into a method to be fired asynchronously as a notificaction of some event.  
The `callback` can be defined in the following formats:

*   a function
*   A string containing an expression to evaluate
*   An object with the following properties:  
    \- target: fire in the scope of this target - when the action fires, the target will be available as `this`.  
    \- methodName: if specified we'll check for a method on the target object with this name.  
    

`Callbacks` are fired via the [Class.fireCallback](classes/Class.md#classmethod-classfirecallback) method, which allows named parameters to be passed into the callback at runtime. If the Callback was specified as a string of script, these parameters are available as local variables at eval time.  
For specific SmartClient methods that make use of `Callback` objects, see local documentation for information on parameters and scope.

---
## Type: CharacterCasing

### Description
—

### Values

| Value | Description |
|-------|-------------|
| TextItem.DEFAULT | No character translation |
| TextItem.UPPER | Map characters to uppercase |
| TextItem.LOWER | Map characters to lowercase |

### Groups

- validation

---
## Type: ChartType

### Description
Known chart types. These are visual representations of data, not separate data models, although some chart types are only capable of showing a single facet of data.

Concrete charting implementations may use any value for `chartType` but should support the provided `chartType` values for charts that correspond to the visual presentation described below, to enable easy switching between charting engines.

### Values

| Value | Description |
|-------|-------------|
| Area | Values represented by area, with stacked values representing multiple facet values. This is equivalent to ChartType "Line" with stacking enabled. |
| Column | Values represented by vertical columns. Typically supports stacking to represent two facets. May support simultaneous stacking and clustering for 3 facets. |
| Bar | Values represented by horizontal bars. Typically supports stacking to represent two facets. May support simultaneous stacking and clustering for 3 facets. |
| Line | Values represented by a lines between data points, or stacked areas for multiple facets. |
| Radar | Values represented on a circular background by a line around the center, or stacked areas for multiple facets |
| Pie | Circular chart with wedges representing values. Multiple or stacked pies for multiple facets. |
| Doughnut | Like a pie chart with a central hole. Multiple or stacked doughnuts for multiple facets. |
| Scatter | A chart with two continuous numeric axes and up to one discrete facet. |
| Bubble | A chart with two continuous numeric axes and up to one discrete facet that also displays values from a third continuous, numeric domain represented as the sizes of the data point shapes. |
| Histogram | Like a column chart, except instead of showing stacked or clustered values for each position on the horizontal axis, the data values are used together with the associated [FacetChart.endValueMetric](classes/FacetChart.md#attr-facetchartendvaluemetric) values to show a series of line segments. |

---
## Type: ChildrenPropertyMode

### Description
when heuristically finding a property that appears to contain child objects, the ChildrenPropertyMode determines how to chose the property appears to contain child objects

### Values

| Value | Description |
|-------|-------------|
| "any" | assume the first object or array value we find is the children property |
| "array" | assume the first array we find is the children property, no matter the contents |
| "object" | assume the first object or array of objects we find is the children property (don't allow arrays that don't have objects) |
| "objectArray" | accept only an array of objects as the children property |

---
## Type: ClickMaskMode

### Description
Passed as a parameter to [Canvas.showClickMask](classes/Canvas.md#method-canvasshowclickmask) to determine the masks behavior when clicked.

### Values

| Value | Description |
|-------|-------------|
| "hard" | When the mask receives a click, it will fire its click action, and cancel the event, leaving the clickMask up. |
| "soft" | When the mask receives a click, it will fire its click action, then dismiss the clickMask and allow the event to proceed to its target. |

### Groups

- clickMask

---
## Type: ColorPickerMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "simple" | Display a palette of 40 basic colors from which to pick. |
| "complex" | In addition to the 40 basic colors, the user can specify a color from anywhere in the spectrum, with an optional alpha component. |

---
## Type: ContentLayoutPolicy

### Description
Policy controlling how the window will manage content within its body.

### Values

| Value | Description |
|-------|-------------|
| Window.NONE | Window does not try to size members at all on either axis. Window body defaults to a Canvas if not autosizing. Otherwise a Layout is used with policies on both axes set to [LayoutPolicy](reference_2.md#type-layoutpolicy) "none". |
| Window.VERTICAL | Window body defaults to VLayout behavior. (Body is actually just a Layout with [Layout.vertical](classes/Layout.md#attr-layoutvertical): true.) |
| Window.HORIZONTAL | Window body defaults to HLayout behavior. (Body is actually just a Layout with [Layout.vertical](classes/Layout.md#attr-layoutvertical): false.) |

---
## Type: ControlName

### Description
Names for the standard controls built into the RichTextEditor. You can use these `ControlNames` in APIs like [RichTextEditor.styleControls](classes/RichTextEditor.md#attr-richtexteditorstylecontrols) to control the order in which controls appear, to omit default controls or to show controls that are not shown by default.

Every `ControlName` is also the name of an [AutoChild](#type-autochild), so all the built-in controls can be skinned or otherwise customized via the [AutoChild system](kb_topics/autoChildUsage.md#kb-topic-using-autochildren).

### Values

| Value | Description |
|-------|-------------|
| "boldSelection" | A button to make the current selection bold. |
| "italicSelection" | A button to make the current selection italic. |
| "underlineSelection" | A button to make the current selection underlined. |
| "fontSelector" | A select item allowing the user to change the font of the current text selection. |
| "fontSizeSelector" | A select item allowing the user to change the font size of the current text selection. |
| "alignLeft" | A button to left-align the selected text. |
| "alignRight" | A button to right-align the selected text. |
| "alignCenter" | A button to center the selected text. |
| "justify" | A button to justify the selected line of text. |
| "color" | A color-picker allowing the user to set the text color. |
| "backgroundColor" | A color picker allowing the user to set the text background color. |
| "indent" | Within text, indents the paragraph. Within a list, increases the list level. |
| "outdent" | Within text, outdents the paragraph. Within a list, decreases the list level. |
| "orderedList" | Turns the current selection into an ordered list (HTML `<ol>`) or converts an unordered list to an ordered list. |
| "unorderedList" | Turns the current selection into an unordered list (HTML `<ul>`) or converts an ordered list to an unordered list. |
| "listProperties" | Shows the [listPropertiesDialog](classes/RichTextEditor.md#attr-richtexteditorlistpropertiesdialog) to allow configuring the options of the currently selected HTML list. |

---
## Type: Coordinate

### Description
A number representing a horizontal or vertical offset from the origin of a [coordinate system](classes/DrawPane.md#class-drawpane) in the `DrawPane`. [DrawRect.left](classes/DrawRect.md#attr-drawrectleft) is an example of a [DrawItem](classes/DrawItem.md#class-drawitem) attribute that's a `Coordinate`. A `Coordinate` is not limited to integers except for [DrawingType](#type-drawingtype) "vml".

---
## Type: CSSStyleName

### Description
CSS class name to apply to some HTML element on this page. This is a string that should match the css class defined for the page in an external stylesheet or in inline html `<STYLE>` tags.

As a general rule, wherever it is possible to provide a CSS styleName (such as [Canvas.styleName](classes/Canvas.md#attr-canvasstylename) or [Button.baseStyle](classes/Button.md#attr-buttonbasestyle), your CSS style can specify border, margins, padding, and any CSS attributes controlling background or text styling. You should not specify any CSS properties related to positioning, clipping, sizing or visibility (such as "overflow", "position", "display", "visibility" and "float") - use SmartClient APIs for this kind of control.

Because text wrapping cannot be consistently controlled cross-browser from CSS alone, you should use SmartClient properties such as [Button.wrap](classes/Button.md#attr-buttonwrap) instead of the corresponding CSS properties, when provided.

Content contained within SmartClient components can use arbitrary CSS, with the caveat that the content should be tested on all supported browsers, just as content outside of SmartClient must be.

**Special note on CSS margins**: wherever possible, use CSS padding and border in lieu of CSS margins, or non-CSS approaches such as [Layout.layoutMargin](classes/Layout.md#attr-layoutlayoutmargin), [Canvas.snapTo](classes/Canvas.md#attr-canvassnapto), or absolute positioning (including specifying percentage left/top coordinates). We recommend this because CSS specifies a very complicated and widely criticized "margin-collapse" behavior which has surprising effects when margins exist on both parents and children. Compounding the problem, margins are implemented very differently on different browsers, especially when it comes to HTML margins.

**Note about CSS "box models"**

The CSS "box model" defines whether the size applied to a DOM element includes padding, borders or margins, or whether such settings effectively **increase** the size of the component beyond the size specified in CSS.

In SmartClient, the size configured for a component _includes_ border, padding and margins if specified (in CSS terminology, the box model is "margin-box"). This allows CSS borders, margins and padding to be treated as purely visual properties with no effect on sizing or layout.

### Groups

- appearance

---
## Type: CurrentPane

### Description
Possible values for the current pane showing in a [SplitPane](classes/SplitPane.md#class-splitpane). See [SplitPane.currentPane](classes/SplitPane.md#attr-splitpanecurrentpane) for details.

### Values

| Value | Description |
|-------|-------------|
| "navigation" | [SplitPane.navigationPane](classes/SplitPane.md#attr-splitpanenavigationpane) is the most recently shown |
| "list" | [SplitPane.listPane](classes/SplitPane.md#attr-splitpanelistpane) is the most recently shown |
| "detail" | [SplitPane.detailPane](classes/SplitPane.md#attr-splitpanedetailpane) is the most recently shown |

---
## Type: Cursor

### Description
You can use whatever cursors are valid for your deployment platforms, but keep in mind that visual representation may vary by browser and OS. See the [MDN `cursor` page](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor) for a live demonstration.

### Values

| Value | Description |
|-------|-------------|
| Canvas.DEFAULT | Use the default arrow cursor for this browser/OS. |
| Canvas.AUTO | Use the default cursor for this element type in this browser/OS |
| Canvas.WAIT | Use the wait cursor. |
| Canvas.HAND | Use the hand cursor. |
| Canvas.MOVE | Use the "move" (crosshairs) cursor. |
| Canvas.HELP | Use the 'help' cursor. |
| Canvas.TEXT | Use the 'text' (i-beam) cursor. |
| Canvas.POINTER | Use the normal hand pointer that appears when you hover over a link |
| "arrow" | — |
| "all-scroll" | — |
| "crosshair" | Use the 'crosshair' ( + ) cursor. |
| "col-resize" | Use the column resize cursor (horizontal double-tipped arrow) |
| "row-resize" | Use the row resize cursor (vertical double-tipped arrow) |
| "e-resize" | Use the "east resize" cursor. |
| "w-resize" | Use the "west resize" cursor. |
| "n-resize" | Use the "north resize" cursor. |
| "s-resize" | Use the "south resize" cursor. |
| "se-resize" | Use the "south-east resize" cursor. |
| "ne-resize" | Use the "north-east resize" cursor. |
| "nw-resize" | Use the "north-west resize" cursor. |
| "sw-resize" | Use the "south-west resize" cursor. |
| "not-allowed" | Use the "not-allowed" cursor. |

### Groups

- cues

### See Also

- [Canvas.cursor](classes/Canvas.md#attr-canvascursor)

---
## Type: DataURLFormat

### Description
The data URL MIME type to use when [DrawPane.getDataURL](classes/DrawPane.md#method-drawpanegetdataurl) is called to convert the drawing to a data URL.

### Values

| Value | Description |
|-------|-------------|
| "any" | Any MIME type supported by the browser is acceptable. Note: The exact MIME type used may depend on the browser, and may change from version to version of SmartClient. |
| "png" | Generate an `image/png` data URL. |

---
## Type: DateDisplayFormat

### Description
Valid display formats for dates. These strings are the names of formatters which can be passed to `DateUtil.setNormalDisplayFormat()` or `DateUtil.setShortDisplayFormat()` and will be subsequently used as default long or short formatters for date objects by SmartClient components.  

Custom formatting can also be applied by passing a [FormatString](#type-formatstring) instead of a `DateDisplayFormat` string to [DateUtil.setNormalDisplayFormat](classes/DateUtil.md#classmethod-dateutilsetnormaldisplayformat) et al. See the `FormatString` docs for details.

Default set of valid display formats is as follows:

### Values

| Value | Description |
|-------|-------------|
| toString | Default native browser 'toString()' implementation. May vary by browser.  
_Example_: `Fri Nov 04 2005 11:03:00 GMT-0800 (Pacific Standard Time)` |
| toLocaleString | Default native browser 'toLocaleString()' implementation. May vary by browser. _Example_: `Friday, November 04, 2005 11:03:00 AM` |
| toUSShortDate | Short date in format MM/DD/YYYY.  
_Example_: `11/4/2005` |
| toUSShortDatetime | Short date with time in format MM/DD/YYYY HH:MM  
_Example_: `11/4/2005 11:03` |
| toEuropeanShortDate | Short date in format DD/MM/YYYY.  
_Example_: `4/11/2005` |
| toEuropeanShortDatetime | Short date with time in format DD/MM/YYYY HH:MM  
_Example_: `4/11/2005 11:03` |
| toJapanShortDate | Short date in format YYYY/MM/DD.  
_Example_: `2005/11/4` |
| toJapanShortDatetime | Short date with time in format YYYY/MM/DD HH:MM  
_Example_: `2005/11/4 11:03` |
| toSerializeableDate | Date in the format YYYY-MM-DD HH:MM:SS  
_Example_: `2005-11-04 11:09:15` |
| toDateStamp | Date in the format `<YYYYMMDD>`T`<HHMMSS>`Z _Example_: `20051104T111001Z`

Note: In addition to these standard formats, custom formatting can be set by passing a function directly to [DateUtil.setNormalDisplayFormat](classes/DateUtil.md#classmethod-dateutilsetnormaldisplayformat) et al. This function will then be executed whenever the appropriate formatter method is called \[eg [Date.toNormalDate](classes/Date.md#method-datetonormaldate)\], in the scope of the date instance in question. |

---
## Type: DateEditingStyle

### Description
The type of date/time editing style to use when editing an event.

### Values

| Value | Description |
|-------|-------------|
| "date" | allows editing of the logical start and end dates of the event |
| "datetime" | allows editing of both date and time |
| "time" | allows editing of the time portion of the event only |

---
## Type: DateInputFormat

### Description
3 character string containing the `"M"`, `"D"` and `"Y"` characters to indicate the format of strings being parsed into Date instances via `DateUtil.parseInput()`.

As an example - an input format of "MDY" would parse "01/02/1999" to Jan 2nd 1999

Note: In addition to these standard formats, a custom date string parser function may be passed directly to [DateUtil.setInputFormat](classes/DateUtil.md#classmethod-dateutilsetinputformat) or passed into [DateUtil.parseInput](classes/DateUtil.md#classmethod-dateutilparseinput) as the inputFormat parameter.

---
## Type: DefaultQueryClause

### Description
The Velocity variable names of the "pieces" of SQL that SmartClient generates to form a complete fetch or update query. You can use these variables in you own custom queries and query clause overrides to build on the SmartClient functionality. See [customQuerying](kb_topics/customQuerying.md#kb-topic-custom-querying-overview) for a full discussion.

### Values

| Value | Description |
|-------|-------------|
| "$defaultSelectClause" | The column names to select, for a fetch operation only |
| "$defaultTableClause" | The table name(s) to select from or update |
| "$defaultAnsiJoinClause" | The [ansi join(s)](classes/DataSource.md#attr-datasourceuseansijoins) to join tables to select from, if enabled. |
| "$defaultWhereClause" | The "where" condition, which will be derived from supplied criteria or a primary key value, depending on the type of operation |
| "$defaultGroupClause" | For a fetch operation when using the [Server Summaries](kb_topics/serverSummaries.md#kb-topic-server-summaries) feature, "group by" part of aggregated query |
| "$defaultGroupWhereClause" | For a fetch operation when using the [Server Summaries](kb_topics/serverSummaries.md#kb-topic-server-summaries) feature, "having" part of aggregated query (or outer "where" part if sub-select approach is used, see [OperationBinding.useHavingClause](classes/OperationBinding.md#attr-operationbindingusehavingclause) for more details) |
| "$defaultValuesClause" | The column names to update and the update values, for an update or add operation |
| "$defaultOrderClause" | The column names to sort by, for a fetch operation only |

### Groups

- customQuerying

---
## Type: DetailViewerViewState

### Description
An object containing the stored grouping information for a detailViewer. Note that this object is not intended to be interrogated directly, but may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: DeviceMode

### Description
Possible layout modes for UI components that are sensitive to the device type being used (a.k.a. "responsive design"). See for example [SplitPane.deviceMode](classes/SplitPane.md#attr-splitpanedevicemode).

### Values

| Value | Description |
|-------|-------------|
| "handset" | mode intended for handset-size devices (phones). Generally only one UI panel will be shown at a time. |
| "tablet" | mode intended for tablet-size devices. Generally, up to two panels are shown side by side in "landscape" [PageOrientation](#type-pageorientation), and only one panel is shown in "portrait" orientation. |
| "desktop" | mode intended for desktop browsers. Three or more panels may be shown simultaneously. |

---
## Type: DialogButtons

### Description
Default buttons that you can use in your Dialogs.

Refer to these buttons via the syntax `isc.Dialog.OK` when passing them into [Dialog.buttons](classes/Dialog.md#attr-dialogbuttons) or into the `properties` argument of helper methods such as [isc.say](classes/isc.md#staticmethod-iscsay).

All buttons added via `setButtons` will fire the [buttonClick event](classes/Dialog.md#method-dialogbuttonclick) (whether they are built-in or custom buttons). Built-in buttons automatically close a Dialog, with the exception of the "Apply" button.

### Values

| Value | Description |
|-------|-------------|
| OK | Dismisses dialog by calling [Dialog.okClick](classes/Dialog.md#method-dialogokclick). Title derived from [Dialog.OK_BUTTON_TITLE](classes/Dialog.md#classattr-dialogok_button_title). |
| APPLY | Does not dismiss dialog. Calls [Dialog.applyClick](classes/Dialog.md#method-dialogapplyclick) Title derived from [Dialog.APPLY_BUTTON_TITLE](classes/Dialog.md#classattr-dialogapply_button_title). |
| YES | Dismisses dialog by calling [Dialog.yesClick](classes/Dialog.md#method-dialogyesclick). Title derived from [Dialog.YES_BUTTON_TITLE](classes/Dialog.md#classattr-dialogyes_button_title). |
| NO | Dismisses dialog by calling [Dialog.noClick](classes/Dialog.md#method-dialognoclick). Title derived from [Dialog.NO_BUTTON_TITLE](classes/Dialog.md#classattr-dialogno_button_title). |
| CANCEL | Dismisses dialog by calling [Dialog.cancelClick](classes/Dialog.md#method-dialogcancelclick). Title derived from [Dialog.CANCEL_BUTTON_TITLE](classes/Dialog.md#classattr-dialogcancel_button_title). |
| DONE | Dismisses dialog by calling [Dialog.doneClick](classes/Dialog.md#method-dialogdoneclick). Title derived from [Dialog.DONE_BUTTON_TITLE](classes/Dialog.md#classattr-dialogdone_button_title). |

---
## Type: Distance

### Description
A number representing the width, height, or radius of a [DrawItem](classes/DrawItem.md#class-drawitem) in the [DrawPane](classes/DrawPane.md#class-drawpane). [DrawRect.width](classes/DrawRect.md#attr-drawrectwidth) is an example of a [DrawItem](classes/DrawItem.md#class-drawitem) attribute that's a `Distance`. A `Distance` is not limited to integers except for [DrawingType](#type-drawingtype) "vml".

---
## Type: double

### Description
A decimal (or "floating point") number, for example, 5.5. May not be null.

---
## Type: Double

### Description
A decimal (or "floating point") number, for example, 5.5. Null is allowed.

### See Also

- [double](#type-double)

---
## Type: DragDataAction

### Description
What do we do with data that's been dropped into another list?

### Values

| Value | Description |
|-------|-------------|
| "none" | Don't do anything, resulting in the same data being in both lists. |
| Canvas.COPY | Copy the data leaving the original in our list. |
| Canvas.MOVE | Remove the data from this list so it can be moved into the other list. |

### Groups

- dragdrop

---
## Type: DragIntersectStyle

### Description
Different styles of determining intersection: with mouse or entire rect of target

### Values

| Value | Description |
|-------|-------------|
| "mouse" | Look for drop targets that are under the current mouse cursor position. |
| "rect" | Look for drop targets by intersection of the entire rect of the drag target with the droppable target. |

### Groups

- dragdrop

---
## Type: DragMaskType

### Description
What kind of mask to use for masking dragged element.

### Values

| Value | Description |
|-------|-------------|
| "div" | creates an element with ordinary HTML content that will block events |
| "iframe" | creates an iframe with empty content |
| "hide" | hides the contents of this widget temporarily |
| "none" | no mask |

### Groups

- dragdrop

---
## Type: DragTrackerMode

### Description
When records are being dragged from within a ListGrid, what sort of drag-tracker should be displayed?

### Values

| Value | Description |
|-------|-------------|
| "none" | Don't display a drag tracker at all |
| "icon" | Display an icon to represent the record(s) being dragged. Icon src is derived from [ListGrid.getDragTrackerIcon](classes/ListGrid_2.md#method-listgridgetdragtrackericon) |
| "title" | Display a title for the record being dragged. Title derived from [ListGrid.getDragTrackerTitle](classes/ListGrid_2.md#method-listgridgetdragtrackertitle) |
| "record" | Display the entire record being dragged |

### Groups

- dragTracker

---
## Type: DrawingType

### Description
The type of drawing back-end used by a [DrawPane](classes/DrawPane.md#class-drawpane) to draw its [draw items](classes/DrawPane.md#attr-drawpanedrawitems) on screen.
#### SVG and bitmap tradeoffs

*   SVG is best supported in IE9+ and Opera 12.16 and earlier, but may also be used in Chrome, Opera 15+, Firefox 4+, and Safari.
*   SVG tends to be higher quality, especially when it comes to text and drawing on high-DPI displays and mobile devices.
*   [DrawItem.zIndex](classes/DrawItem.md#attr-drawitemzindex), [DrawItem.bringToFront](classes/DrawItem.md#method-drawitembringtofront), and [DrawItem.sendToBack](classes/DrawItem.md#method-drawitemsendtoback) are not supported on iOS devices in bitmap drawing mode due to platform limitations. These APIs are supported on iOS in SVG drawing mode.
*   Incremental updates to just a few elements of a drawing are faster in SVG, whereas whole drawing refreshes are faster in bitmap mode.
*   Browsers have limits on the maximum dimensions or area of the `<canvas>` element used in bitmap drawing. The limits on a `<canvas>` imposed by the browser translate to the same limits on the dimensions or area of a `DrawPane` using bitmap drawing. Internet Explorer, for example, limits the width and height of a `<canvas>` to 8192 pixels: [http://msdn.microsoft.com/en-us/library/ie/ff975062(v=vs.85).aspx](http://msdn.microsoft.com/en-us/library/ie/ff975062\(v=vs.85\).aspx); therefore, in IE using bitmap drawing, a `DrawPane` can be at most 8192×8192 in size. To make larger drawings, you can either switch to SVG drawing, use multiple `DrawPane`s, or enable [drag-scrolling](classes/DrawPane.md#attr-drawpanecandragscroll).
*   In bitmap drawing, each pixel uses around 4 to 8 bytes of memory. Large bitmap drawings can therefore use a lot of memory. A 4000×2000 bitmap drawing will use around 31 to 61 Megabytes of memory.  
    Note: To minimize memory use when using bitmap drawing for a large drawing, it may be useful to employ [slicing](http://en.wikipedia.org/wiki/Slicing_\(interface_design\)) if possible. For example, if the drawing is mostly a solid color except for content located at a few small-area places on screen, a [Canvas](classes/Canvas.md#class-canvas) can be created with the solid background color and one `DrawPane` can be created for each content area. Each `DrawPane` is [added as a child](classes/Canvas.md#method-canvasaddchild) to the `Canvas`. The [left](classes/Canvas.md#attr-canvasleft) and [top](classes/Canvas.md#attr-canvastop) properties of the `DrawPane`s are used to absolutely-position them within the `Canvas` parent.

### Values

| Value | Description |
|-------|-------------|
| "svg" | Use Scalable Vector Graphics (SVG). SVG is a W3C standard supported by IE9+, Chrome, Firefox 4+, Safari, and Opera. |
| "bitmap" | Use an HTML5 `<canvas>` element. "bitmap" drawing is supported by IE9+, Chrome, Firefox, Safari, and Opera. |
| "vml" | Use Vector Markup Language (VML). VML is a deprecated vector graphics technology supported only by Internet Explorer 6 through 9. In IE 6, 7, and 8, "vml" drawing is the only supported drawing back-end. |

---
## Type: DrawShapeCommandType

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "close" | Draws a straight line from the current point to the last "moveto" point. There are no arguments. |
| "moveto" | Start a new sub-path at a given (x,y) coordinate. The args array for this command type is a two-element array of the X and Y coordinates. |
| "lineto" | Draw a line from the current point to the given (x,y) coordinate which becomes the new current point. Multiple (x,y) coordinates may be specified to draw a path, in which case the last point becomes the new current point. The args array for this command type is an array of one or more Points (two-element arrays of the X and Y coordinates). |
| "circleto" | Draw a segment of a specified circle. A straight line (the "initial line segment") is drawn from the current point to the start of the circular arc. The args array for this command type contains 4 values:

0.  The center (cx,cy) Point (two-element array) of the circle.
1.  radius
2.  startAngle - Start angle in degrees
3.  endAngle - End angle in degrees

Note that the *"circleto" Command example* can be very helpful when learning how to write "circleto" commands. |

---
## Type: DSInheritanceMode

### Description
For DataSources of type "sql" and "hibernate", specifies the kind of inheritance to use when a dataSource specifies [inheritsFrom](classes/DataSource.md#attr-datasourceinheritsfrom).

### Values

| Value | Description |
|-------|-------------|
| "full" | Inherit fields by copying them onto the inheriting DataSource's underlying table. When we import a DataSource with this inheritanceMode, we create actual columns for inherited fields on the table we create. With this inheritanceMode, inherited fields are updatable. |
| "none" | Do not physically inherit fields onto the inheriting DataSource's SQL table. Columns will not be created for inherited fields on import, and all generated SQL operations will exclude inherited fields. However, those fields are still part of the DataSource's schema so you can, for example, write [custom SQL](kb_topics/customQuerying.md#kb-topic-custom-querying-overview) that returns values for the inherited fields, and they will be delivered to the client. |

### Groups

- fields

---
## Type: DSOperationType

### Description
One of the four basic operations that can be performed on DataSource data: "fetch", "add", "update", "remove". Elsewhere called CRUD operations, where CRUD stands for "create", "retrieve", "update", "delete", which correspond to "add", "fetch", "update" and "remove" in SmartClient terminology. See [dataSourceOperations](kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) for a full description.

There are also additional, non-CRUD operations explained below.

### Values

| Value | Description |
|-------|-------------|
| "fetch" | Fetch one or more records that match a set of search criteria. |
| "add" | Store new records |
| "update" | Update an existing record |
| "remove" | Remove (delete) an existing record |
| "custom" | perform some arbitrary custom logic that is not a CRUD operation. Format of the inputs and outputs is unconstrained, and the operation will be ignored for cache sync purposes by [ResultSet](classes/ResultSet.md#class-resultset)s. See [DataSource.performCustomOperation](classes/DataSource.md#method-datasourceperformcustomoperation). |
| "validate" | Run server-side validation for "add" or "update" without actually adding or updating anything. See [DataSource.validateData](classes/DataSource.md#method-datasourcevalidatedata). |
| "viewFile" | Retrieve a file stored in a binary field in a DataSource record, and allow the browser to choose whether to view it directly or prompt the user to save. See [binaryFields](kb_topics/binaryFields.md#kb-topic-binary-fields). |
| "downloadFile" | Like "viewFile", but the HTTP header Content-Disposition is used to suggest that the browser show a save dialog. See [binaryFields](kb_topics/binaryFields.md#kb-topic-binary-fields). |
| "storeTestData" | Takes a List of Maps and stores the data in Admin Console XML test data format |
| "clientExport" | Upload formatted client data and export it to Excel, XML and other formats. Used automatically by [exportClientData()](classes/DataSource.md#method-datasourceexportclientdata) and cannot be used directly. Usable only with the SmartClient server framework. |
| "getFile" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.getFile](classes/DataSource.md#method-datasourcegetfile), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "hasFile" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.hasFile](classes/DataSource.md#method-datasourcehasfile), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "listFiles" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.listFiles](classes/DataSource.md#method-datasourcelistfiles), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "removeFile" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.removeFile](classes/DataSource.md#method-datasourceremovefile), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "saveFile" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.saveFile](classes/DataSource.md#method-datasourcesavefile), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "renameFile" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.renameFile](classes/DataSource.md#method-datasourcerenamefile), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "getFileVersion" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.getFileVersion](classes/DataSource.md#method-datasourcegetfileversion), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "hasFileVersion" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.hasFileVersion](classes/DataSource.md#method-datasourcehasfileversion), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "listFileVersions" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.listFileVersions](classes/DataSource.md#method-datasourcelistfileversions), and would not normally be used directly. Usable only with the SmartClient server framework. |
| "removeFileVersion" | Use the DataSource as a [source for files](kb_topics/fileSource.md#kb-topic-filesource-operations). Used automatically by [DataSource.removeFileVersion](classes/DataSource.md#method-datasourceremovefileversion), and would not normally be used directly. Usable only with the SmartClient server framework. |

---
## Type: EdgeName

### Description
An edge or corner of a rectange, or it's center. Used in APIs such as [Canvas.resizeFrom](classes/Canvas.md#attr-canvasresizefrom) and [Canvas.getEventEdge](classes/Canvas.md#classmethod-canvasgeteventedge).

### Values

| Value | Description |
|-------|-------------|
| "T" | top edge |
| "B" | bottom edge |
| "L" | left edge |
| "R" | right edge |
| "TL" | top-left corner |
| "TR" | top-right corner |
| "BL" | bottom-left corner |
| "BR" | bottom-right corner |
| "C" | center |

---
## Type: EdgeSizes

### Description
Object used to specify custom edge sizes or offsets. Specified as an object where `defaultSize` will map to the default edge size or offset for the canvas ([Canvas.edgeSize](classes/Canvas.md#attr-canvasedgesize), or [Canvas.edgeOffset](classes/Canvas.md#attr-canvasedgeoffset) and `top`, `left`, `right` and `bottom` will map to the [edgeTop](classes/EdgedCanvas.md#attr-edgedcanvasedgetop)/[edgeOffsetTop](classes/EdgedCanvas.md#attr-edgedcanvasedgeoffsettop), [edgeLeft](classes/EdgedCanvas.md#attr-edgedcanvasedgeleft)/[edgeOffsetLeft](classes/EdgedCanvas.md#attr-edgedcanvasedgeoffsetleft), [edgeRight](classes/EdgedCanvas.md#attr-edgedcanvasedgeright)/[edgeOffsetRight](classes/EdgedCanvas.md#attr-edgedcanvasedgeoffsetright), and [edgeBottom](classes/EdgedCanvas.md#attr-edgedcanvasedgebottom)/[edgeOffsetBottom](classes/EdgedCanvas.md#attr-edgedcanvasedgeoffsetbottom) attributes on the paneContainer respectively. Note that not all these properties have to be set - if unset standard edge sizing rules will apply.

---
## Type: EditCompletionEvent

### Description
What event / user interaction type caused cell editing to complete.

### Values

| Value | Description |
|-------|-------------|
| ListGrid.CLICK_OUTSIDE | User clicked outside editor during edit. |
| ListGrid.CLICK | User started editing another row by clicking on it |
| ListGrid.DOUBLE_CLICK | User started editing another row by double clicking |
| ListGrid.ENTER_KEYPRESS | Enter pressed. |
| ListGrid.ESCAPE_KEYPRESS | User pressed Escape. |
| ListGrid.UP_ARROW_KEYPRESS | Up arrow key pressed. |
| ListGrid.DOWN_ARROW_KEYPRESS | down arrow key. |
| ListGrid.TAB_KEYPRESS | User pressed Tab. |
| ListGrid.SHIFT_TAB_KEYPRESS | User pressed Shift+Tab. |
| ListGrid.EDIT_FIELD_CHANGE | Edit moved to a different field (same row) |
| ListGrid.PROGRAMMATIC | Edit completed via explicit function call |

### Groups

- editing

---
## Type: EnterKeyEditAction

### Description
What to do when a user hits enter while editing a cell

### Values

| Value | Description |
|-------|-------------|
| "done" | end editing (will save edit values if [ListGrid.autoSaveEdits](classes/ListGrid_1.md#attr-listgridautosaveedits) is true). |
| "nextCell" | edit the next editable cell in the record |
| "nextRow" | edit the same field in the next editable record |
| "nextRowStart" | edit the first editable cell in next editable record |

### Groups

- editing

---
## Type: EscapeKeyEditAction

### Description
What to do if the user hits escape while editing a cell.

### Values

| Value | Description |
|-------|-------------|
| "cancel" | cancels the current edit and discards edit values |
| "done" | end editing (will save edit values if [ListGrid.autoSaveEdits](classes/ListGrid_1.md#attr-listgridautosaveedits) is true). |
| "exit" | exit the editor (edit values will be left intact but not saved). |
| "ignore" | do nothing special when the Escape key is pressed (ie, just ignore it) |

### Groups

- editing

---
## Type: EscapingMode

### Description
Mode for escaping text values when using [DataSource.recordsAsText](classes/DataSource.md#method-datasourcerecordsastext) or [DataSource.recordsFromText](classes/DataSource.md#method-datasourcerecordsfromtext).

### Values

| Value | Description |
|-------|-------------|
| "double" | Literal double quotes in data values are doubled (""), as expected by Microsoft Excel when pasting text values |
| "backslash" | double quotes in data values have a blackslash (\\) prepended, similar to String escaping in JavaScript and Java |

---
## Type: FieldFilterMode

### Description
Indicates where a given field can be legally filtered. By default, any field where [DataSourceField.canFilter](classes/DataSourceField.md#attr-datasourcefieldcanfilter) isn't `false` allows filtering either at the server or at the [client](classes/ResultSet.md#attr-resultsetuseclientfiltering), according to related settings.

This is the recommended behavior, but it can be useful or necessary to limit filtering in some cases.

### Values

| Value | Description |
|-------|-------------|
| "both" | \- filter on the client where possible and contact the server when necessary |
| "serverOnly" | \- any change to criteria for a field causes cache invalidation and a trip to the server. This mode is quite useful for cases where client filtering can't replicate server filtering, such as:

*   search engines that consider something a match based on word roots (like treating "sunken" as a match for "sink")
*   server-side formatting, where values are delivered as HTML or even as images, where the value seen in the browser no longer matches the search text
*   searching large files where the files won't be delivered to the client

By using this mode only for fields that are special, you can preserve the performance benefits of client-side filtering on other fields. |

---
## Type: FieldName

### Description
Name for a field.

Must be unique across all fields of its containing field container as well as a valid JavaScript identifier, as specified by ECMA-262 Section 7.6.

Note: The [String.isValidID](classes/String.md#staticmethod-stringisvalidid) function can be used to test whether a name is a valid JavaScript identifier.

---
## Type: FieldNamingStrategy

### Description
The strategy to use when generating field names - for example, for new formula or summary fields created using the built-in editors.

### Values

| Value | Description |
|-------|-------------|
| "simple" | generate names in the format fieldTypeX, where field type might be "formulaField" and X is an index specific to the field-type and component instance |
| "uuid" | generates a UUID for all generated field names |

---
## Type: FiscalYearMode

### Description
Strategies for calculating the FiscalYear within a [FiscalCalendar](#object-fiscalcalendar) from the specified [FiscalCalendar.defaultDate](classes/FiscalCalendar.md#attr-fiscalcalendardefaultdate) and [FiscalCalendar.defaultMonth](classes/FiscalCalendar.md#attr-fiscalcalendardefaultmonth) If the specified fiscal year date starts in one calendar year and ends in the next.

### Values

| Value | Description |
|-------|-------------|
| "end" | The fiscalYear value for the date range will match the calendar year in which the period ends. For example if the defaultDate and defaultMonth were set to represent April 1st, the fiscal year starting on April 1st 2020 would end on April 1st 2021. Setting the fiscalYearMode to `end` would mean the fiscalYear value for this block would be 2021. |
| "start" | The fiscalYear value for the date range will match the calendar year in which the period starts. For example if the defaultDate and defaultMonth were set to represent April 1st, the fiscal year starting on April 1st 2020 would end on April 1st 2021. Setting the fiscalYearMode to `start` would mean the fiscalYear value for this block would be 2020. |

---
## Type: float

### Description
A decimal (or "floating point") number, for example, 5.5. May not be null.

---
## Type: Float

### Description
A decimal (or "floating point") number, for example, 5.5. Null is allowed.

### See Also

- [float](#type-float)

---
## Type: ForceTextApproach

### Description
Approach to force a text value to be interpreted as text rather than parsed as a date, time or other structured types, as can happen with Microsoft Excel. For background information, see [excelPasting](kb_topics/excelPasting.md#kb-topic-copy-and-paste-with-excel).

### Values

| Value | Description |
|-------|-------------|
| "leadingSpace" | a leading space character is added |
| "formula" | text value is turned into a trivial Excel formula (eg "car" becomes ="car"). In Excel, this renders just the value "car" but editing the cell reveals the formula. |

---
## Type: FormatString

### Description
A String to be used as a format specifier for a date, datetime, time or numeric field, via the [format](classes/DataSourceField.md#attr-datasourcefieldformat) and [exportFormat](classes/DataSourceField.md#attr-datasourcefieldexportformat) properties.

For fields with a numeric type, the format string is similar to java.text.NumberFormat (see [DecimalFormat JavaDoc](http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormat.html)), and for date, time, and datetime types, the format string is similar to java.text.SimpleDateFormat (see [SimpleDateFormat JavaDoc](http://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html)).

Note that all the client-side formatting described in this section is is done by the [NumberUtil.format()](classes/NumberUtil.md#classmethod-numberutilformat) and [DateUtil.format()](classes/DateUtil.md#classmethod-dateutilformat) methods. These are static utility methods that your own code can call if you need to programmatically format a date or number using a `FormatString`

There are 3 possible contexts where a `FormatString` may be interpreted, and each has slightly different limitations:

#### in-browser rendering & client-driven exports
Almost complete support for Java's SimpleDateFormat/DecimalFormat, as described below, with some small extensions for formatting with awareness of a [FiscalCalendar](#object-fiscalcalendar).

This category includes cases where code running in the browser does the rendering and the rendered result is passed to the server, such as [client-driven export](classes/ListGrid_2.md#method-listgridexportclientdata) and [PDF export of the printed view](classes/RPCManager.md#classmethod-rpcmanagerexportcontent).

#### Excel export
Almost the same as in-browser rendering, with minor limitations due to missing features in Excel. Exact differences are described under [DataSourceField.exportFormat](classes/DataSourceField.md#attr-datasourcefieldexportformat).
#### non-Excel server export
For example, CSV, XML or JSON [export formats](reference_2.md#type-exportformat) provided via [DataSource.exportData](classes/DataSource.md#method-datasourceexportdata). Full support for SimpleDateFormat/DecimalFormat as provided by whichever Java version you have installed on the server. However note that depending on the context of the export, the default behavior may be to ignore format strings, since formatting intended for end users wouldn't be desirable if data exchange is the goal. See the [Export Formatting overview](kb_topics/exportFormatting.md#kb-topic-exports--formatting) for details.

#### Date Format

| Format token | Description | Sample value |
|---|---|---|
| yy | Year as a two-digit number | "99" or "07" |
| yyyy | Year as a four-digit number | "1999" or "2007" |
| YY | Week year as a two-digit number (week year is the year associated with the entire week deemed to contain a given date, and it may differ from calendar year. For example, the week year of December 31 2012 is 2013) | "99" or "07" |
| YYYY | Week year as a four-digit number | "1999" or "2007" |
| LL | Fiscal year as a two-digit number ([FiscalCalendar](#object-fiscalcalendar)) | "99" or "07" |
| LLLL | Fiscal year as a four-digit number | "1999" or "2007" |
| M | Month in year | "1" to "12" |
| MM | Month in year with leading zero if required | "01" to "12" |
| MMM | Short month name ([DateUtil.shortMonthNames](classes/DateUtil.md#classattr-dateutilshortmonthnames)) | "Jan" to "Dec" |
| MMMM | Full month name ([DateUtil.monthNames](classes/DateUtil.md#classattr-dateutilmonthnames)) | "January" to "December" |
| w | Week in year | "1" to "52" |
| ww | Week in year with leading zero if required | "01" to "52" |
| C | Week in fiscal year ([FiscalCalendar](#object-fiscalcalendar)) | "7" or "29" |
| CC | Week in fiscal year with leading zero if required | "07" or "29" |
| d | Day of the month | "1" to "31" |
| dd | Day of the month with leading zero if required | "01" to "31" |
| ddd | Short day name ([DateUtil.shortDayNames](classes/DateUtil.md#classattr-dateutilshortdaynames)) | "Mon" to "Sun" |
| dddd | Full day name. ([DateUtil.dayNames](classes/DateUtil.md#classattr-dateutildaynames)) | "Monday" to "Sunday" |
| E | Short day name ("EE" and "EEE" are equivalent; all are exactly the same as "ddd" - "E" is supported purely to conform with SimpleDateFormat) | "Mon" to "Sun" |
| EEEE | Full day name (exactly the same as "dddd") | "Monday" to "Sunday" |
| D | Day in year | "1" to "366" |
| DD | Day in year with leading zero if required | "01" to "366" |
| c | Day in fiscal year ([FiscalCalendar](#object-fiscalcalendar)) | "5" or "204" |
| cc | Day in fiscal year with leading zero if required | "05" or "204" |
| u | Day number in week (1 is Monday) | "1" to "7" |
| H | Hour in day, 0-23 (24-hour clock) | "0" to "23" |
| HH | Hour in day with leading zero if required (24-hour) | "00" to "23" |
| h | Hour in day, 1-12 (12-hour clock) | "1" to "12" |
| hh | Hour in day with leading zero if required (12-hour) | "01" to "12" |
| m | Minute in hour | "0" to "59" |
| mm | Minute in hour with leading zero if required | "00" to "59" |
| s | Second in minute | "0" to "59" |
| ss | Second in minute with leading zero if required | "00" to "59" |
| S | Millisecond in second | "0" to "999" |
| SSS | Millisecond in second with leading zero(s) if required | "000" to "999" |
| a | The AM/PM designator ([Time.AMIndicator](classes/Time.md#classattr-timeamindicator)) | " am" or " pm" |

Note that all text that doesn't represent tokens specified above will be passed through to the output, but such unmapped character sequences are reserved for future use. To future-proof your code, you may single quote `"'"` any text to escape it to ensure no formatting is applied, guaranting that it's passed through unaltered. Thus, a format of `"h'h'"` might end up as `"5h"`. To create a single quote itself, use two in a row - for example `"h o''clock"`.

#### Examples - various formatted versions of the datetime "2006-08-03 11:26:18"

| "M/d/yy" | 8/3/06 |
|---|---|
| "MMMM yyyy" | August 2006 |
| "HH:mm" | 11:26 |
| "d MMM yyyy, H:ma" | 3 Aug 2006, 11:26 am |
| "dd/MM/yyyy" | 03/08/2006 |
| "CC/LLLL" | 53/2006 (assuming the fiscal year ends in the first week of August) |

#### `SimpleDateFormat` specifiers that we do **not** support:

*   Era designator, BC/AD (G)
*   Day of week in month (F)
*   Hour in day, 24-hour, with 1-based instead of normal 0-based numbering (hours are 1-24) (k)
*   Hour in day, 12-hour, with 0-based instead of normal 1-based numbering (hours are 0-11) (K)
*   Timezone (z, Z, X)

#### Number Format

| Format char | Description |
|---|---|
| 0 | Digit, zero is displayed |
| # | Digit, zero is not displayed |
| - | Minus sign |
| . | Decimal separator |
| % | Multiply by 100 and show as percentage |
| ‰ (\u2030) | Multiply by 1000 and show as per mille. See below. |
| , | Indicates digit grouping should be used - eg 1,000,000. See below. |
| ; | Separates positive and negative subpatterns. See below. |
| ¤ (\u00A4) | As a prefix or suffix, indicates the local currency symbol should be used. Note that you must use special notation to include this character in an XML file (such as a .ds.xml file). See below. |
| ' | Used to quote special characters in a prefix or suffix, for example, "'#'#" formats 123 to "#123". To create a single quote itself, use two in a row: "# o''clock". |

All other characters in the format string are taken literally and output unchanged.

#### Examples

| Format string | Zero value | Positive value: 12345.678 | Negative value: -2345.123 |
|---|---|---|---|
| "0.00" | 0.00 | 12345.68 | -2345.12 |
| ",##0.00" | 0.00 | 12,345.68 | -2,345.12 |
| "0.###" | 0 | 12345.678 | -2345.123 |
| "¤,0.00" | $0.00 | $12,345.68 | -$2345.12 |
| "0.0#%" | 0.0% | 1234567.8% | -234512.3% |
| "0.0#‰" | 0.0‰ | 12345678.0‰ | -2345123.0‰ |
| "0.0#'%'" | 0.0% | 12345.68% | -2345.12% |
| "0.00;(0.00)" | 0.0% | 12345.68 | (2345.12) |

  
Note, the above examples include cases where there are multiple '#' characters in the integer part of the number format (ie, to the left of the decimal separator, or the entire format if there is no separator). We support this pattern simply because `DecimalFormat` does: the extra '#' characters are not significant. In other words, the format "##0.00" produces exactly the same formatting as "0.00", and "##,###,###.##" produces exactly the same formatting as ",#.##". However, multiple '0' characters in the integer part of the format _are_ significant, as are both '#' and '0' characters in the decimal part of the format (ie, to the right of any decimal separator).

The ";" character marks the boundary between two subpatterns - the first to be used for formatting positive numbers (and 0), the second for negative numbers. Specifying a separate pattern for negative numbers is optional: if no negative subpattern is specified, negative numbers are formatted like positive numbers, but with a leading "-" sign.

The "¤" symbol (\\u00A4) is documented in the Java DecimalFormat class as a placeholder for the currency symbol appropriate to the current locale. For client-driven exports, we replace it with the [localized currency symbol](classes/NumberUtil.md#classattr-numberutilcurrencysymbol). Likewise, we use [decimalSymbol](classes/NumberUtil.md#classattr-numberutildecimalsymbol) and [groupingSymbol](classes/NumberUtil.md#classattr-numberutilgroupingsymbol) to localize the formatting of numbers. Note that "\\u00A4" is the correct way to specify this character in Javascript code. If you need to specify the character in an XML file - the common requirement is in a .ds.xml DataSource descriptor file - you must use the code "&#x00A4;" instead.

The "‰" per mille symbol is specified as "\\u2030" in Javascript code; in XML or HTML you can use either the equivalent notation "&#x2030;" or the special HTML code "&permil;".

#### `DecimalFormat` features that we do **not** support:

*   Scientific notation
*   Doubled currency symbol means "use international currency symbol"
*   We do not support arbitrary digit grouping, by providing patterns of the '#' and ',' characters, like `DecimalFormat` does. Grouping in SmartClient FormatStrings is enabled with a single "," character somewhere before or within the number-formatting part of the string - extra "," characters within the number-formatting part of the string are tolerated, but they have no effect. Grouping in SmartClient always causes digits to be gathered in groups of three

### See Also

- [DataSourceField.format](classes/DataSourceField.md#attr-datasourcefieldformat)
- [DataSourceField.exportFormat](classes/DataSourceField.md#attr-datasourcefieldexportformat)
- [DateUtil.format](classes/DateUtil.md#classmethod-dateutilformat)
- [NumberUtil.format](classes/NumberUtil.md#classmethod-numberutilformat)
- [Time.toTime](classes/Time.md#classmethod-timetotime)
- [Time.toShortTime](classes/Time.md#classmethod-timetoshorttime)

---
## Type: FormattingContext

### Description
The context for which a data-value is being formatted.

### Values

| Value | Description |
|-------|-------------|
| static | for static display in the chart body |
| hover | for transient display in a hover |

---
## Type: FormItemElementType

### Description
HTML elements that make up a complete FormItem (note, not all FormItems use all of these elements)

### Values

| Value | Description |
|-------|-------------|
| "cell" | The form item as a whole, including the text element, any icons, and any hint text for the item. This is the cell containing the form item |
| "control" | The "control" cell containing the text box and picker |
| "pickerIcon" | The cell containing the item's picker icon, if it has one |
| "textBox" | The item's native text box, if it has one |
| "title" | The cell containing the title |

### See Also

- [FormItem.getCustomState](classes/FormItem.md#method-formitemgetcustomstate)

---
## Type: FormItemType

### Description
DynamicForms automatically choose the FormItem type for a field based on the `type` property of the field. The table below describes the default FormItem chosen for various values of the `type` property.

You can also set [field.editorType](classes/FormItem.md#attr-formitemeditortype) to the classname of a [FormItem](classes/FormItem.md#class-formitem) to override this default mapping. You can alternatively override [DynamicForm.getEditorType](classes/DynamicForm.md#method-dynamicformgeteditortype) to create a form with different rules for which FormItems are chosen.

### Values

| Value | Description |
|-------|-------------|
| "text" | Rendered as a [TextItem](classes/TextItem.md#class-textitem), unless the length of the field (as specified by [DataSourceField.length](classes/DataSourceField.md#attr-datasourcefieldlength) attribute) is larger than the value specified by [DynamicForm.longTextEditorThreshold](classes/DynamicForm.md#attr-dynamicformlongtexteditorthreshold), a [TextAreaItem](classes/TextAreaItem.md#class-textareaitem) is shown. |
| "boolean" | Rendered as a [CheckboxItem](classes/CheckboxItem.md#class-checkboxitem) |
| "integer" | Rendered as an [IntegerItem](#class-integeritem), a trivial subclass of [TextItem](classes/TextItem.md#class-textitem), by default. Consider setting editorType:[SpinnerItem](classes/SpinnerItem.md#class-spinneritem). |
| "float" | Rendered as a [FloatItem](#class-floatitem), a trivial subclass of [TextItem](classes/TextItem.md#class-textitem), by default. Consider setting editorType:[SpinnerItem](classes/SpinnerItem.md#class-spinneritem). |
| "date" | Rendered as a [DateItem](classes/DateItem.md#class-dateitem) |
| "time" | Rendered as a [TimeItem](classes/TimeItem.md#class-timeitem) |
| "datetime" | Rendered as a [DateTimeItem](classes/DateTimeItem.md#class-datetimeitem) |
| "enum" | Rendered as a [SelectItem](classes/SelectItem.md#class-selectitem). Also true for any field that specifies a [FormItem.valueMap](classes/FormItem.md#attr-formitemvaluemap). Consider setting editorType:[ComboBoxItem](classes/ComboBoxItem.md#class-comboboxitem). |
| "sequence" | Same as `text` |
| "link" | If [DataSourceField.canEdit](classes/DataSourceField.md#attr-datasourcefieldcanedit)`:false` is set on the field, the value is rendered as a [LinkItem](classes/LinkItem.md#class-linkitem). Otherwise the field is rendered as a [TextItem](classes/TextItem.md#class-textitem). |
| "image" | If the field is editable, rendered as a [TextItem](classes/TextItem.md#class-textitem) to edit the URL or partial URL  
If [non editable](classes/FormItem.md#attr-formitemcanedit), and [readOnlyDisplay](classes/DynamicForm.md#attr-dynamicformreadonlydisplay) is "static", an image will be rendered out, deriving the URL from the field value combined with [FormItem.imageURLPrefix](classes/FormItem.md#attr-formitemimageurlprefix) and [FormItem.imageURLSuffix](classes/FormItem.md#attr-formitemimageurlsuffix) if present. This behavior may be suppressed via [DynamicForm.showImageAsURL](classes/DynamicForm.md#attr-dynamicformshowimageasurl), in which case the value (URL or partial URL) will be rendered out as static text. |
| "imageFile" | Rendered as a [FileItem](classes/FileItem.md#class-fileitem), or a [ViewFileItem](#class-viewfileitem) if not editable |
| "binary" | Rendered as a [FileItem](classes/FileItem.md#class-fileitem), or a [ViewFileItem](#class-viewfileitem) if not editable |

### See Also

- [FormItem.type](classes/FormItem.md#attr-formitemtype)
- [FieldType](reference_2.md#type-fieldtype)

---
## Type: FormMethod

### Description
Form METHOD parameters - how the form fields are submitted to the server

### Values

| Value | Description |
|-------|-------------|
| DynamicForm.GET | GET request -- URL encoding (~4K max) |
| DynamicForm.POST | POST request -- separate field encoding (no max) |

### Groups

- submitting

---
## Type: GlobalId

### Description
An [Identifier](#type-identifier) that's unique in the global scope. For example, the [ID](classes/Canvas.md#attr-canvasid) of a [Canvas](classes/Canvas.md#class-canvas) is a `GlobalId`.

---
## Type: GroupStartOpen

### Description
Possible values for the state of ListGrid groups when groupBy is called

### Values

| Value | Description |
|-------|-------------|
| "all" | open all groups |
| "first" | open the first group |
| "none" | start with all groups closed |

---
## Type: HoverMode

### Description
When [canHover](classes/ListGrid_1.md#attr-listgridcanhover) and [showHoverComponents](classes/ListGrid_1.md#attr-listgridshowhovercomponents) are both true, HoverMode dictates the type of UI to be displayed when a user hovers over a row or cell.

There are a number of builtin HoverModes and you can override [getCellHoverComponent()](classes/ListGrid_2.md#method-listgridgetcellhovercomponent) to create your own hover behaviors.

### Values

| Value | Description |
|-------|-------------|
| "detailField" | Show a single field's value in an [HTMLFlow](classes/HTMLFlow.md#class-htmlflow). Field to use is [ListGrid.detailField](classes/ListGrid_1.md#attr-listgriddetailfield). |
| "details" | Show a [DetailViewer](classes/DetailViewer.md#class-detailviewer) displaying those fields from the record which are not already displayed in the grid. |
| "related" | Show a separate [ListGrid](classes/ListGrid_1.md#class-listgrid) containing related-records. See [ListGridRecord.detailDS](classes/ListGridRecord.md#attr-listgridrecorddetailds) and [ListGrid.recordDetailDSProperty](classes/ListGrid_1.md#attr-listgridrecorddetaildsproperty) for more information. |
| "detailRelated" | Show a [DetailViewer](classes/DetailViewer.md#class-detailviewer) displaying those fields from the record not already displayed in the grid, together with a separate [ListGrid](classes/ListGrid_1.md#class-listgrid) containing related-records. |

### Groups

- hoverComponents

---
## Type: HTML

### Description
A synonym for [HTMLString](#type-htmlstring).

**Deprecated**

---
## Type: HTMLString

### Description
A String of HTML, such as "text".

In many contexts, such as [Button.title](classes/Button.md#attr-buttontitle) and [ListGrid.formatCellValue](classes/ListGrid_2.md#method-listgridformatcellvalue), an HTML String can be specified, allowing you to use normal HTML tags and CSS to do formatting or styling.

However, bear in mind that if you attempt any kind of layout or advanced styling in such an HTML string, different browsers may render the HTML differently - use SmartClient [layout](classes/Layout.md#class-layout) and [styling](classes/Canvas.md#attr-canvasstylename) features wherever possible to avoid this. See also [CSSStyleName](#type-cssstylename).

---
## Type: Identifier

### Description
A string which is a valid JavaScript identifier, as specified by ECMA-262 Section 7.6.

Note: The [String.isValidID](classes/String.md#staticmethod-stringisvalidid) function can be used to test whether a name is a valid JavaScript identifier.

---
## Type: ImageStyle

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Canvas.CENTER | Center (and don't stretch at all) the image if smaller than its enclosing frame.CENTER:"center", |
| Canvas.TILE | Tile (repeat) the image if smaller than its enclosing frame. |
| Canvas.STRETCH | Stretch the image to the size of its enclosing frame. |
| Canvas.NORMAL | Allow the image to have natural size |

### Groups

- appearance

---
## Type: InlineEditEvent

### Description
Event that will trigger inline editing. See [EditProxy.inlineEditEvent](classes/EditProxy.md#attr-editproxyinlineeditevent).

### Values

| Value | Description |
|-------|-------------|
| "click" | A single mouse click triggers inline editing |
| "doubleClick" | A double click triggers inline editing |
| "none" | No mouse event will trigger inline editing, but it can still be triggered by a call to [EditProxy.startInlineEditing](classes/EditProxy.md#method-editproxystartinlineediting). |
| "dblOrKeypress" | A double click triggers inline editing. In addition, _if the widget is selected_, starting to type triggers inline editing. |

### Groups

- editing

---
## Type: int

### Description
A whole number, for example, 5. Decimal numbers, for example 5.5, are not allowed. May not be null.

---
## Type: JoinType

### Description
The type of join to make between two SQL tables when resolving [includeFrom](classes/DataSourceField.md#attr-datasourcefieldincludefrom) fields.

### Values

| Value | Description |
|-------|-------------|
| "inner" | A regular inner join, whereby rows are only included in the resultset where the join can be satisified, so a missing row in the table being joined to results in the entire row being omitted. |
| "outer" | An outer join. All outer joins generated by SmartClient's SQL subsystem are left outer joins, meaning that every row in the join-from (or "left") table that matches the criteria is included, and missing rows in the join-to (or "right") table cause columns to be set to null. |

### Groups

- dataSourceRelations

---
## Type: JSONDateFormat

### Description
Format for encoding dates in JSON. Note you can override [JSONEncoder.encodeDate](classes/JSONEncoder.md#method-jsonencoderencodedate) for a custom format.

### Values

| Value | Description |
|-------|-------------|
| "xmlSchema" | dates are encoded as a String in [XML Schema date format](http://www.w3.org/TR/xmlschema-2/#dateTime) in UTC, for example, "2005-08-02" for logical date fields or "2005-08-01T21:35:48.350" for `datetime` fields. See [Date format and\\n storage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information.  
**Note.**If JSON containing xmlSchema-formatted date values is passed to [JSON.decodeSafe](classes/JSON.md#classmethod-jsondecodesafe) or [JSON.decodeSafeWithDates](classes/JSON.md#classmethod-jsondecodesafewithdates), these formatted date values will not be converted to actual date objects in the generated JavaScript object. Use logicalDateString instead. |
| "dateConstructor" | dates are encoded as raw JavaScript code for creating a Date object, that is:
```
        new Date(1238792738633)
        
```
This is not strictly valid JSON, but if eval()d, will result in an identical date object, regardless of timezone. However, it does not preserve the distinction between logical dates vs full datetime values - use "logicalDateConstructor" mode for that.  
**Note.**This format does not work with [JSON.decodeSafe](classes/JSON.md#classmethod-jsondecodesafe). If you need to use [JSON.decodeSafe](classes/JSON.md#classmethod-jsondecodesafe) and/or [JSON.decodeSafeWithDates](classes/JSON.md#classmethod-jsondecodesafewithdates), you will need to use _logicalDateString_ instead. |
| "logicalDateConstructor" | serializes Date instances in a way that preserves the distinction between logical dates, logical times, and full datetime values, as explained [here](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage). Like 'dateConstructor' mode, this does not produce strictly valid JSON, and instead embeds JavaScript calls.

In addition, unlike 'dateConstructor' mode, using eval() to reconstruct the original JavaScript objects will only work in the presence of SmartClient, and not just in a generic JavaScript interpreter.  
**Note.**This format does not work with [JSON.decodeSafe](classes/JSON.md#classmethod-jsondecodesafe). If you need to use [JSON.decodeSafe](classes/JSON.md#classmethod-jsondecodesafe) and/or [JSON.decodeSafeWithDates](classes/JSON.md#classmethod-jsondecodesafewithdates), you will need to use _logicalDateString_ instead. |
| "logicalDateString" | Dates are encoded as strings in a format that [JSON.decodeSafeWithDates](classes/JSON.md#classmethod-jsondecodesafewithdates) will recognize. This allows developers to round-trip date, time and datetime values to and from strict JSON. |

---
## Type: KnobType

### Description
Entries for the [DrawItem.knobs](classes/DrawItem.md#attr-drawitemknobs) array. Each specified knobType will enable some UI allowing the user to manipulate the DrawItem directly.

**NOTE:** Not all knob types are supported by each DrawItem type. Refer to the DrawItem type's [knobs](classes/DrawItem.md#attr-drawitemknobs) attribute documentation for a list of the supported knob types.

### Values

| Value | Description |
|-------|-------------|
| "resize" | Display up to 8 control knobs at the corners specified by [DrawItem.resizeKnobPoints](classes/DrawItem.md#attr-drawitemresizeknobpoints), allowing the user to drag-resize the item. See also [DrawItem.cornerResizeKnob](classes/DrawItem.md#attr-drawitemcornerresizeknob) and [DrawItem.sideResizeKnob](classes/DrawItem.md#attr-drawitemsideresizeknob). |
| "move" | Display a control knob for moving the item around. See also [DrawItem.moveKnobPoint](classes/DrawItem.md#attr-drawitemmoveknobpoint) and [DrawItem.moveKnobOffset](classes/DrawItem.md#attr-drawitemmoveknoboffset) |
| "startPoint" | Control knob to manipulate [DrawLine.startPoint](classes/DrawLine.md#attr-drawlinestartpoint). |
| "endPoint" | Control knob to manipulate [DrawLine.endPoint](classes/DrawLine.md#attr-drawlineendpoint). |
| "controlPoint1" | Display a draggable control knob along with a DrawLine indicating the angle between controlPoint1 and the startPoint. Dragging the knob will adjust controlPoint1. |
| "controlPoint2" | Display a draggable control knob along with a DrawLine indicating the angle between controlPoint2 and the endPoint. Dragging the knob will adjust controlPoint2. |
| "rotate" | Display a rotation knob above the top resize knob, allowing the user to rotate the item. See also [DrawItem.rotateKnob](classes/DrawItem.md#attr-drawitemrotateknob). |

---
## Type: LabelCollapseMode

### Description
Strategy to apply when there is too little room for labels to be shown for all data points with comfortable padding ([FacetChart.minLabelGap](classes/FacetChart.md#attr-facetchartminlabelgap)).

### Values

| Value | Description |
|-------|-------------|
| "none" | Show all labels regardless, even though they will overlap |
| "time" | Show significant time values such as the first day of the month or week. Data values in Records must be true Date objects, not Strings. |
| "numeric" | Pick round numbers in the range and show labels for just those numbers. Best for continuous datasets that are not time-based |
| "sample" | Pick periodic values from the dataset and show labels for those. Best when the there are no particular points that would clearly be the best to label |

---
## Type: LayoutResizeBarPolicy

### Description
Policy for whether resize bars are shown on members by default.

### Values

| Value | Description |
|-------|-------------|
| "marked" | resize bars are only shown on members marked [showResizeBar:true](classes/Canvas.md#attr-canvasshowresizebar) |
| "middle" | resize bars are shown on all resizable members that are not explicitly marked showResizeBar:false, except the last member. Appropriate for a [LayoutPolicy](reference_2.md#type-layoutpolicy) of "fill" (VLayout, HLayout) since the overall space will always be filled. |
| "all" | resize bars are shown on all resizable members that are not explicitly marked showResizeBar:false, including the last member. Can be appropriate for a [LayoutPolicy](reference_2.md#type-layoutpolicy) of "none" (VStack, HStack) since the overall size of the layout is dictated by it's member's sizes. |
| "none" | resize bars are not shown even if members are marked with [showResizeBar:true](classes/Canvas.md#attr-canvasshowresizebar) |

---
## Type: LegendAlign

### Description
Supported positioning of the chart Legend.

### Values

| Value | Description |
|-------|-------------|
| "left" | Align to the left of the legend section |
| "center" | Align centrally in the legend section |
| "right" | Align to the right of the legend section |

### Groups

- legend

---
## Type: LineBreakStyle

### Description
The style of line-breaks to use when exporting data

### Values

| Value | Description |
|-------|-------------|
| "default" | Use the default line-break style of the server OS |
| "unix" | Use UNIX-style line-breaks (LF only) |
| "mac" | Use MAC-style line-breaks (CR only) |
| "dos" | Use DOS-style line-breaks (both CR & LF) |

---
## Type: LineCap

### Description
Supported styles of drawing the endpoints of a line

### Values

| Value | Description |
|-------|-------------|
| "round" | Semicircular rounding |
| "square" | Squared-off endpoint |
| "butt" | Square endpoint, stops exactly at the line's end coordinates instead of extending 1/2 lineWidth further as "round" and "square" do |

### Groups

- line

---
## Type: LinePattern

### Description
Supported styles of drawing lines.

### Values

| Value | Description |
|-------|-------------|
| "solid" | Solid line |
| "dot" | Dotted line |
| "dash" | Dashed line |
| "shortdot" | Dotted line, with more tightly spaced dots |
| "shortdash" | Dashed line, with shorter, more tightly spaced dashes |
| "longdash" | Dashed line, with longer, more widely spaced dashes |

### Groups

- line

---
## Type: LinkDataFetchMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "separate" | In this mode, link data is fetched from the [ResultTree.linkDataSource](classes/ResultTree.md#attr-resulttreelinkdatasource) and nodes are separately fetched from the [ResultTree.dataSource](classes/ResultTree.md#attr-resulttreedatasource). The two fetches are sent together in a [queue](classes/RPCManager.md#classmethod-rpcmanagerstartqueue), with the link data fetch first and the separate node fetch second. This makes it possible for your server-side code to use the results of the link data fetch to constrain the node fetch (ie, only fetch node information for nodes that appear in a link) |
| "single" | In this mode, nodes and link data are fetched together from the main [ResultTree.dataSource](classes/ResultTree.md#attr-resulttreedatasource), and any duplicated node IDs are handled by creating multiple links to a single node. In this mode, the [ResultTree.linkDataSource](classes/ResultTree.md#attr-resulttreelinkdatasource) is only used for update operations.

Note that the end result of a "single" fetch is exactly the same as fetching link data and nodes separately using "separate" mode; "separate" mode is also conceptually clearer since it emphasises the fact that nodes and link data are separate things. We provide "single" mode because, in some cases, it may be more efficient to fetch the two types of data together in a single database fetch, using [DataSourceField.includeFrom](classes/DataSourceField.md#attr-datasourcefieldincludefrom) or some other kind of join technique on the server. |

---
## Type: ListGridEditEvent

### Description
Event that will trigger inline editing.

### Values

| Value | Description |
|-------|-------------|
| "click" | A single mouse click triggers inline editing |
| "doubleClick" | A double click triggers inline editing |
| "none" | No mouse event will trigger editing. Editing must be programmatically started via [ListGrid.startEditing](classes/ListGrid_2.md#method-listgridstartediting) (perhaps from an external button) or may be triggered by keyboard navigation if [ListGrid.editOnFocus](classes/ListGrid_1.md#attr-listgrideditonfocus) is set. |

### Groups

- editing

---
## Type: ListGridFieldType

### Description
ListGrids format data for viewing and editing based on the _type_ attribute of the field. This table describes how the ListGrid deals with the various built-in types.

### Values

| Value | Description |
|-------|-------------|
| "text" | Simple text rendering for view. For editing a text entry field is shown. If the length of the field (as specified by the [DataSourceField.length](classes/DataSourceField.md#attr-datasourcefieldlength) attribute) is larger than the value specified by [ListGrid.longTextEditorThreshold](classes/ListGrid_1.md#attr-listgridlongtexteditorthreshold), a text input icon is shown that, when clicked on (or field is focused in) opens a larger editor that expands outside the boundaries of the cell (textarea by default, but overrideable via [ListGrid.longTextEditorType](classes/ListGrid_1.md#attr-listgridlongtexteditortype)). |
| "boolean" | For viewing and editing a checkbox is shown with a check mark for the `true` value and no check mark for the `false` value. This behavior may be suppressed by setting [ListGridField.suppressValueIcon](classes/ListGridField.md#attr-listgridfieldsuppressvalueicon) for the field. See [ListGrid.booleanTrueImage](classes/ListGrid_1.md#attr-listgridbooleantrueimage) for customization. |
| "integer" | A whole number, e.g. `123`. Consider setting [editorType](classes/ListGridField.md#attr-listgridfieldeditortype) to use a [SpinnerItem](classes/SpinnerItem.md#class-spinneritem). |
| "float" | A floating point (decimal) number, e.g. `1.23`. Consider setting [editorType](classes/ListGridField.md#attr-listgridfieldeditortype) to use a [SpinnerItem](classes/SpinnerItem.md#class-spinneritem). |
| "date" | Field value should be a `Date` instance representing a logical date, with no time of day information. See [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for details of the logical date type and how it is represented and manipulated.

Dates will be formatted using [ListGridField.dateFormatter](classes/ListGridField.md#attr-listgridfielddateformatter) if specified, otherwise [ListGrid.dateFormatter](classes/ListGrid_1.md#attr-listgriddateformatter). If both these attributes are unset, dates are formatted using the standard [short display format](classes/DateUtil.md#classmethod-dateutilsetshortdisplayformat) for dates.

For editing, by default a [DateItem](classes/DateItem.md#class-dateitem) is used with [DateItem.useTextField](classes/DateItem.md#attr-dateitemusetextfield) set to true, providing textual date entry plus a pop-up date picker. The [dateFormatter](classes/DateItem.md#attr-dateitemdateformatter) and [inputFormat](classes/DateItem.md#attr-dateiteminputformat) for the editor will be picked up from the ListGridField, if specified. |
| "time" | Field value should be a `Date` instance representing a logical time, meaning time value that does not have a specific day and also has no timezone. See [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for details of the logical time type and how it is represented and manipulated.

Times will be formatted using [ListGridField.timeFormatter](classes/ListGridField.md#attr-listgridfieldtimeformatter) if specified, otherwise [ListGrid.timeFormatter](classes/ListGrid_1.md#attr-listgridtimeformatter).

If both these attributes are unset, times are formatted using the standard [short display format](classes/Time.md#classattr-timeshortdisplayformat) for times.

For editing, by default a [TimeItem](classes/TimeItem.md#class-timeitem) is used. The [timeFormatter](classes/TimeItem.md#attr-timeitemtimeformatter) for the editor will be picked up from the ListGridField, if specified. |
| "datetime" | Field value should be a `Date` instance representing a specific date and time value. See [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for details of the datetime type and how it is represented and manipulated.

Dates will be formatted using [ListGridField.dateFormatter](classes/ListGridField.md#attr-listgridfielddateformatter) if specified, otherwise [ListGrid.datetimeFormatter](classes/ListGrid_1.md#attr-listgriddatetimeformatter). If both these attributes are unset, dates are formatted using the standard [short display format](classes/DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat) for datetime values.

For editing, by default a [DateTimeItem](classes/DateTimeItem.md#class-datetimeitem) is used, providing textual date entry plus a pop-up date picker. The [dateFormatter](classes/DateItem.md#attr-dateitemdateformatter) and [inputFormat](classes/DateItem.md#attr-dateiteminputformat) for the editor will be picked up from the ListGridField, if specified. |
| "sequence" | Same as `text` |
| "link" | Renders a clickable html link (using an HTML anchor tag: `<A>`). The target URL is the value of the field, which is also the default display value. You can override the display value by setting [ListGridRecord.linkText](classes/ListGridRecord.md#attr-listgridrecordlinktext) or [ListGridField.linkText](classes/ListGridField.md#attr-listgridfieldlinktext).

Clicking the link opens the URL in a new window by default. To change this behavior, you can set `field.target`, which works identically to the "target" attribute on an HTML anchor (`<A>`) tag. See [ListGridField.target](classes/ListGridField.md#attr-listgridfieldtarget) for more information.

In inline edit mode, this type works like a text field.

To create a link not covered by this feature, consider using [ListGridField.formatCellValue](classes/ListGridField.md#method-listgridfieldformatcellvalue) along with [Canvas.linkHTML](classes/Canvas.md#method-canvaslinkhtml), or simply [styling the field](classes/ListGrid_2.md#method-listgridgetcellstyle) to look like a link, and providing interactivity via [field.recordClick()](classes/ListGridField.md#method-listgridfieldrecordclick). |
| "image" | Renders a different image in each row based on the value of the field. If this URL is not absolute, it is assumed to be relative to [ListGridField.imageURLPrefix](classes/ListGridField.md#attr-listgridfieldimageurlprefix) if specified. The size of the image is controlled by [ListGridField.imageSize](classes/ListGridField.md#attr-listgridfieldimagesize), [ListGridField.imageWidth](classes/ListGridField.md#attr-listgridfieldimagewidth), [ListGridField.imageHeight](classes/ListGridField.md#attr-listgridfieldimageheight) (and by the similarly-named global default attributes on the ListGrid itself).

You can also specify the following attributes on the field: `activeAreaHTML`, and `extraStuff` - these are passed to [Canvas.imgHTML](classes/Canvas.md#method-canvasimghtml) to generate the final URL.

Note if you want to display icons **in addition to** the normal cell value, you can use [valueIcons](classes/ListGridField.md#attr-listgridfieldvalueicons) instead. |
| "icon" | Shows [field.icon](classes/ListGridField.md#attr-listgridfieldicon) in every cell, and also in the header. Useful for a field that is used as a button, for example, launches a detail window or removes a row. Implement a [field.recordClick](classes/ListGridField.md#method-listgridfieldrecordclick) to define a behavior for the button.

NOTE: for a field that shows different icons depending on the field value, see [ListGridField.valueIcons](classes/ListGridField.md#attr-listgridfieldvalueicons).

`type:"icon"` also defaults to a small field width, accommodating just the icon with padding, and to a blank header title, so that the header shows the icon only.

[field.iconWidth](classes/ListGridField.md#attr-listgridfieldiconwidth) and related properties configure the size of the icon both in the header and in body cells.

If you want the icon to appear only in body cells and not in the header, set [field.cellIcon](classes/ListGridField.md#attr-listgridfieldcellicon) instead, leaving field.icon null. |
| "binary" | For viewing, the grid renders a 'view' icon (looking glass) followed by a 'download' icon and then the name of the file is displayed in text. If the user clicks the 'view' icon, a new browser window is opened and the file is streamed to that browser instance, using [DataSource.viewFile](classes/DataSource.md#method-datasourceviewfile). For images and other file types with known handlers, the content is typically displayed inline - otherwise the browser will ask the user how to handle the content. If the download icon is clicked, [DataSource.downloadFile](classes/DataSource.md#method-datasourcedownloadfile) is used to cause the browser to show a "save" dialog. There is no inline editing mode for this field type. |
| "imageFile" | Same as `binary` |
| "summary" | Show a calculated summary based on other field values within the current record. See [ListGridField.recordSummaryFunction](classes/ListGridField.md#attr-listgridfieldrecordsummaryfunction) for more information |
| "any" | Fields of this type can contain any data value and have no default formatting or validation behavior. This is useful as the [parent type](classes/SimpleType.md#attr-simpletypeinheritsfrom) for SimpleTypes where you do not want any of the standard validation or formatting logic to be inherited from the standard built-in types. |
| "localeInt" | An integer number with locale-based formatting, e.g. `12,345,678`. See [Localized Number Formatting](#kb-topic-localized-number-formatting) for more info. |
| "localeFloat" | A float number with locale-based formatting, e.g. `12,345.67`. See [Localized Number Formatting](#kb-topic-localized-number-formatting) for more info. |
| "localeCurrency" | A float number with locale-based formatting and using currency symbol, e.g. `$12,345.67`. See [Localized Number Formatting](#kb-topic-localized-number-formatting) for more info. |
| "phoneNumber" | A telephone number. Uses [FormItem.browserInputType](classes/FormItem.md#attr-formitembrowserinputtype) "tel" to hint to the device to restrict input. On most mobile devices that have software keyboards, this cause a specialized keyboard to appear which only allows entry of normal phone numbers. When displayed read-only, a "phoneNumber" renders as an HTML link with the "tel:" URL scheme, which will invoke the native phone dialing interface on most mobile devices. In addition, the CSS style "sc\_phoneNumber" is applied.

By default, "phoneNumber" fields do not include validators, however the following validator definition would limit to digits, dashes and the "+" character: xml:

`<validator type="regexp" expression="^(\\(?\\+?\[0-9\]\*\\)?)?\[0-9\_\\- \\(\\)\]\*$" errorMessage="Phone number should be in the correct format e.g. +#(###)###-##-##" />`

or directly in JavaScript:

```
 {type:"regexp", expression:"^(\\(?\\+?[0-9]*\\)?)?[0-9_\\- \\(\\)]*$", 
     errorMessage:"Phone number should be in the correct format e.g. +#(###)###-##-##"}
 
```
and adding "#" and "\*" to the regular expressions above would allow for users to enter special keys sometimes used for extension numbers or pauses |

### See Also

- [ListGridField.type](classes/ListGridField.md#attr-listgridfieldtype)
- [FieldType](reference_2.md#type-fieldtype)

---
## Type: ListGridGroupState

### Description
An object containing the stored grouping information for a listGrid. Note that this object is not intended to be interrogated directly, but may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: ListGridSortState

### Description
An object containing the stored sort information for a listGrid. Note that this object is not intended to be interrogated directly, but may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: ListGridViewStatePart

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "all" | All parts of the view state |
| "group" | Group state |
| "field" | Field state |
| "selected" | Selected state |
| "sort" | Sort state |
| "hilite" | Hilite state |
| "userCriteria" | Criteria state |

### Groups

- viewState

---
## Type: LocatorTypeStrategy

### Description
When attempting to identify a component from within a list of possible candidates as described [here](reference_2.md#type-locatorstrategy), if we are unable to find a unique match by name or title, we will use the recorded "type" of the component to verify an apparent match.

By default we check the following properties in order:

*   Does the Class match?
*   If this is not a [framework class](classes/Class.md#classattr-classisframeworkclass), does the core framework superclass match?
*   Does the `role` match?

In some cases an explicit locatorTypeStrategy can be specified to modify this behavior. As with [LocatorStrategy](reference_2.md#type-locatorstrategy), if we are unable to match using the specified type strategy we continue to test against the remaining strategies in order - so if a type strategy of "scClass" was specified but we were unable to find a match with the appropriate core superclass, we will attempt to match by role. Possible values are:

### Values

| Value | Description |
|-------|-------------|
| "Class" | Match by class if possible |
| "scClass" | Ignore specific class and match by the SmartClient framework superclass. |
| "role" | Ignore class altogether and attempt to match by role |
| "none" | Don't attempt to compare type in any way |

### Groups

- autoTest

### See Also

- [LocatorStrategy](reference_2.md#type-locatorstrategy)

---
## Type: LogPriority

### Description
Priority levels for log messages

### Values

| Value | Description |
|-------|-------------|
| Log.FATAL | unrecoverable error |
| Log.ERROR | error, may be recoverable |
| Log.WARN | apparent problem, misused API, partial result |
| Log.INFO | significant events in normal operation |
| Log.DEBUG | diagnostics for developers |

### See Also

- [Class.logDebug](classes/Class.md#method-classlogdebug)

---
## Type: MaxStackDismissMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "oldest" | dismiss the oldest message |
| "countdown" | dismiss the message with least time left |

---
## Type: MenuFieldID

### Description
Simple string identifiers for standard menu fields.

### Values

| Value | Description |
|-------|-------------|
| "icon" | Displays the icon field for the menu. This field contains the item's specified icon (if there is one), or if the item is checked, the checkmark icon for the item. |
| "title" | Displays the item's title |
| "key" | Displays the key field for the menu. This field contains the name or title of any shortcut keys for this menu item. |
| "subMenu" | Field to display the submenu image for items that have a submenu. |

---
## Type: MessagePriority

### Description
A positive integer representing the priority of a message. Lower numerical values have higher priority.

### See Also

- [NotifySettings.messagePriority](classes/NotifySettings.md#attr-notifysettingsmessagepriority)

---
## Type: MockDataType

### Description
Whether the mock data is for a flat grid-like dataset or for a tree. If "grid" is specified, text shortcuts that would cause a hierarchy to be created (such as starting a line with "\[+\]") will not have special meaning and be considered to be just a normal data value.

### Values

| Value | Description |
|-------|-------------|
| "grid" | Mock data for a ListGrid |
| "tree" | Mock data for a TreeGrid |

---
## Type: MockDSExportFormat

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "reifyCSV" | export as Reify-specific CSV |
| "xmlMockDS" | serialize as XML |
| "jsMockDS" | serialize as JavaScript |

---
## Type: MultiAutoChild

### Description
—

### See Also

- [multiAutoChildren](#kb-topic-multiautochildren)

---
## Type: MultiPickerSelectionStyle

### Description
Governs whether a [MultiPickerItem](classes/MultiPickerItem.md#class-multipickeritem) displays selected and unselected option in a drop down pickList, or uses a [shuttle interface](classes/Shuttle.md#class-shuttle)

### Values

| Value | Description |
|-------|-------------|
| "pickList" | Options will be displayed in a [PickList](reference_2.md#interface-picklist) |
| "shuttle" | Options will be displayed in a [Shuttle](classes/Shuttle.md#class-shuttle) |
| "pickTree" | Options will be displayed in a [TreeGrid](classes/TreeGrid.md#class-treegrid). Only suitable for hierarchical data. |

---
## Type: MultipleAppearance

### Description
Appearance for a SelectItem that allows multiple selection

### Values

| Value | Description |
|-------|-------------|
| "picklist" | a drop-down picklist that allows multiple choices by clicking on a checkbox next to each item |
| "grid" | a grid that displays all items in-place. Multiple selection is accomplished by ctrl-click or shift-click. |

---
## Type: MultipleFieldStorage

### Description
Options for how values are stored for a field that is [multiple:true](classes/ListGridField.md#attr-listgridfieldmultiple). See [DataSourceField.multipleStorage](classes/DataSourceField.md#attr-datasourcefieldmultiplestorage).

### Values

| Value | Description |
|-------|-------------|
| "simpleString" | values are saved as a simple delimeter-separated string. Delimeter can be configured via [DataSourceField.multipleStorageSeparator](classes/DataSourceField.md#attr-datasourcefieldmultiplestorageseparator). An empty array is stored as "", and null as the database `null` value. |
| "json" | values are serialized to JSON. Empty array as a distinct value from null (it appears as the text "\[\]"). |
| "none" | no transformation is applied to values; server-side field value remains a Java List when passed to the execute(Fetch|Add|Update|Remove) method of the server-side DataSource class |

### Groups

- multipleField

---
## Type: MultiUpdatePolicy

### Description
Controls when primary keys are required for "update" and "remove" server operations, when allowMultiUpdate has not been explicitly configured on either the [operationBinding.allowMultiUpdate](classes/OperationBinding.md#attr-operationbindingallowmultiupdate) or via the server-side API `DSRequest.setAllowMultiUpdate()`.

### Values

| Value | Description |
|-------|-------------|
| "never" | having a PK is never required, even for requests from a browser. Note: dangerous setting that allows end users to wipe out entire tables |
| "clientRequest" | having a PK is required for requests that come from the client or are specifically marked via dsRequest.setClientRequest(true) |
| "rpcManager" | having a PK is required for any request that is associated with an RPCManager, which includes clientRequests and server-created DSRequests where an RPCManager was explicitly provided |
| "always" | having a PK is always required no matter what |

### See Also

- [DataSource.defaultMultiUpdatePolicy](classes/DataSource.md#attr-datasourcedefaultmultiupdatepolicy)
- [OperationBinding.allowMultiUpdate](classes/OperationBinding.md#attr-operationbindingallowmultiupdate)

---
## Type: NavigationDirection

### Description
Navigation direction.

### Values

| Value | Description |
|-------|-------------|
| "back" | Back |
| "forward" | Forward |
| "none" | none |

---
## Type: NavigationMode

### Description
Controls the navigation mode of records.

### Values

| Value | Description |
|-------|-------------|
| TableView.WHOLE_RECORD | Clicking anywhere on the record navigates |
| TableView.NAVICON_ONLY | Only clicking directly on the navigation icon triggers navigation |

---
## Type: NotifyTransition

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "slide" | message slide-animates onto or off of the screen |
| "fade" | message appears or disappears via a fade effect |
| "instant" | message instantly appears or disappears |

---
## Type: NullAccessType

### Description
The possible access types for records with a null [ownerIdField](classes/DataSource.md#attr-datasourceowneridfield) (only applicable if `ownerIdField` is specified)

### Values

| Value | Description |
|-------|-------------|
| "none" | The default value, means that users have no access to records with a null `ownerIdField`. In this case, users can only see their own records (ie, those where the `ownerIdField` matches the currently authenticaed user's id) |
| "view" | Users are allowed read-only access to records with a null `ownerIdField`. In this case, users can see records with a null owner as well as their own records. |
| "edit" | Users are allowed read, update and delete access to records with a null `ownerIdField`. In this case, users can see and fully manage records with a null owner, as well as their own records. |

### See Also

- [DataSource.ownerIdField](classes/DataSource.md#attr-datasourceowneridfield)
- [DataSource.ownerIdNullAccess](classes/DataSource.md#attr-datasourceowneridnullaccess)
- [DataSource.ownerIdNullRole](classes/DataSource.md#attr-datasourceowneridnullrole)

---
## Type: Object

### Description
An ordinary JavaScript as obtained by "new Object()" or via [Object Literal](#type-objectliteral) syntax.

Methods that return Objects or take Objects as parameters make use of the ability of a JavaScript Object to contain an arbitrary set of named properties, without requiring declaration in advance. This capability makes it possible to use a JavaScript Object much like a HashMap in Java or .NET, but without the need to call get() or set() to create and retrieve properties.

For example if you created an Object using [Object Literal](#type-objectliteral) syntax like so:

```
    var request = {
        actionURL : "/foo.do",
        showPrompt:false
    };
 
```
You could then access it's properties like so:
```
    var myActionURL = request.actionURL;
    var myShowPrompt = request.showPrompt;
 
```
.. and you could assign new values to those properties like so:
```
    request.actionURL = "newActionURL";
    request.showPrompt = newShowPromptSetting;
 
```
Note that while JavaScript allows you to get and set properties in this way on any Object, SmartClient components require that if a setter or getter exists, it must be called, or no action will occur. For example, if you had a [ListGrid](classes/ListGrid_1.md#class-listgrid) and you wanted to change the [showHeader](classes/ListGrid_1.md#attr-listgridshowheader) property:
```
     myListGrid.setShowHeader(false); // correct
     myListGrid.showHeader = false; // incorrect (nothing happens)
 
```
All documented attributes have [flags](#kb-topic-flag-abbreviations) (eg IRW) that indicate when direct property access is allowed or not.

---
## Type: ObjectLiteral

### Description
An "Object literal" is JavaScript shorthand for defining a JavaScript Object with a set of properties. For example, code like this:
```
    var request = {
        actionURL : "/foo.do",
        showPrompt:false
    };
```
.. is equivalent to ..
```
    var request = new Object();
    request.actionURL = "/foo.do";
    request.showPrompt = false;
```
In situations where a set of [properties](#type-properties) may be passed to a method, the Object literal notation is much more compact. For example:
```
    isc.RPCManager.sendRequest({
        actionURL : "/foo.do",
        showPrompt:false
    });
```
**NOTE:** if you have a 'trailing comma' in an object literal, like so:
```
    var request = {
        actionURL : "/foo.do",
        showPrompt:false, // TRAILING COMMA
    };
```
This is considered a syntax error by Internet Explorer, but not by Firefox. This is by far the #1 cause of Internet Explorer-specific errors that do not occur in other browsers. Pay special attention to this error, and, if you can, install the JSSyntaxScannerFilter into your development environment (as described in the [deployment instructions](kb_topics/iscInstall.md#kb-topic-installing-the-smartclient-runtime)).

---
## Type: OperatorId

### Description
An operator is used as part of a [Criterion](reference_2.md#object-criterion) when specifying [AdvancedCriteria](#object-advancedcriteria).

This list of operators indicates the set of operators built into SmartClient DataSources, which can be used for both client and server-side filtering. Some operators offer case-insensitive versions, prefixed with a lower-case _i_, such as `iContains`. **Note that such operators are intended for text-based searches and are not available to numeric or date fields (integer/float/date/datetime and derivatives), where there is no use for case.**

You can extend the list of operators with [DataSource.addSearchOperator](classes/DataSource.md#method-datasourceaddsearchoperator).

### Values

| Value | Description |
|-------|-------------|
| "equals" | exactly equal to |
| "notEqual" | not equal to |
| "iEquals" | exactly equal to, if case is disregarded |
| "iNotEqual" | not equal to, if case is disregarded |
| "greaterThan" | Greater than |
| "lessThan" | Less than. Note that `null` is treated as equivalent to an arbitrarily small value, so null field values will always be returned by `lessThan` / `lessOrEqual` filter operations by default. |
| "greaterOrEqual" | Greater than or equal to |
| "lessOrEqual" | Less than or equal to |
| "contains" | Contains as sub-string (match case) |
| "startsWith" | Starts with (match case) |
| "endsWith" | Ends with (match case) |
| "iContains" | Contains as sub-string (case insensitive) |
| "iStartsWith" | Starts with (case insensitive) |
| "iEndsWith" | Ends with (case insensitive) |
| "notContains" | Does not contain as sub-string (match case) |
| "notStartsWith" | Does not start with (match case) |
| "notEndsWith" | Does not end with (match case) |
| "iNotContains" | Does not contain as sub-string (case insensitive) |
| "iNotStartsWith" | Does not start with (case insensitive) |
| "iNotEndsWith" | Does not end with (case insensitive) |
| "iBetween" | shortcut for "greaterThan" + "and" + "lessThan" (case insensitive) |
| "iBetweenInclusive" | shortcut for "greaterOrEqual" + "and" + "lessOrEqual" (case insensitive) |
| "matchesPattern" | Basic GLOB matching using wildcards (see [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "iMatchesPattern" | Basic GLOB matching using wildcards (case insensitive) (see [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "containsPattern" | GLOB matching using wildcards. Value is considered to meet the criterion if it contains the pattern. See [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "startsWithPattern" | GLOB matching using wildcards. Value is considered to meet the criterion if it starts with the pattern.See [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "endsWithPattern" | GLOB matching using wildcards. Value is considered to meet the criterion if it starts with the pattern.See [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "iContainsPattern" | GLOB matching using wildcards. Value is considered to meet the criterion if it contains the pattern. Matching is case insensitive. See [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "iStartsWithPattern" | GLOB matching using wildcards. Value is considered to meet the criterion if it starts with the pattern. Matching is case insensitive.See [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "iEndsWithPattern" | GLOB matching using wildcards.Value is considered to meet the criterion if it ends with the pattern. Matching is case insensitive. See [DataSource.translatePatternOperators](classes/DataSource.md#attr-datasourcetranslatepatternoperators) for more information on available patterns) |
| "regexp" | Regular expression match - built-in SQL only, JPA and Hibernate do not support regexp operator. Additionally, when using PostgreSQL, it is supported only starting from PostgreSQL version 9.3. |
| "iregexp" | Regular expression match (case insensitive) - regexp operator limitations apply. |
| "isBlank" | value is either null or the empty string. For numeric fields it behaves as isNull |
| "notBlank" | value is neither null nor the empty string ("") |
| "isNull" | value is null |
| "notNull" | value is non-null. Note empty string ("") is non-null |
| "inSet" | value is in a set of values. Specify criterion.value as an Array |
| "notInSet" | value is not in a set of values. Specify criterion.value as an Array |
| "equalsField" | matches another field (match case, specify fieldName as criterion.value) |
| "notEqualField" | does not match another field (match case, specify fieldName as criterion.value) |
| "iEqualsField" | matches another field (case insensitive, specify fieldName as criterion.value) |
| "iNotEqualField" | does not match another field (case insensitive, specify fieldName as criterion.value) |
| "greaterThanField" | Greater than another field (specify fieldName as criterion.value) |
| "lessThanField" | Less than another field (specify fieldName as criterion.value) |
| "greaterOrEqualField" | Greater than or equal to another field (specify fieldName as criterion.value) |
| "lessOrEqualField" | Less than or equal to another field (specify fieldName as criterion.value) |
| "containsField" | Contains as sub-string (match case) another field value (specify fieldName as criterion.value) |
| "startsWithField" | Starts with (match case) another field value (specify fieldName as criterion.value) |
| "endsWithField" | Ends with (match case) another field value (specify fieldName as criterion.value) |
| "iContainsField" | Contains as sub-string (case insensitive) another field value (specify fieldName as criterion.value) |
| "iStartsWithField" | Starts with (case insensitive) another field value (specify fieldName as criterion.value) |
| "iEndsWithField" | Ends with (case insensitive) another field value (specify fieldName as criterion.value) |
| "notContainsField" | Does not contain as sub-string (match case) another field value (specify fieldName as criterion.value) |
| "notStartsWithField" | Does not start with (match case) another field value (specify fieldName as criterion.value) |
| "notEndsWithField" | Does not end with (match case) another field value (specify fieldName as criterion.value) |
| "iNotContainsField" | Does not contain as sub-string (case insensitive) another field value (specify fieldName as criterion.value) |
| "iNotStartsWithField" | Does not start with (case insensitive) another field value (specify fieldName as criterion.value) |
| "iNotEndsWithField" | Does not end with (case insensitive) another field value (specify fieldName as criterion.value) |
| "and" | all subcriteria (criterion.criteria) are true |
| "not" | all subcriteria (criterion.criteria) are false |
| "or" | at least one subcriteria (criterion.criteria) is true |
| "between" | shortcut for "greaterThan" + "lessThan" + "and". Specify criterion.start and criterion.end |
| "betweenInclusive" | shortcut for "greaterOrEqual" + "lessOrEqual" + "and". Specify criterion.start and criterion.end |

### Groups

- advancedFilter

---
## Type: Overflow

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Canvas.VISIBLE | Content that extends beyond the widget's width or height is displayed. Note: To have the content be sized only by the drawn size of the content set the overflow to be Canvas.VISIBLE and specify a small size, allowing the size to expand to the size required by the content. Leaving the width / height for the widget undefined will use the default value of 100, and setting the size to zero may cause the widget not to draw. |
| Canvas.HIDDEN | Content that extends beyond the widget's width or height is clipped (hidden). |
| Canvas.AUTO | Horizontal and/or vertical scrollbars are displayed only if necessary. Content that extends beyond the remaining visible area is clipped. |
| Canvas.SCROLL | Horizontal and vertical scrollbars are always drawn inside the widget. Content that extends beyond the remaining visible area is clipped, and can be accessed via scrolling. |
| Canvas.CLIP_H | Clip horizontally but extend the canvas's clip region vertically if necessary.  
**Note:** only supported for specific widget subclasses. |
| Canvas.CLIP_V | Clip vertically but extend the canvas's clip region horizontally if necessary.  
**Note:** only supported for specific widget subclasses. |

### Groups

- sizing

---
## Type: PageOrientation

### Description
Is this page being viewed in landscape or portrait orientation? Typically used with mobile devices.

### Values

| Value | Description |
|-------|-------------|
| "landscape" | Landscape orientation: page is wider than it is tall. |
| "portrait" | Portrait orientation: page is taller than it is wide. |

---
## Type: PercentBoxModel

### Description
Determines sizing model when sizing / positioning a canvas relative to its [percentBox](classes/Canvas.md#attr-canvaspercentbox).

### Values

| Value | Description |
|-------|-------------|
| "visible" | use coordinates relative to the [drawn height](classes/Canvas.md#method-canvasgetvisibleheight) and width of the other canvas |
| "viewport" | use coordinates relative to the [drawn viewport height](classes/Canvas.md#method-canvasgetviewportheight) and width of the other canvas |
| "specified" | use coordinates relative to the [specified height](classes/Canvas.md#method-canvasgetheight) and width of the other canvas. For [overflow:"visible"](classes/Canvas.md#attr-canvasoverflow) canvases this may be smaller than drawn size. |
| "inner" | use coordinates relative to the [specified inner height](classes/Canvas.md#method-canvasgetinnerheight) and width of the other canvas |

---
## Type: PickerIconName

### Description
Standard pickers

### Values

| Value | Description |
|-------|-------------|
| "clear" | Picker icon to clear a field value. |
| "search" | Picker icon to start a search. |
| "refresh" | Picker icon to refresh a value. |
| "date" | Picker icon for date value. |
| "comboBox" | Picker icon for a general combobox. |

---
## Type: PickListItemIconPlacement

### Description
For PickList items with [PickListItemIconPlacement](#type-picklistitemiconplacement) set such that the pickList does not render near-origin, possible location for rendering formItemIcons.

### Values

| Value | Description |
|-------|-------------|
| "pickerNavigationBar" | icon will be displayed in the [pickerNavigationBar](classes/ComboBoxItem.md#attr-comboboxitempickernavigationbar) only (and not rendered inline within the formItem itself) |
| "formItem" | icon will be displayed inline within the form item itself (and not within the [pickerNavigationBar](classes/ComboBoxItem.md#attr-comboboxitempickernavigationbar) |
| "both" | icon will be displayed both inline (within the form item itself) and within the [pickerNavigationBar](classes/ComboBoxItem.md#attr-comboboxitempickernavigationbar) |

---
## Type: PointShape

### Description
Supported data point shapes for [FacetChart.pointShapes](classes/FacetChart.md#attr-facetchartpointshapes) are:

### Values

| Value | Description |
|-------|-------------|
| Oval | — |
| Square | — |
| Diamond | — |
| Triangle | — |

---
## Type: PositiveInteger

### Description
A positive whole number or 0, for example, 5. Negative values are not allowed. Null is allowed.

---
## Type: PreserveOpenState

### Description
—

### Values

| Value | Description |
|-------|-------------|
| never | Never try to automatically preserve the openState. Nodes will be initially open or closed based solely on the [Tree.openProperty](classes/Tree.md#attr-treeopenproperty) optionally set by the server. |
| whenUnique | If either the [Tree.idField](classes/Tree.md#attr-treeidfield) or [Tree.nameProperty](classes/Tree.md#attr-treenameproperty) has been set on the Tree, (so that nodes have either unique ids or unique paths), preserve openState by respecting the [Tree.openProperty](classes/Tree.md#attr-treeopenproperty) set by the server, then applying the openState. |
| always | Like "whenUnique" but automatically preserves openState even if nodes cannot be uniquely identified. This means that nodes at the same tree positions (eg 3rd child of 5th node under root) will be placed in the same openState, regardless of whether that node has anything to do with the node that previously was at that tree position. |

---
## Type: Properties

### Description
When the type for a parameter mentions "properties" as in "ListGrid Properties" or "RPCRequest Properties", it means that the expected value is a JavaScript Object containing any set of properties generally legal when creating an object of that type.

For example, the first parameter of [RPCManager.sendRequest](classes/RPCManager.md#classmethod-rpcmanagersendrequest) is of type "RPCRequest Properties". This means it should be called like:

```
    isc.RPCManager.sendRequest({
        actionURL : "/foo.do",
        showPrompt:false
    });
```
[actionURL](classes/RPCRequest.md#attr-rpcrequestactionurl) and [showPrompt](classes/RPCRequest.md#attr-rpcrequestshowprompt) are properties of [RPCRequest](#object-rpcrequest).

Note that the notation shown above is an example of a [JavaScript object literal](#type-objectliteral).

---
## Type: PropertyIdentifier

### Description
A means of identifying the properties in an exported dataset - either the property name or its title.

### Values

| Value | Description |
|-------|-------------|
| "name" | Identify properties by internal name |
| "title" | Identify properties by localized descriptive title |

---
## Type: ProportionalResizeMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "none" | proportional resizing is never used |
| "always" | proportional resizing is always used |
| "modifier" | proportional resize is off by default, but holding down one of the [Canvas.proportionalResizeModifiers](classes/Canvas.md#attr-canvasproportionalresizemodifiers) turns proportional resize on for a given resize interaction |
| "modifierOff" | proportional resize is on by default, but holding down one of the [Canvas.proportionalResizeModifiers](classes/Canvas.md#attr-canvasproportionalresizemodifiers) turns proportional resize off for a given resize interaction |

### Groups

- dragdrop

---
## Type: RecordDropPosition

### Description
Position of a [ListGrid.recordDrop](classes/ListGrid_2.md#method-listgridrecorddrop) operation with respect to the target record.

### Values

| Value | Description |
|-------|-------------|
| ListGrid.OVER | User dropped directly onto the record |
| ListGrid.BEFORE | User dropped before the record |
| ListGrid.AFTER | User dropped after the record |
| ListGrid.NONE | Drop position is not over a record |

---
## Type: RecordType

### Description
Defines the various types of record that can be present in a [ListGrid](classes/ListGrid_1.md#class-listgrid).

### Values

| Value | Description |
|-------|-------------|
| "normal" | regular data-records |
| "groupHeader" | a special collapsable record containing related regular records |
| "groupSummary" | a record showing summaries for all records in a parent groupNode |
| "gridSummary" | a record showing summaries for all records in the grid |

---
## Type: RelativeDateShortcut

### Description
A RelativeDateShortcut is a special string that represents a shortcut to a date phrase that can be automatically mapped to a [RelativeDateString](reference_2.md#type-relativedatestring) for use in widgets that leverage relative-dates, such as the [RelativeDateItem](classes/RelativeDateItem.md#class-relativedateitem).

Note that some shortcuts indicate a time period but do not directly indicate whether the value refers to the start or end of the time period in question. This ambiguity can be resolved by specifying an explicit [RelativeDateRangePosition](reference_2.md#type-relativedaterangeposition) when calling APIs that convert from RelativeDates to absolute date values. This is the case for _$today_, _$tomorrow_, _$yesterday_, _$weekAgo_, _$weekFromNow_, _$monthAgo_ and _$monthFromNow_. If a range position is not explicitly passed, these will all default to the start of the day in question.

Builtin options include

*   $now - this moment
*   $today - the current day. By default this resolves to the start of the current day though an explicit [RelativeDateRangePosition](reference_2.md#type-relativedaterangeposition) may be used to specify the end of the current day.
*   $startOfToday - the start of today
*   $endOfToday - the end of today (one millisecond before the $startOfTomorrow)
*   $yesterday - the previous day.
*   $startOfYesterday - the start of yesterday
*   $endOfYesterday - the end of yesterday (one millisecond before the $startOfToday)
*   $tomorrow - the following day
*   $startOfTomorrow - the start of tomorrow
*   $endOfTomorrow - the end of tomorrow
*   $weekAgo - the current day of the previous week
*   $weekFromNow - the current day of the next week
*   $startOfWeek - the start of the current week
*   $endOfWeek - the end of the current week
*   $monthAgo - the current day of the previous month
*   $monthFromNow - the current day of the following month
*   $startOfMonth - the start of the current month
*   $endOfMonth - the end of the current month
*   $startOfYear - the start of the current year
*   $endOfYear - the end of the current year

### See Also

- [RelativeDateString](reference_2.md#type-relativedatestring)

---
## Type: ReorderPosition

### Description
Controls where a drag-item should be dropped in relation to the target row

### Values

| Value | Description |
|-------|-------------|
| ListGrid.BEFORE | Drop the drag-item before the target-row |
| ListGrid.AFTER | Drop the drag-item after the target-row |
| ListGrid.OVER | Drop the drag-item over (onto) the target-row |

### Groups

- dragdrop

---
## Type: ResizeDirection

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "before" | resize bar targets the canvas before it in the layout |
| "after" | resize bar targets the canvas after it in the layout |

---
## Type: RESTRequestFormat

### Description
Indicates the request format to be used for a REST operation. Is only applicable to [RestConnector DataSources](kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector). Note for all of these `RESTRequestFormat` options, only simple key-value criteria are supported; to handle [AdvancedCriteria](#object-advancedcriteria), you can use a [requestTemplate](classes/DataSource.md#attr-datasourcerequesttemplate), or subclass `com.isomorphic.dataSource.RestConnector` and override the `applyValuesOrCriteriaToRequest()` method.

### Values

| Value | Description |
|-------|-------------|
| "params" | Indicates that context is provided to the target REST service by setting parameter values in the URL. With this request format, the [DSRequest](reference_2.md#object-dsrequest)'s values or criteria will be added to the [target dataURL](classes/DataSource.md#attr-datasourcedataurl) as standard HTTP parameters values as follows:

*   For "add" and "update" requests the "values" will be added to the target URL (see the server-side Javadoc for `DSRequest.getValues()`)
*   For "fetch" and "remove" requests, where the concept of "values" doesn't make sense, the "criteria" will be added to the target URL (see the server-side Javadoc for `DSRequest.getCriteria()`)

So if we had a fetch request that specified criteria like this:
```
    {countryCode: "US", stateCode: "CA"}
 
```
and a [dataURL](classes/OperationBinding.md#attr-operationbindingdataurl) like this:
```
    https://somerestservice.com/customer/fetch
 
```
we would end up with a target URL like this:
```
    https://somerestservice.com/customer/fetch?countryCode=US&stateCode=CA
 
```
Also, note that any explicitly declared [params](classes/DataSource.md#attr-datasourceparams) will also be added to the target URL as standard HTTP parameters, as well as the request values/criteria (if there are any name collisions, the request values/criteria take precedence).

This format is often used to supply criteria to "fetch" operations, and primary-key values to "remove" operations. However, this is by no means a universal approach; different REST services adopt different approaches, there is no generally-accepted "right way" to handle things

It is possible to suppress this automatic mapping - see [DataSource.suppressAutoMappings](classes/DataSource.md#attr-datasourcesuppressautomappings) |
| "json" | Indicates that context is provided to the target REST service by providing a block of JSON-encoded text in the body of the HTTP request sent to the REST server. With this request format, `RestConnector` will render an incoming [DSRequest](reference_2.md#object-dsrequest)'s values or criteria as a JSON object; for "add" and "update" requests, the "values" will be used, and for "fetch" and "remove" operations, the criteria will be used (see the server-side Javadoc for `DSRequest.getCriteria()`).

So if we had an add request with the following record:

```
    {
       customerId: 7023,
       customerName: "Bay Financials inc",
       city: "San Francisco",
       countryCode: "US", 
       stateCode: "CA"
    }
 
```
those values would be included, in strict JSON form, in the body of the HTTP request that `RestConnector` sends to the REST webservice:
```
    {"customerId": 7023,"customerName": "Bay Financials inc",
     "city: "San Francisco","countryCode": "US", "stateCode": "CA"}
 
```

This format is most often used when you need to supply more extensive amounts of data, like entire records to "add" and "update" operations. However, as mentioned above, this is by no means a universal approach, and some REST services use URL parameters even when specifying entire records of data. Also, some REST services use XML rather than JSON

Note, if there is a [requestTemplate](classes/DataSource.md#attr-datasourcerequesttemplate) in force, we use that to drive the content and format of the generated JSON block |
| "xml" | Indicates that context is provided to the target REST service by providing a block of XML text in the body of the HTTP request sent to the REST server. With this request format, `RestConnector` will render an incoming [DSRequest](reference_2.md#object-dsrequest)'s values or criteria as a snippet of XML text; for "add" and "update" requests, the "values" will be used, and for "fetch" and "remove" operations, the criteria will be used (see the server-side Javadoc for `DSRequest.getCriteria()`). The name of the enclosing tag is specified in [DataSource.xmlTag](classes/DataSource.md#attr-datasourcexmltag).

So if we had an add request with the following record:

```
    {
       customerId: 7023,
       customerName: "Bay Financials inc",
       city: "San Francisco",
       countryCode: "US", 
       stateCode: "CA"
    }
 
```
those values would be included in the body of the HTTP request that `RestConnector` sends to the REST webservice (assuming the `xmlTag` is "customer"):
```
    <customer>
        <customerId>7023</customerId>
        <customerName>Bay Financials inc"</customerName>
        <city>San Francisco</city>
        <countryCode>US</countryCode>
        <stateCode>CA"</stateCode>
    </customer>
 
```

Note, if there is a [requestTemplate](classes/DataSource.md#attr-datasourcerequesttemplate) in force, we use that to drive the content and format of the generated XML |

### Groups

- serverRestConnector

---
## Type: RESTResponseFormat

### Description
Indicates the response format to be used for a REST operation. Is only applicable to [RestConnector DataSources](kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector).

### Values

| Value | Description |
|-------|-------------|
| "json" | Indicates that the REST service response is a valid [JSON](https://www.json.org/json-en.html) message. We will parse the response text as JSON, and the resulting object structure can be further processed with [XPaths](classes/DataSource.md#attr-datasourcerecordxpath), [templates](classes/DataSource.md#attr-datasourceresponsetemplate) and [scripting](classes/DataSource.md#attr-datasourcetransformresponsescript) |
| "xml" | Indicates that the REST service response is an XML message. We will parse the response text as XML, and the resulting object structure can be further processed with XPaths, templates and scripting |
| "csv" | Indicates that the the REST service response is in delimited text format in the body of the HTTP response. We will parse the response text as delimited flat text data, and the resulting object structure can be further processed with scripting. Note, we do not support XPaths because they do not make sense with flat data, and we also do not support templating of CSV responses. Record-level and field-level transformation scripts, however, are applicable, and field [nativeName](classes/DataSourceField.md#attr-datasourcefieldnativename)s are honored if the CSV text includes a header row

`RestConnector` only supports a couple options for CSV-based REST services - see [DataSource.csvDelimiter](classes/DataSource.md#attr-datasourcecsvdelimiter) and [DataSource.csvQuoteCharacter](classes/DataSource.md#attr-datasourcecsvquotecharacter) |
| "text" | Indicates that REST service response is to be treated simply as a piece of text, with no parsing or other processing attempted. Use this format for services that return simple strings or messages in some non-standard format; you can provide your own parsing logic in a [transformResponseScript](classes/DataSource.md#attr-datasourcetransformresponsescript) |

### Groups

- serverRestConnector

---
## Type: RowCountStatus

### Description
Enumerated status indicating whether a ResultSet has an accurate [ResultSet.getRowCount](classes/ResultSet.md#method-resultsetgetrowcount) row count for the data set.

This is a feature associated with [progressive loading of data](classes/DataSource.md#attr-datasourceprogressiveloading). When progressive loading is active, the [length](classes/ResultSet.md#method-resultsetgetlength) may not indicate the true size of the data set. In this case a different total row count may be maintained by the ResultSet data object and retrieved via [ResultSet.getRowCount](classes/ResultSet.md#method-resultsetgetrowcount). This status code indicates whether this row count is an exact value or not.

### Values

| Value | Description |
|-------|-------------|
| "exact" | The size of the data set is known and the current row count is accurate. This always will be the case if [progressiveLoading](classes/DataSource.md#attr-datasourceprogressiveloading) is not active. If progressiveLoading is active, we may have an accurate row count in the following scenarios:

*   [ResultSet.setFullLength](classes/ResultSet.md#method-resultsetsetfulllength) was explicitly invoked to tell the resultSet its total length.  
    In this case [ResultSet.getLength](classes/ResultSet.md#method-resultsetgetlength) will return the same value as [ResultSet.getRowCount](classes/ResultSet.md#method-resultsetgetrowcount)
*   The user has scrolled all the way to the true end of the progressively loaded data set such that the length is now known.  
    In this case [ResultSet.getLength](classes/ResultSet.md#method-resultsetgetlength) will return the same value as [ResultSet.getRowCount](classes/ResultSet.md#method-resultsetgetrowcount)
*   A successful row count fetch was performed via [ResultSet.fetchRowCount](classes/ResultSet.md#method-resultsetfetchrowcount).  
    In this case [ResultSet.getLength](classes/ResultSet.md#method-resultsetgetlength) will return the same value as [ResultSet.getRowCount](classes/ResultSet.md#method-resultsetgetrowcount) if [ResultSet.applyRowCountToLength](classes/ResultSet.md#attr-resultsetapplyrowcounttolength) is true, otherwise the values may differ.
*   The dataSource fetch response to a request for rows within the resultSet included a [DSResponse.estimatedTotalRows](classes/DSResponse.md#attr-dsresponseestimatedtotalrows) value with an exact value  
    In this case [ResultSet.getLength](classes/ResultSet.md#method-resultsetgetlength) will return the same value as [ResultSet.getRowCount](classes/ResultSet.md#method-resultsetgetrowcount) if [ResultSet.applyRowCountToLength](classes/ResultSet.md#attr-resultsetapplyrowcounttolength) is true, otherwise the values may differ. |
| "unknown" | The current row count is unknown. This value indicates [ResultSet.lengthIsKnown](classes/ResultSet.md#method-resultsetlengthisknown) returns false. |
| "loading" | This value indicates that the ResultSet is waiting for an active [row count fetch](classes/ResultSet.md#method-resultsetfetchrowcount) to complete. |
| "minimum" | The current row count is a minimum - there are at least this many records in the data set. Note that when [progressiveLoading](classes/DataSource.md#attr-datasourceprogressiveloading) is active, this will be the status if no explicit [DSResponse.estimatedTotalRows](classes/DSResponse.md#attr-dsresponseestimatedtotalrows) was available, so [DSResponse.totalRows](classes/DSResponse.md#attr-dsresponsetotalrows) is a minimum, or if [DSResponse.estimatedTotalRows](classes/DSResponse.md#attr-dsresponseestimatedtotalrows) contained a value in the format `_"[rowCount]+"_`. |
| "approximate" | The current row count is an approximation. This will be the status if [progressiveLoading](classes/DataSource.md#attr-datasourceprogressiveloading) is active and a fetch request contained an explicit [DSResponse.estimatedTotalRows](classes/DSResponse.md#attr-dsresponseestimatedtotalrows) in the format `_"~[rowCount]"_`. |
| "maximum" | The current row count is a maximum - there are no more than this many records in the data set. This will be the status if [progressiveLoading](classes/DataSource.md#attr-datasourceprogressiveloading) is active and a fetch request contained an explicit [DSResponse.estimatedTotalRows](classes/DSResponse.md#attr-dsresponseestimatedtotalrows) in the format `_"-[rowCount]"_`. |
| "range" | The data object knows the total number of records in the data set lies within a particular range. In this case [ListGrid.getRowCountRange](classes/ListGrid_2.md#method-listgridgetrowcountrange) may be used to retrieve the upper and lower bound of this range, and [ListGrid.getRowCount](classes/ListGrid_2.md#method-listgridgetrowcount) will return the lower bound. This will be the status if [progressiveLoading](classes/DataSource.md#attr-datasourceprogressiveloading) is active and a fetch request contained an explicit [DSResponse.estimatedTotalRows](classes/DSResponse.md#attr-dsresponseestimatedtotalrows) in the format `_"[minRowCount]-[maxRowCount]"_`. |

### Groups

- rowRangeDisplay

---
## Type: RowEndEditAction

### Description
While editing a ListGrid, what cell should we edit when the user attempts to navigate into a cell past the end of an editable row, via a Tab keypress, or a programmatic saveAndEditNextCell() call?

### Values

| Value | Description |
|-------|-------------|
| "same" | navigate to the first editable cell in the same record |
| "next" | navigate to the first editable cell in the next record |
| "done" | complete the edit. |
| "stop" | Leave focus in the cell being edited (take no action) |
| "none" | take no action |

### Groups

- editing

### See Also

- [ListGrid.rowEndEditAction](classes/ListGrid_1.md#attr-listgridrowendeditaction)

---
## Type: RowSpanEditMode

### Description
When [ListGrid.allowRowSpanning](classes/ListGrid_1.md#attr-listgridallowrowspanning) is enabled, certain cells may span multiple rows. In this case, the cell displays the value from the record in the first row. If the grid is [editable](classes/ListGrid_1.md#attr-listgridcanedit) (and the [field is also editable](classes/ListGridField.md#attr-listgridfieldcanedit)), these settings allow the user to specify what happens to the data when the user edits this cell.

Note that in this scenario, a user may begin an edit on the row-spanning cell directly (via double-click for example), or on a cell in another column in any of the rows spanned by the cell. The appropriate behavior with respect to user-experience and how the data is manipulated will depend on the application in question. Developers may of course entirely disable editing for the field via [ListGridField.canEdit](classes/ListGridField.md#attr-listgridfieldcanedit) or [ListGrid.canEditCell](classes/ListGrid_2.md#method-listgridcaneditcell).

See also: [ListGrid.useRowSpanStyling](classes/ListGrid_1.md#attr-listgriduserowspanstyling)

### Values

| Value | Description |
|-------|-------------|
| "first" | This setting assumes that only the field-value for the first record spanned by this cell is significant. In this case the editor will only show for this cell if the user is editing the first spanned record. If the user initialized the edit on another spanned row, the editor will not show for this field. |
| "each" | This setting assumes that each row's values are logically separate, so if a cell spans multiple rows, and a user initializes an edit on some cell in the second spanned row, the spanning cell will show an editor containing the value for the second spanned row. This may differ from the value displayed when not in edit mode (which is derived from the first spanned row by default). This setting may be useful for developers who which to implement their own logic on how to handle spanning cell display values and/or edit values (for example by using custom [formatting](classes/ListGridField.md#method-listgridfieldformatcellvalue) and applying custom logic to handle editing on [ListGridField.editorEnter](classes/ListGridField.md#method-listgridfieldeditorenter) and [ListGridField.editorExit](classes/ListGridField.md#method-listgridfieldeditorexit)). |

---
## Type: RowSpanSelectionMode

### Description
Behavior of selection when row spanning is active. See [ListGrid.useRowSpanStyling](classes/ListGrid_1.md#attr-listgriduserowspanstyling).

### Values

| Value | Description |
|-------|-------------|
| "forward" | when a cell is clicked on, select any cells in subsequent columns which are at least partially spanned by the clicked cell |
| "both" | when a cell is clicked on, selects any cells in any other columns which are at least partially spanned by the clicked cell |
| "outerSpan" | behaves like "forward", except as though the cell in the first column was clicked instead. If the largest row spans are in the first column and all cells in subsequent columns do not extend out of the first cell's span, this creates a row-like selection model where the span of the left-most cell defines the "row" of cells being selected. |

---
## Type: RPCTransport

### Description
SmartClient supports multiple RPC transports for maximum compatibility and feature richness. All of transports use HTTP as the underlying protocol, but use different mechanisms for sending the HTTP request and processing the response. The transport is typically auto-selected for by based on the feature being used and the current browser settings. For advanced use cases, [RPCRequest.transport](classes/RPCRequest.md#attr-rpcrequesttransport) and [RPCManager.defaultTransport](classes/RPCManager.md#classattr-rpcmanagerdefaulttransport) are exposed as override points.

### Values

| Value | Description |
|-------|-------------|
| "xmlHttpRequest" | Uses the XMLHttpRequest object to make the request to the server. Note that in some browsers with certain configurations, this transport may not be available. See [platformDependencies](kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information. This transport is not useful with file uploads. Cannot be used to target cross-domain URLs directly. |
| "scriptInclude" | Write a SCRIPT tag into the DOM with a SRC attribute that targets an arbitrary URL. This transport is the only one that allows direct cross-domain URL access.

For [RPCRequest.callback](classes/RPCRequest.md#attr-rpcrequestcallback) to work, the server being contacted must support the ability to generate JavaScript code in the response that will call a JavaScript function generated by SmartClient. SmartClient passes the name of the function to call via a URL parameter, which can be controlled with [RPCRequest.callbackParam](classes/RPCRequest.md#attr-rpcrequestcallbackparam). This callback mechanism is sometimes called the "JSONP" (JSON with Padding) approach. |
| "hiddenFrame" | Available with SmartClient Server only. An HTML form is dynamically assembled that targets a hidden IFRAME. This mechanism is supported on all browsers and cannot be disabled by end users.

If using the SmartClient Server and using [Server-side data integration](kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration), the "hiddenFrame" transport is automatically used for all RPCManager and DataSource requests if the "xmlHttpRequest" transport is not available.

Cannot be used to target cross-domain URLs directly. |

---
## Type: SCClassName

### Description
Name of a SmartClient Class, that is, a Class that has been created via [isc.defineClass](classes/isc.md#staticmethod-iscdefineclass), including Classes built into SmartClient, such as "ListGrid".

---
## Type: SCImgURL

### Description
For properties that refer to images by URL, such as [Img.src](classes/Img.md#attr-imgsrc) and [Button.icon](classes/Button.md#attr-buttonicon), SmartClient provides various capabilities to allow for simpler and more uniform settings, and to allow applications to be restructured more easily.

**[StockIcons](reference_2.md#object-stockicon)**

SmartClient defines a list of [known-icons](classes/Media.md#classmethod-mediagetstockiconnames) which can be used by name in src-strings. For example, setting a button's [icon](classes/Button.md#attr-buttonicon) property to "Edit" will show the [current image](classes/StockIcon.md#attr-stockiconsrc) mapped to the builtin StockIcon with that name. You can also modify the image currently assigned to the "Edit" icon by calling [Media.updateIconMapping("Edit", "new src")](classes/Media.md#classmethod-mediaupdateiconmapping).

When using a StockIcon-name as a src, you may also include additional settings to extend the [StockIcon](classes/StockIcon.md#attr-stockiconsrc) if applicable. For example, a src of "Edit:size:24,24;" will take the "Edit" stockIcon's current src and, if that src represents a sprite-string, apply the additional size attributes and render the Edit icon at a larger size.

These features are especially useful in combination with [SVG Symbols](kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview) using runtime-styling, where colors can be easily modified on a per usage-basis, for example with "Edit:color:red;". **the application image directory**

When specifying URLs to image files via SmartClient component properties such as [StretchImg.src](classes/StretchImg.md#attr-stretchimgsrc), any relative path is assumed to be relative to the "application image directory" (`appImgDir`). The application image directory can be set via [Page.setAppImgDir](classes/Page.md#classmethod-pagesetappimgdir), and defaults to "images/", representing the typical practice of placing images in a subdirectory relative to the URL at which the application is accessed.

For applications that may be launched from multiple URLs, the `appImgDir` can be set to the correct relative path to the image directory by calling [Page.setAppImgDir](classes/Page.md#classmethod-pagesetappimgdir) before any SmartClient components are created. This enables applications or components of an application to be launched from multiple locations, or to be relocated, without changing any image URLs supplied to SmartClient components.

**the "\[SKIN\]" URL prefix**

The special prefix "\[SKIN\]" can be used to refer to images within the skin folder whenever image URLs are supplied to SmartClient components.

The value of "\[SKIN\]" is the combination of:

*   the "skin directory", established in `load_skin.js` via [Page.setSkinDir](classes/Page.md#classmethod-pagesetskindir), plus..
*   the setting for [skinImgDir](classes/Canvas.md#attr-canvasskinimgdir) on the component where you set an image URL property

`skinImgDir` defaults to "images/", so creating an [Img](classes/Img.md#class-img) component with [Img.src](classes/Img.md#attr-imgsrc) set to "\[SKIN\]myButton/button.gif" will expand to `Page.getSkinDir() + "/images/myButton/button.gif"`.

Some components that use a large number of images use `skinImgDir` to group them together and make it possible to relocate all the media for the component with a single setting. For example, the [TreeGrid](classes/TreeGrid.md#class-treegrid) class sets `skinImgDir` to "images/TreeGrid/". This allows [TreeGrid.folderIcon](classes/TreeGrid.md#attr-treegridfoldericon) to be set to just "\[SKIN\]folder.gif" but refer to `Page.getSkinDir() + "/images/TreeGrid/folder.gif"`.

A custom subclass of TreeGrid can set `skinImgDir` to a different path, such as "/images/MyTreeGrid", to source all media from a different location.

_TIPS:_

*   subcomponents do not automatically share the parent component's setting for skinImgDir. For example, the [Window.minimizeButton](classes/Window.md#attr-windowminimizebutton) has the default setting for "skinImgDir" ("images/"), so the [src](classes/Img.md#attr-imgsrc) property used with this component is set to "\[SKIN\]/Window/minimize.png" (in the "SmartClient" sample skin).
*   for a particular image, the skinImgDir setting on the component may not be convenient. The prefix "\[SKINIMG\]" can be used to refer to `Page.getSkinDir() + "/images"` regardless of the setting for `skinImgDir`

**Using a css class instead of an image URL**

In some cases, instead of an explicit image URL, developers may wish to apply a named css class with a background-image to an image based component. This may be achieved by specifying your image URL in the format **"style:_`<styleName>`_"**.

For example if your application loads the following css class:

```
 .starImg {
    width: 48px; height: 48px;
    background: url(/images/star.gif) 0 0;    
 }
 
```
It may be displayed in an Img component by setting [Img.src](classes/Img.md#attr-imgsrc) to `"style:startImg"`.

**Sprited images**

In addition to the `"style:..."` prefix for specifying a css class instead of a simple image URL, the prefix `"sprite:..."` may be used to specify properties required to extract an image from an image [sprite](https://www.w3schools.com/Css/css_image_sprites.asp).

For details on how this format may be used, see the [SCSpriteConfig](#type-scspriteconfig) documentation.

**Stateful image URLs**

Many SmartClient components support changing their appearance to reflect their current "state" \[_"Focused"_, _"Disabled"_, etc\]. As such they may display different image media to reflect their current state.  
See the [Stateful Images overview](kb_topics/statefulImages.md#kb-topic-stateful-images) for details on how image states are managed in SmartClient.

**SVG Images**

_For more information about using stylable SVGs for spriting in a way that doesn't involve lots of file-loads or the flickering typically associated with modifying SVGs in-browser, see the [SVG Symbols Overview](kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview)._

If the URL represents an SVG image, you may specify `tag` as a query param to control whether it's rendered in an object or image tag, provided [Canvas.useImageForSVG](classes/Canvas.md#attr-canvasuseimageforsvg) isn't set. If that query param is present and has any value other than `object`, then the SVG image will be rendered in an image tag. Otherwise, it will be rendered in an object tag. For example, an `SCImgURL` of "circle.svg?tag=image" will render in an image tag.

**the special "blank" constant**

If you don't have to show any image for any reason or you need to reset the area where an image is, you can call _myImage.setSrc('blank')_ or set:

```
 isc.Img.create({
    ID: "myImage",
    width:48, height:48,
    src: "blank"
 })
 
```
This will render an empty space, where the blank.gif image, that each skin has, will be used for this purpose.

---
## Type: SCSpriteConfig

### Description
#### Using Sprites
[Image sprites](https://www.w3schools.com/Css/css_image_sprites.asp) are a technique to minimize server http requests when displaying media to a user. Given a series of small images (icons, say), instead of having a separate image file be loaded for each icon, the server can provide a single large composite image to the client, and the client can use CSS to display sections of this larger image to the user.  
See also the "spriting" discussion in the [skinning overview](kb_topics/skinning.md#kb-topic-skinning--theming) documentation.

The SmartClient framework supports the `SCSpriteConfig` format for sprited images.

Note that _SCSpriteConfig_ is just a special class of [image URL](#type-scimgurl), and as such any component attribute of type SCImgURL may be set to a sprite configuration.

SCSpriteConfigs have the following format:  
`"sprite:_`<image URL>`_;offset:_`<Left>`,`<Top>`_;size:_`<Width>`,`<Height>`_;cssClass:_`<className>`_"`

This format allows developers to specify the image source and the native size and offset of the sprite within the image.

The media to load will be retrieved from the specified image URL. Standard [SCImgURL](#type-scimgurl) directory prefixes such as "\[SKIN\]" can be included in this URL.

Developers may also specify [an image data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs) - for example `"sprite:data:image/jpeg;base64,_`<data>`_;offset:-120,0;size:20,20;"`.

An explicit URL is not required. Developers may instead specify a css class which can include an explicit `background-image` attribute.

The `offset:` property specifies the left and top coordinate to apply to the composite image element such that the desired sprite is visible. The `size:` property indicates the size of the sprite in pixels.  
For example, a sprite configuration of _`"sprite:composite.png;offset:0,-20;size:20,20;"`_ would load the image file "composite.png", and display a 20 pixel square from it. The origin of the larger image would be offset vertically by -20px, so the sprite actually visible to the user would have its y-origin at 20px within the larger image.  
As with the image URL, explicit size and offset are not required - a developer may use css properties (`width`, `height` and `background-offset`) from the specified class to specify the specific sprite to display.

The `cssClass:` denotes the css class to apply to the rendered element displaying the sprite. This is optional - a sprite can be specified with an image URL and explicit sizing and offset coordinates, in which case no css class is actually required.  
(Of course for a valid sprite, it is expected that the image URL and size are specified either explicitly in the string, or within the css class definition. If the offset is omitted, it will be assumed to be zero on both axes).

Sprites will scale automatically. If a spriteConfig is used to provide an image for an icon and some other property is used to configure the drawn size of the icon in question ([Button.iconSize](classes/Button.md#attr-buttoniconsize),for example), the sprite image will be scaled to render at the appropriate size.

#### Sprited image configuration and "stateful" images
Many image URLs in SmartClient are "stateful", meaning that variants of the image should be displayed to the user depending on the current state of the widget. (For example a custom button icon may be [displayed on roll over](classes/Button.md#attr-buttonshowrollovericon), or a selection checkbox icon in a treeGrid [may appear disabled](classes/TreeGrid.md#attr-treegridshowdisabledselectioncheckbox) for unselectable nodes).

There are a couple of approaches to display stateful versions of sprited images.

Wherever [SCStatefulImgConfig](#object-scstatefulimgconfig) objects are supported, a developer may include spriteConfig strings as entries for specific states.  
For example, the following SCStatefulImgConfig definition would display different sprites from _"compositeImg.png"_ for base and "Over" states:  
  `{ _base:"sprite:compositeImg.png;offset:-100,-100;size:20,20",       Over:"sprite:compositeImg.png;offset:-100,-120;size:20,20" }`

Alternatively, if a property that behaves as the base URL for a stateful image (such as [Button.icon](classes/Button.md#attr-buttonicon)) is set to a sprite configuration string, the framework will use the state name as a suffix to apply to the source URL or the css class specified in the sprite.  
As with standard [stateful images](kb_topics/statefulImages.md#kb-topic-stateful-images), if a URL was specified for the sprite, the stateful suffix will be applied with a preceding "\_" character.  
So if the state "Over" was applied to a sprite configuration of `"sprite:compositeImg.png;offset:100,100;size:20,20"`, the generated HTML would attempt to load an image from the URL `"compositeImg_Over.png"` (and display a sprite from that image with the specified size/offset).  
If a class name was specified in the sprite, the stateful suffix would be appended with no leading underscore, similar to how [state suffixes](classes/StatefulCanvas.md#method-statefulcanvasgetstatesuffix) are applied to the `baseStyle` of a StatefulCanvas.  
For example a sprite config of `"sprite:cssClass:buttonIcon"` would display styling from `"buttonIconOver"` when the "Over" state was applied.

#### SVG sprites
If you have a collection of SVG graphics, you can combine them into a single `<svg>` container, and then use the `sprite:` mechanism to access them as SVG _symbols_, which can be reused and re-colored at runtime without server traffic.

See the [SVG Symbols overview](kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview) for more information.

---
## Type: SearchEditorMode

### Description
Affects the appearance and behavior of the builtin [SavedSearchEditor](classes/SavedSearchEditor.md#class-savedsearcheditor).

### Values

| Value | Description |
|-------|-------------|
| "normal" | the editor shows a [FilterBuilder](classes/FilterBuilder.md#class-filterbuilder) for editing criteria |
| "grid" | the editor shows only a field for naming (or renaming) a search, since the grid has built-in interfaces for editing criteria |

### Groups

- editing

---
## Type: Selected

### Description
—

### Values

| Value | Description |
|-------|-------------|
| StatefulCanvas.FOCUSED | StatefulCanvas should show focused state |
| StatefulCanvas.SELECTED | StatefulCanvas is selected |
| StatefulCanvas.UNSELECTED | StatefulCanvas is not selected |

### Groups

- state

---
## Type: SelectedAppearance

### Description
Appearance when a component is in [edit mode](classes/Canvas.md#method-canvasseteditmode) and is selected.

Modes such as "tintMask" or "outlineMask" create an ["edit mask"](classes/EditProxy.md#attr-editproxyeditmask) that is layered over the selected component, and blocks all normal interaction with the component, so that behaviors like [EditProxy.supportsInlineEdit](classes/EditProxy.md#attr-editproxysupportsinlineedit) can completely take the place of the component's normal interactivity.

"outlineEdges" mode allows normal interaction with the component, which allows the end user to do things like [freeze ListGrid fields](classes/ListGrid_1.md#attr-listgridcanfreezefields), which the [GridEditProxy](classes/GridEditProxy.md#class-grideditproxy) can implement as a ${isc.DocUtils.linkForRef('attr:GridEditProxy.saveFieldFrozenState','persistent change to grid\\'s configuration')}.

### Values

| Value | Description |
|-------|-------------|
| "tintMask" | editMask on top of the component is updated with [EditProxy.selectedTintColor](classes/EditProxy.md#attr-editproxyselectedtintcolor) and [EditProxy.selectedTintOpacity](classes/EditProxy.md#attr-editproxyselectedtintopacity) |
| "outlineMask" | editMask on top of the component is updated with [EditProxy.selectedBorder](classes/EditProxy.md#attr-editproxyselectedborder) |
| "outlineEdges" | MultiAutoChild is created on top of the component. This constructs a border around the component using 4 separate `outlineEdge` components so that interactivity is not blocked. |
| "none" | no change in appearance. Override [EditProxy.showSelectedAppearance](classes/EditProxy.md#method-editproxyshowselectedappearance) to create a custom appearance. |

---
## Type: SelectionAppearance

### Description
How data selection should be presented to the user.

### Values

| Value | Description |
|-------|-------------|
| "rowStyle" | selected rows should be shown with different appearance - see [ListGrid.getCellStyle](classes/ListGrid_2.md#method-listgridgetcellstyle) and optionally [ListGrid.selectionCanvas](classes/ListGrid_1.md#attr-listgridselectioncanvas). |
| "checkbox" | an extra, non-data column should be automatically added to the ListGrid, showing checkboxes that can be toggled to select rows. See [ListGrid.getCheckboxField](classes/ListGrid_2.md#method-listgridgetcheckboxfield). |

---
## Type: SelectionBoundary

### Description
Boundary type for limiting where contiguous selection (via shift+click or drag selection) can be applied across [facets](classes/Facet.md#attr-facetselectionboundary) or [facetValues](classes/FacetValue.md#attr-facetvalueselectionboundary).

### Values

| Value | Description |
|-------|-------------|
| "after" | selection boundary applies to the bottom / right of the cells |
| "before" | selection boundary applies to the top / left of the cells |
| "both" | selection boundary applies to both edges. |

---
## Type: SelectionStyle

### Description
Different styles of selection that a list, etc. might support

### Values

| Value | Description |
|-------|-------------|
| Selection.NONE | don't select at all |
| Selection.SINGLE | select only one item at a time |
| Selection.MULTIPLE | select one or more items |
| Selection.SIMPLE | select one or more items as a toggle so you don't need to hold down control keys to select more than one object |

### Groups

- selection

---
## Type: SequenceMode

### Description
The possible types of sequence handling SmartClient Server can apply. This refers to the technique used to obtain the primary keys of the most recent insert, which the product uses to enable [automatic cache synchronization](kb_topics/cacheSynchronization.md#kb-topic-automatic-cache-synchronization) (updating client-side components bound to a dataSource to reflect updates to that dataSource). Only applicable to [fields](reference_2.md#object-datasourcefield) of [type](reference_2.md#type-fieldtype) "sequence".

### Values

| Value | Description |
|-------|-------------|
| "jdbcDriver" | Use the JDBC 3.0 API "getGeneratedKeys()" to get the most recent sequence value. Obviously, this is only an option for JDBC 3.0+ drivers. **NOTE: Oracle special case** The Oracle JDBC driver provides a "getGeneratedKeys" method, but that method does not actually return the generated key values; instead, it returns a ROWID, which we must use to fetch the inserted row, and obtain the generated key values from it. For this reason, you may find that "native" is slightly faster to retrieve sequence values than "jdbcDriver" with Oracle (or you may find that it makes no noticeable difference; it depends on too many factors for us to give a concrete recommendation) |
| "native" | Use a database-specific native technique to obtain the most recent sequence value. The actual technique used varies widely depending on the vagaries of the underlying database (and sometimes the vagaries of particular releases of a database product) |
| "none" | No automatic attempt is made to retrieve the most recent sequence value. You are expected to handle this by providing a [cacheSyncOperation](classes/OperationBinding.md#attr-operationbindingcachesyncoperation) that is able to return the entire row without needing generated PK values for context. For example, a query that uses `MAX(pk)` would be capable of this. To give a more complex example, say you have a sequence value that is retrieved from a legacy system: you could store that sequence value in the HTTP session and then have your custom `cacheSyncOperation` reference that session attribute in its `WHERE` clause. Also note that cacheSyncOperations, like any other [DataSource operation](classes/OperationBinding.md#class-operationbinding), can be [written in Java](classes/OperationBinding.md#attr-operationbindingserverobject) or any [JSR223-compliant scripting language](classes/OperationBinding.md#attr-operationbindingscript) - you do not have to use SQL |

---
## Type: ShowDataValuesMode

### Description
Strategy for determining whether and when to show [formatted text labels](classes/FacetChart.md#method-facetchartformatdatavalue) for data-values. There are two basic mechanisms:

*   inChart - data-values are displayed in the chart-body close to their data-points - not all [chart-types](classes/FacetChart.md#attr-facetchartcharttype) support showing data-values in the chart-body, and none will show them all if data-density is such that the labels would overlap or extend beyond their available area
*   inHover - as the mouse moves over the chart body, the data-value for the [nearest data-point](classes/FacetChart.md#method-facetchartgetnearestdrawnvalue) is displayed in a [label](classes/FacetChart.md#attr-facetcharthoverlabelproperties) floating near the shape it represents. When showing values in hovers, the visual element representing the data value is also emphasized by brightening or highlighting it (appearance differs by chart type).

Support for showing data-values differs by [chart-type](classes/FacetChart.md#attr-facetchartcharttype); for example, [Stacked charts](classes/FacetChart.md#attr-facetchartstacked) cannot show data-values in the chart body; column charts can, and they can also [rotate values](classes/FacetChart.md#attr-facetchartrotatedatavalues) to fit if necessary; pie charts, can show just the data-values that fit inside their segments in the chart-body; all types can show data-values in hovers.

### Values

| Value | Description |
|-------|-------------|
| "never" | never show data-values at all |
| "auto" | show data-values in the chart, when the chartType supports it and when they fit without overlapping (including after [rotation](classes/FacetChart.md#attr-facetchartrotatedatavalues)), and in hovers otherwise |
| "inChartOnly" | show data-values in the chart body, but only if they all fit - no hovers |
| "inChartOrHover" | show data-values in the chart body and, if any don't fit, switch to hovers |
| "inChartAndHover" | show data-values that fit in the chart body and also switch on hovers |
| "inHoverOnly" | always show data-values in hovers |

### Groups

- labelsAndTitles

---
## Type: ShowMessageType

### Description
Type of message to display in [ShowMessageTask](#class-showmessagetask). Controls the display of the icon.

### Values

| Value | Description |
|-------|-------------|
| "normal" | Normal message |
| "warning" | Warning message |
| "error" | Error message |

### See Also

- [ShowMessageTask.type](#attr-showmessagetasktype)

---
## Type: Side

### Description
Side of a component.

### Values

| Value | Description |
|-------|-------------|
| Canvas.LEFT | Left side |
| Canvas.RIGHT | Right side |
| Canvas.TOP | Top side |
| Canvas.BOTTOM | Bottom side |

---
## Type: SnapGridStyle

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "crosses" | show array of crosses to indicate snap points |
| "lines" | show grid of lines to indicate snap points |

---
## Type: SQLPagingStrategy

### Description
The technique SmartClient Server's SQL DataSource should use to select a "page" of data from a table.

### Values

| Value | Description |
|-------|-------------|
| "sqlLimit" | Specify the paging directly in the SQL query we generate. The way this is done varies considerably from database to database: with some it is a straightforward built-in facility while others require arcane tricks or simply don't support the idea. This is the most efficient method, where available. Note that this strategy is not supported for operations that make use of a [customSQL](classes/OperationBinding.md#attr-operationbindingcustomsql) clause, because it depends upon being able to determine the size of the whole dataset without actually retrieving the whole dataset. Ordinary operations do this by means of an automatically-generated "row count query", but we cannot generate such a query for a `customSQL` operation. |
| "jdbcScroll" | Implement the paging behavior by use of the `absolute()` method of the JDBC `ResultSet`. |
| "dropAtServer" | Implement the paging behavior by fetching the entire resultset from the database and dropping any unnecessary rows on the server before returning the data to the client. This approach is extremely inefficient, but also extremely straightforward; it is intended as a fallback option, for situations where the more sophisticated approaches cause problems (a JDBC driver that throws vague exceptions when `absolute()` is called, for example) |
| "none" | No paging behavior: we always return the entire resultset to the client. |

### See Also

- [DataSource.sqlPaging](classes/DataSource.md#attr-datasourcesqlpaging)
- [OperationBinding.sqlPaging](classes/OperationBinding.md#attr-operationbindingsqlpaging)

---
## Type: StackDirection

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "up" | older messages move up |
| "down" | older messages move down |
| "right" | older messages move right |
| "left" | older messages move left |

---
## Type: StandardControlGroup

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "fontControls" | [Font controls](classes/RichTextEditor.md#attr-richtexteditorfontcontrols) |
| "formatControls" | [Text formatting controls](classes/RichTextEditor.md#attr-richtexteditorformatcontrols) |
| "styleControls" | [Text styling controls](classes/RichTextEditor.md#attr-richtexteditorstylecontrols) |
| "colorControls" | [Color controls](classes/RichTextEditor.md#attr-richtexteditorcolorcontrols) |
| "bulletControls" | [HTML list controls](classes/RichTextEditor.md#attr-richtexteditorbulletcontrols) |

---
## Type: State

### Description
Constants for the standard states for a StatefulCanvas.

### Values

| Value | Description |
|-------|-------------|
| StatefulCanvas.STATE_UP | state when mouse is not acting on this StatefulCanvas |
| StatefulCanvas.STATE_DOWN | state when mouse is down |
| StatefulCanvas.STATE_OVER | state when mouse is over |
| StatefulCanvas.STATE_DISABLED | disabled |

### Groups

- state

---
## Type: TableMode

### Description
Controls the display mode of TableView record display

### Values

| Value | Description |
|-------|-------------|
| TableView.PLAIN | The default mode which displays a list of rows |
| TableView.GROUPED | Grouped table is a set of rows embedded in a rounded rectangle |

---
## Type: TabName

### Description
An [Identifier](#type-identifier) that must be locally unique within the containing [TabSet](classes/TabSet.md#class-tabset).

---
## Type: TabTitleEditEvent

### Description
An event that triggers title editing in a TabSet.

### Values

| Value | Description |
|-------|-------------|
| "click" | Start editing when the user single-clicks a tab title |
| "doubleClick" | Start editing when the user double-clicks a tab title |

---
## Type: TEXTAREA_WRAP

### Description
—

### Values

| Value | Description |
|-------|-------------|
| TextAreaItem.OFF | don't allow wrapping at all |
| TextAreaItem.SOFT | when the entered text reaches the edge of the text area, wrap visibly but don't include line breaks in the textarea value |
| TextAreaItem.HARD | when the entered text reaches the edge of the text area, insert a line break |

---
## Type: TileLayoutPolicy

### Description
Policy for laying out tiles.

Because a TileLayout can be either horizontally or vertically oriented, the general term "line" is used to mean either a row or column of tiles.

**NOTE**: for typical form layouts (a variety of input fields and buttons in a tabular layout with col-spanning and row-spanning support), use a [DynamicForm](classes/DynamicForm.md#class-dynamicform) and see the [formLayout](kb_topics/formLayout.md#kb-topic-form-layout) topic.

### Values

| Value | Description |
|-------|-------------|
| "fit" | Each line has the same number of tiles, based on [TileLayout.tilesPerLine](classes/TileLayout.md#attr-tilelayouttilesperline) if set, otherwise, based on fitting as many tiles per line as possible consistent with [tileSize](classes/TileLayout.md#attr-tilelayouttilesize) and [TileLayout.tileMargin](classes/TileLayout.md#attr-tilelayouttilemargin).

Tiles that do not specify a size will be sized to fill available space. |
| "flow" | Tiles are laid out with varying numbers of tiles per line according to each tile's size, the [tileMargin](classes/TileLayout.md#attr-tilelayouttilemargin), and the available space.

Tiles are never resized by the TileLayout and [TileLayout.tileSize](classes/TileLayout.md#attr-tilelayouttilesize) is ignored. |

---
## Type: TitleAutoFitRotationMode

### Description
Strategy for determining how to place maximum-sized labels for [DrawItem.titleAutoFit](classes/DrawItem.md#attr-drawitemtitleautofit).

### Values

| Value | Description |
|-------|-------------|
| "never" | do not rotate |
| "auto" | rotate only if doing so would allow label to be larger |
| "always" | always rotate |

---
## Type: TitleRotationMode

### Description
The different ways in which the [titleLabel](classes/DrawItem.md#attr-drawitemtitlelabel) of a [DrawItem](classes/DrawItem.md#class-drawitem) can be rotated with the item.

**NOTE:** The effect of the "withItemAlwaysUp" and "withLineAlwaysUp" settings is not affected by the global rotation, if any (see [DrawPane.rotation](classes/DrawPane.md#attr-drawpanerotation)).

### Values

| Value | Description |
|-------|-------------|
| "neverRotate" | the `titleLabel` is never rotated with the item. |
| "withItem" | the `titleLabel` is rotated exactly to match the item's rotation (see [DrawItem.rotation](classes/DrawItem.md#attr-drawitemrotation)). |
| "withItemAlwaysUp" | the `titleLabel` is rotated exactly to match the item's rotation, except that at certain rotations, the `titleLabel` is flipped by 180° so that the title text is never upside down. |
| "withLine" | (applies only to [DrawLine](classes/DrawLine.md#class-drawline) and [DrawLinePath](classes/DrawLinePath.md#class-drawlinepath)) the `titleLabel` is rotated to match the line or center segment.

If used on a `DrawItem` that is not a `DrawLine` or `DrawLinePath`, then the effect is the same as "withItem". |
| "withLineAlwaysUp" | (applies only to [DrawLine](classes/DrawLine.md#class-drawline) and [DrawLinePath](classes/DrawLinePath.md#class-drawlinepath)) the `titleLabel` is rotated to match the line or center segment, except that at certain rotations, the `titleLabel` is flipped by 180° so that the title text is never upside down.

If used on a `DrawItem` that is not a `DrawLine` or `DrawLinePath`, then the effect is the same as "withItemAlwaysUp". |

---
## Type: TopOperatorAppearance

### Description
Interface to use for showing and editing the [top-level operator](classes/FilterBuilder.md#attr-filterbuildertopoperator) of a FilterBuilder.

### Values

| Value | Description |
|-------|-------------|
| "radio" | radio buttons appear at the top of the form |
| "bracket" | a SelectItem appears with a "bracket" spanning all top-level clauses, exactly the same appearance used for showing [subClauses](classes/FilterBuilder.md#attr-filterbuildershowsubclausebutton), if enabled. |
| "inline" | each line in the FilterBuilder is a top-level item, with a SelectItem shown on the left that allows the user to choose between the main operator in force (either "and" or "or", depending on the setting of topOperator) and "and not". |
| "none" | no interface is shown. The top-level operator is expected to be shown to the user outside the FilterBuilder, and, if editable, [FilterBuilder.setTopOperator](classes/FilterBuilder.md#method-filterbuildersettopoperator) should be called to update it |

---
## Type: TourActionType

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "click" | The [target](classes/TourStep.md#attr-toursteptarget) must be clicked to complete the step |
| "mouseDown" | The target will complete the step on mouseDown |
| "doubleClick" | The target must be double-clicked to complete the step |
| "rightClick" | The target must be right-clicked to complete the step |
| "mouseOver" | The target must be moused-over to complete the step |
| "drag" | The target must be dragged to complete step. If [dropTarget](classes/TourStep.md#attr-tourstepdroptarget) is also specified, the target component must be dropped onto the `dropTarget`. |
| "change" | The target FormItem must change to complete the step. Specify [expectedValue](classes/TourStep.md#attr-tourstepexpectedvalue) if a specific value must be entered to continue. Depending on the FormItem type this may occur by the user typing or by selecting a value. See [TourStep.inputValidation](classes/TourStep.md#attr-tourstepinputvalidation) for how validation is performed. **Note:** for composite formItems such as [DateItem](classes/DateItem.md#class-dateitem) or [RadioGroupItem](classes/RadioGroupItem.md#class-radiogroupitem), you may specify either the item as a whole or a sub item as the target. Either way the tour will look for the expected value on the composite (parent) item. |
| "menuItemOver" | The target locator should resolve to an item within a Menu that has a sub-menu. The submenu must be opened (by rolling over, or clicking the target) to complete the step. |
| "menuItemSelect" | The target locator should resolve to an item within a Menu. The item must be selected (clicked) to complete the step. |
| "none" | No interaction is allowed with the target and the user must click the next button to complete the step |
| "any" | Interaction is allowed with the target but the user must click the next button to complete the step |

---
## Type: TourInputValidationMode

### Description
Policy for how [inputValidation](classes/TourStep.md#attr-tourstepinputvalidation) is performed for [actionType](classes/TourStep.md#attr-tourstepactiontype):"change". When users enter incorrect values, they are informed via the [Notify](classes/Notify.md#class-notify) system, and the specific message displayed is controlled by [inputValidationNotifyMessage](classes/TourStep.md#attr-tourstepinputvalidationnotifymessage).

The notification can be disabled for the step by setting [TourStep.showInputValidationMessage](classes/TourStep.md#attr-tourstepshowinputvalidationmessage) to `false`.

### Values

| Value | Description |
|-------|-------------|
| "notify" | When there is a brief pause in typing, notify the user that they have typed something wrong. The pause delay is controlled by [inputValidationNotifyDelay](classes/TourStep.md#attr-tourstepinputvalidationnotifydelay). |
| "strict" | Prevent the user from typing any characters that don't match the [expectedValue](classes/TourStep.md#attr-tourstepexpectedvalue), and tell them immediately when they have typed something wrong. |
| "onExit" | text entry is only validated on field exit or click on [afterInputTarget](classes/TourStep.md#attr-tourstepafterinputtarget). |

---
## Type: TourMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "tour" | For a tourStep if you only specify instructions and target, the pointer appearance is used and points at the target - no interaction is expected. To make the step require an interaction, set actionType. |
| "tutorial" | For a tourStep if you only specify instructions and target, the actionType is defaulted and the big red arrow appearance is used. Set actionType:"none" or "any" if your step has a target but doesn't require an interaction. |

---
## Type: TreeFilterMode

### Description
Mode for applying criteria to a tree.

### Values

| Value | Description |
|-------|-------------|
| "strict" | only nodes that actually match criteria are shown. If a parent does not match the criteria, it will not be shown, even if it has children that do match the criteria |
| "keepParents" | parent nodes are kept if they have children which match the criteria, or, in a tree with [loadDataOnDemand:true](classes/ResultTree.md#attr-resulttreeloaddataondemand), if they have not loaded children yet. |

### Groups

- treeFilter

---
## Type: TreeGridViewState

### Description
An object containing the "view state" information for a treeGrid. In addition to the state data contained by a [ListGridViewState](reference_2.md#type-listgridviewstate) object, this will also contain the current open state of the treeGrid in question.  
Note that this object is not intended to be interrogated directly, but may be stored (for example) as a blob on the server for view state persistence across sessions.

### Groups

- viewState

---
## Type: TreeModelType

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "parent" | In this model, each node has an ID unique across the whole tree and a parent ID that points to its parent. The name of the unique ID property can be specified via [Tree.idField](classes/Tree.md#attr-treeidfield) and the name of the parent ID property can be specified via [Tree.parentIdField](classes/Tree.md#attr-treeparentidfield). The initial set of nodes can be passed in as a list to [Tree.data](classes/Tree.md#attr-treedata) and also added as a list later via [Tree.linkNodes](classes/Tree.md#method-treelinknodes). Whether or not a given node is a folder is determined by the value of the property specified by [Tree.isFolderProperty](classes/Tree.md#attr-treeisfolderproperty).  
  
The "parent" modelType is best for integrating with relational storage (because nodes can map easily to rows in a table) and collections of Beans and is the model used for DataBound trees. |
| "children" | In this model, nodes specify their children as a list of nodes. The property that holds the children nodes is determined by [Tree.childrenProperty](classes/Tree.md#attr-treechildrenproperty). Nodes are not required to have an ID that is unique across the whole tree (in fact, no ID is required at all). Node names (specified by the [Tree.nameProperty](classes/Tree.md#attr-treenameproperty), unique within their siblings, are optional but not required. Whether or not a given node is a folder is determined by the presence of the children list ([Tree.childrenProperty](classes/Tree.md#attr-treechildrenproperty)). |

---
## Type: URI

### Description
A Uniform Resource Identifier string, as defined by [https://tools.ietf.org/html/rfc3986](https://tools.ietf.org/html/rfc3986).

---
## Type: ValidatorType

### Description
Used to name a validator or reference a standard, built-in [Validator](classes/Validator.md#class-validator) - see list below.

To make use of a standard validator type for a field in a DataSource, or DynamicForm instance, specify the `validators` property to an array containing a validator definition where the `type` property is set to the appropriate type.

A custom error message can be specified for any validator type by setting the `errorMessage` property on the validator definition object, and some validator types make use of additional properties on the validator definition object such as `max` or `min`.

For example, to use the `integerRange` validator type:  
  
  `field:{       validators:[         {type:"integerRange", min:1, max:100}       ]     }`

Custom validators can be reused on the client by adding them to the global validator list, via the [Validator.addValidatorDefinition](classes/Validator.md#classmethod-validatoraddvalidatordefinition) method.

### Values

| Value | Description |
|-------|-------------|
| isBoolean | Validation will fail if this field is non-empty and has a non-boolean value. |
| isString | Validation will fail if the value is not a string value. |
| isInteger | Tests whether the value for this field is a whole number. If `validator.convertToInteger` is true, float values will be converted into integers and validation will succeed. |
| isFloat | Tests whether the value for this field is a valid floating point number. |
| isFunction | Tests whether the value for this field is a valid expression or function; if it is valid, creates a [stringMethod](kb_topics/stringMethods.md#kb-topic-string-methods-overview) object with the value and set the resultingValue to the StringMethod. |
| requiredIf | RequiredIf type validators should be specified with an `expression` property set to a [stringMethod](kb_topics/stringMethods.md#kb-topic-string-methods-overview), which takes four parameters:

*   item - the DynamicForm item on which the error occurred (may be null)
*   validator - a pointer to the validator object
*   value - the value of the field in question
*   record - the "record" object - the set of values being edited by the widget

When validation is performed, the expression will be evaluated (or executed). If it returns `true`, the field will be treated as a required field, so validation will fail if the field has no value, or, in the case of a [FileItem](classes/FileItem.md#class-fileitem) or [UploadItem](classes/UploadItem.md#class-uploaditem) and if client-side validation is supported by the browser, if no file is selected for upload or the selected file is empty.

To allow server-side enforcement, a `required` validator can be used instead. With the exception of "binary" fields, conditional criteria can be specified with the [applyWhen](classes/Validator.md#attr-validatorapplywhen) property.

See *conditionallyRequired example*.

**NOTE:** A requiredIf validator cannot be used to guarantee that a non-empty file is uploaded. The user's browser might not support client-side file validation. Using a requiredIf validator on a "binary" field may be appropriate in scenarios where the application does not technically require a non-empty file to be uploaded by the user. For example, in a bug tracking application, a file upload may be required if the "Have a test case?" checkbox is checked, but the value of the "Have a test case?" checkbox is not actually saved by the application; instead, whether the user is providing a test case is inferred by whether a non-empty test case file was uploaded. |
| matchesField | Tests whether the value for this field matches the value of some other field. The field to compare against is specified via the `otherField` property on the validator object (should be set to a field name).

See *matchValue example*. |
| equals | Tests whether the value for this field matches some value specified via `value`. |
| notEqual | Tests whether the value for this field does not match some value specified via `value`. |
| isOneOf | Tests whether the value for this field matches any value from an arbitrary list of acceptable values. The set of acceptable values is specified via the `list` property on the validator, which should be set to an array of values. If validator.list is not supplied, the valueMap for the field will be used. If there is no valueMap, not providing validator.list is an error. |
| inSet | Tests whether the value for this field matches any value from an arbitrary list of acceptable values. The set of acceptable values is specified via the `list` property on the validator, which should be set to an array of values. If validator.list is not supplied, the valueMap for the field will be used. If there is no valueMap, not providing validator.list is an error. |
| notInSet | Tests whether the value for this field does not match any value from an arbitrary list of unacceptable values. The set of unacceptable values is specified via the `list` property on the validator, which should be set to an array of values. Not providing validator.list is an error. |
| integerRange | Tests whether the value for this field is a whole number within the range specified. The `max` and `min` properties on the validator are used to determine the acceptable range, inclusive. To specify the range as exclusive of the min/mix values, set `exclusive` to `true`.

See *validationBuiltins example*. |
| lengthRange | This validator type applies to string values only. If the value is a string value validation will fail if the string's length falls outside the range specified by `validator.max` and `validator.min`.

Note that non-string values will always pass validation by this validator type.

Note that the `errorMessage` for this validator will be evaluated as a dynamicString - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`. |
| contains | Determine whether a string value contains some substring specified via `validator.substring`. |
| doesntContain | Determine whether a string value does **not** contain some substring specified via `validator.substring`. |
| substringCount | Determine whether a string value contains some substring multiple times. The substring to check for is specified via `validator.substring`. The `validator.operator` property allows you to specify how to test the number of substring occurrences. Valid values for this property are `==`, `!=`, `<`, `<=`, `>`, `>=`.

The number of matches to check for is specified via `validator.count`. |
| regexp | `regexp` type validators will determine whether the value specified matches a given regular expression. The expression should be specified on the `validator` object as the `expression` property.

See *formsRegularExpression example*. |
| mask | Validate against a regular expression mask, specified as `validator.mask`. If validation is successful a transformation can also be specified via the `validator.transformTo` property. This should be set to a string in the standard format for string replacement via the native JavaScript `replace()` method.

See *formsValueTransform example*. |
| dateRange | Tests whether the value for a date field is within the range specified. Range is inclusive, and is specified via `validator.min` and `validator.max`, which should be specified in [XML Schema date format](http://www.w3.org/TR/xmlschema-2/#dateTime) or as a live JavaScript Date object (for client-only validators only). To specify the range as exclusive of the min/mix values, set `exclusive` to `true`.

Note that the `errorMessage` for this validator will be evaluated as a dynamicString - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`. |
| floatLimit | Validate a field as a valid floating point value within a value range. Range is specified via `validator.min` and `validator.max`. Also checks precision, specified as number of decimal places in `validator.precision`. If `validator.roundToPrecision` is set a value that doesn't match the specified number of decimal places will be rounded to the nearest value that does.

For backwards compatibility only. Use "floatRange" and/or "floatPrecision" instead. |
| floatRange | Tests whether the value for this field is a floating point number within the range specified. The `max` and `min` properties on the validator are used to determine the acceptable range, inclusive. To specify the range as exclusive of the min/mix values, set `exclusive` to `true`.

Note that the `errorMessage` for this validator will be evaluated as a dynamicString - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`. |
| floatPrecision | Tests whether the value for this field is a floating point number with the appropriate number of decimal places - specified in `validator.precision` If the value is of higher precision and `validator.roundToPrecision` is specified, the value will be rounded to the specified number of decimal places and validation will pass, otherwise validation will fail. |
| required | A non-empty value is required for this field to pass validation.

In the case of a "binary" field, a non-empty file must be uploaded. |
| isUnique | Returns true if the value for this field is unique. The uniqueness check is performed across the whole DataSource unless you specify property `validator.criteriaFields` as a comma-separated string of field names; in that case, the uniqueness check is done in the context of those extra criteria, allowing you to check, for example, whether an employee number is unique for the department and location found on the record being validated. By default the uniqueness check is not case sensitive but this can be controlled through the [caseSensitive](classes/Validator.md#attr-validatorcasesensitive) attribute. You can specify the [operation](classes/DataSource.md#attr-datasourceoperationbindings) to use for the uniqueness check with the [operationId](classes/Validator.md#attr-validatoroperationid) attribute.

Validators of this type have [requiresServer](classes/ValidatorDefinition.md#attr-validatordefinitionrequiresserver) set to `true` and do not run on the client, unless all of the following are true:

*   The validation is run in the context of a DataBoundComponent or ValuesManager bound to some DataSource.
*   The DataSource is either clientOnly:true or cacheAllData: true and all data is loaded
*   The item is made available to the validator. Note that the item is not be available during a save performed without a form (eg programmatic save), or if the field is not available in the form.

Note when isUnique validator is executed as part of validation process during update operation, it will perform uniqueness check only for single row updates. If update targets [multiple records](classes/OperationBinding.md#attr-operationbindingallowmultiupdate), then isUnique validator will be skipped. If uniqueness check is needed when updating multiple records, consider using [custom DMI](kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) approach to add this check manually.

See *uniqueCheckValidation example*. |
| hasRelatedRecord | Returns true if the record implied by a relation exists. The relation can be derived automatically from the [DataSourceField.foreignKey](classes/DataSourceField.md#attr-datasourcefieldforeignkey) attribute of the field being validated, or you can specify it manually via `validator.relatedDataSource` and `validator.relatedField`.

You can specify at DataSource level that this validator should be automatically applied to all fields that specify a [foreignKey](classes/DataSourceField.md#attr-datasourcefieldforeignkey) - see [DataSource.validateRelatedRecords](classes/DataSource.md#attr-datasourcevalidaterelatedrecords).

By default the uniqueness check is not case sensitive but this can be controlled through the [caseSensitive](classes/Validator.md#attr-validatorcasesensitive) attribute.

Validators of this type have [requiresServer](classes/ValidatorDefinition.md#attr-validatordefinitionrequiresserver) set to `true` and do not run on the client.

Note that this validation is generally unnecessary for data coming from a UI. The typical UI uses a [SelectItem](classes/SelectItem.md#class-selectitem) or [ComboBoxItem](classes/ComboBoxItem.md#class-comboboxitem) with an [optionDataSource](classes/FormItem.md#attr-formitemoptiondatasource) for user entry, such that the user can't accidentally enter a related record if that doesn't exist, and a typical SQL schema will include constraints that prevent a bad insert if the user attempts to circumvent the UI. The primary purpose of declaring this validation explicitly is to provide clear, friendly error messages for use cases such as [BatchUploader](classes/BatchUploader.md#class-batchuploader), where values aren't individually chosen by the user. See also the example *Related Records*. |
| maxFileSize | This validator type is not for direct usage, instead [DataSourceField.maxFileSize](classes/DataSourceField.md#attr-datasourcefieldmaxfilesize) can be set and `maxFileSize` validator will be added automatically. Use [DataSource.maxFileSizeExceededMessage](classes/DataSource.md#classattr-datasourcemaxfilesizeexceededmessage) to customize validation error message.

In supported browsers (Internet Explorer 10+, Chrome, Firefox, Safari 6+, Opera 11.1+), returns `true` if the file(s) selected by the user are not larger than the field's [DataSourceField.maxFileSize](classes/DataSourceField.md#attr-datasourcefieldmaxfilesize). If not supported by the browser, the validator will always return `true`.

Note that server-side enforcement of the `maxFileSize` is always required because the user's browser might not support client-side file size checks. Also, any client-side check can be bypassed by a malicious user. |
| custom | Custom client-side validator. [Validator.condition](classes/Validator.md#attr-validatorcondition) will be called to verify data. |
| serverCustom | Custom server-side validator that either evaluates the Velocity expression provided in [serverCondition](classes/Validator.md#attr-validatorservercondition) (see *velocityValidation example*) or makes DMI call to [serverObject](classes/Validator.md#attr-validatorserverobject) to evaluate condition (see *dmiValidation example*).

Validators of this type have [requiresServer](classes/ValidatorDefinition.md#attr-validatordefinitionrequiresserver) set to `true` and do not run on the client. |

---
## Type: ValueItemType

### Description
Enum used within the [FilterBuilder](classes/FilterBuilder.md#class-filterbuilder) class to indicate the role of a particular value-field form item within a filter clause.

### Values

| Value | Description |
|-------|-------------|
| "value" | This is the single form item that will populate the generated [Criterion.value](classes/Criterion.md#attr-criterionvalue) for this clause. This applies for operators with [Operator.valueType](classes/Operator.md#attr-operatorvaluetype) of `"fieldType"` or `"custom"`. |
| "name" | This is the single form item that will populate the generated [Criterion.value](classes/Criterion.md#attr-criterionvalue) for [Operator.valueType](classes/Operator.md#attr-operatorvaluetype) of `"fieldName"`. |
| "start" | Indicates this item will generate the lower-bound value (or "start") when generating criteria with [Operator.valueType](classes/Operator.md#attr-operatorvaluetype) `"valueRange"`. |
| "end" | Indicates this item will generate the higher-bound value (or "end") when generating criteria with [Operator.valueType](classes/Operator.md#attr-operatorvaluetype) `"valueRange"`. |

---
## Type: VerticalAlignment

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Canvas.TOP | At the top of the container |
| Canvas.CENTER | Center within container. |
| Canvas.BOTTOM | At the bottom of the container |

### Groups

- appearance

---
## Type: ViewState

### Description
An object containing the "view state" information for a databound component.

Note that this object is a JavaScript string, and may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: VisibilityMode

### Description
Settings for whether multiple sections can be in the expanded state simultaneously.

### Values

| Value | Description |
|-------|-------------|
| "mutex" | Only one section can be expanded at a time. |
| "multiple" | Multiple sections can be expanded at the same time, and will share space. |

---
## Type: WriteToGeneratedFields

### Description
Indicates the category of "generated fields" the SmartClient Server should write values to, if defined on a [DSRequest](reference_2.md#object-dsrequest) - see [writeToGeneratedFields](classes/DSRequest.md#attr-dsrequestwritetogeneratedfields). At the time of writing we only support one such category, but this may be extended in the future.

### Values

| Value | Description |
|-------|-------------|
| "modifiersAndTimestamps" | Write `dsRequest`\-provided values for fields of type `modifier`, `creator`, `modifierTimestamp` and `creatorTimestamp` |

---
## Type: XMLDocument

### Description
XMLDocument is the "parsed" or object form of XML, which allows XML to be navigated as a tree of nodes with attributes, namespaces and other metadata, as opposed to being manipulated as just a String.

XMLDocument is a native object supplied directly by the browser. The SmartClient-supported interfaces for this object are methods that take an XMLDocument as an argument (such as [XMLTools.selectNodes](classes/XMLTools.md#classmethod-xmltoolsselectnodes)). If you want to retrieve XML data and display it in a SmartClient component, read about [XML Data Binding](kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration). To extract data as JavaScript Objects from XML, see [XMLTools.toJS](classes/XMLTools.md#classmethod-xmltoolstojs). Direct manipulation of XMLDocument is subject to cross-browser inconsistencies, bugs, memory leaks and performance issues.

---
## Type: XMLElement

### Description
An XMLElement represents one complete XML tag, including any subelements contained between the start and end tags.

XMLElement is a native object supplied directly by the browser. The SmartClient-supported interfaces for this object include methods that take an XMLElement as an argument (such as [XMLTools.selectNodes](classes/XMLTools.md#classmethod-xmltoolsselectnodes)). If you want to retrieve XML data and display it in a SmartClient component, read about [XML Data Binding](kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration). To extract data as JavaScript Objects from XML, see [XMLTools.toJS](classes/XMLTools.md#classmethod-xmltoolstojs). Direct manipulation of XMLElements objects is subject to cross-browser inconsistencies, bugs, memory leaks and performance issues.

---
## Type: XPathExpression

### Description
A standard XPath expression as a string. To learn about XPath, try the following search: [http://www.google.com/search?q=xpath+tutorial](http://www.google.com/search?q=xpath+tutorial)

---
## Object: AdvancedCriteria

### Description
AdvancedCriteria is a format for representing search criteria which may include operators on field values such as "less than", or may include sub-clauses such as several criteria applied to fields joined by an "OR" operator.

SmartClient DataSources can use AdvancedCriteria to search a list of [Record](#object-record)s, and the SmartClient Java Server can translate AdvancedCriteria to either SQL or Hibernate queries (**Note:** The server-side AdvancedCriteria handling feature is only available with the **Power** and **Enterprise** Editions of SmartClient; the Pro Edition is limited to ordinary criteria handling on the server side).

If the entire dataset is cached locally, SmartClient can perform AdvancedCriteria filtering on the client, avoiding a server call.

An AdvancedCriteria is an ordinary JavaScript object which can be created directly with JavaScript literal notation. For example:

```
 var advancedCriteria = {
        _constructor:"AdvancedCriteria",
        operator:"and",
        criteria:[
            // this is a Criterion
            { fieldName:"salary", operator:"lessThan", value:80000 },
            { operator:"or", criteria:[
                  { fieldName:"title", operator:"iContains", value:"Manager" },
                  { fieldName:"reports", operator:"notNull" }
              ]  
            },
            { fieldName:"startDate", operator:"greaterThan", value:new Date(1388552400000) }
        ]
    }
 
```
This makes AdvancedCriteria very easy to store and retrieve as JSON strings, using [JSONEncoder](classes/JSON.md#classmethod-jsonencode).

AdvancedCriteria can also be specified in [Component XML](kb_topics/componentXML.md#kb-topic-component-xml):

```
 <AdvancedCriteria operator="and" _constructor="AdvancedCriteria">
     <criteria>
         <Criterion fieldName="salary" operator="lessThan">
             <value xsi:type="xsd:float">80000</value>
         </Criterion>
         <Criterion operator="or">
             <criteria>
                 <Criterion fieldName="title" operator="iContains">
                     <value xsi:type="xsd:text">Manager</value>
                 </Criterion>
                 <Criterion fieldName="reports" operator="notNull"/>
             </criteria>
         </Criterion>
         <Criterion fieldName="startDate" operator="greaterThan">
             <value xsi:type="xsd:datetime">2014-01-01T05:00:00.000</value>
         </Criterion>
     </criteria>
 </AdvancedCriteria>
 
```
An AdvancedCriteria is in effect a [Criterion](reference_2.md#object-criterion) that has been marked with \_constructor:"AdvancedCriteria" to mark it as complete criteria.

In addition to directly creating an AdvancedCriteria object as described above, the [DataSource.convertCriteria](classes/DataSource.md#classmethod-datasourceconvertcriteria) and [DataSource.combineCriteria](classes/DataSource.md#classmethod-datasourcecombinecriteria) methods may be used to create and modify criteria based on simple fieldName / value mappings.

[Shorthand formats are allowed](kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) when defining AdvancedCriteria.

When passed to the SmartClient Server, a server-side AdvancedCriteria instance (in the package com.isomorphic.criteria) can be retrieved from a DSRequest via com.isomorphic.datasource.DSRequest.getAdvancedCriteria(). These same AdvancedCriteria objects can be directly created server side, and applied to a DSRequest via setAdvancedCriteria().

[RestDataSource](classes/RestDataSource.md#class-restdatasource), the recommended way of integration with servers that are not running the SmartClient Server Framework, defines a standard XML and JSON serialization of `AdvancedCriteria`. Date, DateTime and Time values use the same XML Schema representation used for other XML serialization like RestDataSource. Further details can be found at [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

It's a best practice for XML representation to have ``<value>`` as a subelement with `xsi:type`. Although most systems will auto-convert criteria explicitly setting type leaves the least room for error or ambiguity.

For other servers, you can translate `AdvancedCriteria` into whatever format is expected by the server, typically by implementing [DataSource.transformRequest](classes/DataSource.md#method-datasourcetransformrequest).

See [Criteria Editing](kb_topics/criteriaEditing.md#kb-topic-criteria-editing) for information about editing AdvancedCriteria in a DynamicForm.

When using the SmartClient Server, AdvancedCriteria created on the client and stored as JSON can be used directly by server code (without involvement of the browser and client-side system). Use the server-side API AdvancedCriteria.decodeClientCriteria() to obtain an AdvancedCriteria that can then be used with a server-created DSRequest object. Note that the client must be serialized by the [JSONEncoder](classes/JSONEncoder.md#class-jsonencoder) class, using [JSONEncoder.dateFormat](classes/JSONEncoder.md#attr-jsonencoderdateformat) "logicalDateConstructor".

### Groups

- advancedFilter

### See Also

- [ResultTree.useSimpleCriteriaLOD](classes/ResultTree.md#attr-resulttreeusesimplecriterialod)

---
## Object: AdvancedCriterionSubquery

### Description
A specialized subclass of [DSRequest](reference_2.md#object-dsrequest) that you use to declare the properties of a subquery (a [fieldQuery](classes/Criterion.md#attr-criterionfieldquery) or [valueQuery](classes/Criterion.md#attr-criterionvaluequery)) to be used in [AdvancedCriteria](#object-advancedcriteria). Subquery definitions are often very compact; only a few properties are permitted for a client-driven subquery (see "Restrictions on client-driven subqueries", below), and many use cases can be satisfied specifying just a [dataSource](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerydatasource) and a [summary function](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerysummaryfunctions).

Criteria subquery definitions fall into two broad categories:

*   **Aggregation**, where the subquery uses a [SummaryFunction](reference_2.md#type-summaryfunction) to aggregate or summarize a related dataset, and then filter on that aggregated or summarized value. For example, orders with more than 10 lines, customers with an average order value more than $1000, UK customers with an outstanding payment more than a week old, etc
*   **Related value**, where the subquery selects a value (or, for `inSet`\-type clauses, a set of values) from a related dataSource and then filters on that value. For example, Products that were not ordered last month, Employees who are based in one of the North American offices, Orders that include a particular category of Product, etc

In ideal circumstances - when both main and subquery [dataSource](classes/DataSource.md#class-datasource)s are [SQL DataSources](kb_topics/sqlDataSource.md#kb-topic-sql-datasources), and a number of other restrictions are satisfied - subqueries are implemented by incorporating their functionality into a larger overall SQL query, because this is the most efficient thing to do, and gives the best performance. See [canEmbedSQL](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerycanembedsql) for a description of the rules and nuances around this.

In cases where we cannot implement subqueries by embedding SQL, they are implemented by converting the subquery definitions into separate real `DSRequest`s, executing them, and then combining their results into the wider resultset.

#### Subquery Overview
Subqueries are used to derive a value to be compared as part of the main query, from a set of related data where there is no way to directly join to a single record (usually because the subquery is summarizing or extracting from a larger dataset). Each subquery must return a single value per record in the main query, because it going to be compared to a single value from each main record (this value either comes directly from the main record, or is derived via a `fieldQuery`)

Because the nature of a subquery is that it is deriving a single value from multiple records, subqueries are often involved in some kind of aggregation (returning a record count, or the minimum value, for example). While this is the most common use of subqueries, it is not the only one - see the "Simple valueQuery" example below.

Whether or not a subquery is aggregating multiple records, it typically needs to be constrained by a join to the outer query. For example, if you were looking for all customers that have placed more than $1000-worth of orders, you would use something like the "Simple aggregating subquery" below. As you will see, that example displays no explicit means of joining the subquery to the outer query, and yet one is obviously necessary because we are looking for the sum of "lineValue" customer-by-customer, not the total sum for all customers.

This join from the subquery to the outer query is applied implicitly by SmartClient's SQL engine. It auto-discovers a Relation between the main dataSource and subquery dataSource by following [foreignKey](classes/DataSourceField.md#attr-datasourcefieldforeignkey) definitions from the subquery dataSource, until it finds a path to the main dataSource. This auto-discovery usually does the right thing, but there are two possibilities it does not address:

*   There is no direct or indirect Relation from the subquery dataSource to the main dataSource. This is an unusual case for a subquery - most use use cases call for related dataSources - but valid cases are conceivable. To cope with this scenario, you set [queryFK](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryfk) to the special value "`***none***`". Note, if SmartClient fails to find a path from the subquery dataSource to the main dataSource and `queryFK:"*none*"` has not been set, the framework will log a warning and the fetch will fail
*   There is more than one direct or indirect Relation from the subquery dataSource to the main dataSource, and you want to use a different one from the one that was auto-discovered. Again, the solution is to explicitly name the [queryFK](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryfk) - see the documentation for that property for details of the syntax

Since SmartClient can only make use of a single value as output from a subquery, if your subquery returns multiple records, we will simply use the first. If the query returns multiple fields, you can specify the field to use as the subquery output with [queryOutput](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryoutput). If the subquery returns more than one field and no `queryOutput` is specified, we will use the first aggregated ([summaryFunction](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerysummaryfunctions)) field, or the first [grouped](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerygroupby) field if there are no aggregated fields, or the [primaryKey](classes/DataSourceField.md#attr-datasourcefieldprimarykey) field if there are also no `groupBy` fields, or just the first numeric field failing all else. Note, however, that although we attempt to derive a sensible value, it never makes sense to return multiple records from a subquery, and it only really makes sense to return multiple fields if you explicitly identify the correct field with `queryOutput`. Ideally, for the sake of clarity, return a single record, and either have that record contain a single field, or specify `queryOutput`

#### Restrictions on client-driven subqueries
For security reasons, subqueries in [requests](reference_2.md#object-dsrequest) that came from the client-side are only permitted to specify a handful of properties. These properties are sufficient to allow the full power of the subquery feature to be used, without allowing any of the much broader set of general properties associated with the `DSRequest` superclass. The properties that can be set in a client-driven subquery are just those that are documented as direct properties of the `AdvancedCriterionSubquery` class - specifically [canEmbedSQL](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerycanembedsql), [criteria](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerycriteria), [dataSource](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerydatasource), [groupBy](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerygroupby), [operationId](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryoperationid), [queryFK](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryfk), [queryOutput](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryoutput), and [summaryFunctions](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerysummaryfunctions)

For `DSRequest`s that originally came from the server, it is possible to have a subquery that specifies any `DSRequest` property. Many of these would only have any relevance or effect if the subquery was run separately rather than embedded (as described above and in the [canEmbedSQL](classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerycanembedsql) doc). If you need to do this, look in the server Javadoc for `DSRequest.setAllowArbitrarySubqueries(boolean)`

Finally, note that it is possible to switch off the ability to use subqueries altogether, either [per-DataSource](classes/DataSource.md#attr-datasourceallowcriteriasubqueries), or globally by setting the `allowCriteriaSubqueries` flag in your `server.properties` file:

```
 allowCriteriaSubqueries: false
 
```

#### Examples
Subqueries are quite hard to describe in narrative text, but the following examples demonstrate their use and should make things clearer

#### Simple aggregating subquery
This example uses a `fieldQuery` to select all Order records for customer 1234, where the order total (sum of all the order line values) is greater than $1000.
```
 Order.fetchData({
     _constructor: "AdvancedCriteria", operator: "and", criteria: [
         {fieldName: "customerNumber", operator: "equals", value: 1234},
         {
              fieldQuery: {
                  dataSource: "OrderLine",
                  summaryFunctions: {lineValue: "sum"}
              }, operator: "greaterThan", value: 1000
         }
     ] 
 });
 
```
#### Simple valueQuery
This example uses a `valueQuery` to derive the employeeNumber of a manager when we only know the email address of that manager, so we can find out who reports to her. This example shows how to use additional criteria within a subquery. It also demonstrates the relatively rare situation where no join to the outer dataSource is required (hence the declaration of `queryFK: "*none*"`)
```
 Employee.fetchData({
     _constructor: "AdvancedCriteria", operator: "and", criteria: [
         {
             fieldName: "reportsTo", 
             operator: "equals",
                 valueQuery: {
                     dataSource: "Employee",
                     queryFK: "*none*",
                     criteria: { operator: "and", criteria: [
                         {fieldName: "email", operator: "equals", value: 'mpatterson@classicmodelcars.com'}
                     ]
                 }
             }
         }
     ]
 });
 
```
#### More complex aggregation example
This example uses both a `fieldQuery` and a `valueQuery` to select all US-based customers who placed more orders in 2022 than they placed in 2021. Note, this is the number of orders, not the value, and the particular field that we add the "count" function to is not important (count is the same regardless of which field you count). We chose the orderNumber in this case, but that choice is arbitrary
```
 Customer.fetchData({
     _constructor: "AdvancedCriteria", operator: "and", criteria: [
         {fieldName: "country", operator: "equals", value: "USA"},
         {
             fieldQuery: {
                 dataSource: "Order",
                 summaryFunctions : { orderNumber : "count" },
                 criteria: {fieldName: "orderDate", operator: "iBetweenInclusive", 
                                         start:new Date("2021-01-01"), end:new Date("2021-12-31")}
             }, 
             operator: "lessThan",
             valueQuery: {
                 dataSource: "Order",
                 summaryFunctions : { orderNumber : "count" },
                 criteria: {fieldName: "orderDate", operator: "iBetweenInclusive", 
                                         start:new Date("2022-01-01"), end:new Date("2022-12-31")}
             }
         }
     ]
 });
 
```

### Groups

- advancedFilter

---
## Object: AIMessage

### Description
An individual message in the list of [AIRequest.messages](classes/AIRequest.md#attr-airequestmessages) of an AI request.

---
## Object: AIRequest

### Description
Represents a request to AI for a response.

---
## Object: AnimateShowEffect

### Description
Configuration object for effect to apply during an animated show or hide.

---
## Object: ApplyAIFilterResponse

### Description
Represents the result of a request to evaluate an "aiFilter" [AdvancedCriteria](#object-advancedcriteria) on a list of records.

### See Also

- [AI.applyAIFilter](classes/AI.md#classmethod-aiapplyaifilter)

---
## Object: AsyncDataBoundOperationContext

### Description
Context for an asynchronous data-bound operation.

### See Also

- [AsyncDataBoundOperationParams](#object-asyncdataboundoperationparams)

---
## Object: AsyncDataBoundOperationParams

### Description
Parameters to an asynchronous data-bound operation.

### See Also

- [AsyncDataBoundOperationContext](#object-asyncdataboundoperationcontext)

---
## Object: AsyncMultipleValuesGenerationResult

### Description
The result of an asynchronous operation to generate multiple values.

### Groups

- fieldGeneration

---
## Object: AsyncOperationContext

### Description
Context for an asynchronous operation.

### See Also

- [AsyncOperationParams](#object-asyncoperationparams)

---
## Object: AsyncOperationParams

### Description
Parameters to an asynchronous operation.

### See Also

- [AsyncOperationContext](#object-asyncoperationcontext)

---
## Object: AsyncOperationResult

### Description
An object containing information about the result of an asynchronous operation.

Note: [isc.defaultAsyncOperationCatchCallback](classes/isc.md#staticmethod-iscdefaultasyncoperationcatchcallback) can be used to provide default error handling for a [Promise](reference_2.md#object-promise)-based asynchronous operation.

---
## Object: AsyncSingleValueGenerationResult

### Description
The result of an asynchronous operation to generate a value.

### Groups

- fieldGeneration

---
## Object: AutoTestLocatorConfiguration

### Description
Configuration object for generating [AutoTestLocators](reference_2.md#type-autotestlocator).

An AutoTestLocatorConfiguration may be passed to [AutoTest.getLocator](classes/AutoTest.md#classmethod-autotestgetlocator) to override default locator configuration settings.

---
## Object: BrowserWindowSettings

### Description
Allows specifying additional browser window settings when calling the underlying JavaScript or OpenFin call to create the child window in [MultiWindow.open](classes/MultiWindow.md#classmethod-multiwindowopen).

---
## Object: BuildAIFieldRequestContext

### Description
—

### See Also

- [AI.buildAIFieldRequest](classes/AI.md#classmethod-aibuildaifieldrequest)

---
## Object: BuildAIFieldRequestResponse

### Description
Represents a response to a request to build an [AIFieldRequest](reference_2.md#object-aifieldrequest) from a natural language description of the per-record values to generate for a new AI-generated field.

### See Also

- [AI.buildAIFieldRequest](classes/AI.md#classmethod-aibuildaifieldrequest)

---
## Object: BuildCriterionResponse

### Description
Represents a response to a request to build an [AdvancedCriteria](#object-advancedcriteria) object from a natural language description of a filter.

### See Also

- [AI.buildCriterion](classes/AI.md#classmethod-aibuildcriterion)

---
## Object: BuildHilitesRequest

### Description
Represents a request to AI for creation of one or more [Hilite](reference_2.md#object-hilite) objects from a natural language description of hilite criteria and styling to apply.

### See Also

- [AI.buildHilites](classes/AI.md#classmethod-aibuildhilites)

---
## Object: BuildHilitesResponse

### Description
Represents a response from AI to a request to build one or more [Hilite](reference_2.md#object-hilite) objects.

### See Also

- [AI.buildHilites](classes/AI.md#classmethod-aibuildhilites)

---
## Object: BuildUIViaAIContext

### Description
Context for an ongoing build-UI-via-AI operation.

---
## Object: BuildUIViaAIResponse

### Description
Represents a response from AI to a user's request to build UI element(s).

---
## Object: BuildViaAIRequest

### Description
Base class for a representation of a high-level request to AI to build something.

---
## Object: BuildViaAIResponse

### Description
Base class for a representation of a response to a high-level request to AI to build something.

---
## Object: CalendarEvent

### Description
A type of [Record](#object-record) which represents an event to occur at a specific time, displayed within the calendar.

### Groups

- data

---
## Object: CellRecord

### Description
A CellRecord represents the data for one cell of the body area.

Each CellRecord should be an object that minimally has a property named after each visible facetId with the value being a facetValueId from that facet, and also a value for [CubeGrid.valueProperty](classes/CubeGrid.md#attr-cubegridvalueproperty).

Cell records can contain any other properties desired, such as cell ids, or values for facets not initially shown.

---
## Object: CreateScreenSettings

### Description
Controls what class and instance substitutions, if any, are applied during a call to [RPCManager.createScreen](classes/RPCManager.md#classmethod-rpcmanagercreatescreen). Classes and instances can be mapped (constructed as) other classes, and existing widget instances can be returned for new ones.

### See Also

- [CreateScreenSettings.classSubstitutions](classes/CreateScreenSettings.md#attr-createscreensettingsclasssubstitutions)
- [CreateScreenSettings.componentSubstitutions](classes/CreateScreenSettings.md#attr-createscreensettingscomponentsubstitutions)

---
## Object: CriteriaOutputSettings

### Description
Settings for generation of AdvancedCriteria descriptions.

---
## Object: CriterionValues

### Description
An object that contains information needed to evaluate an [operator](#object-operator) on a record.

### Groups

- advancedFilter

---
## Object: DataContext

### Description
A mapping from [DataSource](classes/DataSource.md#class-datasource) IDs to specific [Records](#object-record).

To understand how `dataContext` is used to automatically populate [DataBoundComponents](#interface-databoundcomponent), see [Canvas.autoPopulateData](classes/Canvas.md#attr-canvasautopopulatedata).

For example, in JavaScript:

```
   {
      "Customer": { customerNumber: "15", name: "Trish Joiner" },
      "Employee": { employeeID: "4231", name: "Fred Smith" }
   }
 
```

---
## Object: DataContextBinding

### Description
Identical to a [DataContext](#object-datacontext) but in addition to fixed values, [ruleContext](classes/Canvas.md#method-canvasgetrulecontext) values can be specified by prefixing the `ruleContext` path with `$ruleScope.` as shown below:

For example, in JavaScript:

```
   {
      "Customer": { customerNumber: "$ruleScope.customerGrid.values.customerNumber" }
   }
 
```

When used within a Workflow [SetScreenDataTask](#class-setscreendatatask) or [AddScreenTask](classes/AddScreenTask.md#class-addscreentask), any applicable [taskInputExpression](kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) can be used as a value.

To use a literal value that starts with one of the expressions described above, prefix the leading dollar sign ($) with a backslash (\\) (ex. "\\$ruleScope.goes.here") to prevent the value from being resolved as an expression.

---
## Object: DBCField

### Description
Represents a field in a [DataBoundComponent](#interface-databoundcomponent).

### See Also

- [ListGridField](reference_2.md#object-listgridfield)
- [DetailViewerField](#object-detailviewerfield)

---
## Object: DetailViewerField

### Description
An object literal with a particular set of properties used to configure the display of and interaction with the rows of a [DetailViewer](classes/DetailViewer.md#class-detailviewer).

---
## Object: DetailViewerRecord

### Description
A DetailViewerRecord is an object literal with properties that define the values for the various fields of a [DetailViewer](classes/DetailViewer.md#class-detailviewer).

For example a DetailViewer that defines the following fields:

```
 fields : [
     {name: "field1"},
     {name: "field2"}
 ],
 
```
Might have the following data:
```
 data : [
     {field1: "foo", field2: "bar"},
     {field1: "field1 value", field2: "field2 value"}
 ]
 
```
Each element in the data array above is an instance of DetailViewerRecord - notice that these are specified simply as object literals with properties.

---
## Object: DrawShapeCommand

### Description
Holds the information of a drawing command.

---
## Object: EditNode

### Description
An object representing a component that is currently being edited within an [EditContext](classes/EditContext.md#class-editcontext).

An EditNode is essentially a copy of a [PaletteNode](#object-palettenode), initially with the same properties as the PaletteNode from which it was generated. However unlike a PaletteNode, an EditNode always has a [liveObject](classes/EditNode.md#attr-editnodeliveobject) - the object created from the [PaletteNode.defaults](classes/PaletteNode.md#attr-palettenodedefaults) or other properties defined on a paletteNode.

Like a Palette, an EditContext may use properties such as [PaletteNode.icon](classes/PaletteNode.md#attr-palettenodeicon) or [PaletteNode.title](classes/PaletteNode.md#attr-palettenodetitle) to display EditNodes.

An EditContext generally offers some means of editing EditNodes and, as edits are made, updates [EditNode.defaults](classes/EditNode.md#attr-editnodedefaults) with the information required to re-create the component.

---
## Object: ElementWaitConfig

### Description
Configuration object for [AutoTest.waitForElement](classes/AutoTest.md#classmethod-autotestwaitforelement)

---
## Object: EventStreamData

### Description
A JavaScript object representing the state of a live [EventStream](classes/EventStream.md#class-eventstream) instance, including all captured events retained by the stream. When [EventStream.end](classes/EventStream.md#method-eventstreamend) is called to complete capturing, a `EventStreamData` object is returned.

Note that `EventStreamData` is essentially JSON, except that dates remain JavaScript [Date](reference_2.md#object-date)s, rather than being converted to string format. This ensures that if you [serialize](classes/JSON.md#classmethod-jsonencode) the data and then [deserialize](classes/JSON.md#classmethod-jsondecode) it, dates round trip properly and time zone information is not lost.

### Groups

- experimental

### See Also

- [EventStreamEvent](#object-eventstreamevent)

---
## Object: EventStreamEvent

### Description
A JavaScript object representing an event captured by a [EventStream](classes/EventStream.md#class-eventstream). `EventStreamEvent`s may represent DOM events (wrapped by the [EventHandler](classes/EventHandler.md#class-eventhandler)), or other operations such as [relogins](kb_topics/relogin.md#kb-topic-relogin) or [Reify](kb_topics/reify.md#kb-topic-reify-overview) file operations on screens and projects.

An [eventType](classes/EventStreamEvent.md#attr-eventstreameventeventtype) should always be present, but not all properties will be present for a given `EventStreamEvent`, since their relevance depends on the `eventType`.

In addition to the instance attributes documented for `EventStreamEvent`, if we're capturing [move events](classes/EventStream.md#attr-eventstreamcapturemoveevents) but not [drag events](classes/EventStream.md#attr-eventstreamcapturedragevents), the move event starting a drag will be tagged with the drag start `eventType` as a boolean attribute. So for example,

```
     dragResizeStart: true
```
might appear in the `EventStreamEvent` for a `mouseMove`, if it started a drag but we weren't capturing [drag events](classes/EventStream.md#attr-eventstreamcapturedragevents).

### Groups

- experimental

---
## Object: FacetValue

### Description
Facet value definition object made use of by the [CubeGrid](classes/CubeGrid.md#class-cubegrid) and [FacetChart](classes/FacetChart.md#class-facetchart) classes (contained by facets).

---
## Object: FacetValueMap

### Description
A JavaScript Object where each property name is a facetId and each property value is a facetValueId for that facet.

The facetId → facetValueId mappings in a FacetValueMap describe a specific slice of the dataset. If mappings are included for all facets, a FacetValueMap describes a unique cell. If some facets are omitted, it describes a row, column, or set of rectangular areas, or equivalently, a particular row or column header (if all facetIds in the map are displayed on the same axis)

FacetValueMaps are used in various contexts to describe headers, datasets to be loaded, screen regions, etc.

---
## Object: FileSpec

### Description
A record which specifies files for use with [FileSource Operations](kb_topics/fileSource.md#kb-topic-filesource-operations).

### Groups

- fileSource

### See Also

- [DataSource.makeFileSpec](classes/DataSource.md#classmethod-datasourcemakefilespec)

---
## Object: FiscalCalendar

### Description
An object representing the start date for fiscal years in the current locale.

A fiscal year spans a configurable date range - it may not exactly match a calendar year in length and it can start on any date within the calendar year and potentially end in the next calendar year.

Developers may specify explicit fiscal year start dates by adding [FiscalYear](reference_2.md#object-fiscalyear) objects to the [fiscal years array](classes/FiscalCalendar.md#attr-fiscalcalendarfiscalyears). If none are provided, or if there is no entry for the given year, one is manufactured based on the default [month](classes/FiscalCalendar.md#attr-fiscalcalendardefaultmonth) and [date](classes/FiscalCalendar.md#attr-fiscalcalendardefaultdate).

---
## Object: FormItemIcon

### Description
Form item icon descriptor objects used by Form Items to specify the appearance and behavior of icons displayed after the item in the page flow.

### Groups

- formIcons

### See Also

- [FormItem.icons](classes/FormItem.md#attr-formitemicons)

---
## Object: GroupNode

### Description
An auto-generated subclass of [TreeNode](reference_2.md#object-treenode) representing the group nodes in a grouped [ListGrid](classes/ListGrid_1.md#class-listgrid).

### Groups

- grouping

### See Also

- [ListGrid.groupBy](classes/ListGrid_2.md#method-listgridgroupby)

---
## Object: History

### Description
This class provides synthetic history support. Using this class, you can create history entries at any point and be called back when the user next navigates to any of these history entries via any of the browser mechanisms that enable navigation: back/forward buttons, history dropdown and bookmarks.

The history entries created using this mechanism work just like history entries created natively by the browser, except you get a callback whenever a transition occurs. This implementation correctly handles "deep" history - i.e. it correctly maintains forward and back history when the user navigates forward or back away from the page that uses this module.

This module is usable independent of the rest of SmartClient - you can use it on pages that don't load any other modules.

**Platform Notes:**  
In Safari (4.0 and above), this module has the limitation that the arbitrary data parameter in addHistoryEntry() is not reliable.  
Internet Explorer: If you set document.domain on the top-level page, the History mechanism will behave sub-optimally in IE - three clicks one the forward/back buttons will be required to transition to the next history entry.

**Usage overview**  
Synthetic history entries are added to the browser history via [History.addHistoryEntry](classes/History.md#staticmethod-historyaddhistoryentry). When this method is called, the page's URL will be modified and the native browser back button will become active.  
The [History.registerCallback](classes/History.md#staticmethod-historyregistercallback) allows the developer to register a callback method to fire when the user navigates to these generated history entries. This method will be fired with an appropriate history ID when the user hits the back-button or explicitly navigates to the URL generated for some synthetic history entry.

---
## Object: IconSet

### Description
An object with a unique name that groups together [known images](classes/IconSet.md#attr-iconsetstockicons) as an array of [stockIcons](reference_2.md#object-stockicon) and/or [mappings](classes/IconSet.md#attr-iconsetmappings) from existing [stockIcon-names](classes/StockIcon.md#attr-stockiconname) to new [src-strings of any type](#type-scimgurl). Provides a means of applying an overlay that will replace many or all registered stockIcons, and/or install a set of custom stockIcons, in a single call.

The framework ships with many builtin [StockIcons](classes/Media.md#classmethod-mediagetstockiconnames) and has two builtin IconSets that use them:

*   "skin" - this is the default IconSet for skins - it doesn't apply any mappings, so it uses the StockIcon ${isc.DocUtils.linkForRef('attr:StockIcon.fromSrc','fromSrc\\'s')} and shows the icons from the skin's "images/" directory
*   "svg\[:weight:style\]" - this _IconSet_ installs _mappings_ that replace all framework usage of on-disk image files with stylable [SVG symbols](kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview), largely from a single .svg file. These SVG graphics are available at weights ranging from 100 to 700 and in _outlined_ and _filled_ styles. You choose among these by appending a weight and/or a style-name, "filled" or "outlined", each prefixed with a colon (":").

These builtin IconSets may be used at runtime by passing their names directly to [Media.useMedia()](classes/Media.md#classmethod-mediausemedia).
```
 // use the default media from the skin's images/ directory
 isc.Media.useMedia("skin")

 // use "svg", which requires either a weight or style 

 // no style - uses the default style "outlined"
 isc.Media.useMedia("svg:400")
 
 // no weight - uses the default weight, "400"
 isc.Media.useMedia("svg:outlined")
 
 // weight 500, style "filled"
 isc.Media.useMedia("svg:500:filled")
 
```
Note that the "svg" IconSet requires skin-configuration changes to achieve sizing and scaling behavior that matches our Shiva skin.

Developers may also create custom `IconSets` to define new StockIcons or map existing ones to new image-sources. A custom IconSet may be applied at runtime by passing it directly to [Media.useMedia()](classes/Media.md#classmethod-mediausemedia). This will [add the IconSet](classes/Media.md#classmethod-mediaaddiconset) to the [registered list](classes/Media.md#classattr-mediaiconsets), if it isn't already there, and then [add](classes/Media.md#classmethod-mediaaddstockicons) any [new stockIcons](classes/IconSet.md#attr-iconsetstockicons) it defines and apply its [mappings](classes/Media.md#classmethod-mediaupdateiconmappings) to modify the src-strings for existing icons, replacing all uses of each named stockIcon in your application.

Typically, this will take effect immediately with no further action by the developer.

If you define multiple [iconSets](classes/Media.md#classattr-mediaiconsets) with mappings, you can switch between them to change all your app-icons at runtime without any need for code-changes.

Similarly, you can define multiple iconSets that only add new StockIcons for a certain part of your product, so they're only installed when that product-module is loaded, or affect only some of the registered _StockIcons_. Then, you can call _useMedia()_ multiple times, so you can compartmentalize your graphics into separate overlays, if that's beneficial.
## Examples

#### Example 1
In this example, the "chevronIconSet" IconSet maps a bunch of builtin StockIcon-names to new target src-strings, replacing all uses of the original. This code maps the original PNG files to sprite-strings that use SVG Symbols from a custom file at _\[APP\]newMedia/svgSprite.svg_. The code only shows 4 icons being mapped, but you could equally map all of the builtin StockIcons in a single "overlay" IconSet, and that would replace all framework icons with customized ones.
- // IconSet that maps the builtin Chevron StockIcons to new src-strings, which point to
- // individual [SVG Symbols](kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview) in a sprite file
- var chevronIconSet = {
- name: "chevronIconSet",
- mappings: {
- "Chevron\_Up": "sprite:svg:\[APP\]newMedia/svgSprite.svg#chevron\_up",
- "Chevron\_Down": "sprite:svg:\[APP\]newMedia/svgSprite.svg#chevron\_down",
- "Chevron\_Left": "sprite:svg:\[APP\]newMedia/svgSprite.svg#chevron\_left",
- "Chevron\_Right": "sprite:svg:\[APP\]newMedia/svgSprite.svg#chevron\_right"
- }
- };
- isc.Media.useMedia(chevronIconSet);
#### Example 2
In this example, the "logoIconSet" defines a few new StockIcons for existing image-paths.
```
  // IconSet that defines StockIcons for logo images in the application root
  var logoIconSet = {
      name: "logoIconSet",
      stockIcons: [
          {
              name: "ProductLogo",
              fromSrc: "[APP]productLogo.png",
          },
          {
              name: "AccountsModuleLogo",
              fromSrc: "[APP]accountsLogo.png",
          },
          {
              name: "CalendarModuleLogo",
              fromSrc: "[APP]calendarLogo.png",
          }
      ]
  };

  isc.Media.useMedia(logoIconSet);
 
```

If your project bootstrap runs this code, you may then use the names of these new StockIcons in image-sources, such as [Button.icon](classes/Button.md#attr-buttonicon): "ProductLogo", and extend them as described [here](reference_2.md#object-stockicon), anywhere in your project. Any request for the StockIcon-names will render the associated **fromSrc**, since no [target src](classes/StockIcon.md#attr-stockiconsrc) has been set.

#### Example 3
If you support multiple skins in your project, you may have icons that look great on light-colored backgrounds, but need to be lighter in order to look good on dark backgrounds. To do that, you can create another IconSet that defines new src-string mappings for your StockIcons, and install it in the dark-skin's _load\_skin.js_ file, or other load-time code, after the first IconSet has been installed so the StockIcons are present.
```
  // IconSet that maps custom logo-StockIcons to lighter images in darker skins
  var logoIconSetLight = {
      name: "logoIconSetLight",
      mappings: {
          "ProductLogo": "[APP]productLogoLight.png"
          "AccountsModuleLogo": "[APP]accountsLogoLight.png",
          "CalendarModuleLogo": "[APP]calendarLogoLight.png",
      }
  };

  isc.Media.useMedia(logoIconSetLight);
 
```
When this code is run in a Dark skin, any requests from code for the original "\[APP\]productLogo.png" or it's StockIcon name "ProductLogo" will be automatically mapped to the new file, "\[APP\]productLogoLight.png".

### Groups

- media
- stockIcons

---
## Object: ImgProperties

### Description
A set of properties that can be used to create an image.

**Deprecated**

---
## Object: isA

### Description
A library of functions for determining the types of other objects.  
  
The "isA" methods for the basic JavaScript types are much faster and more consistent across platforms than JavaScript's "typeof" operator.  
  
An isA method is automatically created for every ISC Class and Interface definition, for example, isA.Canvas().

---
## Object: isc

### Description
`window.isc` is the base object for the Isomorphic SmartClient framework. Every SmartClient class is available on this object as `isc._ClassName_`. The `isc` also contains a number of static utility methods.

See also [Simple Names mode](kb_topics/simpleNamesMode.md#kb-topic-simple-names-mode).

---
## Object: KeyIdentifier

### Description
Identifier for a key pressed by the user, optionally specifying whether the Shift, Control, and/or Alt keys should be held or not held when the key is pressed, used by various methods.

---
## Object: Lane

### Description
Lane shown in a [Timeline](#class-timeline) view, or in a [day view](classes/Calendar.md#attr-calendardayview) when [showDayLanes](classes/Calendar.md#attr-calendarshowdaylanes) is true. Each lane is a row or column, respectively, that can contain a set of [CalendarEvent](#object-calendarevent)s. CalendarEvents are placed in lanes by matching the [Lane.name](classes/Lane.md#attr-lanename) property to the value of the [Calendar.laneNameField](classes/Calendar.md#attr-calendarlanenamefield) property on the CalendarEvent.

Lanes are typically used to show tasks assigned to different people, broadcasts planned for different channels, and similar displays.

---
## Object: LinearGradient

### Description
Definition of a linear gradient between two points, ([x1](#attr-lineargradientx1), [y1](#attr-lineargradienty1)) and ([x2](#attr-lineargradientx2), [y2](#attr-lineargradienty2)).

---
## Object: LoadingIndicatorSettings

### Description
Set of properties to configure the loading indicator displayed by [FileLoader.showLoadingIndicator](classes/FileLoader.md#classmethod-fileloadershowloadingindicator)

---
## Object: MultiWindowSettings

### Description
Allows specifying settings to apply to the [MultiWindow](classes/MultiWindow.md#class-multiwindow) of a child window.

---
## Object: NavItem

### Description
Properties for a navigation item in a [NavPanel](classes/NavPanel.md#class-navpanel).

---
## Object: NotifyAction

### Description
Represents an action that's associated with a message. Similar to the object form of [Callback](#type-callback), except a title must also be specified, which is rendered as a clickable link in the message (unless [wholeMessage](#attr-notifyactionwholemessage) is set).

### See Also

- [Notify.configureMessages](classes/Notify.md#classmethod-notifyconfiguremessages)

---
## Object: NotifySettings

### Description
An object used to configure how messages shown by [Notify.addMessage](classes/Notify.md#classmethod-notifyaddmessage) are drawn and behave.

### See Also

- [Notify.addMessage](classes/Notify.md#classmethod-notifyaddmessage)
- [Notify.configureMessages](classes/Notify.md#classmethod-notifyconfiguremessages)

---
## Object: Number

### Description
Extra methods added to the Number object, available on all number variables. Attributes, parameters, or return values declared as `Number` may be null.

### See Also

- [Integer](reference_2.md#type-integer)
- [Double](#type-double)
- [Float](#type-float)

---
## Object: Operator

### Description
Specification of an operator for use in filtering, for example "equals". Use with [DataSource.addSearchOperator](classes/DataSource.md#method-datasourceaddsearchoperator) to define custom filtering behaviors for client-side filtering.

### Groups

- advancedFilter

---
## Object: PaletteNode

### Description
An object representing a component which the user may create dynamically within an application.

A PaletteNode expresses visual properties for how the palette will display it (eg [title](classes/PaletteNode.md#attr-palettenodetitle), [icon](classes/PaletteNode.md#attr-palettenodeicon)) as well as instructions for creating the component the paletteNode represents ([PaletteNode.type](classes/PaletteNode.md#attr-palettenodetype), [PaletteNode.defaults](classes/PaletteNode.md#attr-palettenodedefaults)).

Various types of palettes ([ListPalette](#class-listpalette), [TreePalette](#class-treepalette), [MenuPalette](#class-menupalette), [TilePalette](#class-tilepalette)) render a PaletteNode in different ways, and allow the user to trigger creation in different ways (eg drag and drop, or just click). All share a common pattern for how components are created from palettes.

Note that in a TreePalette, a PaletteNode is essentially a [TreeNode](reference_2.md#object-treenode) and can have properties expected for a TreeNode (eg, [showDropIcon](classes/TreeGrid.md#attr-treegridcustomicondropproperty)). Likewise a PaletteNode in a MenuPalette can have the properties of a [MenuItem](reference_2.md#object-menuitem), such as [MenuItem.enableIf](classes/MenuItem.md#method-menuitemenableif).

---
## Object: PlaceholderDefaults

### Description
An object representing the configuration of the placeholder. When a placeholder is created and not replaced by the target component, these are the properties that are applied.

### Groups

- devTools

---
## Object: PointerSettings

### Description
A set of properties that can be used to configure a [canvas pointer](classes/Canvas.md#attr-canvasshowpointer).

---
## Object: RadialGradient

### Description
Definition of a radial gradient.

---
## Object: ReapplyAIFilterRequest

### Description
Represents a request to AI to re-evaluate an "aiFilter" [AdvancedCriteria](#object-advancedcriteria) on a list of updated records.

### See Also

- [AI.asyncReapplyAIFilter](classes/AI.md#classmethod-aiasyncreapplyaifilter)

---
## Object: ReapplyAIFilterResponse

### Description
Represents the result of a request to re-evaluate an "aiFilter" [AdvancedCriteria](#object-advancedcriteria) on a list of updated records.

### See Also

- [AI.asyncReapplyAIFilter](classes/AI.md#classmethod-aiasyncreapplyaifilter)

---
## Object: Record

### Description
A Record is an ordinary JavaScript Object with properties that are treated as data to be displayed and edited by a [DataBoundComponent](#interface-databoundcomponent).

[DataBoundComponent](#interface-databoundcomponent)s have a concept of [named fields](classes/DataBoundComponent.md#attr-databoundcomponentfields), where values for each field are found under the same-named property in a Record.

A Record is always an ordinary JavaScript Object regardless of how the record is loaded (static data, java server, XML web service, etc), and so supports the normal behaviors of JavaScript Objects, including accessing and assigning to properties via dot notation:

```
     var fieldValue = record.fieldName;
     record.fieldName = newValue;
 
```

The concept of working with Records is common to all [DataBoundComponent](#interface-databoundcomponent)s, although individual DataBoundComponents may work with singular records ([DynamicForm](classes/DynamicForm.md#class-dynamicform)) or may work with lists ([ListGrid](classes/ListGrid_1.md#class-listgrid)), trees ([TreeGrid](classes/TreeGrid.md#class-treegrid)), or cubes ([CubeGrid](classes/CubeGrid.md#class-cubegrid)) of records.

Individual DataComponents may also look for special properties on Records which control styling or behavior for those records, such as [`record.canEdit`](classes/ListGrid_1.md#attr-listgridrecordeditproperty).

---
## Object: RelationPath

### Description
A simple object representing the path for navigation from source to target DataSources via foreign key declarations defined between each.

---
## Object: RelativeDate

### Description
An object representing a relative date, useful for representing date ranges etc in criteria. RelativeDate objects may be created directly by SmartClient components such as the [RelativeDateItem](classes/RelativeDateItem.md#class-relativedateitem).

RelativeDate objects will have `"_constructor"` set to `"RelativeDate"` and must have a specified [RelativeDate.value](#attr-relativedatevalue). Any other attributes are optional.

---
## Object: RESTAuthentication

### Description
Authentication settings, applicable only to the [RestConnector](kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector)

### Groups

- serverRestConnector

---
## Object: RPCRequest

### Description
Encapsulates a client/server RPC request. You'll need to provide an instance of this class (or a constructor for it) to the [RPCManager.sendRequest](classes/RPCManager.md#classmethod-rpcmanagersendrequest) method. If you use the [RPCManager.send](classes/RPCManager.md#classmethod-rpcmanagersend) method, an instance of RPCRequest will be created for you.

### See Also

- [RPCManager.send](classes/RPCManager.md#classmethod-rpcmanagersend)
- [RPCManager.sendRequest](classes/RPCManager.md#classmethod-rpcmanagersendrequest)

---
## Object: SCStatefulImgConfig

### Description
A configuration object containing image URLs for a set of possible images to display based on the [state](classes/StatefulCanvas.md#attr-statefulcanvasstate) of some components. See the [stateful images overview](kb_topics/statefulImages.md#kb-topic-stateful-images) for more information.

Each attribute in this configuration object maps a state to a target URL.  
Each URL may be specified in one of three ways

*   a standard [SCImgURL](#type-scimgurl) may be used to refer directly to an image file.
*   the `"#state:"` prefix may be used to display media from another specified state.
*   the `"#modifier:"` prefix may be used to specify a modifier string to apply to the [base image](classes/SCStatefulImgConfig.md#attr-scstatefulimgconfig_base).  
    The modifier will be applied to the base file name before the file type suffix.

For example, consider a stateful image config with the following properties:
```
 {    _base:"button.png",
      Over:"bright_button.png",
      Focused:"#state:Over",
      Selected:"#state:Over",
      Disabled:"#modifier:_Disabled",
      SelectedDisabled:"#state:Selected"
 }
 
```
In this case

*   the base image URL and the the "Over" state image URL would be determined using the standard [SCImgURL](#type-scimgurl) rules
*   the "Focused" and "Selected" state images would re-use the "Over" state image (`"bright_button.png"`)
*   the "Disabled" state image would be the base state image with a `"_Disabled"` suffix applied to the file name (`"button_Disabled.png"`)
*   the `"SelectedDisabled"` entry would be used for the combined `"Selected"` and `"Disabled"` states, and would re-use the "Selected" state image (which in turn maps back to the "Over" state, resolving to `"bright_button.png"`)

The default set of standard states are explicitly documented, but this object format is extensible. A developer may specify additional attributes on a SCStatefulImgConfig beyond the standard documented states and they may be picked up if a custom state is applied to a component (via a call to [StatefulCanvas.setState](classes/StatefulCanvas.md#method-statefulcanvassetstate), for example).

In some cases, an icon may have only custom states - for example, a tree-folder icon is always either opened or closed. In these cases, a `_base` entry is only required if entries in the object use the _#state_ or _#modifier_ components.

#### Combined states and missing entries:
The [focused](classes/Canvas.md#method-canvasisfocused) and [selected](classes/StatefulCanvas.md#attr-statefulcanvasselected) states may be applied to a component in combination with other states. For example an [ImgButton](classes/ImgButton.md#class-imgbutton) marked both _Selected_ and _Disabled_ will look for media to represent this combined state. To provide such media in a SCStatefulImgConfig, use the combined state names (in this case `SelectedDisabled`).  
If a component is both _Selected_ and _Focused_, three-part combined states are also possible (Selected + Focused + Over gives `SelectedFocusedOver` for example).

The SCStatefulImgConfig format may be sparse - developers may skip providing values for certain states (or combined states) in the SCStatefulImgConfig object. In this case the system will back off to using one of the state image entries that has been explicitly provided, according to the following rules:

| State(s) | Stateful image attributes to consider (in order of preference) |
|---|---|
| Focused and Selected | If both focused and selected states are applied, the system will use the first (populated) value from the following attribute list:"FocusedSelected""Focused""Selected" |
| Over or Down in combination with Focused / Selected | System will check for a combined state attribute with the Focused / Selected state first.For example for Focused + Selected + Over, consider the following attributes:"FocusedSelectedOver""FocusedOver""SelectedOver"If no combined state entry is specified, back off to considering just the Focused / Selected state:"FocusedSelected""Focused""Selected"If no focused / selected state entry is present in the config object, look for an entry for the unmodified state name"Over" |
| All other states, including Disabled (in combination with Focused / Selected) | Check for a combined state attribute with the Focused / Selected state first.For example for Focused + Selected + "CustomState", consider the following attributes:"FocusedSelectedCustomState""FocusedCustomState""SelectedCustomState"If no combined state entry is specified, back off to considering just the unmodified state name"CustomState"If there is no explicit entry for the state name, use the Focused / Selected state without a state name:"FocusedSelected""Focused""Selected" |

  
If no entry can be found for the specified state / combined states using the above approach, the `"_base"` attribute will be used.

---
## Object: SectionStackSection

### Description
Section descriptor used by a SectionStack to describe a section of items which are shown or hidden together along with their associated header.

A section header (see [SectionStack.sectionHeaderClass](classes/SectionStack.md#attr-sectionstacksectionheaderclass)) is created from this descriptor when the SectionStack is created. Any changes after creation must be made to the section header: [SectionStack.getSectionHeader](classes/SectionStack.md#method-sectionstackgetsectionheader).

Additional SectionHeader properties set on the SectionStackSection not explicitly documented, such as "iconAlign" or "prompt", are supported.

---
## Object: SeleniumCommand

### Description
A JavaScript object representing a Selenium command in a Selenese script.

### Groups

- experimental

### See Also

- [EventStream.transformSelenese](#method-eventstreamtransformselenese)
- [EventStream.getAsSeleneseHTML](classes/EventStream.md#method-eventstreamgetasselenesehtml)
- [EventStream.getAsSeleneseCommands](classes/EventStream.md#method-eventstreamgetasselenesecommands)

---
## Object: SerializationContext

### Description
Flags for XML serialization

---
## Object: SerializationSettings

### Description
Settings to control [EditContext](classes/EditContext.md#class-editcontext) serialization.

### Groups

- devTools

---
## Object: Shadow

### Description
A class used to define a shadow used in a Draw`<Shape>` Types.

---
## Object: SimpleGradient

### Description
Definition of a simple linear gradient defined by 2 colors and a [direction](#attr-simplegradientdirection).

---
## Object: StyleGroup

### Description
An ordinary JavaScript object with properties that define an editable group of [settings](#object-stylesetting) for use in [CSSEditor](classes/CSSEditor.md#class-csseditor)s.

---
## Object: StyleSetting

### Description
An ordinary JavaScript object with properties that configure a setting for use in a [CSS-editor](classes/CSSEditor.md#class-csseditor).

---
## Object: SummarizeRecordsPartialResult

### Description
The result for a batch of records in a record summarization operation.

---
## Object: SummarizeRecordsResult

### Description
The result of a record summarization operation.

---
## Object: SummarizeValueExample

### Description
An example to provide to AI.

---
## Object: SummarizeValueResult

### Description
The result of a value summarization operation.

---
## Object: SummaryConfiguration

### Description
Settings for use with [SimpleType.applySummaryFunction](classes/SimpleType.md#classmethod-simpletypeapplysummaryfunction).

---
## Object: SystemDoneConfig

### Description
Configuration object for [AutoTest.isSystemDone](classes/AutoTest.md#classmethod-autotestissystemdone).

Note that this format is extended by [SystemWaitConfig](#object-systemwaitconfig) and [ElementWaitConfig](#object-elementwaitconfig), used by [AutoTest.waitForSystemDone](classes/AutoTest.md#classmethod-autotestwaitforsystemdone) and [AutoTest.waitForElement](classes/AutoTest.md#classmethod-autotestwaitforelement).

Note also that [AutoTest.waitForSystemDone](classes/AutoTest.md#classmethod-autotestwaitforsystemdone) may have different default configuration from [AutoTest.isSystemDone](classes/AutoTest.md#classmethod-autotestissystemdone) - the default behavior for each option is documented on the appropriate config object type for the method.

---
## Object: SystemWaitConfig

### Description
Configuration object for [AutoTest.waitForSystemDone](classes/AutoTest.md#classmethod-autotestwaitforsystemdone)

---
## Object: Tab

### Description
Tabs are specified as objects, not class instances. For example, when developing in JavaScript, a typical initialization block for a TabSet would look like this:
```
 TabSet.create({
     tabs: [
         {title: "tab1", pane: "pane1"},
         {title: "tab2"}
     ]
 });
 
```
And in XML:
```
 <TabSet>
    <tabs>
        <Tab title="tab1" pane="pane1"/>
        <Tab title="tab2"/>
    </tabs>
 </TabSet>
 
```

---
## Object: TileRecord

### Description
A TileRecord is a JavaScript Object whose properties contain values for each TileField. A TileRecord may have additional properties which affect the record's appearance or behavior, or which hold data for use by custom logic or other, related components.

---
## Object: TreeGridField

### Description
An object literal with a particular set of properties used to configure the display of and interaction with the columns of a [TreeGrid](classes/TreeGrid.md#class-treegrid). [TreeGrid](classes/TreeGrid.md#class-treegrid) is a subclass of [ListGrid](classes/ListGrid_1.md#class-listgrid) and as a result, for all fields except the field containing the [Tree](classes/Tree.md#class-tree) itself (specified by [TreeGridField.treeField](classes/TreeGridField.md#attr-treegridfieldtreefield), all properties settable on [ListGridField](reference_2.md#object-listgridfield) apply to TreeGridField as well.

This class documents just those properties that are specific to TreeGridFields - see [ListGridField](reference_2.md#object-listgridfield) for the set of inherited properties.

### See Also

- [ListGridField](reference_2.md#object-listgridfield)
- [TreeGrid.fields](classes/TreeGrid.md#attr-treegridfields)
- [ListGrid.setFields](classes/ListGrid_2.md#method-listgridsetfields)

---
## Object: UserFormula

### Description
An object representing a user-created formula.

Note that the current implementation of formulas simply executes the [text](classes/UserFormula.md#attr-userformulatext) as a JavaScript string after making special variables and methods available to the formula. It is safe to allow users to define formulas for themselves (since an end user can always execute whatever JavaScript they want via the browser's built-in developer tools), and is safe to allow formulas to be shared between trusted users. However it would not be safe to allow an untrusted user to create formulas that are shared to other users.

Also, while the current implementation would allow creation of a formula that calls JavaScript functions which are not part of the standard or custom [MathFunctions](classes/MathFunction.md#class-mathfunction), this behavior should not be relied upon, as future versions of the formula engine may prohibit such calls.

[ListGrid](classes/ListGrid_1.md#class-listgrid)s additionally allow the formula to be user-modifiable, with the formula created and edited with a [FormulaBuilder](classes/FormulaBuilder.md#class-formulabuilder), either directly or via the [ListGrid.canAddFormulaFields](classes/ListGrid_1.md#attr-listgridcanaddformulafields) behavior.

### Groups

- fieldGeneration

---
## Object: UserSummary

### Description
An object representing a user-created summary.

[ListGrid](classes/ListGrid_1.md#class-listgrid)s additionally allow the summary to be user-modifiable, with the summary created and edited with a [SummaryBuilder](classes/SummaryBuilder.md#class-summarybuilder), either directly or via the [ListGrid.canAddSummaryFields](classes/ListGrid_1.md#attr-listgridcanaddsummaryfields) behavior.

### Groups

- fieldGeneration

---
## Interface: DataBoundComponent

### Description
A DataBoundComponent is a widget that can configure itself for viewing or editing objects which share a certain schema by "binding" to the schema for that object (called a "DataSource").

A schema (or DataSource) describes an object as consisting of a set of properties (or "fields").

DataBoundComponents have a [common set of APIs](classes/DataBoundComponent.md#attr-databoundcomponentdatasource) for dealing with binding to DataSources, [overriding or augmenting](classes/DataBoundComponent.md#attr-databoundcomponentfields) the schema information provided by a DataSource, and manipulating objects or sets of object from the DataSource.

The following visual components currently support databinding:

- [DynamicForm](classes/DynamicForm.md#class-dynamicform)
- [DetailViewer](classes/DetailViewer.md#class-detailviewer)
- [ListGrid](classes/ListGrid_1.md#class-listgrid)
- [TreeGrid](classes/TreeGrid.md#class-treegrid)
- [TileGrid](classes/TileGrid.md#class-tilegrid)
- [ColumnTree](classes/ColumnTree.md#class-columntree)
- [CubeGrid](classes/CubeGrid.md#class-cubegrid)
The following non-visual components also support databinding:
- [ValuesManager](classes/ValuesManager.md#class-valuesmanager)
- [ResultSet](classes/ResultSet.md#class-resultset)
- [ResultTree](classes/ResultTree.md#class-resulttree)

---
## Interface: Palette

### Description
An interface that provides the ability to create components from a [PaletteNode](#object-palettenode).

### Groups

- devTools

---
