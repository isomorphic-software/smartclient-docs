# TextAreaItem Documentation

[← Back to API Index](../main.md)

---

## Class: TextAreaItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
Class for editable multi-line text areas (uses HTML ``<TEXTAREA>`` object)

---
## ClassAttr: TextAreaItem.HARD

### Description
A declared value of the enum type [TEXTAREA\_WRAP](../main.md#type-textarea_wrap).

**Flags**: R

---
## ClassAttr: TextAreaItem.SOFT

### Description
A declared value of the enum type [TEXTAREA\_WRAP](../main.md#type-textarea_wrap).

**Flags**: R

---
## ClassAttr: TextAreaItem.OFF

### Description
A declared value of the enum type [TEXTAREA\_WRAP](../main.md#type-textarea_wrap).

**Flags**: R

---
## Attr: TextAreaItem.selectOnFocus

### Description
Allows the [selectOnFocus](DynamicForm.md#attr-dynamicformselectonfocus) behavior to be configured on a per-FormItem basis. Normally all items in a form default to the value of [DynamicForm.selectOnFocus](DynamicForm.md#attr-dynamicformselectonfocus).

### Groups

- focus

**Flags**: IRW

---
## Attr: TextAreaItem.textBoxStyle

### Description
Base CSS class to apply to this item's input element. NOTE: See the [CompoundFormItem_skinning](../main.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

### Groups

- appearance

**Flags**: IRW

---
## Attr: TextAreaItem.supportsCutPasteEvents

### Description
Does the current formItem support native cut and paste events?

This attribute only applies to freeform text entry fields such as [TextItem](TextItem.md#class-textitem) and [TextAreaItem](#class-textareaitem), and only if [TextAreaItem.changeOnKeypress](#attr-textareaitemchangeonkeypress) is true. If true, developers can detect the user editing the value via cut or paste interactions (triggered from keyboard shortcuts or the native browser menu options) using the [FormItem.isCutEvent](FormItem.md#method-formitemiscutevent) and [FormItem.isPasteEvent](FormItem.md#method-formitemispasteevent) methods. This allows custom cut/paste handling to be added to the various change notification flow methods including [FormItem.change](FormItem.md#method-formitemchange), and [FormItem.transformInput](FormItem.md#method-formitemtransforminput).

**Flags**: IRW

---
## Attr: TextAreaItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Attr: TextAreaItem.selectOnClick

### Description
Allows the [selectOnClick](DynamicForm.md#attr-dynamicformselectonclick) behavior to be configured on a per-FormItem basis. Normally all items in a form default to the value of [DynamicForm.selectOnClick](DynamicForm.md#attr-dynamicformselectonclick).

### Groups

- focus

**Flags**: IRW

---
## Attr: TextAreaItem.formatOnBlur

### Description
With `formatOnBlur` enabled, this textAreaItem will format its value according to the rules described in [FormItem.mapValueToDisplay](FormItem.md#method-formitemmapvaluetodisplay) as long as the item does not have focus. Once the user puts focus into the item the formatter will be removed. This provides a simple way for developers to show a nicely formatted display value in a freeform text field, without the need for an explicit [FormItem.formatEditorValue](FormItem.md#method-formitemformateditorvalue) and [FormItem.parseEditorValue](FormItem.md#method-formitemparseeditorvalue) pair.

**Flags**: IRW

---
## Attr: TextAreaItem.wrap

### Description
Text wrapping style.

### Groups

- appearance

**Flags**: IRW

---
## Attr: TextAreaItem.pickerIconHeight

### Description
TextAreaItem has an explicit pickerIconHeight as we don't want the picker icon, if shown, to size itself to match the height of the item.

**Flags**: IRW

---
## Attr: TextAreaItem.height

### Description
Default height of this item

Note that when item is rendered as read-only with `readOnlyDisplay` as "static" the property [FormItem.staticHeight](FormItem.md#attr-formitemstaticheight) is used instead.

### Groups

- appearance

**Flags**: IRW

---
## Attr: TextAreaItem.width

### Description
default width of this item

### Groups

- appearance

**Flags**: IRW

---
## Attr: TextAreaItem.enforceLength

### Description
If a [TextAreaItem.length](#attr-textareaitemlength) is specified for this item, should user input be limited to the specified length? If set to true, user input and values passed to [setValue()](FormItem.md#method-formitemsetvalue) will be trimmed to the specified length. Otherwise values exceeding the specified length will raise an error on validation.

Note that having this value set to true limits user interactivity in some ways. For example users would be unable to paste a longer string into the field for editing without seeing it be truncated. Given how text areas are typically used to edit longer values than non-wrapping [TextItem](TextItem.md#class-textitem)s, this value is false by default for textAreaItems.

**Flags**: IRW

---
## Attr: TextAreaItem.emptyStringValue

### Description
How should an empty string entered by the user be stored? This value is typically set to `null` or `""`.

Note that a call to [setValue(null)](FormItem.md#method-formitemsetvalue) or [setValue("")](FormItem.md#method-formitemsetvalue) automatically updates this property to ensure that "empty" values are stored in a consistent format.

### Groups

- formValues

**Flags**: IRW

---
## Attr: TextAreaItem.staticHeight

### Description
Height of the FormItem when `canEdit` is false and `readOnlyDisplay` is "static". The normal [TextAreaItem.height](#attr-textareaitemheight) is used if this property is not set.

### Groups

- formLayout

### See Also

- [TextAreaItem.height](#attr-textareaitemheight)

**Flags**: IR

---
## Attr: TextAreaItem.iconVAlign

### Description
Align icons with the top edge of text area icons by default.

### Groups

- formIcons

**Flags**: IR

---
## Attr: TextAreaItem.usePlaceholderForHint

### Description
If [showing the hint in field](#attr-textareaitemshowhintinfield) and if supported by the browser, should the HTML5 [`placeholder` attribute](http://www.whatwg.org/specs/web-apps/current-work/multipage/forms.html#attr-input-placeholder) be used to display the hint within the field? If set to `false`, then use of the `placeholder` attribute is disabled and an alternative technique to display the hint in-field is used instead.

The HTML5 `placeholder` attribute is supported in the following major browsers:

*   Chrome 4+
*   Firefox 4+
*   Internet Explorer 10+
*   Safari 5+
*   Opera 11.50+
*   Android 2.1+ `WebView` (used by the stock Browser app and when [packaging with PhoneGap](../kb_topics/phonegapIntegration.md#kb-topic-integration-with-phonegap))
*   Mobile Safari for iOS 3.2+

In browsers other than the above, in-field hints are implemented via a different technique.

Note that placeholder behavior is known to differ in Internet Explorer and certain old versions of the above browsers due to a recent change in the HTML5 specification regarding the `placeholder` attribute. Under the old rules, the placeholder is cleared when the element is focused. In the latest HTML5 spec as published by WHATWG, the placeholder is still displayed when the element is focused as long as the value is an empty string.

#### Styling the placeholder
While there isn't a standard way to style the placeholder text, Chrome, Firefox, Internet Explorer, and Safari provide vendor-prefixed pseudo-classes and/or pseudo-elements that can be used in CSS selectors:

| Browser | Pseudo-class or pseudo-element |
|---|---|
| Chrome, Safari | ::-webkit-input-placeholder |
| Firefox 4 - 18 | :-moz-placeholder |
| Firefox 19+ | ::-moz-placeholder |
| Internet Explorer | :-ms-input-placeholder |

Note that unlike other browsers, Firefox 19+ applies opacity:0.4 to the placeholder text. See [Bug 556145 - Placeholder text default style should use opacity instead of GrayText](https://bugzilla.mozilla.org/show_bug.cgi?id=556145)

Because browsers are required to ignore the entire rule if a selector is invalid, separate rules are needed for each browser. For example:

```
::-webkit-input-placeholder {
    color: blue;
    opacity: 1;
}
:-moz-placeholder {
    color: blue;
    opacity: 1;
}
::-moz-placeholder {
    color: blue;
    opacity: 1;
}
:-ms-input-placeholder {
    color: blue;
    opacity: 1;
}
```

If using [Sass](http://sass-lang.com), it may be useful to utilize Sass' [parent selector feature](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#parent-selector). For example:

```
.myCustomItem,
.myCustomItemRTL,
.myCustomItemDisabled,
.myCustomItemDisabledRTL,
.myCustomItemError,
.myCustomItemErrorRTL,
.myCustomItemFocused,
.myCustomItemFocusedRTL,
.myCustomItemHint,
.myCustomItemHintRTL,
.myCustomItemDisabledHint,
.myCustomItemDisabledHintRTL {
    // ...

    &::-webkit-input-placeholder {
        color: blue;
        opacity: 1;
    }
    &:-moz-placeholder {
        color: blue;
        opacity: 1;
    }
    &::-moz-placeholder {
        color: blue;
        opacity: 1;
    }
    &:-ms-input-placeholder {
        color: blue;
        opacity: 1;
    }
}
```

If using [Compass](http://compass-style.org), the [`input-placeholder` mixin](http://compass-style.org/reference/compass/css3/user_interface/#mixin-input-placeholder) that was added in version 1.0 can further simplify the code to style the placeholder text For example:

```
.myCustomItem,
.myCustomItemRTL,
.myCustomItemDisabled,
.myCustomItemDisabledRTL,
.myCustomItemError,
.myCustomItemErrorRTL,
.myCustomItemFocused,
.myCustomItemFocusedRTL,
.myCustomItemHint,
.myCustomItemHintRTL,
.myCustomItemDisabledHint,
.myCustomItemDisabledHintRTL {
    // ...

    @include input-placeholder {
        color: blue;
        opacity: 1;
    }
}
```
#### Accessibility concerns
The HTML5 specification notes that a placeholder should not be used as a replacement for a title. The placeholder is intended to be a _short_ hint that assists the user who is entering a value into the empty field. The placeholder can be mistaken by some users for a pre-filled value, particularly in Internet Explorer because the same color is used, and the placeholder text color may provide insufficient contrast, particularly in Firefox 19+ because of the default 0.4 opacity. Furthermore, not having a title reduces the hit area available for setting focus on the item.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)

**Flags**: IRA

---
## Attr: TextAreaItem.showHintInField

### Description
If [showing a hint for this form item](FormItem.md#attr-formitemshowhint), should the hint be shown within the field?

Unless the HTML5 `placeholder` attribute is used to display the hint (see [TextAreaItem.usePlaceholderForHint](#attr-textareaitemuseplaceholderforhint)), the value of the `<input>` element for this item will be set to the hint whenever this item is not focused. Also, when displaying the hint, the CSS style of the data element will be set to the [textBoxStyle](TextItem.md#attr-textitemtextboxstyle) with the suffix "Hint" appended to it; or, if the item is disabled, the suffix "DisabledHint" will be used. In [RTL mode](Page.md#classmethod-pageisrtl) when [showRTL](FormItem.md#attr-formitemshowrtl) is `true`, an additional "RTL" suffix will be appended; i.e. the CSS style of the data element when the hint is displayed will be the `textBoxStyle` plus "HintRTL" or "DisabledHintRTL".

To change this attribute after being drawn, it is necessary to call [FormItem.redraw](FormItem.md#method-formitemredraw) or redraw the form.

#### Styling the in-field hint
The in-field hint can be styled with CSS for the `textBoxStyle` + "Hint" / "HintRTL" / "DisabledHint" / "DisabledHintRTL" styles. For example, if this item's `textBoxStyle` is set to "mySpecialItem", then changing the hint color to blue can be accomplished with the following CSS:
```
.mySpecialItemHint,
.mySpecialItemHintRTL,
.mySpecialItemDisabledHint,
.mySpecialItemDisabledHintRTL {
    color: blue;
}
```

In [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode), this property will be defaulted true if left unset.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)
- [TextAreaItem.usePlaceholderForHint](#attr-textareaitemuseplaceholderforhint)

**Flags**: IRW

---
## Attr: TextAreaItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: TextAreaItem.changeOnKeypress

### Description
Should this form item fire its [change](FormItem.md#method-formitemchange) handler (and store its value in the form) on every keypress? Set to `false` to suppress the 'change' handler firing (and the value stored) on every keypress.

Note: If `false`, the value returned by [getValue](FormItem.md#method-formitemgetvalue) will not reflect the value displayed in the form item element as long as focus is in the form item element.

### Groups

- eventHandling
- values

**Flags**: IRW

---
## Attr: TextAreaItem.browserAutoCorrect

### Description
In Mobile Safari, should automatic correction be offered for text in the item's text box? If `null`, then Mobile Safari determines automatically whether to enable autocorrect.

When enabled, Mobile Safari displays "autocorrect bubbles" to suggest automatic corrections:  
![Screenshot of Mobile Safari suggesting "On my way!" to replace "omw"](data:image/png;base64,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)

**Flags**: IRA

---
## Attr: TextAreaItem.escapeHTML

### Description
By default HTML characters will be escaped when [canEdit](FormItem.md#attr-formitemcanedit) is false and [readOnlyDisplay](FormItem.md#attr-formitemreadonlydisplay) is "static", so that the raw value of the field (for example `"`<b>`AAA`</b>`"`) is displayed to the user rather than the interpreted HTML (for example `"**AAA**"`). Setting `escapeHTML` false will instead force HTML values in a textAreaItem to be interpreted by the browser in that situation.

### Groups

- appearance

**Flags**: IRW

---
## Attr: TextAreaItem.minHeight

### Description
Minimum valid height for this TextAreaItem in px. If the specified [TextAreaItem.height](#attr-textareaitemheight) is less than this value, the text area will still render at this height.

**Flags**: IRW

---
## Attr: TextAreaItem.length

### Description
If set, maximum number of characters for this field. If [TextAreaItem.enforceLength](#attr-textareaitemenforcelength) is set to true, user input will be limited to this value, and values exceeding this length passed to [setValue()](FormItem.md#method-formitemsetvalue) will be trimmed. Otherwise values exceeding the specified length will raise an error on validation.

See also [DataSourceField.length](DataSourceField.md#attr-datasourcefieldlength).

### Groups

- validation

**Flags**: IRW

---
## Attr: TextAreaItem.printFullText

### Description
When generating a print-view of the component containing this TextArea, should the form item expand to accommodate its value? If set to false the text box not expand to fit its content in the print view, instead showing exactly as it does in the live form, possibly with scrollbars.

### Groups

- printing

**Flags**: IRW

---
## Attr: TextAreaItem.browserAutoCapitalize

### Description
—

**Flags**: IRA

---
## Attr: TextAreaItem.showInputElement

### Description
When set to false, prevents this item's input element from being written into the DOM. If there are [valueIcons](FormItem.md#attr-formitemvalueicons) or a [picker icon](FormItem.md#attr-formitemshowpickericon), these are displayed as normal, and the item will auto-sizing to that content if its [width](FormItem.md#attr-formitemwidth) is set to null.

**Flags**: IRWA

---
## Method: TextAreaItem.transformPastedValue

### Description
Notification fired in response to a clipboard "paste" event on freeform text items, giving developers an opportunity to reformat the pasted text. The `pastedValue` argument contains the text pasted from the clipboard. This method should return the text value to actually insert into the input element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item into which the user pasted a value |
| form | [DynamicForm](#type-dynamicform) | false | — | Pointer to the item's form |
| pastedValue | [String](#type-string) | false | — | Pasted text value |

### Returns

`[String](#type-string)` — Reformatted version of the pasted text.

### Groups

- eventHandling

---
## Method: TextAreaItem.selectValue

### Description
Put focus in this item and select the entire value. Only applies to text based items

---
## Method: TextAreaItem.setSelectionRange

### Description
Puts focus into this form item and selects characters between the given indices. Only applies to drawn text based items.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [int](../main.md#type-int) | false | — | selection starting character index |
| end | [int](../main.md#type-int) | false | — | end of selection character index |

---
## Method: TextAreaItem.deselectValue

### Description
If this item currently has focus, clear the current selection. leaving focus in the item. Has no effect if the item is undrawn or unfocused. Only applies to text-based items.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [Boolean](#type-boolean) | true | — | By default the text insertion cursor will be moved to the end of the current value - pass in this parameter to move to the start instead |

---
## Method: TextAreaItem.getEnteredValue

### Description
Returns the raw text value that currently appears in the text field, which can differ from [FormItem.getValue](FormItem.md#method-formitemgetvalue) in various cases - for example:

*   for items that constrain the value range, such as a [DateItem](DateItem.md#class-dateitem) with [enforceDate](DateItem.md#attr-dateitemenforcedate):true, or a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) with [addUnknownValues](ComboBoxItem.md#attr-comboboxitemaddunknownvalues):false
*   for items with a defined valueMap or edit value formatter and parser functions which converts display value to data value
*   while the item has focus if [changeOnKeypress](TextItem.md#attr-textitemchangeonkeypress) is false

### Returns

`[String](#type-string)` — current entered value

---
## Method: TextAreaItem.getSelectionRange

### Description
For text-based items, this method returns the indices of the start/end of the current selection if the item currently has the focus. In browsers other than Internet Explorer 6-9, if this item does not have focus, then this method returns the indices of the start/end of the selection the last time that this item had focus. In IE 6-9, returns null if the item does not have focus.

In all browsers, clicking anywhere outside of the item causes the item to lose focus; hence, in IE 6-9, this method will not work in other components' event handlers for certain events. For example, within the [click()](Canvas.md#method-canvasclick) handler of a button, this item will have already lost focus, so in IE 6-9, this method will return null if called within the button's click() handler. One cross-browser solution to this issue is to save the selection range for later in a [mouseDown()](Canvas.md#method-canvasmousedown) or [mouseOver()](Canvas.md#method-canvasmouseover) handler.

Notes:

*   In browsers other than IE 6-9, calling [setValue()](FormItem.md#method-formitemsetvalue) or otherwise changing the [entered value](#method-textareaitemgetenteredvalue) invalidates the past selection range.
*   The returned indices are indices within the entered value rather than the item's value as returned by [getValue()](FormItem.md#method-formitemgetvalue). The distinction is particularly important for [TextAreaItem](#class-textareaitem)s because browsers normalize the line endings in the ``<textarea>`` element's value. Internet Explorer 6, 7, and 8 convert line endings to "\\r\\n" while other browsers convert line endings to "\\n" [as specified by the HTML5 standard](http://www.w3.org/TR/html5/forms.html#concept-textarea-api-value).

### Returns

`[Array of int](#type-array-of-int)` — 2 element array showing character index of the current or past selection's start and end points within this item's [entered value](TextItem.md#method-textitemgetenteredvalue). In IE 6-9, returns null if the item does not have focus.

---
