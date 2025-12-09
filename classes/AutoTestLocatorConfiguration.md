# AutoTestLocatorConfiguration Documentation

[← Back to API Index](../reference.md)

---

## Attr: AutoTestLocatorConfiguration.searchSegmentsIncludeHidden

### Description
When generating locators with [search segments](#attr-autotestlocatorconfigurationusesearchsegments), should the generation logic always consider hidden components as well as visible components to determine whether the search segment will uniquely resolve?

Setting this property to true ensures that, even for visible components, search segments will be guaranteed to resolve uniquely when considering both visible and hidden components on the page. Any search segments in the generated locator will include a marker to indicate that both hidden and visible widgets should be considered when resolving the locator back to a target via [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement), [AutoTest.getObject](AutoTest.md#classmethod-autotestgetobject) and related methods.

Note that this setting has no impact on locators being generated for components that are currently hidden. Any search segments for hidden components will always consider uniqueness among all components (hidden and visible), and include the marker to ensure that they are considered when resolving the locator back to an object.

See the [AutoTestLocator overview](../reference_2.md#type-autotestlocator) for more information about search segments in AutoTestLocators

**Flags**: IRA

---
## Attr: AutoTestLocatorConfiguration.useMinimalFallbackAttributes

### Description
Should generated locators omit fallback locator attributes when generating segments that identify components or other objects by attribute values?

See the [AutoTestLocator overview](../reference_2.md#type-autotestlocator) for details of locator fallback attributes.

**Flags**: IR

---
## Attr: AutoTestLocatorConfiguration.useIDsAsLocators

### Description
May a simple widget ID with no other content be returned from [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator)?

If true, when a locator is requested for a component, and that component has an explicitly specified [Canvas.ID](Canvas.md#attr-canvasid), the ID will be returned as the entire locator.

This only applies when the target of the locator is the component itself or its handle. If the target is a child, or an interior DOM element that requires additional locator segments to identify, a standard multi-segment locator will be generated.

See the [AutoTestLocator overview](../reference_2.md#type-autotestlocator) for more information on locators.

**Flags**: IR

---
## Attr: AutoTestLocatorConfiguration.useSearchSegments

### Description
Should generated locators include search segments (as detailed in the [AutoTestLocator overview](../reference_2.md#type-autotestlocator)) to identify components with [defining property values](Canvas.md#method-canvasgetdefiningpropertyname)?

See also [AutoTestLocatorConfiguration.searchSegmentsIncludeHidden](#attr-autotestlocatorconfigurationsearchsegmentsincludehidden)

**Flags**: IR

---
## Attr: AutoTestLocatorConfiguration.useCompactFallbackSyntax

### Description
This setting controls whether locator segments that identify components or other objects by attribute values use a compact or verbose syntax.

See the [AutoTestLocator overview](../reference_2.md#type-autotestlocator) for details of locator attributes.

**Flags**: IR

---
