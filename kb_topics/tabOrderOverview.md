# Tab Order Overview

[← Back to API Index](../reference.md)

---

## KB Topic: Tab Order Overview

### Description
SmartClient has logic to automatically assign and manage tab indices for focusable components and elements within those components (for example Buttons, FormItems, Form Item icons, etc). This system has been designed to provide an intuitive user interaction experience by default, and to support being customized for alternative tabbing behaviors by application code (see "Custom Tab Orders", below).

The [TabIndexManager](../classes/TabIndexManager.md#class-tabindexmanager) class is a singleton class responsible for maintaining the tab order for a chain of elements, and parcelling out tab index values. This class is not directly responsible for updating any elements in the DOM - instead it associates a unique ID with a position in a [hierarchical data structure](../classes/Tree.md#class-tree), and provides APIs to restructure and reorder entries in the tree, request a numeric tab index value for each entry, and fire a notification method when an entry's tab index changes due to the tree being restructured.

The actual tab indices are lazily generated when requested, and will be slotted within the "auto-generated tab index" range (see Canvas.TAB\_INDEX\_FLOOR and TAB\_INDEX\_CEILING). A gap will be left between the assigned tab indices to minimize needing to reshuffle due to slotting elements before already assigned tab-indices, and logic is in place to handle reassigning tab indices to accommodate this if it does become necessary.

A notification method will be fired if any calculated tab index becomes obsolete due to the tree structure changing (either a parent is moved or we run out of space between elements and have to reassign indices to later elements).

Each SmartClient Canvas uses its own ID to register with the TabIndexManager at creation time and has built in logic to update its position in the as the page structure changes, and, for focusable widgets, ensure the returned tabIndex value is assigned to the widget handle. [FormItem](../classes/FormItem.md#class-formitem)s and [FormItemIcon](../reference.md#object-formitemicon)s are similarly registered with TabIndexManager and apply the returned tab index to the appropriate element on the page.

By default canvas tab positions are updated as follows:

*   On draw, top level elements are always moved to the end of the tab-order
*   When children are added to a parent, they will be moved to be a sub-element of the parent entry, in the position returned by [Canvas.getChildTabPosition](../classes/Canvas.md#method-canvasgetchildtabposition). Note that this method is overridden for Layouts to have tabbing occur in specified member order.

Other manipulations may occur for other widgets. See [DynamicForm.sortItemsIntoTabOrder](../classes/DynamicForm.md#method-dynamicformsortitemsintotaborder) and [FormItem.getIconTabPosition](../classes/FormItem.md#method-formitemgeticontabposition) for details on how the TabIndexManager is integrated with FormItems and FormItemIcons.

Note that for canFocus false widgets, or widgets with tab index explicitly specified as either -1 or some value below TAB\_INDEX\_FLOOR will still be present in the TabIndexManager's data tree (we'll just never request a tab-index for them). This allows us to manage the tab index of their children in a logically consistent manner

**Custom Tab order** Tabbing behavior for canvases may be customized in a number of ways:

*   An explicit [Canvas.tabIndex](../classes/Canvas.md#attr-canvastabindex) may be specified for any canvas. This is appropriate for very simple customizations only. It will not impact the tab-index of any child, so to build an intuitive user experience using explicit tabIndex values typically requires an explicit tabIndex be specified for every focusable element on the page.
*   The [Canvas.setRelativeTabPosition](../classes/Canvas.md#method-canvassetrelativetabposition) method may be used to assign a custom relative, or "local" tab position for a canvas. This is the position within the canvas's parent widget, or within top level widgets if the canvas has no parent or [Canvas.updateTabPositionOnReparent](../classes/Canvas.md#attr-canvasupdatetabpositiononreparent) is false.
*   For more sophisticated behavior, Canvases embedded in a parent may be placed into an explicit sequence for tabbing by overriding [Canvas.getChildTabPosition](../classes/Canvas.md#method-canvasgetchildtabposition) on the parent to return something other than the index of the canvas in the parent's children array.
*   Developers may override [Canvas.updateChildTabPositions](../classes/Canvas.md#method-canvasupdatechildtabpositions) and [Canvas.updateChildTabPosition](../classes/Canvas.md#method-canvasupdatechildtabposition) to explicitly modify how parent canvases order their children's tabbing behavior.
*   To actually provide an explicit tab-position for some Canvas, a developer may use the [TabIndexManager.moveTarget](../classes/TabIndexManager.md#classmethod-tabindexmanagermovetarget) method and pass in the canvas' ID as the first parameter.
*   Canvases may also choose not to have their tab position updated on draw (see [Canvas.updateTabPositionOnDraw](../classes/Canvas.md#attr-canvasupdatetabpositionondraw) or reparent (see [Canvas.updateTabPositionOnReparent](../classes/Canvas.md#attr-canvasupdatetabpositiononreparent)).  
    This is useful for providing tab index management logic that doesn't match up with top level draw order, or the canvas parent-child hierarchy.

Focusable elements other than SmartClient components (for example, native HTML elements embedded in some canvas, or third party widgets) can also participate in the automatically assigned tab order. See [customTabElements](customTabElements.md#kb-topic-including-custom-elements-in-the-tab-order) for details on how to achieve this.

---
