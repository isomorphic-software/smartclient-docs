# TourConfirmStep Documentation

[← Back to API Index](../main.md)

---

## Class: TourConfirmStep

*Inherits from:* [UserTask](UserTask.md#class-usertask)

### Description
Chooses one or another next process element based on confirmation of a message shown to user.

If the user clicks OK, the [nextElement](#attr-tourconfirmstepnextelement) is chosen, otherwise the choice is [failureElement](#attr-tourconfirmstepfailureelement).

---
## Attr: TourConfirmStep.targetViewDefaults

### Description
Defaults for the [TourConfirmStep.targetView](#attr-tourconfirmsteptargetview) autoChild.

**Flags**: IR

---
## Attr: TourConfirmStep.instructions

### Description
Text to show in body of window.

### Groups

- appearance
- i18nMessages

**Flags**: IR

---
## Attr: TourConfirmStep.title

### Description
Title for the Window.

### Groups

- appearance
- i18nMessages

**Flags**: IR

---
## Attr: TourConfirmStep.targetView

### Description
Automatically generated view (typically a window) to show for tour step.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [showCancelButton](#attr-tourconfirmstepshowcancelbutton) for the [TourWindow.showCancelButton](TourWindow.md#attr-tourwindowshowcancelbutton)
*   [cancelButtonTitle](#attr-tourconfirmstepcancelbuttontitle) for the [TourWindow.cancelButtonTitle](TourWindow.md#attr-tourwindowcancelbuttontitle)
*   [actionButtonTitle](#attr-tourconfirmstepactionbuttontitle) for the [TourWindow.actionButtonTitle](TourWindow.md#attr-tourwindowactionbuttontitle)

**Flags**: R

---
## Attr: TourConfirmStep.failureElement

### Description
ID of the next element to process if the user clicks the `cancelButton`. If not set, the process will exit.

**Flags**: IR

---
## Attr: TourConfirmStep.targetViewConstructor

### Description
The name of the widget class (as a string) to use for the target view.

**Flags**: IR

---
## Attr: TourConfirmStep.nextElement

### Description
Next [element](ProcessElement.md#class-processelement) to execute if the user clicks the `actionButton`.

`nextElement` does not need to be specified if this gateway is part of a [sequence](Process.md#attr-processsequences) and has a next element in the sequence. This is normal for a tour.

**Flags**: IR

---
## Attr: TourConfirmStep.showCancelButton

### Description
Should the [TourConfirmStep.targetView](#attr-tourconfirmsteptargetview) [cancel button](TourWindow.md#attr-tourwindowshowcancelbutton) be shown for this step?

If no value is provided it will be defaulted to `true`.

**Flags**: IR

---
## Attr: TourConfirmStep.actionButtonTitle

### Description
Applied directly to [TourConfirmStep.targetView](#attr-tourconfirmsteptargetview).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: TourConfirmStep.cancelButtonTitle

### Description
Applied directly to [TourConfirmStep.targetView](#attr-tourconfirmsteptargetview).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: TourConfirmStep.showActionButton

### Description
Should the [TourConfirmStep.targetView](#attr-tourconfirmsteptargetview) [action button](TourWindow.md#attr-tourwindowshowactionbutton) be shown for this step?

If no value is provided it will be defaulted to `true`.

**Flags**: IR

---
