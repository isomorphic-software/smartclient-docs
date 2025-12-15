# TypeScript Support

[← Back to API Index](../reference.md)

---

## KB Topic: TypeScript Support

### Description
Isomorphic ships a TypeScript descriptor file that provides code completion and inline documentation with modern IDEs. Modern versions of Eclipse, Visual Studio, IntelliJ and other IDEs can detect this file for you, or you may choose to add explicit descriptor references in a special comment at the top of your own .ts file. For example:
```
 /// <reference path="path/to/isomorphic/system/development/smartclient.d.ts"/>
 
```
As you can see above, the descriptor file resides in the isomorphic/system/development directory and is called smartclient.d.ts. You can copy this file to another location if you prefer (it is fully self contained), but note that new versions of SmartClient will ship with an up-to-date version of this file.

Some things to keep in mind:

*   This support generally works with .ts and .js files with IDEs that support descriptor references like the above.
*   The goal is to provide autocomplete, inline docs, and spelling/type checks for your code, not every TypeScript feature. This means, for example, that you generally cannot extends Isomorphic's classes using the typescript 'extends' syntax. Instead, you should use the standard [isc.defineClass](../classes/isc.md#staticmethod-iscdefineclass) call to create new class definitions. Isomorphic actually recommends using JavaScript to interact with SmartClient, negating the need for transpilation and allowing you to debug exactly what you've written.
*   There is specialized support for the instantiation [Class.create](../classes/Class.md#classmethod-classcreate) method. Generally, with SmartClient, you can pass as many object literals as you want to this method. The TypeScript descriptor currently supports only 2. The first one is a type-checked property block that supports only the methods and properties declared on the class you are attempting to create (or any of its superclasses or implemented interfaces). The second block does no type checking. The goal here is to make it easy for you to use auto-complete, type checking, and spell checking when you intend to reference actual API methods and properties, but to still allow you to pass arbitrary properties and custom methods that you may be using in your specific instance of the class (via that second constructor block).  
      
    For example:  
    ```
     isc.ListGrid.create({
         // this block will be type-checked and auto-complete enabled
    
         // the "false" value will be flagged as an error becuse a boolean, not a string is expected
         autoDraw: "false",
    
         // valid, no error
         width: 100, 
    
         // the typo in the property name "height" will be flagged as an error
         heght: 100 
     },{
         // this block will not be validated in any way
         myCustomMethod: function () { },
         myFoo: "bar"
     });
     
    ```
    
*   Using the static [_Class_.getById()](../classes/Canvas.md#classmethod-canvasgetbyid) methods allow developers to retrieve instances of specific classes by their [global ID](../classes/Canvas.md#attr-canvasid) in a type-aware manner. IDEs with TypeScript support can then offer appropriate auto-completion, type checking and documentation for attributes and methods on the returned object.

---
