# TourStep Documentation

[← Back to API Index](../reference.md)

---

## Class: TourStep

*Inherits from:* [UserTask](UserTask.md#class-usertask)

### Description
User task configuration for a step within a [Tour](Tour.md#class-tour). As each step is executed, it will show a [TourWindow](TourWindow.md#class-tourwindow) to the user (the automatically generated [TourStep.targetView](#attr-toursteptargetview)).

At a minimum tourSteps will typically have a [title](#attr-toursteptitle) and/or [description](ProcessElement.md#attr-processelementdescription). Without a [target](#attr-toursteptarget) the window will be shown in the center of the screen.

To relate the step to a component provide a [target](#attr-toursteptarget) value. An [actionType](#attr-tourstepactiontype) value determines what action, if any, is expected with the `target`. Some `actionTypes` like "none" and "any" just highlight the target for review and the user must click the next button to complete the step. Others like "click" or "change" expect the user to interact with the target component in a certain way. Many of these will advance to the next step when the required action is completed. See [action types](../reference.md#type-touractiontype) for details.

In most cases the `actionType` can be left unset because a default is applied based on the other step properties and the [Tour.mode](Tour.md#attr-tourmode). However, actions like `doubleClick`, `rightClick` and `mouseOver` must be provided.

To explicitly suppress automatic completion of a step on user interaction, devlopers may set [autoComplete](#attr-tourstepautocomplete) to false.

---
## Attr: TourStep.pointerSnapTo

### Description
Applied directly to [TourStep.targetView](#attr-toursteptargetview) [pointerSettings](Canvas.md#attr-canvaspointersettings).

### Groups

- snapPositioning

**Flags**: IR

---
## Attr: TourStep.bindEnteredText

### Description
When set on a step with an [actionType](#attr-tourstepactiontype) of "change", the entered or selected value will be automatically bound to the specified value in the [tour state](Process.md#attr-processstate).

**Flags**: IR

---
## Attr: TourStep.afterInputTarget

### Description
Target component which must clicked to process [TourStep.expectedValue](#attr-tourstepexpectedvalue) entered into [target](#attr-toursteptarget) with [actionType](#attr-tourstepactiontype) of "change".

This is commonly used for a dialog where the must select a value and then click a submit button.

Target may be specified as a [GlobalId](../reference.md#type-globalid) for a Component or FormItem, or as a [AutoTestLocator](../reference_2.md#type-autotestlocator) for an element.

**Flags**: IR

---
## Attr: TourStep.allowDropOnDescendants

### Description
For [actionType:"drag"](#attr-tourstepactiontype) tourSteps with a [TourStep.dropTarget](#attr-tourstepdroptarget), should we allow the drop to complete and the tour to proceed if the user drops on a descendant of the drop target.

For example - if a user has been prompted to drag a component into a Layout, but the layout already contains a nested child layout, should the user be able to drop into that child layout and continue the tour?

If unset this will be derived from [Tour.allowDropOnDescendants](Tour.md#attr-tourallowdropondescendants)

**Flags**: IR

---
## Attr: TourStep.showInputValidationMessage

### Description
Should [inputValidationNotifyMessage](#attr-tourstepinputvalidationnotifymessage) be shown as detailed in [TourInputValidationMode](../reference.md#type-tourinputvalidationmode)? Defaults from [Tour.showInputValidationMessage](Tour.md#attr-tourshowinputvalidationmessage) if not set.

If set to `false` reporting messages to the user are suppressed and therefore [Tour.notifyValidationMessage](Tour.md#method-tournotifyvalidationmessage) will not be called.

**Flags**: IR

---
## Attr: TourStep.title

### Description
Title for the Window.

### Groups

- appearance
- i18nMessages

**Flags**: IR

---
## Attr: TourStep.expectedValueCaseSensitive

### Description
Should the [expectedValue](#attr-tourstepexpectedvalue) be matched as case-sensitive?

**Flags**: IR

---
## Attr: TourStep.targetView

### Description
Automatically generated view (typically a TourWindow) to show for tour step.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pointerSnapTo](#attr-toursteppointersnapto) for the [Canvas.pointerSettings](Canvas.md#attr-canvaspointersettings)
*   [showCancelButton](#attr-tourstepshowcancelbutton) for the [TourWindow.showCancelButton](TourWindow.md#attr-tourwindowshowcancelbutton)
*   [cancelButtonTitle](#attr-tourstepcancelbuttontitle) for the [TourWindow.cancelButtonTitle](TourWindow.md#attr-tourwindowcancelbuttontitle)
*   [actionButtonTitle](#attr-tourstepactionbuttontitle) for the [TourWindow.actionButtonTitle](TourWindow.md#attr-tourwindowactionbuttontitle)

**Flags**: R

---
## Attr: TourStep.target

### Description
Component that is the target of this step. The interaction for this step is indicated in [actionType](#attr-tourstepactiontype). For actions that need multiple targets, this target is the primary one.

Target may be specified as a [GlobalId](../reference.md#type-globalid) for a Component or FormItem, or as a [AutoTestLocator](../reference_2.md#type-autotestlocator) for an element.

**Flags**: IR

---
## Attr: TourStep.actionButtonTitle

### Description
Applied directly to [TourStep.targetView](#attr-toursteptargetview). Defaults from [Tour.stepActionButtonTitle](Tour.md#attr-tourstepactionbuttontitle).

**Flags**: IR

---
## Attr: TourStep.showActionButton

### Description
Should the [TourStep.targetView](#attr-toursteptargetview) [action button](TourWindow.md#attr-tourwindowshowactionbutton) be shown for this step?

If no value is provided it will be defaulted to `true` when [autoComplete](../reference.md#type-autocomplete) is `not false` and any of the following are true:

*   [actionType](#attr-tourstepactiontype) is "click"
*   actionType is "mouseDown"
*   actionType is "doubleClick"
*   actionType is "rightClick"
*   actionType is "menuItemOpen"
*   actionType is "menuItemSelect"
*   actionType is "change" and an [expectedValue](#attr-tourstepexpectedvalue) is provided
*   a [dropTarget](#attr-tourstepdroptarget) is provided

If no value is provided and autoComplete is `false` but auto completion would normally occur (i.e. actionType "click", "change" with expectedValue, etc.) then the action button is shown but is disabled until the expected action is completed at which time the button is enabled so the user can continue.

**Flags**: IR

---
## Attr: TourStep.instructions

### Description
Text to show in body of window.

### Groups

- appearance
- i18nMessages

**Flags**: IR

---
## Attr: TourStep.showOutline

### Description
Should the target(s) be outlined? Defaults to `true` in [Tour.mode](Tour.md#attr-tourmode):"tutorial".

### See Also

- [TourStep.showPointer](#attr-tourstepshowpointer)
- [TourStep.showArrow](#attr-tourstepshowarrow)

**Flags**: IR

---
## Attr: TourStep.autoComplete

### Description
If this step has a target that prompts a user for a specific action, should the step be automatically completed and have the tour move forward to the next step when the user takes this action?

Has no effect except on [action types](../reference.md#type-touractiontype) that can auto-complete.

If autoComplete is `false` the action button is shown but is disabled until the expected action is completed at which time the button is enabled so the user can continue.

**Flags**: IR

---
## Attr: TourStep.actionType

### Description
Indicates the type of action that is expected with the [target component](#attr-toursteptarget).

If not specified a default type is determined by the [Tour.mode](Tour.md#attr-tourmode) setting, the target and other tourStep properties.

**Details:**

when `tourMode` is "tour"

*   then actionType = "none"

when `tourMode` is "tutorial"

*   and `expectedValue` or `afterInputTarget` are set
    *   then actionType = "change"
*   and `dropTarget` is set
    *   then actionType = "drag"
*   otherwise
    *   actionType = "click"

**Flags**: IR

---
## Attr: TourStep.showArrow

### Description
For a step with an [action](#attr-tourstepactiontype) a large arrow shows to indicate the target or direction of required action. Setting `showArrow` to `false` suppresses the display of the arrow. Note that the tour window is shown as if the arrow were there.

[ShowPointer](#attr-tourstepshowpointer) takes precedence over `showArrow:true`.

### See Also

- [TourStep.showPointer](#attr-tourstepshowpointer)
- [TourStep.showOutline](#attr-tourstepshowoutline)

**Flags**: IR

---
## Attr: TourStep.windowDefaults

### Description
Defaults for the [TourStep.targetView](#attr-toursteptargetview) autoChild. These defaults are applied after [Tour.windowDefaults](Tour.md#attr-tourwindowdefaults) if any.

**Flags**: IR

---
## Attr: TourStep.dropTarget

### Description
Target component on which a [target](#attr-toursteptarget) must be dropped to complete step. If [actionType](#attr-tourstepactiontype) is not specified and this property is provided, `actionType` defaults to "drag".

Target may be specified as a [GlobalId](../reference.md#type-globalid) for a Component or FormItem, or as a [AutoTestLocator](../reference_2.md#type-autotestlocator) for an element.

**Flags**: IR

---
## Attr: TourStep.inputValidationNotifyDelay

### Description
The time between keypresses that is used during [TourStep.inputValidation](#attr-tourstepinputvalidation) before showing the expected text notification. Does not apply to `inputValidation="onExit"`.

**Flags**: IR

---
## Attr: TourStep.cancelButtonTitle

### Description
Applied directly to [TourStep.targetView](#attr-toursteptargetview). Defaults from [Tour.stepCancelButtonTitle](Tour.md#attr-tourstepcancelbuttontitle).

**Flags**: IR

---
## Attr: TourStep.expectedValue

### Description
The expected value for [actionType](#attr-tourstepactiontype):"change". The value must be matched exactly ignoring case for string values. A string value can also be matched case-sensitive by setting [expectedValueCaseSensitive](#attr-tourstepexpectedvaluecasesensitive) to `true`.

A regular expression can be used to match the entered value by providing the expected value as a string with leading and trailing slashes (ex. "/get.\*/").

### See Also

- [TourStep.inputValidation](#attr-tourstepinputvalidation)

**Flags**: IR

---
## Attr: TourStep.showPointer

### Description
Should a [canvas pointer](Canvas.md#attr-canvasshowpointer) be shown pointing to the target? Defaults to `true` in [Tour.mode](Tour.md#attr-tourmode):"tour".

### See Also

- [TourStep.showOutline](#attr-tourstepshowoutline)
- [TourStep.showArrow](#attr-tourstepshowarrow)

**Flags**: IR

---
## Attr: TourStep.targetViewConstructor

### Description
The name of the widget class (as a string) to use for the target view.

**Flags**: IR

---
## Attr: TourStep.targetViewDefaults

### Description
Defaults for the [TourStep.targetView](#attr-toursteptargetview) autoChild.

**Flags**: IR

---
## Attr: TourStep.inputValidation

### Description
How should the [TourStep.expectedValue](#attr-tourstepexpectedvalue) be validated and notified to the user?

Defaults to "onExit" if [TourStep.afterInputTarget](#attr-tourstepafterinputtarget) is specified. Otherwise the default is "notify".

**Flags**: IR

---
## Attr: TourStep.showCancelButton

### Description
Should the [TourStep.targetView](#attr-toursteptargetview) [cancel button](TourWindow.md#attr-tourwindowshowcancelbutton) be shown for this step?

If no value is provided it will be defaulted to `true` unless this step is the last step in the tour.

**Flags**: IR

---
## Attr: TourStep.inputValidationNotifyMessage

### Description
Message to be displayed by [Tour.notifyValidationMessage](Tour.md#method-tournotifyvalidationmessage).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only two dynamic variables, value and expectedValue, are available and represent the currently entered and expected values.

### Groups

- i18nMessages

**Flags**: IR

---
