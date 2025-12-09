# autoChildren

[← Back to API Index](../reference.md)

---

## KB Topic: autoChildren

### Description
An autoChild is an automatically generated subcomponent that a component creates to handle part of its presentation or functionality.

An example is the Window component and its subcomponent the "header".

AutoChildren support a standard set of properties that can be used to customize or skin them.

This topic explains how to use the autoChild system when creating custom components in order to create maximum flexibility. To learn how to use the autoChild system with pre-existing components, [go here](autoChildUsage.md#kb-topic-using-autochildren).

Before reading this topic, be sure you have read the *QuickStart Guide* material on creating custom components and have reviewed the provided examples.

_Note:_ the autoChild pattern allows you to generate instances of any [Canvas](../classes/Canvas.md#class-canvas) subclass, but FormItems [may not be created outside of a DynamicForm](../classes/FormItem.md#classmethod-formitemcreate) and as such can not be instantiated as autoChildren using the APIs described below.

#### Basics

The following is an example of creating subcomponents **without** using the AutoChild pattern. In this case a fictitious "Portlet" class is being created, which uses an instance of isc.Label to serve as it's header.

```
 isc.defineClass("Portlet", "VLayout").addProperties({
     initWidget : function () {
         this.Super("initWidget", arguments);

         this.headerLabel = isc.Label.create({
             autoDraw:false,
             contents: this.title, 
             styleName: this.titleStyleName,
             portlet:this,
             click : function () { this.portlet.bringToFront() },
             wrap:false,  
             overflow:"hidden", 
             width:"100%"
         });
         this.addMember(this.headerLabel);
         ...
 
```
While straightforward, this approach provides limited flexibility to someone using the "Portlet" class. There is no way to:

1.  avoid creating the headerLabel, for a "headerless" portlet
2.  use a different, more advanced class as a header (eg, StretchImgButton or a custom class)
3.  skin / change the appearance of the headerLabel, beyond setting its `styleName`
4.  change it's layout behavior (eg enable autoSize)
5.  add or override event handlers

Let's imagine we wanted to add some of the above features. We could change the code like so:

```
 isc.defineClass("Portlet", "VLayout").addProperties({
     showHeaderLabel:true,
     headerLabelConstructor:isc.Label,
     initWidget : function () {
         this.Super("initWidget", arguments);

         if (this.showHeaderLabel) {
             this.headerLabel = this.headerLabelConstructor.create({
                 autoDraw:false,
                 contents: this.title, 
                 styleName: this.titleStyleName,
                 portlet:this,
                 click : function () { this.portlet.bringToFront() },
                 wrap:false,  
                 overflow:"hidden", 
                 width:"100%"
             }, this.headerLabelProperties);
             this.addMember(this.headerLabel);
         }
         ...
 
```
Our additions solve our initial concerns:

*   `showHeaderLabel:false` can be set to suppress the header label
*   `headerLabelConstructor` allows you to switch to a different class
*   `headerLabelProperties` give you a means to add arbitrary properties (skinning properties, sizing properties, event handlers, etc)

However, the code is becoming more verbose and repetitive, and we've created a few additional properties that now need documentation and testing. This extra work is going to be multiplied by every subcomponent we create where we want this kind of flexibility.

Enter the AutoChild system: the purpose of the AutoChild system is to define a standard pattern for creating subcomponents with maximum flexibility. This means:

*   developers creating custom components write less code, have less to test and less to document
*   developers can more easily understand each other's code for custom components, because it follows a standard pattern
*   developers **using** custom components have a standard pattern for customization, instead of learning customization APIs for every component separately

The code below uses the autoChild system to create the "headerLabel" subcomponent. This version of the code would still respect all of the customization properties from earlier examples (`headerLabelProperties` et al) and offers several additional degrees of flexibility still to be explained, yet it's significantly shorter. More importantly, this code is less redundant; the "boilerplate" code is gone and what's left is just the actual settings for the headerLabel subcomponent.
```
 isc.defineClass("Portlet", "VLayout").addProperties({
     headerLabelDefaults : {
         _constructor:isc.Label,
         click : function () { this.creator.bringToFront() },
         wrap:false,  
         overflow:"hidden", 
         width:"100%"
     },
     initWidget : function () {
         this.Super("initWidget", arguments);

         this.addAutoChild("headerLabel", {
             contents: this.title, 
             styleName: this.titleStyleName
         });
         ...
 
```

The documentation for [addAutoChild()](../classes/Class.md#method-classaddautochild) and [autoChildUsage](autoChildUsage.md#kb-topic-using-autochildren) explains why this code will still respect the `showHeaderLabel` flag and other customization properties even though they aren't mentioned specifically.  
In this case the `_constructor` property has been used to make the headerLabel be generated as an instance of [Label](../classes/Label.md#class-label), but the developer could alternatively have used `headerLabelConstructor`. If both `_autoChildName_Constructor` and `_constructor` are set, `_autoChildName_Constructor` will be used.

Note that AutoChildren are not always created as soon as the parent component, and may be created only when the parent is drawn, or in some cases, only when needed. For the best chance of forward compatibility, use properties and defaults instead of accessing the live reference, and if you do access the live reference, access it only when it is clear that the AutoChild must have been created by that point. For example, even if you determined by experimentation that the Window class currently creates it's "header" AutoChild when the Window is created, you should avoid accessing it until the Window has drawn, to leave room for the Window's implementation to change such that creation of the "header" AutoChild is deferred until draw.

#### AutoChildren lifecycle

By default any auto-children created by [Class.addAutoChild](../classes/Class.md#method-classaddautochild) or [Class.createAutoChild](../classes/Class.md#method-classcreateautochild) will be [destroyed](../classes/Canvas.md#method-canvasdestroy) when the canvas that created them is destroyed. You can suppress this behavior by setting `dontAutoDestroy` to `true` on the auto child. To do this you could add the property to the defaults or properties block for the autoChild, or pass it into the creating method in the dynamic set of properties.

#### Subclassing a component with autoChildren

If you are subclassing a component that has an autoChild and you want to change defaults for that autoChild, the correct way to do so is to use [changeDefaults()](../classes/Class.md#classmethod-classchangedefaults):

```
 isc.defineClass("MyWindow", "Window");
 isc.MyWindow.changeDefaults("headerDefaults", { layoutMargin:10 });
 isc.MyWindow.addProperties({ 
    ...
 
```

`changeDefaults()` creates a copy of the superclass defaults and applies your changes, which is important because you want to inherit the superclass behavior without affecting the superclass, and yet apply overrides.

The following code sample indicates two common incorrect patterns for working with defaults, and the consequences of each:

```
 isc.defineClass("MyWindow", "Window").addProperties({
     // NO.  Superclass behavior / settings for autoChild
     // won't be inherited.  Use changeDefaults() instead.
     headerDefaults : { ... },
 
     initWidget : function () {
         this.Super("initWidget", arguments);

         // NO.  "headerDefaults" object is shared across the class,
         // changing it affects all instances created from here on.
         // Pass dynamic defaults to addAutoChild() instead
         this.headerDefaults.myProperty = this.newValue;
         ...
 });
 
```
**defaults vs properties**

For AutoChildren, defaults and properties both provide similar means of adding properties to an AutoChild, and the distinction between them is primarily one of convention: a class that uses AutoChildren should never define a default value for _autoChildName_Properties, so that instances can freely specify _autoChildName_Properties without overriding built-in behavior.

```
 isc.defineClass("MyWindow", "Window").addProperties({
     // NO.  Any further use of "headerProperties", in
     // instances or in subclasses, would wipe out behavior
     headerProperties : { ... },
 
```

By consistently using [Class.changeDefaults](../classes/Class.md#classmethod-classchangedefaults) whenever you override autoChild defaults in a subclass, you ensure that your classes can in turn be subclassed and extended uniformly.

#### autoParents and creation order

The AutoChild pattern can create an entire hierarchy of generated subcomponents. For example, the [Window](../classes/Window.md#class-window) class included with SmartClient uses several AutoChildren as part of the overall header structure: separate autoChildren for the minimize button, close button, and then the header itself, a Layout-derived class that contains all other header controls.

To facilitate construction of hierarchies of autoChildren, the special `autoParent` property may appear in either defaults or properties for an autoChild, and indicates the name of another autoChild that should used as a parent. For example, to create a "closeButton" autoChild that will be a member of the "header" autoChild:

```
 isc.defineClass("Portlet", "VLayout").addProperties({
     headerDefaults : {
         _constructor:isc.HLayout,
         ...
     },
     closeButtonDefaults : {
         autoParent:"header",
         _constructor:isc.ImgButton,
         ...
     },
     initWidget : function () {
         this.Super("initWidget", arguments);

         this.addAutoChild("header");
         this.addAutoChild("closeButton");
         ...
 
```

In addition to cutting down on code and making inter-autoChild relationships clearer, using `autoParent` rather than manual calls to addMember() allows a subclass of your component to potentially completely rearrange the autoChildren you have defined, while retaining their behavior.

When using `autoParent` to arrange autoChildren, create parents first, then children.

**Tip:** if you want all of the behaviors of [addAutoChild()](../classes/Class.md#method-classaddautochild) _except_ automatically adding the autoChild to a parent, set `autoParent:"none"`.

**special case: TabSets and SectionStacks**

An autoChild that appears as a [Tab.pane](../classes/Tab.md#attr-tabpane) or [section item](../classes/SectionStackSection.md#attr-sectionstacksectionitems) does not have a clear way to refer to it's tab or section via the `autoParent` property. For this special case, the TabSet and SectionStack components allow tab.pane / section.items to contain the special string "autoChild:_autoChildName_". This will cause the corresponding autoChild to be automatically created when the tab is selected or section expanded.

Generally, whatever component is creating the AutoChildren should be the logically reusable, self-contained component, and all the meaty logic should appear as methods on that component. Then you know that the [creator](../classes/Class.md#attr-classcreator) is always the same thing, and always where all the logic is.

For example:

```
 isc.defineClass("Portlet", "VLayout").addProperties({
     ...
     mainTabsDefaults : {
         _constructor:isc.TabSet,
         tabs : [
             { title:"First Pane", pane:"autoChild:firstPane" }
         ]
     },
     firstPaneDefaults : {
         ...
     },
     initWidget : function () {
         this.Super("initWidget", arguments);

         // this automatically creates firstPane as an autoChild
         this.addAutoChild("mainTabs");
         ...
 
```

### Related

- [AutoChild](../reference.md#type-autochild)
- [Class.addAutoChild](../classes/Class.md#method-classaddautochild)
- [Class.createAutoChild](../classes/Class.md#method-classcreateautochild)
- [Class.creator](../classes/Class.md#attr-classcreator)
- [Class.autoCreator](../classes/Class.md#attr-classautocreator)
- [Canvas.autoParent](../classes/Canvas.md#attr-canvasautoparent)

### See Also

- [Canvas.autoParent](../classes/Canvas.md#attr-canvasautoparent)
- [Class.autoCreator](../classes/Class.md#attr-classautocreator)

---
