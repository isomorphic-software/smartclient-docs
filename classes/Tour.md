# Tour Documentation

[← Back to API Index](../reference.md)

---

## Class: Tour

*Inherits from:* [Process](Process.md#class-process)

### Description
The Tour class allows you to build tours and tutorials for end users, highlighting specific components on the page and prompting for specific user-interactions.

Tours are a specific type of [Workflow Process](Process.md#class-process) and consist of a series of [TourSteps](TourStep.md#class-tourstep). Typically each step refers to an element on the page, which is either being highlighted for the user, or, for a tutorial, is an element that the user is being prompted to interact with (see TourStep.clickTarget, for example).

Most steps have a TourWindow, which shows explanatory or instructional text. For tutorial steps that request a user action, the target can be highlighted and a large arrow is shown pointing at the target.

The placement of the TourWindow and arrow is automatic, and intelligently takes into account the type of interaction requested. For example, if a tutorial requires a user to change a value in a SelectItem, the TourWindow and arrow will avoid appearing underneath the select, where they could be occluded by the drop-down picklist. Similarly, for a drag and drop interaction, the TourWindow avoids overlapping both the drag source and the drop area.

Because of all this automatic behavior, a tutorial step typically consists of just:

1\. explanatory text (tourStep.title and tourStep.description)  
2\. the target  
3\. the expected interaction (eg click the target, or type something in, or drag something to another widget)  
4\. validation of input (what was typed or chosen), if applicable

Developers may use [AutoTest locators](AutoTest.md#classmethod-autotestgetlocator) to specify specific components or elements as action targets. Using locators means that tours and tutorials will typically still work even if your application changes (for example, new controls are added). Note that we recommend making use of the [locator shortcut](AutoTest.md#classmethod-autotestinstalllocatorshortcut) to rapidly generate locators.

A tour is typically written as a `.proc.xml` document stored in the folder configured via the `project.processes` setting in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) (webroot/processes by default). They may be loaded via the [Tour.loadTour](#classmethod-tourloadtour) method.

**The Tour feature is available with Power or better licenses only** See [smartclient.com/product](http://smartclient.com/product) for details.  
It requires the standard DataBinding and [optional](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) `Tour` module.

---
## Attr: Tour.tourStepWizardAutoCompleteTitle

### Description
Title for the _Auto Complete_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardRecordStepHeaderPrompt

### Description
Prompt for the _Record Step_ window header in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardShowProgressTitle

### Description
Title for the _Show Progress_ picker in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourCompleteTitle

### Description
Title for the _Tour Complete_ dialog displayed after recording a Tour.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.stepActionButtonTitle

### Description
Default value for [TourStep.actionButtonTitle](TourStep.md#attr-tourstepactionbuttontitle) for steps other than the first and last ones.

Default titles for the first and last steps are configured by [firstStepActionButtonTitle](#attr-tourfirststepactionbuttontitle) and [lastStepActionButtonTitle](#attr-tourlaststepactionbuttontitle) respectively.

### Groups

- i18nMessages

### See Also

- [Tour.stepCancelButtonTitle](#attr-tourstepcancelbuttontitle)

**Flags**: IR

---
## Attr: Tour.windowDefaults

### Description
Defaults for each [TourStep.targetView](TourStep.md#attr-toursteptargetview) autoChild in the tour. These defaults are applied before [TourStep.windowDefaults](TourStep.md#attr-tourstepwindowdefaults) if any.

**Flags**: IR

---
## Attr: Tour.canCancel

### Description
Set to `false` to prevent tour steps from allowing the user to cancel the tour. By default the cancel button will still be shown but is disabled. Set [Tour.showCancelButton](#attr-tourshowcancelbutton) to false to suppress the cancel button entirely.

Any time the cancel button is visible, its hover can be customized via [Tour.stepCancelButtonPrompt](#attr-tourstepcancelbuttonprompt). For `canCancel:false` tours where the cancel button is not hidden, a custom prompt may be useful to provide an explanation to the user as the tour can't be canceled.

**Flags**: IR

---
## Attr: Tour.tourStepWizardNextStepButtonTitle

### Description
Title for the _Next Step_ button in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardTourTypeTitle

### Description
Title for the Tour Type picker in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardInstructionsTitle

### Description
Title for the _Instructions_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardAutoCompletePrompt

### Description
Prompt for the _Auto Complete_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.dropOutlineBorder

### Description
Set the CSS border of the outline for drop targets as a CSS string including border-width, border-style, and/or color (eg "1px dashed blue"). See [Tour.outlineBorder](#attr-touroutlineborder) for properties applied to non-drop targets.

This property applies the same border to all four sides of the outlined component(s).

### See Also

- [Tour.outlineBorder](#attr-touroutlineborder)

**Flags**: IRW

---
## Attr: Tour.autoReset

### Description
Should tour be auto-reset once it finishes in any manner so it can restarted?

**Flags**: IR

---
## Attr: Tour.tourStepWizardDropTargetTitle

### Description
Title for the _Drop Target_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourCompleteMakeChangesButtonTitle

### Description
Title for the _Make Changes..._ button in the TourComplete dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.notifyMessageSettings

### Description
Defaults settings for [notifyType](../reference_2.md#type-notifytype) message displayed by [notifyValidationMessage](#method-tournotifyvalidationmessage).

**Flags**: IR

---
## Attr: Tour.outlineBorder

### Description
Set the CSS border of the outline of non-drop targets as a CSS string including border-width, border-style, and/or color (eg "1px dashed blue"). See [Tour.dropOutlineBorder](#attr-tourdropoutlineborder) for properties applied to drop targets.

This property applies the same border to all four sides of the outlined component(s).

### See Also

- [Tour.dropOutlineBorder](#attr-tourdropoutlineborder)

**Flags**: IRW

---
## Attr: Tour.tourStepWizardTargePrompt

### Description
Prompt for the _Target_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.firstStepActionButtonTitle

### Description
Default value of [TourStep.actionButtonTitle](TourStep.md#attr-tourstepactionbuttontitle) for the first step in the tour.

Default titles for the middle and last steps are configured by [stepActionButtonTitle](#attr-tourstepactionbuttontitle) and [lastStepActionButtonTitle](#attr-tourlaststepactionbuttontitle) respectively.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardTargeNotifyText

### Description
Descriptive text displayed in a popup [notification window](Notify.md#class-notify) when a Target is selected for this TourStep.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardBindOutputTitle

### Description
Title for the _Bind Output_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardRecordStepTitle

### Description
Title for the _Record Tour Step_ window in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardDropTargetPrompt

### Description
Prompt for the _Drop Target_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.showProgress

### Description
Should a progress bar be shown in each step to indicate progress through the tour?

**Flags**: IR

---
## Attr: Tour.tourStepWizardTargetTitle

### Description
Title for the _Target_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardReifyTourTitle

### Description
Title for the _Reify Tutorial_ option in the Tour Type picker in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardExpectedValueHint

### Description
Hint for the _Expected Value_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardInteractiveTourTitle

### Description
Title for the _interactive Tutorial_ option in the Tour Type picker in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardDropTargetNotifyText

### Description
Descriptive text displayed in a popup [notification window](Notify.md#class-notify) when a _Drop Target_ is selected for this TourStep.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardCaseSensitiveTitle

### Description
Title for the _Case Sensitive_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardExpectedValueTitle

### Description
Title for the _Expected Value_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.lastStepActionButtonTitle

### Description
Default value of [TourStep.actionButtonTitle](TourStep.md#attr-tourstepactionbuttontitle) for the last step in the tour.

Default titles for the first and middle steps are configured by [firstStepActionButtonTitle](#attr-tourfirststepactionbuttontitle) and [stepActionButtonTitle](#attr-tourstepactionbuttontitle) respectively.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.showProgressPercent

### Description
Show progress percent next to progress bar when [Tour.showProgress](#attr-tourshowprogress) is enabled?

**Flags**: IR

---
## Attr: Tour.allowDropOnDescendants

### Description
Default value for [TourStep.allowDropOnDescendants](TourStep.md#attr-tourstepallowdropondescendants) within this tour.

**Flags**: IRW

---
## Attr: Tour.tourCompleteViewXMLButtonTitle

### Description
Title for the _View XML_ button in the TourComplete dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardTitle

### Description
Title for the _TourStep Title_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourCompleteRunTourButtonTitle

### Description
Title for the _View XML_ button in the TourComplete dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardTitle

### Description
Title for the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.showCancelButton

### Description
This property allows you to override the [TourWindow.showCancelButton](TourWindow.md#attr-tourwindowshowcancelbutton) to hide the cancel button for all steps of the tour.

See also [Tour.canCancel](#attr-tourcancancel)

**Flags**: IR

---
## Attr: Tour.tourWizardRequiredDataSourcesTitle

### Description
Title for the _Required DataSources_ item in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.notifyType

### Description
Category of message to use in +{notifyValidationMessage,notifyValidationMessage} by default.

If this category has not been configured in [Notify](Notify.md#class-notify) it will be automatically configured using +{notifyMessageSettings,notifyMessageSettings}.

**Flags**: IR

---
## Attr: Tour.cancelSteps

### Description
The [ProcessElement](ProcessElement.md#class-processelement)s representing steps that should be performed if the user cancels the tour. These steps are typically [TourStep](TourStep.md#class-tourstep)s.

Alternately, or in addition to these cancelation steps, the [finished](Process.md#method-processfinished) method will be called once there are no more steps to process in the tour.

**Flags**: IR

---
## Attr: Tour.tourStepWizardBindOutputHint

### Description
Hint for the _Bind Output_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.firstStepCancelButtonTitle

### Description
Default value of [TourStep.cancelButtonTitle](TourStep.md#attr-tourstepcancelbuttontitle) for the first step in the tour.

Default title for the middle steps is configured by [stepCancelButtonTitle](#attr-tourstepcancelbuttontitle). No cancel button is shown for the last step.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardRequiredDataSourcesHint

### Description
Hint text for the _Required DataSources_ item in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardRecordButtonTitle

### Description
Title for the _Record Tour_ button in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.stepCancelButtonTitle

### Description
Default value for [TourStep.cancelButtonTitle](TourStep.md#attr-tourstepcancelbuttontitle) for all steps where the cancel button is shown.

Default title for the first step is configured by [firstStepCancelButtonTitle](#attr-tourfirststepcancelbuttontitle).

### Groups

- i18nMessages

### See Also

- [Tour.stepActionButtonTitle](#attr-tourstepactionbuttontitle)

**Flags**: IR

---
## Attr: Tour.tourWizardUITourTitle

### Description
Title for the _non-interactive UI Tour_ option in the Tour Type picker in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourWizardNewScreenPickerTitle

### Description
Title for the _Start with New Screen_ picker in the Tour Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardDropTargetHint

### Description
Hint for the _Drop Target_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.steps

### Description
The [ProcessElement](ProcessElement.md#class-processelement)s representing steps in this tour. These steps are typically [TourStep](TourStep.md#class-tourstep)s.

**Flags**: IR

---
## Attr: Tour.tourStepWizardDoneButtonTitle

### Description
Title for the _Done_ button in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourStepWizardNoStepsMessage

### Description
Empty message for the grid in the _Tour Wizard_ when no steps are present.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.tourCompleteTourIdTitle

### Description
Title for the _Tour ID_ field in the TourComplete dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.showInputValidationMessage

### Description
Should [TourStep.inputValidationNotifyMessage](TourStep.md#attr-tourstepinputvalidationnotifymessage) be shown as detailed in [TourInputValidationMode](../reference.md#type-tourinputvalidationmode) for the entire tour? Set to `false` to suppress reporting messages to the user. [notifyValidationMessage](#method-tournotifyvalidationmessage) will not be called.

This setting can be overridden for individual [tourSteps](TourStep.md#class-tourstep).

**Flags**: IR

---
## Attr: Tour.stepCancelButtonPrompt

### Description
Prompt displayed in hover for cancel button.

**Flags**: IR

---
## Attr: Tour.tourStepWizardActionTypeTitle

### Description
Title for the _Action Type_ field in the TourStep Wizard.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Tour.mode

### Description
The tour mode allows step configuration to be simplified by using the context to apply appropriate defaults.

**Flags**: IRW

---
## ClassMethod: Tour.getTour

### Description
Get a Tour instance by it's ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tourId | [Identifier](../reference.md#type-identifier) | false | — | tour ID to retrieve |

### Returns

`[Tour](#type-tour)` — the tour, or null if not defined

---
## ClassMethod: Tour.loadTour

### Description
Loads an XML tour definition stored in XML from the server.

Tour files are stored as .proc.xml files in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) format, in the directory indicated by the `project.processes` setting in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) (`_webroot_/processes` by default). To load a tour saved in a file _tourId_.proc.xml, pass just _tourId_ to this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tourId | [Identifier](../reference.md#type-identifier)|[Array of Identifier](#type-array-of-identifier) | false | — | tour ID or IDs to load |
| callback | [ProcessCallback](#type-processcallback) | false | — | called when the tour is loaded with argument "process", the first tour. Other tours can be looked up via [Tour.getTour](#classmethod-tourgettour). |

---
## Method: Tour.notifyValidationMessage

### Description
Notify user of expected value entry validation message. Default implementation uses the [Notify system](Notify.md#class-notify) to show the message in it's default position. See [notifyType](../reference_2.md#type-notifytype) for notification configuration details.

Override this method to display message by a different means.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message provided by [TourStep.inputValidationNotifyMessage](TourStep.md#attr-tourstepinputvalidationnotifymessage) |

---
