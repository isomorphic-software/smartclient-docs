# Dashboards & Tools Framework Overview

[← Back to API Index](../reference.md)

---

## KB Topic: Dashboards & Tools Framework Overview

### Description
The Dashboards & Tools framework enables you to build interfaces in which a set of UI components can be edited by end users, saved and later restored.

This includes interfaces such as:

*   **Dashboards**: where a library of possible widgets can be created & configured, arranged into freehand or portal-style layouts, then stored for future use and shared with other users
*   **Diagramming & Flowchart tools**: tools similar to Visio™ which allow users to use shapes and connectors to create a flowchart or diagram representing a workflow, equipment or locations being monitored, a storyboard, or any similar interactive & modifiable visualization.
*   **Form Builders & Development Tools**: tools which enable end users to create new forms or new screens, define interactive behaviors and rules, and add the screens to an application on the fly

#### Overview

Dashboards & Tools provides a pattern for end user creation and configuration of UI components which enables the framework to store and re-create components exactly as the user configured them.

Unlike simple serialization, Dashboards & Tools is designed to capture _only_ UI state created directly by end user actions, and not transient or derived state (for more on this behavior and how it is different from serialization, see "Stored vs Derived State" below).

To achieve this, user-editable components are created via a special pattern (not just the usual `isc.SomeComponent.create()`), and changes to user-editable components that are meant to be saved are likewise applied via special APIs (not just direct calls to `someComponent.setSomething()`).

The main components and behaviors involved in Dashboards & Tools are covered in brief below - each of these points is covered in more detail in further sections:

