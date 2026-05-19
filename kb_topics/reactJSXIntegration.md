# React JSX Integration

[← Back to API Index](../reference.md)

---

## KB Topic: React JSX Integration

### Description
SmartClient ships a React 18 wrapper layer that lets every SmartClient class be created and composed as a React component — `SC.ListGrid`, `SC.DynamicForm`, `SC.Button`, etc. — while keeping the underlying SmartClient widget in charge of rendering, layout, sizing, and event handling. JSX is the markup; SmartClient is the framework.

#### JSX-valued properties
Any SmartClient property that accepts a string of HTML (for example [Canvas.contents](../classes/Canvas.md#attr-canvascontents) or [Hover.contents](#hovercontents)) also accepts a React element value:
```
   <SC.Canvas contents={<MyHeader title="Hello"/>}/>
 
```
Two rendering modes are supported automatically based on the JSX value's content:

*   **SSR mode** (the default for static JSX) — the JSX is rendered once via React's static markup renderer and the resulting HTML is handed to the SmartClient setter. Cheap, no React runtime in the widget, no lifecycle.
*   **Root mode** (used when the JSX value references live React state or contains other SmartClient React wrappers) — the wrapper writes a placeholder ``<div>`` via the setter, then mounts a React 18 root inside the placeholder. Subsequent updates re-render through that root, so React state and JSX children flow through normally.

Mode is detected automatically; application code never selects.

#### JSX cell rendering
[ListGridField.cellTemplate](../classes/ListGridField.md#attr-listgridfieldcelltemplate) accepts a JSX-returning function:
```
   <SC.ListGrid>
       <fields>
           <field name="status" cellTemplate={record =>
               <StatusBadge state={record.state}/>
           }/>
       </fields>
   </SC.ListGrid>
 
```
Each rendered cell mounts its own per-cell React portal inside the body's ``<td>``, reconciled against the grid's live cell-geometry on render, resize, freeze/unfreeze, and column reorder. Per-cell portals are created and torn down alongside the grid's normal cell lifecycle — no manual cleanup required.

#### Dynamic Templates in JSX
The same {expr} [dynamic template](dynamicTemplates.md#kb-topic-dynamic-templates) syntax used in plain SmartClient property values also works inside JSX string props. When the wrapper is rendered inside a React tree, {expr} placeholders bind to React state (resolved via [SC.useRuleScope](#scuserulescope)) instead of the rules-engine ruleScope, so the same markup is portable between React and non-React builds. React state changes propagate to the SmartClient widget through the normal setter pipeline, with no manual setter calls.

#### Bridging rule scope and React state
[SC.useRuleScope](#scuserulescope) is a React hook that exposes the surrounding SmartClient ruleScope as a React state slice for use in JSX children. [SC.ContextBridge](#sccontextbridge) propagates React context across the SmartClient-to-React-and-back boundary that Root-mode portals introduce, so React providers in the host application remain visible to JSX rendered inside a SmartClient widget's contents.

#### Defining custom React classes
[SC.defineClass](#scdefineclass) registers a React component as a first-class SmartClient class, usable in JSX as `<SC.MyClass.../>` and discoverable to the SmartClient generator for typed prop declarations. Use this to factor an application's own widget abstractions consistently with SmartClient's own wrapper layer.

#### Performance
All optimisations live in core SmartClient (suppressRedraw windows, the [GridRenderer._cellsRendered](#method-gridrenderer_cellsrendered) hook, scID error placeholders, ResizeObserver wiring for external content, the {expr} template engine itself), so any external DOM manager — React, Web Components, vanilla JS, Angular wrappers — benefits without per-host duplication. React-specific code paths are restricted to call sites that must invoke React APIs directly.

---
