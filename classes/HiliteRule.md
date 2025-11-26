# HiliteRule Documentation

[← Back to API Index](../reference.md)

---

## Class: HiliteRule

*Inherits from:* [HLayout](../reference.md#class-hlayout)

### Description
A widget for editing the criteria of a single [DataBoundComponent](../reference.md#interface-databoundcomponent) hilite. The default implementation presents a series of [formItems](FormItem.md#class-formitem) for selecting the various elements of a simple criterion and a foreground or background color. To specify more complex criteria, specify both foreground and background colors or to apply the hilite to multiple fields, you can create an [advanced hilite rule](AdvancedHiliteEditor.md#class-advancedhiliteeditor).

_**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](../kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

---
## Attr: HiliteRule.hiliteForm

### Description
AutoChild [DynamicForm](DynamicForm.md#class-dynamicform) displaying the [formItems](FormItem.md#class-formitem) used to specify the hiliting properties of this rule.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteRule.hiliteFormProperties`.

**Flags**: IR

---
## Attr: HiliteRule.removeIconSize

### Description
When set, dictates the size of the [remove button](#attr-hiliteruleremovebutton) shown for this HiliteRule.

**Flags**: IR

---
## Attr: HiliteRule.backgroundColorTitle

### Description
The [title](FormItem.md#attr-formitemtitle) of the 'Background' color picker.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteRule.colorFieldTitle

### Description
The title for the Color picker field.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteRule.clause

### Description
AutoChild [FilterClause](FilterClause.md#class-filterclause) displaying the [formItems](FormItem.md#class-formitem) used to specify the criteria for this HiliteRule.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteRule.clauseProperties`.

**Flags**: IR

---
## Attr: HiliteRule.removeIconBaseStyle

### Description
CSS class to apply to the [remove button](#attr-hiliteruleremovebutton) shown for this HiliteRule.

**Flags**: IR

---
## Attr: HiliteRule.showRemoveButton

### Description
If true, show a [button](#attr-hiliteruleremovebutton) for this HiliteRule, allowing it to be removed.

**Flags**: IR

---
## Attr: HiliteRule.removeButton

### Description
The Hilite removal ImgButton that appears before this Hilite if [HiliteRule.showRemoveButton](#attr-hiliteruleshowremovebutton) is set.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteRule.removeButtonProperties`.

**Flags**: IR

---
## Attr: HiliteRule.removeButtonPrompt

### Description
The hover prompt text for the [remove button](#attr-hiliteruleremovebutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteRule.advancedClauseEditButton

### Description
AutoChild [ImgButton](ImgButton.md#class-imgbutton) displayed by an advanced hilite-rule and used to open it for editing in an [advanced hilite editor](AdvancedHiliteEditor.md#class-advancedhiliteeditor).

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteRule.advancedClauseEditButtonProperties`.

**Flags**: IR

---
## Attr: HiliteRule.iconFieldTitle

### Description
The [title](FormItem.md#attr-formitemtitle) of the 'Icon' picker.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteRule.foregroundColorTitle

### Description
The [title](FormItem.md#attr-formitemtitle) of the 'Text' color picker.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: HiliteRule.advancedClauseLabel

### Description
AutoChild [Label](Label.md#class-label) displaying the human-readable description of an advanced hilite-rule.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `hiliteRule.advancedClauseLabelProperties`.

**Flags**: IR

---
## Method: HiliteRule.remove

### Description
Remove this HiliteRule. Default implementation calls markForDestroy().

---
## Method: HiliteRule.getHilite

### Description
Return the hilite definition being edited, including criteria and hilite properties.

### Returns

`[Hilite](#type-hilite)` — the hilite

---
