# Accessibility / Section 508 compliance

[← Back to API Index](../main.md)

---

## KB Topic: Accessibility / Section 508 compliance

### Description
SmartClient is a fully accessible technology which fulfills the Section 508 requirements of U.S. government law and similar international standards. Specificallly:

*   components are fully keyboard navigable and the browser's native focus indicator reveals keyboard focus to the user
*   components are themable/brandable, allowing a variety of high contrast and limited color range look and feel options to compensate for visual acuity disabilities
*   the WAI-ARIA standard is supported for adding semantic markup to components to identify them to screen readers such as NVDA or JAWS.

**WAI-ARIA support**

ARIA is a standard from the WAI (Web Accessibility Institute) that allows modern Ajax applications to add semantic markup to the HTML used to create modern Ajax interfaces to enable screen reader support. This semantic markup allows a screen reader to identify the function and state of complex components such as load-on-demand lists and trees even though they are composed of simple elements such a `<div>`s.

Note that ARIA support is the correct way to evaluate the accessibility of a web _application_. Standards which apply to a web _site_, such as ensuring that all interactive elements are composed of native HTML anchor (`<a>`) or `<form>` controls, cannot and should not be applied to a web _application_. A web application's accessibility must be evaluated in terms of its ARIA support.

By default, SmartClient components will write out limited ARIA markup sufficient to navigate basic menus and buttons. Full screen reader mode is not enabled by default because it has a small performance impact and subtly changes the management of keyboard focus in a way that may be less intuitive when primarily navigating an application with the mouse.

The limited ARIA support which is enabled by default is intended to allow a screen reader user to navigate to a menu to enable full screen reader support. This is analogous to a partially visually impaired user ariving at a site with normal theming and needing to switch to a high-contrast skin.

To enable full screenReader mode, call [isc.setScreenReaderMode](../classes/isc.md#staticmethod-iscsetscreenreadermode) before any SmartClient components are created or drawn. This implies that if an end user dynamically enables full screen reader support, the application page must be reloaded, as an any existing components will not have full ARIA markup.

For an overview of ARIA, see [http://www.w3.org/WAI/intro/aria.php](http://www.w3.org/WAI/intro/aria.php).

To completely disable ARIA markup, call [isc.setScreenReaderMode(false)](../classes/isc.md#staticmethod-iscsetscreenreadermode) before any components are drawn.

**Recommended Screen Reader Configuration**

The recommended configuration for screen reader use is the most recent available release of Firefox and either the JAWS or NVDA screen reader.

While WAI-ARIA markup is provided for other browsers, support for WAI-ARIA itself is known to be limited in current release versions of IE and other browsers supported by SmartClient.

**Application-level concerns**

While SmartClient enables accessible web applications to be created, it is always possible for an application to violate accessibility standards. The following is a brief and not exhaustive list of concerns for application authors:

*   for any operation that can be triggered via drag and drop, you should offer an equivalent keyboard-only means of performing the same operation. For common grid to grid drags, this is easily accomplished using [ListGrid.transferSelectedData](../classes/ListGrid_2.md#method-listgridtransferselecteddata).
*   if you use a component in a way that is not typical, such as using an ImgButton as a non-interactive stateful display, set its [Canvas.ariaRole](../classes/Canvas.md#attr-canvasariarole) appropriately. For a list of ARIA roles, see [http://www.w3.org/WAI/PF/aria/roles#role\_definitions](http://www.w3.org/WAI/PF/aria/roles#role_definitions). Note that in most cases you will not need to modify the default ariaRole written out by the SmartClient framework with screenReader mode enabled.
*   for plain HTML content that is incorporated into an Ajax interface (such as an embedded help system), embed the HTML into an [HTMLFlow](../classes/HTMLFlow.md#class-htmlflow) (whose default ARIA role is "article") and ensure the HTML itself is accessible (for example, has "alt" attributes on all images which are semantically meaningful)
*   in addition to setting explicit ARIA roles per canvas, SmartClient also allows developers to specify values for explicit [ARIA states](../classes/Canvas.md#attr-canvasariastate) (see [http://www.w3.org/TR/wai-aria/states\_and\_properties](http://www.w3.org/TR/wai-aria/states_and_properties)) to be written out with the HTML for a component.  
    Note that, as with ariaRoles, in most cases the framework automatically writes out any appropriate aria state information based on the component being generated - you'd only make use of this property if using components in some custom way. To provide a concrete example: a developer might implement a logical nested "menu" built from a set of Button instances. In that case, some button might have ariaRole set to `"menuitem"` and (if it launches a sub-menu), also the ["haspopup"](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-haspopup) aria state. The code for this would be something like:
    ```
     isc.Button.create({
          // ... various properties
          
          ariaRole:"menuitem",
          ariaState:{haspopup:true}
     });
     
    ```
    

**Known Screen Reader bugs / quirks**

JAWS: By default, JAWS treats a web page as a web document - text interspersed with graphics, links, etc. - and not as an application consisting of form controls, interactive buttons, lists, and so on. To enable application mode in JAWS, it is necessary to add `role="application"` to the `<body>` tag. See [Freedom Scientific Bulletin - In ARIA, what is the difference in how JAWS treats role="application" and role="document"?](https://support.freedomscientific.com/support/technicalsupport/bulletin/1665)

### Related

- [isc.setScreenReaderMode](../classes/isc.md#staticmethod-iscsetscreenreadermode)
- [Canvas.setAriaState](../classes/Canvas.md#method-canvassetariastate)
- [ListGrid.getCellRole](../classes/ListGrid_2.md#method-listgridgetcellrole)
- [ListGrid.getCellAriaState](../classes/ListGrid_2.md#method-listgridgetcellariastate)
- [ListGrid.getRowRole](../classes/ListGrid_2.md#method-listgridgetrowrole)
- [ListGrid.getRowAriaState](../classes/ListGrid_2.md#method-listgridgetrowariastate)
- [ListGrid.getHeaderButtonAriaState](../classes/ListGrid_2.md#method-listgridgetheaderbuttonariastate)
- [ListGrid.canTabToHeader](../classes/ListGrid_1.md#attr-listgridcantabtoheader)
- [ListGrid.canTabToSorter](../classes/ListGrid_1.md#attr-listgridcantabtosorter)
- [ListGrid.screenReaderCellSeparator](../classes/ListGrid_1.md#attr-listgridscreenreadercellseparator)
- [ListGrid.screenReaderRowSeparator](../classes/ListGrid_1.md#attr-listgridscreenreaderrowseparator)
- [ListGrid.screenReaderIncludeFieldTitles](../classes/ListGrid_1.md#attr-listgridscreenreaderincludefieldtitles)
- [ListGrid.screenReaderWriteRowLabelledBy](../classes/ListGrid_1.md#attr-listgridscreenreaderwriterowlabelledby)
- [Img.altText](../classes/Img.md#attr-imgalttext)
- [Canvas.ariaRole](../classes/Canvas.md#attr-canvasariarole)
- [Canvas.ariaState](../classes/Canvas.md#attr-canvasariastate)
- [FormItem.ariaRole](../classes/FormItem.md#attr-formitemariarole)
- [FormItem.ariaState](../classes/FormItem.md#attr-formitemariastate)
- [ListGrid.ariaRole](../classes/ListGrid_1.md#attr-listgridariarole)

---
