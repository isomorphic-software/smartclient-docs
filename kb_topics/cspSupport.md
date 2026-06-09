# Content Security Policy (CSP)

[← Back to API Index](../reference.md)

---

## KB Topic: Content Security Policy (CSP)

### Description
#### Content Security Policy (CSP) and Component Frameworks

The browser Content Security Policy mechanism includes `script-src` directives such as `'unsafe-eval'` and `'unsafe-inline'` that restrict the use of `eval()`, `new Function()`, inline event handlers, and dynamic script loading. These restrictions were introduced to mitigate injection attacks in applications where untrusted user input is carelessly concatenated into executable code — a class of vulnerability that arises primarily from naive application-level coding practices, not from the use of mature, security-audited frameworks.

SmartClient does **not** currently support running under a CSP policy that disables `unsafe-eval` or `unsafe-inline`. This is a deliberate architectural decision, not an oversight. The sections below explain why.

#### Why CSP Provides No Meaningful Security Benefit for Component Frameworks

CSP's `script-src` directives were designed to protect against a specific threat: an attacker who can inject a string into an HTML page such that it is executed as code. This threat is real when application developers use patterns like:

```
     element.innerHTML = "<img onerror='steal(document.cookie)' src=x>";
     eval("processData(" + userInput + ")");
 
```

In a SmartClient application, developers do not write code like this. The framework manages all DOM rendering, event handling, and server communication through controlled internal pathways. User-supplied data flows through typed DataSource fields, validated both client- and server-side, and is never interpolated into executable contexts. The attack surface that CSP was designed to close simply does not exist in a properly built SmartClient application.

SmartClient has been deployed by major banks, defense contractors, intelligence agencies, and financial institutions worldwide for over two decades, passing hundreds of independent security audits, with no history of meaningful injection exploits against the framework itself. This real-world security track record is far more significant than compliance with a header that addresses an inapplicable threat model.

#### Most Advanced Frameworks Cannot Fully Support CSP

SmartClient is not unusual in this regard. The more capable and feature-rich a JavaScript framework is, the more likely it is to rely on dynamic code generation for core functionality. Among major frameworks:

*   **Vue.js and Ember.js**: Both rely on dynamic template compilation at runtime, which requires `unsafe-eval`. Avoiding it requires a precompilation build step that eliminates runtime template compilation entirely, meaning templates cannot be composed or modified dynamically at runtime.
*   **Angular**: The JIT (Just-In-Time) compiler requires `unsafe-eval`. The AOT (Ahead-Of-Time) mode avoids it, but at the cost of eliminating dynamic template compilation, requiring a heavyweight precompilation build, and producing larger deployment bundles. Many Angular libraries and plugins still assume JIT availability.
*   **Ext JS / Sencha**: Uses dynamic code generation extensively for templates, formulas, and data binding, and does not fully support strict CSP.

Frameworks that do claim full CSP support tend to be either much simpler (providing no comparable dynamic features), or they achieve compatibility only through a precompilation step that sacrifices the ability to compose, modify, or generate UI definitions at runtime. Every framework that has undertaken CSP compatibility documents resulting performance penalties, increased bundle sizes, and reduced runtime capabilities.

#### Capabilities and Performance Lost Under CSP Restrictions

SmartClient uses `eval()`, `new Function()`, and related facilities for their intended purpose: high-performance code generation, powerful dynamic features, and runtime flexibility. These are not naive uses of dangerous APIs — they are deliberate architectural choices that deliver significant value. Disabling them would degrade or eliminate the following capabilities:

