# Dialog Documentation

[← Back to API Index](../main.md)

---

## Class: Dialog

*Inherits from:* [Window](Window.md#class-window)

### Description
Dialogs are a specialized version of [Window](Window.md#class-window) used for small windows that contain just a text message or a text mesage with some standard buttons.

Many typical modal dialogs such as alerts and confirmations are built into the system with convenience APIs - see [isc.say](isc.md#staticmethod-iscsay), [isc.warn](isc.md#staticmethod-iscwarn) and [isc.askForValue](isc.md#staticmethod-iscaskforvalue) .

Dialogs can be modal or non-modal according to [isModal](Window.md#attr-windowismodal).

NOTE: If you are building a dialog that will involve more than just buttons and a message, consider starting from the [Window](Window.md#class-window) class instead, where arbitrary components can be added to the body area via [Window.addItem](Window.md#method-windowadditem).

This is an example of creating a custom dialog:

```
  isc.Dialog.create({
      message : "Please choose whether to proceed",
      icon:"[SKIN]ask.png",
      buttons : [
          isc.Button.create({ title:"OK" }),
          isc.Button.create({ title:"Cancel" })
      ],
      buttonClick : function (button, index) {
          this.hide();
      }
  });
 
```

---
## ClassAttr: Dialog.ASK_TITLE

### Description
Default title for the dialog displayed in response to the [isc.ask](isc.md#staticmethod-iscask) method. Note that a custom title can be specified as the `title` attribute of the `properties` parameter passed to that method.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: Dialog.Ask

### Description
A singleton Dialog instance that will be shown in response to a [isc.askForValue](isc.md#staticmethod-iscaskforvalue) call. Notes:  
Because this is a singleton object, properties set on the Ask object directly will persist each time it is shown.  
Developers should use the `askForValue()` method to show this object rather than manipulating the Dialog directly.

### Groups

- Prompting

### See Also

- [isc.askForValue](isc.md#staticmethod-iscaskforvalue)

**Flags**: A

---
## ClassAttr: Dialog.YES_BUTTON_TITLE

### Description
Title for the `"Yes"` button.

### Groups

- i18nMessages

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

**Flags**: IRW

---
## ClassAttr: Dialog.DONE_BUTTON_TITLE

### Description
Title for the `"Done"` button.

### Groups

- i18nMessages

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

**Flags**: IRW

---
## ClassAttr: Dialog.NO_BUTTON_TITLE

### Description
Title for the `"No"` button.

### Groups

- i18nMessages

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

**Flags**: IRW

---
## ClassAttr: Dialog.ASK_FOR_VALUE_TITLE

### Description
Default title for the dialog displayed by [isc.askForValue](isc.md#staticmethod-iscaskforvalue). A custom title can alternatively be specified as the `title` attribute of the `properties` parameter passed to that method.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: Dialog.Warn

### Description
A singleton Dialog instance that will show text to the user and provide buttons for their response. The Dialog will expand to show all the text that you put into it. This dialog is shown in response to calls to [isc.say](isc.md#staticmethod-iscsay), [isc.warn](isc.md#staticmethod-iscwarn), [isc.ask](isc.md#staticmethod-iscask) and [isc.confirm](isc.md#staticmethod-iscconfirm).

This can be used in cases where a developer would alternatively make use of the native JavaScript `alert()` and `confirm()` methods. The main differences between those methods and using the Warn object are:  
\- The Warn object can be customized by modifying which buttons are visible, the style applied to it, etc.  
\- The `isc.ask()` and `isc.warn()` methods are asynchronous - rather than returning a value indicating the user's response, a callback method will be fired when the user interacts with the dialog.  
  
Notes:  
Because this is a singleton object, properties set on the Warn object directly will persist each time it is shown.  
Developers should use the `warn()` or `ask()` methods to show and hide this object rather than manipulating the Dialog directly.

### Groups

- Prompting

### See Also

- [isc.warn](isc.md#staticmethod-iscwarn)
- [isc.ask](isc.md#staticmethod-iscask)

**Flags**: A

---
## ClassAttr: Dialog.APPLY_BUTTON_TITLE

### Description
Title for the `"Apply"` button.

### Groups

- i18nMessages

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

**Flags**: IRW

---
## ClassAttr: Dialog.CONFIRM_TITLE

### Description
Default title for the dialog displayed in response to the [isc.confirm](isc.md#staticmethod-iscconfirm) method. Note that a custom title can be specified as the `title` attribute of the `properties` parameter passed to that method.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: Dialog.SAY_TITLE

### Description
Default title for the dialog displayed in response to the [isc.say](isc.md#staticmethod-iscsay) method. Note that a custom title can be specified as the `title` attribute of the `properties` parameter passed to that method.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: Dialog.WARN_TITLE

### Description
Default title for the dialog displayed in response to the [isc.warn](isc.md#staticmethod-iscwarn) method. Note that a custom title can be specified as the `title` attribute of the `properties` parameter passed to that method.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: Dialog.OK_BUTTON_TITLE

### Description
Title for the `"OK"` button.

### Groups

- i18nMessages

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

**Flags**: IRW

---
## ClassAttr: Dialog.CANCEL_BUTTON_TITLE

### Description
Title for the `"Cancel"` button.

### Groups

- i18nMessages

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

**Flags**: IRW

---
## ClassAttr: Dialog.Prompt

### Description
The "Prompt" object on the dialog class is a singleton Dialog instance. The Prompt is used to show text to the user in a modal fashion - it will expand to show all the text that you put into it. By default this Dialog has no end-user controls and is expected to be programmatically dismissed.  
Common use-case: During server-interactions, the Prompt will be used to display a suitable wait message, and suppress user input.  
  
Notes:  
Because this is a singleton object, properties set on the Prompt directly will persist each time it is shown.  
Developers should use the `showPrompt()` and `clearPrompt()` methods to show and hide the prompt rather than manipulating the prompt directly.

### Groups

- Prompting

### See Also

- [isc.showPrompt](isc.md#staticmethod-iscshowprompt)
- [isc.clearPrompt](isc.md#staticmethod-iscclearprompt)

**Flags**: A

---
## Attr: Dialog.styleName

### Description
Style of the Dialog background

### Groups

- appearance

**Flags**: IRW

---
## Attr: Dialog.messageStyle

### Description
Style to apply to the message text shown in the center of the dialog

**Flags**: IR

---
## Attr: Dialog.defaultWidth

### Description
—

### Groups

- appearance

**Flags**: IR

---
## Attr: Dialog.message

### Description
Message to show in this dialog.

If a message is set the primary purpose of the dialog will be assumed to be to show a message with buttons - auto-sizing to the message text will be enabled, and, if [Dialog.icon](#attr-dialogicon) has also been set, the [messageLabel](#attr-dialogmessagelabel) and [messageIcon](#attr-dialogmessageicon) AutoChildren will be created and placed together in the [messageStack](#attr-dialogmessagestack) AutoChild, with the toolbar underneath as usual. If any of these behaviors are inconvenient or you want more precise control over a message and some custom widgets, start from the superclass [Window](Window.md#class-window) instead, and add controls via [Window.addItem](Window.md#method-windowadditem).

The message string may contain "${loadingImage}", if so, the standard loading spinner will appear at that location in the text (see [Canvas.loadingImageSrc](Canvas.md#classattr-canvasloadingimagesrc)).

The message will be styled with the [Dialog.messageStyle](#attr-dialogmessagestyle).

**Flags**: IRW

---
## Attr: Dialog.autoFocus

### Description
If a toolbar is showing, automatically place keyboard focus in the first button.

An alternative button can be specified by [autoFocusButton](#attr-dialogautofocusbutton).

### Groups

- appearance
- toolbar

**Flags**: IR

---
## Attr: Dialog.iconSize

### Description
Size of the icon to show in this dialog.

**Flags**: IR

---
## Attr: Dialog.messageStack

### Description
AutoChild that combines [Dialog.message](#attr-dialogmessage) and [Dialog.icon](#attr-dialogicon).

**Flags**: IR

---
## Attr: Dialog.messageLabel

### Description
AutoChild that shows [Dialog.message](#attr-dialogmessage).

**Flags**: IR

---
## Attr: Dialog.confirmIcon

### Description
Icon to show in the [isc.confirm](isc.md#staticmethod-iscconfirm) dialog.

**Flags**: IR

---
## Attr: Dialog.icon

### Description
Icon to show in this dialog - see [Dialog.message](#attr-dialogmessage).

**Flags**: IR

---
## Attr: Dialog.messageIcon

### Description
AutoChild that shows [Dialog.icon](#attr-dialogicon).

**Flags**: IR

---
## Attr: Dialog.toolbar

### Description
[AutoChild](../main.md#type-autochild) of type Toolbar used to create the [Dialog.toolbarButtons](#attr-dialogtoolbarbuttons).

**Flags**: IR

---
## Attr: Dialog.toolbarButtons

### Description
This is a synonym for [Dialog.buttons](#attr-dialogbuttons)

**Flags**: IR

---
## Attr: Dialog.iconStyle

### Description
Specifies the CSS style if the [Dialog.icon](#attr-dialogicon) in this Dialog.

**Flags**: IR

---
## Attr: Dialog.showToolbar

### Description
Whether to show a toolbar of buttons at the bottom of the Dialog. Default of null will cause the value to be resolved automatically to true or false when the Dialog is first drawn according as [Dialog.toolbarButtons](#attr-dialogtoolbarbuttons) contains buttons or not.

### Groups

- appearance
- toolbar

**Flags**: IR

---
## Attr: Dialog.askIcon

### Description
Icon to show in the [isc.ask](isc.md#staticmethod-iscask) dialog.

**Flags**: IR

---
## Attr: Dialog.sayIcon

### Description
Icon to show in the [isc.say](isc.md#staticmethod-iscsay) dialog.

**Flags**: IR

---
## Attr: Dialog.buttons

### Description
Array of Buttons to show in the [toolbar](#attr-dialogshowtoolbar), if shown.

The set of buttons to use is typically set by calling one of the shortcuts such as [isc.say](isc.md#staticmethod-iscsay) or [isc.confirm](isc.md#staticmethod-iscconfirm) . A custom set of buttons can be passed to these shortcuts methods via the "properties" argument, or to a directly created Dialog.

In both cases, a mixture of [built-in buttons](../main.md#type-dialogbuttons), custom buttons, and other components (such as a [LayoutSpacer](../main.md#class-layoutspacer)) can be passed. Built-in buttons can be referred to as `isc.Dialog.OK`, for example:

```
 isc.Dialog.create({
    buttons:[
       isc.Dialog.OK,
       isc.Dialog.CANCEL,
       isc.LayoutSpacer.create({width:50}),
       { title:"Not now", click:"doSomething()" }
    ]
 })
 
```
Built-in buttons will call standard methods on the Dialog itself, such as [Dialog.cancelClick](#method-dialogcancelclick), as explained in the [list of built-in buttons](../main.md#type-dialogbuttons).

**Flags**: IR

---
## Attr: Dialog.autoFocusButton

### Description
If a toolbar is showing and [autoFocus](#attr-dialogautofocus) is enabled, which button should receive initial focus.

### Groups

- appearance
- toolbar

**Flags**: IR

---
## Attr: Dialog.warnIcon

### Description
Icon to show in the [isc.warn](isc.md#staticmethod-iscwarn) dialog.

**Flags**: IR

---
## Method: Dialog.closeClick

### Description
Handles a click on the close button of this window. The default implementation calls [close()](Window.md#method-windowclose) and returns false to prevent bubbling of the click event.

Override this method if you want other actions to be taken. Custom implementations may call `close()` to trigger the default behavior.

### Returns

`[Boolean](#type-boolean)` — Return false to cancel bubbling the click event

### Groups

- buttons

---
## Method: Dialog.setButtons

### Description
Set the buttons for the toolbar displayed in this dialog. Synonym for [Dialog.setToolbarButtons](#method-dialogsettoolbarbuttons)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newButtons | [Array of Button](#type-array-of-button)|[Array of Button Properties](#type-array-of-button-properties) | false | null | buttons for the toolbar |

---
## Method: Dialog.applyClick

### Description
Handle a click on the 'apply' button of this Dialog. Default implementation is to call `saveData()`, but NOT close the Dialog.

### Groups

- buttons

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

---
## Method: Dialog.setToolbarButtons

### Description
Set the [Dialog.toolbarButtons](#attr-dialogtoolbarbuttons) for this dialog. Synonym for [Dialog.setButtons](#method-dialogsetbuttons).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newButtons | [Array of Button](#type-array-of-button)|[Array of Button Properties](#type-array-of-button-properties) | false | null | buttons for the toolbar |

---
## Method: Dialog.cancelClick

### Description
Handle a click on the 'cancel' button of this Dialog. Default implementation is to return null and hide the Dialog. Override to do something else.

### Groups

- buttons

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

---
## Method: Dialog.saveData

### Description
Method to save this Dialog's data. Called from `okClick()`, `applyClick()`. No default implementation - override to perform some action if required.

### Groups

- buttons

### See Also

- [Dialog.okClick](#method-dialogokclick)
- [Dialog.applyClick](#method-dialogapplyclick)

**Flags**: A

---
## Method: Dialog.okClick

### Description
Handle a click on the 'ok' button of this Dialog. Default implementation is to call `saveData()`, hide the Dialog, then return `true`. Override to do something else.

### Groups

- buttons

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

---
## Method: Dialog.doneClick

### Description
Handle a click on the 'done' button of this Dialog. Default implementation is to hide the dialog then return `true`. Override to do something else.

### Groups

- buttons

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

---
## Method: Dialog.buttonClick

### Description
Fires when any button in this Dialog's toolbar is clicked. Default implementation does nothing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| button | [StatefulCanvas](#type-statefulcanvas) | false | — | button that was clicked |
| index | [int](../main.md#type-int) | false | — | index of the button that was clicked |

### Groups

- buttons

---
## Method: Dialog.setMessage

### Description
Method to update the message on this Dialog.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMessage | [HTMLString](../main.md#type-htmlstring) | false | — | new message to show |

---
## Method: Dialog.yesClick

### Description
Handle a click on the 'yes' button of this Dialog. Default implementation is to return `true`. Override to do something else

### Groups

- buttons

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

---
## Method: Dialog.noClick

### Description
Handle a click on the 'no' button of this Dialog. Default implementation is to return `false`. Override to do something else.

### Groups

- buttons

### See Also

- [DialogButtons](../main.md#type-dialogbuttons)

---
