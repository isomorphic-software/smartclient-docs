# Integration with JSF

[← Back to API Index](../main.md)

---

## KB Topic: Integration with JSF

### Description
SmartClient can be used within JSF applications to add AJAX richness and interactivity.

Because JSF is a pre-AJAX architecture, the recommended approach in adding SmartClient to JSF applications is to create pages that use SmartClient components exclusively, so that older, server-based JSF components do not introduce full-page refreshes.

JSF pages that render components on the server access data via JSF Expression Language. SmartClient-based JSF pages can similarly load initial data by using JSTL, as shown in [this example](/examples/server_integration/#jstlList), where a ListGrid is populated by JSTL access to Java Beans stored in the JSP `pageContext`.

Once a SmartClient JSF page has loaded, SmartClient components will request data via background HTTP requests that load only data, not a complete page. The [Direct Method Invocation](dmiOverview.md#kb-topic-direct-method-invocation) system can be used to declaratively map SmartClient's background data requests directly to Java Methods. The SmartClient server automatically translates inbound request data into Java Objects that are passed to the method you specify, and the Java method return value is automatically translated into data for SmartClient components.

#### Incorporating server-side JSF components into a SmartClient JSF page

An [HTMLFlow](../classes/HTMLFlow.md#class-htmlflow) or [HTMLPane](../classes/HTMLPane.md#class-htmlpane) component can be used to incorporate server-generated content within a SmartClient-based page. With [contentsType](../classes/HTMLFlow.md#attr-htmlflowcontentstype) set to "page", the HTMLPane/Flow will act like a standalone page-within-a-page (via a SmartClient-managed HTML IFRAME element), allowing interactive server-side JSF components to participate normally, with limitations as discussed under the documentation for [contentsType](../classes/HTMLFlow.md#attr-htmlflowcontentstype).

---
