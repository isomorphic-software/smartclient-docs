# isc Documentation

[← Back to API Index](../reference.md)

---

## StaticMethod: isc.warn

### Description
Show a modal dialog with a message, icon, and "OK" button. See [Dialog.warnIcon](Dialog.md#attr-dialogwarnicon).

The callback will receive boolean true for an OK button click, or null if the Dialog is dismissed via the close button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [HTMLString](../reference.md#type-htmlstring) | false | — | message to display |
| callback | [Callback](../reference.md#type-callback) | true | — | Optional Callback to fire when the user dismisses the dialog. This has the single parameter 'value', indicating the value returned by the Warn dialog from 'okClick()' etc. |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog. To set [custom buttons](Dialog.md#attr-dialogbuttons) for the Dialog, set properties.buttons to an array of buttons eg: { buttons : \[Dialog.OK, Dialog.CANCEL\] } |

### Groups

- Prompting

### See Also

- [Dialog.Warn](Dialog.md#classattr-dialogwarn)
- [isc.say](#staticmethod-iscsay)
- [isc.ask](#staticmethod-iscask)
- [Dialog.okClick](Dialog.md#method-dialogokclick)
- [Dialog.WARN_TITLE](Dialog.md#classattr-dialogwarn_title)

---
## StaticMethod: isc.showConsole

### Description
Method available on the isc object to open the Developer Console.

### Groups

- debug

---
## StaticMethod: isc.showPrompt

### Description
Method available on the isc object to show a modal prompt to the user. This method will display the message using the Dialog.Prompt singleton object.  
Note: if this prompt is to be shown to the user during some slow JavaScript logic, we advise calling this method, then using [Class.delayCall](Class.md#method-classdelaycall) or [Timer.setTimeout](Timer.md#classmethod-timersettimeout) to kick off the slow logic in a separate thread. This ensures that the prompt is showing before the lengthy execution begins.

Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [HTMLString](../reference.md#type-htmlstring) | false | — | message to display |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog, applied before the Dialog is shown |

### Groups

- Prompting

### See Also

- [Dialog.Prompt](Dialog.md#classattr-dialogprompt)

---
## StaticMethod: isc.shallowClone

### Description
Creates a shallow copy of the passed-in Object or Array of Objects, that is, copies all properties of an Object to a new Object, so that the clone now has exactly the same property values as the original Object.

If `shallowClone()` is passed an immutable type such as String and Number, it is returned unchanged. Dates are copied via `new Date(originalDate.getTime())`.

Note that if an Array is passed, all non-Array elements of the Array will be shallow cloned. For a copy of an Array that contains exactly the same elements (not copies), use Array.duplicate().

Only an Array directly passed to `shallowClone()` is copied. Arrays contained within Arrays will not be copied.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object)|[Array](#type-array)|[Object](../reference.md#type-object) | false | — | object to be cloned |

### Returns

`[Object](../reference.md#type-object)|[Array of Object](#type-array-of-object)` — a shallow copy of the passed-in data

---
## StaticMethod: isc.notify

### Description
Displays a new message that's automatically dismissed after a configurable amount of time, as an alternative to [modal notification](#staticmethod-iscconfirm) dialogs that can lower end user productivity.

This method is simply a shorthand way to call [Notify.addMessage](Notify.md#classmethod-notifyaddmessage). For further study, see the [Notify](Notify.md#class-notify) class overview, and the class methods [dismissMessage()](Notify.md#classmethod-notifydismissmessage) and [configureMessages()](Notify.md#classmethod-notifyconfiguremessages).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| contents | [HTMLString](../reference.md#type-htmlstring) | false | — | message to be displayed |
| actions | [Array of NotifyAction](#type-array-of-notifyaction) | true | — | actions (if any) for this message |
| notifyType | [NotifyType](../reference_2.md#type-notifytype) | true | — | category of message |
| settings | [NotifySettings](#type-notifysettings) | true | — | display and behavior settings for this message, overriding any stored settings for this `NotifyType` |

### Returns

`[MessageID](#type-messageid)` — opaque identifier for message

### See Also

- [isc.say](#staticmethod-iscsay)
- [isc.confirm](#staticmethod-iscconfirm)

---
## StaticMethod: isc.showLoginDialog

### Description
Handle a complete login interaction with a typical login dialog asking for username and password credentials using the [LoginDialog](LoginDialog.md#class-logindialog) class.

As with other convenience methods that show Dialogs, such as [isc.warn](#staticmethod-iscwarn), the dialog is shown and the function immediately returns. When the user responds, the provided callback function is called.

If the user clicks the "Log in" button, the credentials entered by the user are passed to the provided "loginFunc" as an Object with properties "username" and "password" (NOTE: both property names are all lowercase), as the variable "credentials". For example:

```
{ username: "barney", password: "rUbbL3" }
```

The "loginFunc" should then attempt to log in by whatever means is necessary. The second parameter to the loginFunc, "dialogCallback", is a function, which must be called _whether login succeeds or fails_ with a true/false value indicating whether login succeeded.

If the login dialog is dismissable (settable as properties.dismissable, default false) and the user dismisses it, the loginFunc will be fired with null for the credentials.

The following code shows typical usage. This code assumes you have created a global function sendCredentials() that send credentials to some authentication system and fires a callback function with the result:

```
 isc.showLoginDialog(function (credentials, dialogCallback) {
     if (credentials == null) return; // dismissed

     // send credentials
     sendCredentials(credentials, function (loginSucceeded) {
         // report success or failure
         dialogCallback(loginSucceeded);
     })
 })
 
```
The login dialog has several built-in behaviors:

*   keyboard focus is automatically placed in the username field
*   hitting enter in the username field proceeds to the password field
*   hitting enter in the password field submits (fires the provided callback)

In addition to normal properties supported by Dialog/Window, the following special properties can be passed:

*   `username`: initial value for the username field
*   `password`: initial value for the password field
*   `usernameTitle`: title for the username field
*   `passwordTitle`: title for the password field
*   `errorMessage`: default error message on login failure
*   `loginButtonTitle`: title for the login button
*   `dismissable`: whether the dialog can be dismissed, default false
*   `errorStyle`: CSS style for the error message, if shown

See below for links to the default values for these properties.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| loginFunc | [Callback](../reference.md#type-callback) | false | — | Function to call to attempt login. Receives parameters "credentials" and "dialogCallback", described above |
| properties | [LoginDialog Properties](#type-logindialog-properties) | true | — | additional properties for the Dialog |

### Groups

- Prompting

### See Also

- [LoginDialog.LOGIN_TITLE](LoginDialog.md#classattr-logindialoglogin_title)
- [LoginDialog.USERNAME_TITLE](LoginDialog.md#classattr-logindialogusername_title)
- [LoginDialog.PASSWORD_TITLE](LoginDialog.md#classattr-logindialogpassword_title)
- [LoginDialog.LOGIN_BUTTON_TITLE](LoginDialog.md#classattr-logindialoglogin_button_title)
- [LoginDialog.LOGIN_ERROR_MESSAGE](LoginDialog.md#classattr-logindialoglogin_error_message)

---
## StaticMethod: isc.ignore

### Description
Clear an observation set up by [Page.observe](Page.md#classmethod-pageobserve).

This method is available as `isc.Page.ignore()` or just `isc.ignore()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| observerID | [String](#type-string) | false | — | ID returned from [Page.observe](Page.md#classmethod-pageobserve) call we want to clear |

---
## StaticMethod: isc.echoAll

### Description
Same as [Log.echoAll](Log.md#classmethod-logechoall).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

---
## StaticMethod: isc.ask

### Description
Show a modal dialog with a message, icon, and "Yes" and "No" buttons. See [Dialog.askIcon](Dialog.md#attr-dialogaskicon).

The callback will receive boolean true for a Yes button click, boolean false for a No button click, or null if the Dialog is dismissed via the close button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [HTMLString](../reference.md#type-htmlstring) | false | — | message to display |
| callback | [Callback](../reference.md#type-callback) | true | — | Callback to fire when the user clicks a button to dismiss the dialog. This has the single parameter 'value', indicating the value returned by the Warn dialog from 'okClick()' etc. |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog. To set [custom buttons](Dialog.md#attr-dialogbuttons) for the Dialog, set properties.buttons to an array of buttons eg: { buttons : \[Dialog.OK, Dialog.CANCEL\] } |

### Groups

- Prompting

### See Also

- [Dialog.Warn](Dialog.md#classattr-dialogwarn)
- [isc.warn](#staticmethod-iscwarn)
- [Dialog.yesClick](Dialog.md#method-dialogyesclick)
- [Dialog.noClick](Dialog.md#method-dialognoclick)
- [Dialog.ASK_TITLE](Dialog.md#classattr-dialogask_title)

---
## StaticMethod: isc.logWarn

### Description
Same as [Log.logWarn](Log.md#classmethod-loglogwarn).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in, defaults to "Log" |

---
## StaticMethod: isc.askForValue

### Description
Show a modal dialog with a text entry box, asking the user to enter a value.

As with other convenience methods that show Dialogs, such as [isc.warn](#staticmethod-iscwarn), the dialog is shown and the function immediately returns. When the user responds, the provided callback is called.

If the user clicks OK, the value typed in is passed to the callback (including the empty string ("") if nothing was entered. If the user clicks cancel, the value passed to the callback is null.

A default value for the text field can be passed via `properties.defaultValue`.

Keyboard focus is automatically placed in the text entry field, and hitting the enter key is the equivalent of pressing OK.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to display |
| callback | [Callback](../reference.md#type-callback) | true | — | Callback to fire when the user clicks a button to dismiss the dialog. This has the single parameter 'value', indicating the user entry, or null if cancel was pressed or the window closed |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog. To set [custom buttons](Dialog.md#attr-dialogbuttons) for the Dialog, set properties.buttons to an array of buttons eg: { buttons : \[Dialog.OK, Dialog.CANCEL\] } |

### Groups

- Prompting

### See Also

- [Dialog.okClick](Dialog.md#method-dialogokclick)
- [Dialog.cancelClick](Dialog.md#method-dialogcancelclick)
- [Dialog.ASK_FOR_VALUE_TITLE](Dialog.md#classattr-dialogask_for_value_title)

---
## StaticMethod: isc.observe

### Description
Method to set up a static [observation](Class.md#method-classobserve) on some target object. This allows developers to perform some action every time a particular method is invoked on a target object.

This method returns a unique observation identifier string. To cancel the observation, pass this identifier to [Page.ignore](Page.md#classmethod-pageignore).

If multiple observations are set up for the same target object and method, the notification actions will be fired in the order in which they were registered.

This method is available as `isc.Page.observe()` or just `isc.observe()`

Note _\[potential memory leak\]_: If the target object is a simple JavaScript object (not an instance of a SmartClient class), developers should always call [Page.ignore](Page.md#classmethod-pageignore) to stop observing the object if an observation is no longer necessary.  
This ensures that if the object is subsequently allowed to go out of scope by application code, the Page level observation system will not retain a reference to it (so the browser can reclaim the allocated memory).  
While cleaning up observations that are no longer required is always good practice, this memory leak concern is not an issue if the target object is an instance of a SmartClient class. In that case the observation is automatically released when the target is [destroyed](Class.md#method-classdestroy).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to observe. This may be any JavaScript object with the specified target method, including native arrays, and instances of SmartClient classes such as [Canvas](Canvas.md#class-canvas). |
| methodName | [String](#type-string) | false | — | Name of the method to observe. Every time this method is invoked on the target object the specified action will fire (after the default implementation completes). |
| action | [Function](#type-function)|[String](#type-string) | false | — | Action to take when the observed method is invoked.  
If `action` is a string to execute, certain keywords are available for context:

*   `observed` is the target object being observed (on which the method was invoked).
*   `returnVal` is the return value from the observed method (if there is one)
*   For functions defined with explicit parameters, these will also be available as keywords within the action string

If `action` is a function, the arguments for the original method will also be passed to this action function as arguments. If developers need to access the target object being observed from the action function they may use native javascript techniques such as [javascript closure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) to do so. The return value from the observed method is not available to the action function. |

### Returns

`[String](#type-string)` — Identifier for the observation. Pass this to [Page.ignore](Page.md#classmethod-pageignore) to stop observing the method in question.

---
## StaticMethod: isc.setScreenReaderMode

### Description
Enables full screen reader mode. Must be called before any components are created. See [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newState | [boolean](../reference.md#type-boolean) | false | — | new setting |

### Groups

- accessibility

---
## StaticMethod: isc.confirm

### Description
Show a modal dialog with a message, icon, and "OK" and "Cancel" buttons. See [Dialog.confirmIcon](Dialog.md#attr-dialogconfirmicon).

The callback will receive boolean true for an OK button click, or null for a Cancel click or if the Dialog is dismissed via the close button.

Note: this does not override the native window.confirm() method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [HTMLString](../reference.md#type-htmlstring) | false | — | message to display |
| callback | [Callback](../reference.md#type-callback) | true | — | Callback to fire when the user clicks a button to dismiss the dialog. This has the single parameter 'value', indicating the value returned by the Warn dialog from 'okClick()' etc. |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog. To set [custom buttons](Dialog.md#attr-dialogbuttons) for the Dialog, set properties.buttons to an array of buttons eg: { buttons : \[Dialog.OK, Dialog.CANCEL\] } |

### Groups

- Prompting

### See Also

- [isc.notify](#staticmethod-iscnotify)
- [Dialog.Warn](Dialog.md#classattr-dialogwarn)
- [isc.warn](#staticmethod-iscwarn)
- [Dialog.okClick](Dialog.md#method-dialogokclick)
- [Dialog.cancelClick](Dialog.md#method-dialogcancelclick)
- [Dialog.CONFIRM_TITLE](Dialog.md#classattr-dialogconfirm_title)

---
## StaticMethod: isc.getValues

### Description
Return all values of a given object

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to get properties from |

### Returns

`[Array](#type-array)` — values of all properties. NOTE: never null

---
## StaticMethod: isc.logInfo

### Description
Same as [Log.logInfo](Log.md#classmethod-logloginfo).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in, defaults to "Log" |

---
## StaticMethod: isc.rejectWithError

### Description
Creates a [Promise](../reference_2.md#object-promise) that rejects with an "error"-[type](AsyncOperationResult.md#attr-asyncoperationresulttype) [AsyncOperationResult](../reference.md#object-asyncoperationresult).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errorMessage | [HTMLString](../reference.md#type-htmlstring) | true | — | a message describing the error, if available. |
| additionalProperties | [AsyncOperationResult Properties](#type-asyncoperationresult-properties) | true | — | additional properties to add to the reject result. Note that the `type` and/or `errorMessage` properties, if set on `additionalProperties`, will not be preserved. |

### Returns

`[Promise](#type-promise)` — the `Promise`.

---
## StaticMethod: isc.getIconPageRect

### Description
Returns the size / position of an icon on the page as an array of coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Object](../reference.md#type-object) | false | — | icon definition for the icon you want to determine the position of (defaults to first icon in this.icons). |

### Returns

`[Array](#type-array)` — four element array representing the Left, Top, Width, and Height of the icon in px.

**Flags**: A

---
## StaticMethod: isc.getIconLeft

### Description
Returns the (offset) left-coordinate of an icon within its containing widget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Object](../reference.md#type-object) | false | — | icon definition |

### Returns

`[number](#type-number)` — icon left position in px

**Flags**: A

---
## StaticMethod: isc.say

### Description
Show a modal dialog with a message, icon, and "OK" button. Intended for notifications which are not really warnings (default icon is less severe). See [Dialog.sayIcon](Dialog.md#attr-dialogsayicon).

The callback will receive boolean true for an OK button click, or null if the Dialog is dismissed via the close button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [HTMLString](../reference.md#type-htmlstring) | false | — | message to display |
| callback | [Callback](../reference.md#type-callback) | true | — | Optional Callback to fire when the user dismisses the dialog. This has the single parameter 'value', indicating the value returned by the Warn dialog from 'okClick()' etc. |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog. To set [custom buttons](Dialog.md#attr-dialogbuttons) for the Dialog, set properties.buttons to an array of buttons eg: { buttons : \[Dialog.OK, Dialog.CANCEL\] } |

### Groups

- Prompting

### See Also

- [isc.notify](#staticmethod-iscnotify)
- [Dialog.Warn](Dialog.md#classattr-dialogwarn)
- [isc.warn](#staticmethod-iscwarn)
- [isc.ask](#staticmethod-iscask)
- [Dialog.okClick](Dialog.md#method-dialogokclick)
- [Dialog.SAY_TITLE](Dialog.md#classattr-dialogsay_title)

---
## StaticMethod: isc.echoLeaf

### Description
Same as [Log.echoLeaf](Log.md#classmethod-logecholeaf).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

---
## StaticMethod: isc.getValueForKey

### Description
Given a key and an object of `key:value` pairs, return the value that corresponds to that key.

If the key is not found, `defaultValue` will be returned if provided, otherwise the key will be returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [String](#type-string)|[number](#type-number) | false | — | key to look for |
| valueMap | [Object](../reference.md#type-object) | false | — | object of key:value pairs |
| defaultValue | [Any](#type-any) | true | — | default value to return if key not found |

### Returns

`[Any](#type-any)` — returns value in valueMap under name key, or defaultValue if key not found

---
## StaticMethod: isc.clearPrompt

### Description
Clear the modal prompt being shown to the user.

### Groups

- Prompting

### See Also

- [Dialog.Prompt](Dialog.md#classattr-dialogprompt)

---
## StaticMethod: isc.getKeys

### Description
Return all keys (property names) of a given object

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to get properties from |

### Returns

`[Array](#type-array)` — String names of all properties. NOTE: never null

---
## StaticMethod: isc.getIconRect

### Description
Returns the size / position of an icon with respect to the widget rendering out the form item as an array of coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Object](../reference.md#type-object) | false | — | icon definition for the icon you want to determine the position of (defaults to first icon in this.icons). |

### Returns

`[Array](#type-array)` — four element array representing the Left, Top, Width, and Height of the icon in px.

**Flags**: A

---
## StaticMethod: isc.makeReverseMap

### Description
Given a key:value map, return a new map as value:key.

If the same value appears more than once, the key will correspond to the last instance of that value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valueMap | [Object](../reference.md#type-object) | false | — | object of key:value pairs |

### Returns

`[Object](../reference.md#type-object)` — reversed value map

---
## StaticMethod: isc.firstKey

### Description
Return the first property name in a given Object, according to for..in iteration order.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to get properties from |

### Returns

`[String](#type-string)` — first property name, or null if Object has no properties

---
## StaticMethod: isc.setRadioGroup

### Description
Sets the [radioGroup](StatefulCanvas.md#attr-statefulcanvasradiogroup) identifier for this canvas's mutually exclusive selection group.

### Groups

- state
- event handling

---
## StaticMethod: isc.sortObjectByProperties

### Description
Given a simple javascript object, return that object sorted by properties, such that when iterating through the properties of the object, values will show up in sorted order.  
Usage example - may be used to sort a [formItem valueMap](FormItem.md#attr-formitemvaluemap) defined as an object by display value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to sort |
| comparator | [Function](#type-function) | true | — | Comparator function to use when sorting the object properties |

### Returns

`[Object](../reference.md#type-object)` — sorted version of the object passed in.

---
## StaticMethod: isc.logEchoAll

### Description
Logs the echoed object (using [isc.echoAll](#staticmethod-iscechoall)) as a warning, prefixed with an optional message.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | object to echo |
| message | [String](#type-string) | false | — | message to log |

### See Also

- [Log.logWarn](Log.md#classmethod-loglogwarn)

---
## StaticMethod: isc.eval

### Description
Evaluate a string of script and return the result. Falls through to [Class.evaluate()](Class.md#classmethod-classevaluate)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| expression | [String](#type-string) | false | — | Expression to evaluate |

### Returns

`[Any](#type-any)` — Result of evaluating the expression passed in

---
## StaticMethod: isc.sortObject

### Description
Given a simple javascript object, return that object sorted by keys, such that when iterating through the properties of the object, they will show up in sorted order.  
Usage example - may be used to sort a [formItem valueMap](FormItem.md#attr-formitemvaluemap) defined as an object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to sort |
| comparator | [Function](#type-function) | true | — | Comparator function to use when sorting the objects keys |

### Returns

`[Object](../reference.md#type-object)` — sorted version of the object passed in.

---
## StaticMethod: isc.getKeyForValue

### Description
Given a value and an object of `key:value` pairs, return a key that corresponds to that value.

If the key is not found, `defaultKey` will be returned if provided, otherwise the value will be returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string)|[number](#type-number) | false | — | value to look for |
| valueMap | [Object](../reference.md#type-object) | false | — | object of key:value pairs |
| defaultKey | [Any](#type-any) | true | — | default key to return if value not found |

### Returns

`[Any](#type-any)` — returns first key in valueMap with value, or defaultKey if value not found

---
## StaticMethod: isc.echo

### Description
Same as [Log.echo](Log.md#classmethod-logecho).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

---
## StaticMethod: isc.setAutoDraw

### Description
Set the global default setting for [Canvas.autoDraw](Canvas.md#attr-canvasautodraw).

After calling `isc.setAutoDraw()`, any newly created Canvas which is not given an explicit setting for [autoDraw](Canvas.md#attr-canvasautodraw) will follow the new default setting.

autoDraw:false is the recommended default setting for most applications since it ensures that extra draws will not occur when developers inadvertently omit the autoDraw:false setting on child components.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| enable | [boolean](../reference.md#type-boolean) | true | — | whether autoDraw should be enabled or disabled. Defaults to true. |

### Groups

- autoDraw

### See Also

- [Canvas.autoDraw](Canvas.md#attr-canvasautodraw)

---
## StaticMethod: isc.getIconTop

### Description
Returns the (offset) top-coordinate of an icon within its containing widget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Object](../reference.md#type-object) | false | — | icon definition |

### Returns

`[number](#type-number)` — icon top position in px

**Flags**: A

---
## StaticMethod: isc.clone

### Description
Create a deep clone of an object that can be edited without affecting the original

All mutable types, including Objects, Arrays and Dates, are copied. All immutable types (Number, String, etc) are just preserved by reference.

Only JavaScript built-in types may be cloned. SmartClient UI widgets do not support cloning but must be created explicitly via [Class.create](Class.md#classmethod-classcreate).  
Note that you also can't duplicate a live canvas by passing into _create()_ as an argument. If you need to create multiple components with similar configuration, some common patterns inclulde:

*   Create a new SmartClient class with the desired default configuration, and create instances of this class as needed.
*   For components created by some specific instance, the [AutoChild](../reference.md#type-autochild) system may be used. Developers can specify a standard configuration in `_autoChildName_Defaults` and `_autoChildName_Properties`, and use [Class.createAutoChild](Class.md#method-classcreateautochild) to create a number of standard auto child components.
*   A less formal approach might be to have a simple _getter_ type method which created and returned a new component each time it was called, passing in a standard configuration block.

Does not handle looping references (will infinite loop).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to clone |

### Returns

`[Object](../reference.md#type-object)` — cloned object

### Groups

- serialization

---
## StaticMethod: isc.overwriteClass

### Description
Shortcut for `isc.ClassFactory.overwriteClass()`.

### See Also

- [ClassFactory.overwriteClass](ClassFactory.md#classmethod-classfactoryoverwriteclass)

---
## StaticMethod: isc.defaultAsyncOperationCatchCallback

### Description
A catch callback that can be used on a Promise for an [AsyncOperationResult](../reference.md#object-asyncoperationresult) to provide default error handling.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [Any](#type-any) | true | — | The reason (result of a rejected Promise). |

### Returns

`[AsyncOperationResult](#type-asyncoperationresult)` — an `AsyncOperationResult` from the provided reason.

---
## StaticMethod: isc.timeStamp

### Description
Shorthand for `new Date().getTime();`, this returns a timeStamp - a large number which is incremented by 1 every millisecond. Can be used to generate unique identifiers, or perform timing tasks.

### Returns

`[int](../reference.md#type-int)` — a large integer (actually the number of milliseconds since 1/1/1970)

---
## StaticMethod: isc.logEcho

### Description
Logs the echoed object (using [isc.echo](#staticmethod-iscecho)) as a warning, prefixed with an optional message.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | object to echo |
| message | [String](#type-string) | false | — | message to log |

### See Also

- [Log.logWarn](Log.md#classmethod-loglogwarn)

---
## StaticMethod: isc.dismissCurrentDialog

### Description
If a dialog triggered via [isc.say](#staticmethod-iscsay), [isc.ask](#staticmethod-iscask), [isc.warn](#staticmethod-iscwarn), [isc.confirm](#staticmethod-iscconfirm) or [isc.askForValue](#staticmethod-iscaskforvalue) is currently visible, it will be dismissed. The callback passed to the relevant method will never fire.

Note this is a rarely used API with very few valid use cases. As an example, perhaps some kind of periodic (non-user triggered) event would cause an entire area of the UI to be removed (such as a tab) and the system wants to ensure that no modal dialogs are currently showing from that part of the UI. In this case, while `dismissCurrentDialog` could be used to ensure the part of the UI being removed didn't leave behind a modal dialog.

To clear a modal prompt shown by [isc.showPrompt](#staticmethod-iscshowprompt), use [isc.clearPrompt](#staticmethod-iscclearprompt) instead.

### Groups

- Prompting

---
## StaticMethod: isc.createErrorResult

### Description
Creates an "error"-[type](AsyncOperationResult.md#attr-asyncoperationresulttype) [AsyncOperationResult](../reference.md#object-asyncoperationresult).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errorMessage | [HTMLString](../reference.md#type-htmlstring) | true | — | a message describing the error, if available. |
| additionalProperties | [AsyncOperationResult Properties](#type-asyncoperationresult-properties) | true | — | additional properties to add to the error result. Note that the `type` and/or `errorMessage` properties, if set on `additionalProperties`, will not be preserved. |

---
## StaticMethod: isc.addProperties

### Description
Add all properties and methods from any number of objects to a destination object, overwriting properties in the destination object.

Common uses of `addProperties` include creating a shallow copy of an object:

```
     isc.addProperties({}, someObject);

 
```
Combining settings in order of precedence:
```
     isc.addProperties({}, defaults, overrides, skinOverrides);

 
```

**NOTES**:

*   Do not use `addProperties` to add defaults to an ISC class. Use [Class.addProperties](Class.md#classmethod-classaddproperties), as in: _MyClassName_`.addProperties()`.
*   You may find it more convenient to use the instance method [Class.addProperties](Class.md#method-classaddproperties), as in: _myClassInstance_`.addProperties()`, but there's no functional difference from using this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| destination | [Object](../reference.md#type-object) | false | — | object to add properties to |
| arguments 1-N | [Object](../reference.md#type-object) | true | — | objects to obtain properties from. Properties of all arguments other than destination are applied in turn. |

### Returns

`[Object](../reference.md#type-object)` — returns the destination object

### See Also

- [Class.addProperties](Class.md#classmethod-classaddproperties)
- [Class.addProperties](Class.md#method-classaddproperties)

---
## StaticMethod: isc.addDefaults

### Description
Copy any properties that do not already have a value in destination. Null and zero values are not overwritten, but 'undef' values will be.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| destination | [Object](../reference.md#type-object) | false | — | Object to which properties will be added. |
| source | [Object](../reference.md#type-object) | false | — | Object from which properties will be added. |

### Returns

`[Object](../reference.md#type-object)` — The destination object is returned.

---
## StaticMethod: isc.defineClass

### Description
Shortcut for `isc.ClassFactory.defineClass()`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | Name for the new class. |
| superClass | [Class](#type-class) | true | — | Optional SuperClass Class object or name |

### Returns

`[Class](#type-class)` — Returns the new Class object.

### See Also

- [ClassFactory.defineClass](ClassFactory.md#classmethod-classfactorydefineclass)

---
## StaticMethod: isc.getAsyncMessage

### Description
Returns a user-displayable message for the given [AsyncOperationResult](../reference.md#object-asyncoperationresult) if its [type](AsyncOperationResult.md#attr-asyncoperationresulttype) is not "success".

[isc.getAsyncMessage()](#staticmethod-iscgetasyncmessage) and [AsyncUtil.getAsyncMessage()](AsyncUtil.md#classmethod-asyncutilgetasyncmessage) are equivalent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [AsyncOperationResult](#type-asyncoperationresult) | false | — | the `AsyncOperationResult`. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — If the [type](AsyncOperationResult.md#attr-asyncoperationresulttype) is "success", then `null`; otherwise, a user-displayable message describing the non-successful result.

### See Also

- [AsyncUtil.asyncErrorMessageGeneric](AsyncUtil.md#classattr-asyncutilasyncerrormessagegeneric)
- [AsyncUtil.asyncCanceledMessage](AsyncUtil.md#classattr-asyncutilasynccanceledmessage)
- [AsyncUtil.asyncCanceledMessageGeneric](AsyncUtil.md#classattr-asyncutilasynccanceledmessagegeneric)
- [AsyncUtil.asyncDisabledMessageGeneric](AsyncUtil.md#classattr-asyncutilasyncdisabledmessagegeneric)
- [AsyncUtil.asyncNonSuccessMessage](AsyncUtil.md#classattr-asyncutilasyncnonsuccessmessage)
- [AsyncUtil.asyncNonSuccessMessageGeneric](AsyncUtil.md#classattr-asyncutilasyncnonsuccessmessagegeneric)

---
## StaticMethod: isc.propertyDefined

### Description
Is some property specified on the object passed in? This will return true if `object[propertyName]` has ever been set to any value, and not deleted.  
May return true even if `object[propertyName] === undefined` if the property is present on the object and has been explicitly set to undefined.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to test |
| propertyName | [String](#type-string) | false | — | Which property is being tested for? |

### Returns

`[boolean](../reference.md#type-boolean)` — true if property is defined

---
## StaticMethod: isc.showFadingPrompt

### Description
Method available on the isc object to show a temporary modal prompt to the user. This method will display the message using the Dialog.Prompt singleton object, then hide it using a fade animation effect.  
Note: if this prompt is to be shown to the user during some slow JavaScript logic, we advise calling this method, then using [Class.delayCall](Class.md#method-classdelaycall) or [Timer.setTimeout](Timer.md#classmethod-timersettimeout) to kick off the slow logic in a separate thread. This ensures that the prompt is showing before the lengthy execution begins.

The prompt may be cleared before the duration has elapsed via a call to [isc.clearPrompt](#staticmethod-iscclearprompt) and any callback specified will still be fired even if the prompt is dismissed early.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to display |
| duration | [number](#type-number) | false | — | how long the message should appear for in milliseconds before fading from view. |
| callback | [Callback](../reference.md#type-callback) | true | — | When the prompt is hidden, callback will be fired. |
| properties | [Dialog Properties](#type-dialog-properties) | true | — | additional properties for the Dialog, applied before the Dialog is shown |

### Groups

- Prompting

### See Also

- [Dialog.Prompt](Dialog.md#classattr-dialogprompt)

---
