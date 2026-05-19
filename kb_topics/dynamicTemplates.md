# Dynamic Templates

[← Back to API Index](../reference.md)

---

## KB Topic: Dynamic Templates

### Description
Dynamic templates let SmartClient property values include {expr} expression delimiters that are re-evaluated when their inputs change. The expression `{Customer.name}` inside a property value resolves the path `Customer.name` against the rules engine's ruleScope and substitutes its current value into the surrounding string. When the underlying ruleScope value changes, the property is re-evaluated and the widget's setter is called with the new value.

Dynamic templates are syntactic sugar over the existing [Class.dynamicProperties](../classes/Class.md#attr-classdynamicproperties) mechanism: each template compiles to a DynamicProperty whose formula is the template expression. No new reactive runtime is introduced.

#### {expr} syntax
Expressions are wrapped in braces:
```
   isc.Button.create({ title: "Save {Customer.name}'s data" });
   isc.Layout.create({ layoutStartMargin: isc.dynamic("form.values.margin + 10") });
 
```
To include a literal brace in the output, double it: `{{` produces `{` and `}}` produces `}`.

Brace delimiters were chosen over JavaScript's template literal `${}` form to avoid a false expectation of lexical scope capture, and to align with React JSX expression syntax so documentation and samples are inter-convertible between React and non-React environments.

#### Where templates can appear
Properties typed [DynString](../reference.md#type-dynstring) or [DynHTMLString](../reference_2.md#type-dynhtmlstring) accept {expr} templates directly — no wrapper required. Examples include [Button.title](../classes/Button.md#attr-buttontitle), [ListGridField.cellTemplate](../classes/ListGridField.md#attr-listgridfieldcelltemplate), and [Canvas.contents](../classes/Canvas.md#attr-canvascontents). On any other property, wrap the value with one of the marker functions to opt in:

*   [isc.dyn](../classes/isc.md#staticmethod-iscdyn) — string template producing a reactive string
*   [isc.dynamic](../classes/isc.md#staticmethod-iscdynamic) — inline expression returning a typed value (number, boolean, etc.)
*   [isc.dynRestricted](../classes/isc.md#staticmethod-iscdynrestricted) — string template compiled in restricted mode (see security)
*   [isc.dynOnce](../classes/isc.md#staticmethod-iscdynonce) — evaluated once at create() time, no reactive listener

#### Security: full vs. restricted mode
Templates compile to JavaScript via `new Function()`, so the trust level of the template source matters. For developer-authored templates that appear directly in source code, full expression mode is the default and any JavaScript expression is allowed. For templates that originate from untrusted sources (end-user preferences, database-stored configuration, external feeds), use [isc.dynRestricted](../classes/isc.md#staticmethod-iscdynrestricted), or set [dynRestricted:true](../classes/Class.md#classattr-classdynrestricted) on the instance to compile in restricted mode — only dot expressions, ternaries, and literal values are permitted. Function calls, assignment, bracket access, and similar constructs are rejected with a development-mode warning.

#### Disabling detection
Detection runs once per property value at create() time and is cheap, but for projects that prefer the verbose [Class.dynamicProperties](../classes/Class.md#attr-classdynamicproperties) syntax or need backward compatibility during incremental adoption, detection can be turned off at three levels:

*   `isc.dynamicTemplates = false` — system-wide; the detection loop is skipped entirely
*   [Class.useDynamicTemplates = false](../classes/Class.md#classattr-classusedynamictemplates) — per class, applies to all instances
*   `useDynamicTemplates: false` on [create()](../classes/Class.md#classmethod-classcreate) — per instance

#### See also
[reactJSXIntegration](reactJSXIntegration.md#kb-topic-react-jsx-integration) — the same {expr} syntax in JSX string props binds to React state instead of ruleScope, so application markup is portable between React and non-React builds.

---
