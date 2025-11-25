# Component Containment and Hierarchy

[← Back to API Index](../main.md)

---

## KB Topic: Component Containment and Hierarchy

### Description
Canvas hierarchy in the DOM is defined via [parent](../classes/Canvas.md#attr-canvasparentcanvas) and [child](../classes/Canvas.md#attr-canvaschildren) relationships.

These may be set up explicitly via APIs such as [Canvas.addChild](../classes/Canvas.md#method-canvasaddchild), or may be automatically set up by composite components. For example [TabSets](../classes/TabSet.md#class-tabset) will nest their [panes](../classes/Tab.md#attr-tabpane) inside an appropriate sub component.  
Developers using the [autoChildren](autoChildren.md#kb-topic-autochildren) subsystem may also use the [autoParent](../classes/Canvas.md#attr-canvasautoparent) attribute to specify a target parent.

In addition to parent-child relationships, SmartClient components support [master](../classes/Canvas.md#method-canvasgetmastercanvas)-[peer](../classes/Canvas.md#attr-canvaspeers) relationships. When a canvas is set to be the peer of some other canvas, the master and peer will share the same parent canvas ([reparenting](../classes/Canvas.md#method-canvasaddchild) a master will automatically reparent any peers). Peers will move, resize and redraw with their masters and commonly use [snapTo positioning](../classes/Canvas.md#attr-canvassnapto)

### Related

- [Canvas.addChild](../classes/Canvas.md#method-canvasaddchild)
- [Canvas.removePeer](../classes/Canvas.md#method-canvasremovepeer)
- [Canvas.depeer](../classes/Canvas.md#method-canvasdepeer)
- [Canvas.deparent](../classes/Canvas.md#method-canvasdeparent)
- [Canvas.removeChild](../classes/Canvas.md#method-canvasremovechild)
- [Canvas.addPeer](../classes/Canvas.md#method-canvasaddpeer)
- [Canvas.getParentCanvas](../classes/Canvas.md#method-canvasgetparentcanvas)
- [Canvas.getMasterCanvas](../classes/Canvas.md#method-canvasgetmastercanvas)
- [Canvas.getParentElements](../classes/Canvas.md#method-canvasgetparentelements)
- [Canvas.contains](../classes/Canvas.md#method-canvascontains)
- [Canvas.parentElement](../classes/Canvas.md#attr-canvasparentelement)
- [Canvas.parentCanvas](../classes/Canvas.md#attr-canvasparentcanvas)
- [Canvas.topElement](../classes/Canvas.md#attr-canvastopelement)
- [Canvas.masterElement](../classes/Canvas.md#attr-canvasmasterelement)
- [Canvas.children](../classes/Canvas.md#attr-canvaschildren)
- [Canvas.peers](../classes/Canvas.md#attr-canvaspeers)

---
