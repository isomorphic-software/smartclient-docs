# Safe Skinning

[← Back to API Index](../reference.md)

---

## KB Topic: Safe Skinning

### Description
The skinning mechanism is extremely powerful and gives you the ability to change internal functionality of components. While this is useful for workarounds, you should think through any properties you override, considering what will happen with future versions of SmartClient, where the defaults may change or be expanded.

The following kinds of overrides are generally very safe:

*   Change [styleName](../classes/Canvas.md#attr-canvasstylename) or [baseStyle](../classes/Button.md#attr-buttonbasestyle) to provide a custom CSS style or series of styles
*   Change a media path such as the [src](../classes/Img.md#attr-imgsrc) of the [Window.minimizeButton](../classes/Window.md#attr-windowminimizebutton).
*   Change the size of any part of the UI that has a fixed pixel size, such as the height and width of the [Window.minimizeButton](../classes/Window.md#attr-windowminimizebutton), especially when this is done to match the size of media you have created
*   Set properties such as [Button.showRollOver](../classes/Button.md#attr-buttonshowrollover) that cause a component to visually react to more or fewer UI states (disabled, over, down, etc)

The following should be very carefully considered:

*   Adding custom behaviors by passing in event handlers such as (eg [showContextMenu()](../classes/Canvas.md#method-canvasshowcontextmenu)). If future versions of the component add more functionality, you may prevent new features from functioning, cause them to function only partially, or break.
    
    If you want to ensure that you do not break new functionality added in future SmartClient versions, be sure to call [Super()](../classes/Class.md#method-classsuper) for methods you override, and do not prevent events from bubbling.
    
    If you want to ensure that **only** your custom behavior is used if a future version of a SmartClient component adds functionality, override all methods involved in the interaction, even if your methods do nothing. For example, for a custom drop interaction, override dropOver, dropMove, dropOut and drop, even if you do nothing on dropMove(). Then, do not call Super() if there is no superclass behavior required for the interaction you've implemented. Also, for any event handlers (such as drop()) return false if you consider your code to have completely handled the event (no parent component should react).
    

The following are not recommended:

*   Providing a global [ID](../classes/Canvas.md#attr-canvasid) to a subcomponent (only works once).
*   Overriding [Canvas.backgroundColor](../classes/Canvas.md#attr-canvasbackgroundcolor), [border](../classes/Canvas.md#attr-canvasborder), [margin](../classes/Canvas.md#attr-canvasmargin), [padding](../classes/Canvas.md#attr-canvaspadding), or in general any single attribute otherwise controlled by CSS. Future SmartClient versions may change the base CSS style, rendering your single-property customization senseless. Change the entire CSS style via [styleName](../classes/Canvas.md#attr-canvasstylename) instead.

---
