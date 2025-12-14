# ButtonItem Documentation

[← Back to API Index](../reference.md)

---

## Class: ButtonItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
FormItem for adding a Button to a form.

---
## Attr: ButtonItem.enableWhen

### Description
Criteria to be evaluated to determine whether this item should be enabled. This property is incompatible with [readOnlyWhen](FormItem.md#attr-formitemreadonlywhen) and any setting you provide for the latter will be ignored if this property is set.

Criteria are evaluated against the ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','form\\'s current values')} as well as the current [rule context](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated every time form values or the rule context changes, whether by end user action or by programmatic calls.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

Note: A ButtonItem using enableWhen must have a [name](FormItem.md#attr-formitemname) defined. [shouldSaveValue](CanvasItem.md#attr-canvasitemshouldsavevalue) can be set to `false` to prevent the field from storing its value into the form's values.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: ButtonItem.button

### Description
This item is an autoChild generated [Canvas](Canvas.md#class-canvas) displayed by the ButtonItem and is an instance of [Button](Button.md#class-button) by defaut, cuztomizeable via the [ButtonItem.buttonConstructor](#attr-buttonitembuttonconstructor) attribute.

**Flags**: R

---
## Attr: ButtonItem.buttonProperties

### Description
Custom Properties to apply to our button item.

**Flags**: IRA

---
## Attr: ButtonItem.endRow

### Description
These items are in a row by themselves by default

### Groups

- formLayout

**Flags**: IRW

---
## Attr: ButtonItem.autoFit

### Description
Should the button auto fit to its title. Maps to [Button.autoFit](Button.md#attr-buttonautofit) attribute. Note that if an explicit width or height is specified for this item, it will be respected, disabling autoFit behavior

**Flags**: IR

---
## Attr: ButtonItem.height

### Description
By default buttonItems are sized to match their content (see [ButtonItem.autoFit](#attr-buttonitemautofit)). Specifying an explicit size for the button will disable this behavior.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ButtonItem.baseStyle

### Description
Optional `baseStyle` will be applied to the button.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ButtonItem.buttonTitleAlign

### Description
The (horizontal) alignment of this button's title.

### Groups

- positioning

**Flags**: IRW

---
## Attr: ButtonItem.showFocusedAsOver

### Description
This property governs whether [showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is true on the automatically created [Button](Button.md#class-button) for this item.

**Flags**: IRW

---
## Attr: ButtonItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ButtonItem.buttonConstructor

### Description
Constructor class for the button.

**Flags**: IRA

---
## Attr: ButtonItem.icon

### Description
Optional icon image to display on the button for this item. See [Button.icon](Button.md#attr-buttonicon).

### Groups

- appearance

**Flags**: IR

---
## Attr: ButtonItem.readOnlyDisplay

### Description
If this item is [read-only](FormItem.md#method-formitemgetcanedit), how should this item be displayed to the user? If set, overrides the form-level [DynamicForm.readOnlyDisplay](DynamicForm.md#attr-dynamicformreadonlydisplay) default.

### Groups

- appearance
- readOnly

### See Also

- [DynamicForm.readOnlyDisplay](DynamicForm.md#attr-dynamicformreadonlydisplay)

**Flags**: IRW

---
## Attr: ButtonItem.startRow

### Description
These items are in a row by themselves by default

### Groups

- formLayout

**Flags**: IRW

---
## Attr: ButtonItem.showTitle

### Description
Buttons do not show a title by default.

### Groups

- appearance

**Flags**: IRW

---
## Method: ButtonItem.setShowFocusedAsOver

### Description
Sets showFocusedAsOver.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showFocusedAsOver | [boolean](../reference.md#type-boolean) | false | — | — |

---
## Method: ButtonItem.click

### Description
Called when a ButtonItem is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |

### Returns

`[boolean](../reference.md#type-boolean)` — Return false to cancel the click event. This will prevent the event from bubbling up, suppressing [click](Canvas.md#method-canvasclick) on the form containing this item.

### Groups

- eventHandling

---
## Method: ButtonItem.setButtonTitleAlign

### Description
Sets the (horizontal) alignment of this button's title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| alignment | [Alignment](../reference.md#type-alignment) | false | — | new title alignment |

### Groups

- positioning

---
## Method: ButtonItem.setTitle

### Description
Set the title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [String](#type-string) | false | — | new title |

### Groups

- appearance

---
