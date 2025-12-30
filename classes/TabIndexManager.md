# TabIndexManager Documentation

[← Back to API Index](../reference.md)

---

## Class: TabIndexManager

### Description
Singleton class with static APIs for managing automatically assigned tab order for SmartClient components and other focusable elements.

The TabIndexManager separates the logic required to maintain a sensible tab-order for a page's components from the logic to handle allocation of actual tab index values. It is common to have non-focusable components with an implied position in the page's tab order - for example Layouts containing focusable buttons, or DynamicForms containing focusable items, and this class handles maintaining relative tab order within such groups, and supplying explicit TabIndex values for the items which actually need them.

Entries are registered with the TabIndexManager via the [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget) API. A numeric tab index for each entry will be lazily generated when requested via [TabIndexManager.getTabIndex](#classmethod-tabindexmanagergettabindex). The class provides APIs to modify the position of entries in the tab tree. When a target is registered, a couple of custom callback functions can be provided. The first is a notification method for the tab index being updated (due to, for example, a parent being repositioned and all its children having new tab indices assigned), and can be used to take an appropriate action such as updating the tab index of an element in the DOM. The second callback will be fired when a call to the special [TabIndexManager.focusInTarget](#classmethod-tabindexmanagerfocusintarget) or [TabIndexManager.shiftFocus](#classmethod-tabindexmanagershiftfocus) API requests focus be passed to an entry. This allows a developer to take an appropriate action (such as programmatically focussing in some DOM element).

For standard SmartClient components (focusable [canvases](Canvas.md#class-canvas) and [formItems](FormItem.md#class-formitem)), developers will typically use APIs directly on the widget to customize tab sequence behavior rather than interacting with the TabIndexManager class. See the [tab order overview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview) topic for more information on tab order management for components in SmartClient.  
Developers wishing to embed focusable components into a page which are not SmartClient components (native HTML elements and third party widgets), may use TabIndexManager APIs to do so. This process is described in [customTabElements](../kb_topics/customTabElements.md#kb-topic-including-custom-elements-in-the-tab-order).

---
## ClassMethod: TabIndexManager.getTabIndex

### Description
Returns a tabIndex number for some target ID registered via [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget). Generated tab indices are guaranteed to be in order.

As targets are added to, or moved within the TabIndexManager, their tab index may become invalid. The `tabIndexUpdated` notification will be fired when this occurs, giving developers a way to pick up the new tab index, and assign it to the appropriate DOM element if appropriate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | ID of the target for which you want to get a numeric tabIndex. |

### Returns

`[Integer](../reference_2.md#type-integer)` — returns the numeric tabIndex value for the specified target

---
## ClassMethod: TabIndexManager.focusInTarget

### Description
Request the TabIndexManager shift focus to a registered focus target.

This method does not directly change the focus within the DOM - instead it invokes the `shiftFocusCallback` registered for the specified target if it is marked as `canFocus:true`.

Returns false if the target had no no `shiftFocusCallback`, the `shiftFocusCallback` returned false, or if the target is marked as not `canFocus:true`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | target to shift focus to |

### Returns

`[boolean](../reference.md#type-boolean)` — returns false to indicate failure to shift focus.

---
## ClassMethod: TabIndexManager.showAllocatedTabChain

### Description
Show the current hierarchy of targets passed to [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget) together with current canFocus state and tabIndex (if assigned). Results are output to the developer console.

---
## ClassMethod: TabIndexManager.removeTarget

### Description
Removes a target from this TabIndexManager. Any children of this target will also be removed - developers wishing to preserve children should first call [TabIndexManager.moveTarget](#classmethod-tabindexmanagermovetarget) to move the children out of this parent

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | target to remove |

---
## ClassMethod: TabIndexManager.setCanFocus

### Description
Modifies whether or not some specified target should be treated as focusable and provide a meaningful TabIndex on a call to [TabIndexManager.getTabIndex](#classmethod-tabindexmanagergettabindex).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | target ID |
| canFocus | [boolean](../reference.md#type-boolean) | false | — | new value for canFocus |

---
## ClassMethod: TabIndexManager.shiftFocusWithinGroup

### Description
Method to shift focus to the next registered focusable target within some group. This method will move focus forward or backward, considering only the specified target and any targets within its group (registered as children of the target via [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget) or [TabIndexManager.moveTarget](#classmethod-tabindexmanagermovetarget)).

The second parameter can be passed to specify an explicit starting position to shift focus from. If this is not present, this method will attempt to focus into the group target itself if moving forward (or its last child, if moving backward) and failing that, shift focus from there.

This method does not directly change the focus within the DOM - instead it finds the next target marked as `canFocus:true`, and invokes the `shiftFocusCallback` registered for that target. This callback is expected to take the appropriate action (typically shifting native focus to an element in the DOM), and return true (or return false, if the target could not receieve focus for some reason, in which case we'll find the next `canFocus:true` target and repeat the action there.

Targets with no `shiftFocusCallback` will be skipped entirely in this process.

A return value of false indicates that this method was unable to shift focus to a new target.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetGroup | [String](#type-string) | false | — | ID of registered target. Focus will be shifted within this target and its descendants only. |
| currentTarget | [String](#type-string) | false | — | Optional ID of current focus target within the group focus will be shifted in the specified direction from this node. |
| forward | [boolean](../reference.md#type-boolean) | false | — | should focus move forward to the next focusable target, or backward to the previous focusable target. |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true to indicate focus was successfully shifted, false to indicate this method was unable to change focus.

---
## ClassMethod: TabIndexManager.addTarget

### Description
Register a target to have its tab order position managed by the TabIndexManager.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | Unique ID to associate with a tab position. For a Canvas this would typically be the [Canvas.ID](Canvas.md#attr-canvasid) but any unique string is valid. |
| canFocus | [boolean](../reference.md#type-boolean) | false | — | Is this target directly focusable? Governs whether an explicit tabIndex will be created for this target. This parameter should be passed as `false` for targets which do not require an explicit tabIndex as they are not focusable, or not explicit tab-stops for the user tabbing through the page. They will still have an implicit tab order position which governs where descendants appear, and would be used to generate a tabIndex if canFocus is subsequently updated via [TabIndexManager.setCanFocus](#classmethod-tabindexmanagersetcanfocus). |
| parentID | [String](#type-string) | true | — | For cases where the tab position should be treated part of a group to be moved together, the ID of the parent target containing all members of this group. An example of this would be a Layout managing the tab order of all its members. If present, the passed parentID must already be being managed by this TabIndexManager. May be updated for registered targets via [TabIndexManager.moveTarget](#classmethod-tabindexmanagermovetarget). |
| position | [Integer](../reference_2.md#type-integer) | true | — | Position in the tab-order within the specified parent \[or within top level widgets\]. Omitting this parameter will add the target to the end of the specified parent's tab group. May be updated for registered targets via [TabIndexManager.moveTarget](#classmethod-tabindexmanagermovetarget). |
| tabIndexUpdatedCallback | [TabIndexUpdatedCallback](#type-tabindexupdatedcallback) | true | — | This notification method will be fired when the tabIndex is actually updated, typically due to the target, or some parent of it being re-positioned in the managed Tab order. In some cases tab indices may also be updated to make space for unrelated entries being added to the TabIndexManager. This notification is typically used to update the appropriate element in the DOM to reflect a new tab index. |
| shiftFocusCallback | [ShiftFocusCallback](#type-shiftfocuscallback) | true | — | This notification method will be fired when the special [TabIndexManager.shiftFocus](#classmethod-tabindexmanagershiftfocus) method is called to programmatically move focus through the registered targets (simulating the user tabbing through elements in the tab index chain). The implementation should attempt to update the UI state by focusing in the appropriate UI for this target -- typically this means putting browser focus into a DOM element, and return true to indicate success.  
Returning false indicates the element is currently not focusable (disabled, masked, etc), and cause the TabIndexManager to call the shiftFocusCallback on the next registered entry (skipping over this entry).  
If this method was not supplied, calls to [TabIndexManager.shiftFocus](#classmethod-tabindexmanagershiftfocus) will simply skip this entry. |

---
## ClassMethod: TabIndexManager.setAlwaysUseExplicitFocusNavigation

### Description
Should [TabIndexManager.useExplicitFocusNavigation](#classmethod-tabindexmanageruseexplicitfocusnavigation) to always return true?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [boolean](../reference.md#type-boolean) | false | — | whether we should always use explicit focus navigation |

---
## ClassMethod: TabIndexManager.useExplicitFocusNavigation

### Description
Should focus navigation be achieved by explicitly calling the TabIndexManager [shiftFocus()](#classmethod-tabindexmanagershiftfocus) method for the specified node?

Developers integrating custom focusable element's into a SmartClient based application can use this method to ensure the elements in question interact correctly with [click masks](Canvas.md#method-canvasshowclickmask) and [grid editing](ListGrid_1.md#attr-listgridcanedit). See the [tab order overview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview) topic for more information on integrating custom focusable UI into a SmartClient application.

This method will return true if the [TabIndexManager.setAlwaysUseExplicitFocusNavigation](#classmethod-tabindexmanagersetalwaysuseexplicitfocusnavigation) has been set to true (typically because a [click mask](Canvas.md#method-canvasshowclickmask) is showing), or if the entry or some ancestor has been marked as [useExplicitFocusNavigation:true](#classmethod-tabindexmanagersetuseexplicitfocusnavigation). Note that this is the case for entries registered under a canvas with [Canvas.alwaysManageFocusNavigation](Canvas.md#attr-canvasalwaysmanagefocusnavigation) set to true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | TabIndexManager registered target ID |

### Returns

`[boolean](../reference.md#type-boolean)` — true if explicit focus navigation should be used

---
## ClassMethod: TabIndexManager.suppressCallbacks

### Description
Temporarily suppress firing any tabIndexChanged callback passed into [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget) for the specified targets should their tab index change.

This is useful for cases where a developer is managing a list of items and wants to avoid any potential for multiple notifications until the entire list has been managed

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targets | [Array of String](#type-array-of-string) | false | — | targets for which callbacks should be suppressed |

### See Also

- [TabIndexManager.resumeCallbacks](#classmethod-tabindexmanagerresumecallbacks)

---
## ClassMethod: TabIndexManager.moveTarget

### Description
Move a target to the newly specified parent / position. This method may change the calculated tab index for this entry, or other canFocus:true entries which already have a calculated tabIndex. The registered tabIndexUpdated notification method will for for any entry where this occurs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | ID of the target to move |
| parentID | [String](#type-string) | true | — | ID of the new parent (if null, will move to the top level) |
| position | [Integer](../reference_2.md#type-integer) | true | — | Position within the specified parent. If null will be the last entry. |

---
## ClassMethod: TabIndexManager.shiftFocusAfterGroup

### Description
Method to shift focus to the next registered focusable target beyond some registered target and any targets registered as children within its group via [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget) or [TabIndexManager.moveTarget](#classmethod-tabindexmanagermovetarget).

This method does not directly change the focus within the DOM - instead it finds the next target marked as `canFocus:true`, and invokes the `shiftFocusCallback` registered for that target. This callback is expected to take the appropriate action (typically shifting native focus to an element in the DOM), and return true (or return false, if the target could not receieve focus for some reason, in which case we'll find the next `canFocus:true` target and repeat the action there.

Targets with no `shiftFocusCallback` will be skipped entirely in this process.

A return value of false indicates that this method was unable to shift focus to a new target.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetGroup | [String](#type-string) | false | — | ID of registered target. Focus will be shifted to the next registered focusable element, skipping this group and its descendants. |
| forward | [boolean](../reference.md#type-boolean) | false | — | should focus move forward to the next focusable target, or backward to the previous focusable target. |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true to indicate focus was successfully shifted, false to indicate this method was unable to change focus.

---
## ClassMethod: TabIndexManager.moveTargets

### Description
Move a list of targets to the newly specified parent / position. This method may change the calculated tab index for these entries, or other canFocus:true entries which already have a calculated tabIndex. The registered tabIndexUpdated notification method will for for any entry where this occurs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| IDs | [Array of String](#type-array-of-string) | false | — | IDs of the targets to move |
| parentID | [String](#type-string) | true | — | ID of the new parent (if null, will move to the top level) |
| position | [Integer](../reference_2.md#type-integer) | true | — | Position within the specified parent. If null will be added at the end |

---
## ClassMethod: TabIndexManager.setUseExplicitFocusNavigation

### Description
Mark the specified node (and its descendents) as using explicit focus navigation rather than relying on native browser Tab event handling behavior. See [TabIndexManager.useExplicitFocusNavigation](#classmethod-tabindexmanageruseexplicitfocusnavigation) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | registered TabIndexManager target |
| newValue | [boolean](../reference.md#type-boolean) | false | — | should explicit focus navigation be used for the specified target and its descendents |

---
## ClassMethod: TabIndexManager.getAllocatedTabChain

### Description
Get a report of the current hierarchy of targets passed to [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget) together with current canFocus state and tabIndex (if assigned).

### Returns

`[String](#type-string)` — —

---
## ClassMethod: TabIndexManager.shiftFocus

### Description
Method to shift focus to the next registered focusable target.

This method does not directly change the focus within the DOM - instead it finds the next target marked as `canFocus:true`, and invokes the `shiftFocusCallback` registered for that target. This callback is expected to take the appropriate action (typically shifting native focus to an element in the DOM), and return true (or return false, if the target could not receieve focus for some reason, in which case we'll find the next `canFocus:true` target and repeat the action there.

Targets with no `shiftFocusCallback` will be skipped entirely in this process.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | current focus target. If null, focus will be applied to the first focusable target (or the last if the `forward` parameter is false). |
| forward | [boolean](../reference.md#type-boolean) | false | — | should focus move forward to the next focusable target, or backward to the previous focusable target. |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true to indicate focus was successfully shifted, false to indicate this method was unable to change focus.

---
## ClassMethod: TabIndexManager.resumeCallbacks

### Description
Resume firing any callbacks suppressed by [TabIndexManager.suppressCallbacks](#classmethod-tabindexmanagersuppresscallbacks)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targets | [Array of String](#type-array-of-string) | false | — | targets for which callbacks should be resumed |

### See Also

- [TabIndexManager.suppressCallbacks](#classmethod-tabindexmanagersuppresscallbacks)

---
## ClassMethod: TabIndexManager.hasTarget

### Description
Has the specified target been added to this TabIndexManager via [TabIndexManager.addTarget](#classmethod-tabindexmanageraddtarget)?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | Unique ID to test for. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if we are managing the tab index for the specified target

---
