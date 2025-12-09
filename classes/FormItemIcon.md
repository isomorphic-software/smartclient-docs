# FormItemIcon Documentation

[← Back to API Index](../reference.md)

---

## Attr: FormItemIcon.neverDisable

### Description
If `icon.neverDisable` is true, when this form item is disabled, the icon will remain enabled. Note that disabling the entire form will disable all items, together with their icons including those marked as neverDisable - this property only has an effect if the form is enabled and a specific item is disabled within it.

If this property is true, the icons will also remain enabled if a form item is marked as [canEdit:false](FormItem.md#attr-formitemcanedit). For finer grained control over whether icons are enabled for read-only icons see [FormItem.disableIconsOnReadOnly](FormItem.md#attr-formitemdisableiconsonreadonly) and [FormItemIcon.disableOnReadOnly](#attr-formitemicondisableonreadonly)

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItemIcon.text

### Description
As an alternative to displaying an image, an [inline](#attr-formitemiconinline) `FormItemIcon` can display a string of HTML where the icon's image would have appeared. This enables advanced customizations such as using text, icon font symbols, Unicode dingbats and emoji, and/or SVG in place of an image.

Setting an inline icon's text property will cause the HTML to be used instead of an image, as long as the browser and form item support inline icons.

This property only has an effect on inline icons. If the inline property is false, or the browser or form item does not support inline icons, then the image specified by [FormItemIcon.src](#attr-formitemiconsrc) (or the form item's [defaultIconSrc](FormItem.md#attr-formitemdefaulticonsrc)) will be used.

Typically, the HTML is styled via [FormItemIcon.baseStyle](#attr-formitemiconbasestyle).

Auto-sizing of the HTML is not supported; the HTML will be clipped to the icon's [width](#attr-formitemiconwidth) and [height](#attr-formitemiconheight).

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItemIcon.inline

### Description
When set, this icon is rendered inside the [textBox](FormItem.md#attr-formitemtextboxstyle) area of the `FormItem` (where input occurs in a [TextItem](TextItem.md#class-textitem), [TextAreaItem](TextAreaItem.md#class-textareaitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)) as opposed to as a trailing icon.

Use [inlineIconAlign](#attr-formitemiconinlineiconalign) to control alignment of the icon. Multiple icons can be inlined on both the left and right side of the `textBox` area. [hspace](#attr-formitemiconhspace) is honored for spacing between multiple adjacent icons.

Inline icons are not supported in Internet Explorer 6, or when the `FormItem` is not a `TextItem`, `TextAreaItem` or `ComboBoxItem`. When unsupported, the icon will fall back to non-inline mode.

The [picker icon](FormItem.md#attr-formitemshowpickericon), if any, cannot be inlined.

As an alternative to displaying an image, an inline icon may display a string of HTML instead. See [FormItemIcon.text](#attr-formitemicontext).

**Flags**: IR

---
## Attr: FormItemIcon.baseStyle

### Description
Base CSS style. If set, as the component changes state and/or is focused, suffixes will be added to the base style. Possible suffixes include "Over" if the user mouses over the icon and [this.showOver](#attr-formitemiconshowover) is true, "Disabled" if the icon is disabled, and "Focused". In addition, if [showRTL](#attr-formitemiconshowrtl) is enabled, then an "RTL" suffix will be added.

**Flags**: IRWA

---
## Attr: FormItemIcon.showError

### Description
Whether this icon's image and/or [baseStyle](#attr-formitemiconbasestyle) should change to an appropriate _Error_ state when the item has validation errors.

When set to true and the item has errors, appends _Error_ to the image src and/or `baseStyle`. If other physical states apply, such as _Over_, that state is also appended, reulting in a suffix of, for example, _ErrorOver_.

### Groups

- formIcons

### See Also

- [FormItem.showOverIcons](FormItem.md#attr-formitemshowovericons)

**Flags**: IRWA

---
## Attr: FormItemIcon.showRTL

### Description
Should this icon's [src](#attr-formitemiconsrc) and/or [baseStyle](#attr-formitemiconbasestyle) switch to the appropriate RTL value when the FormItem is in RTL mode? If true, then the image URL for all states will have "\_rtl" added before the extension. Also, if baseStyle is set, all style names will have an "RTL" suffix. This should only be enabled if RTL media is available.

For example, if an icon's src is "\[SKINIMG\]formItemIcons/myFormIcon.png" and the baseStyle is "myFormIcon", then in the "Down" state, SmartClient will use "\[SKINIMG\]formItemIcons/myFormIcon\_Down\_rtl.png" for the image source and "myFormIconDownRTL" for the style name.

### Groups

- RTL
- formIcons

**Flags**: IRA

---
## Attr: FormItemIcon.cursor

### Description
Specifies the cursor image to display when the mouse pointer is over this icon. It corresponds to the CSS cursor attribute. See Cursor type for different cursors.

See also [FormItemIcon.disabledCursor](#attr-formitemicondisabledcursor).

### Groups

- cues

**Flags**: IRWA

---
## Attr: FormItemIcon.src

### Description
If set, this property determines this icon's image source. If unset the form item's `defaultIconSrc` property will be used instead.  
As with `defaultIconSrc` this URL will be modified by adding "\_Over" or "\_Disabled" if appropriate to show the icon's over or disabled state. If [showRTL](#attr-formitemiconshowrtl) is enabled, then "\_rtl" will be added to the source URL before the extension.

The special value "blank" means that no image will be shown for this icon. This is particularly useful together with [FormItemIcon.baseStyle](#attr-formitemiconbasestyle) to implement spriting of the different icon states.

For an [inline](#attr-formitemiconinline) `FormItemIcon`, [text](#attr-formitemicontext) may be specified to show a string of HTML instead of an image.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string.

### Groups

- formIcons

### See Also

- [FormItem.defaultIconSrc](FormItem.md#attr-formitemdefaulticonsrc)

**Flags**: IRW

---
## Attr: FormItemIcon.showDisabledOnFocus

### Description
If show-on-focus behavior is enabled for this icon via [FormItemIcon.showOnFocus](#attr-formitemiconshowonfocus) or related properties at the item level, and this icon is marked as disabled, should it be shown on focus? If unset, will be derived from the [FormItem.showDisabledIconsOnFocus](FormItem.md#attr-formitemshowdisablediconsonfocus) or [FormItem.showDisabledPickerIconOnFocus](FormItem.md#attr-formitemshowdisabledpickericononfocus) settings.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItemIcon.showFocused

### Description
Should this icon's image and/or [baseStyle](#attr-formitemiconbasestyle) switch to the appropriate "Focused" value when the user puts focus on the form item or icon?

### Groups

- formIcons

### See Also

- [FormItem.showFocusedIcons](FormItem.md#attr-formitemshowfocusedicons)
- [FormItemIcon.showFocusedWithItem](#attr-formitemiconshowfocusedwithitem)

**Flags**: IRWA

---
## Attr: FormItemIcon.visibleWhen

### Description
Criteria to be evaluated to determine whether this icon should be visible.

Criteria are evaluated against the ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','form\\'s current values')} as well as the current [rule context](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated every time form values or the rule context changes, whether by end user action or by programmatic calls.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

Note: A FormItemIcon using visibleWhen must have a [name](FormItem.md#attr-formitemname) defined on its FormItem.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: FormItemIcon.tabIndex

### Description
TabIndex for this formItemIcon.

Set to -1 to remove the icon from the tab order, but be cautious doing so: if the icon triggers important application functionality that cannot otherwise be accessed via the keyboard, it would be a violation of accessibility standard to remove the icon from the tab order.

Any usage other than setting to -1 is extremely advanced in the same way as using [FormItem.globalTabIndex](FormItem.md#attr-formitemglobaltabindex).

### Groups

- formIcons

**Flags**: IRA

---
## Attr: FormItemIcon.showOverWhen

### Description
If [FormItemIcon.showOver](#attr-formitemiconshowover) or [FormItem.showOverIcons](FormItem.md#attr-formitemshowovericons) is true, this property may be set to customize when the 'over' styling is applied to the item. If unset, rollover styling will be applied when the user is over the icon only.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItemIcon.prompt

### Description
If set, this property will be displayed as a prompt (and tooltip text) for this form item icon.

If unset the form item's `iconPrompt` property will be used instead.

Has no effect when [FormItem.canHover](FormItem.md#attr-formitemcanhover) is set to false.

### Groups

- formIcons

### See Also

- [FormItem.canHover](FormItem.md#attr-formitemcanhover)
- [FormItem.iconPrompt](FormItem.md#attr-formitemiconprompt)

**Flags**: IRWA

---
## Attr: FormItemIcon.hspace

### Description
If set, this property determines the number of pixels space to be displayed on the left of this form item icon, or for [inline](#attr-formitemiconinline) icons whose [inlineIconAlign](#attr-formitemiconinlineiconalign) is `"left"`, on the right of this form item icon. Must be non-negative. If unset, the form item's [iconHSpace](FormItem.md#attr-formitemiconhspace) will be used instead.

### Groups

- formIcons

**Flags**: IR

---
## Attr: FormItemIcon.enableWhen

### Description
Criteria to be evaluated to determine whether this icon should appear enabled.

Criteria are evaluated against the ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','form\\'s current values')} as well as the current [rule context](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated every time form values or the rule context changes, whether by end user action or by programmatic calls.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

Note: A FormItemIcon using enableWhen must have a [name](FormItem.md#attr-formitemname) defined on its FormItem.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: FormItemIcon.inlineIconAlign

### Description
Horizontal alignment for icons marked [inline](#attr-formitemiconinline).

By default, the first icon that specifies inline is aligned left, and the second and all subsequent icons to the right. `"center"` alignment is invalid and will be ignored.

In RTL mode, the alignment is automatically mirrored; `inlineIconAlign:"left"` results in the icon being placed on the right and `inlineIconAlign:"right"` results in the icon being placed on the left.

**Flags**: IR

---
## Attr: FormItemIcon.width

### Description
If set, this property determines the width of this icon in px. If unset the form item's `iconWidth` property will be used instead.

### Groups

- formIcons

### See Also

- [FormItem.iconWidth](FormItem.md#attr-formitemiconwidth)

**Flags**: IRW

---
## Attr: FormItemIcon.disabled

### Description
Whether this icon is disabled. Can be updated at runtime via the [FormItem.setIconDisabled](FormItem.md#method-formitemseticondisabled) method. Note that if the formItem containing this icon is disabled, the icon will behave in a disabled manner regardless of the setting of the icon.disabled property.

### Groups

- appearance

### See Also

- [FormItem.setIconDisabled](FormItem.md#method-formitemseticondisabled)

**Flags**: IRW

---
## Attr: FormItemIcon.disabledCursor

### Description
Specifies the cursor image to display when the mouse pointer is over this icon if this icon is disabled. It corresponds to the CSS cursor attribute. See Cursor type for different cursors.

### Groups

- cues

**Flags**: IRWA

---
## Attr: FormItemIcon.height

### Description
If set, this property determines the height of this icon in px. If unset the form item's `iconHeight` property will be used instead.

### Groups

- formIcons

### See Also

- [FormItem.iconHeight](FormItem.md#attr-formitemiconheight)

**Flags**: IRW

---
## Attr: FormItemIcon.iconPlacement

### Description
For PickList items with [PickListItemIconPlacement](../reference.md#type-picklistitemiconplacement) set such that the pickList does not render near-origin, should this icon be rendered inline within the formItem itself, or within the [ComboBoxItem.pickerNavigationBar](ComboBoxItem.md#attr-comboboxitempickernavigationbar).

If not explicitly specified at the icon level, this will be picked up from [PickList.iconPlacement](PickList.md#attr-picklisticonplacement).

For mobile browsing with limited available screen space, icons rendered in the navigation bar may be easier for the user to interact with.

**Flags**: IR

---
## Attr: FormItemIcon.showOnFocus

### Description
Show this icon when its item gets focus, and hide it when it loses focus. If non-null, overrides the default behavior specified by [FormItem.showIconsOnFocus](FormItem.md#attr-formitemshowiconsonfocus) or [FormItem.showPickerIconOnFocus](FormItem.md#attr-formitemshowpickericononfocus), as appropriate. This feature allows space to be saved in the form for items not being interacted with, and helps draw attention to the item currently in focus.

### Groups

- formIcons

### See Also

- [FormItem.setIconShowOnFocus](FormItem.md#method-formitemseticonshowonfocus)

**Flags**: IRWA

---
## Attr: FormItemIcon.disableOnReadOnly

### Description
If [FormItem.canEdit](FormItem.md#attr-formitemcanedit) is set to false, should this icon be disabled. If unset this is determined by [FormItem.disableIconsOnReadOnly](FormItem.md#attr-formitemdisableiconsonreadonly). Note that if [FormItemIcon.neverDisable](#attr-formitemiconneverdisable) is set to true, the icons will be rendered enabled regardless of this setting and whether the item is editable.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItemIcon.showFocusedWithItem

### Description
If this icon will be updated to show focus (see [FormItemIcon.showFocused](#attr-formitemiconshowfocused), [FormItem.showFocusedIcons](FormItem.md#attr-formitemshowfocusedicons)), this property governs whether the focused state should be shown when the item as a whole receives focus or just if the icon receives focus. If this property is unset, default behavior is to show focused state when the item receives focus.

### Groups

- formIcons

### See Also

- [FormItem.showFocusedIcons](FormItem.md#attr-formitemshowfocusedicons)
- [FormItemIcon.showFocused](#attr-formitemiconshowfocused)

**Flags**: IRWA

---
## Attr: FormItemIcon.canFocus

### Description
Set to false to suppress all focus features for this icon. Clicking the icon will not apply focus to the icon or to the form item.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItemIcon.name

### Description
Identifier for this form item icon. This identifier (if set) should be unique within this form item and may be used to get a pointer to the icon object via [FormItem.getIcon](FormItem.md#method-formitemgeticon).

**Flags**: IR

---
## Attr: FormItemIcon.showOver

### Description
Should this icon's image and/or [baseStyle](#attr-formitemiconbasestyle) switch to the appropriate "Over" value when the user rolls over or focuses on the icon?

Note if [FormItem.showOver](FormItem.md#attr-formitemshowover) is true and [FormItemIcon.showOverWhen](#attr-formitemiconshowoverwhen) is set to "textBox", this icon will show over state when the user rolls over the text box (or control table, if visible) for the item. This is most commonly used for [inline](#attr-formitemiconinline) icons.

### Groups

- formIcons

### See Also

- [FormItem.showOverIcons](FormItem.md#attr-formitemshowovericons)

**Flags**: IRWA

---
## Attr: FormItemIcon.extraCSS

### Description
Additional CSS-text that overrides the icon's [FormItemIcon.baseStyle](#attr-formitemiconbasestyle), applying arbitrary styling to the icon's outer element.

This is an advanced attribute - while it can be used to modify many properties, such as colors, font-style and border-radius, it should not be used to modify any property that may affect element-size, such as height, padding/margin or overflow.

**Flags**: IRA

---
## Method: FormItemIcon.click

### Description
Click handler for this icon.

Return false to cancel this event. If this event is not cancelled by the icon-level click handler, it may also be handled at the FormItem level via [FormItem.pickerIconClick](FormItem.md#method-formitempickericonclick) \[for the picker icon only\], and then [FormItem.iconClick](FormItem.md#method-formitemiconclick)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | The Dynamic Form to which this icon's item belongs. |
| item | [FormItem](#type-formitem) | false | — | The Form Item containing this icon |
| icon | [FormItemIcon](#type-formitemicon) | false | — | A pointer to the form item icon clicked |

### Returns

`[Boolean](#type-boolean)` — Return false to cancel the event.

### Groups

- formIcons

---
## Method: FormItemIcon.keyPress

### Description
StringMethod action to fire when this icon has focus and receives a keypress event. If unset the form item's `iconKeyPress` method will be fired instead (if specified).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | Name of the key pressed |
| character | [Character](#type-character) | false | — | character produced by the keypress |
| form | [DynamicForm](#type-dynamicform) | false | — | The Dynamic Form to which this icon's item belongs. |
| item | [FormItem](#type-formitem) | false | — | The Form Item containing this icon |
| icon | [FormItemIcon](#type-formitemicon) | false | — | A pointer to the form item icon |

### Groups

- formIcons

---
## Method: FormItemIcon.showIf

### Description
If specified, `icon.showIf` will be evaluated when the form item is drawn or redrawn. Return true if the icon should be visible, or false if it should be hidden. Note that if [FormItem.showIcon](FormItem.md#method-formitemshowicon) or [FormItem.hideIcon](FormItem.md#method-formitemhideicon) is called, this method will be overridden.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the DynamicForm in which the icon is embedded |
| item | [FormItem](#type-formitem) | false | — | the item to which this icon is attached. |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true if the icon should be visible, false otherwise.

---
