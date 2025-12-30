# Using AutoChildren

[← Back to API Index](../reference.md)

---

## KB Topic: Using AutoChildren

### Description
An AutoChild is an automatically generated subcomponent that a parent component creates to handle part of its presentation or functionality. An example is the [Window](../classes/Window.md#class-window) component and its subcomponent the [header](../classes/Window.md#attr-windowheader).

AutoChildren support a standard set of properties that can be used to customize or skin them. The names of these properties are derived from the name of the AutoChild itself. These properties will generally not be separately documented for every AutoChild unless there are special usage instructions; the existence of the properties is implied whenever you see an AutoChild documented.

The properties affecting AutoChildren are:

**"show" + name** (eg showHeader)

Controls whether the AutoChild should be created and shown at all. Note that the first letter of the AutoChild name is uppercased for this property ("header" -> "Header").

**name + "Properties"** (eg headerProperties)

Properties to apply to the autoChild created by this particular instance of the parent component. For example:
```
        isc.Window.create({
            ID: "myWindow",
            headerProperties: { layoutMargin: 10 }
        });
 
```
The above applies a [layoutMargin](../classes/Layout.md#attr-layoutlayoutmargin) of 10 to the header of `myWindow`, increasing the empty space around the subcomponents of the header (buttons, title label, etc).

Generally, \*Properties is null. **Do not** use the \*Properties mechanism for skinning. See \*Defaults next.

**name + "Defaults"** (eg headerDefaults)

Defaults that will be applied to the AutoChild created by any instance of the parent class. \*Defaults is used for skinning. This property should never be set when creating an instance of the parent component, as it will generally wipe out defaults required for the component's operation. Use [changeDefaults()](../classes/Class.md#classmethod-classchangedefaults) to alter defaults instead. This is generally as part of a custom skin and/or custom component creation - see the [overview of AutoChildren for component development](autoChildren.md#kb-topic-autochildren) for details and examples.

**name + "Constructor"** (eg headerConstructor)

SmartClient Class of the component to be created. An advanced option, this property should generally only be used when there is documentation encouraging you to do so. For example, [ListGrid](../classes/ListGrid_1.md#class-listgrid) offers the ability to use simple CSS-based headers or more complex [StretchImg](../classes/StretchImg.md#class-stretchimg) based headers via [ListGrid.headerButtonConstructor](../classes/ListGrid_1.md#attr-listgridheaderbuttonconstructor). The constructor can also be specified using the `_constructor` property in the defaults for the AutoChild.

The AutoChild system can be used to create both [direct children](../classes/Canvas.md#attr-canvaschildren) and indirect children (children of children). For example, the [minimizeButton](../classes/Window.md#attr-windowminimizebutton) of the Window is also an autoChild, even though it is actually located within the window header.

#### Skinning AutoChildren

Skinning AutoChildren by changing the AutoChild defaults is typically done for two purposes:

*   Changing the default appearance or behavior of a component, for example, making all Window headers shorter
*   Creating a customized variation of an existing component _while retaining the base component unchanged_. For example, creating a subclass of Window called "PaletteWindow" with a very compact appearance, while leaving the base Window class unchanged so that warning dialogs and other core uses of Windows do not look like PaletteWindows.

The best code examples for skinning are in the load\_skin.js file for the "SmartClient" skin, in `isomorphic/skins/SmartClient/load_skin.js`.

#### Passthroughs (eg window.headerStyle)

In many cases a component will provide shortcuts to skinning or customizing its AutoChildren, such as [Window.headerStyle](../classes/Window.md#attr-windowheaderstyle), which becomes header.styleName. When these shortcuts exist, they must be used instead of the more general AutoChild skinning system.

#### Safe Skinning

Before skinning an AutoChild consider the [safe skinning guidelines](safeSkinning.md#kb-topic-safe-skinning).

#### Accessing AutoChildren Dynamically

For a component "Window" with an AutoChild named "header", if you create a Window called `myWindow`, the header AutoChild is available as `myWindow.header` .

Unless documented otherwise, an AutoChild should be considered an internal part of a component. Always configure AutoChildren by APIs on the parent component when they exist. It makes sense to access an AutoChild for troubleshooting purposes or for workarounds, but in general, an AutoChild's type, behavior, and internal structure are subject to change without notice in future SmartClient versions.

Accessing an AutoChild may give you a way to make a dynamic change to a component that is not otherwise supported by the parent component (for example, changing a text label where there is no setter on the parent). Before using this approach, consider whether simply recreating the parent component from scratch is a viable option. This approach is more than fast enough for most smaller components, and will not create a reliance on unsupported APIs.

---
