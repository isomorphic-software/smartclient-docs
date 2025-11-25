# Dynamic Strings

[← Back to API Index](../main.md)

---

## KB Topic: Dynamic Strings

### Description
A dynamic string is a simple but powerful template format. Its contents are treated literally, except that the result of evaluating a JavaScript expression may be substituted into the string using the syntax:  
`${_[JavaScript to evaluate]_}`

To include the literal string "`${`", place a backslash before it to escape.

To include a backslash before the result of an evaluated expression, the backslash must be in the result of an evaluated expression; either the subsequent evaluated expression may additionally output the backslash or the backslash may be replaced by its own evaluated expression, such as:  
`${String.fromCharCode(92)}`

A separate context [ValueMap](../main_2.md#type-valuemap) can be provided to make variables in-scope for the evaluated expressions within the dynamic string. For instance, expressions within the [Canvas.contents](../classes/Canvas.md#attr-canvascontents) string (when [dynamicContents](../classes/Canvas.md#attr-canvasdynamiccontents) is `true`) can use values from the [Canvas.dynamicContentsVars](../classes/Canvas.md#attr-canvasdynamiccontentsvars) ValueMap.

**Important:** As with any dynamically-evaluated content, never concatenate an untrusted or user-provided string into a dynamic string, because malicious input could execute arbitrary logic or exfiltrate sensitive data. "Escaping" an arbitrary, user-provided string for concatenation into a dynamic string is complicated and inherently unsafe, as it depends on which characters will precede and follow the escaped string. Rather than escaping, a better approach is to simply include the string via an expression. For example, rather than something like:  
`"DataSource " + dataSourceId + " could not be loaded."`  
.. you can use an expression for the string that should be added within, as with:  
`"DataSource ${dataSourceId} could not be loaded."`  and adding a 'dataSourceId' mapping to the context ValueMap.

Note: If the resulting string, after evaluating the dynamic string, will be used as HTML, then it is also important to HTML-escape expression results (see [String.asHTML](../classes/String.md#method-stringashtml)), or use trusted HTML as the results of expressions.

### Related

- [DynamicString](../main_2.md#type-dynamicstring)
- [AI.sendPrompt](../classes/AI.md#classmethod-aisendprompt)
- [Canvas.dynamicContents](../classes/Canvas.md#attr-canvasdynamiccontents)
- [Label.dynamicContents](../classes/Label.md#attr-labeldynamiccontents)

---