*   User-editable components are created by [Palettes](../reference.md#interface-palette). `Palettes` create components from [PaletteNodes](../reference.md#object-palettenode), which are [data records](../reference.md#object-record) containing the component's class and default settings. Some `Palettes` provide an end user UI for creating components (eg drag a node from a Tree).
*   An editable component created by a `Palette` is represented by an [EditNode](../reference.md#object-editnode), which tracks the created component along with the data necessary to save and re-create the component.
*   An [EditContext](../classes/EditContext.md#class-editcontext) manages a list or [Tree](../classes/Tree.md#class-tree) of [EditNodes](../reference.md#object-editnode), and provides APIs for serializing and restoring `EditNodes` to and from XML and JSON, and updating the nodes as users make changes.
*   Many UI components have ["edit mode"](../classes/Canvas.md#method-canvasseteditmode) behaviors. When "edit mode" is enabled, when an end user interacts with the component, the component will save changes to its [EditNode](../reference.md#object-editnode) or to child [EditNodes](../reference.md#object-editnode) in the [EditContext](../classes/EditContext.md#class-editcontext). For example, [PortalLayout](../classes/PortalLayout.md#class-portallayout) can track and persist changes to the placement and size of portlets made by end users. `EditMode` behaviors are implemented by [EditProxies](../classes/EditProxy.md#class-editproxy), and different edit mode behaviors can be turned on and off for different kinds of tools.

A simple tool based on the Dashboards & Tools framework would typically consist of:

*   one or more `Palettes` showing components that the user can create
*   a main editing area where you can drag things from a [Palette](../reference.md#interface-palette) to create them. The editing area is just an ordinary UI component that has been placed into "edit mode" and provided with an `EditContext`. Depending on the type of tool, the main editing area might be a [DrawPane](../classes/DrawPane.md#class-drawpane) (for diagrams), a [DynamicForm](../classes/DynamicForm.md#class-dynamicform) (for a form builder) or various other widgets.
*   Buttons, Menus and pop-up dialogs that act on the currently selected widget. Dashboards & Tools has [built-in UI](../classes/EditProxy.md#attr-editproxycanselectchildren) for selecting one or more of the components being edited. [EditContext.getSelectedEditNode](../classes/EditContext.md#method-editcontextgetselectededitnode) provides the current edit node, and [EditContext.setNodeProperties](../classes/EditContext.md#method-editcontextsetnodeproperties) lets you manipulate its persisted state.
*   Buttons, Menus and pop-up dialogs providing the ability to load or save. These would use APIs on `EditContext` to [obtain XML or JSON Strings](../classes/EditContext.md#method-editcontextserializeeditnodes) representing the data to be saved, as well as to [restore saved state](../classes/EditContext.md#method-editcontextaddpalettenodesfromxml) from such Strings. DataSources can be used to store whatever is being edited: the serialized form is just an XML or JSON String, so it can be stored as an ordinary [DataSourceField](../reference_2.md#object-datasourcefield) value.

#### Creating editable components: `Palettes`

User-editable components are created by [Palettes](../reference.md#interface-palette). `Palettes` create components from [PaletteNodes](../reference.md#object-palettenode), which are [data records](../reference.md#object-record) containing the component's class and default settings.

Most types of `palettes` provide a UI for an end user to create components from `paletteNodes`. For example, a [TreePalette](../reference.md#class-treepalette) presents a hierarchical set of `paletteNodes` as a tree, and allows end users to drag nodes out in order to create components. All `palettes` also support [programmatic creation of components](../classes/Palette.md#method-palettemakeeditnode) from `paletteNodes`.

`paletteNodes` can be programmatically provided to a `Palette`, or, `Palettes` that are derived from [DataBoundComponents](../reference.md#interface-databoundcomponent) can load `paletteNodes` from a [DataSource](../classes/DataSource.md#class-datasource).

When a component is created from a `paletteNode`, an [EditNode](../reference.md#object-editnode) is created that tracks the [live component](../classes/EditNode.md#attr-editnodeliveobject) and the state needed to re-create it, called the [defaults](../classes/EditNode.md#attr-editnodedefaults).

#### EditContexts & EditProxies

An [EditContext](../classes/EditContext.md#class-editcontext) manages a [Tree](../classes/Tree.md#class-tree) of [EditNodes](../reference.md#object-editnode), and provides APIs for serializing and restoring `EditNodes` and updating the tree of nodes.

When an `EditNode` is added to an EditContext, typically it is immediately placed into ["Edit Mode"](../classes/Canvas.md#method-canvasseteditmode) (see [EditContext.autoEditNewNodes](../classes/EditContext.md#attr-editcontextautoeditnewnodes) for how this can be controlled). In Edit Mode, components introduce special behaviors, such as the ability to directly edit the titles of [Tab](../reference.md#object-tab)s in a [TabSet](../classes/TabSet.md#class-tabset) by double-clicking, or support for dragging new [FormItem](../classes/FormItem.md#class-formitem)s into a [DynamicForm](../classes/DynamicForm.md#class-dynamicform). Changes made while a component is in Edit Mode are saved to the component's [EditNode](../reference.md#object-editnode), in [EditNode.defaults](../classes/EditNode.md#attr-editnodedefaults).

Each component that has `editMode` features has a corresponding [EditProxy](../classes/EditProxy.md#class-editproxy) that implements those features. A component's `EditProxy` is automatically created when a component [goes into edit mode](../classes/Canvas.md#method-canvasseteditmode), and overrides the normal behavior of the component. By configuring the `EditProxy` for a component, you configure what behaviors the component will have when in edit mode, and which specific actions on the component will cause changes to be saved to its `EditNode`.

For example, [CanvasEditProxy](../reference.md#class-canvaseditproxy) has features for [saving coordinates as child widgets are dragged](../classes/EditProxy.md#attr-editproxypersistcoordinates), and [GridEditProxy](../classes/GridEditProxy.md#class-grideditproxy) has features for persisting [field visibility](../classes/GridEditProxy.md#attr-grideditproxysavefieldvisibility) when end users show and hide fields.

You can configure which EditProxy behaviors are active via [PaletteNode.editProxyProperties](../classes/PaletteNode.md#attr-palettenodeeditproxyproperties) and [EditNode.editProxyProperties](../classes/EditNode.md#attr-editnodeeditproxyproperties), and via the [editProxy AutoChild](../classes/Canvas.md#attr-canvaseditproxy).

#### EditContext & Trees of EditNodes

The `EditContext` has the capability to manage a `Tree` of `EditNodes` in order to enable tools that create a hierarchy of SmartClient components. When you use [EditContext.addNode](../classes/EditContext.md#method-editcontextaddnode) and add a new EditNode underneath another EditNode, the EditContext will automatically try to determine how the parent and child are related and actually call APIs on the widgets to establish a relationship, such as a Tab being added to a TabSet, or a FormItem being added to a DynamicForm. The EditContext uses the same approach as is used for Reify Drag and Drop - see [Reify overview](reify.md#kb-topic-reify-overview) for details.

Note that many if not most kinds of tools use only a flat list of EditNodes - for example, in a collage editor, photos may sometimes be stacked on top of each other, but a parent/child relationship in the sense of [Canvas.children](../classes/Canvas.md#attr-canvaschildren) is not established by doing so. Likewise, although the *Mockup Editor sample* allows end users to create mockups using SmartClient components, the components never truly become children of other components. Instead, as is typical of most mockup tools, hierarchy is achieved visually by simply placing a component on top of another and within its bounding rectangle.

Most types of tools use a flat list of `EditNodes` - generally speaking you will only use the hierarchy management features of `Editcontext` if you are creating a tool that actually allows end users to build functioning SmartClient screens, such as the *Form Builder example*. For such applications, use [EditContext.allowNestedDrops](../classes/EditContext.md#attr-editcontextallownesteddrops) to enable drag and drop interactions that will allow end users to place components inside of other components.

#### Stored vs Derived state

The purpose of having an `EditNode` for each UI component is to maintain a distinction between the current state of the live UI component and the state that should be saved. For example:

*   a component may have a current width of 510 pixels when viewed within a tool, but what should persist is the configured width of 40% of available space
*   a component may have editing behaviors enabled, such as the ability to double-click to edit labels or titles, which should be enabled in the tool but not at runtime
*   a tool may allow end users to create a Window, and then drag components into the Window. Every Window automatically creates subcomponents such as a header, but these should not be persisted because they don't represent state created by the end user. Only the components the end user actually dragged into the Window should be persisted
*   an end user may try out the effect of a property change, then abandon it and revert to the default value. We don't want the temporary change saved, and we don't even want to save the reversion to the default value - nothing about the saved state should be changed

By being careful to save _only intentional changes made by the user_:

*   the saved state remains minimal in size, and re-creating components from the stored state is more efficient
*   the saved state is much easier to edit since it contains only intentional settings, and not generated or derived information
*   the stored state is more robust against changes over time and easier to re-use. When we avoiding spuriously saving default values that the user has not modified, we avoid possible conflicts when a saved UI is deployed to a new version or in a different environment with different defaults

Specifically, only two things affect the state that will be stored for a given component:

1.  Features enabled when a component is in EditMode, configured via the component's EditProxy
2.  Direct calls to [EditContext.setNodeProperties](../classes/EditContext.md#method-editcontextsetnodeproperties) by application code

Any other kind of change to the widget is not automatically persisted.

#### Module requirements
**NOTE:** you must load the Tools [Optional Module](loadingOptionalModules.md#kb-topic-loading-optional-modules) for this framework.

Any tools that work with hierarchies of system components or derivations of them will also need the system schema which can be loaded by either of the following:

_JSP tag:_

```
<script><isomorphic:loadSystemSchema /></script>
```

_HTML tag:_

```
<SCRIPT SRC="../isomorphic/DataSourceLoader?dataSource=$systemSchema"></SCRIPT>
```

### Related

- [EditContext](../classes/EditContext.md#class-editcontext)
- [SerializationSettings](../reference.md#object-serializationsettings)
- [Palette](../reference.md#interface-palette)
- [HiddenPalette](../reference.md#class-hiddenpalette)
- [TreePalette](../reference.md#class-treepalette)
- [ListPalette](../reference.md#class-listpalette)
- [TilePalette](../reference.md#class-tilepalette)
- [MenuPalette](../reference.md#class-menupalette)
- [EditPane](../classes/EditPane.md#class-editpane)
- [EditTree](../classes/EditTree.md#class-edittree)
- [Placeholder](../classes/Placeholder.md#class-placeholder)
- [PlaceholderDefaults](../reference.md#object-placeholderdefaults)
- [EditProxy](../classes/EditProxy.md#class-editproxy)
- [ValuesManagerEditProxy](../reference.md#class-valuesmanagereditproxy)
- [CanvasEditProxy](../reference.md#class-canvaseditproxy)
- [HandPlacedContainerEditProxy](../reference.md#class-handplacedcontainereditproxy)
- [LayoutEditProxy](../reference.md#class-layouteditproxy)
- [LayoutResizeBarEditProxy](../reference.md#class-layoutresizebareditproxy)
- [SplitPaneEditProxy](../reference.md#class-splitpaneeditproxy)
- [TabSetEditProxy](../classes/TabSetEditProxy.md#class-tabseteditproxy)
- [StatefulCanvasEditProxy](../reference.md#class-statefulcanvaseditproxy)
- [RibbonButtonEditProxy](../reference.md#class-ribbonbuttoneditproxy)
- [ImgEditProxy](../reference.md#class-imgeditproxy)
- [ToolStripSeparatorEditProxy](../reference.md#class-toolstripseparatoreditproxy)
- [RibbonGroupEditProxy](../reference.md#class-ribbongroupeditproxy)
- [LabelEditProxy](../reference.md#class-labeleditproxy)
- [HeaderEditProxy](../reference.md#class-headereditproxy)
- [ProgressbarEditProxy](../reference.md#class-progressbareditproxy)
- [WindowEditProxy](../reference.md#class-windoweditproxy)
- [DetailViewerEditProxy](../classes/DetailViewerEditProxy.md#class-detailviewereditproxy)
- [MenuEditProxy](../classes/MenuEditProxy.md#class-menueditproxy)
- [SectionStackEditProxy](../reference.md#class-sectionstackeditproxy)
- [SectionStackSectionEditProxy](../reference.md#class-sectionstacksectioneditproxy)
- [ScreenLoaderEditProxy](../reference.md#class-screenloadereditproxy)
- [FormEditProxy](../reference.md#class-formeditproxy)
- [FormItemEditProxy](../classes/FormItemEditProxy.md#class-formitemeditproxy)
- [FileItemEditProxy](../reference.md#class-fileitemeditproxy)
- [TextItemEditProxy](../classes/TextItemEditProxy.md#class-textitemeditproxy)
- [BlurbItemEditProxy](../reference.md#class-blurbitemeditproxy)
- [TextAreaItemEditProxy](../reference.md#class-textareaitemeditproxy)
- [ButtonItemEditProxy](../reference.md#class-buttonitemeditproxy)
- [SelectItemEditProxy](../classes/SelectItemEditProxy.md#class-selectitemeditproxy)
- [RadioGroupItemEditProxy](../reference.md#class-radiogroupitemeditproxy)
- [CheckboxItemEditProxy](../reference.md#class-checkboxitemeditproxy)
- [DateItemEditProxy](../classes/DateItemEditProxy.md#class-dateitemeditproxy)
- [GridEditProxy](../classes/GridEditProxy.md#class-grideditproxy)
- [TileGridEditProxy](../reference.md#class-tilegrideditproxy)
- [DrawPaneEditProxy](../reference.md#class-drawpaneeditproxy)
- [DrawItemEditProxy](../reference.md#class-drawitemeditproxy)
- [DrawLabelEditProxy](../reference.md#class-drawlabeleditproxy)
- [FacetChartEditProxy](../classes/FacetChartEditProxy.md#class-facetcharteditproxy)
- [EditContext.screenMode](../classes/EditContext.md#classattr-editcontextscreenmode)
- [EditContext.editNodePasteOffset](../classes/EditContext.md#classattr-editcontexteditnodepasteoffset)
- [EditContext.rootComponent](../classes/EditContext.md#attr-editcontextrootcomponent)
- [Palette.generateNames](../classes/Palette.md#attr-palettegeneratenames)
- [TreePalette.componentDefaults](../reference.md#attr-treepalettecomponentdefaults)
- [EditPane.rootComponent](../classes/EditPane.md#attr-editpanerootcomponent)
- [EditTree.rootComponent](../classes/EditTree.md#attr-edittreerootcomponent)

---
