# EditContext Documentation

[← Back to API Index](../reference.md)

---

## Class: EditContext

### Description
An EditContext provides an editing environment for a set of components.

An EditContext is typically populated by adding a series of [EditNodes](../reference.md#object-editnode) created via a [Palette](../reference.md#interface-palette), either via drag and drop creation, or when loading from a saved version, via [addFromPaletteNode()](#method-editcontextaddfrompalettenode) or [addPaletteNodesFromXML()](#method-editcontextaddpalettenodesfromxml).

An EditContext then provides interfaces for further editing of the components represented by EditNodes.

Developers may explicitly define an edit context and initialize it with a [EditContext.rootComponent](#attr-editcontextrootcomponent) - the root of the user interface being created. The EditContext itself is not visible to the user, but the root component's [liveObject](EditNode.md#attr-editnodeliveobject) may be.  
As child editNodes are added to the rootComponent node or its descendants, liveObjects in the user will update to reflect these changes. The live objects for the edit nodes will be nested using the appropriate parent-child relationships, for the types of node in question. For example Canvases will be added as [members](Layout.md#attr-layoutmembers) of layouts and FormItems will be added as [fields](DynamicForm.md#attr-dynamicformfields) of DynamicForms.

To enable drag and drop creation of widgets from a [Palette](../reference.md#interface-palette), a developer can use [Canvas.setEditMode](Canvas.md#method-canvasseteditmode) to enable editing behaviors on the live object of the desired drop target (typically the root component).  
To enable editNode creation via double-click on a [Palette](../reference.md#interface-palette), developers can set the [Palette.defaultEditContext](Palette.md#attr-palettedefaulteditcontext).

Developers can also make use of [EditPane](EditPane.md#class-editpane) or [EditTree](EditTree.md#class-edittree) classes which provide a visual interface for managing an EditContext.

### Groups

- devTools

---
## ClassAttr: EditContext.screenMode

### Description
Should components managed by an EditContext have the characteristics of a [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) screen loaded via [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen) or equivalent? This mode must be enabled to have multiple EditContext instances at one time where component might have matching IDs.

If not set, components will have [global IDs](Canvas.md#attr-canvasid) as assigned by the [EditNode](../reference.md#object-editnode) configuration.

### Groups

- devTools

**Flags**: IR

---
## ClassAttr: EditContext.editNodePasteOffset

### Description
The number of pixels to offset a pasted node from the node being copied

### Groups

- devTools

**Flags**: IRW

---
## Attr: EditContext.selectedTintOpacity

### Description
Opacity applied to [editMask](EditProxy.md#attr-editproxyeditmask) of selected component when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "tintMask".

This value is applied as a default to [EditProxy.selectedTintOpacity](EditProxy.md#attr-editproxyselectedtintopacity).

### See Also

- [EditContext.selectedTintColor](#attr-editcontextselectedtintcolor)

**Flags**: IR

---
## Attr: EditContext.selectedAppearance

### Description
Appearance that is applied to selected component.

This value is applied as a default to [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance).

### See Also

- [EditContext.selectedBorder](#attr-editcontextselectedborder)
- [EditContext.selectedTintColor](#attr-editcontextselectedtintcolor)
- [EditContext.selectedTintOpacity](#attr-editcontextselectedtintopacity)

**Flags**: IR

---
## Attr: EditContext.hideGroupBorderOnDrag

### Description
Should the group selection box shown when [canGroupSelect](#attr-editcontextcangroupselect) is true be hidden during drag?

Treated as `true` if not explicitly set to false.

**Flags**: IR

---
## Attr: EditContext.defaultPalette

### Description
[Palette](../reference.md#interface-palette) to use when an [EditNode](../reference.md#object-editnode) is being created directly by this EditContext, instead of being created due to a user interaction with a palette (eg dragging from a [TreePalette](../reference.md#class-treepalette), or clicking on [MenuPalette](../reference.md#class-menupalette)).

If no defaultPalette is provided, the EditContext uses an automatically created [HiddenPalette](../reference.md#class-hiddenpalette).

**Flags**: IRW

---
## Attr: EditContext.canDragGroup

### Description
Should the group selection box shown when [canGroupSelect](#attr-editcontextcangroupselect) is true allow dragging the group as a whole?

Treated as `true` if not set and [canGroupSelect](#attr-editcontextcangroupselect) is true.

**Flags**: IR

---
## Attr: EditContext.editMaskProperties

### Description
Properties to apply to all [EditProxy.editMask](EditProxy.md#attr-editproxyeditmask)s created for components in edit mode. This mask can be modified when the node is selected by [EditContext.selectedBorder](#attr-editcontextselectedborder), [EditContext.selectedTintColor](#attr-editcontextselectedtintcolor) and [EditContext.selectedTintOpacity](#attr-editcontextselectedtintopacity) depending on the [EditContext.selectedAppearance](#attr-editcontextselectedappearance) setting.

**Flags**: IR

---
## Attr: EditContext.persistCoordinates

### Description
When enabled, changes to a [liveObject](EditNode.md#attr-editnodeliveobject)'s position and size will be persisted to their [EditNodes](../reference.md#object-editnode) by default. This applies to both programmatic calls and user interaction (drag reposition or drag resize).

This feature can be disabled by either setting this property or [EditProxy.persistCoordinates](EditProxy.md#attr-editproxypersistcoordinates) to `false`. This property affects all nodes within the EditContext whereas the latter property affects children of a single node.

In some use-cases, like Reify, coordinates should not be persisted except when a component explicitly enables this feature. By setting this property to `null` no component will persist coordinates of children unless `EditProxy.persistCoordinates` is explicitly set to `true`.

**Flags**: IRW

---
## Attr: EditContext.showSelectedLabel

### Description
Should the selection outline show a label for selected components? A component may also be highlighted with the selection outline and label to indicate the target of a drop. To suppress showing a label at any time set this property to `false`.

To suppress labels during selection but still show them when targeted for a drop, see [EditContext.showSelectedLabelOnSelect](#attr-editcontextshowselectedlabelonselect).

NOTE: A selected component label is only supported when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "outlineEdges".

**Flags**: IR

---
## Attr: EditContext.hoopSelectorProperties

### Description
Properties to apply to [EditProxy.hoopSelector](EditProxy.md#attr-editproxyhoopselector).

**Flags**: IR

---
## Attr: EditContext.canSelectEditNodes

### Description
Should editNodes added to this EditContext be selectable? When `true`, each [EditProxy.canSelectChildren](EditProxy.md#attr-editproxycanselectchildren) property is enabled unless explicitly set to `false`. This allows an individual component to override this setting.

**Flags**: IR

---
## Attr: EditContext.useCopyPasteShortcuts

### Description
If set, auto-enables [EditProxy.useCopyPasteShortcuts](EditProxy.md#attr-editproxyusecopypasteshortcuts) on the [EditProxy](EditProxy.md#class-editproxy) for the [root editNode](#method-editcontextgetrooteditnode). This works whether there is currently a root editNode or one is added later.

**Flags**: IR

---
## Attr: EditContext.enableInlineEdit

### Description
Whether inline editing should be enabled for any components that are added and are placed into editMode. Enabling this will turn on inline edit for any EditProxy where [EditProxy.supportsInlineEdit](EditProxy.md#attr-editproxysupportsinlineedit) is true.

**Flags**: IR

---
## Attr: EditContext.extraPalettes

### Description
Additional [Palettes](../reference.md#interface-palette) to consult for metadata when deserializing [Edit Nodes](../reference.md#object-editnode). Note that the [defaultPalette](#attr-editcontextdefaultpalette) is always consulted and need not be provided again here.

**Flags**: IRW

---
## Attr: EditContext.autoEditNewNodes

### Description
New nodes added to the editContext are automatically placed into edit mode if the new node's parent is in edit mode. To suppress this action set `autoEditNewNodes` to false.

**Flags**: IRW

---
## Attr: EditContext.showSelectedLabelOnSelect

### Description
Should the selection outline show a label when the component is selected? This property is similar to [EditContext.showSelectedLabel](#attr-editcontextshowselectedlabel). Whereas [showSelectedLabel](#attr-editcontextshowselectedlabel) controls whether a label is shown at any time, this property allows normal selection to suppress the label but still show a label during the drop process on the target. Leave [showSelectedLabel](#attr-editcontextshowselectedlabel) unset and set this property to `false`.

NOTE: A selected component label is only supported when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "outlineEdges".

**Flags**: IR

---
## Attr: EditContext.allowDropThrough

### Description
Dropping a component near the edge of another component allows the component to be dropped through an ancestor component. To suppress this action set `allowDropThrough` to false.

**Flags**: IRW

---
## Attr: EditContext.allowNestedDrops

### Description
Controls whether components can be dropped into other components which support child components.

When enabled, during a drop interaction in which a [PaletteNode](../reference.md#object-palettenode) or [EditNode](../reference.md#object-editnode) is the drop data, the [Component Schema](../kb_topics/componentSchema.md#kb-topic-component-schema) of the current candidate drop target is inspected to see whether that parent allows children of the type being dropped. If it does, the drop will result in a call to [EditContext.addNode](#method-editcontextaddnode) for a paletteNode or for an existing [EditNode](../reference.md#object-editnode) in the same tree.

Specific components can disable nested drops by explicitly setting [EditProxy.allowNestedDrops](EditProxy.md#attr-editproxyallownesteddrops) to false.

This mode is enabled by default unless explicitly disabled by setting this property to false.

**Flags**: IR

---
## Attr: EditContext.canGroupSelect

### Description
Should a group selection outline covering the outermost bounding boxes of all selected components be shown in this container?

Treated as `true` if not set and hoop selection is enabled (see [EditProxy.canSelectChildren](EditProxy.md#attr-editproxycanselectchildren) and [selectionType](#attr-editcontextselectiontype).

**Flags**: IR

---
## Attr: EditContext.hoopSelectionMode

### Description
Defines the mode of inclusion for components encountered during hoop selection which is enabled when [selectionType](#attr-editcontextselectiontype) is `multiple`. `encloses` mode causes selection of components that are completely enclosed by the hoop. `intersects` mode selects components that come into contact with the hoop.

### See Also

- [HoopSelectionStyle](../reference.md#type-hoopselectionstyle)

**Flags**: IR

---
## Attr: EditContext.defaultParent

### Description
The default parent [EditNode](../reference.md#object-editnode) to be used when a new EditNode is added to the EditContext without a specified parent. This commonly occurs when a paletteNode is double-clicked in a palette.

If not specified, the root editNode (see [EditContext.getRootEditNode](#method-editcontextgetrooteditnode)) is used.

Note: this property is automatically cleared if node is removed from the editTree such as on calls to [EditContext.destroyAll](#method-editcontextdestroyall) or [EditContext.removeNode](#method-editcontextremovenode).

**Flags**: IWR

---
## Attr: EditContext.selectedLabelBackgroundColor

### Description
The background color for the selection outline label. The default is defined on [SelectionOutline](SelectionOutline.md#class-selectionoutline).

This value is applied as a default to [EditProxy.selectedLabelBackgroundColor](EditProxy.md#attr-editproxyselectedlabelbackgroundcolor).

NOTE: A selected component label is only supported when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "outlineEdges".

### See Also

- [EditContext.showSelectedLabel](#attr-editcontextshowselectedlabel)

**Flags**: IR

---
## Attr: EditContext.selectedBorder

### Description
Set the CSS border to be applied to the selection outline of the selected components. This property is used when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is `outlineMask` or `outlineEdges`.

This value is applied as a default to [EditProxy.selectedBorder](EditProxy.md#attr-editproxyselectedborder).

**Flags**: IR

---
## Attr: EditContext.selectedTintColor

### Description
Mask color applied to [editMask](EditProxy.md#attr-editproxyeditmask) of selected component when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "tintMask".

This value is applied as a default to [EditProxy.selectedTintColor](EditProxy.md#attr-editproxyselectedtintcolor).

### See Also

- [EditContext.selectedTintOpacity](#attr-editcontextselectedtintopacity)

**Flags**: IR

---
## Attr: EditContext.selectionType

### Description
Defines selection behavior when in edit mode. Only two styles are supported: "single" and "multiple". Multiple enables hoop selection.

### See Also

- [SelectionStyle](../reference.md#type-selectionstyle)

**Flags**: IRW

---
## Attr: EditContext.rootComponent

### Description
Root of data to edit. Must contain the "type" property, with the name of a valid [schema](DataSource.md#class-datasource) or nothing will be able to be dropped on this EditContext. A "liveObject" property representing the rootComponent is also suggested. Otherwise, a live object will be created from the palette node.

Can be retrieved at any time. Use [EditContext.getRootEditNode](#method-editcontextgetrooteditnode) to retrieve the [EditNode](../reference.md#object-editnode) created from the rootComponent.

### Groups

- devTools

**Flags**: IR

---
## Method: EditContext.serializeEditNodesAsJSON

### Description
Serialize the provided [EditNodes](../reference.md#object-editnode) to a JSON representation of [PaletteNodes](../reference.md#object-palettenode). Note that the EditNodes must have been added to this EditContext. The result can be supplied to [addPaletteNodesFromJSON()](#method-editcontextaddpalettenodesfromjson) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of EditNode](#type-array-of-editnode) | false | — | EditNodes to be serialized |
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — a JSON representtion of the provided EditNodes

---
## Method: EditContext.removeAll

### Description
Removes all [EditNodes](../reference.md#object-editnode) from the EditContext, but does not destroy the [liveObjects](EditNode.md#attr-editnodeliveobject).

---
## Method: EditContext.makePaletteNodeTree

### Description
Creates a [Tree](Tree.md#class-tree) of [PaletteNodes](../reference.md#object-palettenode) from an [EditNode](../reference.md#object-editnode) in this context's [editNodeTree](#method-editcontextgeteditnodetree), by using [EditContext.makePaletteNode](#method-editcontextmakepalettenode) on the passed `EditNode` and its descendents within the [editNodeTree](#method-editcontextgeteditnodetree).

The root node of the returned [Tree](Tree.md#class-tree) will be a PaletteNode derived from the passed `EditNode`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | root editNode to make Tree of PaletteNodes from |
| removeAutoIDs | [Boolean](#type-boolean) | false | — | should ID and autoID defaults be removed? |

### Returns

`[Tree](#type-tree)` — a Tree of paletteNodes or null

---
## Method: EditContext.getRootEditNode

### Description
Returns the root [EditNode](../reference.md#object-editnode) of the EditContext typically created from [EditContext.rootComponent](#attr-editcontextrootcomponent).

### Returns

`[EditNode](#type-editnode)` — the root EditNode

---
## Method: EditContext.setNodeProperties

### Description
Update an editNode's serializable "defaults" with the supplied properties. If you wish to remove a property from the defaults (rather than setting it to null), then use [removeNodeProperties()](#method-editcontextremovenodeproperties) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to update |
| properties | [Canvas Properties](#type-canvas-properties) | false | — | the properties to apply |
| skipLiveObjectUpdate | [Boolean](#type-boolean) | true | — | whether to skip updating the [liveObject](EditNode.md#attr-editnodeliveobject), e.g. if you have already updated the liveObject |

### See Also

- [EditContext.removeNodeProperties](#method-editcontextremovenodeproperties)
- [EditContext.getNodeProperty](#method-editcontextgetnodeproperty)

---
## Method: EditContext.substitutedNode

### Description
Notification fired when a different [PaletteNode](../reference.md#object-palettenode) is substituted for one being dropped into a container.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| origNode | [PaletteNode](#type-palettenode) | false | — | node that was originally dropped |
| newNode | [PaletteNode](#type-palettenode) | false | — | node that was substituted |
| parentNode | [EditNode](#type-editnode) | false | — | parent node of the drop |

---
## Method: EditContext.getPaletteNodesFromXML

### Description
Obtain [PaletteNodes](../reference.md#object-palettenode) from an XML representation, but do not add them to the EditContext.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| xmlString | [String](#type-string) | false | — | XML string |
| callback | [PaletteNodeCallback](#type-palettenodecallback) | false | — | Callback used to return the PaletteNodes |

### See Also

- [Callbacks.PaletteNodeCallback](Callbacks.md#method-callbackspalettenodecallback)
- [EditContext.serializeAllEditNodes](#method-editcontextserializealleditnodes)
- [EditContext.serializeEditNodes](#method-editcontextserializeeditnodes)

---
## Method: EditContext.getEditNodesByType

### Description
Returns [EditNodes](../reference.md#object-editnode) as an array that match the specified type or types. By default the `types` are matched against the [EditNode.type](EditNode.md#attr-editnodetype) or the general type of the component. By setting `strict` to `true` the match is made against the editNode type exactly.

For example, searching for "Canvas" nodes will return nodes for any component that derives from Canvas unless `strict` is set. In the strict case, the search will only return nodes for explict Canvas nodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| types | [Array of String](#type-array-of-string)|[String](#type-string) | false | — | type or types of nodes to find |
| strict | [boolean](../reference.md#type-boolean) | true | — | true to match the [EditNode.type](EditNode.md#attr-editnodetype) exactly |

### Returns

`[Array of EditNode](#type-array-of-editnode)` — the filtered list of EditNodes

---
## Method: EditContext.copyEditNodes

### Description
Copies the passed editNode or editNodes to an internal "clipboard" space, for later application via [EditContext.pasteEditNodes](#method-editcontextpasteeditnodes).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode)|[Array of EditNode](#type-array-of-editnode) | false | — | — |

---
## Method: EditContext.getSelectedLabelText

### Description
Overridable method to provide a custom selection outline label. This method is called when a label is to be shown with an outline.

The default implementation returns the same description shown in the edit tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [Object](../reference.md#type-object) | false | — | the Canvas or FormItem component to label |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — string to be displayed

---
## Method: EditContext.inlineEditorShowing

### Description
Notification method fired when an inline title or value editor is shown or closed for a component in the designer pane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [FormItem](#type-formitem) | false | — | the field within the inline editor when showing. null if the editor is closed. |
| type | [String](#type-string) | false | — | the type of editor showing: "title" or "value" |

---
## Method: EditContext.makeEditNode

### Description
Creates and returns an EditNode using the [EditContext.defaultPalette](#attr-editcontextdefaultpalette). Does not add the newly created EditNode to an EditContext.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNode | [PaletteNode](#type-palettenode) | false | — | the palette node to use to create the new node |

### Returns

`[EditNode](#type-editnode)` — the EditNode created from the paletteNode

---
## Method: EditContext.enableEditing

### Description
Enable edit mode for an [EditNode](../reference.md#object-editnode). This is a shortcut for calling [Canvas.setEditMode](Canvas.md#method-canvasseteditmode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the EditNode on which to enable editing |

### See Also

- [Canvas.setEditMode](Canvas.md#method-canvasseteditmode)
- [EditContext.isNodeEditingOn](#method-editcontextisnodeeditingon)

---
## Method: EditContext.makePaletteNode

### Description
Creates a [PaletteNode](../reference.md#object-palettenode) from an [EditNode](../reference.md#object-editnode) in this context's [editNodeTree](#method-editcontextgeteditnodetree).

This essentially creates a new [PaletteNode](../reference.md#object-palettenode) with the [EditNode.defaults](EditNode.md#attr-editnodedefaults) from the passed `editNode`. The returned `paletteNode` could then be used with [EditContext.addFromPaletteNode](#method-editcontextaddfrompalettenode) to effectively create a copy of the original editNode - specifically a new editNode with a new [EditNode.liveObject](EditNode.md#attr-editnodeliveobject) created from the same defaults.

However note that `makePaletteNode()` does not copy descendant nodes - use [EditContext.makePaletteNodeTree](#method-editcontextmakepalettenodetree) for that.

May return null if the passed editNode cannot validly by transformed into a paletteNode, for example if [EditNode.canDuplicate](EditNode.md#attr-editnodecanduplicate) was set false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to use to make a paletteNode |

### Returns

`[PaletteNode](#type-palettenode)` — paletteNode derived from the editNode or null

---
## Method: EditContext.nodeRemoved

### Description
Notification fired when an [EditNode](../reference.md#object-editnode) has been removed from the EditContext

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| removedNode | [EditNode](#type-editnode) | false | — | node that was removed |
| parentNode | [EditNode](#type-editnode) | false | — | parent node of the node that was removed |
| rootNode | [EditNode](#type-editnode) | false | — | root node of the edit context |

---
## Method: EditContext.getSelectedEditNodes

### Description
Returns all selected EditNodes as an Array.

### Returns

`[Array of EditNode](#type-array-of-editnode)` — the selected edit nodes

---
## Method: EditContext.nodeMoved

### Description
Notification fired when an [EditNode](../reference.md#object-editnode) has been moved to a new position in the component tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldNode | [EditNode](#type-editnode) | false | — | node that was removed |
| oldParentNode | [EditNode](#type-editnode) | false | — | parent node of the node that was removed |
| newNode | [EditNode](#type-editnode) | false | — | node that was added |
| newParentNode | [EditNode](#type-editnode) | false | — | parent node of the node that was added |
| rootNode | [EditNode](#type-editnode) | false | — | root node of the edit context |

---
## Method: EditContext.addPaletteNodesFromXML

### Description
Recreate [EditNodes](../reference.md#object-editnode) from an XML representation of [PaletteNodes](../reference.md#object-palettenode) (possibly created by calling [EditContext.serializeAllEditNodes](#method-editcontextserializealleditnodes) or [EditContext.serializeEditNodes](#method-editcontextserializeeditnodes).

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| xmlString | [String](#type-string) | false | — | XML string |
| parentNode | [EditNode](#type-editnode) | true | — | parent node (defaults to the root) |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |
| callback | [Function](#type-function) | true | — | Callback to fire after nodes have been added |

### See Also

- [EditContext.serializeAllEditNodes](#method-editcontextserializealleditnodes)
- [EditContext.serializeEditNodes](#method-editcontextserializeeditnodes)

---
## Method: EditContext.removeNodeProperties

### Description
Removes the specified properties from an editNode's serializable "defaults". Note that the [liveObject](EditNode.md#attr-editnodeliveobject) is not updated by this method. To set a property to null (rather than removing it), use [setNodeProperties()](#method-editcontextsetnodeproperties) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to update |
| properties | [Array of String](#type-array-of-string) | false | — | an array of property names to remove |

### See Also

- [EditContext.setNodeProperties](#method-editcontextsetnodeproperties)

---
## Method: EditContext.addFromPaletteNodes

### Description
Add the supplied [PaletteNodes](../reference.md#object-palettenode) to the parentNode, preserving internal references from one supplied PaletteNode to another. This method should be used with an array of possibly inter-related PaletteNodes (for instance, those produced as a result of serialization via [serializeAllEditNodes()](#method-editcontextserializealleditnodes)) rather than calling [addFromPaletteNode()](#method-editcontextaddfrompalettenode) on each individual PaletteNode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNodes | [Array of PaletteNode](#type-array-of-palettenode) | false | — | array of PaletteNodes |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add to (defaults to the root) |

### Returns

`[Array of EditNode](#type-array-of-editnode)` — an array of the EditNodes added to the parentNode

### See Also

- [EditContext.addFromPaletteNode](#method-editcontextaddfrompalettenode)

---
## Method: EditContext.setDefaultPalette

### Description
[Palette](../reference.md#interface-palette) to use when an [EditNode](../reference.md#object-editnode) is being created directly by this EditContext, instead of being created due to a user interaction with a palette (eg dragging from a [TreePalette](../reference.md#class-treepalette), or clicking on [MenuPalette](../reference.md#class-menupalette)).

If no defaultPalette is provided, the EditContext uses an automatically created [HiddenPalette](../reference.md#class-hiddenpalette).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| palette | [Palette](#type-palette) | false | — | the default Palette |

---
## Method: EditContext.selectEditNode

### Description
Select an EditNode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | editNode to select |

---
## Method: EditContext.nodeAdded

### Description
Notification fired when an [EditNode](../reference.md#object-editnode) has been added to the EditContext

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newNode | [EditNode](#type-editnode) | false | — | node that was added |
| parentNode | [EditNode](#type-editnode) | false | — | parent node of the node that was added |
| rootNode | [EditNode](#type-editnode) | false | — | root node of the edit context |

---
## Method: EditContext.isNodeEditingOn

### Description
Returns true if `editNode` is in edit mode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the EditNode |

### Returns

`[boolean](../reference.md#type-boolean)` — true if node is in edit mode

---
## Method: EditContext.setEditProxyProperties

### Description
Update an editNode's [EditProxy](EditProxy.md#class-editproxy) properties. If editProxy has not yet been created, `editProxyProperties` is updated or created instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to update |
| properties | [EditProxy Properties](#type-editproxy-properties) | false | — | the properties to apply |

---
## Method: EditContext.addNode

### Description
Add a new [EditNode](../reference.md#object-editnode) to the EditContext, under the specified parent. If the parentNode is not provided it will be determined from [EditContext.defaultParent](#attr-editcontextdefaultparent).

The EditContext will interrogate the parent and new nodes to determine what field within the parent allows a child of this type, and to find a method to add the newNode's liveObject to the parentNode's liveObject. The new relationship will then be stored in the tree of EditNodes.

For example, when a Tab is dropped on a TabSet, the field TabSet.tabs is discovered as the correct target field via naming conventions, and the method TabSet.addTab() is likewise discovered as the correct method to add a Tab to a TabSet.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newNode | [EditNode](#type-editnode) | false | — | new node to be added |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add the new node under. |
| index | [Integer](../reference_2.md#type-integer) | true | — | index within the parent's children array |
| parentProperty | [String](#type-string) | true | — | the property of the liveParent to which the new node should be added, if not auto-discoverable from the schema |
| skipParentComponentAdd | [Boolean](#type-boolean) | true | — | whether to skip adding the liveObject to the liveParent (default false) |
| forceSingularFieldReplace | [Boolean](#type-boolean) | true | — | whether to replace existing single field node if newNode liveObject is the same (default false) |

### Returns

`[EditNode](#type-editnode)` — newNodenode added

---
## Method: EditContext.serializeEditNodes

### Description
Serialize the provided [EditNodes](../reference.md#object-editnode) to an XML representation of [PaletteNodes](../reference.md#object-palettenode). Note that the EditNodes must have been added to this EditContext. The result can be supplied to [addPaletteNodesFromXML()](#method-editcontextaddpalettenodesfromxml) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of EditNode](#type-array-of-editnode) | false | — | EditNodes to be serialized |
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — an XML representtion of the provided EditNodes

---
## Method: EditContext.pasteEditNodes

### Description
"Pastes" `editNodes` previously captured via [EditContext.copyEditNodes](#method-editcontextcopyeditnodes).

New editNodes will be added as root-level nodes of the [editNodeTree](#method-editcontextgeteditnodetree) unless a `targetEditNode` is passed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetEditNode | [EditNode](#type-editnode) | true | — | — |

---
## Method: EditContext.deselectEditNodes

### Description
Deselect a list of EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNodes | [List of EditNode](#type-list-of-editnode) | false | — | editNodes to deselect |

---
## Method: EditContext.editNodeHasDataSource

### Description
Does the [editNode](../reference.md#object-editnode) have a DataSource assigned?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | editNode to check for a DataSource |

### Returns

`[Boolean](#type-boolean)` — true if the editNode has a DataSource assigned

---
## Method: EditContext.createPaletteNodeTree

### Description
Creates a [Tree](Tree.md#class-tree) from the supplied [PaletteNodes](../reference.md#object-palettenode) preserving internal references from one supplied PaletteNode to another. This method should be used with an array of possibly inter-related PaletteNodes (for instance, those produced as a result of serialization via [serializeAllEditNodes()](#method-editcontextserializealleditnodes)) rather than calling [addFromPaletteNode()](#method-editcontextaddfrompalettenode) on each individual PaletteNode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNodes | [Array of PaletteNode](#type-array-of-palettenode) | false | — | array of PaletteNodes |

### Returns

`[Tree](#type-tree)` — a tree of the PaletteNodes

### See Also

- [EditContext.addFromPaletteNode](#method-editcontextaddfrompalettenode)

---
## Method: EditContext.addPaletteNodesFromJSON

### Description
Recreate [EditNodes](../reference.md#object-editnode) from a JSON representation of [PaletteNodes](../reference.md#object-palettenode) (possibly created by calling [EditContext.serializeAllEditNodesAsJSON](#method-editcontextserializealleditnodesasjson) or [EditContext.serializeEditNodesAsJSON](#method-editcontextserializeeditnodesasjson).

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsonString | [String](#type-string) | false | — | JSON string representing an array of PaletteNodes |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add to (defaults to the root) |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |
| callback | [Function](#type-function) | true | — | Callback to fire after nodes have been added |

### See Also

- [EditContext.addFromPaletteNodes](#method-editcontextaddfrompalettenodes)
- [EditContext.serializeAllEditNodesAsJSON](#method-editcontextserializealleditnodesasjson)
- [EditContext.serializeEditNodesAsJSON](#method-editcontextserializeeditnodesasjson)

---
## Method: EditContext.addFromPaletteNodeTree

### Description
Add the supplied [PaletteNode](../reference.md#object-palettenode) tree to the parentNode, preserving internal references from one supplied PaletteNode to another.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNodeTree | [Tree](#type-tree) | false | — | tree of PaletteNodes |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add to (defaults to the root) |

### Returns

`[Array of EditNode](#type-array-of-editnode)` — an array of the EditNodes added to the parentNode

### See Also

- [EditContext.addFromPaletteNode](#method-editcontextaddfrompalettenode)

---
## Method: EditContext.getNodeProperty

### Description
Returns the specified property from the editNode's serializable "defaults".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to query |
| name | [String](#type-string) | false | — | the property name to query |

### See Also

- [EditContext.setNodeProperties](#method-editcontextsetnodeproperties)

---
## Method: EditContext.selectSingleEditNode

### Description
Select a single EditNode and deselect everything else.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | editNode to select |

---
## Method: EditContext.isEditNodeSelected

### Description
Returns true if the editNode is selected.

### Returns

`[boolean](../reference.md#type-boolean)` — true if editNode is selected; false otherwise

---
## Method: EditContext.convertedNode

### Description
Notification fired when an [EditNode](../reference.md#object-editnode) is converted to a different type when moved from one container to another.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| origNode | [EditNode](#type-editnode) | false | — | node that was being moved |
| newNode | [EditNode](#type-editnode) | false | — | node that was placed into new container |
| parentNode | [EditNode](#type-editnode) | false | — | parent node of the drop |

---
## Method: EditContext.getDefaultPalette

### Description
[Palette](../reference.md#interface-palette) to use when an [EditNode](../reference.md#object-editnode) is being created directly by this EditContext, instead of being created due to a user interaction with a palette (eg dragging from a [TreePalette](../reference.md#class-treepalette), or clicking on [MenuPalette](../reference.md#class-menupalette)).

If no defaultPalette is provided, the EditContext uses an automatically created [HiddenPalette](../reference.md#class-hiddenpalette).

### Returns

`[Palette](#type-palette)` — the default Palette

---
## Method: EditContext.getPaletteNodesFromJS

### Description
Obtain [PaletteNodes](../reference.md#object-palettenode) from a JavaScript source representation.

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsCode | [String](#type-string) | false | — | JavaScript code to eval. |
| callback | [PaletteNodeCallback](#type-palettenodecallback) | false | — | Callback used to return the PaletteNodes |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |

### See Also

- [Callbacks.PaletteNodeCallback](Callbacks.md#method-callbackspalettenodecallback)

---
## Method: EditContext.editMaskClicked

### Description
Executed when the left mouse is clicked (pressed and then released) on any selectable component with [EditProxy.editMask](EditProxy.md#attr-editproxyeditmask) enabled. implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode clicked |
| liveObject | [Object](../reference.md#type-object) | false | — | the object clicked |

---
## Method: EditContext.serializeAllEditNodesAsJSON

### Description
Encode the tree of [EditNodes](../reference.md#object-editnode) to a JSON representation of [PaletteNodes](../reference.md#object-palettenode). The result can be supplied to [addPaletteNodesFromJSON()](#method-editcontextaddpalettenodesfromjson) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — a JSON representation of PaletteNodes which can be used to recreate the tree of EditNodes.

### See Also

- [EditContext.addPaletteNodesFromJSON](#method-editcontextaddpalettenodesfromjson)

---
## Method: EditContext.getEditNodeTree

### Description
Gets the tree of editNodes being edited by this editContext. Standard tree traversal methods can then be used to locate desired editNodes for interaction.

**Note: the returned tree is read-only and must only be modified by calling methods on EditContext like [EditContext.addNode](#method-editcontextaddnode) or [EditContext.setNodeProperties](#method-editcontextsetnodeproperties).**

### Returns

`[Tree](#type-tree)` — the tree of EditNodes

---
## Method: EditContext.selectedEditNodesUpdated

### Description
Called when editMode selection changes. Note this method fires exactly once for any given change.

This event is fired once after selection/deselection has completed. The result is one event per mouse-down event. For a drag selection there will be one event fired when the range is completed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | first selected node, if any |
| editNodeList | [Array of EditNode](#type-array-of-editnode) | false | — | List of nodes that are now selected |

---
## Method: EditContext.getSelectedEditNode

### Description
Returns selected EditNode or first selected EditNode if multiple nodes are selected.

### Returns

`[EditNode](#type-editnode)` — the selected or first edit node

---
## Method: EditContext.editNodeUpdated

### Description
Fires whenever editNode.defaults are modified by setNodeProperties() and/or editProxy features

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | currently editing node |
| editContext | [EditContext](#type-editcontext) | false | — | current context |
| modifiedProperties | [Array of String](#type-array-of-string) | false | — | properties that were modified |

---
## Method: EditContext.serializeAllEditNodes

### Description
Serialize the tree of [EditNodes](../reference.md#object-editnode) to an XML representation of [PaletteNodes](../reference.md#object-palettenode). The result can be supplied to [addPaletteNodesFromXML()](#method-editcontextaddpalettenodesfromxml) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — an XML representation of PaletteNodes which can be used to recreate the tree of EditNodes.

### See Also

- [EditContext.addPaletteNodesFromXML](#method-editcontextaddpalettenodesfromxml)

---
## Method: EditContext.selectAllEditNodes

### Description
Select all EditNodes.

---
## Method: EditContext.addPaletteNodesFromJS

### Description
Add [PaletteNodes](../reference.md#object-palettenode) from a JavaScript source representation.

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsCode | [String](#type-string) | false | — | JavaScript code to eval. |
| parentNode | [EditNode](#type-editnode) | true | — | parent node (defaults to the root) |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |

---
## Method: EditContext.destroyAll

### Description
Removes all [EditNodes](../reference.md#object-editnode) from the EditContext, and calls [destroy()](Canvas.md#method-canvasdestroy) on the [liveObjects](EditNode.md#attr-editnodeliveobject).

---
## Method: EditContext.deselectAllEditNodes

### Description
Deselect all EditNodes.

---
## Method: EditContext.editNodeHasFields

### Description
Does the [editNode](../reference.md#object-editnode) have at least one field assigned?

Note that if this method is called for a component editNode that could have child components rather than fields, it will return `true` if there are any child nodes other than a DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | editNode to check for fields |

### Returns

`[Boolean](#type-boolean)` — true if the editNode has fields or child nodes other than a DataSource

---
## Method: EditContext.removeNode

### Description
Removes [EditNode](../reference.md#object-editnode) from the EditContext. The editNode liveObject is not destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | node to be removed |

---
## Method: EditContext.addPaletteNodeFormItemConstructors

### Description
Add [PaletteNode](../reference.md#object-palettenode) constructors for the specific type of [FormItem](FormItem.md#class-formitem) that will be created to the paletteNodes in the specified tree created by [EditContext.createPaletteNodeTree](#method-editcontextcreatepalettenodetree).

Normally, the specific FormItem is applied from the DataSource and DataBoundComponent at time of use but there are times when having the explicit constructor on the paletteNodes is helpful such as for validation or serialization.

Note that the paletteNodes are updated in place.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodeTree | [Tree](#type-tree) | false | — | tree of PaletteNodes |

---
## Method: EditContext.addFromPaletteNode

### Description
Creates a new EditNode from a PaletteNode, using the [EditContext.defaultPalette](#attr-editcontextdefaultpalette). If you have an array of possibly inter-related PaletteNodes, then you should use [addFromPaletteNodes()](#method-editcontextaddfrompalettenodes) on the array instead, in order to preserve the relationships.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNode | [PaletteNode](#type-palettenode) | false | — | the palette node to use to create the new node |
| parentNode | [EditNode](#type-editnode) | true | — | optional the parent node if the new node should appear under a specific parent |

### Returns

`[EditNode](#type-editnode)` — the EditNode created from the paletteNode

### See Also

- [EditContext.addFromPaletteNodes](#method-editcontextaddfrompalettenodes)

---
