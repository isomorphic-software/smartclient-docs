# EditTree Documentation

[← Back to API Index](../main.md)

---

## Class: EditTree

*Inherits from:* [TreeGrid](TreeGrid.md#class-treegrid)

### Description
A TreeGrid that allows drag and drop creation and manipulation of a tree of objects described by DataSources.

Nodes can be added via drag and drop from a [Palette](../main.md#interface-palette) or may be programmatically added via [addNode()](EditContext.md#method-editcontextaddnode). Nodes may be dragged within the tree to reparent them.

Eligibility to be dropped on any given node is determined by inspecting the DataSource of the parent node. Drop is allowed only if the parent schema has a field which accepts the type of the dropped node.

On successful drop, the newly created component will be added to the parent node under the detected field. Array fields, declared by setting `dataSourceField.multiple:true`, are supported.

An EditTree is initialized by setting [EditTree.rootComponent](#attr-edittreerootcomponent) or [EditTree.editContext](#attr-edittreeeditcontext). EditTree.data (the Tree instance) should never be directly set or looked at.

EditTree automatically creates an [EditContext](EditContext.md#class-editcontext) and provides several APIs and settings that are passthroughs to the underlying EditContext for convenience.

### Groups

- devTools

---
## Attr: EditTree.rootComponent

### Description
Root of data to edit. Must contain the "type" property, with the name of a valid [schema](DataSource.md#class-datasource) or nothing will be able to be dropped on this EditContext. A "liveObject" property representing the rootComponent is also suggested. Otherwise, a live object will be created from the palette node.

Can be retrieved at any time. Use [EditTree.getRootEditNode](#method-edittreegetrooteditnode) to retrieve the [EditNode](../main.md#object-editnode) created from the rootComponent.

### Groups

- devTools

**Flags**: IR

---
## Attr: EditTree.canShowFilterEditor

### Description
Option to show filter editor is disabled for editTree

**Flags**: IRA

---
## Attr: EditTree.defaultPalette

### Description
[Palette](../main.md#interface-palette) to use when an [EditNode](../main.md#object-editnode) is being created directly by this EditContext, instead of being created due to a user interaction with a palette (eg dragging from a [TreePalette](../main.md#class-treepalette), or clicking on [MenuPalette](../main.md#class-menupalette)).

If no defaultPalette is provided, the EditContext uses an automatically created [HiddenPalette](../main.md#class-hiddenpalette).

**Flags**: IR

---
## Attr: EditTree.persistCoordinates

### Description
When enabled, changes to a [liveObject](EditNode.md#attr-editnodeliveobject)'s position and size will be persisted to their [EditNodes](../main.md#object-editnode) by default. This applies to both programmatic calls and user interaction (drag reposition or drag resize).

This feature can be disabled by either setting this property or [EditProxy.persistCoordinates](EditProxy.md#attr-editproxypersistcoordinates) to `false`. This property affects all nodes within the EditContext whereas the latter property affects children of a single node.

In some use-cases, like Reify, coordinates should not be persisted except when a component explicitly enables this feature. By setting this property to `null` no component will persist coordinates of children unless `EditProxy.persistCoordinates` is explicitly set to `true`.

**Flags**: IR

---
## Attr: EditTree.useCopyPasteShortcuts

### Description
If set, auto-enables [EditProxy.useCopyPasteShortcuts](EditProxy.md#attr-editproxyusecopypasteshortcuts) on the [EditProxy](EditProxy.md#class-editproxy) for the [root editNode](#method-edittreegetrooteditnode). This works whether there is currently a root editNode or one is added later.

**Flags**: IR

---
## Attr: EditTree.canDragGroup

### Description
Should the group selection box shown when [canGroupSelect](EditContext.md#attr-editcontextcangroupselect) is true allow dragging the group as a whole?

Treated as `true` if not set and [canGroupSelect](EditContext.md#attr-editcontextcangroupselect) is true.

**Flags**: IR

---
## Attr: EditTree.showSelectedLabel

### Description
Should the selection outline show a label for selected components? A component may also be highlighted with the selection outline and label to indicate the target of a drop. To suppress showing a label at any time set this property to `false`.

To suppress labels during selection but still show them when targeted for a drop, see [EditContext.showSelectedLabelOnSelect](EditContext.md#attr-editcontextshowselectedlabelonselect).

NOTE: A selected component label is only supported when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "outlineEdges".

**Flags**: IR

---
## Attr: EditTree.selectedLabelBackgroundColor

### Description
The background color for the selection outline label. The default is defined on [SelectionOutline](SelectionOutline.md#class-selectionoutline).

This value is applied as a default to [EditProxy.selectedLabelBackgroundColor](EditProxy.md#attr-editproxyselectedlabelbackgroundcolor).

NOTE: A selected component label is only supported when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is "outlineEdges".

### See Also

- [EditContext.showSelectedLabel](EditContext.md#attr-editcontextshowselectedlabel)

**Flags**: IR

---
## Attr: EditTree.hideGroupBorderOnDrag

### Description
Should the group selection box shown when [canGroupSelect](EditContext.md#attr-editcontextcangroupselect) is true be hidden during drag?

Treated as `true` if not explicitly set to false.

**Flags**: IR

---
## Attr: EditTree.selectedBorder

### Description
Set the CSS border to be applied to the selection outline of the selected components. This property is used when [EditProxy.selectedAppearance](EditProxy.md#attr-editproxyselectedappearance) is `outlineMask` or `outlineEdges`.

This value is applied as a default to [EditProxy.selectedBorder](EditProxy.md#attr-editproxyselectedborder).

**Flags**: IR

---
## Attr: EditTree.allowNestedDrops

### Description
Controls whether components can be dropped into other components which support child components.

When enabled, during a drop interaction in which a [PaletteNode](../main.md#object-palettenode) or [EditNode](../main.md#object-editnode) is the drop data, the [Component Schema](../kb_topics/componentSchema.md#kb-topic-component-schema) of the current candidate drop target is inspected to see whether that parent allows children of the type being dropped. If it does, the drop will result in a call to [EditTree.addNode](#method-edittreeaddnode) for a paletteNode or for an existing [EditNode](../main.md#object-editnode) in the same tree.

Specific components can disable nested drops by explicitly setting [EditProxy.allowNestedDrops](EditProxy.md#attr-editproxyallownesteddrops) to false.

This mode is enabled by default unless explicitly disabled by setting this property to false.

**Flags**: IR

---
## Attr: EditTree.autoEditNewNodes

### Description
New nodes added to the editContext are automatically placed into edit mode if the new node's parent is in edit mode. To suppress this action set `autoEditNewNodes` to false.

**Flags**: IR

---
## Attr: EditTree.extraPalettes

### Description
Additional [Palettes](../main.md#interface-palette) to consult for metadata when deserializing [Edit Nodes](../main.md#object-editnode). Note that the [defaultPalette](#attr-edittreedefaultpalette) is always consulted and need not be provided again here.

**Flags**: IR

---
## Attr: EditTree.canGroupSelect

### Description
Should a group selection outline covering the outermost bounding boxes of all selected components be shown in this container?

Treated as `true` if not set and hoop selection is enabled (see [EditProxy.canSelectChildren](EditProxy.md#attr-editproxycanselectchildren) and [selectionType](EditContext.md#attr-editcontextselectiontype).

**Flags**: IR

---
## Attr: EditTree.editContext

### Description
The [EditContext](EditContext.md#class-editcontext) managed by this EditTree. If not set an instance will be automatically created.

**Flags**: IR

---
## Attr: EditTree.canSaveSearches

### Description
Option to save searches is disabled for editTree

**Flags**: IRA

---
## Method: EditTree.makePaletteNode

### Description
Creates a [PaletteNode](../main.md#object-palettenode) from an [EditNode](../main.md#object-editnode) in this context's [editNodeTree](#method-edittreegeteditnodetree).

This essentially creates a new [PaletteNode](../main.md#object-palettenode) with the [EditNode.defaults](EditNode.md#attr-editnodedefaults) from the passed `editNode`. The returned `paletteNode` could then be used with [EditContext.addFromPaletteNode](EditContext.md#method-editcontextaddfrompalettenode) to effectively create a copy of the original editNode - specifically a new editNode with a new [EditNode.liveObject](EditNode.md#attr-editnodeliveobject) created from the same defaults.

However note that `makePaletteNode()` does not copy descendant nodes - use [EditTree.makePaletteNodeTree](#method-edittreemakepalettenodetree) for that.

May return null if the passed editNode cannot validly by transformed into a paletteNode, for example if [EditNode.canDuplicate](EditNode.md#attr-editnodecanduplicate) was set false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to use to make a paletteNode |

### Returns

`[PaletteNode](#type-palettenode)` — paletteNode derived from the editNode or null

---
## Method: EditTree.getPaletteNodesFromXML

### Description
Obtain [PaletteNodes](../main.md#object-palettenode) from an XML representation, but do not add them to the EditContext.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| xmlString | [String](#type-string) | false | — | XML string |
| callback | [PaletteNodeCallback](#type-palettenodecallback) | false | — | Callback used to return the PaletteNodes |

### See Also

- [Callbacks.PaletteNodeCallback](Callbacks.md#method-callbackspalettenodecallback)
- [EditTree.serializeAllEditNodes](#method-edittreeserializealleditnodes)
- [EditTree.serializeEditNodes](#method-edittreeserializeeditnodes)

---
## Method: EditTree.destroyAll

### Description
Removes all [EditNodes](../main.md#object-editnode) from the EditContext, and calls [destroy()](Canvas.md#method-canvasdestroy) on the [liveObjects](EditNode.md#attr-editnodeliveobject).

---
## Method: EditTree.getRootEditNode

### Description
Returns the root [EditNode](../main.md#object-editnode) of the EditContext typically created from [EditTree.rootComponent](#attr-edittreerootcomponent).

### Returns

`[EditNode](#type-editnode)` — the root EditNode

---
## Method: EditTree.addPaletteNodesFromJSON

### Description
Recreate [EditNodes](../main.md#object-editnode) from a JSON representation of [PaletteNodes](../main.md#object-palettenode) (possibly created by calling [EditTree.serializeAllEditNodesAsJSON](#method-edittreeserializealleditnodesasjson) or [EditTree.serializeEditNodesAsJSON](#method-edittreeserializeeditnodesasjson).

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsonString | [String](#type-string) | false | — | JSON string representing an array of PaletteNodes |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add to (defaults to the root) |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |
| callback | [Function](#type-function) | true | — | Callback to fire after nodes have been added |

### See Also

- [EditTree.addFromPaletteNodes](#method-edittreeaddfrompalettenodes)
- [EditTree.serializeAllEditNodesAsJSON](#method-edittreeserializealleditnodesasjson)
- [EditTree.serializeEditNodesAsJSON](#method-edittreeserializeeditnodesasjson)

---
## Method: EditTree.makeEditNode

### Description
Creates and returns an EditNode using the [EditTree.defaultPalette](#attr-edittreedefaultpalette). Does not add the newly created EditNode to an EditContext.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNode | [PaletteNode](#type-palettenode) | false | — | the palette node to use to create the new node |

### Returns

`[EditNode](#type-editnode)` — the EditNode created from the paletteNode

---
## Method: EditTree.getDefaultPalette

### Description
[Palette](../main.md#interface-palette) to use when an [EditNode](../main.md#object-editnode) is being created directly by this EditContext, instead of being created due to a user interaction with a palette (eg dragging from a [TreePalette](../main.md#class-treepalette), or clicking on [MenuPalette](../main.md#class-menupalette)).

If no defaultPalette is provided, the EditContext uses an automatically created [HiddenPalette](../main.md#class-hiddenpalette).

### Returns

`[Palette](#type-palette)` — the default Palette

---
## Method: EditTree.removeAll

### Description
Removes all [EditNodes](../main.md#object-editnode) from the EditContext, but does not destroy the [liveObjects](EditNode.md#attr-editnodeliveobject).

---
## Method: EditTree.reorderNode

### Description
Moves an [EditNode](../main.md#object-editnode) from one child index to another in the EditContext under the specified parent.

No changes are made to the live objects.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| parentNode | [EditNode](#type-editnode) | false | — | parent to reorder child nodes |
| index | [Integer](../main_2.md#type-integer) | false | — | index within the parent's children array to be moved |
| moveToIndex | [Integer](../main_2.md#type-integer) | false | — | index within the parent's children array at which to place moved node |

---
## Method: EditTree.copyEditNodes

### Description
Copies the passed editNode or editNodes to an internal "clipboard" space, for later application via [EditTree.pasteEditNodes](#method-edittreepasteeditnodes).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode)|[Array of EditNode](#type-array-of-editnode) | false | — | — |

---
## Method: EditTree.addFromPaletteNodes

### Description
Add the supplied [PaletteNodes](../main.md#object-palettenode) to the parentNode, preserving internal references from one supplied PaletteNode to another. This method should be used with an array of possibly inter-related PaletteNodes (for instance, those produced as a result of serialization via [serializeAllEditNodes()](#method-edittreeserializealleditnodes)) rather than calling [addFromPaletteNode()](#method-edittreeaddfrompalettenode) on each individual PaletteNode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNodes | [Array of PaletteNode](#type-array-of-palettenode) | false | — | array of PaletteNodes |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add to (defaults to the root) |

### Returns

`[Array of EditNode](#type-array-of-editnode)` — an array of the EditNodes added to the parentNode

### See Also

- [EditTree.addFromPaletteNode](#method-edittreeaddfrompalettenode)

---
## Method: EditTree.getEditContext

### Description
Returns the [EditContext](EditContext.md#class-editcontext) instance managed by the EditTree.

### Returns

`[EditContext](#type-editcontext)` — the EditContext instance

---
## Method: EditTree.addNode

### Description
Add a new [EditNode](../main.md#object-editnode) to the EditContext, under the specified parent. If the parentNode is not provided it will be determined from [EditContext.defaultParent](EditContext.md#attr-editcontextdefaultparent).

The EditContext will interrogate the parent and new nodes to determine what field within the parent allows a child of this type, and to find a method to add the newNode's liveObject to the parentNode's liveObject. The new relationship will then be stored in the tree of EditNodes.

For example, when a Tab is dropped on a TabSet, the field TabSet.tabs is discovered as the correct target field via naming conventions, and the method TabSet.addTab() is likewise discovered as the correct method to add a Tab to a TabSet.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newNode | [EditNode](#type-editnode) | false | — | new node to be added |
| parentNode | [EditNode](#type-editnode) | true | — | parent to add the new node under. |
| index | [Integer](../main_2.md#type-integer) | true | — | index within the parent's children array |
| parentProperty | [String](#type-string) | true | — | the property of the liveParent to which the new node should be added, if not auto-discoverable from the schema |
| skipParentComponentAdd | [Boolean](#type-boolean) | true | — | whether to skip adding the liveObject to the liveParent (default false) |
| forceSingularFieldReplace | [Boolean](#type-boolean) | true | — | whether to replace existing single field node if newNode liveObject is the same (default false) |

### Returns

`[EditNode](#type-editnode)` — newNodenode added

---
## Method: EditTree.makePaletteNodeTree

### Description
Creates a [Tree](Tree.md#class-tree) of [PaletteNodes](../main.md#object-palettenode) from an [EditNode](../main.md#object-editnode) in this context's [editNodeTree](#method-edittreegeteditnodetree), by using [EditTree.makePaletteNode](#method-edittreemakepalettenode) on the passed `EditNode` and its descendents within the [editNodeTree](EditContext.md#method-editcontextgeteditnodetree).

The root node of the returned [Tree](Tree.md#class-tree) will be a PaletteNode derived from the passed `EditNode`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | root editNode to make Tree of PaletteNodes from |
| removeAutoIDs | [Boolean](#type-boolean) | false | — | should ID and autoID defaults be removed? |

### Returns

`[Tree](#type-tree)` — a Tree of paletteNodes or null

---
## Method: EditTree.enableEditing

### Description
Enable edit mode for an [EditNode](../main.md#object-editnode). This is a shortcut for calling [Canvas.setEditMode](Canvas.md#method-canvasseteditmode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the EditNode on which to enable editing |

### See Also

- [Canvas.setEditMode](Canvas.md#method-canvasseteditmode)
- [EditTree.isNodeEditingOn](#method-edittreeisnodeeditingon)

---
## Method: EditTree.pasteEditNodes

### Description
"Pastes" `editNodes` previously captured via [EditTree.copyEditNodes](#method-edittreecopyeditnodes).

New editNodes will be added as root-level nodes of the [editNodeTree](#method-edittreegeteditnodetree) unless a `targetEditNode` is passed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetEditNode | [EditNode](#type-editnode) | true | — | — |

---
## Method: EditTree.isNodeEditingOn

### Description
Returns true if `editNode` is in edit mode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the EditNode |

### Returns

`[boolean](../main.md#type-boolean)` — true if node is in edit mode

---
## Method: EditTree.serializeEditNodes

### Description
Serialize the provided [EditNodes](../main.md#object-editnode) to an XML representation of [PaletteNodes](../main.md#object-palettenode). Note that the EditNodes must have been added to this EditContext. The result can be supplied to [addPaletteNodesFromXML()](#method-edittreeaddpalettenodesfromxml) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of EditNode](#type-array-of-editnode) | false | — | EditNodes to be serialized |
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — an XML representtion of the provided EditNodes

---
## Method: EditTree.getNodeProperty

### Description
Returns the specified property from the editNode's serializable "defaults".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to query |
| name | [String](#type-string) | false | — | the property name to query |

### See Also

- [EditTree.setNodeProperties](#method-edittreesetnodeproperties)

---
## Method: EditTree.removeNodeProperties

### Description
Removes the specified properties from an editNode's serializable "defaults". Note that the [liveObject](EditNode.md#attr-editnodeliveobject) is not updated by this method. To set a property to null (rather than removing it), use [setNodeProperties()](#method-edittreesetnodeproperties) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to update |
| properties | [Array of String](#type-array-of-string) | false | — | an array of property names to remove |

### See Also

- [EditTree.setNodeProperties](#method-edittreesetnodeproperties)

---
## Method: EditTree.setNodeProperties

### Description
Update an editNode's serializable "defaults" with the supplied properties. If you wish to remove a property from the defaults (rather than setting it to null), then use [removeNodeProperties()](#method-edittreeremovenodeproperties) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the editNode to update |
| properties | [Canvas Properties](#type-canvas-properties) | false | — | the properties to apply |
| skipLiveObjectUpdate | [Boolean](#type-boolean) | true | — | whether to skip updating the [liveObject](EditNode.md#attr-editnodeliveobject), e.g. if you have already updated the liveObject |

### See Also

- [EditTree.removeNodeProperties](#method-edittreeremovenodeproperties)
- [EditTree.getNodeProperty](#method-edittreegetnodeproperty)

---
## Method: EditTree.serializeAllEditNodes

### Description
Serialize the tree of [EditNodes](../main.md#object-editnode) to an XML representation of [PaletteNodes](../main.md#object-palettenode). The result can be supplied to [addPaletteNodesFromXML()](#method-edittreeaddpalettenodesfromxml) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — an XML representation of PaletteNodes which can be used to recreate the tree of EditNodes.

### See Also

- [EditTree.addPaletteNodesFromXML](#method-edittreeaddpalettenodesfromxml)

---
## Method: EditTree.getPaletteNodesFromJS

### Description
Obtain [PaletteNodes](../main.md#object-palettenode) from a JavaScript source representation.

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
## Method: EditTree.getEditNodeTree

### Description
Gets the tree of editNodes being edited by this editContext. Standard tree traversal methods can then be used to locate desired editNodes for interaction.

**Note: the returned tree is read-only and must only be modified by calling methods on EditContext like [EditContext.addNode](EditContext.md#method-editcontextaddnode) or [EditContext.setNodeProperties](EditContext.md#method-editcontextsetnodeproperties).**

### Returns

`[Tree](#type-tree)` — the tree of EditNodes

---
## Method: EditTree.addPaletteNodesFromXML

### Description
Recreate [EditNodes](../main.md#object-editnode) from an XML representation of [PaletteNodes](../main.md#object-palettenode) (possibly created by calling [EditTree.serializeAllEditNodes](#method-edittreeserializealleditnodes) or [EditTree.serializeEditNodes](#method-edittreeserializeeditnodes).

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| xmlString | [String](#type-string) | false | — | XML string |
| parentNode | [EditNode](#type-editnode) | true | — | parent node (defaults to the root) |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |
| callback | [Function](#type-function) | true | — | Callback to fire after nodes have been added |

### See Also

- [EditTree.serializeAllEditNodes](#method-edittreeserializealleditnodes)
- [EditTree.serializeEditNodes](#method-edittreeserializeeditnodes)

---
## Method: EditTree.setDefaultPalette

### Description
[Palette](../main.md#interface-palette) to use when an [EditNode](../main.md#object-editnode) is being created directly by this EditContext, instead of being created due to a user interaction with a palette (eg dragging from a [TreePalette](../main.md#class-treepalette), or clicking on [MenuPalette](../main.md#class-menupalette)).

If no defaultPalette is provided, the EditContext uses an automatically created [HiddenPalette](../main.md#class-hiddenpalette).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| palette | [Palette](#type-palette) | false | — | the default Palette |

---
## Method: EditTree.addFromPaletteNode

### Description
Creates a new EditNode from a PaletteNode, using the [EditTree.defaultPalette](#attr-edittreedefaultpalette). If you have an array of possibly inter-related PaletteNodes, then you should use [addFromPaletteNodes()](#method-edittreeaddfrompalettenodes) on the array instead, in order to preserve the relationships.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNode | [PaletteNode](#type-palettenode) | false | — | the palette node to use to create the new node |
| parentNode | [EditNode](#type-editnode) | true | — | optional the parent node if the new node should appear under a specific parent |

### Returns

`[EditNode](#type-editnode)` — the EditNode created from the paletteNode

### See Also

- [EditTree.addFromPaletteNodes](#method-edittreeaddfrompalettenodes)

---
## Method: EditTree.addPaletteNodesFromJS

### Description
Add [PaletteNodes](../main.md#object-palettenode) from a JavaScript source representation.

By default, components that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](RPCManager.md#classattr-rpcmanagerall_globals) for the `globals` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsCode | [String](#type-string) | false | — | JavaScript code to eval. |
| parentNode | [EditNode](#type-editnode) | true | — | parent node (defaults to the root) |
| globals | [Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs |

---
## Method: EditTree.serializeEditNodesAsJSON

### Description
Serialize the provided [EditNodes](../main.md#object-editnode) to a JSON representation of [PaletteNodes](../main.md#object-palettenode). Note that the EditNodes must have been added to this EditContext. The result can be supplied to [addPaletteNodesFromJSON()](#method-edittreeaddpalettenodesfromjson) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of EditNode](#type-array-of-editnode) | false | — | EditNodes to be serialized |
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — a JSON representtion of the provided EditNodes

---
## Method: EditTree.removeNode

### Description
Removes [EditNode](../main.md#object-editnode) from the EditContext. The editNode liveObject is not destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | node to be removed |

---
## Method: EditTree.serializeAllEditNodesAsJSON

### Description
Encode the tree of [EditNodes](../main.md#object-editnode) to a JSON representation of [PaletteNodes](../main.md#object-palettenode). The result can be supplied to [addPaletteNodesFromJSON()](#method-edittreeaddpalettenodesfromjson) to recreate the EditNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [SerializationSettings](#type-serializationsettings) | true | — | Additional serialization settings |

### Returns

`[String](#type-string)` — a JSON representation of PaletteNodes which can be used to recreate the tree of EditNodes.

### See Also

- [EditTree.addPaletteNodesFromJSON](#method-edittreeaddpalettenodesfromjson)

---
