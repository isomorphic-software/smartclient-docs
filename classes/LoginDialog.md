# LoginDialog Documentation

[← Back to API Index](../reference.md)

---

## Class: LoginDialog

*Inherits from:* [Window](Window.md#class-window)

### Description
Handle a complete login interaction with a typical login dialog asking for username and password credentials. Use this class to quickly present a traditional username/password authentication mechanism in a SmartClient window.

To adapt this class to your requirements, first implement LoginDialog.loginFunc to submit the username and password to the authentication mechanism of your choice, calling dialogCallback once the authentication process completes.

### Groups

- Prompting

### See Also

- [isc.showLoginDialog](isc.md#staticmethod-iscshowlogindialog)

---
## ClassAttr: LoginDialog.LOGIN_ERROR_MESSAGE

### Description
Default error message displayed on failed login in the dialog shown by [isc.showLoginDialog](isc.md#staticmethod-iscshowlogindialog).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: LoginDialog.LOGIN_TITLE

### Description
Default title for the dialog displayed by [isc.showLoginDialog](isc.md#staticmethod-iscshowlogindialog). A custom title can alternatively be specified as the `title` attribute of the `properties` parameter passed to that method.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: LoginDialog.USERNAME_TITLE

### Description
Default title for the ["usernameItem"](#attr-logindialogusernameitem) field in the dialog displayed by [isc.showLoginDialog](isc.md#staticmethod-iscshowlogindialog).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: LoginDialog.PASSWORD_TITLE

### Description
Default title for the ["passwordItem"](#attr-logindialogpassworditem) field in the dialog displayed by [isc.showLoginDialog](isc.md#staticmethod-iscshowlogindialog).

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: LoginDialog.LOGIN_BUTTON_TITLE

### Description
Default title for login button in the dialog displayed by [isc.showLoginDialog](isc.md#staticmethod-iscshowlogindialog).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: LoginDialog.passwordItemTitle

### Description
Specifies the title of the "passwordItem" field of the [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Attr: LoginDialog.errorMessage

### Description
Specifies the default error message displayed on the login form when authentication fails.

**Flags**: IR

---
## Attr: LoginDialog.passwordItem

### Description
Password field item in [LoginDialog.loginForm](#attr-logindialogloginform).

### See Also

- [LoginDialog.allowBlankPassword](#attr-logindialogallowblankpassword)
- [LoginDialog.passwordItemTitle](#attr-logindialogpassworditemtitle)

**Flags**: IR

---
## Attr: LoginDialog.errorStyle

### Description
Specifies the CSS style of the error text shown for a login failure.

**Flags**: IR

---
## Attr: LoginDialog.dismissable

### Description
Whether the user should be able to dismiss the login dialog without entering credentials. Set to true if logging in is optional. When set, a close button will be present, and hitting escape will also dismiss the dialog.

If the Dialog is dismissed, [LoginDialog.loginFunc](#method-logindialogloginfunc) is called with null arguments.

Note that this attribute overrides the dismissOnEscape and showCloseButton attributes.

**Flags**: IR

---
## Attr: LoginDialog.loginButtonTitle

### Description
Specifies the contents of the login submission button of the [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Attr: LoginDialog.showLostPasswordLink

### Description
If true, display a [LinkItem](LinkItem.md#class-linkitem) ([LoginDialog.lostPasswordItem](#attr-logindialoglostpassworditem)) meant for the user to click if the account's credentials are forgotten. The text of the link is controlled by [LoginDialog.lostPasswordItemTitle](#attr-logindialoglostpassworditemtitle). If clicked, the link will fire [LoginDialog.lostPassword](#method-logindialoglostpassword).

**Flags**: IR

---
## Attr: LoginDialog.registrationItem

### Description
[LinkItem](LinkItem.md#class-linkitem) to page requesting new user registration in [LoginDialog.loginForm](#attr-logindialogloginform).

To handle user clicks on this link, implement [LoginDialog.register](#method-logindialogregister).

To handle a user click as a physical link to another page, set [defaultValue](FormItem.md#attr-formitemdefaultvalue) via loginDialog.registrationItemProperties: `registrationItemProperties: { defaultValue: "register.html" },`

### See Also

- [LoginDialog.showRegistrationLink](#attr-logindialogshowregistrationlink)
- [LoginDialog.registrationItemTitle](#attr-logindialogregistrationitemtitle)

**Flags**: IR

---
## Attr: LoginDialog.lostPasswordItem

### Description
[LinkItem](LinkItem.md#class-linkitem) to page requesting forgotten password in [LoginDialog.loginForm](#attr-logindialogloginform).

To handle user clicks on this link, implement [LoginDialog.lostPassword](#method-logindialoglostpassword).

To handle a user click as a physical link to another page, set [defaultValue](FormItem.md#attr-formitemdefaultvalue) via loginDialog.lostPasswordItemProperties: `lostPasswordItemProperties: { defaultValue: "register.html" },`

### See Also

- [LoginDialog.showLostPasswordLink](#attr-logindialogshowlostpasswordlink)
- [LoginDialog.lostPasswordItemTitle](#attr-logindialoglostpassworditemtitle)

**Flags**: IR

---
## Attr: LoginDialog.showRegistrationLink

### Description
If true, display a [LinkItem](LinkItem.md#class-linkitem) ([LoginDialog.registrationItem](#attr-logindialogregistrationitem)) meant for the user to click if the user wishes to register a new account. The text of the link is controlled by [LoginDialog.registrationItemTitle](#attr-logindialogregistrationitemtitle). If clicked, the link will fire [LoginDialog.register](#method-logindialogregister).

**Flags**: IR

---
## Attr: LoginDialog.loginForm

### Description
Form used to request login credentials from the user.

### See Also

- [LoginDialog.formFields](#attr-logindialogformfields)

**Flags**: R

---
## Attr: LoginDialog.usernameItem

### Description
Username field item in [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Attr: LoginDialog.dismissOnEscape

### Description
Do not set LoginDialog.dismissOnEscape; it is controlled by the [LoginDialog.dismissable](#attr-logindialogdismissable) property.

**Flags**: IRW

---
## Attr: LoginDialog.title

### Description
Specifies the title of the dialog box.

**Flags**: IR

---
## Attr: LoginDialog.showCloseButton

### Description
Do not set LoginDialog.showCloseButton; it is controlled by the [LoginDialog.dismissable](#attr-logindialogdismissable) property.

**Flags**: IRW

---
## Attr: LoginDialog.items

### Description
Specifies the dialog contents. By default, the dialog only contains [LoginDialog.loginForm](#attr-logindialogloginform). If desired, additional widgets may be placed before/after the loginForm. To specify these widgets as [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren), use the syntax "autoChild:_childName_" [as used for panes/items of\\n Tabs/SectionStacks](../kb_topics/autoChildren.md#kb-topic-autochildren).

**Flags**: IR

---
## Attr: LoginDialog.loginFailureItem

### Description
Field item containing login error message (if required) in [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Attr: LoginDialog.formFields

### Description
Customizes the fields present in the dialog, or specifies new fields to be present, in the same manner as with [DynamicForm.fields](DynamicForm.md#attr-dynamicformfields).

### See Also

- [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields)

**Flags**: IR

---
## Attr: LoginDialog.lostPasswordItemTitle

### Description
Specifies the contents of the password request button (if configured) on the [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Attr: LoginDialog.registrationItemTitle

### Description
Specifies the contents of the registration link (if configured) on the [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Attr: LoginDialog.loginButton

### Description
Login submission button in [LoginDialog.loginForm](#attr-logindialogloginform).

### See Also

- [LoginDialog.loginButtonTitle](#attr-logindialogloginbuttontitle)

**Flags**: IR

---
## Attr: LoginDialog.allowBlankPassword

### Description
If true, the login form will allow blank passwords to be submitted. Otherwise the form fails to be validated until the user enters at least one character into the password field.

**Flags**: IR

---
## Attr: LoginDialog.usernameItemTitle

### Description
Specifies the title of the "usernameItem" field of the [LoginDialog.loginForm](#attr-logindialogloginform).

**Flags**: IR

---
## Method: LoginDialog.loginFunc

### Description
User-supplied callback function to process login transactions.

If the user clicks the "Log in" button, the credentials entered by the user are passed to loginFunc as an Object with properties "username" and "password" (NOTE: both property names are all lowercase), as the variable "credentials". For example:

```
{ username: "barney", password: "rUbbL3" }
```

This function should then attempt to log in by whatever means is necessary. The second parameter to the loginFunc, "dialogCallback", is a function, which must be called _whether login succeeds or fails_ with a true/false value indicating whether login succeeded.

If the login dialog is dismissable (settable as properties.dismissable, default false) and the user dismisses it, loginFunc will be fired with null for the credentials.

The following code shows typical usage. This code assumes you have created a global function sendCredentials() that send credentials to some authentication system and fires a callback function with the result:

```
 ...
 loginFunc : function (credentials, dialogCallback) {
     if (credentials == null) return; // dismissed

     // send credentials
     sendCredentials(credentials, function (loginSucceeded) {
         // report success or failure
         dialogCallback(loginSucceeded);
     })
 })
 ...
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| credentials | [Object](../reference.md#type-object) | false | — | Login credentials supplied by the user |
| dialogCallback | [Function](#type-function) | false | — | Function that must be called once the login transaction completes |

---
## Method: LoginDialog.register

### Description
Called if the user clicks on the [registration link](#attr-logindialogregistrationitem) on the login form. Implement this method to allow the user to register for a new account.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | Current values of form fields |
| form | [DynamicForm](#type-dynamicform) | false | — | Form on which the link was clicked |

---
## Method: LoginDialog.lostPassword

### Description
Called if the user clicks on the ["Lost Password"](#attr-logindialoglostpassworditem) link on the login form. Implement this method to allow the user to request the password be resent or reset.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | Current values of form fields |
| form | [DynamicForm](#type-dynamicform) | false | — | Form on which the link was clicked |

---
