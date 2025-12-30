# RichTextEditor Documentation

[← Back to API Index](../reference.md)

---

## Class: RichTextEditor

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
RichTextEditing component. Provides a rich-text editing area along with UI for executing rich-text commands on selected content.

The HTML generated from this component may vary by browser, and, as with any HTML value created on the client, we recommend values be sanitized on the server before storing and displaying to other users.

---
## Attr: RichTextEditor.justifyPrompt

### Description
The prompt for the built-in [justify](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.moveFocusOnTab

### Description
If the user presses the "Tab" key, should focus be taken from this editor? If set to `false` a "Tab" keypress will cause a Tab character to be inserted into the text, and focus will be left in the edit area.

**Flags**: IRW

---
## Attr: RichTextEditor.toolbar

### Description
Layout used to contain each of the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups).

**Flags**: R

---
## Attr: RichTextEditor.backgroundColorPrompt

### Description
The prompt for the built-in [backgroundColor](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.alignCenterPrompt

### Description
The prompt for the built-in [alignCenter](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.editAreaBackgroundColor

### Description
Background color for the [edit canvas](#attr-richtexteditoreditarea).

**Flags**: IR

---
## Attr: RichTextEditor.fontSelectorItem

### Description
The [AutoChild](../reference.md#type-autochild) [SelectItem](SelectItem.md#class-selectitem) used for choosing the font to apply to the current selection.

**Flags**: IR

---
## Attr: RichTextEditor.alignLeftPrompt

### Description
The prompt for the built-in [alignLeft](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.pasteSelectionPrompt

### Description
The prompt for the built-in [pasteSelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.colorPrompt

### Description
The prompt for the built-in [color](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.toolbarBackgroundColor

### Description
The background color for the toolbar.

**Flags**: IR

---
## Attr: RichTextEditor.strikethroughSelectionPrompt

### Description
The prompt for the built-in [strikethroughSelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.fontSizes

### Description
ValueMap of css font size property values to font size titles to display in the font size selector if `"fontSizeSelector"` is included in [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups). Default value for this attribute:  
`{   "1": "1 (8 pt)",   "2": "2 (10 pt)",   "3": "3 (12 pt)",   "4": "4 (14 pt)",   "5": "5 (18 pt)",   "6": "6 (24 pt)",   "7": "7 (36 pt)"}`

**Flags**: IRA

---
## Attr: RichTextEditor.bulletControls

### Description
Default HTML list control group. Consists of an array of [ControlName](../reference.md#type-controlname)s and/or [Canvas](Canvas.md#class-canvas) instances. To display this group of controls for some RichTextEditor, include `"bulletControls"` in the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups) array.

**Flags**: IRA

---
## Attr: RichTextEditor.fontSelectorPrompt

### Description
The prompt for the built-in [font selector](#attr-richtexteditorfontselectoritem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.toolArea

### Description
Layout used to contain all of the [toolbar](#attr-richtexteditortoolbar) AutoChildren that contain the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups).

**Flags**: R

---
## Attr: RichTextEditor.listPropertiesWarningText

### Description
The warning message displayed in a dialog when a user tries to configure a list without first putting the cursor in an appropriate place.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.formatControls

### Description
Default text formatting control group. Consists of an array of [ControlName](../reference.md#type-controlname)s and/or [Canvas](Canvas.md#class-canvas) instances. To display this group of controls for some RichTextEditor, include `"formatControls"` in the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups) array.

**Flags**: IRA

---
## Attr: RichTextEditor.copySelectionPrompt

### Description
The prompt for the built-in [copySelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.editArea

### Description
The edit canvas created automatically for this RichTextEditor.

**Flags**: R

---
## Attr: RichTextEditor.indentPrompt

### Description
The prompt for the built-in [indent](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.controlGroups

### Description
An array of control groups specifying which groups of controls should be included in the editor tool area. The values of this array may be the name of a control group such as one of the [StandardControlGroup](../reference.md#type-standardcontrolgroup)s, a [Canvas](Canvas.md#class-canvas), or the special string "break" which causes the subsequent control groups to continue onto a new line.

For each control group name, this\[controlGroupName\] should be defined as an array of [ControlName](../reference.md#type-controlname)s or Canvas instances. This allows the controls of a control group to be customized.

**Flags**: IRA

---
## Attr: RichTextEditor.colorControls

### Description
Control group for modifying text color / background color. Consists of an array of [ControlName](../reference.md#type-controlname)s and/or [Canvas](Canvas.md#class-canvas) instances. To display this group of controls for some RichTextEditor, include `"formatControls"` in the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups) array.

**Flags**: IRA

---
## Attr: RichTextEditor.listPropertiesPrompt

### Description
The prompt for the built-in [listProperties](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.fontSizeSelectorPrompt

### Description
The prompt for the built-in [font-size selector](#attr-richtexteditorfontsizeselectoritem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.underlineSelectionPrompt

### Description
The prompt for the built-in [underlineSelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.alignRightPrompt

### Description
The prompt for the built-in [alignRight](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.fontControls

### Description
Default font control group. Consists of an array of [ControlName](../reference.md#type-controlname)s and/or [Canvas](Canvas.md#class-canvas) instances. To display this group of controls for some RichTextEditor, include `"fontControls"` in the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups) array.

**Flags**: IRA

---
## Attr: RichTextEditor.italicSelectionPrompt

### Description
The prompt for the built-in [italicSelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.cutSelectionPrompt

### Description
The prompt for the built-in [cutSelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.styleControls

### Description
Default text styling control group. Consists of an array of [ControlName](../reference.md#type-controlname)s and/or [Canvas](Canvas.md#class-canvas) instances. To display this group of controls for some RichTextEditor, include `"styleControls"` in the [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups) array.

**Flags**: IRA

---
## Attr: RichTextEditor.orderedListPrompt

### Description
The prompt for the built-in [orderedList](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.listPropertiesDialog

### Description
Dialog shown when the ["listProperties" control](../reference.md#type-controlname) is pressed. Provides options for the user to control formatting of lists.

**Flags**: R

---
## Attr: RichTextEditor.value

### Description
Initial value for the edit area. Use `getValue()` and `setValue()` to update at runtime.

**Flags**: IRW

---
## Attr: RichTextEditor.useDesignMode

### Description
Should this editor use a separate IFRAME with special cross-browser support for editing HTML content? By default, the value is auto-detected according to browser details. If set to false, the editor falls back to normal browser contentEditable behavior, which may differ between browsers.

**Flags**: IRA

---
## Attr: RichTextEditor.styleWithCSS

### Description
When true, applies style attributes in markup instead of presentation elements.

**Flags**: IRA

---
## Attr: RichTextEditor.outdentPrompt

### Description
The prompt for the built-in [outdent](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.boldSelectionPrompt

### Description
The prompt for the built-in [boldSelection](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.fontSizeSelectorItem

### Description
The [AutoChild](../reference.md#type-autochild) [SelectItem](SelectItem.md#class-selectitem) used for choosing the font-size to apply to the current selection.

**Flags**: IR

---
## Attr: RichTextEditor.unorderedListPrompt

### Description
The prompt for the built-in [unorderedList](../reference.md#type-controlname) control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: RichTextEditor.fontNames

### Description
ValueMap of css fontName properties to font name titles to display in the font selector if `"fontSelector"` is included in [RichTextEditor.controlGroups](#attr-richtexteditorcontrolgroups) for this editor. Default value for this attribute:  
`{   "arial,helvetica,sans-serif": "Arial",   'courier new,courier,monospace': "Courier New",   'georgia,times new roman,times,serif': "Georgia",   'tahoma,arial,helvetica,sans-serif': "Tahoma",   'times new roman,times,serif': "Times New Roman",   'verdana,arial,helvetica,sans-serif': "Verdana",   "impact": "Impact"}`

**Flags**: IRA

---
## Method: RichTextEditor.setValue

### Description
Updates the current value of the edit area.

---
## Method: RichTextEditor.richEditorSupported

### Description
Does this browser support the full RichTextEditor feature set. Returns false for browsers in which some features are not natively supported (Safari before version 3.1 and Opera before version 9.50).

### Returns

`[Boolean](#type-boolean)` — false if this browser doesn't fully support RichTextEditing

---
## Method: RichTextEditor.getValue

### Description
Retrieves the current value of the edit area.

---
## Method: RichTextEditor.setMoveFocusOnTab

### Description
Setter for [RichTextEditor.moveFocusOnTab](#attr-richtexteditormovefocusontab).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| moveFocusOnTab | [boolean](../reference.md#type-boolean) | false | — | new value for moveFocusOnTab |

---
## Method: RichTextEditor.doWarn

### Description
Display a warning if Rich Text Editing is not fully supported in this browser. Default behavior logs a warning to the developer console - Override this if a user-visible warning is required

---
