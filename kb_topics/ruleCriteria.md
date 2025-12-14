# Dynamic Rules

[← Back to API Index](../reference.md)

---

## KB Topic: Dynamic Rules

### Description
If a property says it supports "rule criteria" it means that the criteria will be evaluated in the context of the current [Canvas.ruleScope](../classes/Canvas.md#attr-canvasrulescope), so can set [Criterion.fieldName](../classes/Criterion.md#attr-criterionfieldname) to a path that references state in the current rule context.

Because this type of criteria are allowed to reference UI state (such as whether any records are selected in an adjacent grid) they are not generally used to filter DataSource records, since such criteria would not be able to be evaluated on the server.

All RuleCriteria are also [Dynamic Criteria](dynamicCriteria.md#kb-topic-dynamiccriteria) unless otherwise noted.

**Schemaless Criteria Evaluation**

Values manually provided to the ruleScope with [Canvas.provideRuleContext](../classes/Canvas.md#method-canvasproviderulecontext) do not have a schema definition unless the DataSource and optionally the fieldName are provided. When no schema defines a value, criteria evaluation uses the following means to compare values:

*   Date values are compared as a logical date - without time part (see [DateUtil.compareLogicalDates](../classes/DateUtil.md#classmethod-dateutilcomparelogicaldates))
*   All other values are compared using the JavaScript `==` operator

### Related

- [Tab.visibleWhen](../classes/Tab.md#attr-tabvisiblewhen)
- [Tab.enableWhen](../classes/Tab.md#attr-tabenablewhen)
- [Canvas.visibleWhen](../classes/Canvas.md#attr-canvasvisiblewhen)
- [Canvas.enableWhen](../classes/Canvas.md#attr-canvasenablewhen)
- [FormItem.requiredWhen](../classes/FormItem.md#attr-formitemrequiredwhen)
- [FormItem.visibleWhen](../classes/FormItem.md#attr-formitemvisiblewhen)
- [FormItem.readOnlyWhen](../classes/FormItem.md#attr-formitemreadonlywhen)
- [FormItemIcon.enableWhen](../classes/FormItemIcon.md#attr-formitemiconenablewhen)
- [FormItemIcon.visibleWhen](../classes/FormItemIcon.md#attr-formitemiconvisiblewhen)
- [ButtonItem.enableWhen](../classes/ButtonItem.md#attr-buttonitemenablewhen)
- [NavItem.enableWhen](../classes/NavItem.md#attr-navitemenablewhen)
- [ListGridField.visibleWhen](../classes/ListGridField.md#attr-listgridfieldvisiblewhen)
- [ListGridField.enableWhen](../classes/ListGridField.md#attr-listgridfieldenablewhen)
- [MenuItem.enableWhen](../classes/MenuItem.md#attr-menuitemenablewhen)
- [MenuItem.visibleWhen](../classes/MenuItem.md#attr-menuitemvisiblewhen)

---
