# StyleSheetHandler Documentation

[← Back to API Index](../main.md)

---

## Class: StyleSheetHandler

### Description
This class allows developers to create, modify and load/unload custom CSS stylesheets with simple API calls.

---
## Attr: StyleSheetHandler.autoLoad

### Description
When true, this handler will automatically [inject](#method-stylesheethandlerinjectsheet) it's stylesheet into the DOM.

**Flags**: IRW

---
## Attr: StyleSheetHandler.name

### Description
The name for this handler. This value is applied as both the 'id' and 'title' attributes on the handler's [stylesheet](#attr-stylesheethandlerstylesheet).

**Flags**: IR

---
## Attr: StyleSheetHandler.cssText

### Description
A string representation of all the CSS styles in this handler's [StyleSheetHandler.styleSheet](#attr-stylesheethandlerstylesheet).

**Flags**: IRW

---
## Attr: StyleSheetHandler.styleSheet

### Description
A reference to this handler's stylesheet-element in the DOM. This attribute cannot be set - see [injectSheet()](#method-stylesheethandlerinjectsheet) and [unload()](#method-stylesheethandlerunload) for details.

**Flags**: R

---
## Method: StyleSheetHandler.renameClass

### Description
Rename the passed _oldClass_ to _newClass_ in all rules that reference it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldName | [String](#type-string) | false | — | name of the CSS class to rename in the stylesheet |
| newName | [String](#type-string) | false | — | new name for the CSS class |

### Returns

`[boolean](../main.md#type-boolean)` — returns true if a class was renamed, false otherwise

---
## Method: StyleSheetHandler.loaded

### Description
Has this handler's [styleSheet](#attr-stylesheethandlerstylesheet) been loaded into the DOM?

---
## Method: StyleSheetHandler.unload

### Description
Remove this handler's [stylesheet](#attr-stylesheethandlerstylesheet) from the DOM and destroy it.

---
## Method: StyleSheetHandler.setCssText

### Description
Replace the entire CSS in this handler's [stylesheet](#attr-stylesheethandlerstylesheet).

If the stylesheet is already in the DOM, it is first [unloaded](#method-stylesheethandlerunload), the [cssText](#attr-stylesheethandlercsstext) is updated and then the stylesheet is [injected](#method-stylesheethandlerinjectsheet) back into the DOM. Otherwise, the handler's cssText is updated and no further action is taken.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cssText | [String](#type-string) | false | — | complete cssText to apply to the stylesheet |

---
## Method: StyleSheetHandler.modifyClass

### Description
Inject a string of css settings into a single CSS class, via a new rule in this handler's [stylesheet](#attr-stylesheethandlerstylesheet).

The passed 'cssText' should contain semi-colon -separated CSS settings only, not the selector/className or enclosing braces - { }.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | name of the CSS class to apply the cssText to |
| cssText | [String](#type-string) | false | — | string of css settings to apply to the passed className in this handler's [stylesheet](#attr-stylesheethandlerstylesheet). |

### Returns

`[boolean](../main.md#type-boolean)` — returns true if CSS was applied, false otherwise

---
## Method: StyleSheetHandler.injectCssText

### Description
Injects text defining a block of selectors into this handler's [stylesheet](#attr-stylesheethandlerstylesheet).

The passed 'cssText' string should contain one or more selectors, each in the format '.className \[, className ...\] { css settings; }'. Use [modifyClass(className, cssText-without-braces)](#method-stylesheethandlermodifyclass) to apply styles to a specific CSS class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cssText | [String](#type-string) | false | — | string of css selectors and their settings to apply to this handler's [stylesheet](#attr-stylesheethandlerstylesheet). |

### Returns

`[boolean](../main.md#type-boolean)` — returns true if CSS was injected, false otherwise

---
## Method: StyleSheetHandler.filterCssText

### Description
Returns all styles for the passed className or array of classNames. The output is a single compound string in the format "_.class1 { css settings; } .class2 { css settings; } ..._ ".

This string may then be imported directly into another stylesheet, either [replacing content](#method-stylesheethandlersetcsstext) or [adding to it](#method-stylesheethandlerinjectcsstext).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | one or more CSS-class names to get the declaration for |

### Returns

`[String](#type-string)` — the CSS declaration for the passed className

---
## Method: StyleSheetHandler.removeClass

### Description
Remove the passed CSS class from the [stylesheet](#attr-stylesheethandlerstylesheet), by deleting it's rules and pruning it from multi-class selectors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | name of the CSS class to remove from the stylesheet |

### Returns

`[boolean](../main.md#type-boolean)` — returns true if CSS was removed, false otherwise

---
## Method: StyleSheetHandler.getClassList

### Description
Returns the list of CSS class-names defined in this handler's [stylesheet](#attr-stylesheethandlerstylesheet).

### Returns

`[Array of String](#type-array-of-string)` — the CSS declaration for the passed className

---
## Method: StyleSheetHandler.injectSheet

### Description
Create this handler's [stylesheet](#attr-stylesheethandlerstylesheet) element in the DOM.

---