**User-Defined [Formula Fields](../classes/FormulaBuilder.md#class-formulabuilder), [Summary Fields](../classes/SummaryBuilder.md#class-summarybuilder), and [Dynamic Properties](../classes/Class.md#attr-classdynamicproperties)**

End users can define calculated grid columns using spreadsheet-like formula expressions (e.g., `A + B * 0.1`) and summary templates (e.g., `#{lastName}, #{firstName}`). These are compiled into JavaScript functions for evaluation on every grid row. [Dynamic Properties](../classes/Class.md#attr-classdynamicproperties) use the same mechanism: a component property value can be computed from data values and other application context via a [UserFormula](../reference.md#object-userformula) or [UserSummary](../reference.md#object-usersummary) expression — for example, deriving a grid column's [title](../classes/ListGridField.md#attr-listgridfieldtitle) from a formula like `ruleScope.currentUser.region`. Without dynamic code generation, none of these user-defined function capabilities would be available.

**Server Communication Performance**

SmartClient uses an optimized pseudo-JSON serialization format for server responses that supports JavaScript Date constructors and other non-strict-JSON constructs. Deserializing these responses falls back to `eval()` when `JSON.parse()` cannot handle the format. Under CSP restrictions, every server response would need to use strict JSON, requiring additional server-side serialization overhead and client-side date reconstruction, measurably slowing all DataSource operations.

**The [Developer Console](debugging.md#kb-topic-debugging)**

The SmartClient Developer Console is a powerful debugging tool that allows developers to evaluate arbitrary JavaScript expressions against live application state, inspect component trees, watch DataSource traffic, and profile performance. All of this depends on dynamic code evaluation. Without it, the single most important tool for diagnosing issues in running SmartClient applications would be non-functional.

**[Reify](reify.md#kb-topic-reify-overview) (Low Code Visual Builder)**

Reify enables visual, drag-and-drop application construction that generates SmartClient component trees from declarative screen definitions. Screens loaded from the server (via [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) and [RPCManager.createScreen](../classes/RPCManager.md#classmethod-rpcmanagercreatescreen)) are instantiated by evaluating their JavaScript representation at runtime. CSP restrictions would make it impossible to load or create screens dynamically, defeating the purpose of the tool.

**[AI Integration](integratingAI.md#kb-topic-integrating-ai-technology) and [AI-Generated Components](#aibuilduioperation)**

SmartClient's AI features allow natural-language operations like filtering grids, adding calculated columns, and generating entire data-bound components from user descriptions. The AI engine produces JavaScript component definitions that must be dynamically evaluated to create live UI. Chain-of-Thought prompt templates also use dynamic expression evaluation for variable interpolation. These features are fundamentally incompatible with CSP `eval` restrictions.

**The [FileLoader](../reference_2.md#object-fileloader) and Dynamic Module Loading**

[FileLoader](../reference_2.md#object-fileloader) supports background loading and caching of JavaScript and CSS resources to optimize application startup time. The `scriptInclude` [RPC transport](../reference.md#type-rpctransport) enables cross-domain communication by dynamically injecting ``<script>`` tags. Both mechanisms are restricted under strict CSP policies.

**Internal Performance Optimizations**

Throughout the framework, `new Function()` is used to generate optimized accessor functions, criteria evaluators, and serialization routines. These dynamically compiled functions are significantly faster than interpreted alternatives because the JavaScript engine can JIT-compile them with full optimization. Replacing them with generic, data-driven alternatives would produce measurably slower execution across many hot code paths, including DataSource filtering, record validation, grid rendering, and sort operations.

#### Effective Alternatives to CSP for Application Security

Rather than crippling the framework to comply with a policy that addresses an inapplicable threat, organizations concerned about application-level code quality have several effective alternatives:

*   **Static analysis**: Tools like ESLint (and dozens of alternatives) can enforce rules that prohibit `eval()` and similar patterns in _application-level_ code, which is where injection risks actually originate.
*   **Strict mode**: JavaScript `"use strict"` prevents certain unsafe patterns at the language level.
*   **TypeScript and ES6+ tooling**: Type checking and module systems used for application code naturally prevent the string-interpolation patterns that lead to injection vulnerabilities. SmartClient has excellent [TypeScript support](typeScriptSupport.md#kb-topic-typescript-support).
*   **Code review**: Security-sensitive organizations already mandate code review, which catches injection patterns far more reliably than blunt runtime restrictions that also disable legitimate framework functionality.

These approaches target the actual source of risk — application code written by developers who may be inexperienced with security — without degrading the capabilities of battle-tested framework code.

#### Official Stance and Feature Sponsorship

SmartClient does not plan to add CSP `unsafe-eval` compatibility to its roadmap, because doing so would mean permanently maintaining a crippled, slower variant of the framework with no genuine security benefit.

However, for customers who face an intractable organizational requirement for CSP compliance, we offer the possibility of creating a restricted mode through our [Feature Sponsorship](https://www.smartclient.com/services/index.jsp) program. Such an effort would produce a version of the framework that can run under `unsafe-eval` restrictions, with the following caveats:

*   A significant subset of features (including the Developer Console, user-defined formula and summary fields, Dynamic Properties, Reify screen loading, AI-generated UI, the `scriptInclude` transport, and others) would be **unavailable** in this mode.
*   Server communication, DataSource operations, and component rendering would be **measurably slower** due to the elimination of dynamically compiled code paths.
*   Certain browser-specific workarounds that currently use dynamic code generation would be removed, potentially introducing **new edge-case bugs** related to memory management and accessibility.
*   The resulting restricted mode would **not be backwards compatible** with existing applications that use any of the affected features.
*   Because the full-capability and restricted modes would need to be maintained in parallel, Feature Sponsorship for this work involves substantial **initial and ongoing** costs.

If your organization has this requirement, contact Isomorphic Software to discuss scope and sponsorship terms.

---
