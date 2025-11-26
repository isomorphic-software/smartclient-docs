# ClassFactory Documentation

[← Back to API Index](../reference.md)

---

## ClassMethod: ClassFactory.overwriteClass

### Description
Intentionally clobber an existing SmartClient Class, if it already exists. Works identically to [ClassFactory.defineClass](#classmethod-classfactorydefineclass), except that no warning is logged to the console.

---
## ClassMethod: ClassFactory.defineClass

### Description
Create a new SmartClient class, which can then be used to create instances of this object type, via [Class.create](Class.md#classmethod-classcreate).

The new Class is returned by `defineClass`, is available as `isc._ClassName_` and is also available in global scope if not in [portal mode](../reference.md#object-isc). Typically, [Class.addProperties](Class.md#classmethod-classaddproperties) is then called to establish different defaults in the new class, or to add methods. For example:

```
    isc.defineClass("MyListGrid", "ListGrid").addProperties({
        headerHeight : 40, // change default for listGrid.headerHeight

        // override listGrid.recordClick
        recordClick : function (viewer, record) { 
           isc.say(record.description);
        }
    })
    isc.MyListGrid.create(); // create an instance of the new class
 
```

See also [Super()](Class.md#method-classsuper) for calling superclass methods.

NOTE: `isc.defineClass()` also creates a new function `[class:isA](../reference.md#object-isa)._ClassName()_` object for identifying instances of this Class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | Name for the new class. |
| superClass | [Class](#type-class) | true | — | Optional SuperClass Class object or name |

### Returns

`[Class](#type-class)` — Returns the new Class object.

---
## ClassMethod: ClassFactory.getClass

### Description
Given a class name, return a pointer to the Class object for that class

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | name of a class |

### Returns

`[Class](#type-class)` — Class object, or null if not found

---
## ClassMethod: ClassFactory.newInstance

### Description
Given the name of a class, create an instance of that class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | Name of a class. (ClassObject) Actual class object to use. |
| props | [Object](../reference.md#type-object) | true | — | Properties to apply to the instance. |
| props2 | [Object](../reference.md#type-object) | true | — | More properties to apply to the instance. |
| props3 | [Object](../reference.md#type-object) | true | — | Yet more properties to apply to the instance. |

### Returns

`[Class](#type-class)` — Pointer to the new class.

---
