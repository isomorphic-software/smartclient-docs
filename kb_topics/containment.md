# Component Containment and Hierarchy

[← Back to API Index](../reference.md)

---

## KB Topic: Component Containment and Hierarchy

### Description
Canvas hierarchy in the DOM is defined via [parent](../classes/Canvas_1.md#attr-canvasparentcanvas) and [child](../classes/Canvas_1.md#attr-canvaschildren) relationships.

These may be set up explicitly via APIs such as [Canvas.addChild](../classes/Canvas_1.md#method-canvasaddchild), or may be automatically set up by composite components. For example [TabSets](../classes/TabSet.md#class-tabset) will nest their [panes](../classes/Tab.md#attr-tabpane) inside an appropriate sub component.  
Developers using the [autoChildren](autoChildren.md#kb-topic-autochildren) subsystem may also use the [autoParent](../classes/Canvas_1.md#attr-canvasautoparent) attribute to specify a target parent.

In addition to parent-child relationships, SmartClient components support [master](../classes/Canvas_1.md#method-canvasgetmastercanvas)-[peer](../classes/Canvas_1.md#attr-canvaspeers) relationships. When a canvas is set to be the peer of some other canvas, the master and peer will share the same parent canvas ([reparenting](../classes/Canvas_1.md#method-canvasaddchild) a master will automatically reparent any peers). Peers will move, resize and redraw with their masters and commonly use [snapTo positioning](../classes/Canvas_1.md#attr-canvassnapto)

### Related

- [Canvas.addChild](../classes/Canvas_1.md#method-canvasaddchild)
- [Canvas.removePeer](../classes/Canvas_1.md#method-canvasremovepeer)
- [Canvas.depeer](../classes/Canvas_1.md#method-canvasdepeer)
- [Canvas.deparent](../classes/Canvas_2.md#method-canvasdeparent)
- [Canvas.removeChild](../classes/Canvas_2.md#method-canvasremovechild)
- [Canvas.addPeer](../classes/Canvas_1.md#method-canvasaddpeer)
- [Canvas.getParentCanvas](../classes/Canvas_1.md#method-canvasgetparentcanvas)
- [Canvas.getMasterCanvas](../classes/Canvas_1.md#method-canvasgetmastercanvas)
- [Canvas.getParentElements](../classes/Canvas_1.md#method-canvasgetparentelements)
- [Canvas.contains](../classes/Canvas_1.md#method-canvascontains)
- [Canvas.parentElement](../classes/Canvas_1.md#attr-canvasparentelement)
- [Canvas.parentCanvas](../classes/Canvas_1.md#attr-canvasparentcanvas)
- [Canvas.topElement](../classes/Canvas_1.md#attr-canvastopelement)
- [Canvas.masterElement](../classes/Canvas_1.md#attr-canvasmasterelement)
- [Canvas.children](../classes/Canvas_1.md#attr-canvaschildren)
- [Canvas.peers](../classes/Canvas_1.md#attr-canvaspeers)

---
